---
category: general
date: 2026-02-28
description: Crea PDF ricercabile in C# combinando le immagini verticalmente. Scopri
  come impilare le immagini verticalmente e convertire le pagine PDF scansionate con
  Aspose OCR.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: it
og_description: Crea PDF ricercabile in C# combinando le immagini verticalmente. Questa
  guida mostra come impilare le immagini verticalmente e convertire le pagine scansionate
  in PDF usando Aspose OCR.
og_title: Crea PDF Ricercabile in C# – Unisci Immagini Verticalmente
tags:
- Aspose OCR
- C#
- PDF generation
title: Crea PDF Ricercabile in C# – Combina le Immagini Verticalmente
url: /it/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF Ricercabile in C# – Combina Immagini Verticalmente

Hai mai avuto bisogno di **creare PDF ricercabile** da una manciata di PNG scansionati ma non sapevi da dove cominciare? Non sei solo. In molti progetti di automazione dei documenti il punto dolente più grande è trasformare una pila di file immagine in un unico PDF ordinato e ricercabile che puoi indicizzare e condividere.  

In questo tutorial percorreremo un esempio completo, pronto‑all’uso, che ti mostra **come impilare le immagini verticalmente**, **combinare le immagini verticalmente**, e infine **convertire le pagine scansionate in PDF** in un unico documento ricercabile usando il motore accelerato da GPU di Aspose.OCR. Alla fine avrai un programma autonomo che potrai inserire in qualsiasi soluzione .NET.

> **Cosa imparerai**
> - Inizializzare un motore OCR con supporto GPU.
> - Elaborare un batch di immagini in parallelo.
> - **Combinare le immagini verticalmente** per simulare una scansione multipagina.
> - Esportare un PDF ricercabile e un report JSON dettagliato per analisi successive.

## Prerequisiti

- .NET 6+ (il codice si compila con .NET 6, .NET 7 o .NET 8)
- Pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Una macchina con GPU abilitata se vuoi mantenere l'impostazione `ProcessingMode.Gpu` (il fallback CPU funziona comunque)
- Una cartella con alcuni file PNG/JPEG scansionati (la demo utilizza `page1.png`, `page2.png`, `page3.png`)

Nessun servizio esterno, nessun file di configurazione nascosto—solo puro C#.

## Passo 1 – Configura il motore OCR per **creare PDF ricercabile**

Per prima cosa creiamo un `OcrEngine`, attiviamo l'accelerazione GPU, scegliamo l'inglese come lingua e aggiungiamo un paio di filtri di pre‑elaborazione. Questi filtri migliorano l'accuratezza raddrizzando le pagine inclinate (`DeskewFilter`) e rimuovendo il rumore (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Perché è importante:** Il motore OCR si occupa del lavoro pesante di riconoscere il testo. Abilitare `ProcessingMode.Gpu` può dimezzare il tempo di riconoscimento su una scheda grafica moderna, mentre i filtri riducono gli artefatti di scansione comuni che altrimenti produrrebbero output confuso.

## Passo 2 – Configura un Processore Batch per **convertire le pagine scansionate in PDF** in modo efficiente

Elaborare ogni pagina una alla volta va bene per un paio di immagini, ma i progetti reali spesso coinvolgono decine o centinaia di pagine. `OcrBatchProcessor` di Aspose.OCR ci permette di eseguire i riconoscimenti in parallelo, accelerando notevolmente il passaggio **convertire le pagine scansionate in PDF**.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Consiglio professionale:** Se sei su una macchina solo CPU, imposta `ProcessingMode = ProcessingMode.Cpu`. Il processore batch rispetterà comunque `MaxDegreeOfParallelism`, così potrai regolarlo per evitare di sovraccaricare il computer.

## Passo 3 – Esegui l'OCR sul batch e raccogli i risultati

Ora riconosciamo effettivamente il testo. Il metodo `Recognize` restituisce un elenco di oggetti `OcrResult`, ognuno dei quali contiene sia l'immagine originale sia il testo estratto.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

A questo punto hai tutto il necessario per **creare PDF ricercabile**: le immagini (ancora in memoria) e gli strati di testo associati.

## Passo 4 – **Combinare le immagini verticalmente** e generare il PDF ricercabile

La maggior parte dei documenti scansionati sono PDF multipagina, quindi dobbiamo unire le singole immagini delle pagine in un'unica immagine alta che rispecchi una pila fisica. Aspose.OCR fornisce `Image.CombineVertical` proprio per questo scopo.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

Il file risultante (`combined_searchable.pdf`) contiene testo selezionabile e ricercabile sotto ogni immagine della pagina—esattamente ciò di cui hai bisogno per **creare PDF ricercabile** da fonti scansionate.

![Esempio di creazione PDF ricercabile](/images/create-searchable-pdf.png "esempio di creazione pdf ricercabile")

*Testo alternativo dell'immagine: esempio di creazione pdf ricercabile che mostra un PDF combinato con testo ricercabile.*

**Perché impilare verticalmente?** Molte librerie OCR trattano ogni immagine come una pagina separata. Impilandole, manteniamo l'ordine delle pagine del PDF intatto pur sfruttando un'unica passata OCR per l'intero documento.

## Passo 5 – Esporta JSON dettagliato per la prima pagina (ottimo per flussi di lavoro successivi)

A volte hai bisogno di più di un PDF; forse vuoi inviare i dati OCR a un database o a una pipeline di machine‑learning. Aspose.OCR ti consente di serializzare ogni `OcrResult` in JSON, preservando le bounding box, i punteggi di confidenza e altro.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Snippet JSON previsto (troncato):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

Ora puoi inviare questo JSON a qualsiasi sistema successivo—che tu stia indicizzando il testo in Elasticsearch o fornendolo a una dashboard di analisi personalizzata.

---

## Come **impilare le immagini verticalmente** – Un rapido riepilogo

Se ti chiedi **come impilare le immagini verticalmente** senza Aspose, potresti usare `System.Drawing` per creare un nuovo bitmap e disegnare ogni pagina una dopo l'altra. Tuttavia, `Image.CombineVertical` integrato in Aspose gestisce DPI, formato pixel e gestione della memoria per te, rendendolo la scelta più affidabile per il codice di produzione.

### Alternativa: Usare `System.Drawing` (solo per curiosità)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

L'approccio manuale funziona, ma perdi la comodità della gestione automatica del DPI e la possibilità di inviare direttamente il risultato a `RecognizeToPdf`. Rimani su `CombineVertical` a meno che tu non abbia un requisito molto specifico.

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **Errori Out‑of‑memory** durante l'elaborazione di decine di scansioni ad alta risoluzione | Ogni immagine rimane in memoria fino a quando il PDF non viene scritto | Disporre degli oggetti `Image` non appena hai finito (`using` blocks) o ridimensionare le immagini prima di combinarle |
| **Testo spazzatura** dopo l'OCR | Scansioni inclinate o basso contrasto | Mantieni `DeskewFilter` e `DenoiseFilter`; considera di aggiungere `ContrastFilter` se necessario |
| **Mancanza del livello ricercabile** | Usato `Recognize` invece di `RecognizeToPdf` | Assicurati di chiamare `ocrEngine.RecognizeToPdf` sull'immagine combinata |
| **Il fallback GPU fallisce** su macchine senza driver adeguati | `ProcessingMode.Gpu` genera un'eccezione | Avvolgi la creazione del motore in try/catch e passa a `ProcessingMode.Cpu` |

## Prossimi passi – Estendere il flusso di lavoro

Ora che sai come **creare PDF ricercabile**, potresti voler:

- **Elaborare in batch intere cartelle** usando `Directory.GetFiles` e un ciclo `foreach`.
- **Aggiungere filigrane** a ogni pagina prima di combinare (usa `ImageProcessor` da Aspose.Imaging).
- **Dividere il PDF ricercabile in pagine individuali** se in seguito ti servono PDF per pagina (`PdfDocument.Split` da Aspose.PDF).
- **Integrare con Azure Blob Storage** per prelevare le immagini dal cloud e caricare nuovamente il PDF finale.

Tutte queste estensioni coinvolgono naturalmente gli stessi concetti fondamentali: configurazione OCR, gestione delle immagini e esportazione PDF.

---

## Conclusione

Abbiamo coperto tutto ciò di cui hai bisogno per **creare PDF ricercabile** da una collezione di immagini scansionate in C#. Inizializzando un `OcrEngine` abilitato alla GPU, eseguendo un batch parallelo con `OcrBatchProcessor`, **combinando le immagini verticalmente** e infine chiamando `RecognizeToPdf`, ottieni un documento ordinato e ricercabile pronto per l'archiviazione o l'indicizzazione. L'esportazione JSON aggiuntiva ti offre piena visibilità sui risultati OCR, aprendo porte a analisi o flussi di lavoro personalizzati.

Provalo, sperimenta con filtri diversi e osserva la tua pipeline di automazione dei documenti diventare molto più fluida. Se incontri qualche strano problema, lascia un commento—buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}