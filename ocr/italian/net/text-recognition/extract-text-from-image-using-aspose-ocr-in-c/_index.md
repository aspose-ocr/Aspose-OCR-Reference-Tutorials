---
category: general
date: 2026-08-09
description: Estrai il testo da un'immagine con Aspose OCR in C#. Scopri come caricare
  l'immagine per l'OCR, impostare la lingua dell'OCR, elaborare l'OCR dell'immagine
  e convertire l'immagine in testo in modo efficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for ocr
- process image ocr
- set ocr language
language: it
lastmod: 2026-08-09
og_description: Estrai il testo da un'immagine usando Aspose OCR in C#. Questo tutorial
  mostra come caricare l'immagine per l'OCR, impostare la lingua dell'OCR, elaborare
  l'OCR dell'immagine e convertire l'immagine in testo in poche righe di codice.
og_image_alt: Screenshot of C# console output showing extracted text from an image
  using Aspose OCR
og_title: Estrai testo da immagine con Aspose OCR – Guida C#
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  headline: Extract text from image using Aspose OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  name: Extract text from image using Aspose OCR in C#
  steps:
  - name: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
    text: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
  - name: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
    text: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
  - name: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
    text: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
  - name: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
    text: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
  - name: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
    text: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
  - name: Instantiates `OcrEngine`.
    text: Instantiates `OcrEngine`.
  - name: '**Sets OCR language** to Cyrillic (or any language you choose).'
    text: '**Sets OCR language** to Cyrillic (or any language you choose).'
  - name: '**Loads image for OCR** from disk.'
    text: '**Loads image for OCR** from disk.'
  - name: '**Processes image OCR** to obtain the textual result.'
    text: '**Processes image OCR** to obtain the textual result.'
  - name: '**Converts image to text** and prints it.'
    text: '**Converts image to text** and prints it.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Estrai testo da immagine usando Aspose OCR in C#
url: /it/net/text-recognition/extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine usando Aspose OCR in C#

Se devi **estrarre testo da un'immagine** in un'applicazione .NET, questa guida ti accompagna passo passo in una soluzione completa, pronta all'uso. Vedrai come **caricare l'immagine per l'OCR**, scegliere il modulo linguistico corretto, eseguire il motore OCR e, infine, **convertire l'immagine in testo** con poche righe di C#.

Il tutorial copre tutto il necessario per ottenere risultati affidabili con Aspose.OCR, inclusi i problemi più comuni come formati di immagine non supportati e le sfumature specifiche delle lingue. Alla fine avrai un programma autonomo che stampa il testo riconosciuto sulla console.

## Cosa otterrai

* Caricare un file immagine nel motore OCR di Aspose.  
* **Impostare la lingua OCR** (cirillico nell'esempio, ma funziona con qualsiasi lingua supportata).  
* **Elaborare l'OCR dell'immagine** e ottenere la rappresentazione testuale.  
* **Convertire l'immagine in testo** e visualizzarlo, pronto per ulteriori elaborazioni o archiviazione.  

**Prerequisiti**

* .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.6+).  
* Visual Studio 2022 (o qualsiasi IDE che supporti C#).  
* Pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`).  

---

## Estrarre testo da immagine – walkthrough completo del codice

Di seguito trovi il programma completo e eseguibile. Copialo in un nuovo progetto console e sostituisci `YOUR_DIRECTORY/sample_cyrillic.jpg` con il percorso della tua immagine.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create an OCR engine instance.
            // The using block ensures the engine is disposed correctly.
            using (var engine = new OcrEngine())
            {
                // Step 2: Set OCR language.
                // Change OcrLanguage.Cyrillic to any other supported language,
                // e.g., OcrLanguage.English, OcrLanguage.Chinese, OcrLanguage.Hindi.
                engine.Language = OcrLanguage.Cyrillic;

                // Step 3: Load image for OCR.
                // ImageStream.FromFile reads the image from disk.
                // Supported formats: JPEG, PNG, BMP, TIFF, GIF.
                engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.jpg");

                // Step 4: Process image OCR.
                // The Process method runs the recognition engine and returns an OcrResult.
                var result = engine.Process();

                // Step 5: Convert image to text.
                // The recognized text is available via result.Text.
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

### Perché ogni passaggio è importante

1. **Creare un'istanza del motore OCR** – L'`OcrEngine` incapsula tutta la funzionalità OCR. Rilasciarla subito libera le risorse native, cosa fondamentale per servizi a lungo termine.  
2. **Impostare la lingua OCR** – Selezionare il modulo linguistico corretto migliora notevolmente la precisione. Aspose fornisce oltre 30 pacchetti linguistici; quello predefinito è l'inglese. L'esempio usa il cirillico per dimostrare una scrittura non latina.  
3. **Caricare l'immagine per l'OCR** – Il motore lavora con un `ImageStream`. Fornire un'immagine ad alta risoluzione (≥300 dpi) riduce gli errori di riconoscimento, soprattutto per script complessi.  
4. **Elaborare l'OCR dell'immagine** – Qui avviene il lavoro pesante. Il metodo restituisce un `OcrResult` contenente il testo estratto, i punteggi di confidenza e, opzionalmente, dati di layout.  
5. **Convertire l'immagine in testo** – `result.Text` è una semplice `string`. Puoi scriverla su file, indicizzarla in un motore di ricerca o passarla a pipeline NLP successive.

---

## Caricare immagine per l'OCR

Il metodo `ImageStream.FromFile` supporta i formati raster più comuni. Se ricevi le immagini come array di byte (ad esempio da un'API web), usa invece `ImageStream.FromBytes(byte[])`:

```csharp
byte[] imageBytes = File.ReadAllBytes("path/to/image.png");
engine.Image = ImageStream.FromBytes(imageBytes);
```

**Consiglio:** Verifica sempre che l'immagine non sia corrotta prima di passarla al motore. Un rapido controllo `try { Image.FromFile(...); } catch { ... }` evita eccezioni a runtime.

---

## Impostare la lingua OCR

Aspose.OCR include pacchetti linguistici che puoi abilitare a runtime. Per elencare tutte le lingue disponibili:

```csharp
foreach (var lang in Enum.GetValues(typeof(OcrLanguage)))
{
    Console.WriteLine(lang);
}
```

Se devi riconoscere più lingue nello stesso documento, combinane i valori con l'operatore OR bitwise:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Russian;
```

**Caso limite:** Mescolare lingue da destra a sinistra (RTL) (ad es. arabo) con script da sinistra a destra può richiedere una gestione aggiuntiva del layout. Aspose rileva automaticamente la direzione, ma puoi affinare il comportamento tramite `engine.PageSegmentationMode`.

---

## Elaborare l'OCR dell'immagine

La chiamata `Process` è sincrona e blocca l'esecuzione finché il motore non termina. Per batch di grandi dimensioni o applicazioni UI, considera la versione asincrona:

```csharp
var task = engine.ProcessAsync();
OcrResult result = await task;
```

**Errore comune:** Dimenticare di impostare `engine.Image` prima di chiamare `Process` genera un `InvalidOperationException`. Assegna sempre prima l'immagine.

---

## Convertire l'immagine in testo

La stringa estratta può essere manipolata come qualsiasi altra `string` .NET. Per esempio, per scrivere l'output su file:

```csharp
File.WriteAllText("output.txt", result.Text);
```

Se devi mantenere esattamente gli a capo così come appaiono nell'immagine, usa direttamente `result.Text`. Per post‑elaborazione (ad es. rimuovere spazi bianchi extra), applica i metodi standard delle stringhe:

```csharp
string cleaned = result.Text
    .Replace("\r\n", "\n")
    .Trim();
```

---

## Riepilogo dell'esempio completo

Mettendo insieme tutti i passaggi, il programma:

1. Istanzia `OcrEngine`.  
2. **Imposta la lingua OCR** al cirillico (o a qualsiasi altra lingua tu scelga).  
3. **Carica l'immagine per l'OCR** dal disco.  
4. **Elabora l'OCR dell'immagine** per ottenere il risultato testuale.  
5. **Converte l'immagine in testo** e lo stampa.

Eseguendo il campione con un'immagine cirillica chiara otterrai un output simile a:

```
=== Recognized Text ===
Пример текста на кириллице
```

Se l'immagine contiene testo in inglese, basta cambiare `engine.Language = OcrLanguage.English;` e lo stesso codice **estrarrà testo da immagine** correttamente.

---

## Conclusione

Ora sai come **estrarre testo da immagine** usando Aspose OCR in C#. Il tutorial ha coperto il caricamento dell'immagine, la selezione della lingua appropriata, l'esecuzione del processo OCR e la **conversione dell'immagine in testo** per usi successivi.  

Da qui puoi:

* Sperimentare altre lingue (`load image for OCR` → `set OCR language` → `process image OCR`).  
* Integrare il passaggio OCR in una pipeline più ampia (ad es. ingestione documenti, PDF ricercabili).  
* Ottimizzare le prestazioni elaborando batch di immagini o usando l'API asincrona.

Sentiti libero di esplorare la documentazione di Aspose.OCR per funzionalità avanzate come dizionari personalizzati, modalità di segmentazione pagina e ottimizzazione della precisione OCR. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che ampliano le tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci alternativi nei tuoi progetti.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}