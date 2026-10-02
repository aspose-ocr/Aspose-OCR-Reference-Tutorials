---
category: general
date: 2026-01-12
description: c# ocr tutorial that shows you how to recognize text image, extract text
  image c# and generate an image to pdf ocr file with confidence scores.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: en
og_description: Learn a complete c# ocr tutorial to recognize text image, extract
  text image c# and create an image to pdf ocr document with confidence scores.
og_title: c# ocr tutorial – Convert Images to Searchable PDFs
tags:
- OCR
- C#
- PDF
title: c# ocr tutorial – Turn Images into Searchable PDFs
url: /net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Turn Images into Searchable PDFs

Ever wondered how to **recognize text image** files in a C# project without hunting for third‑party services? You're not alone. In many real‑world apps—think invoice scanners, receipt trackers, or multilingual document archives—developers need a reliable, on‑premise OCR engine that also spits out confidence scores.  

This **c# ocr tutorial** will walk you through everything you need: from loading a picture, selecting language models, toggling GPU acceleration, to saving the result as a searchable PDF. By the end you’ll have a ready‑to‑run code sample that extracts text, reports OCR confidence, and optionally creates an *image to pdf ocr* file—all in under a minute of coding.

## What You’ll Build

- Load a multi‑language image (`sample_multi_lang.jpg` is used as a placeholder).  
- Choose Arabic, Hindi, and Russian language models (you can add more).  
- Turn on GPU processing if your machine supports it.  
- Get the raw OCR result **with confidence scores**.  
- Serialize the result to pretty‑printed JSON **or** write a searchable PDF.  

No external web services, no hidden magic—just Aspose.OCR for .NET, a few lines of C#, and a clear explanation of **why** each line matters.

## Prerequisites

- .NET 6.0 or later (the code compiles on .NET Core and .NET Framework).  
- Visual Studio 2022 (or any IDE you like).  
- An Aspose.OCR for .NET license (the free trial works for testing).  
- Optional: a CUDA‑compatible GPU if you want to speed up recognition.

> **Pro tip:** If you don’t have a GPU, just set `UseGpu = false` and the engine will fall back to CPU without any code changes.

## Step 1: Install the Required NuGet Packages

Open the **Package Manager Console** and run:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

These three packages give you the OCR engine, GPU acceleration, and a nice JSON serializer for the confidence output.

## Step 2: Set Up the Project Structure

Create a new console project (`dotnet new console -n AsposeOcrDemo`) and replace the generated `Program.cs` with the code below.  
All the logic lives inside the `Program` class; the only extra type is a small extension method that formats the OCR result for JSON.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### Why This Code Works

1. **GPU toggle** – `GpuOcrEngine` leverages CUDA cores; the ternary operator makes switching painless.  
2. **Automatic language download** – `AutoDownloadResources = true` ensures the Arabic, Hindi, and Russian models are fetched the first time you run the app.  
3. **Confidence scores** – `result.Words` contains a `Confidence` for each recognized word; the extension method formats them into a clean JSON object.  
4. **Searchable PDF** – `result.Pdf` is already a fully searchable PDF, so we just write the byte array to disk. No extra libraries needed.

## Step 6: Run the Sample

Open a terminal, navigate to the project folder, and execute:

```bash
dotnet run
```

If you chose **JSON** output, you’ll see something like:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

If you switched to **PDF**, the console prints the path and you’ll find a searchable PDF right next to the source image.

## Common Questions & Edge Cases

- **What if a language model isn’t available?**  
  The OCR engine throws a clear `ResourceNotFoundException`. Because we set `AutoDownloadResources = true`, the missing model is fetched automatically the first time, so the exception rarely surfaces in production.

- **Can I process a batch of images?**  
  Absolutely. Wrap the `engine.Recognize` call in a `foreach` loop over a directory of files. The same `OcrResultExtensions` works for each image.

- **Do I need a license for GPU?**  
  No. The free trial works for both CPU and GPU. A full license removes the trial watermark and lifts the page‑limit restrictions.

- **How accurate are the confidence scores?**  
  Scores range from 0.0 (no confidence) to 1.0 (perfect confidence). In practice, anything above 0.90 is reliable for downstream processing; you can filter lower‑confidence words if you need stricter validation.

## Step 7: Next Steps (Expand Your OCR Toolkit)

1. **Add more languages** – just append `LanguageModel.French` (or any supported model) to the `Languages` array.  
2. **Combine OCR with PDF/A conversion** – Aspose.PDF can embed the OCR layer into a PDF/A‑2b compliant document for archival.  
3. **Integrate with Azure Functions** – wrap the logic into a serverless endpoint to process uploads on the fly.  
4. **Fine‑tune confidence thresholds** – use `result.Words.Where(w => w.Confidence < 0.85)` to flag uncertain words for manual review.

---

### TL;DR

This **c# ocr tutorial** shows you how to:

- Load an image and select multiple language models.  
- Turn on GPU acceleration with a single boolean flag.  
- Retrieve OCR results **with confidence scores** and serialize them to JSON.  
- Optionally write a searchable PDF (**image to pdf ocr**).  

All of that is achievable with just a handful of lines, a free Aspose.OCR trial, and the code above. Give it a spin, tweak the language list, and you’ll have a production‑ready OCR pipeline in minutes.

---

![c# ocr tutorial example image](https://example.com/placeholder-image.jpg "c# ocr tutorial example image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}