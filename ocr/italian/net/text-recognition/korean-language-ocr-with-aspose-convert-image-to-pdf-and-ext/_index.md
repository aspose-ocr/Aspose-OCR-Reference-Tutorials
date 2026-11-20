---
category: general
date: 2026-05-28
description: Tutorial OCR per lingua coreana con Aspose in C#. Scopri come caricare
  un'immagine dallo stream, estrarre il testo semplice, convertire l'immagine in PDF
  ed esportare un PDF ricercabile.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: it
og_description: OCR della lingua coreana in C# con Aspose. Guida passo‑passo per caricare
  l'immagine dallo stream, estrarre il testo semplice, convertire l'immagine in PDF
  ed esportare un PDF ricercabile.
og_title: OCR per lingua coreana – Converti immagine in PDF ed estrai testo (Guida
  C#)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'OCR della lingua coreana con Aspose: Converti immagine in PDF ed estrai testo
  in C#'
url: /it/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR della lingua coreana con Aspose: Converti immagine in PDF ed estrai testo in C#

Ti sei mai chiesto come eseguire **Korean Language OCR** su un'immagine senza inviare nulla al cloud? Non sei l'unico. Che tu stia digitalizzando segnali stradali, elaborando ricevute o costruendo un indice di ricerca multilingue, la capacità di riconoscere i caratteri coreani localmente può farti risparmiare tempo, denaro e problemi di privacy.

In questo tutorial percorreremo un esempio completo e eseguibile che mostra come **load image from stream**, **extract plain text**, **convert image to PDF** e infine **export searchable PDF**—tutto con Aspose.OCR e poche righe di C#. Nessun servizio esterno, nessuna magia nascosta—solo puro codice .NET che puoi inserire in qualsiasi applicazione console.

## Cosa otterrai

- Un programma console funzionante che legge un file JPEG tramite uno stream di file.  
- Testo coreano estratto come stringhe Unicode plain.  
- Un report JSON dettagliato dell'esecuzione OCR per debug o analisi.  
- Un PDF ricercabile che puoi aprire in qualsiasi lettore PDF e selezionare effettivamente le parole coreane.  

**Prerequisiti**  
- .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.7+).  
- Pacchetto NuGet Aspose.OCR per .NET installato (`Install-Package Aspose.OCR`).  
- Una cartella che contiene `korean_sign.jpg` e una posizione scrivibile per i file di output.  

Se hai già tutto pronto, ottimo—mettiamoci al lavoro.

## Passo 1: Inizializza il motore OCR per la lingua coreana

La prima cosa di cui hai bisogno è un'istanza di `OcrEngine`. Abilitare la GPU (se ne possiedi una) accelera notevolmente il riconoscimento, e disattivare il download automatico delle risorse costringe la libreria a utilizzare i language pack offline che fornisci.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Perché è importante:**  
> *GPU acceleration* può ridurre il tempo di elaborazione da secondi a millisecondi per grandi lotti. Impostare `AutomaticResourceDownload` su `false` garantisce che la demo funzioni offline—un requisito cruciale per molti ambienti aziendali.

## Passo 2: Carica immagine dallo stream

Leggere l'immagine tramite uno stream ti offre flessibilità: puoi prelevare file dal disco, da condivisioni di rete o anche da blob memorizzati in cache. Qui apriamo un file JPEG locale, ma lo stesso schema funziona per qualsiasi `Stream`.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Consiglio professionale:** Se mai dovessi elaborare immagini caricate tramite un'API web, basta sostituire `File.OpenRead` con `IFormFile.OpenReadStream()` in ingresso—il resto rimane identico.

## Passo 3: Scegli la lingua coreana e applica filtri di pre‑elaborazione

Aspose.OCR supporta una serie di passaggi di pre‑elaborazione che puliscono l'immagine prima del riconoscimento. Per i cartelli coreani, la correzione di inclinazione (deskew) e la riduzione del rumore (denoise) sono di solito sufficienti.

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **Cosa succede dietro le quinte?**  
> Il filtro `Deskew` raddrizza il testo ruotato, mentre `Denoise` rimuove il rumore che può confondere il classificatore di caratteri. Saltare questi passaggi porta spesso a output incomprensibili, specialmente su foto a bassa risoluzione.

## Passo 4: Estrai testo plain in modo asincrono

Ora arriva il momento della verità—chiedere al motore di riconoscere i caratteri e restituirci una stringa pulita. Usare `RecognizeAsync` mantiene l'interfaccia reattiva se lo integri in un'app desktop o web.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

Quando esegui il programma, dovresti vedere qualcosa del genere:

```
OCR complete. Extracted text:
서울시청
```

> **Perché asincrono?**  
> L'OCR può essere intensivo per la CPU. L'esecuzione asincrona impedisce al thread di bloccarsi, il che è particolarmente utile in ASP.NET Core dove la carenza di thread è una preoccupazione reale.

## Passo 5: Ottieni un risultato di riconoscimento dettagliato e salva come JSON

A volte ti serve più della semplice stringa grezza—potresti voler i punteggi di confidenza, i riquadri di delimitazione o i dati dell'immagine originale. Il metodo `RecognizeDetailed` restituisce un oggetto `RecognitionResult` che può essere serializzato in JSON per analisi successive.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

Aprendo `korean_ocr.json` vedrai una struttura simile a:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **Quando usarlo?**  
> Se stai costruendo un indice di ricerca, i valori di confidenza ti permettono di filtrare i risultati di bassa qualità. Se devi evidenziare il testo in un'interfaccia, i riquadri di delimitazione sono la tua mappa.

## Passo 6: Converti immagine in PDF ed esporta PDF ricercabile

Aspose rende il passaggio da raster a vettoriale senza sforzo. Impostando `OutputFormat` su `SearchablePdf`, la libreria incorpora l'immagine originale e sovrappone uno strato di testo invisibile contenente l'output OCR. Il PDF risultante può essere cercato, copiato e indicizzato come qualsiasi PDF nativo.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

Apri `korean_searchable.pdf` in Adobe Reader o in qualsiasi visualizzatore PDF, premi **Ctrl+F**, digita una parola coreana e osserva come il documento salti esattamente al punto corrispondente. Questa è la potenza di un PDF ricercabile.

> **Suggerimento extra:** Se ti serve solo un PDF visivo senza lo strato di testo nascosto, imposta `OutputFormat` su `Pdf` invece.

## Esempio completo funzionante

Di seguito trovi il programma completo—copia, incolla, sostituisci `YOUR_DIRECTORY` con un percorso reale e premi **F5**.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Output atteso della console

```
OCR complete. Extracted text:
서울시청
```

E troverai tre nuovi file accanto all'immagine di origine:

- `korean_ocr.json` – dati completi del riconoscimento.  
- `korean_searchable.pdf` – un PDF ricercabile.  
- (opzionale) eventuali log intermedi che decidi di aggiungere.

## Domande comuni e casi limite

**E se non ho una GPU?**  
Imposta `EnableGpu = false`; il fallback su CPU è perfettamente adeguato per piccoli lotti.

**Posso elaborare più immagini in un'unica esecuzione?**  
Assolutamente. Avvolgi la logica principale in un ciclo `foreach (var file in Directory.GetFiles(...))` e riassegna `ocrEngine.Image` ad ogni iterazione.

**Come gestire altre lingue insieme al coreano?**  
Aspose.OCR ti consente di impostare `Language = Language.AutoDetect` o combinare lingue con l'operatore OR bitwise (ad esempio, `Language.Korean | Language.English`).

**E se la confidenza dell'OCR è bassa?**  
Ispeziona `detailedResult.Pages[0].Words` e filtra le voci con `Confidence < 0.7`. Puoi anche modificare i filtri di pre‑elaborazione—prova ad aggiungere `PreprocessFilter.ContrastEnhancement`.

## Conclusioni

Hai appena visto come eseguire **Korean Language OCR** end‑to‑end, da **loading image from stream** a **extract plain text**, poi **convert image to PDF** e infine **export searchable PDF**. L'approccio è modulare, così puoi sostituire la sorgente dell'immagine, cambiare il formato di output o collegare il JSON a qualsiasi pipeline successiva.

Cosa segue

## Tutorial correlati

- [Estrai testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Riconosci testo da immagine con Aspose OCR per più lingue](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Estrai testo da immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}