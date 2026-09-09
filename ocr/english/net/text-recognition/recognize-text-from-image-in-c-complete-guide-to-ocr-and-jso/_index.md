---
category: general
date: 2026-01-10
description: Learn how to recognize text from image, extract text coordinates, and
  convert receipt to JSON using Aspose OCR in C#. Step‑by‑step tutorial.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: en
og_description: recognize text from image in C# using Aspose OCR. This guide shows
  how to extract text, get coordinates, and convert receipt to JSON.
og_title: recognize text from image – Full C# OCR Tutorial
tags:
- OCR
- C#
- Aspose
title: recognize text from image in C# – Complete Guide to OCR and JSON
url: /net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# recognize text from image – Full C# OCR Tutorial

Ever needed to recognize text from image but weren’t sure which library to pick? You’re not alone. In many real‑world apps—expense trackers, receipt scanners, or document archivers—extracting text reliably is the first hurdle.  

In this tutorial we’ll walk through **how to extract text**, pull out its bounding boxes, and finally **convert receipt to JSON** using Aspose.OCR for .NET. By the end you’ll have a self‑contained C# project that takes a photo of a receipt and spits out a tidy JSON file with confidence scores and coordinates.

## What You’ll Need

Before we dive in, make sure you have the following on your machine:

- **.NET 6.0 SDK** (or any later version). Older frameworks work too, but .NET 6 is the sweet spot for modern libraries.
- **Visual Studio 2022** or VS Code with the C# extension.
- **Aspose.OCR for .NET** NuGet package (`Aspose.OCR` and `Aspose.OCR.Output`). You can install it via the Package Manager Console:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- A sample receipt image (e.g., `receipt.jpg`) placed in a folder you’ll reference later.

That’s it—no extra SDKs, no native binaries, just pure managed code.

## Step 1: Create a New Console Project

First things first, spin up a console app. It’s the quickest way to test OCR without UI overhead.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Pro tip:** Keep the project folder tidy; create a sub‑folder called `Resources` and drop `receipt.jpg` there. It makes path handling painless.

## Step 2: Load the Receipt Image

Now we actually **recognize text from image**. The first step is to point the OCR engine at the file.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

Why do we wrap the load in a simple existence check? Because in production you often deal with user uploads that might be missing or corrupted. Catching the issue early saves you from cryptic exceptions later.

## Step 3: Perform OCR – **recognize text from image**

With the image in memory, we ask Aspose to **recognize text from image**. This operation is synchronous and returns a rich result set.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

Behind the scenes Aspose runs a neural network trained on millions of characters. The engine populates `ocrEngine.Text`, `ocrEngine.RecognitionResult`, and a collection of `OcrRegion` objects that hold coordinates. That’s exactly what we need for the next step.

## Step 4: **How to extract text** – Getting the raw string

If you only care about the plain text (maybe for a quick search), you can pull it straight from the engine:

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

You’ll notice line breaks where the OCR detected paragraph boundaries. In many receipt‑scanning scenarios the raw string is enough to pull out totals, dates, or vendor names using simple regexes.

## Step 5: **extract text coordinates** – Bounding boxes for each word

Often you need to know *where* on the image a particular piece of text lives—for example, to highlight the total amount in a UI. Aspose gives us that via `OcrRegion` objects.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

Notice we’re looping over **extract text coordinates** for every recognized segment. The coordinates are relative to the original image, so you can overlay them in a graphics canvas or HTML `<canvas>` element.

## Step 6: **convert receipt to JSON** – Saving detailed results

Now comes the part that ties everything together: we want a machine‑readable structure that includes the text, confidence scores, and the bounding boxes. Aspose ships with `JsonSaveOptions` that make this a breeze.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

The resulting file looks something like this (trimmed for brevity):

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

You now have a **convert receipt to JSON** artifact that can be fed into downstream services—think expense‑report APIs, analytics pipelines, or even a simple UI that draws rectangles around each word.

## Full Working Example

Putting all the pieces together, here’s the complete `Program.cs` you can copy‑paste into your project:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

Run the program (`dotnet run`) and watch the console output. Open `Resources/receipt.json` to verify the structure.

## Common Questions & Edge Cases

- **What if the image is blurry?**  
  Aspose OCR works best with 300 dpi or higher. If you get low confidence scores, consider applying a sharpening filter before feeding the image to the engine.

- **Can I recognize multiple languages?**  
  Yes. Set `ocrEngine.Language = Language.English | Language.Spanish;` before calling `Recognize()`.

- **How do I limit output to only numbers (e.g., totals)?**  
  After you have the plain text, run a regex like `\d+\.\d{2}` on `ocrEngine.Text`. Because we already have coordinates, you can map the matched string back to its region for visual highlighting.

- **Is the JSON format customizable?**  
  The `JsonSaveOptions` class exposes a handful of flags. If you need a completely custom schema, you can iterate over `ocrEngine.RecognitionResult.Regions` and serialize the objects yourself with `System.Text.Json`.

## Conclusion

We’ve just demonstrated how to **recognize text from image** in C# using Aspose.OCR, **how to extract text**, pull out **extract text coordinates**, and finally **convert receipt to JSON**. The entire flow lives in a single, easy‑to‑run console app, making it perfect for prototypes or as a building block in larger systems.

Next steps? Try feeding the JSON into a front‑end that draws the bounding boxes, or plug the output into an expense‑report service. You could also experiment with different image formats (PNG, TIFF) or batch‑process a folder of receipts.

Got more questions about OCR, Aspose, or JSON handling? Drop a comment below, and happy coding! 

![Receipt image example for recognize text from image](receipt.jpg "Receipt image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}