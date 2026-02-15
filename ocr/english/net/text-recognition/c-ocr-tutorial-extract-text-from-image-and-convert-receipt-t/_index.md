---
category: general
date: 2026-02-14
description: 'c# ocr tutorial: Learn how to extract text from image, include confidence
  scores, and convert a receipt to JSON using Aspose OCR.'
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- how to include confidence
- convert receipt to json
- Aspose OCR C#
language: en
og_description: 'c# ocr tutorial: Step‑by‑step guide to extract text from image, include
  confidence scores, and convert a receipt to JSON with Aspose OCR.'
og_title: c# ocr tutorial – Extract Text from Image and Convert Receipt to JSON
tags:
- OCR
- C#
- Aspose
title: c# ocr tutorial – Extract Text from Image and Convert Receipt to JSON
url: /net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-convert-receipt-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR Tutorial – Turn a Receipt Image into Structured JSON

Ever wondered how to **extract text from image** files in C# without wrestling with low‑level pixel math? Maybe you’re building a bookkeeping app and need to pull line‑items from a scanned receipt. The good news is you don’t have to reinvent the wheel—Aspose OCR does the heavy lifting for you.

In this **c# ocr tutorial** we’ll walk through everything you need: loading a receipt picture, telling the engine to **include confidence** values, and finally **convert receipt to json** so your downstream logic can consume it like a regular object. By the end you’ll have a ready‑to‑run console program that prints a nicely‑structured JSON string.

## What You’ll Need

- **.NET 6.0** or later (the code works on .NET Framework too, but the newer SDK gives you nice implicit usings).  
- A valid **Aspose.OCR** NuGet package (`dotnet add package Aspose.OCR`).  
- An image of a receipt (JPEG, PNG, BMP – anything the library supports).  
- A favorite IDE (Visual Studio, Rider, or VS Code).  

That’s it. No extra native libraries, no OCR training data, nothing fancy. Let’s dive in.

---

## c# OCR Tutorial: Step‑by‑Step Implementation

Below is the complete, runnable program. Feel free to copy‑paste it into a new console project and hit **F5**.

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
            // Step 1 – Create the OCR engine.
            // The Engine class is the entry point; it holds all the settings.
            var ocrEngine = new Engine();

            // Step 2 – Load the receipt image from disk.
            // ImageStream.FromFile reads the file into a format the engine understands.
            var receiptImage = ImageStream.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

            // Step 3 – Tell the engine what we want in the JSON output.
            // IncludeBoundingBoxes gives us the location of each word,
            // IncludeConfidence adds a confidence score (0‑100),
            // IncludeWords makes the JSON human‑readable.
            var jsonOutputOptions = new JsonOutputOptions
            {
                IncludeBoundingBoxes = true,
                IncludeConfidence = true,
                IncludeWords = true
            };

            // Step 4 – Run OCR and receive a JSON string.
            // RecognizeToJson does the recognition and serialises the result.
            string jsonResult = ocrEngine.RecognizeToJson(receiptImage, jsonOutputOptions);

            // Step 5 – Show the JSON result on the console.
            // In a real app you might write this to a file or a database.
            Console.WriteLine(jsonResult);
        }
    }
}
```

> **Pro tip:** Replace `YOUR_DIRECTORY/receipt.jpg` with the absolute path to your test receipt. If you’re using a relative path, make sure the working directory of the console app points to the folder containing the image.

### Why Each Step Matters

| Step | Purpose | How it helps you |
|------|---------|------------------|
| **Create the OCR engine** | Instantiates the core processing object. | You can later tweak language, DPI, or custom dictionaries if needed. |
| **Load the receipt image** | Converts a file into an `ImageStream` that Aspose can read. | Guarantees the engine sees the exact pixels you want to analyse. |
| **Define JSON output options** | Configures the shape of the result. | `IncludeConfidence` is crucial for downstream validation; you can discard low‑confidence words. |
| **Recognize to JSON** | Executes the OCR and serialises the data in one call. | Saves you from writing manual parsers; you get a clean, structured string. |
| **Display the JSON** | Quick visual feedback to verify everything worked. | Lets you spot formatting issues early, before you integrate the data. |

---

## How to Include Confidence Scores in Your OCR Results

If you’ve ever tried OCR, you know it’s not always perfect. **How to include confidence** is a common question because developers need to decide whether to trust a word or ask the user to confirm it.

In the code above the line:

```csharp
IncludeConfidence = true,
```

does exactly that. The resulting JSON will contain a `confidence` field for each recognized word, typically ranging from `0` (no confidence) to `100` (perfect match). Here’s a tiny excerpt of what the output looks like:

```json
{
  "pages": [
    {
      "words": [
        {
          "text": "Total",
          "boundingBox": { "x": 45, "y": 320, "width": 50, "height": 20 },
          "confidence": 98
        },
        {
          "text": "$12.34",
          "boundingBox": { "x": 110, "y": 320, "width": 60, "height": 20 },
          "confidence": 95
        }
      ]
    }
  ]
}
```

You can now write logic like:

```csharp
if (word.confidence < 80) { /* flag for manual review */ }
```

That simple check dramatically improves the reliability of any downstream accounting workflow.

---

## Extract Text from Image Using Aspose OCR – A Quick Test

Before you commit the whole JSON pipeline, it’s useful to verify that the plain text extraction works. You can temporarily set `IncludeWords = true` **and** turn off the other flags:

```csharp
var jsonOutputOptions = new JsonOutputOptions
{
    IncludeBoundingBoxes = false,
    IncludeConfidence = false,
    IncludeWords = true
};
```

Running the program will now print a compact JSON that only contains the `text` fields, something like:

```json
{
  "pages": [
    {
      "words": [
        { "text": "Item" },
        { "text": "Qty" },
        { "text": "Price" }
        // …
      ]
    }
  ]
}
```

If you see the expected words, you know the OCR engine can read your receipt image correctly. From there you can re‑enable the confidence and bounding‑box options for a richer output.

---

## Convert Receipt to JSON – What the Structure Means

The **convert receipt to json** step is more than just stringifying text. The JSON produced by Aspose OCR follows a hierarchical model:

- **pages** – an array (most receipts are a single page, but the format handles multi‑page PDFs).
- **words** – each word object carries:
  - `text` – the recognized string.
  - `boundingBox` – coordinates that let you highlight the word on the original image.
  - `confidence` – the score we discussed earlier.

Why is this useful? Imagine you’re building a UI that shows the scanned receipt side‑by‑side with the extracted data. You can draw rectangles using the `boundingBox` values and colour‑code them based on `confidence`. Users get a visual cue about which parts the engine was unsure about.

If you need a flatter structure (e.g., just a list of line items), you can post‑process the JSON with LINQ:

```csharp
var receipt = JsonSerializer.Deserialize<ReceiptRoot>(jsonResult);
var lineItems = receipt.Pages
    .SelectMany(p => p.Words)
    .Where(w => w.Confidence > 80) // filter low‑confidence words
    .Select(w => w.Text)
    .ToList();
```

---

## Full Working Example – All Pieces Together

Below is the **entire** source file, ready to compile. It includes a small helper class that mirrors the JSON structure, making deserialization painless.

```csharp
using System;
using System.Text.Json;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    // Helper POCOs matching the JSON schema
    public class ReceiptRoot
    {
        public Page[] Pages { get; set; }
    }

    public class Page
    {
        public Word[] Words { get; set; }
    }

    public class Word
    {
        public string Text { get; set; }
        public BoundingBox BoundingBox { get; set; }
        public int Confidence { get; set; }
    }

    public class BoundingBox
    {
        public int X { get; set; }
        public int Y { get; set; }
        public int Width { get; set; }
        public int Height { get; set; }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var engine = new Engine();

            // 2️⃣ Load receipt image (adjust the path!)
            var image = ImageStream.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

            // 3️⃣ Configure JSON output – we want everything.
            var options = new JsonOutputOptions
            {
                IncludeBoundingBoxes = true,
                IncludeConfidence = true,
                IncludeWords = true
            };

            // 4️⃣ Perform OCR and get JSON string
            string json = engine.RecognizeToJson(image, options);

            // 5️⃣ Show raw JSON (great for debugging)
            Console.WriteLine("--- Raw JSON Output ---");
            Console.WriteLine(json);

            // 6️⃣ Optional: deserialize to C# objects for further processing
            var receipt = JsonSerializer.Deserialize<ReceiptRoot>(json);
            Console.WriteLine("\n--- High‑confidence words (>90) ---");
            foreach (var word in receipt.Pages[0].Words)
            {
                if (word.Confidence > 90)
                    Console.WriteLine($"{word.Text} (confidence: {word.Confidence}%)");
            }
        }
    }
}
```

**Expected console output** (truncated for brevity):

```
--- Raw JSON Output ---
{
  "pages":[
    {
      "words":[
        {"text":"Subtotal","boundingBox":{"x":30,"y":250,"width":80,"height":20},"confidence":97},
        {"text":"$45.00","boundingBox":{"x":120,"y":250,"width":50,"height":20},"confidence":95},
        ...
      ]
    }
  ]
}

--- High‑confidence words (>90) ---
Subtotal (

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}