---
category: general
date: 2026-03-17
description: How to batch OCR PNG images in C# quickly. Learn to extract text PNG
  files, convert PNG to text, and read images from directory with a simple script.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: en
og_description: How to batch OCR PNG images in C# with step‑by‑step code. Extract
  text PNG files, convert PNG to text, and read images from directory effortlessly.
og_title: How to Batch OCR PNG Images in C# – Complete Guide
tags:
- OCR
- C#
- Image Processing
title: How to Batch OCR PNG Images in C# – Complete Guide
url: /net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Batch OCR PNG Images in C# – Complete Guide

Ever wondered **how to batch OCR** a folder full of screenshots without opening each file manually? You're not the only one—developers constantly ask how to batch OCR large collections of PNGs, especially when the goal is to extract text PNG files for downstream analysis.  

In this tutorial we’ll walk through a ready‑to‑run C# example that **extracts text PNG** files, **converts PNG to text**, and shows you the best way to **read images from directory**. By the end you’ll have a single script that drops a `.txt` next to every image, saving you hours of manual copy‑pasting.

## What You’ll Achieve

- Initialize an OCR engine once and reuse it for the whole batch.  
- Scan every `*.png` in a given folder without writing a loop yourself.  
- Write each OCR result to its own text file, preserving the original file name.  
- Handle common edge cases like empty folders or non‑image files gracefully.

### Prerequisites

- .NET 6.0 or later (the code works on .NET Core and .NET Framework as well).  
- An OCR library that exposes `OcrEngine`, `ImageStream`, and `OcrResult` types (for example, the fictional **FastOCR** SDK used in the snippets).  
- Basic C# knowledge—no advanced patterns required.

---

## How to Batch OCR PNG Images – Overview

Below is the **complete, runnable program**. Feel free to copy‑paste it into a new console project, replace the placeholder paths, and hit **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Expected output:** For every `image01.png` you’ll find an `image01.txt` containing the recognized characters. The console will list each file as it’s written.

![How to batch OCR diagram](how-to-batch-ocr-diagram.png "Diagram illustrating how to batch OCR PNG images using C#")

---

## Step‑by‑Step Explanation

### 1. Initialize the OCR Engine – the Heart of the Process  

The line `var ocrEngine = new OcrEngine();` creates a single engine instance that will be reused for the entire batch. Re‑using the engine is **crucial** because most OCR libraries allocate heavy resources (like language models) on construction. Initializing once improves performance dramatically—especially when you have dozens or hundreds of PNGs.

> **Pro tip:** If you need a language other than English, set `ocrEngine.Config.Language = Language.Spanish;` (or any supported enum).  

### 2. Read Images from Directory – locating every PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` does exactly what the secondary keyword *read images from directory* promises. It returns an array of absolute paths, which we later feed into the OCR engine.  

> **Why not use `SearchOption.AllDirectories`?** If your images are nested, you can switch to `GetFiles(path, "*.png", SearchOption.AllDirectories)`. Just remember that deeper scans might bring in unwanted files, so filter accordingly.

### 3. Convert File Paths to ImageStream Objects  

Most OCR SDKs expect a stream rather than a raw path. The LINQ expression `Select(path => ImageStream.FromFile(path)).ToList()` builds a **list of streams** that the batch recognizer can consume in one call. This step also ensures that file handles are opened only once, reducing I/O overhead.

> **Edge case:** If a file is corrupted, `ImageStream.FromFile` may throw. Wrap the conversion in a `try/catch` if you need resilience.

### 4. Recognize Text in the Entire Batch  

`ocrEngine.RecognizeBatch(imageStreams)` is the sweet spot for *how to batch OCR*. Instead of looping over each image and calling a single‑image method, we hand the whole collection to the engine. Internally the library may parallelize the work, giving you a speed boost on multi‑core machines.

> **Tip:** If your OCR library doesn’t expose a batch method, you can still achieve similar performance by using `Parallel.ForEach` around the single‑image `Recognize` call.

### 5. Write Each OCR Result – converting PNG to text  

The final `for` loop writes `ocrResults[i].Text` to a `.txt` file whose name mirrors the original PNG. This is exactly what the secondary keyword *convert PNG to text* describes. The `Path.Combine` call guarantees the output folder exists and prevents path‑traversal bugs.

> **Common pitfall:** Forgetting to create the output directory first will cause a `DirectoryNotFoundException`. The line `Directory.CreateDirectory(outputFolder);` pre‑emptively solves that.

---

## Handling Real‑World Variations

| Situation | What to Change | Why |
|-----------|----------------|-----|
| **Empty input folder** | Keep the early `if (imagePaths.Length == 0)` guard | Prevents a needless OCR call and gives a friendly message |
| **Mixed file types** | Use `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | Guarantees you only process PNGs, satisfying *extract text png* without errors |
| **Huge images ( > 5 MB )** | Downscale before feeding to OCR: `ImageStream.FromFile(path).Resize(1920, 1080)` (if API supports) | Reduces memory pressure and often improves recognition accuracy |
| **Different OCR language** | Set `ocrEngine.Config.Language = Language.French;` | Aligns the engine with the language of the source images |

---

## Frequently Asked Questions (FAQ)

**Q: Does this work with JPEG or TIFF files?**  
A: The core logic stays the same; just change the search pattern to `"*.jpg"` or `"*.tif"` and ensure the OCR library can decode those formats.

**Q: How can I process thousands of images without running out of memory?**  
A: Replace the batch call with a streaming approach—process a chunk of, say, 50 images at a time, then release the streams before loading the next chunk.

**Q: I need the OCR confidence score. Where do I find it?**  
A: Most `OcrResult` objects expose a `Confidence` property. You can extend the write‑out step:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## Wrap‑Up

We’ve just covered **how to batch OCR** PNG images in C# from start to finish. By initializing a single engine, reading images from directory, converting them to streams, recognizing the whole batch, and finally writing each result to a text file, you now have a solid, production‑ready pattern for **extract text PNG**, **convert PNG to text**, and **read images from directory** tasks.

What’s next? Try swapping the OCR provider, add multi‑threaded post‑processing (e.g., spell‑checking), or feed the `.txt` files into a search index. The sky’s the limit once you’ve mastered the batch workflow.

Got a twist you’d like to share? Drop a comment, and happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}