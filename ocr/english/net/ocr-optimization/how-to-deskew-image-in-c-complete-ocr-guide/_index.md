---
category: general
date: 2026-05-06
description: Learn how to deskew image and extract text from image using Aspose OCR
  – step‑by‑step guide to improve OCR accuracy and how to denoise image.
draft: false
keywords:
- how to deskew image
- extract text from image
- how to use OCR
- improve OCR accuracy
- how to denoise image
language: en
og_description: Learn how to deskew image and extract text from image with Aspose
  OCR. This tutorial shows how to denoise image and improve OCR accuracy.
og_title: How to Deskew Image in C# – Complete OCR Guide
tags:
- OCR
- C#
- Image Processing
title: How to Deskew Image in C# – Complete OCR Guide
url: /net/ocr-optimization/how-to-deskew-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Deskew Image in C# – Complete OCR Guide

Ever needed to **how to deskew image** before running OCR, but weren’t sure which filters to apply? You’re not alone—many developers hit the same snag when the source photo is a bit crooked or noisy. The good news? With a few lines of C# and Aspose.OCR you can straighten, clean, and finally extract text from image with impressive accuracy.

In this tutorial we’ll walk through everything you need: loading a skewed picture, applying deskew and denoise filters, boosting contrast, and finally pulling the text out. By the end you’ll understand **how to use OCR**, see how to **improve OCR accuracy**, and have a ready‑to‑run code sample that you can drop into any .NET project.

## What You’ll Need

- .NET 6 or later (the API works with .NET Core and .NET Framework)
- Aspose.OCR for .NET (free trial or licensed version) – you can get it from NuGet with `Install-Package Aspose.OCR`
- A sample image that’s skewed and a little noisy (e.g., `skewed_noisy.jpg`)
- Visual Studio, VS Code, or any editor you prefer

No extra native libraries are required; Aspose handles everything internally.

## Step 1: Set Up the Project and Install Aspose.OCR

### Create a new console app

```bash
dotnet new console -n DeskewOcrDemo
cd DeskewOcrDemo
```

### Add the Aspose.OCR package

```bash
dotnet add package Aspose.OCR
```

That’s it—your project now references the OCR engine and the built‑in filters we’ll need.

## Step 2: Load the Image You Want to Process

We’ll start by creating an `OcrEngine` instance and pointing it at the file we want to clean up.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 2: Load the image you want to process
        var ocrEngine = new OcrEngine();
        ocrEngine.SetImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // The rest of the pipeline will be added next…
    }
}
```

> **Why this matters:** Loading the image is the first hook for any subsequent filter. If the path is wrong, the whole pipeline fails silently, so double‑check the location.

## Step 3: Build a Processing Pipeline – Deskew, Denoise, Then Enhance Contrast

Here’s where the magic happens. We’ll add three filters in the exact order that yields the best OCR results:

1. **DeskewFilter** – straightens the image.
2. **MedianDenoiseFilter** – removes random speckles without blurring edges.
3. **ContrastStretchFilter** – boosts the difference between text and background.

```csharp
        // Step 3: Build a processing pipeline – deskew, denoise, then enhance contrast
        ocrEngine.Filters.Add(new DeskewFilter());               // how to deskew image
        ocrEngine.Filters.Add(new MedianDenoiseFilter());        // how to denoise image
        ocrEngine.Filters.Add(new ContrastStretchFilter());      // improve OCR accuracy
```

> **Pro tip:** The order is crucial. Deskew first, because a tilted image can confuse the denoiser. After the image is upright, the median filter can clean up grain, and finally the contrast stretch makes the letters pop.

## Step 4: Run the OCR Recognition

Now we let Aspose do the heavy lifting. The `Recognize` method returns an `OcrResult` object that contains the extracted string and some confidence metrics.

```csharp
        // Step 4: Run the OCR recognition
        var ocrResult = ocrEngine.Recognize();

        // Optional: check confidence (0‑100). Higher means more reliable.
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

> **How to use OCR:** The `Recognize` call internally applies all the filters we added, then runs the OCR engine. You don’t need to call each filter manually; the pipeline does it for you.

## Step 5: Output the Recognized Text

Finally, we print the text to the console. In real applications you’d probably write it to a file, a database, or pass it to another service.

```csharp
        // Step 5: Output the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Full, Runnable Example

Putting it all together, here’s the complete program you can copy‑paste into `Program.cs`:

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to process
        ocrEngine.SetImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 3️⃣ Build a processing pipeline – deskew, denoise, then enhance contrast
        ocrEngine.Filters.Add(new DeskewFilter());               // how to deskew image
        ocrEngine.Filters.Add(new MedianDenoiseFilter());        // how to denoise image
        ocrEngine.Filters.Add(new ContrastStretchFilter());      // improve OCR accuracy

        // 4️⃣ Run the OCR recognition
        var ocrResult = ocrEngine.Recognize();

        // 5️⃣ Show confidence and extracted text
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Run it with:

```bash
dotnet run
```

You should see a confidence score followed by the plain‑text version of whatever was on your original photo.

## Verifying the Result – What to Expect

If the source image contains, say, a printed invoice line:

```
Invoice #12345
Total: $1,250.00
Date: 2024‑04‑30
```

After the pipeline runs, the console will output something like:

```
Confidence: 96%
=== Extracted Text ===
Invoice #12345
Total: $1,250.00
Date: 2024-04-30
```

A high confidence value (typically above 90%) indicates that the **how to deskew image** and **how to denoise image** steps helped the OCR engine see the characters clearly.

## Common Questions & Edge Cases

### What if the image is rotated more than 45 degrees?

`DeskewFilter` automatically detects the angle up to ±45°. For larger rotations, pre‑rotate the image using `ocrEngine.Filters.Add(new RotateFilter(angle))` before deskewing.

### My confidence is low—what else can I try?

- Add a **BinarizationFilter** to force black‑and‑white conversion.
- Increase the **MedianDenoiseFilter** radius: `new MedianDenoiseFilter(3)`.
- Use a higher‑resolution source image (300 dpi or more).

### Can I process multiple images in a loop?

Absolutely. Just move the engine creation outside the loop, call `SetImage` for each file, and reuse the same filter collection.

```csharp
foreach (var file in Directory.GetFiles("images", "*.jpg"))
{
    ocrEngine.SetImage(file);
    var result = ocrEngine.Recognize();
    // handle result...
}
```

### Does this work on PDFs?

Aspose.OCR can read PDF pages as images, but you’ll need the Aspose.PDF library to extract each page as a bitmap first.

## Tips for Maximizing OCR Accuracy

1. **Crop out unnecessary borders** – extra whitespace can confuse the OCR engine.
2. **Use a uniform background** – plain white or light gray works best.
3. **Avoid extreme lighting** – shadows create false edges that the denoise filter may not fully remove.
4. **Test with real‑world samples** – synthetic data looks clean; production images often contain artifacts.

## Conclusion

We’ve just covered **how to deskew image**, **how to denoise image**, and the full flow of **how to use OCR** with Aspose to **extract text from image** while **improving OCR accuracy**. The example code is complete, runnable, and ready for you to adapt to batch processing, UI integration, or cloud services.

Next steps? Try swapping the `MedianDenoiseFilter` for a `GaussianDenoiseFilter` and compare confidence scores, or feed the extracted text into a natural‑language parser to automatically fill forms. The sky’s the limit once you’ve mastered the preprocessing pipeline.

Happy coding, and may your OCR results be crystal‑clear! 

--- 

![how to deskew image example](/images/deskew-example.png "how to deskew image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}