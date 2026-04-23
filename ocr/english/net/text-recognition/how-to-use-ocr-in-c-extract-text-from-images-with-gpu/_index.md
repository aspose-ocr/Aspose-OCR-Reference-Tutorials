---
category: general
date: 2026-02-13
description: Learn how to use OCR in C# to extract text from image files, enable GPU
  processing, and convert scans to text quickly.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: en
og_description: How to use OCR in C#? This guide shows you how to extract text from
  image files, enable GPU processing, and convert scans to text.
og_title: How to Use OCR in C# – Extract Text from Images with GPU
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: How to Use OCR in C# – Extract Text from Images with GPU
url: /net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use OCR in C# – Extract Text from Images with GPU

Ever wondered **how to use OCR** to pull text out of a scanned document without breaking a sweat? You're not the only one—developers constantly ask, “How can I extract text from image files efficiently?” The good news is that with Aspose.OCR you can do exactly that, and you can even **enable GPU processing** for a noticeable speed boost on supported hardware.

In this tutorial we’ll walk through a complete, end‑to‑end example that shows you **how to use OCR**, how to **extract text from image**, how to **convert scan to text**, and what to do if the GPU isn’t available. By the end you’ll have a ready‑to‑run C# console app that prints the recognized text and tells you whether the GPU was actually used.

## What You’ll Need

- .NET 6 SDK or later (the code works with .NET Core as well)  
- Visual Studio 2022 or any editor you prefer  
- Aspose.OCR for .NET package (available via NuGet)  
- A high‑resolution image file (e.g., `highres_scan.tif`) to test with  

No fancy setup required—just a few NuGet commands and you’re good to go.

## Step 1: Install Aspose.OCR and Prepare the Project

First things first. You have to bring the OCR library into your project. Open a terminal in your solution folder and run:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

That creates a fresh console project named **OcrDemo** and adds the `Aspose.OCR` NuGet package. The library contains the `OcrEngine` class we’ll be using.

> **Pro tip:** If you’re on a machine with a dedicated GPU, make sure the latest graphics driver is installed; otherwise the library will automatically fall back to CPU mode.

## Step 2: Write the Complete OCR Code

Now open `Program.cs` and replace its content with the following. Every line is commented so you can see *why* we do what we do.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Why This Works

- **ProcessingMode = Gpu** tells the engine to try the GPU first. The library abstracts away the low‑level CUDA/OpenCL calls, so you don’t need to manage device contexts yourself.  
- **IsGpuEnabled** is a boolean that confirms whether the GPU path succeeded. If you see `false`, the engine fell back to CPU automatically—nothing to panic about.  
- **RecognizeImage** does all the heavy lifting: it loads the image, runs the OCR model, and returns the plain‑text result. No need to manually preprocess the bitmap unless you have special requirements (e.g., deskewing).

## Step 3: Run the Application and Verify the Output

Compile and execute:

```bash
dotnet run
```

If everything is set up correctly, you’ll see something like:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

If the GPU isn’t available, the first line will read `GPU used: False`, but the extracted text will still appear—thanks to the graceful fallback.

> **Common question:** *What if my image is a JPEG instead of a TIFF?*  
> The `RecognizeImage` method accepts any format supported by .NET’s `System.Drawing` (JPEG, PNG, BMP, etc.). Just change the file extension in `imagePath`.

## Step 4: Optional – Tweak Settings for Better Accuracy

Aspose.OCR offers a few knobs you can turn:

| Setting | What it Does | When to Use |
|---------|--------------|-------------|
| `ocrEngine.Language` | Forces a specific language (e.g., `OcrLanguage.English`) | If you know the document’s language |
| `ocrEngine.PageSegMode` | Controls how the engine splits pages into blocks | For multi‑column layouts |
| `ocrEngine.DetectOrientation` | Auto‑rotates text that isn’t upright | Scans that may be upside‑down |

You can set these properties before calling `RecognizeImage`. For example:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## Step 5: Visualize the Flow (Image with Alt Text)

Below is a simple diagram that illustrates **how to use OCR** with optional GPU acceleration. It’s not required for the code to run, but it helps you see the big picture.

![Diagram showing how to use OCR with GPU processing](/images/ocr-gpu-flow.png)

*Alt text:* *Diagram showing how to use OCR with GPU processing, highlighting the fallback to CPU when needed.*

## Edge Cases & Troubleshooting

1. **Out‑of‑Memory on GPU** – Very large images may exceed GPU memory. In that case, the library will revert to CPU automatically. You can pre‑scale the image to keep memory usage low.  
2. **Unsupported Image Format** – If `RecognizeImage` throws *NotSupportedException*, verify the file extension and ensure the image isn’t corrupted. Converting to PNG often solves the issue.  
3. **Low Confidence Scores** – When the OCR result contains many unreadable characters, consider preprocessing (binarization, noise removal) or switching to a higher‑resolution scan.  

## Wrap‑Up: What We Achieved

We’ve just covered **how to use OCR** in a C# console app, demonstrated how to **extract text from image** files, and showed you how to **enable GPU processing** for faster results. You now know how to **convert scan to text**, verify whether the GPU was actually employed, and tweak a few settings for edge‑case scenarios.

### Next Steps

- Try feeding the output into a **search index** (e.g., Elasticsearch) so your scanned PDFs become searchable.  
- Experiment with **batch processing**—loop over a folder of images and write each result to a `.txt` file.  
- Combine OCR with **translation APIs** to automatically translate scanned foreign‑language documents.  

Got more questions? Drop a comment, and happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}