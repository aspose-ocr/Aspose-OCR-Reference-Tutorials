---
category: general
date: 2026-01-01
description: Учебник по OCR на C#, показывающий, как извлекать текст, загружать изображение
  для OCR и записывать JSON в файл с использованием Aspose.OCR – пошаговое руководство.
draft: false
keywords:
- c# OCR tutorial
- how to extract text
- write json to file
- load image for OCR
- OCR image to JSON
language: ru
og_description: Учебник по OCR на C#, который пошагово покажет, как извлекать текст
  из изображений, загружать изображение для OCR и записывать JSON в файл с помощью
  Aspose.OCR.
og_title: c# OCR tutorial – Извлечение текста и экспорт в JSON
tags:
- Aspose.OCR
- C#
- Text Extraction
title: C# OCR‑урок – извлечение текста из изображений и экспорт в JSON
url: /ru/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Извлечение текста из изображений и экспорт в JSON

Ever wondered how to extract text from a scanned invoice without spending hours writing custom parsers? You're not alone. In this **c# OCR tutorial** we’ll show you exactly how to load an image for OCR, run the recognition engine, and then **write JSON to file** so you can feed the data into downstream systems.

Imagine you have a folder of receipts, each named `receipt1.png`, `receipt2.png`, and you need a quick way to turn them into searchable JSON records. That's the problem we’ll solve, and by the end you’ll have a ready‑to‑run console app that does just that. No extra dependencies beyond Aspose.OCR, and no magic—just clear, reproducible steps.

> **What you’ll learn**
> - How to **load image for OCR** using Aspose.OCR.
> - The best way to **how to extract text** and get confidence scores.
> - Converting the OCR result into a nicely structured **OCR image to JSON** payload.
> - Safely **write JSON to file** and verify the output.

## Prerequisites

- .NET 6 SDK or later (the code works on .NET Core as well).  
- Visual Studio 2022 or any editor you prefer.  
- Aspose.OCR NuGet package (`Install-Package Aspose.OCR`).  
- An image file (PNG, JPG, BMP) you’d like to process – for demo we’ll use `invoice.png`.

If you’re missing any of these, grab the SDK from Microsoft’s site and add the NuGet package via the Package Manager Console:

```powershell
Install-Package Aspose.OCR
```

Now that the groundwork is set, let’s dive into the actual implementation.

## Step 1: c# OCR tutorial – Initialize the OCR Engine

Before we can **load image for OCR**, we need an instance of the engine that will drive the recognition process. The `OcrEngine` class is lightweight, but it’s good practice to wrap it in a `using` block so resources are released promptly.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine – this is the heart of the c# OCR tutorial
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow…
```

*Pro tip:* If you plan to process many images in a batch, reuse the same `OcrEngine` instance instead of creating a new one each time. It reduces memory churn and speeds things up.

## Step 2: Load image for OCR

Now we actually **load image for OCR**. Aspose.OCR supports a variety of formats, so you can point it at a PNG, JPEG, or even a multi‑page TIFF. The `OcrImage.FromFile` method reads the file and prepares it for recognition.

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the folder that holds your invoice.png
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);
```

> **Why this matters:** Loading the image separately lets you inspect its dimensions, DPI, or even pre‑process it (e.g., binarization) before sending it to the engine. If the image is corrupted, `FromFile` will throw a clear exception, which you can catch and log.

## Step 3: How to extract text – Run the recognition

With the image in hand, we can finally **how to extract text** from it. The `Recognize` method returns an `OcrResult` object that contains not only the plain text but also positional data and confidence scores for each word.

```csharp
        // Step 3: Perform OCR – this is the core of how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);
```

*Edge case:* Some PDFs contain invisible text layers. If you feed a PDF page rendered as an image, the engine may see nothing. In those cases, consider using Aspose.PDF to extract the hidden layer first, then fall back to OCR only when needed.

## Step 4: OCR image to JSON – Convert the result

The `OcrResult` class offers a convenient `ToJson()` helper that serializes the entire result set—including each word’s bounding box and confidence—into a JSON string. This is the cleanest way to achieve **OCR image to JSON** without writing your own serializer.

```csharp
        // Step 4: Convert the OCR result to JSON (includes words, confidence, locations)
        string jsonResult = ocrResult.ToJson();
```

If you prefer a custom schema, you can iterate over `ocrResult.Words` and build your own object, but for most scenarios the built‑in JSON is sufficient and already well‑structured.

## Step 5: Write JSON to file

Now comes the final piece of the puzzle: persisting the JSON payload. The `File.WriteAllText` method ensures the file is created (or overwritten) atomically. Be sure the target directory exists, otherwise you’ll hit a `DirectoryNotFoundException`.

```csharp
        // Step 5: Save the JSON output – this demonstrates write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);
```

*Tip:* If you need UTF‑8 with BOM or a different encoding, use the overload that accepts an `Encoding` argument.

## Step 6: Verify the output

A quick `Console.WriteLine` tells us the process completed successfully. You can also open the JSON file in a viewer to confirm the structure.

```csharp
        // Step 6: Inform the user that the JSON file has been saved
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### Expected JSON snippet

```json
{
  "Text": "Invoice #12345\nDate: 2025-12-31\nTotal: $250.00",
  "Words": [
    { "Text": "Invoice", "Confidence": 0.98, "Location": { "X": 10, "Y": 15, "Width": 80, "Height": 20 } },
    { "Text": "#12345", "Confidence": 0.96, "Location": { "X": 95, "Y": 15, "Width": 60, "Height": 20 } }
    // … more words …
  ]
}
```

The JSON includes each word’s location, which is handy if you later want to highlight text in a UI.

## Full Working Example

Below is the complete, copy‑and‑paste‑ready program. Replace `YOUR_DIRECTORY` with the actual path where your image resides.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to recognize
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR – how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 4: Convert the result to JSON (OCR image to JSON)
        string jsonResult = ocrResult.ToJson();

        // Step 5: Write JSON to file – write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);

        // Step 6: Verify
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

Run the program (`dotnet run` from the project folder) and you’ll find `invoice.json` alongside your original PNG.

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **FileNotFoundException** when loading the image | Path typo or missing file | Use `Path.Combine` and check `File.Exists` before calling `FromFile`. |
| **Low confidence scores** | Poor image quality, low DPI | Pre‑process with `ocrImage.AdjustContrast` or upscale the image to 300 DPI. |
| **JSON file empty** | `ocrResult` returned null (engine failed) | Verify that the image format is supported and that the license (if any) is correctly applied. |
| **Performance bottleneck on large batches** | Re‑creating `OcrEngine` each iteration | Reuse a single `OcrEngine` instance across the batch, disposing only at the end. |

## Next Steps

Now that you’ve mastered the **c# OCR tutorial**, you might want to:

- **Batch process** an entire folder and aggregate the JSON files into a single database.
- **Integrate** the output with Azure Cognitive Search for searchable PDFs.
- **Add language support** by setting `ocrEngine.Language = OcrLanguage.Spanish` (or any supported language).
- **Post‑process** the JSON to extract tables or key‑value pairs using regular expressions.

Each of these extensions builds on the core concepts we covered: loading images for OCR, extracting text, converting to JSON, and writing that JSON to disk.

---

### Conclusion

In this **c# OCR tutorial** we walked through every step required to **load image for OCR**, **how to extract text**, transform the result into an **OCR image to JSON** payload, and finally **write JSON to file**. The complete code example is ready to drop into any .NET project, and the explanations give you the context you need to adapt the solution to real‑world scenarios.

Give it a try with your own set of receipts or invoices—tweak the image preprocessing, experiment with different languages, and watch the JSON output grow. If you hit any snags, revisit the pitfalls table or drop a comment below. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}