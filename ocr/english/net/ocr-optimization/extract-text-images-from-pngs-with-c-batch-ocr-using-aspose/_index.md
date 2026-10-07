---
category: general
date: 2026-02-09
description: extract text images quickly with C# by setting max parallelism for batch
  OCR – learn to convert scanned pages, handle multiple image OCR and read png text
  efficiently.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: en
og_description: extract text images in C# by setting max parallelism. This tutorial
  shows how to convert scanned pages, run multiple image OCR and read png text with
  Aspose OCR.
og_title: extract text images from PNGs with C# – Complete Batch OCR Guide
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: extract text images from PNGs with C# – Batch OCR using Aspose OCR
url: /net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extract text images from PNGs with C# – Batch OCR using Aspose OCR

Ever needed to **extract text images** from a folder of scanned PNGs but felt stuck at the “how do I make it fast?” question? You’re not alone. In many real‑world projects, developers have to **set max parallelism** so that dozens of pages are processed in seconds instead of minutes.  

In this guide we’ll walk through a complete, runnable example that **converts scanned pages**, runs **multiple image OCR**, and finally **reads png text** without breaking a sweat. No vague “see the docs” links—just code you can copy‑paste, explanations of why each line matters, and tips to avoid the usual pitfalls.

> **Pro tip:** If you’re already using Aspose OCR elsewhere, you’ll notice the same `OcrEngine` class appears here, but we’ll tweak its configuration for true parallel processing.

---

## What You’ll Need

- **.NET 6+** (or .NET Framework 4.6+). The API works the same, but newer runtimes give better thread handling.  
- **Aspose.OCR for .NET** – install via NuGet: `Install-Package Aspose.OCR`.  
- A folder that contains a few PNG scans (`page1.png`, `page2.png`, …).  
- An IDE or editor you’re comfortable with (Visual Studio, Rider, VS Code…).

That’s it. No extra services, no cloud keys, just pure local processing.

---

## extract text images – Setting Max Parallelism for Batch OCR

When you fire off OCR on several files, the engine will, by default, use a single thread. That’s safe but painfully slow. By configuring `MaxDegreeOfParallelism` you tell the engine how many threads it may spin up simultaneously.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Why 4?**  
Four is a sweet spot on most modern laptops—enough cores to keep the CPU busy, but not so many that you starve other processes. If you run this on a server with 16 cores, bump the number up to 12 or 14 for a noticeable speed‑up.

---

## Convert scanned pages – Building the Image Stream Collection

Aspose expects each image as an `ImageStream`. The `FromFile` helper reads the file, keeps it in memory, and hands it off to the OCR engine. You can also feed a `MemoryStream` if your images come from a database or an HTTP response.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Edge case:** If any file is missing or corrupted, `FromFile` will throw a `FileNotFoundException`. Wrap the construction in a `try/catch` if you expect unreliable input.

---

## multiple image ocr – Performing Batch OCR

Now the heavy lifting happens. `RecognizeBatch` spawns up to the number of threads you set earlier, processes each image, and returns a list of `OcrResult` objects.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

Behind the scenes, each thread loads its image, runs the neural network, and extracts plain text. The order of results matches the order of the input list, so you can safely map page 1 → result 0, and so on.

---

## read png text – Displaying the Extracted Content

Finally we loop through the results and print the plain text to the console. This is where you can pipe the output to a file, a database, or even a downstream NLP service.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Expected Console Output

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

If you see blank sections, double‑check that the PNGs are not pure white images—OCR needs some contrast.

---

## Practical Tips & Common Pitfalls

| Situation | What to Do |
|-----------|------------|
| **Memory pressure** on large batches | Process images in chunks of 10‑20 files, then call `GC.Collect()` if you notice spikes. |
| **Incorrect language detection** | Set `ocrEngine.Configuration.Language = OcrLanguage.English;` (or your target language) before calling `RecognizeBatch`. |
| **Slow performance despite parallelism** | Verify that your SSD isn’t throttling I/O; read all files into memory first (as we do with `ImageStream.FromFile`). |
| **Missing characters** | Increase `ocrEngine.Configuration.DPI = 300;` for higher‑resolution processing. |

---

## Extending the Example – From PNG to PDF or DOCX

If you eventually need to **convert scanned pages** into searchable PDFs, simply feed the same `ocrResults[i].PlainText` into a PDF library (e.g., Aspose.PDF) and overlay the text as an invisible layer. The same parallelism trick works there, too.

---

## Full Source Code (Copy‑Paste Ready)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Save this as `BatchExample.cs`, run `dotnet run`, and watch your console fill with the text that used to be hidden inside those PNG scans.

---

## Visual Summary

![extract text images example](images/ocr-batch.png){alt="extract text images example"}

The diagram shows the flow: **PNG files → ImageStream collection → OcrEngine (max parallelism) → OCR results → Console / downstream storage**.

---

## Conclusion

You now have a solid, end‑to‑end recipe for how to **extract text images** in C# while **setting max parallelism**, **converting scanned pages**, handling **multiple image OCR**, and **reading png text** efficiently. The code is self‑contained, the explanations cover both the “how” and the “why,” and the tips keep you from common headaches.

What’s next? Try swapping the PNG list for a dynamic `Directory.GetFiles` loop, experiment with different thread counts, or feed the output into a searchable PDF. The same pattern scales to hundreds of pages with barely a line of extra code.

Got questions or a tricky edge case? Drop a comment below, and happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}