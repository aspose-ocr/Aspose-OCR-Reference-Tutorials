---
category: general
date: 2026-04-26
description: Crea PDF ricercabile da un'immagine scannerizzata usando Aspose OCR in
  C#. Scopri come convertire l'immagine scannerizzata, estrarre il testo e generare
  rapidamente un PDF ricercabile.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: it
og_description: Crea PDF ricercabile da un'immagine scannerizzata usando Aspose OCR.
  Codice C# passo‑passo per convertire, estrarre il testo e generare un PDF ricercabile.
og_title: Crea PDF Ricercabile da Immagine Scansionata – Guida C#
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: Crea PDF ricercabile da immagine scannerizzata – Guida C#
url: /it/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF Ricercabile da Immagine Scansionata – Guida C#

Hai mai avuto bisogno di **creare PDF ricercabili** da contratti cartacei, ricevute o vecchi archivi? Non sei solo—la maggior parte degli sviluppatori si imbatte in questo ostacolo quando un cliente consegna una pila di scansioni TIFF e si aspetta un PDF ricercabile come risultato finale.  

In questo tutorial ti mostreremo esattamente **come fare OCR su un documento** e trasformare un'immagine scansionata in un **PDF ricercabile** con Aspose OCR per .NET. Alla fine sarai in grado di **convertire immagini scansionate**, **estrarre testo da immagini** e gestire anche TIFF a più pagine senza alcuna difficoltà.

## Cosa Ti Serve

* .NET 6.0 o versioni successive (l'API funziona con .NET Core, .NET Framework e .NET 5+).  
* Una licenza valida di Aspose OCR oppure sei soddisfatto del watermark di valutazione.  
* Il pacchetto NuGet `Aspose.OCR` installato (`dotnet add package Aspose.OCR`).  
* Un file TIFF di esempio (ad es., `contract_scan.tif`) che desideri trasformare in un PDF ricercabile.

Tutto qui—nessuna libreria aggiuntiva, nessuna configurazione complicata. Pronto? Iniziamo.

![Create searchable PDF example](create-searchable-pdf.png "create searchable pdf example")

## Passo 1 – Inizializza il Motore OCR (Crea PDF Ricercabile)

Prima di tutto: ti serve un'istanza di `OcrEngine`. Questo oggetto è il cavallo di battaglia che legge il bitmap, identifica i caratteri e ti restituisce il testo.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**Perché impostare la lingua?**  
Se lo lasci al valore predefinito, Aspose proverà tutti i pacchetti linguistici, rallentando il processo. Specificare `Language.Latin` indica al motore di concentrarsi sull'alfabeto latino, fornendo un aumento di velocità e risultati più accurati per contratti in lingua inglese.

## Passo 2 – Carica la Tua Immagine Scansionata (Converti Immagine Scansionata)

Ora forniamo al motore l'immagine da elaborare. Aspose può leggere un percorso file, uno stream o anche un `byte[]`. Per semplicità useremo `ImageStream.FromFile`.

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

Se in futuro avrai bisogno di **convertire TIFF in PDF**, tieni presente che i TIFF a più pagine vengono gestiti automaticamente—ogni frame diventa una pagina PDF separata.

## Passo 3 – Esegui l'OCR e Ottieni il Testo (Estrai Testo da Immagine)

Eseguire l'OCR è semplice come chiamare `Recognize`. Il motore restituirà un `RecognitionResult` che contiene il testo semplice, i punteggi di confidenza e le informazioni di layout.

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Consiglio professionale:** Se ti serve solo il testo (senza PDF), puoi fermarti qui e scrivere `extractedText` in un file `.txt`. Ma nella maggior parte dei casi il nostro obiettivo è un PDF ricercabile, quindi continuiamo.

## Passo 4 – Salva come PDF Ricercabile (Crea PDF Ricercabile)

Aspose rende il passaggio finale banale: basta chiamare `Save` con `SaveFormat.PdfSearchable`. Internamente la libreria incorpora il testo estratto come livello invisibile mantenendo l'aspetto originale dell'immagine.

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

Quando apri `contract_searchable.pdf` in qualsiasi visualizzatore PDF, potrai selezionare, copiare e cercare il testo—esattamente ciò che un cliente si aspetta da un “PDF ricercabile”.

## Gestione dei TIFF a più pagine (Converti TIFF in PDF)

Se il tuo file di origine contiene diverse pagine, Aspose tratterà automaticamente ogni frame come una pagina separata. Non sono necessari loop aggiuntivi. Tuttavia, potresti voler controllare DPI o qualità dell'immagine per ogni pagina:

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

Dopo aver impostato queste opzioni, ripeti il **Passo 2** per ogni frame, oppure punta semplicemente `ImageStream.FromFile` al TIFF a più pagine e lascia che Aspose faccia il lavoro pesante.

## Problemi Comuni e Come Risolverli

| Sintomo | Probabile Causa | Soluzione |
|---------|----------------|-----------|
| Il testo è confuso o mancante | Lingua impostata errata | Imposta `ocrEngine.Language` al pacchetto linguistico corretto (ad es., `Language.German`). |
| Il PDF è enorme (10 MB per una scansione a pagina singola) | La compressione immagine predefinita è bassa | Regola `ocrEngine.ImageProcessingOptions.Compression` a `Jpeg` e imposta un valore di `Quality` ragionevole (0‑100). |
| L'OCR è molto lento | Uso del rilevamento lingua predefinito `Auto` | Imposta esplicitamente la lingua prevista. |
| Nessuno strato ricercabile appare | Salvato con `SaveFormat.Pdf` invece di `PdfSearchable` | Usa `PdfSearchable`. |

## Esempio Completo End‑to‑End

Mettendo tutto insieme, ecco un'app console pronta per l'esecuzione che puoi copiare‑incollare in Visual Studio:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Cosa vedrai:**  
* Una finestra della console che stampa un frammento del testo OCRizzato.  
* Un file `contract_searchable.pdf` accanto al tuo TIFF originale. Aprilo, premi **Ctrl + F** e cerca qualsiasi parola presente nella scansione originale—voilà, funziona.

## Prossimi Passi e Argomenti Correlati

* **Come fare OCR su batch di documenti** – avvolgi il codice sopra in un ciclo `foreach` e processa un'intera cartella.  
* **Converti formati di immagini scansionate** diversi da TIFF (PNG, JPEG) – la stessa API funziona; basta cambiare l'estensione del file.  
* **Estrai testo da immagine** per ulteriori analisi – passa `result.Text` in una pipeline di elaborazione del linguaggio naturale.  
* **Ottimizza le dimensioni del PDF** – esplora `PdfSaveOptions` per comprimere ulteriormente le immagini o incorporare i font solo quando necessario.  

Sperimenta con queste idee e diventerai rapidamente la persona di riferimento per qualsiasi richiesta di “trasformare questa scansione in un PDF ricercabile”.

---

### TL;DR

Ora sai come **creare PDF ricercabili** da immagini scansionate usando Aspose OCR in C#. Il processo è: inizializzare il motore, caricare l'immagine, eseguire l'OCR e salvare con `PdfSearchable`. Regola le impostazioni della lingua, DPI e compressione per gestire i casi particolari, e sei pronto a **convertire immagini scansionate**, **estrarre testo da immagini**, e persino **convertire TIFF in PDF** su larga scala. Buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}