---
category: general
date: 2026-09-06
description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step guide
  to extract text from image and get JSON output.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: en
lastmod: 2026-09-06
og_description: ocr image to json in C# with Aspose.OCR. Learn how to load an image
  for OCR, recognize text from photo, and convert the result to JSON.
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: Convert an OCR image to JSON in C# – complete Aspose.OCR guide
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: How to convert an OCR image to JSON in C# with Aspose.OCR
url: /net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to convert an OCR image to JSON in C# with Aspose.OCR

If you need to **ocr image to json** in a .NET application, this guide shows you how to do it with Aspose.OCR. We'll walk through loading an image for OCR, recognizing text from photo, and converting the result to JSON so you can consume the data in APIs or databases.

Extracting text from image files is a common requirement for invoice processing, receipt scanning, and archival projects. By the end of this tutorial you will be able to **convert image to text**, retrieve the plain‑text result, and generate a structured JSON payload that preserves layout information.

## Prerequisites

Before you start, make sure you have:

- .NET 6.0 SDK or later installed  
- Visual Studio 2022 (or any editor that supports .NET)  
- An Aspose.OCR NuGet package (`Aspose.OCR`) added to your project  
- A sample image (`input.jpg`) placed in a folder you can reference from code  

You don't need any additional OCR engines; Aspose.OCR handles the heavy lifting internally.

## Step 1: Install the Aspose.OCR NuGet package

Open a terminal at your project folder and run:

```bash
dotnet add package Aspose.OCR
```

The package includes the `Aspose.OCR.OcrEngine` class, which provides methods for **load image for ocr**, language selection, and result export.

## Step 2: Create a new C# console project

If you don't already have a project, create one:

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

Add the `using` directives that you will need:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## Step 3: Load the image and configure the OCR engine

The following code demonstrates how to **load image for ocr**, set the language, and prepare the engine for processing. In this example we use Cyrillic, but you can switch to `OcrLanguage.English`, `OcrLanguage.French`, etc., depending on the source language.

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **Why this matters:** Setting the correct language dramatically improves accuracy when you **recognize text from photo**. The engine uses language‑specific dictionaries and character sets.

## Step 4: Run the OCR process and retrieve results

Now run the OCR engine. If the process succeeds, you can **extract text from image** as plain text, HTML, or JSON. Aspose.OCR provides a `SaveJson` method that writes the structured result to a file.

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### Expected JSON structure

A typical `output.json` file looks like this (formatted for readability):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

The JSON payload contains each line’s text, a confidence score, and the rectangle that encloses the line in the original photo. This makes it easy to map the OCR result back to UI elements or database fields.

## Step 5: Full source code for the demo

Below is the complete, ready‑to‑run program that performs the **ocr image to json** workflow. Copy it into `Program.cs` and run `dotnet run`.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### Running the example

1. Place an image named `input.jpg` in the project root.  
2. Execute `dotnet run`.  
3. Observe the console output and open `output.json` to see the structured data.

## Pro tips and common pitfalls

| Situation | Recommendation |
|-----------|----------------|
| **Low‑resolution photos** | Increase DPI before processing or use `ocrEngine.Image = ImageStream.FromFile(path, 300)` to force 300 DPI. |
| **Mixed languages** | Set `ocrEngine.Language = OcrLanguage.Multilingual` and optionally supply a language list via `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }`. |
| **Large documents** | Process one page at a time to keep memory usage low; the engine supports multi‑page TIFFs. |
| **Incorrect characters** | Verify that the correct `OcrLanguage` is selected; using the wrong language reduces accuracy when you **convert image to text**. |
| **JSON missing fields** | Ensure you are using Aspose.OCR version 23.6 or later; older releases did not expose the `SaveJson` method. |

## Frequently asked questions

**Q: Can I get the OCR result as a byte array instead of a file?**  
A: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`, then call `stream.ToArray()`.

**Q: Does the engine support PDF input?**  
A: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but the OCR engine itself works on raster images. Convert PDFs to images first, then **load image for ocr**.

**Q: How do I handle right‑to‑left scripts like Arabic?**  
A: Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the correct text direction, which you can render in UI frameworks that support RTL.

## Conclusion

You now have a complete solution for **ocr image to json** in C#. By loading an image, configuring the language, running the OCR engine, and exporting the result as JSON, you can **extract text from image**, **convert image to text**, and **recognize text from photo** in a single, streamlined workflow.  

From here you might explore:

- Integrating the JSON output with a Web API (`ASP.NET Core`)  
- Storing the result in a NoSQL database like MongoDB  
- Adding post‑processing to correct common OCR errors  

Feel free to experiment with different languages, image formats, and output options to fit your project’s needs. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [recognize text from image in C# – Complete Guide to OCR and JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Convert Image to Text in C# with Aspose OCR – Step‑by‑Step Guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}