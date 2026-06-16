---
category: general
date: 2026-02-22
description: How to batch OCR JPEG images in C# with Aspose.OCR. Learn to extract
  text from jpg, convert jpg to txt, and batch process images efficiently.
draft: false
keywords:
- how to batch ocr
- extract text from jpg
- convert jpg to txt
- batch process images
- c# ocr example
language: en
og_description: How to batch OCR JPEG images in C# using Aspose.OCR. This tutorial
  shows you how to extract text from jpg, convert jpg to txt, and batch process images
  in minutes.
og_title: How to Batch OCR JPEG Images in C# – Complete Guide
tags:
- OCR
- C#
- Aspose
- Image Processing
title: How to Batch OCR JPEG Images in C# – Complete Guide
url: /net/text-recognition/how-to-batch-ocr-jpeg-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Batch OCR JPEG Images in C# – Complete Guide

Ever wondered **how to batch OCR** a folder full of pictures without writing a separate program for each file? In this guide we’ll show you exactly **how to batch OCR** JPEG files using Aspose.OCR, so you can **extract text from jpg** and **convert jpg to txt** with just a few lines of code.  

If you’ve ever stared at a directory of scanned invoices and thought, “There’s got to be a faster way,” you’re in the right place. We’ll walk through every step, explain why each piece matters, and even sprinkle in a few pro tips for handling large batches.

## What You’ll Build

By the end of this tutorial you’ll have a small console application that:

* Scans a given directory for `*.jpg` files.  
* Sends each image through the Aspose OCR engine (GPU‑accelerated if you have a capable card).  
* Writes the recognized text to a `.txt` file that sits next to the original picture.  

No external services, no manual copy‑pasting—just pure C# and a reliable OCR library.

### Prerequisites

* .NET 6.0 or later (the code works on .NET Framework 4.8 as well).  
* Visual Studio 2022 or any editor that supports C#.  
* An Aspose.OCR NuGet package (free trial works for testing).  

If you’re missing any of those, pause now and install them; the rest of the guide assumes they’re already in place.

![How to batch OCR example](/images/how-to-batch-ocr.png "how to batch ocr diagram")

## Step 1: Install the Aspose.OCR NuGet Package

First thing’s first—your project needs the OCR library. Open a terminal in the solution folder and run:

```bash
dotnet add package Aspose.OCR
```

Or use the NuGet Package Manager UI in Visual Studio. This pulls in everything you need, including the GPU‑enabled binaries if your machine supports them.

> **Pro tip:** If you plan to run this on a server without a GPU, set `UseGpu = false` later; the engine will fall back to CPU automatically.

## Step 2: Configure the OCR Engine

Creating and configuring the `OcrEngine` is where the magic starts. You’ll tell the engine which language to expect, whether to use the GPU, and what format the output should be.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 2: Initialize and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most documents; change if you need another language.
    Language = Language.English,

    // Enable GPU for faster processing on supported hardware.
    UseGpu = true,

    // We only need plain text for our .txt files.
    OutputFormat = OutputFormat.Text
};
```

**Why this matters:** Setting `Language` improves accuracy because the engine can narrow down character sets. Enabling `UseGpu` can cut processing time by half on a modern graphics card, which is a real win when you’re **batch processing images**.

## Step 3: Recognize All JPEG Files in a Folder

Now we let Aspose do the heavy lifting. The static `BatchProcessor.RecognizeFolder` method walks the directory, runs OCR on each matching file, and returns a collection of results.

```csharp
using System.Collections.Generic;

// ...

// Step 3: Run OCR on every *.jpg in the target directory
IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
    ocrEngine,
    @"C:\Images\Invoices",   // <-- replace with your folder path
    searchPattern: "*.jpg"); // Only JPEG files are processed
```

**Edge case handling:** If the folder contains sub‑folders, you can add a `SearchOption.AllDirectories` overload (or manually recurse) to make sure you don’t miss any files.

## Step 4: Write Each Result to a Matching `.txt` File

The `OcrResult` objects contain the original file path and the recognized text. Loop through them, change the extension, and write the output.

```csharp
using System.IO;

// ...

// Step 4: Persist OCR results as .txt files next to the source images
foreach (var result in ocrResults)
{
    // Change "image.jpg" → "image.txt"
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");

    // Save the extracted text
    File.WriteAllText(txtFilePath, result.Text);
}
```

That’s it—each JPEG now has a sibling text file that you can feed into downstream processes, search indexes, or simply archive.

## Step 5: Run the Application and Verify Output

Compile and run the program:

```bash
dotnet run
```

Assuming the folder contains `invoice1.jpg` and `receipt2.jpg`, you should see `invoice1.txt` and `receipt2.txt` appear alongside them. Open any of the `.txt` files; you’ll find the raw OCR output, e.g.:

```
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

If the text looks garbled, double‑check that the source images are high‑contrast and that the `Language` property matches the document language.

## Step 6: Advanced Tweaks (Optional)

### a) Handling Low‑Quality Scans

Sometimes JPEGs are noisy. You can pre‑process images with Aspose.Imaging or any other library:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

// Example: increase contrast before OCR
using (var image = Image.Load(result.SourceFilePath))
{
    image.Contrast = 30; // boost contrast
    image.Save(result.SourceFilePath); // overwrite or save to temp file
}
```

### b) Parallelizing the Batch

If you have many files and a multi‑core CPU, wrap the loop in `Parallel.ForEach`:

```csharp
Parallel.ForEach(ocrResults, result =>
{
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
    File.WriteAllText(txtFilePath, result.Text);
});
```

Just be aware that the Aspose OCR engine itself isn’t thread‑safe; you’d need a separate `OcrEngine` instance per thread or use a concurrent queue.

### c) Logging and Error Handling

A robust solution logs failures so you can retry later:

```csharp
try
{
    // OCR and write logic here
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {result.SourceFilePath}: {ex.Message}");
    // Optionally write to a log file
}
```

## Complete Working Example

Putting everything together, here’s the full program you can copy‑paste into a new Console App:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create and configure the OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = Language.English,
            UseGpu = true,
            OutputFormat = OutputFormat.Text
        };

        // 2️⃣ Recognize all JPEG images in the target folder
        IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
            ocrEngine,
            @"C:\Images\Invoices",   // <-- change to your directory
            searchPattern: "*.jpg");

        // 3️⃣ Write each OCR result to a matching .txt file
        foreach (var result in ocrResults)
        {
            string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
            File.WriteAllText(txtFilePath, result.Text);
        }

        Console.WriteLine("Batch OCR complete. Check the folder for .txt files.");
    }
}
```

Run it, watch the console output, and then open a few `.txt` files to confirm the **extract text from jpg** step succeeded.  

---

## Conclusion

We’ve just covered **how to batch OCR** a collection of JPEG images in C# using Aspose.OCR, turning each picture into a searchable `.txt` file. The solution is compact, GPU‑aware, and easy to extend for error handling, image pre‑processing, or parallel execution.  

If you’re ready to go further, consider these next steps:

* **Batch process images** of other formats (`*.png`, `*.tif`) by tweaking the `searchPattern`.  
* Combine the output with a full‑text search engine like Lucene.NET for instant document lookup.  
* Explore Aspose’s PDF conversion features to generate searchable PDFs directly from the OCR results.  

Feel free to experiment—swap out the language, turn off the GPU, or pipe the text into a database. The core pattern stays the same, and now you have a solid foundation to build on.

Happy coding, and may your OCR pipelines be ever fast and accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}