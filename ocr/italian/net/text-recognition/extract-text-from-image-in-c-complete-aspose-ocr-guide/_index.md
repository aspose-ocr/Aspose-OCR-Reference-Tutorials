---
category: general
date: 2026-01-10
description: Estrai il testo dall'immagine usando Aspose OCR in C#. Scopri come convertire
  il testo di documenti scansionati con l'elaborazione batch e salvare i risultati.
draft: false
keywords:
- extract text from image
- convert scanned document text
- batch OCR processing
- Aspose OCR
- C# OCR tutorial
language: it
og_description: Estrai il testo da un'immagine con Aspose OCR in C#. Questo tutorial
  mostra come convertire il testo di documenti scansionati utilizzando l'elaborazione
  batch.
og_title: Estrai testo da immagine in C# – Guida completa Aspose OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Estrai il testo da un'immagine in C# – Guida completa a Aspose OCR
url: /it/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine – Guida completa a Aspose OCR

Hai mai dovuto **estrarre testo da immagine** ma non sapevi da dove cominciare? Non sei solo; molti sviluppatori si trovano di fronte a questo ostacolo quando lavorano con PDF scansionati, TIFF a più pagine o ricevute basate su foto. La buona notizia è che con Aspose OCR puoi **convertire il testo di documenti scansionati** in poche righe di C#.

In questo tutorial percorreremo uno scenario reale: prendere un TIFF a più pagine, eseguire OCR batch su ogni pagina e scrivere un unico file di testo che contenga il contenuto di tutte le pagine. Alla fine avrai un’app console pronta all’uso, comprenderai perché ogni passaggio è importante e saprai come modificare il flusso per casi particolari come immagini protette da password o pacchetti linguistici personalizzati.

## Prerequisiti

- .NET 6.0 SDK o successivo (il codice funziona anche con .NET Core e .NET Framework)  
- Visual Studio 2022 (o qualsiasi editor tu preferisca)  
- Un file di licenza Aspose OCR (oppure puoi usare la modalità di valutazione gratuita)  
- Un file immagine a più pagine (ad es., `multipage.tif`) collocato in una cartella a cui puoi fare riferimento  

Non sono richiesti pacchetti NuGet aggiuntivi oltre a `Aspose.OCR`; lo installeremo nel primo passaggio.

## Passo 1 – Installa Aspose OCR e configura il progetto

Per iniziare, crea un nuovo progetto console e aggiungi la libreria Aspose OCR.

```bash
dotnet new console -n ImageTextExtractor
cd ImageTextExtractor
dotnet add package Aspose.OCR
```

> **Suggerimento:** Se disponi di un file di licenza (`Aspose.OCR.lic`), copialo nella radice del progetto. La libreria lo rileverà automaticamente a runtime.

Perché questo passo? L’installazione del pacchetto ti dà accesso a `BatchProcessor`, `OcrEngine` e altre classi utili che astraggono la gestione a basso livello delle immagini. Garantisce inoltre che tu stia usando gli ultimi algoritmi OCR forniti da Aspose.

## Passo 2 – Carica l’immagine a più pagine con BatchProcessor

`BatchProcessor` è progettato proprio per questo scenario: iterare su ogni pagina di un’immagine a più pagine senza dover suddividere manualmente i file.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System.Text;

// Step 2: Initialize the batch processor with the path to your TIFF
var batchProcessor = new BatchProcessor(@"YOUR_DIRECTORY\multipage.tif");

// Verify that pages were loaded
if (batchProcessor.Pages.Count == 0)
{
    Console.WriteLine("No pages found – double‑check the file path.");
    return;
}
```

Il `BatchProcessor` legge tutte le pagine in memoria, esponendole tramite `batchProcessor.Pages`. Ogni oggetto pagina conosce il proprio numero (`ocrPage.Number`) che utilizzeremo più avanti per intestazioni chiare.

## Passo 3 – Prepara un StringBuilder per accumulare i risultati

Vogliamo un unico file di testo che contenga l’output OCR di tutte le pagine, separato da intestazioni. `StringBuilder` è il modo più efficiente per concatenare stringhe in un ciclo.

```csharp
// Step 3: Create a StringBuilder to collect OCR results
var extractedText = new StringBuilder();
```

Perché un `StringBuilder`? Concatenare stringhe con `+` all’interno di un ciclo creerebbe una nuova stringa ad ogni iterazione, penalizzando le prestazioni—soprattutto con documenti di grandi dimensioni.

## Passo 4 – Itera su ogni pagina, esegui OCR e aggiungi i risultati

Ora il cuore del tutorial: scorrere ogni pagina, riconoscere il testo e memorizzarlo con un marcatore di pagina.

```csharp
// Step 4: Process each page individually
foreach (var ocrPage in batchProcessor.Pages)
{
    // Create a fresh OcrEngine for every page – this isolates settings
    var ocrEngine = new OcrEngine
    {
        Image = ocrPage
    };

    // Perform recognition
    ocrEngine.Recognize();

    // Append a clear header and the recognized text
    extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
    extractedText.AppendLine(ocrEngine.Text);
}
```

**Perché un nuovo `OcrEngine` per pagina?** Alcuni sviluppatori riutilizzano lo stesso engine cambiandone la proprietà `Image`, ma questo può mantenere impostazioni linguistiche o risultati precedenti, generando bug sottili. Creare un nuovo engine garantisce una base pulita.

### Gestione dei casi limite più comuni

- **Pagine vuote:** Se una pagina non contiene testo riconoscibile, `ocrEngine.Text` sarà una stringa vuota. Potresti inserire un segnaposto come “(Nessun testo rilevato)”.
- **Selezione della lingua:** Per impostazione predefinita Aspose OCR usa l’inglese. Per elaborare tedesco o francese, imposta `ocrEngine.Language = Language.German;` prima di chiamare `Recognize()`.
- **Suggerimento di performance:** Per TIFF molto grandi, puoi abilitare `ocrEngine.UseParallelProcessing = true;` per sfruttare più core.

## Passo 5 – Scrivi l’output combinato in un file di testo

Infine, persisti la stringa accumulata su disco.

```csharp
// Step 5: Save the result to a .txt file
string outputPath = @"YOUR_DIRECTORY\multipage_result.txt";
File.WriteAllText(outputPath, extractedText.ToString());

Console.WriteLine($"OCR complete! Results saved to {outputPath}");
```

Il file risultante `multipage_result.txt` avrà un aspetto simile a questo:

```
--- Page 1 ---
This is the first page of the scanned document.
It contains a title and some introductory text.

--- Page 2 ---
Continuation of the report.
Data tables and figures follow.
```

Ora hai **estratto testo da immagine** e hai effettivamente **convertito il testo di documenti scansionati** in un formato ricercabile e modificabile.

## Bonus – Panoramica visiva (Testo alternativo)

Di seguito trovi un semplice diagramma di flusso che illustra il processo.  
*Testo alternativo:* “Diagramma che mostra come estrarre testo da immagine usando il batch processing di Aspose OCR in C#”.

![OCR Flow Diagram](placeholder-image-url.png)

*(Se pubblichi questo tutorial su un sito statico, sostituisci il segnaposto con un SVG o PNG reale.)*

## Domande frequenti

**Funziona con file PDF?**  
Sì, Aspose OCR può leggere le pagine PDF come immagini. Devi solo convertire il PDF in immagini prima, oppure usare `PdfDocument` da `Aspose.PDF` e fornire l’immagine rasterizzata di ogni pagina a `OcrEngine`.

**E se il mio TIFF è protetto da password?**  
`BatchProcessor` non gestisce direttamente la crittografia. Decrittografa il file usando una libreria come `Aspose.Imaging` prima di passarlo al pipeline OCR.

**Posso generare JSON invece del testo semplice?**  
Assolutamente. Sostituisci la logica di `StringBuilder` con un serializzatore JSON (ad es., `System.Text.Json`) e memorizza il testo di ogni pagina sotto una chiave `pageNumber`.

## Esempio completo funzionante

Ecco il programma completo che puoi copiare‑incollare in `Program.cs`. Include tutti i `using`, la gestione degli errori e i commenti.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Text;

namespace ImageTextExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            string inputImagePath = @"YOUR_DIRECTORY\multipage.tif";
            string outputTextPath = @"YOUR_DIRECTORY\multipage_result.txt";

            // 1️⃣ Load the multi‑page image
            var batchProcessor = new BatchProcessor(inputImagePath);
            if (batchProcessor.Pages.Count == 0)
            {
                Console.WriteLine("No pages detected – verify the file path.");
                return;
            }

            // 2️⃣ Prepare a StringBuilder for the final output
            var extractedText = new StringBuilder();

            // 3️⃣ Process each page
            foreach (var ocrPage in batchProcessor.Pages)
            {
                var ocrEngine = new OcrEngine
                {
                    Image = ocrPage,
                    // Uncomment to change language:
                    // Language = Language.German,
                    // UseParallelProcessing = true
                };

                // Run OCR
                ocrEngine.Recognize();

                // Append header and text
                extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
                // Guard against empty results
                string pageText = string.IsNullOrWhiteSpace(ocrEngine.Text)
                    ? "(No text detected on this page)"
                    : ocrEngine.Text;
                extractedText.AppendLine(pageText);
            }

            // 4️⃣ Write to file
            File.WriteAllText(outputTextPath, extractedText.ToString());

            Console.WriteLine($"✅ Extraction complete. File saved at: {outputTextPath}");
        }
    }
}
```

Esegui il programma con:

```bash
dotnet run
```

Dovresti vedere il messaggio nella console che conferma il successo, e il file di output conterrà i risultati OCR concatenati.

## Conclusione

Abbiamo appena dimostrato un modo pratico per **estrarre testo da immagine** usando Aspose OCR, trasformando qualsiasi file scansionato a più pagine in testo semplice e ricercabile. Sfruttando `BatchProcessor` e una configurazione pulita di `OcrEngine` per pagina, puoi convertire in modo affidabile il **testo di documenti scansionati** mantenendo il codice semplice e manutenibile.

Sentiti libero di sperimentare: prova lingue diverse, passa a output JSON, o integra questa logica in un’API web che elabora upload al volo. Il modello di base rimane lo stesso—carica, riconosci, accumula e persisti.

Hai altre domande su OCR, licenze Aspose o sulla gestione di grandi batch di documenti? Lascia un commento qui sotto o consulta la documentazione ufficiale di Aspose per approfondimenti. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}