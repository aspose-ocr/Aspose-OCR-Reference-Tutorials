---
category: general
date: 2026-01-15
description: Convert image to JSON using Aspose OCR in C#. Learn how to extract text
  from image, get JSON bounding boxes and recognize receipt image.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: en
og_description: Convert image to JSON using Aspose OCR in C#. Step‑by‑step guide to
  extract text from image, recognize receipt image, and get JSON bounding boxes.
og_title: Convert Image to JSON with Aspose OCR C# Guide
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Convert Image to JSON with Aspose OCR C# Guide
url: /net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert Image to JSON with Aspose OCR C# Guide

Ever needed to **convert image to JSON** but weren't sure which library could give you both the raw text and the exact word coordinates? You’re not alone. Many developers hit this wall when they try to extract text from image files—especially receipts—while also needing a machine‑readable JSON payload for downstream processing.

In this tutorial we’ll walk through a complete **Aspose OCR C# example** that shows you how to extract text from image, recognize receipt image, and output **JSON bounding boxes** for every word. By the end you’ll have a ready‑to‑run console app that prints a nicely formatted JSON string you can feed into any API, database, or analytics pipeline.

> **What you’ll walk away with**  
> • A fully functional C# project that **converts image to JSON**  
> • Insight into why we enable `IncludeBoundingBoxes` (it’s the key to `json bounding boxes`)  
> • Tips for handling different image formats and languages  

Let’s get started.

---

## What You’ll Need

Before we dive into code, make sure you have the following prerequisites installed:

- **.NET 6.0 SDK** (or any later version) – the code targets .NET 6 but works on .NET Framework 4.7+ as well.  
- **Aspose.OCR for .NET** NuGet package – you can pull it via `dotnet add package Aspose.OCR`.  
- A sample receipt image (`receipt.jpg`) placed in a folder you can reference from your project.  
- Visual Studio 2022, VS Code, or any IDE you prefer.

No other external services are required; everything runs locally.

---

## Convert Image to JSON – Overview

The core idea is simple: load an image, tell Aspose OCR to recognize English (or any supported language), ask it to include bounding boxes, and finally ask for the result in **JSON** format. The library does all the heavy lifting—OCR, layout analysis, and JSON serialization.

Here’s a high‑level diagram of the flow (imagine a tiny picture):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

That tiny diagram captures the entire pipeline we’ll implement.

---

## Step 1: Set Up the Project and Install Aspose OCR

First, create a new console project and pull in the Aspose OCR package.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** If you’re using Visual Studio, right‑click the project → *Manage NuGet Packages* → search for **Aspose.OCR** and install the latest stable version (currently 23.12).

---

## Step 2: Load the Image You Want to Recognize

We’ll use the `OcrImage.FromFile` method to read the receipt image. Make sure the path points to a real file; otherwise you’ll hit a `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

If your image lives next to the `.csproj`, you can simply use `"receipt.jpg"`.

---

## Step 3: Configure OCR Options for JSON Bounding Boxes

The magic happens when we enable `OutputFormat = OutputFormat.Json` **and** `IncludeBoundingBoxes = true`. The former tells Aspose to serialize the result as JSON, while the latter adds `x`, `y`, `width`, and `height` for every word—exactly what you need for `json bounding boxes`.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

You can also tweak `ocrOptions.Dpi` or `ocrOptions.Language` if you need higher resolution or a different language.

---

## Step 4: Perform the Recognition – Extract Text from Image

Now we call `Recognize`. The method returns an `OcrResult` object that contains the JSON string, raw text, and more.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

If you need to handle other languages, replace `Language.English` with `Language.Spanish`, `Language.French`, etc. Aspose supports over 30 languages out of the box.

---

## Step 5: Output the Result – Your JSON Payload

Finally, we print the JSON to the console. In a real app you’d probably write it to a file or push it to a service.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

Running the program should produce a JSON document similar to the snippet below.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Notice how each word now carries its **JSON bounding box**—perfect for feeding into a UI overlay or a downstream parser.

---

## Full Working Example

Below is the complete, copy‑paste‑ready program. No hidden parts, no external calls—just pure C#.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Watch out for:**  
> • **File path errors** – double‑check the image location.  
> • **Missing NuGet package** – ensure `Aspose.OCR` is referenced.  
> • **Unsupported image formats** – stick to JPEG, PNG, BMP, or TIFF for best results.

---

## Common Questions & Edge Cases

### Can I convert a **PDF page** to JSON instead of a JPEG?

Yes. Convert the PDF page to an image first (e.g., using `Aspose.PDF`), then feed that image into the same OCR pipeline. The JSON output will be identical because the OCR step only cares about raster data.

### What if the receipt is blurry?

Increase the DPI in `ocrOptions`. For example:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

Higher DPI may increase memory usage, so balance quality vs. performance.

### I need **multiple languages** on the same receipt (e.g., English + Spanish).

You can pass an array of languages:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose will attempt to recognize each language in the specified order.

### How do I write the JSON to a file?

Just replace the `Console.WriteLine` line with:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

Now you have a persistent file you can ship to other services.

---

## Visual Summary

![convert image to json example](convert-image-to-json.png "convert image to json example")

*The screenshot shows the console output of the JSON payload after running the demo.*

---

## Conclusion

We’ve just shown you how to **convert image to JSON** using Aspose OCR in C#. By configuring `OutputFormat` and `IncludeBoundingBoxes`, you can **extract text from image**, **recognize receipt image**, and obtain precise **JSON bounding boxes** for every word. The complete, runnable code lives in the snippet above, so you can drop it into any .NET project right now.

What’s next? Try feeding the JSON into a front‑end viewer that highlights each word, or push the data into a machine‑learning model that classifies line items on receipts. You could also experiment with other languages, higher DPI settings, or batch‑processing multiple images in a loop.

If you hit any snags, remember the tips about file paths, DPI, and language arrays. Feel free to leave a comment or open an issue on the GitHub repo you create for this demo. Happy coding, and enjoy turning pictures into structured JSON!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}