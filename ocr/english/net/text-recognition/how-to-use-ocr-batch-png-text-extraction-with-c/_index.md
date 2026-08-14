---
category: general
date: 2026-03-04
description: How to use OCR to read PNG files and extract text quickly. Learn batch
  OCR processing and convert images to text with Aspose OCR in C#.
draft: false
keywords:
- how to use OCR
- batch ocr processing
- extract text png
- read png files
- convert images to text
language: en
og_description: How to use OCR to read PNG files, batch OCR processing and convert
  images to text in a single, easy-to-follow guide.
og_title: 'How to Use OCR: Batch PNG Text Extraction with C#'
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 'How to Use OCR: Batch PNG Text Extraction with C#'
url: /net/text-recognition/how-to-use-ocr-batch-png-text-extraction-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use OCR: Batch PNG Text Extraction with C#

Ever wondered **how to use OCR** on a folder full of screenshots? Maybe you have a mountain of PNG receipts, invoices, or scanned forms and you need the text without opening each file manually. The good news? With a few lines of C# and Aspose OCR you can **read PNG files**, **extract text PNG**‑by‑PNG, and **convert images to text** in parallel—no sweat.

In this tutorial we’ll walk through a complete, ready‑to‑run solution that shows **batch OCR processing** from start to finish. By the end you’ll have a console app that scans a directory, pulls out every character string, and prints a quick progress report. No external scripts, no hidden magic—just clear code and explanations you can copy‑paste right now.

---

## What You’ll Need

- .NET 6 (or later) – the current LTS version as of 2026.
- Aspose.OCR NuGet package – install with `dotnet add package Aspose.OCR`.
- A folder full of PNG images you want to process.
- Any IDE you like (Visual Studio, VS Code, Rider…).

That’s it. If you’ve got those, you’re good to go.

---

## How to Use OCR: Setting Up the Project

First, create a new console project and pull in the Aspose OCR library.

```bash
dotnet new console -n OcrBatchDemo
cd OcrBatchDemo
dotnet add package Aspose.OCR
```

Now open `Program.cs`. We’ll replace the default content with a full example that demonstrates **batch OCR processing** and **extract text png** files efficiently.

---

## Step 1 – Locate All PNG Images in a Directory

Finding the files is the simplest part, yet it’s essential to **read PNG files** reliably on any OS.

```csharp
using System;
using System.Collections.Concurrent;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static async Task Main(string[] args)
    {
        // 👉 Change this path to where your PNGs live
        string sourceFolder = @"C:\Images\ToProcess";
        if (!Directory.Exists(sourceFolder))
        {
            Console.WriteLine($"Folder not found: {sourceFolder}");
            return;
        }

        // Step 1: Locate all PNG images in the source folder
        string[] imagePaths = Directory.GetFiles(sourceFolder, "*.png", SearchOption.AllDirectories);
        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found. Make sure the folder contains .png images.");
            return;
        }

        // Continue to the next steps…
```

> **Why this matters:** Using `SearchOption.AllDirectories` lets you **read PNG files** even if they’re nested in subfolders, saving you a manual walk‑through later.

---

## Step 2 – Prepare a Thread‑Safe Collection for Results

Because we’ll be running OCR on multiple cores, we need a container that can handle concurrent writes.

```csharp
        // Step 2: Prepare a thread‑safe bag to store extracted text
        ConcurrentBag<string> extractedTexts = new ConcurrentBag<string>();
```

> **Pro tip:** `ConcurrentBag<T>` is lock‑free and ideal for gathering results when the order isn’t important. If you need ordering, switch to `ConcurrentQueue<T>`.

---

## Step 3 – Configure the OCR Engine for Batch Processing

Here’s where the **batch OCR processing** magic happens. We set the language, enable optimal parallelism, and reuse the same engine instance for every image.

```csharp
        // Step 3: Set up the OCR batch processor with English language and optimal parallelism
        OcrBatchProcessor ocrBatchProcessor = new OcrBatchProcessor
        {
            Engine = new OcrEngine { Language = Language.English },
            MaxDegreeOfParallelism = Environment.ProcessorCount // uses all logical cores
        };
```

> **Why reuse the engine?** Creating a new `OcrEngine` per image adds overhead. By reusing it, you cut memory churn and speed up the whole **batch OCR processing** run.

---

## Step 4 – Process Each Image Asynchronously and Collect Text

Now we actually run the OCR. The `ProcessAsync` method takes the file list, runs each image on a separate thread, and fires a callback with the result.

```csharp
        // Step 4: Process each image asynchronously, collect the text, and report progress
        await ocrBatchProcessor.ProcessAsync(imagePaths, (imagePath, ocrResult) =>
        {
            // Store the extracted string
            extractedTexts.Add(ocrResult.Text);

            // Simple progress line – shows how many characters we got
            Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        });

        // All done – let's show a quick summary
        Console.WriteLine($"\nFinished! Processed {imagePaths.Length} PNG files.");
        Console.WriteLine($"Total extracted text blocks: {extractedTexts.Count}");
    }
}
```

> **What you see:** The console prints a line for each file like `invoice123.png → 342 chars`. That’s a handy sanity check that the OCR actually read something.

---

## Full Working Example (Copy‑Paste Ready)

If you prefer to grab everything at once, here’s the complete program:

```csharp
using System;
using System.Collections.Concurrent;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static async Task Main(string[] args)
    {
        // 👉 Adjust this to your own folder
        string sourceFolder = @"C:\Images\ToProcess";

        if (!Directory.Exists(sourceFolder))
        {
            Console.WriteLine($"Folder not found: {sourceFolder}");
            return;
        }

        // Step 1: Locate all PNG images in the source folder
        string[] imagePaths = Directory.GetFiles(sourceFolder, "*.png", SearchOption.AllDirectories);
        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found. Place some .png images in the folder and try again.");
            return;
        }

        // Step 2: Prepare a thread‑safe bag to store extracted text
        ConcurrentBag<string> extractedTexts = new ConcurrentBag<string>();

        // Step 3: Set up the OCR batch processor with English language and optimal parallelism
        OcrBatchProcessor ocrBatchProcessor = new OcrBatchProcessor
        {
            Engine = new OcrEngine { Language = Language.English },
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 4: Process each image asynchronously, collect the text, and report progress
        await ocrBatchProcessor.ProcessAsync(imagePaths, (imagePath, ocrResult) =>
        {
            extractedTexts.Add(ocrResult.Text);
            Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        });

        // Summary
        Console.WriteLine($"\nFinished! Processed {imagePaths.Length} PNG files.");
        Console.WriteLine($"Total extracted text blocks: {extractedTexts.Count}");
    }
}
```

### Expected Output

```
receipt001.png → 128 chars
invoice_2025.png → 342 chars
menu.png → 57 chars

Finished! Processed 3 PNG files.
Total extracted text blocks: 3
```

If any image is unreadable, Aspose OCR returns an empty string – you’ll see `0 chars` in the console, which is a cue to check that file’s quality.

---

## Handling Edge Cases & Common Pitfalls

### Non‑PNG Images

Our glob pattern `*.png` ignores other formats. If you also need JPEGs or BMPs, change the search line to:

```csharp
string[] imagePaths = Directory.GetFiles(sourceFolder, "*.*", SearchOption.AllDirectories)
                               .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                                           f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                                           f.EndsWith(".bmp", StringComparison.OrdinalIgnoreCase))
                               .ToArray();
```

### Very Large Files

Huge images can blow up memory. A quick fix is to downscale them before handing them to the OCR engine:

```csharp
ocrBatchProcessor.Engine.ImageSize = new Size(2000, 0); // keep aspect ratio, max width 2000px
```

### OCR Errors

If you get garbled output, consider:

- Switching `Language` to the correct locale (`Language.Spanish`, etc.).
- Enabling `Engine.Preprocess` to improve contrast.
- Using `Engine.DetectOrientation = true` for rotated scans.

---

## Pro Tips for Faster **Batch OCR Processing**

1. **Warm‑up the engine** – run a single tiny image through the engine before the loop; it loads native DLLs and reduces the first‑run latency.
2. **Avoid console bottlenecks** – printing a line for every file can become a slowdown on thousands of images. Comment out the `Console.WriteLine` inside the callback if you only need the final summary.
3. **Persist results** – instead of a `ConcurrentBag`, write each OCR result to a database or a CSV as soon as it’s ready. That way you won’t lose data if the process crashes.

---

## Extending the Example: Save Extracted Text to Files

If you’d rather have a `.txt` file per image, tweak the callback:

```csharp
await ocrBatchProcessor.ProcessAsync(imagePaths, (imagePath, ocrResult) =>
{
    string txtPath = Path.ChangeExtension(imagePath, ".txt");
    File

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}