---
category: general
date: 2026-04-29
description: Batch OCR images quickly with Aspose OCR in C#. Learn how to extract
  text from jpg files, read text from scans, and process image list in parallel.
draft: false
keywords:
- batch OCR images
- extract text from jpg
- read text from scans
- parallel OCR processing
- process image list
language: en
og_description: Batch OCR images quickly with Aspose OCR. This guide shows how to
  extract text from jpg, read text from scans, and process an image list in parallel.
og_title: Batch OCR Images in C# – Parallel OCR of JPG Scans
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Batch OCR Images in C# – Parallel OCR of JPG Scans
url: /net/ocr-optimization/batch-ocr-images-in-c-parallel-ocr-of-jpg-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Batch OCR Images in C# – Parallel OCR of JPG Scans

Ever needed to **batch OCR images** but weren’t sure how to scale the work across multiple files? You’re not alone—developers often hit a wall when they try to read text from scans one by one. The good news is that with Aspose OCR you can **extract text from jpg** files, **read text from scans**, and **process image list** items in parallel with just a few lines of C#.

In this tutorial we’ll walk through a complete, ready‑to‑run example that shows exactly how to do that. By the end you’ll have a self‑contained console app that recognises a folder of JPEG scans, prints each page’s text, and tells you how long each operation took. No external docs to chase, no half‑filled code snippets—just a full solution you can drop into Visual Studio and run.

## What You’ll Need

- **.NET 6.0** or later (the code compiles on .NET Framework 4.6+ as well)
- **Aspose.OCR** NuGet package (`Install-Package Aspose.OCR`)
- A handful of JPG or scanned image files you want to process
- Any IDE you like; I’m using Visual Studio 2022, but VS Code works fine too

That’s it. If you already have the NuGet package, you’re good to go.

## Step 1 – Initialize the OCR Engine (Batch OCR Images Setup)

The first thing we do is create an `OcrEngine` instance and tell it which language to look for. In most cases English is enough, but you can swap `OcrLanguage.English` for any supported language.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine and set the language to English
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };
```

*Why this matters:* Initialising the engine once and re‑using it across all images is far more efficient than creating a new instance per file. It also lets Aspose share internal resources, which is essential for **parallel OCR processing**.

## Step 2 – Build the List of Images (Process Image List)

Next we define the collection of file paths we want to feed into the batch recogniser. You can generate this list dynamically with `Directory.GetFiles`, but for clarity we’ll hard‑code a few entries.

```csharp
        // Step 2: Define the image files that will be processed
        var imagePaths = new List<string>
        {
            @"YOUR_DIRECTORY/page1.jpg",
            @"YOUR_DIRECTORY/page2.jpg",
            @"YOUR_DIRECTORY/page3.jpg"
        };
```

*Tip:* If you have thousands of scans, consider using `Directory.EnumerateFiles` with a filter like `*.jpg` to avoid loading the entire list into memory at once.

## Step 3 – Run the Batch Recognition (Parallel OCR Processing)

Now comes the heart of the matter: calling `BatchRecognize`. The method accepts a `maxDegreeOfParallelism` argument, which controls how many threads Aspose will spin up. By default it uses four threads, but you can bump that up if your CPU has more cores.

```csharp
        // Step 3: Run batch recognition (4 parallel threads by default)
        var recognitionResults = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);
```

*What’s happening under the hood?* Aspose splits the `imagePaths` collection into chunks, hands each chunk to a separate thread, and aggregates the results. This is the most efficient way to **extract text from jpg** files when you have a **process image list** that can be tackled concurrently.

## Step 4 – Display the Results (Read Text from Scans)

Finally we loop through the `recognitionResults` collection and print each file’s text and processing time. The `OcrResult` object also gives us the source file name, which helps when you need to log or store the output.

```csharp
        // Step 4: Output the results for each image
        foreach (var result in recognitionResults)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

**Expected output (example):**

```
File: C:\Scans\page1.jpg
Time: 1.34s
The quick brown fox jumps over the lazy dog.
----------------------------------------
File: C:\Scans\page2.jpg
Time: 1.27s
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----------------------------------------
File: C:\Scans\page3.jpg
Time: 1.41s
Invoice #12345
Total: $1,250.00
----------------------------------------
```

Notice how each block tells you the filename, how long the OCR took, and the extracted text. That’s exactly the information you need when you’re **reading text from scans** in a production pipeline.

## Handling Common Edge Cases

| Situation | What to Watch For | Quick Fix |
|-----------|-------------------|-----------|
| **Missing file** | `FileNotFoundException` thrown inside `BatchRecognize` | Validate paths with `File.Exists` before adding to `imagePaths`. |
| **Unsupported format** | Aspose only handles raster images (JPG, PNG, BMP, TIFF). | Convert PDFs to images first (use Aspose.PDF) or skip those files. |
| **Memory pressure** | Very large images can blow up RAM when many threads run. | Lower `maxDegreeOfParallelism` or resize images before OCR. |
| **Non‑English text** | Language set to English will miss other scripts. | Change `Language = OcrLanguage.French` (or a multilingual combo). |

These tips keep your batch job robust, especially when you’re **processing an image list** that comes from user uploads or a scanned archive.

## Pro Tip – Tuning Parallelism

If you run this on a 8‑core machine, bump the parallelism to 6 or 8 and watch the speed improve. However, remember that each thread also consumes memory for the bitmap. A good rule of thumb:

```csharp
int cores = Environment.ProcessorCount;
int maxThreads = Math.Max(1, cores - 1); // leave one core free for UI/OS
```

Plug `maxThreads` into `BatchRecognize` for a dynamic, machine‑aware configuration.

## Full Working Example (Copy‑Paste Ready)

Below is the complete program, ready to compile. Just replace `YOUR_DIRECTORY` with the path that holds your JPG scans.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine – English language
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };

        // 2️⃣ Build the list of image files to process
        var imagePaths = new List<string>();
        string folder = @"C:\Scans"; // <-- change this
        foreach (var file in Directory.EnumerateFiles(folder, "*.jpg"))
        {
            imagePaths.Add(file);
        }

        if (imagePaths.Count == 0)
        {
            Console.WriteLine("No JPG files found in the specified folder.");
            return;
        }

        // 3️⃣ Run batch OCR – let the library use 4 threads (adjust as needed)
        var results = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);

        // 4️⃣ Output each result
        foreach (var result in results)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

> **Note:** The `using System.IO;` line is required for the `Directory` helper. The code prints a friendly message if no JPGs are found, preventing a silent failure.

## Conclusion

We’ve just demonstrated a clean, **batch OCR images** workflow that **extracts text from jpg** files, **reads text from scans**, and efficiently **processes an image list** using **parallel OCR processing**. The full, runnable example shows exactly how to set up the engine, feed it a collection of files, and handle the results—all while keeping memory usage and thread count under control.

Ready for the next step? Try swapping the language to French, add PDF‑to‑image conversion, or store the OCR text in a database. The pattern stays the same: initialise once, feed a list, and let Aspose do the heavy lifting in parallel.

Got questions or want to share your own tweaks? Drop a comment below, and happy coding! 

![Batch OCR images processing flow](https://example.com/placeholder.png "Diagram illustrating batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}