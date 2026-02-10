---
category: general
date: 2026-02-09
description: Learn how to perform OCR in C# to extract text from image, recognize
  text from PNG, and write JSON file C# quickly.
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: en
og_description: How to perform OCR in C#? Follow this step‑by‑step guide to extract
  text from image, recognize text from PNG, and write JSON file C# efficiently.
og_title: How to Perform OCR in C# – Extract Text and Write JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: How to Perform OCR in C# – Extract Text and Write JSON
url: /net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Perform OCR in C# – Complete Guide

How to perform OCR in C# is a common hurdle when you need to **extract text from image** files. In this guide we’ll walk through recognizing text from PNG, exporting the detailed result to a JSON string, and finally **write JSON file C#** style. Ever stared at a scanned form and wondered how to turn those squiggles into searchable text? You’re not alone; many developers hit this snag early on.

We’ll use the Aspose.OCR library because it gives per‑symbol confidence out of the box and plays nicely with .NET 6+ projects. By the end of this tutorial you’ll have a ready‑to‑run console app that loads a PNG, pulls out every character, and saves a tidy JSON file you can feed into a database or an AI model. No mystery “see the docs” shortcuts—just a self‑contained solution.

## What You’ll Need

- **.NET 6 SDK** (or later) – the current LTS version at the time of writing.
- **Aspose.OCR for .NET** NuGet package – `Install-Package Aspose.OCR`.
- A PNG image you want to scan (e.g., `form.png`).  
- An IDE or editor – Visual Studio, VS Code, Rider – whatever you’re comfortable with.

That’s it. If you’ve got those pieces, you’re good to go.

![How to perform OCR example](ocr-example.png "How to perform OCR in C#")

*Image alt text: how to perform OCR illustration showing a C# console app processing a PNG.*

## Step 1: Set Up the Project and Add Dependencies

First, spin up a new console project and pull in the Aspose OCR library.

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **Pro tip:** Use the `--framework net6.0` flag if you want to lock the target framework explicitly.

Why this step matters: the NuGet package contains the `OcrEngine`, `ImageStream`, and `JsonExporter` classes we’ll rely on. Without it, the compiler will have no idea what “OCR” even means.

## Step 2: Write the Core OCR Logic

Open `Program.cs` (or create a new file) and replace its contents with the following. Each section is commented so you can see why it’s there.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### Why Each Piece Is Important

- **OcrEngine**: Think of it as the brain of the operation. It loads language models and sets up the inference pipeline.
- **ImageStream.FromFile**: Handles any PNG, JPEG, BMP, etc. It abstracts away file‑I/O quirks.
- **RecognitionResult**: Holds the raw text plus confidence scores. This is where you get the granular data you need for downstream validation.
- **JsonExporter**: Converts the rich `RecognitionResult` into a clean JSON payload, perfect for APIs.
- **File.WriteAllText**: The straightforward .NET way to **write JSON file C#** without extra dependencies.

## Step 3: Run the Application and Verify Output

Compile and execute the program:

```bash
dotnet run
```

You should see a console message similar to:

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

Open `form.json` – you’ll find something like:

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

The **extract text from image** step succeeded, and you now have a machine‑readable JSON representation of every character.

## Step 4: Handle Common Edge Cases

### Missing or Corrupt Files

If the PNG path is wrong, `ImageStream.FromFile` throws a `FileNotFoundException`. Wrap the loading code in a try‑catch block:

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### Low Confidence Scores

Sometimes OCR returns low confidence for noisy scans. You can filter symbols before exporting:

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

This ensures the JSON only contains reasonably reliable characters—useful when you feed the data into downstream validation pipelines.

### Large Files & Memory

Processing a multi‑megabyte PNG can spike memory usage. Consider streaming the image in chunks or using `OcrEngine.RecognizeAsync` (available in newer Aspose versions) to keep the UI responsive.

## Step 5: Extend the Solution (Optional)

- **Batch processing**: Loop over a directory of PNGs and generate a matching JSON per file.
- **Database storage**: Insert the JSON into a SQL `NVARCHAR(MAX)` column for later analytics.
- **Language selection**: Set `ocrEngine.Language = OcrLanguage.Spanish;` if you need non‑English support.

All these extensions follow the same **how to perform OCR** pattern we established—initialize, recognize, export, and persist.

## Frequently Asked Questions

**Q: Does this work with JPG or TIFF?**  
A: Absolutely. `ImageStream.FromFile` auto‑detects the format, so you can replace the PNG with any supported raster image.

**Q: What if I need to extract text from a PDF?**  
A: Convert each PDF page to an image first (e.g., using `Aspose.PDF`) and then feed the PNG into the OCR flow described here.

**Q: Can I get the OCR result as XML instead of JSON?**  
A: Yes. Aspose.OCR also ships with an `XmlExporter`. Swap `JsonExporter` for `XmlExporter` and adjust the file extension.

## Conclusion

We’ve walked through **how to perform OCR** in C# from start to finish, showing you how to **extract text from image**, **recognize text from PNG**, and **write JSON file C#** without a hitch. The complete, runnable example lives in the code snippets above, and you now understand the why behind each step—initializing the engine, handling edge cases, and persisting results.

Next, you might explore batch OCR pipelines, integrate the JSON output with Azure Cognitive Search, or experiment with custom language models. The sky’s the limit once you’ve mastered the basics of OCR in C#.

If you ran into any snags or have ideas for further extensions, drop a comment below. Happy coding, and enjoy turning those pixelated scans into clean, searchable data!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}