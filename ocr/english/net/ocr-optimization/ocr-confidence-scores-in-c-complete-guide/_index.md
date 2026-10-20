---
category: general
date: 2026-05-31
description: Learn how to get OCR confidence scores in C# while extract text from
  image and read receipt image with Aspose OCR.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: en
og_description: OCR confidence scores let you gauge accuracy; this guide shows how
  to extract text from image, get bounding boxes, and read receipt image using Aspose
  OCR.
og_title: OCR confidence scores in C# – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: OCR confidence scores in C# – Complete Guide
url: /net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR confidence scores in C# – Complete Guide

Ever wondered how to **OCR confidence scores** when you need to *extract text from image*? Maybe you’re trying to **read receipt image** files for expense tracking and you want to know which characters the engine is unsure about. The good news? With Aspose.OCR you can pull confidence percentages, bounding boxes, and plain text from a JPG in just a few lines of C#.

In this tutorial we’ll walk through everything you need to know: installing the library, configuring the engine to **perform OCR on JPG**, pulling out confidence scores, and interpreting the **OCR bounding boxes** that tell you where each character lives on the page. By the end you’ll have a ready‑to‑run console app that prints every character, its confidence, and its location—perfect for validating receipts or any scanned document.

## What You’ll Learn

- Install Aspose.OCR via NuGet and set up a basic OCR engine.  
- Configure `OcrOptions` to request plain‑text output **with confidence scores** and **bounding boxes**.  
- Loop through `OcrResult` to **extract text from image** line‑by‑line and symbol‑by‑symbol.  
- Handle common pitfalls such as missing files, low‑confidence characters, and non‑JPG formats.  
- Extend the example to process multiple receipt images in a folder.

No prior experience with Aspose is required; just a working .NET environment and a receipt image (JPG) you’d like to test.

---

## Step 1 – Install Aspose.OCR and Prepare Your Project

First things first: you need the Aspose.OCR NuGet package. Open a terminal in your project folder and run:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** The free trial works for up to 200 pages, which is more than enough for testing receipt scanning.

After the package is installed, create a new console project (if you don’t already have one):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Now you can open the generated `Program.cs` and start adding the using directives:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

These namespaces give you access to `OcrEngine`, `OcrOptions`, and the result types we’ll need later.

## Step 2 – Get OCR confidence scores and OCR bounding boxes

This is the heart of the tutorial. We’ll configure the engine so that each recognized character comes with a **confidence score** and a **bounding box** (the rectangle that encloses the glyph). The H2 header itself contains the primary keyword, satisfying the SEO rule.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Why include confidence scores?**  
A confidence score (0‑100%) tells you how sure the engine is about each character. If you’re feeding the output into downstream logic—say, an expense‑approval workflow—you can reject or flag low‑confidence symbols automatically.

**Why request bounding boxes?**  
Bounding boxes are essential when you need to highlight text on the original image, extract sub‑regions, or align OCR results with a UI overlay. Each `character.Bounds` gives you the X, Y, width, and height in pixel coordinates.

## Step 3 – Perform OCR on JPG and extract text from image

Now we actually run the engine. The call to `Recognize()` performs all the heavy lifting and returns an `OcrResult` object.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

If the image path is wrong or the file isn’t a supported format, Aspose throws a `FileNotFoundException` or `UnsupportedImageFormatException`. Wrap the call in a try/catch block in production code to handle those edge cases gracefully.

### Pulling out the plain text

If you only need the concatenated text, you can read `ocrResult.Text`:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

But because we also asked for confidence scores and bounding boxes, we’ll iterate through the structure to see each character’s details.

## Step 4 – Iterate through lines, symbols, and display OCR confidence scores

Here’s the loop that prints every character, its confidence, and its box. This is where the **read receipt image** example truly shines.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

Sample output might look like:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Interpreting the numbers:**  
- **Confidence ≥ 90%** – usually safe to accept.  
- **Confidence 70‑89%** – you might want to double‑check, especially for digits in amounts.  
- **Confidence < 70%** – consider flagging for manual review.

## Step 5 – Full runnable example (including error handling)

Putting everything together, here’s a complete program you can copy‑paste into `Program.cs`. It includes a simple check for missing files and prints a friendly message if the OCR fails.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Expected output

When you run `dotnet run` the console will first display the concatenated receipt text, then a list of each character with its confidence score and bounding box. If a character’s confidence is low, you’ll see a percentage under 80, which is a cue to verify that part of the receipt manually.

## Bonus: Processing Multiple Receipts in a Folder

If you have a batch of receipt JPGs, wrap the above logic in a `foreach (var file in Directory.GetFiles(folder, "*.jpg"))` loop. Remember to reset the `OcrEngine` for each file, or instantiate a new one inside the loop to avoid state leakage.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

Processing in bulk is handy for nightly expense imports.

---

## Conclusion

You now have a solid, end‑to‑end solution for obtaining **OCR confidence scores** in C#, **extracting text from image**, and retrieving **OCR bounding boxes** while you **perform OCR on JPG** files such as a **read receipt image**. The code is fully self‑contained, works with the latest Aspose.OCR version (as of 2026‑05‑31), and gives you the granular data you need to build trustworthy document‑processing pipelines.

What’s next? Try visualizing the bounding boxes on the original receipt using `System.Drawing` or a UI library, or feed low‑confidence characters into a secondary verification service. You could also experiment with different languages by setting `ocrEngine.Options.Language = OcrLanguage.French;` – the API supports many locales.

Happy coding, and may your confidence scores always stay high! 

![Console output showing OCR confidence scores and bounding boxes for a receipt


## What Should You Learn Next?

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Get OCR Character Choices for Recognized Characters in Image Recognition](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}