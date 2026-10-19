---
category: general
date: 2026-09-13
description: Scopri come convertire una pagina scansionata in PDF in C# usando Aspose
  OCR. Questa guida mostra la pre‑elaborazione, il riconoscimento del testo coreano
  e la creazione di un PDF ricercabile.
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Scopri come convertire una pagina scansionata in PDF in C# con Aspose
  OCR. Il tutorial copre la pre‑elaborazione delle immagini, l'OCR accelerato da GPU
  per il testo coreano e la generazione di un PDF ricercabile in pochi minuti.
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: Come convertire una pagina scansionata in PDF in C# con OCR
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: Come convertire una pagina scansionata in PDF in C# con OCR
url: /it/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come trasformare una pagina scansionata in PDF in C# con OCR

Se hai bisogno di **convertire una pagina scansionata in PDF** mantenendo il testo ricercabile, sei nel posto giusto. Questo tutorial ti guida nell'uso di Aspose OCR per **preprocessare l'immagine per OCR**, **riconoscere un'immagine di testo coreano**, e infine **creare un'immagine PDF ricercabile** – il tutto da una semplice applicazione console C#.

## Risposte rapide
- **Quale libreria gestisce l'OCR?** Aspose.OCR per .NET  
- **Posso usare la GPU?** Sì – abilita l'accelerazione GPU per una velocità fino a 2× più rapida  
- **È necessario un pacchetto lingua coreano?** Viene scaricato automaticamente al primo utilizzo  
- **L'output sarà ricercabile?** Il PDF generato contiene un livello di testo invisibile  
- **Quali versioni .NET sono supportate?** .NET 6.0 e successive (inclusi .NET Core e .NET Framework)

## Requisiti

- **.NET 6.0 o successivo** – funziona su .NET Core, .NET Framework e .NET 5/6+  
- **Pacchetto NuGet Aspose.OCR per .NET** (`Aspose.OCR`) – le chiavi di prova sono gratuite sul sito Aspose  
- Un'immagine di esempio con caratteri coreani, ad es. `korean_book_page.jpg`  
- Il tuo IDE preferito (Visual Studio 2022, VS Code, Rider, ecc.)

> **Consiglio pro:** Conserva le immagini in una cartella `Resources/` così i percorsi rimangono coerenti su tutte le macchine.

## Panoramica del processo

1. Inizializza il motore OCR con supporto GPU.  
2. Aggiungi filtri di **preprocessare l'immagine per OCR** come deskew e denoise.  
3. Scarica e carica il modello linguistico coreano (gestito automaticamente).  
4. Esegui l'OCR sull'immagine.  
5. Esporta il risultato con **SearchablePdfExporter** per **creare un'immagine PDF ricercabile**.  
6. (Facoltativo) Serializza l'output OCR in JSON per pipeline successive.

Di seguito espandiamo ogni passaggio, spieghiamo *perché* è importante e ti forniamo il codice esatto da copiare‑incollare.

## Come funziona la conversione di una pagina scansionata in PDF?

`OcrEngine` è la classe principale in Aspose.OCR che esegue il riconoscimento ottico dei caratteri sulle immagini.  
`SearchablePdfExporter` crea un PDF che contiene l'immagine originale e un livello di testo invisibile per la ricerca.  
`RecognitionResult` contiene il testo e i dati di confidenza restituiti dal motore OCR.

Carica la tua immagine con `new OcrEngine()` e chiama `engine.Recognize("korean_book_page.jpg")`, quindi passa il `RecognitionResult` a `SearchablePdfExporter.Export`. Questo flusso a due step legge il bitmap, estrae il testo Unicode e lo incorpora entrambi in un unico PDF dove il livello di testo è invisibile ma ricercabile. L'accelerazione GPU dimezza il tempo di riconoscimento, mentre i filtri deskew e denoise aumentano l'accuratezza fino al 15 % su scansioni rumorose.

## Converti immagine in PDF – flusso completo

Il frammento seguente è il *programma completo*. Crea un nuovo progetto console (`dotnet new console -n OcrPdfDemo`) e sostituisci il file `Program.cs` generato automaticamente con il codice mostrato nel segnaposto.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### Perché funziona

- **Accelerazione GPU** dimezza il tempo di riconoscimento rispetto alla modalità solo CPU.  
- **Deskew** e **Denoise** sono tecniche classiche di *preprocessare l'immagine per OCR*; correggono difetti di scansione comuni che altrimenti fanno perdere caratteri al motore.  
- **Caricamento del modello linguistico** è essenziale per **riconoscere un'immagine di testo coreano** – senza il modello coreano il motore ricade su un alfabeto latino generico e produce risultati incomprensibili.  
- **SearchablePdfExporter** combina il bitmap originale e una sovrapposizione di testo invisibile, fornendoti un risultato di **creare un'immagine PDF ricercabile** che puoi indicizzare in qualsiasi visualizzatore PDF.

## Perché funziona

- **Accelerazione GPU** dimezza il tempo di riconoscimento rispetto alla modalità solo CPU.  
- **Deskew** e **Denoise** sono tecniche classiche di *preprocessare l'immagine per OCR*; correggono difetti di scansione comuni che altrimenti fanno perdere caratteri al motore.  
- **Caricamento del modello linguistico** è essenziale per **riconoscere un'immagine di testo coreano** – senza il modello coreano il motore ricade su un alfabeto latino generico e produce risultati incomprensibili.  
- **SearchablePdfExporter** combina il bitmap originale e una sovrapposizione di testo invisibile, fornendoti un risultato di **creare un'immagine PDF ricercabile** che puoi indicizzare in qualsiasi visualizzatore PDF.

## Preprocessare l'immagine per OCR – consigli e trucchi

`DeskewFilter` corregge la rotazione delle pagine scansionate.  
`ContrastFilter` regola il contrasto dell'immagine per migliorare l'accuratezza OCR.  
`BinarizationFilter` converte l'immagine in bianco‑nero basandosi su una soglia, riducendo il rumore di sfondo.  
`OrientationFilter` rileva e corregge pagine miste in orientamento ritratto/paesaggio.  

| Problema | Filtro aggiuntivo | Come aggiungere |
|----------|-------------------|-----------------|
| Basso contrasto | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Rumore di sfondo intenso | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Orientamento misto (ritratto & paesaggio) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Nota:** L'aggiunta di troppi filtri può rallentare l'elaborazione. Testa ogni modifica su una singola pagina prima di scalare.

## Riconoscere immagine di testo coreano – problemi comuni

Gli script coreani contengono sillabe Hangul molto dense. Se noti output confuso:

1. **Assicurati che il modello linguistico sia stato scaricato completamente** – controlla la console per un messaggio tipo “Downloading Korean model…”.  
2. **Aumenta il `MaxAngle`** in `DeskewFilter` se le tue scansioni sono ruotate oltre i 12°.  
3. **Incrementa la memoria GPU** impostando `ocrEngine.GpuMemoryLimit = 2048;` (valore in MB).  

`LanguageModel.Korean` carica i dati linguistici coreani per l'OCR, consentendo un riconoscimento Hangul accurato.  

Queste regolazioni influenzano direttamente il successo di **riconoscere un'immagine di testo coreano**.

## Creare immagine PDF ricercabile – verifica del risultato

Al termine del programma, apri `korean_page.pdf` in qualsiasi lettore PDF (Adobe Acrobat Reader, Foxit, anche Chrome). Dovresti poter:

- **Selezionare il testo** con il mouse come se fosse un PDF nativo.  
- **Cercare** parole coreane usando la casella di ricerca integrata.  

Se il livello di testo appare vuoto, verifica che il metodo `Export` abbia ricevuto il percorso immagine corretto e che il risultato OCR contenga un `RecognitionResult.Text` non vuoto.

## Output JSON completo – cosa aspettarsi

La console stampa un payload JSON formattato in modo leggibile. Un esempio ridotto è il seguente:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

Puoi inviare questo JSON a servizi downstream (ad es. pipeline di indicizzazione, API di traduzione) senza dover rieseguire l'OCR.

## Risoluzione dei problemi e FAQ

**D: Il mio PDF è molto più grande rispetto all'immagine originale.**  
R: L'esportatore incorpora il bitmap originale alla sua risoluzione nativa. Se le dimensioni sono un problema, ridimensiona l'immagine *prima* del riconoscimento:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**D: L'OCR restituisce stringhe vuote.**  
R: Verifica che il percorso dell'immagine sia corretto e che il file non sia corrotto. Inoltre, assicurati che il driver GPU sia aggiornato; driver obsoleti possono causare fallimenti silenziosi.

**D: Posso elaborare più pagine in un ciclo?**  
R: Assolutamente. Avvolgi i passaggi 4‑6 in un ciclo `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` e modifica di conseguenza il percorso di output PDF.

## Conclusione

Abbiamo appena **convertito un'immagine in PDF** mantenendo il testo ricercabile, grazie al potente pipeline di Aspose OCR. **Preprocessando l'immagine per OCR**, aumenti l'accuratezza; **riconoscendo un'immagine di testo coreano**, gestisci script complessi; e **creando un'immagine PDF ricercabile**, ottieni un documento portatile e indicizzabile.

Prendi il codice, puntalo alle tue scansioni e sperimenta con filtri o modelli linguistici aggiuntivi. Lo stesso schema funziona per cinese, giapponese o qualsiasi lingua basata su alfabeto latino—basta sostituire `LanguageModel.Korean` con l'enum appropriato.

Hai altre domande? Lascia un commento, e buona programmazione!

---

**Last Updated:** 2026-09-13  
**Tested with:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose

## Tutorial correlati

- [Create Searchable Pdf From Scanned Files Using Aspose Ocr](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [Ocr Preprocessing Pipeline How To Recognize Text From Image](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Recognize Text From Image With Aspose Ocr Complete C Guide](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}