---
category: general
date: 2026-03-17
description: c# OCR tutorial – discover how to extract text from image files, read
  text from WebP photos, and convert image to text using a simple OcrEngine.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: en
og_description: c# OCR tutorial shows you how to extract text from image files, read
  text from WebP photos, and convert image to text with a few lines of code.
og_title: c# OCR tutorial – Extract Text from Images in Minutes
tags:
- C#
- OCR
- Image Processing
title: 'c# OCR tutorial: Extract Text from Images (WebP, Photo) – Quick Guide'
url: /net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Extract Text from Images (WebP, Photo)

Ever needed to **extract text from image** files but weren’t sure where to start in C#? Maybe you’ve got a WebP screenshot, a JPEG of a receipt, or a scanned PDF page and you just want the words inside. In this **c# OCR tutorial** we’ll walk through a complete, ready‑to‑run example that reads text from a photo, handles WebP and other modern formats, and converts the image to plain text—all in a handful of lines.

**What’s the payoff?** You’ll be able to turn any picture of text into searchable strings, feed them into databases, or feed them to downstream AI pipelines. No magic, just a solid OCR engine, a few .NET APIs, and clear explanations of the “why” behind each step.

## What You’ll Need

Before we dive in, make sure you have:

- **.NET 6 SDK** (or later). The code below compiles with .NET 6+ and runs on Windows, Linux, or macOS.
- **Visual Studio 2022** or any editor you prefer (VS Code works fine).
- The **`Microsoft.Windows.SDK.Contracts`** NuGet package (provides `Windows.Media.Ocr`). Install with:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- An image file you want to process – for this tutorial we’ll use a **WebP** photo named `photo.webp` placed in a folder called `YOUR_DIRECTORY`.

> Pro tip: If you’re on a non‑Windows platform, you can swap the `OcrEngine` for a cross‑platform library like **Tesseract**. The surrounding code stays virtually the same.

## Step 1: Set Up a C# OCR Tutorial Project

First, create a fresh console app. Open a terminal and run:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Add the required package (as shown above) and open the project in your IDE. This scaffolding gives us a clean slate for the **c# OCR tutorial**.

## Step 2: Import Namespaces and Prepare the Image

We need a few `using` directives so the compiler knows where to find `OcrEngine`, `SoftwareBitmap`, and image‑loading helpers.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Why these namespaces?**  
> `Windows.Media.Ocr` houses the `OcrEngine` class that actually performs the recognition. `Windows.Graphics.Imaging` lets us decode the image (including WebP) into a `SoftwareBitmap` that the engine can understand. The `System.IO` and `Windows.Storage.Streams` helpers make loading files painless.

Now, load the image. The built‑in decoder can handle WebP, HEIF, PNG, JPEG, and more, so you can **read text from WebP** without extra plugins.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **Edge case:** If your image is already black‑and‑white, you can skip the conversion step. The grayscale conversion is a small performance win and often improves recognition on noisy photos.

## Step 3: Run the OCR Engine – Recognize Text from Photo

Here’s the heart of the **c# OCR tutorial**. We create an instance of `OcrEngine`, feed it the bitmap, and pull out the recognized text.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**What’s happening?**  
- `TryCreateFromUserProfileLanguages()` picks the language(s) your Windows user profile is set to, which usually covers English, Spanish, etc. If you need a specific language, use `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.
- `RecognizeAsync` runs the heavy lifting on a background thread, returning an `OcrResult` that contains the raw string, word bounding boxes, and confidence scores.
- Finally, we print `ocrResult.Text`, giving you the **convert image to text** result you can pipe elsewhere.

## Step 4: Full, Runnable Example

Putting it all together, here’s a self‑contained program you can copy‑paste into `Program.cs`. It compiles, runs, and prints the text extracted from `photo.webp`.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### Expected Output

If `photo.webp` contains the sentence “Hello, world! This is a test.” you’ll see something like:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

The exact line breaks depend on the layout of the source image, but the **extract text from image** result will always be a plain string you can manipulate further.

## Common Questions & Edge Cases

### Does this work with other image formats?

Absolutely. The decoder used (`BitmapDecoder`) auto‑detects JPEG, PNG, BMP, GIF, **WebP**, HEIF, and more. So you can **read text from WebP**, JPEG, or even a TIFF without changing the code.

### What if the OCR engine returns low confidence?

You can inspect `ocrResult.Lines` and each `OcrWord` for a `ConfidenceScore`. If the score is below a threshold (e.g., 0.6), consider:

- Pre‑processing the image (increase contrast, sharpen, deskew).
- Using a higher‑resolution source image.
- Switching to a dedicated library like **Tesseract** for multilingual support.

### How to handle multiple languages in the same image?

Create separate `OcrEngine` instances for each language and run them sequentially, or use a library that supports mixed‑language detection. For the built‑in engine, you can pass a `Language` object:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Can I run this on Linux/macOS?

The `Windows.Media.Ocr` API is Windows‑only. On non‑Windows platforms, replace the OCR section with **Tesseract** (via `Tesseract.Net.SDK`). The loading and preprocessing code remains identical, so the rest of this **c# OCR tutorial** still applies.

## Pro Tips for Better Accuracy

- **Resize** large images to a maximum of 2000 px on the longest side – OCR engines work faster on moderate sizes.
- **Denoise** using a simple Gaussian blur if the photo is grainy.
- **Deskew** the bitmap if the text isn’t perfectly horizontal; `SoftwareBitmap` can be rotated before passing to `OcrEngine`.
- **Cache** the `OcrEngine` instance if you’re processing many images in a batch; creating it repeatedly adds overhead.

## Related Topics to Explore

- **Convert image to text** using **Tesseract** for cross‑platform projects.
- **Extract text from PDF** by rendering each page to an image first.
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}