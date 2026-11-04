---
category: general
date: 2026-02-28
description: Create searchable PDF in C# by combining images vertically. Learn how
  to stack images vertically and convert scanned pages PDF with Aspose OCR.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: en
og_description: Create searchable PDF in C# by combining images vertically. This guide
  shows how to stack images vertically and convert scanned pages PDF using Aspose
  OCR.
og_title: Create Searchable PDF in C# – Combine Images Vertically
tags:
- Aspose OCR
- C#
- PDF generation
title: Create Searchable PDF in C# – Combine Images Vertically
url: /net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Searchable PDF in C# – Combine Images Vertically

Ever needed to **create searchable PDF** from a handful of scanned PNGs but weren’t sure where to start? You’re not alone. In many document‑automation projects the biggest pain point is turning a stack of image files into one tidy, searchable PDF that you can index and share.  

In this tutorial we’ll walk through a complete, ready‑to‑run example that shows you **how to stack images vertically**, **combine images vertically**, and finally **convert scanned pages PDF** into a single searchable document using Aspose.OCR’s GPU‑accelerated engine. By the end you’ll have a self‑contained program you can drop into any .NET solution.

> **What you’ll learn**
> - Initialize an OCR engine with GPU support.
> - Process a batch of images in parallel.
> - **Combine images vertically** to mimic a multi‑page scan.
> - Export a searchable PDF and a detailed JSON report for downstream analysis.

## Prerequisites

- .NET 6+ (the code compiles with .NET 6, .NET 7, or .NET 8)
- Aspose.OCR NuGet package (`Install-Package Aspose.OCR`)
- A GPU‑enabled machine if you want to keep the `ProcessingMode.Gpu` setting (CPU fallback works too)
- A folder with a few scanned PNG/JPEG files (the demo uses `page1.png`, `page2.png`, `page3.png`)

No external services, no hidden configuration files—just pure C#.

## Step 1 – Set Up the OCR Engine to **Create Searchable PDF**

First we create an `OcrEngine`, turn on GPU acceleration, pick English as the language, and add a couple of preprocessing filters. These filters improve accuracy by straightening tilted pages (`DeskewFilter`) and removing noise (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Why this matters:** The OCR engine does the heavy lifting of recognizing text. Enabling `ProcessingMode.Gpu` can cut recognition time in half on a modern graphics card, while the filters reduce common scanning artefacts that would otherwise produce garbled output.

## Step 2 – Configure a Batch Processor to **Convert Scanned Pages PDF** Efficiently

Processing each page one‑by‑one is fine for a couple of images, but real‑world projects often involve dozens or hundreds of pages. Aspose.OCR’s `OcrBatchProcessor` lets us run recognitions in parallel, dramatically speeding up the **convert scanned pages pdf** step.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Pro tip:** If you’re on a CPU‑only box, set `ProcessingMode = ProcessingMode.Cpu`. The batch processor will still respect `MaxDegreeOfParallelism`, so you can tune it to avoid over‑loading the machine.

## Step 3 – Run OCR on the Batch and Gather Results

Now we actually recognize the text. The `Recognize` method returns a list of `OcrResult` objects, each containing both the original image and the extracted text.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

At this point you have everything you need to **create searchable PDF**: the images (still in memory) and the associated text layers.

## Step 4 – **Combine Images Vertically** and Generate the Searchable PDF

Most scanned documents are multi‑page PDFs, so we need to stitch the individual page images into one tall image that mirrors a physical stack. Aspose.OCR provides `Image.CombineVertical` for exactly that purpose.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

The resulting file (`combined_searchable.pdf`) contains selectable, searchable text underneath each page image—exactly what you need to **create searchable PDF** from scanned sources.

![Create searchable PDF example](/images/create-searchable-pdf.png "create searchable pdf example")

*Image alt text: create searchable pdf example showing a combined PDF with searchable text.*

**Why vertical stacking?** Many OCR libraries treat each image as a separate page. By stacking them, we keep the PDF’s page order intact while still leveraging a single OCR pass for the whole document.

## Step 5 – Export Detailed JSON for the First Page (Great for Downstream Workflows)

Sometimes you need more than a PDF; perhaps you want to feed the OCR data into a database or a machine‑learning pipeline. Aspose.OCR lets you serialize each `OcrResult` to JSON, preserving bounding boxes, confidence scores, and more.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Expected JSON snippet (truncated):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

You can now feed this JSON into any downstream system—whether you’re indexing the text in Elasticsearch or feeding it to a custom analytics dashboard.

---

## How to **Stack Images Vertically** – A Quick Recap

If you’re wondering **how to stack images vertically** without Aspose, you could use `System.Drawing` to create a new bitmap and draw each page one after another. However, Aspose’s built‑in `Image.CombineVertical` handles DPI, pixel format, and memory management for you, making it the most reliable choice for production code.

### Alternative: Using `System.Drawing` (just for curiosity)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

The manual approach works, but you lose the convenience of automatic DPI handling and the ability to directly feed the result back into `RecognizeToPdf`. Stick with `CombineVertical` unless you have a very niche requirement.

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Out‑of‑memory errors** when processing dozens of high‑resolution scans | Each image stays in memory until the PDF is written | Dispose of `Image` objects as soon as you’re done (`using` blocks) or downscale images before combining |
| **Garbage text** after OCR | Skewed scans or low contrast | Keep the `DeskewFilter` and `DenoiseFilter`; consider adding `ContrastFilter` if needed |
| **Missing searchable layer** | Used `Recognize` instead of `RecognizeToPdf` | Ensure you call `ocrEngine.RecognizeToPdf` on the combined image |
| **GPU fallback fails** on machines without proper drivers | `ProcessingMode.Gpu` throws an exception | Wrap engine creation in a try/catch and fall back to `ProcessingMode.Cpu` |

## Next Steps – Extending the Workflow

Now that you know how to **create searchable PDF**, you might want to:

- **Batch‑process entire folders** using `Directory.GetFiles` and a `foreach` loop.
- **Add watermarks** to each page before combining (use `ImageProcessor` from Aspose.Imaging).
- **Split the searchable PDF back into individual pages** if you need per‑page PDFs later (`PdfDocument.Split` from Aspose.PDF).
- **Integrate with Azure Blob Storage** to pull images from the cloud and push the final PDF back.

All of these extensions naturally involve the same core concepts: OCR setup, image handling, and PDF export.

---

## Conclusion

We’ve covered everything you need to **create searchable PDF** from a collection of scanned images in C#. By initializing a GPU‑enabled `OcrEngine`, running a parallel batch with `OcrBatchProcessor`, **combining images vertically**, and finally calling `RecognizeToPdf`, you end up with a tidy, searchable document ready for archiving or indexing. The extra JSON export gives you full visibility into the OCR results, opening doors for analytics or custom workflows.

Give it a spin, experiment with different filters, and watch your document‑automation pipeline become a lot smoother. If you run into any quirks, drop a comment—happy coding!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}