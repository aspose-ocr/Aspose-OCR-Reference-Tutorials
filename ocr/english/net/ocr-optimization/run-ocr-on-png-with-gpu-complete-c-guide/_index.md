---
category: general
date: 2026-01-02
description: run OCR on PNG quickly using Aspose OCR and GPU support. Learn how to
  recognize text from image, extract text from image and set GPU memory limit.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: en
og_description: run OCR on PNG efficiently by leveraging Aspose OCR and GPU acceleration.
  This tutorial shows you how to recognize text from image, extract text from image
  and control GPU memory usage.
og_title: run OCR on PNG with GPU – Complete C# Guide
tags:
- OCR
- C#
- GPU
title: run OCR on PNG with GPU – Complete C# Guide
url: /net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# run OCR on PNG with GPU – Complete C# Guide

Ever needed to **run OCR on PNG** files but felt stuck at the performance line? You're not the only one. In many real‑world pipelines a single high‑resolution PNG can throttle a CPU‑only OCR engine, turning what should be a quick lookup into a minute‑long wait.  

The good news is that Aspose OCR ships with GPU extensions that let you **recognize text from image** files in a fraction of the time. In this tutorial we’ll walk through a hands‑on example that shows you exactly how to **run OCR on PNG** using C#, how to **extract text from image**, and even how to **set GPU memory limit** so you stay within your hardware budget.

We'll also cover the “how” and the “why” behind each step, so you’ll walk away with a solid mental model—not just a copy‑paste snippet.

## What You’ll Learn

- The prerequisites for using Aspose OCR’s GPU support.  
- How to load a PNG into a `Bitmap` and feed it to the OCR engine.  
- How to configure `GpuDevice` and `GpuMemoryLimitMb` for optimal performance.  
- How to **recognize text from image** and retrieve the plain‑text result.  
- Tips for handling common edge cases such as low‑memory GPUs or multi‑page PNGs.  

By the end of this guide you’ll be able to **run OCR on PNG** files at GPU speed and confidently control the memory footprint of your OCR jobs.

![Diagram showing run OCR on PNG with GPU acceleration](run-ocr-on-png-diagram.png "run OCR on PNG example")

## Prerequisites

Before we dive in, make sure you have:

1. .NET 6.0 or later (the code works with .NET Core and .NET Framework as well).  
2. An NVIDIA GPU with CUDA support (the example picks device index 0).  
3. The Aspose.OCR NuGet package and its GPU extensions (`Aspose.OCR.Extensions`).  
4. A sample PNG (`input.png`) placed in a folder you can reference from your project.  

If any of these sound unfamiliar, don’t worry—we’ll note alternatives where relevant.

---

## Step 1 – Install Aspose OCR and GPU Extensions

First things first. Without the right libraries the rest of the code won’t compile.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

The `Aspose.OCR.Extensions` package pulls in the native CUDA binaries required for GPU acceleration.  
*Pro tip:* If you’re on a machine without a GPU, you can still compile the project; just set `PreferGpu = false` later on.

---

## Step 2 – Load the PNG You Want to Process

Now we actually **run OCR on PNG** by loading it into a `Bitmap`. This step is straightforward but worth a quick note: `Bitmap` expects a file path, so make sure the path is correct relative to your executable.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

If the PNG is unusually large (say, > 5000 px on a side), you might want to downscale it first to avoid exhausting GPU memory. That’s where the **set GPU memory limit** option becomes handy later on.

---

## Step 3 – Create and Configure the OCR Engine for GPU Use

Here’s the heart of the tutorial: configuring the OCR engine to **recognize text from image** using the GPU. Two properties are key:

- `GpuDevice` – selects which CUDA device to use.  
- `GpuMemoryLimitMb` – caps the amount of GPU memory the engine can allocate.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**Why set a memory limit?** Some GPUs share memory with the display or run multiple workloads simultaneously. By capping the allocation you prevent out‑of‑memory crashes, especially when processing many PNGs in parallel.

---

## Step 4 – Define Recognition Options (Language & GPU Preference)

The `RecognitionOptions` object tells the engine what language to look for and whether to **prefer GPU** even for small images. For most English documents this is sufficient, but you can swap `Language.English` for other supported locales.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

If you ever need to **extract text from image** in a language other than English, just change the `Language` enum. The library supports dozens of languages out of the box.

---

## Step 5 – Run the OCR and Retrieve the Result

With everything wired up, the final call is a single line that actually **run OCR on PNG** and returns a rich result object.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

The `OcrResult` contains not only plain text (`ocrResult.Text`) but also confidence scores, bounding boxes, and even the original image with highlighted words—useful if you need to debug or visualize the extraction.

**Expected output** (for a sample PNG that says “Hello World”):

```
=== OCR Output ===
Hello World
```

If the text appears garbled, double‑check that the PNG is not corrupted and that the GPU memory limit isn’t too low for the image size.

---

## Step 6 – Handling Edge Cases and Best‑Practice Tips

### Low‑Memory GPUs

If you see an exception like `CudaException: out of memory`, lower `GpuMemoryLimitMb` or split the PNG into tiles before processing. Tiling can be done with `Graphics.DrawImage` on a `Bitmap` clone.

### Multiple PNGs in a Batch

When processing a folder of PNGs, reuse the same `OcrEngine` instance—initializing it once saves GPU context switches.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### Fallback to CPU

If a GPU isn’t available, simply set `PreferGpu = false`. The engine will automatically fall back to CPU without any code changes.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Full Working Example

Below is the complete program you can copy‑paste into a new console project. It includes all the steps above, plus a few safety checks.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Save the file as `Program.cs`, run `dotnet run`, and you should see the extracted text printed to the console.

---

## Conclusion

We’ve just demonstrated how to **run OCR on PNG** files using Aspose OCR’s GPU extensions, how to **recognize text from image**, and how to **extract text from image** while controlling the **set GPU memory limit**. By configuring `GpuDevice` and `GpuMemoryLimitMb` you keep your application fast and stable, even on modest GPUs.

From here you might:

- Experiment with other languages (`Language.French`, `Language.Spanish`).  
- Integrate the OCR step into a larger document‑processing pipeline.  
- Add post‑processing such as spell‑checking or entity extraction to polish the raw text.  

Remember, the key is not just the code but understanding why each setting matters. When you know how to **set GPU memory limit** and when to fall back to CPU, you’ll build OCR solutions that scale gracefully.

Got questions about a specific PNG size, multi‑page TIFFs, or troubleshooting GPU errors? Drop a comment below, and happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}