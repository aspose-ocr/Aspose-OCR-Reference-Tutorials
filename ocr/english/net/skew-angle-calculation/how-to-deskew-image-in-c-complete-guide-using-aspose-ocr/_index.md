---
category: general
date: 2026-03-21
description: Learn how to deskew image files and recognize text image with Aspose
  OCR. Convert jpg to text and correct image rotation in a few lines of C# code.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: en
og_description: How to deskew image and extract text from JPEGs using Aspose OCR.
  Follow this step‑by‑step guide to convert jpg to text and correct image rotation.
og_title: How to Deskew Image in C# – Quick Aspose OCR Tutorial
tags:
- OCR
- C#
- Aspose
title: How to Deskew Image in C# – Complete Guide Using Aspose OCR
url: /net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Deskew Image in C# – Complete Guide Using Aspose OCR

Ever wondered **how to deskew image** files that came out of a scanner tilted at a weird angle? You're not alone—many developers hit that snag when they try to extract text from receipts, invoices, or handwritten notes. The good news is that with Aspose OCR you can correct image rotation and pull out clean, searchable text in just a handful of lines.

In this tutorial we’ll walk through the whole process: from installing the library, enabling automatic deskewing, to recognizing text image and finally converting a JPG to text. By the end you’ll have a ready‑to‑run console app that **recognize text jpg** files without manually rotating them first.

## What You’ll Need

- **.NET 6.0** or later (the code works on .NET Core and .NET Framework alike)  
- **Aspose.OCR for .NET** NuGet package – version 23.12 or newer is recommended  
- A sample **skewed JPEG** (e.g., `skewed_receipt.jpg`) placed somewhere your app can read  
- Visual Studio, VS Code, or any C# editor you prefer  

No other third‑party tools are required. The library handles deskewing, OCR, and even language detection internally.

![how to deskew image example](/images/deskew-example.png "how to deskew image using Aspose OCR")

## Step 1: Set Up the Project and Install Aspose.OCR

To keep things tidy, start a fresh console project:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

The `dotnet add package` line pulls in the **Aspose.OCR** binaries plus all native dependencies. If you’re on Windows you’ll get the native DLLs automatically; on Linux/macOS you may need the `libgdiplus` package, but that’s a one‑time install.

## Step 2: Enable Automatic Deskewing (Correct Image Rotation)

Now open `Program.cs` and replace its contents with the code below. The key line here is `ocrEngine.Settings.Deskew = true;` – that’s the flag that tells the engine **how to deskew image** automatically.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Why Enable Deskew?

When a scanner feeds a page at an angle, the text baseline is slanted. Traditional OCR engines would read each character as a tilted version, dramatically reducing accuracy. By setting `Deskew = true`, Aspose OCR runs a fast Hough‑transform under the hood, rotates the bitmap back to horizontal, and then performs recognition. The result is the same as if you had manually rotated the image in Photoshop—only faster and fully automated.

## Step 3: Recognize Text Image and Convert JPG to Text

The `Recognize` call does two things at once:

1. **Deskews** the image (because we turned the flag on).  
2. **Extracts** the textual content, returning it in an `OcrResult` object.

You can treat `ocrResult.Text` as a plain string, write it to a file, or feed it into downstream processing pipelines. If you need the raw confidence scores per word, `ocrResult.Words` gives you a collection with `Confidence` values.

### Example Output

Assuming `skewed_receipt.jpg` contains a simple receipt, you might see something like:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

Notice how the numbers line up nicely despite the original image being rotated by about 7°. That’s the magic of **correct image rotation** built into the library.

## Step 4: Running the Example and Verifying Results

Compile and run:

```bash
dotnet run
```

If everything is wired correctly you’ll see the extracted text printed to the console. If you get an exception like `FileNotFoundException`, double‑check the path to your JPEG and ensure the file is readable.

### Common Pitfalls & Pro Tips

- **Large Images** – OCR memory usage grows with image dimensions. Resize overly large files (e.g., > 3000 px width) before feeding them to the engine.  
- **Non‑Latin Scripts** – By default the engine assumes English. Set `ocrEngine.Settings.Language = OcrLanguage.French;` (or any supported language) if you need to **recognize text image** in other alphabets.  
- **Batch Processing** – For many files, reuse the same `OcrEngine` instance; creating a new engine per file incurs unnecessary overhead.  
- **Quality Check** – After deskewing you can export the corrected bitmap via `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` to visually verify the rotation fix.

## Full Working Example (All Together)

Below is the complete, self‑contained program you can copy‑paste into `Program.cs`. It includes comments, error handling, and an optional step to save the deskewed image.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

Running the program will **recognize text jpg** files, automatically correct any skew, and print clean, searchable text to the console.

## Wrapping Up

You now have a solid, production‑ready snippet that shows **how to deskew image** files and extract their contents using Aspose OCR. The approach works for receipts, invoices, scanned contracts, or any JPEG where the text isn’t perfectly horizontal. 

Next steps you might explore:

- **Batch processing** of a folder of JPEGs and writing each result to a `.txt` file (ties back to *convert jpg to text*).  
- Integrating the OCR step into an ASP.NET Core API so clients can upload images and receive JSON‑formatted text.  
- Experimenting with different OCR settings like `ocrEngine.Settings.Language` or `ocrEngine.Settings.RecognitionMode` to improve accuracy for non‑English documents.  

Give it a try, tweak the settings, and let the engine do the heavy lifting. As always, if you hit a snag or have a clever optimization to share, drop a comment below. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}