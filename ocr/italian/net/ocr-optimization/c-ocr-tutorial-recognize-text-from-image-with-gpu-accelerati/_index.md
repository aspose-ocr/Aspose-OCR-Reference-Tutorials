---
category: general
date: 2026-01-15
description: Tutorial OCR in C# che mostra come riconoscere il testo da un'immagine,
  estrarre il testo da una fattura e convertire l'immagine in testo usando Aspose
  OCR sulla GPU.
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- extract text from invoice
- convert image to text
- load image for ocr
language: it
og_description: tutorial OCR in C# che ti insegna a riconoscere il testo da un'immagine,
  estrarre il testo da una fattura e convertire l'immagine in testo con Aspose OCR
  sulla GPU.
og_title: c# tutorial OCR – Riconoscimento del testo veloce con GPU
tags:
- OCR
- C#
- Aspose
- GPU
title: c# tutorial OCR – Riconosci il testo da un'immagine con accelerazione GPU
url: /it/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Riconoscere il Testo da Immagine con Accelerazione GPU

Hai mai avuto bisogno di un **c# ocr tutorial** che funzioni davvero senza infinite prove ed errori? Forse stai osservando una fattura ad alta risoluzione e ti chiedi come **estrarre testo da fattura** in pochi secondi. La buona notizia è che non devi reinventare la ruota: Aspose.OCR ti offre un'API pulita, accelerata dalla GPU, che fa il lavoro pesante per te.

In questa guida percorreremo un esempio completo, eseguibile, che mostra come **riconoscere testo da immagine**, **convertire immagine in testo**, e gestire le difficoltà più comuni. Alla fine avrai un programma autonomo in grado di leggere qualsiasi foto di un documento, dalle ricevute ai contratti scansionati, e produrre testo pulito e ricercabile.

## Cosa Imparerai

- Come installare e referenziare il pacchetto NuGet Aspose.OCR.  
- Come configurare il motore OCR per l'esecuzione sulla GPU per prestazioni fulminee.  
- Il modo corretto di **caricare immagine per ocr** usando `OcrImage.FromFile`.  
- Come chiamare `Recognize` con la lingua desiderata e recuperare il risultato.  
- Suggerimenti per gestire PDF multi‑pagina, scansioni a basso contrasto e gestione degli errori.

Non è necessaria alcuna esperienza pregressa con Aspose; basta un ambiente di sviluppo .NET funzionante (Visual Studio 2022 o VS Code) e una GPU modesta (anche una GPU integrata Intel basta).

---

## Step 1 – Install Aspose.OCR and Prepare Your Project

First things first: you need the Aspose.OCR library. The easiest way is via NuGet.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** If you’re targeting .NET 6 or later, the package will automatically pull in the native GPU binaries for Windows, Linux, and macOS. No extra DLLs to copy.

Once the package is added, open your project file (`*.csproj`) and verify the reference:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.12.0" />
</ItemGroup>
```

Now you have everything you need to start coding.

## Step 2 – Create a GPU‑Enabled OCR Engine (c# ocr tutorial)

The heart of the **c# ocr tutorial** is the `OcrEngine`. By setting `Engine = Engine.Gpu` we tell Aspose to use the graphics card instead of the CPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine with GPU acceleration.
            var ocrEngine = new OcrEngine
            {
                Engine = Engine.Gpu // GPU acceleration is selected; the library auto‑detects the device.
            };

            // The rest of the steps are broken out into separate methods for clarity.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            PerformOcr(ocrEngine, imagePath);
        }
    }
}
```

> **Why GPU?** A GPU can process thousands of pixels in parallel, cutting OCR time from seconds to fractions of a second on large, high‑DPI images.

## Step 3 – Load Image for OCR (load image for ocr)

Loading the image correctly is more important than you might think. `OcrImage.FromFile` supports PNG, JPEG, BMP, TIFF, and even PDF pages. It also reads the image’s DPI, which influences accuracy.

```csharp
static void PerformOcr(OcrEngine engine, string filePath)
{
    // Step 3: Load the image you want to recognize.
    // The FromFile method automatically detects the format.
    var image = OcrImage.FromFile(filePath);

    // Optional: Pre‑process the image for better results.
    // For example, you can increase contrast or convert to grayscale.
    image = ImagePreprocessor.AdjustContrast(image, 1.2);
    image = ImagePreprocessor.ConvertToGrayscale(image);
    
    // Continue to recognition...
    RecognizeAndDisplay(engine, image);
}
```

**Note:** If you’re dealing with a PDF, you can extract each page as an `OcrImage` and feed them one by one.

## Step 4 – Recognize Text from Image (recognize text from image)

Now the magic happens. We ask the engine to recognize English text, but you can pass any language supported by Aspose (Spanish, German, Chinese, etc.).

```csharp
static void RecognizeAndDisplay(OcrEngine engine, OcrImage image)
{
    // Step 4: Perform OCR on the image using the desired language.
    var result = engine.Recognize(image, Language.English);

    // Step 5: Output the recognized text.
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(result.Text);
}
```

The `result.Text` property contains the plain string. If you need the confidence score for each word, you can inspect `result.Regions`.

### Expected Output

```
=== OCR RESULT ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,234.56
Thank you for your business!
```

If the image is blurry, you might see garbled characters—this is where the preprocessing from Step 3 helps.

## Step 5 – Extract Text from Invoice – Real‑World Example

Let’s say you have a folder full of scanned invoices and you want to pull out the total amount. Below is a quick extension of the previous code that uses a simple regular expression.

```csharp
using System.Text.RegularExpressions;

static void ExtractTotalAmount(string ocrText)
{
    // Look for a pattern like "$1,234.56"
    var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
    if (match.Success)
        Console.WriteLine($"Detected total: {match.Value}");
    else
        Console.WriteLine("Total amount not found.");
}
```

You would call `ExtractTotalAmount(result.Text);` right after printing the OCR result. This demonstrates how easy it is to **extract text from invoice** files once you have the raw string.

## Step 6 – Convert Image to Text in Bulk (convert image to text)

Processing a single file is fine for a demo, but production code often needs to handle dozens or hundreds of images. Here’s a concise loop that processes an entire directory:

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    foreach (var file in Directory.EnumerateFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly)
                                 .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
    {
        Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
        var img = OcrImage.FromFile(file);
        var res = engine.Recognize(img, Language.English);
        Console.WriteLine(res.Text);
        ExtractTotalAmount(res.Text); // optional invoice extraction
    }
}
```

Running `ProcessFolder(ocrEngine, @"C:\Invoices")` will **convert image to text** for every supported file in the folder, leveraging the GPU for speed.

## Edge Cases and Common Pitfalls

| Situazione | Perché Accade | Soluzione Rapida |
|------------|----------------|-------------------|
| **Scansione a basso contrasto** | L'OCR fatica a distinguere lo sfondo dal primo piano. | Aumenta il contrasto (`ImagePreprocessor.AdjustContrast`) o applica una soglia adattiva. |
| **PDF multi‑pagina** | `OcrImage.FromFile` legge solo la prima pagina. | Usa `PdfDocument` per estrarre ogni pagina come `OcrImage` e iterare. |
| **Lingua non supportata** | La lingua predefinita è l'inglese. | Passa `Language.Spanish` o qualsiasi valore enum supportato. |
| **GPU non rilevata** | Mancano i binari nativi o il driver è obsoleto. | Verifica che il driver della GPU sia aggiornato; reinstalla il pacchetto NuGet con il flag `-runtime`. |
| **Out‑of‑memory su immagini enormi** | La memoria della GPU è limitata. | Ridimensiona l'immagine (`image = ImagePreprocessor.Resize(image, 2000, 0)`). |

Affrontare questi problemi in anticipo ti farà risparmiare ore di debug in seguito.

## Full Working Example

Below is the complete program you can copy‑paste into a new console app. It includes all the helper methods discussed above.

```csharp
using System;
using System.IO;
using System.Linq;
using System.Text.RegularExpressions;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize GPU‑accelerated OCR engine.
            var ocrEngine = new OcrEngine { Engine = Engine.Gpu };

            // 2️⃣ Define the path to a single image or a folder.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            // string folderPath = @"C:\Invoices";

            // Uncomment one of the following lines:
            PerformOcr(ocrEngine, imagePath);
            // ProcessFolder(ocrEngine, folderPath);
        }

        // -------------------------------------------------
        // Load image, preprocess, recognize, and display.
        // -------------------------------------------------
        static void PerformOcr(OcrEngine engine, string filePath)
        {
            var image = OcrImage.FromFile(filePath);
            image = ImagePreprocessor.AdjustContrast(image, 1.2);
            image = ImagePreprocessor.ConvertToGrayscale(image);

            var result = engine.Recognize(image, Language.English);
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);

            ExtractTotalAmount(result.Text);
        }

        // -------------------------------------------------
        // Bulk processing of a folder.
        // -------------------------------------------------
        static void ProcessFolder(OcrEngine engine, string folderPath)
        {
            foreach (var file in Directory.EnumerateFiles(folderPath, "*.*")
                                          .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
            {
                Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
                var img = OcrImage.FromFile(file);
                var res = engine.Recognize(img, Language.English);
                Console.WriteLine(res.Text);
                ExtractTotalAmount(res.Text);
            }
        }

        // -------------------------------------------------
        // Simple regex to pull the total amount from an invoice.
        // -------------------------------------------------
        static void ExtractTotalAmount(string ocrText)
        {
            var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
            if (match.Success)
                Console.WriteLine($"Detected total: {match.Value}");
            else
                Console.WriteLine("Total amount not found.");
        }
    }
}
```

**Run it** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}