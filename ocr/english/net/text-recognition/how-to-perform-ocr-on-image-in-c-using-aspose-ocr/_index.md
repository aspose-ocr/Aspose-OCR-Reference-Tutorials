---
category: general
date: 2026-10-11
description: Learn how to perform OCR on image in C# with Aspose.OCR, including installing
  System.Drawing.Common and extracting text from JPG files.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: en
lastmod: 2026-10-11
og_description: Perform OCR on image in C# using Aspose.OCR. This guide shows you
  how to install System.Drawing.Common, load an image for OCR, and extract text from
  JPG.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: Perform OCR on image in C# – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: How to perform OCR on image in C# using Aspose.OCR
url: /net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to perform OCR on image in C# using Aspose.OCR

If you need to **perform OCR on image** files in a .NET application, this guide shows you a complete solution. Using Aspose.OCR you can quickly **recognize text from picture** files such as JPGs and display the result in a console window.

You will learn how to:

* **install System.Drawing.Common package** – the library that supplies the `Image` class,
* **load image for OCR** – read a JPEG or PNG into memory,
* configure the language model,
* **perform OCR on image** and finally,
* **extract text from JPG** and output it.

The steps are written for .NET 6+, but they also work with .NET Framework 4.6.1 or later.

---

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | Provides the runtime for the C# console app. |
| Visual Studio 2022 (or any IDE) | Makes it easy to add NuGet packages and run the program. |
| Internet connection (first run only) | Aspose.OCR downloads the language module automatically. |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | Used to demonstrate **extract text from JPG**. |

---

## Step 1: Install System.Drawing.Common package

The `System.Drawing.Common` NuGet package supplies the `Image` class that you will **load image for OCR**. Open the Package Manager Console and run:

```powershell
Install-Package System.Drawing.Common
```

> **Pro tip:** Target `net6.0-windows` or add `<UseWindowsForms>true</UseWindowsForms>` to the project file if you encounter platform‑specific warnings on Linux/macOS.

---

## Step 2: Add the Aspose.OCR NuGet package

Aspose.OCR contains the OCR engine and language models. Install it with:

```powershell
Install-Package Aspose.OCR
```

The package is lightweight; the required language data (e.g., Cyrillic) is downloaded the first time you set `OcrEngine.Language`.

---

## Step 3: How to load image for OCR

Loading the picture is the first concrete step before you can **perform OCR on image**. The `Image.FromFile` method reads any format supported by GDI+, including JPG, PNG, BMP, and TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*If the file does not exist, `FileNotFoundException` is thrown – wrap the call in a try/catch block for production code.*

---

## Step 4: Configure the engine and **perform OCR on image**

Create an `OcrEngine` instance, select the language model, assign the loaded image, and call `Recognize()`.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

The `Recognize()` method returns an `OcrResult` object that holds the extracted text, confidence scores, and bounding boxes. The language module is downloaded automatically on first use, so no extra files are required.

---

## Step 5: **Extract text from JPG** and display it

Now you can **recognize text from picture** and output the result. The `Text` property of `OcrResult` contains the plain string.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Expected console output

```
Recognized text:
Пример текста на кириллице
```

If the source image contains English text, the output will be the English sentence you placed in the picture.

---

## Edge cases and best‑practice tips

| Situation | Recommendation |
|-----------|----------------|
| **Large images ( > 5 MB )** | Resize the image to ≤ 2000 px on the longest side before OCR to reduce memory usage and improve speed. |
| **Multiple languages in one picture** | Call `ocrEngine.AddLanguage(OcrLanguage.English)` in addition to Cyrillic, then set `ocrEngine.Language = OcrLanguage.Multilingual`. |
| **Low‑contrast scans** | Increase contrast with `System.Drawing.Graphics` before passing the bitmap to the engine. |
| **Running on Linux/macOS** | Ensure the `libgdiplus` native dependency is installed (`sudo apt-get install -y libgdiplus`). |
| **Repeated OCR calls** | Reuse the same `OcrEngine` instance and only replace `ocrEngine.Image` to avoid repeated module loading. |

---

## Full, runnable program

Below is the complete console application that incorporates all previous steps. Copy the code into a new C# console project, replace the image path, and run it.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Running the program** prints the recognized string to the console, confirming that you have successfully **performed OCR on image** and **extracted text from JPG**.

---

## Conclusion

You now know how to **perform OCR on image** files in C# using Aspose.OCR, from installing the required **System.Drawing.Common package** to **loading image for OCR**, selecting the appropriate language, and finally **extracting text from JPG**. This end‑to‑end example gives you a solid foundation for building more advanced document‑processing pipelines, such as batch‑processing folders of pictures or integrating OCR into a web API.

### What’s next?

* Explore **recognize text from picture** in PDFs by converting each page to an image first.
* Experiment with the `OcrEngine` properties `Resolution`, `Threshold`, and `MaxProcessingTime` to fine‑tune accuracy on noisy scans.
* Combine the OCR output with a natural‑language processing library to automatically categorize extracted content.

Feel free to adapt the code for other image formats, add error handling, or integrate it into larger applications. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image in C# – Complete Aspose OCR Guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}