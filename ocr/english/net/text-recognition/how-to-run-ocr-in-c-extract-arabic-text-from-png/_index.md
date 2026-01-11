---
category: general
date: 2026-01-10
description: How to run OCR quickly and extract Arabic text from an image. Learn to
  convert image to text, read text from PNG, and see how to extract text with Aspose
  OCR.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: en
og_description: How to run OCR in C# and extract Arabic text from a PNG image. This
  guide shows you how to convert image to text and read text from PNG step‑by‑step.
og_title: How to Run OCR in C# – Extract Arabic Text from PNG
tags:
- OCR
- C#
- Aspose
title: How to Run OCR in C# – Extract Arabic Text from PNG
url: /net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Run OCR in C# – Extract Arabic Text from PNG

Ever wondered **how to run OCR** on a picture that contains Arabic characters? You’re not alone. Many developers hit a wall when they need to **extract Arabic text** from a PNG but don’t know which library will handle right‑to‑left scripts without a headache.  

In this tutorial we’ll walk through everything you need to know to **convert image to text**, **read text from PNG**, and finally **how to extract text** using Aspose.OCR in a clean C# console app. By the end you’ll have a ready‑to‑run program that prints the Arabic string right to your terminal.

## What You’ll Learn

- Install and reference the Aspose.OCR NuGet package.  
- Configure the OCR engine for Arabic language support.  
- Load a PNG image and run the recognition process.  
- Retrieve and display the extracted text.  
- Tweak settings for better accuracy and handle common pitfalls.

No prior experience with OCR is required, just a basic understanding of C# and a .NET development environment (Visual Studio, Rider, or the `dotnet` CLI will do).

---

## How to Run OCR – Setting Up Aspose OCR

### Step 1: Add the Aspose.OCR NuGet Package

The first thing we need is the OCR library itself. Aspose.OCR is a commercial product, but it offers a free trial that works perfectly for learning purposes.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

Alternatively, open the **NuGet Package Manager** in Visual Studio, search for **Aspose.OCR**, and click **Install**.

> **Pro tip:** If you plan to use the library in a CI pipeline, add the `-v` flag to lock the version, e.g., `dotnet add package Aspose.OCR -v 23.10`.

### Step 2: Create a New Console Project (if you don’t have one)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

Now you have a fresh `Program.cs` file ready for our code.

---

## Extract Arabic Text – Writing the OCR Code

Below is the complete, ready‑to‑run program. Save it as `Program.cs` (or replace the auto‑generated file).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### Why Each Line Matters

- **`OcrEngine`**: The central class that coordinates image loading, language selection, and recognition.  
- **`Language = OcrLanguage.Arabic`**: Arabic uses a right‑to‑left script and unique glyphs; setting the language tells the engine to apply the correct character models.  
- **`ImageStream.FromFile`**: Handles PNG, JPEG, BMP, and many other formats. If you ever need to read from a `MemoryStream` (e.g., an uploaded file), replace this call accordingly.  
- **`Recognize()`**: Performs the heavy lifting—pixel analysis, segmentation, and character classification.  
- **`ocrEngine.Text`**: The final Unicode string, ready for further processing, storage, or display.

### Expected Output

If `arabic_sample.png` contains the phrase “مرحبا بالعالم” (Hello World), the console will print:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

If the output looks garbled, double‑check that the image is clear, the language is set to Arabic, and the OCR engine version matches the documentation.

---

## Convert Image to Text – Tweaking Accuracy

While the default settings work for most clean scans, real‑world images often need a bit of extra love.

| Setting | What It Does | When to Use |
|---------|--------------|-------------|
| `ocrEngine.Config.Preprocess = true` | Enables automatic binarization and noise removal. | Scanned documents with shadows. |
| `ocrEngine.Config.Deskew = true` | Rotates the image to correct slight tilt. | Photos taken at an angle. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | Treats the whole image as one block of text. | Simple captions or single‑line labels. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | Limits recognition to Arabic characters only. | Reduces false positives on mixed‑language pages. |

You can add these lines right after creating the engine:

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## Read Text from PNG – Handling Different Image Sources

Sometimes the PNG lives in a database or comes from a web request. Here’s a quick variant that reads from a `byte[]`:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

The rest of the flow stays identical, which means **how to extract text** remains consistent regardless of the source.

---

## How to Extract Text – Advanced Options & Edge Cases

### 1. Multi‑Page PDFs or TIFFs

If you need to OCR a multi‑page document, loop over each page:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **Note:** You’ll need the `Aspose.PDF` package for this snippet.

### 2. Detecting Language Automatically

Aspose.OCR also offers auto‑detect, but it’s slower. If you’re unsure whether the image contains Arabic or another script, enable it:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

The engine will try each language model and pick the best match.

### 3. Performance Tips

- **Reuse the `OcrEngine`** object for multiple images; creating a new instance each time adds overhead.  
- **Run in parallel** only if you have separate engine instances per thread—sharing one instance causes race conditions.

---

## Conclusion

We’ve covered **how to run OCR** in C# from start to finish, showing you how to **extract Arabic text**, **convert image to text**, **read text from PNG**, and answer **how to extract text** in a variety of scenarios. The sample code is complete, self‑contained, and ready for you to paste into any .NET console project.

Next steps? Try swapping `OcrLanguage.Arabic` for Korean or Serbian Cyrillic to see the library’s multilingual power. Experiment with the preprocessing flags to boost accuracy on noisy scans, or integrate the OCR routine into a web API so users can upload images and get instant text results.

Happy coding, and may your OCR results always be crystal‑clear!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}