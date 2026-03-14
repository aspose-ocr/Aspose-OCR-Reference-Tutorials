---
category: general
date: 2026-03-13
description: How to use OCR in C# to extract text from scans. Learn to convert TIFF
  to text with Aspose OCR, GPU acceleration, and step‑by‑step code.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: en
og_description: How to use OCR in C# to extract text from scans. This guide shows
  you how to convert TIFF to text with Aspose OCR and GPU acceleration.
og_title: How to Use OCR in C# – Extract Text from Scans Fast
tags:
- OCR
- C#
- Aspose
- Image Processing
title: How to Use OCR in C# – Extract Text from Scans Fast
url: /net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use OCR in C# – Extract Text from Scans Fast

Ever wondered **how to use OCR** to pull readable text out of a stack of scanned TIFF files? You're not the only one. In many real‑world projects—think invoice digitisation, archival of historic documents, or simply making PDFs searchable—developers need a reliable way to **extract text from scans** without breaking a sweat.

The good news? With Aspose OCR and a few lines of C# you can convert TIFF to text in a matter of seconds, even on a modest workstation. Below you’ll get a complete, ready‑to‑run example, plus the reasoning behind each choice so you can adapt it to your own workflow.

## What You’ll Need

Before we dive in, make sure you have the following on hand:

| Prerequisite | Why it matters |
|--------------|----------------|
| .NET 6+ (or .NET Framework 4.7+) | The Aspose OCR NuGet package targets modern .NET runtimes. |
| Visual Studio 2022 (or any IDE you like) | Gives you IntelliSense and easy debugging. |
| A CUDA‑compatible GPU & driver (optional) | Enables `ocrEngine.UseGpu = true` for a noticeable speed boost on large batches. |
| A folder of TIFF images you want to process | This tutorial uses `*.tif` files, but you can adapt the pattern. |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | The core library that does the heavy lifting. |

If you’re missing any of these, grab them now—no point in reading further only to hit a missing dependency later.

## Overview of the Solution

At a high level the program does three things:

1. **Create an OCR engine** and optionally turn on GPU acceleration.  
2. **Iterate over every TIFF file** in a directory, run recognition, and capture the resulting plain‑text.  
3. **Write the text** to a `.txt` file sitting next to the original image.

That’s it. The code is deliberately tiny, yet it showcases best practices like explicit language selection, proper resource disposal, and error handling for the most common edge cases.

![How to use OCR in C# example](/images/how-to-use-ocr-csharp.png "Illustration of how to use OCR in C# to extract text from scans")

## Step 1: Initialise the OCR Engine (How to Use OCR)

The first thing you need is an instance of `OcrEngine`. This object is the gateway to all Aspose OCR functionality. By default it works on the CPU, but setting `UseGpu = true` tells the library to offload the heavy matrix calculations to your graphics card—provided you have a CUDA‑compatible driver installed.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Why this matters:**  
- **GPU acceleration** can cut processing time by up to 70 % for high‑resolution scans.  
- **Explicit language selection** avoids the engine guessing and improves accuracy, especially for non‑Latin scripts.

## Step 2: Point the Engine at Your Scans (Convert TIFF to Text)

Next we tell the program where to look for the images. Using `Directory.GetFiles` with a `*.tif` filter keeps the logic simple and avoids pulling in unrelated files like `.jpg` or `.png`.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Edge case note:** If the directory is empty, the loop below simply never executes, which is perfectly fine. You’ll see a friendly “No files found” message later.

## Step 3: Process Each TIFF File (Extract Text from Scans)

Now the heart of the program: loading each image, running OCR, and persisting the output. The `ImageStream.FromFile` helper streams the file directly into memory, which is more efficient than loading a `Bitmap` first.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Why we wrap each iteration in a `try/catch`:**  
Scanning a batch of documents is messy; a corrupted TIFF or an out‑of‑memory hiccup shouldn’t abort the whole run. The catch block logs the problem and moves on, keeping the pipeline robust.

### Expected Output

For every `example.tif` you’ll find a sibling `example.txt` containing something like:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

If the OCR engine can’t read a line, it will simply leave a blank line or a garbled character—nothing crashes.

## Step 4: Clean‑up and Dispose (Best Practice)

`OcrEngine` implements `IDisposable`, so it’s polite to free native resources when you’re done. In a short console app you could rely on the GC, but explicit disposal is a habit worth forming.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Full Working Example (Copy‑Paste Ready)

Below is the complete program you can paste into a new Console App project. It compiles as‑is, assuming you’ve added the Aspose.OCR NuGet package.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### Quick Checklist

- **GPU flag** – remove or set to `false` if you don’t have a CUDA driver.  
- **Language** – swap `Language.English` for any other supported language.  
- **File pattern** – change `"*.tif"` to `"*.png"` or `"*.*"` if your scans are in another format.  

## Common Pitfalls & Pro Tips (c# OCR tutorial)

| Pitfall | How to avoid it |
|---------|-----------------|
| **Out‑of‑memory errors** on huge batches | Process files in smaller chunks or call `GC.Collect()` after every 50 files (rarely needed). |
| **GPU not detected** but `UseGpu = true` | The engine silently falls back to CPU, but you can check `ocrEngine.IsGpuAvailable` after construction. |
| **Wrong language pack** leads to garbled output | Always set `ocrEngine.Language` explicitly; the default may be `Language.Unknown`. |
| **File path contains Unicode characters** | Use `Path.GetFullPath` to normalise, or prefix with `@"\\?\"` on Windows if paths exceed

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}