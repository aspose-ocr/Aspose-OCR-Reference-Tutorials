---
category: general
date: 2026-02-17
description: How to batch OCR multiple PDFs and images in C# using Aspose OCR. Learn
  to extract text from pdf, convert pdf to text, and recognize text from images.
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: en
og_description: How to batch OCR multiple documents in C# with Aspose OCR. Get step‑by‑step
  code to extract text from pdf, convert pdf to text, and recognize text from images.
og_title: How to batch OCR files in C# – Complete Guide
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: How to batch OCR files in C# – Full Code Example
url: /net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to batch OCR files in C# – Complete Guide

Ever wondered **how to batch OCR** a stack of PDFs and image scans without writing a separate loop for each file? You're not alone. Most developers hit this wall when they need to pull text from dozens of pages in one go. The good news? With Aspose OCR you can feed a collection of files to a single engine and let it do the heavy lifting.  

In this tutorial we’ll walk through a practical solution that lets you **extract text from pdf**, **convert pdf to text**, and **recognize text from images** all in one batch run. By the end you’ll have a ready‑to‑run console app that prints the OCR result for every page, and you’ll understand the why behind each step so you can adapt it to your own projects.

## Prerequisites – What You Need Before We Start

- **.NET 6.0 or later** (the code works on .NET Framework too, but .NET 6+ is recommended)
- **Aspose.OCR NuGet package** – install it with `dotnet add package Aspose.OCR`
- A couple of sample files: a multi‑page PDF (`doc1.pdf`) and a scanned TIFF (`doc2.tif`). Place them in a folder you can reference, e.g., `C:\OCRSamples`.
- Basic C# knowledge – you should be comfortable with `using` statements and collections.

> Pro tip: If you don’t have a license, Aspose offers a free temporary key that removes the 100‑page limit during development.

## Step 1: Set Up the Project and Import Namespaces

First, create a new console project (or add to an existing one) and bring in the required namespaces.

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **Why this matters:** Importing `Aspose.OCR.Image` gives you the convenient `ImageStream.FromFile` method, which automatically splits PDF pages into separate image streams. That’s the secret sauce that makes batch processing painless.

## Step 2: Initialise the OCR Engine

The engine is the workhorse that talks to the underlying OCR engine. You only need one instance for the whole batch.

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Explanation:** Re‑using the same `OcrEngine` reduces memory churn and speeds up processing because the native libraries stay loaded between pages.

## Step 3: Build a List of Image Streams

Here we gather every document we want to process. `ImageStream.FromFile` is smart enough to break a PDF into individual pages, so a three‑page PDF becomes three separate streams behind the scenes.

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **Edge case:** If you have a mixture of PDFs, TIFFs, JPEGs, or PNGs, just add them to the same list – Aspose handles the format detection automatically.

## Step 4: Run the Batch OCR Operation

Now we hand the list over to the engine. `RecognizeBatch` returns a collection of `OcrResult` objects, one per page.

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **Why batch?** Running OCR page‑by‑page in a manual loop forces the engine to re‑initialise each time, which can double processing time. `RecognizeBatch` keeps the engine warm and streams results back as they become available.

## Step 5: Output the Recognized Text

Finally, we loop through the results and write each page’s text to the console. This is where you can replace `Console.WriteLine` with file writes, database inserts, or any other downstream action.

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### Expected Console Output

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

If you run the program with the sample files, you should see a block of text for each page, proving that you’ve successfully **extract text scanned pdf** content in a single pass.

## Handling Common Pitfalls

| Problem | Why It Happens | Quick Fix |
|---------|----------------|-----------|
| **Out‑of‑memory errors** | Large PDFs generate many high‑resolution images. | Limit the DPI when loading PDFs: `ocrEngine.Settings.ImageDpi = 200;` |
| **Garbage characters** | The source scan is low‑quality or uses an unsupported language. | Set the language explicitly: `ocrEngine.Language = Language.English;` |
| **Partial results** | The batch list contains a corrupted file. | Wrap `RecognizeBatch` in a try/catch and log `e.Message` for the offending file. |
| **Performance bottleneck** | Running on a single thread on a multi‑core machine. | Use `Parallel.ForEach` with separate `OcrEngine` instances per thread (advanced). |

## Bonus: Saving OCR Results to Text Files

If you prefer to keep a separate `.txt` file per page, just add a tiny write block inside the loop:

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

Now you’ve turned **convert pdf to text** into a tidy folder of plain‑text files—perfect for downstream indexing or search.

## Full Working Example

Below is the complete, copy‑and‑paste‑ready program. No hidden dependencies, no external scripts.

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

Run `dotnet run` from the project folder and watch the console fill with the extracted text. That’s **how to batch OCR** a collection of documents in just a few lines of C#.

## What We Covered – Quick Recap

- Set up a .NET console app and installed Aspose.OCR.  
- Created a single `OcrEngine` instance to keep the process efficient.  
- Built a list of `ImageStream` objects that automatically split PDFs into pages.  
- Executed `RecognizeBatch` to **extract text from pdf** and other image formats in one go.  
- Printed the results and optionally saved them as individual `.txt` files, completing the **convert pdf to text** workflow.  

## Next Steps and Related Topics

- **Scale up**: Use `Parallel.ForEach` with a pool of `OcrEngine` objects to process hundreds of files concurrently.  
- **Language packs**: Swap `Language.English` for `Language.French` or load a custom dictionary when you need to **recognize text from images** in other languages.  
- **Post‑processing**: Pipe the OCR output through a spell‑checker or a natural‑language parser to improve accuracy for scanned contracts.  
- **Alternative libraries**: Compare Aspose OCR with Tesseract.NET if you’re looking for an open‑source option—both can **extract text scanned pdf** but differ in licensing and out‑of‑the‑box accuracy.

---

![how to batch OCR example](alt="how to batch OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}