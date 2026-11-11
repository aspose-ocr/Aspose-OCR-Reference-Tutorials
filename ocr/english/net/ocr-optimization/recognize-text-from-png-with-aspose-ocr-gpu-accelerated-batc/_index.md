---
category: general
date: 2026-04-01
description: Learn how to recognize text from png files quickly by setting gpu device
  id and enabling GPU acceleration in Aspose OCR. Step‑by‑step C# guide.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: en
og_description: recognize text from png files fast by setting gpu device id. Follow
  this complete C# guide to enable GPU acceleration with Aspose OCR.
og_title: recognize text from png – GPU‑Accelerated Aspose OCR Tutorial
tags:
- C#
- OCR
- GPU
- Aspose
title: recognize text from png with Aspose OCR – GPU‑Accelerated Batch Demo
url: /net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# recognize text from png – Full C# GPU‑Accelerated Batch Tutorial

Ever needed to **recognize text from png** images but found the process painfully slow? You’re not alone. Most developers start with a simple OCR call, then stare at a console that crawls like a snail when a folder contains dozens of screenshots.  

The good news? Aspose OCR can offload the heavy lifting to your graphics card, and with just a couple of lines you can **set gpu device id** to pick the exact GPU you want. In this guide we’ll walk through a complete, runnable example that pulls every PNG from a folder, turns on GPU acceleration, selects the first GPU, and prints the character count for each file.

By the end you’ll have a self‑contained program that you can drop into any .NET project, and you’ll understand why enabling the GPU matters, how to handle edge cases, and what to tweak for even better performance.

## What You’ll Need

- **.NET 6.0** or later (the code compiles with .NET Core as well).  
- The **Aspose.OCR** NuGet package – install it with `dotnet add package Aspose.OCR`.  
- A machine with a CUDA‑compatible GPU (NVIDIA is typical) and the appropriate driver.  
- A folder full of **PNG** images you want to process.  

If any of those sound unfamiliar, don’t panic. The steps below include the exact commands you need, and we’ll also discuss what to do when a GPU isn’t present.

## Step 1: Initialise the OCR Engine and Enable GPU Acceleration  

The first thing you have to do is create an `OcrEngine` instance and turn on GPU support. This flag tells Aspose to use the native CUDA libraries under the hood.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Why this matters:** Without `UseGpuAcceleration`, each image is processed on the CPU, which can be orders of magnitude slower, especially for high‑resolution PNGs. Enabling the flag also prepares the engine to accept a specific GPU device later on.

## Step 2: Set GPU Device ID (Optional but Recommended)  

If your workstation has more than one GPU, you can decide which one to use. The device IDs start at **0**, so `0` picks the first GPU, `1` the second, and so on.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Pro tip:** When running on a shared server, explicitly setting the GPU device ID can prevent your job from stealing resources from other processes. If you omit this line, Aspose will pick the default device, which is usually fine for a single‑GPU setup.

## Step 3: Gather All PNG Files from Your Batch Folder  

Next we need to locate every PNG you want to run OCR on. The `Directory.GetFiles` method does the heavy lifting.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Edge case:** If the folder is empty, `imageFiles` will be an empty array. We’ll handle that later with a friendly message.

## Step 4: Process Each Image and Output the Recognised Character Count  

Now the core loop. For every PNG we call `Recognize`, then print the file name and the length of the extracted text.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**What you’ll see:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

If an image contains no text, the count will be `0`. That’s perfectly normal for screenshots that are purely graphical.

## Step 5: Run the Program and Verify GPU Usage  

Compile the file (`dotnet build`) and run it (`dotnet run`). While the console scrolls, you can open your GPU monitoring tool (like NVIDIA Smi) to see the GPU utilization spike briefly for each image. If you don’t see any activity, double‑check that:

1. The CUDA driver is installed.  
2. `UseGpuAcceleration` is set to `true`.  
3. The correct `GpuDeviceId` matches a physical GPU.

If the GPU isn’t available, Aspose will fall back to CPU automatically, but you’ll lose the speed advantage.

## Common Variations & Tips  

| Situation | What to Change |
|-----------|----------------|
| **Different image format** (e.g., JPEG) | Change the search pattern to `*.jpg` or `*.*` and Aspose will still recognise the text. |
| **Batch size is huge** (thousands of files) | Process in chunks to avoid memory pressure: split `imageFiles` into smaller arrays. |
| **Need the actual text, not just length** | Replace `ocrResult.Text.Length` with `ocrResult.Text` in the `WriteLine`. |
| **Running on a headless server** | Ensure the server has a GPU driver; otherwise, set `UseGpuAcceleration = false` to avoid unnecessary errors. |
| **Multiple GPUs, want to balance load** | Loop over `ocrEngine.GpuDeviceId = i % gpuCount` inside the `foreach` to rotate devices. |

## Expected Output & Verification  

When everything works, the console prints each file name followed by the character count, as shown earlier. To double‑check the actual OCR output, you can temporarily dump the text:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

Just remember to remove or comment out that line for large batches; printing thousands of lines can swamp your terminal.

## Full Working Example (Copy‑Paste Ready)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

Save this as `GpuBatchDemo.cs`, run `dotnet add package Aspose.OCR`, then `dotnet run`. You should see the character counts appear almost instantly for each PNG, thanks to GPU acceleration.

## Conclusion  

You now know how to **recognize text from png** files efficiently by enabling GPU acceleration and explicitly **set gpu device id** in Aspose OCR. The complete, copy‑and‑paste program handles folder discovery, edge‑case checks, and gives you immediate feedback on OCR performance.  

Next steps? Try swapping the `Recognize` call for `ocrEngine.RecognizeAsync` if you need non‑blocking processing, or experiment with different image preprocessing options (e.g., binarization) that Aspose provides. You could also pipe the OCR results into a database or a search index for a full‑text search solution.

Got questions about handling multi‑page PDFs, or want to compare Aspose OCR with Tesseract? Drop a comment or explore our other tutorials on **batch OCR C#**, **OCR performance tips**, and **GPU‑driven image processing**. Happy coding!  

![Console output showing recognised character counts for PNG files – recognize text from png using GPU acceleration](image-placeholder.png "recognize text from png output example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}