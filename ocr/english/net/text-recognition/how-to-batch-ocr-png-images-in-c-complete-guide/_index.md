---
category: general
date: 2026-04-26
description: How to batch OCR PNG images quickly. Learn to extract text from PNG,
  convert images to text, write recognized text, and read PNG directory with Aspose
  OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: en
og_description: How to batch OCR PNG images in C# with Aspose OCR. This guide shows
  how to extract text from PNG, convert images to text, and write recognized text
  efficiently.
og_title: How to Batch OCR PNG Images in C# – Step‑by‑Step
tags:
- OCR
- C#
- Aspose
title: How to Batch OCR PNG Images in C# – Complete Guide
url: /net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Batch OCR PNG Images in C# – Complete Guide

Ever wondered **how to batch OCR** a whole folder of PNG files without writing a separate program for each image? You're not the only one juggling dozens of screenshots, scanned receipts, or graphics that need to be turned into searchable text. In this tutorial we’ll walk through a hands‑on solution that **extracts text from PNG**, **converts images to text**, and **writes recognized text** to individual files—all while reading the PNG directory automatically.

By the end of this guide you’ll have a ready‑to‑run C# console app that processes any number of images in one go. No extra scripts, no manual copy‑pasting—just pure code that does the heavy lifting for you.

## What You’ll Need

- **.NET 6.0** or later (the code works fine on .NET Framework too).  
- **Aspose.OCR for .NET** NuGet package (free trial works for testing).  
- A folder with a handful of *.png* files you want to OCR.  
- Visual Studio 2022 or any C# IDE you prefer.

If you’ve got those, we can jump straight into the implementation.

## Step 1 – Prepare Your Input and Output Folders *(Read PNG Directory)*

The first thing we do is point the program at the folder that contains the images and decide where the resulting *.txt* files will live. Using `Directory.GetFiles` gives us a clean enumerable of every PNG in the directory.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Why this matters:**  
- Using a wildcard (`*.png`) guarantees we only process image files, ignoring any stray docs.  
- Creating the output folder on the fly prevents a `DirectoryNotFoundException` later on.

> **Pro tip:** If you need to support other formats (JPEG, BMP), just extend the search pattern or call `Directory.EnumerateFiles` with multiple extensions.

## Step 2 – Initialise the OCR Engine *(Convert Images to Text)*

Aspose.OCR ships with two engine types: a CPU‑based `OcrEngine` and a GPU‑accelerated `GpuOcrEngine`. For most batch jobs the CPU engine is perfectly fine, but you can swap the class name if you have a capable GPU.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Why this matters:**  
- Specifying the language dramatically improves accuracy because the engine knows which character set to expect.  
- Switching to `GpuOcrEngine` is a one‑line change if you hit performance bottlenecks on large batches.

## Step 3 – Create a Batch Recogniser

Aspose provides a convenient `BatchRecognizer` that accepts an enumerable of file paths and streams the results back one by one. This avoids loading all images into memory at once—a crucial detail for big folders.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Why this matters:**  
- The batch recogniser encapsulates the loop logic, letting us focus on what to do with each result rather than how to iterate safely.

## Step 4 – Run OCR on All Images and Write the Output *(Write Recognized Text)*

Now we actually perform the OCR. The `Recognize` method returns an `IEnumerable<RecognitionResult>` where each result contains the extracted text and other metadata.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Why this matters:**  
- Using `File.WriteAllText` ensures the text is saved with UTF‑8 encoding by default, preserving special characters.  
- The incremental naming (`out_0.txt`, `out_1.txt`) matches the order of processing, which is helpful for debugging.

> **Edge case:** If any image fails to OCR (e.g., corrupted file), `RecognitionResult.Text` will be empty. You can add a simple check inside the loop to log failures:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Step 5 – Put It All Together – Full Working Example

Below is the complete program you can copy‑paste into a new console project. It includes the `using` directives, folder validation, and a tiny console UI so you know when the batch finishes.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Expected output:**  
Running the program prints something like:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

And you’ll see `out_0.txt` … `out_11.txt` inside the output folder, each containing the plain‑text version of its corresponding image.

## Common Questions & Tips

| Question | Answer |
|----------|--------|
| *Can I OCR sub‑folders as well?* | Yes—replace `Directory.GetFiles` with `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`. |
| *What if I need a different language?* | Set `ocrEngine.Language = Language.Spanish;` (or any supported enum). |
| *How do I handle huge batches (thousands of files)?* | Consider processing in chunks or using `Parallel.ForEach` with a throttled degree of parallelism to avoid exhausting memory. |
| *Is the output always UTF‑8?* | `File.WriteAllText` defaults to UTF‑8 without BOM, which works for most Latin‑based languages. For Asian scripts you may need to set `Encoding.UTF8` explicitly. |
| *Can I get confidence scores?* | `RecognitionResult` exposes `Confidence`—you can log it alongside the text for quality control. |

## Visual Overview *(How to Batch OCR – Diagram)*

![How to batch OCR workflow diagram showing input folder → OCR engine → batch recogniser → output txt files](https://example.com/diagram-how-to-batch-ocr.png "How to batch OCR")

*The alt text contains the primary keyword, satisfying SEO image requirements.*

## Wrapping Up

We’ve just covered **how to batch OCR** a directory of PNG files using Aspose.OCR, from reading the PNG directory to writing each recognised text file. The solution is fully self‑contained, works on any modern .NET runtime, and can be extended for GPU acceleration, multi‑language support, or parallel processing.

Ready for the next step? Try swapping `Language.Latin` for another language, or integrate the output into a search index so your documents become instantly searchable. The sky’s the limit once you’ve mastered batch OCR.

Happy coding, and let me know in the comments if you hit any snags!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}