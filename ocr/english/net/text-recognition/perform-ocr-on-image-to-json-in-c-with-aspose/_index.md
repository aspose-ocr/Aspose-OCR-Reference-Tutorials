---
category: general
date: 2026-04-08
description: Learn how to perform OCR on image and write JSON file C# using Aspose
  OCR. This aspose ocr c# tutorial shows OCR image to JSON conversion with confidence
  values.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: en
og_description: Perform OCR on image and export results to a JSON file in C#. This
  tutorial covers the full Aspose OCR C# workflow, including confidence scores.
og_title: Perform OCR on Image to JSON in C# – Aspose OCR Guide
tags:
- Aspose
- OCR
- C#
- JSON
title: Perform OCR on Image to JSON in C# with Aspose
url: /net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Perform OCR on Image to JSON in C# with Aspose

Ever needed to **perform OCR on image** files but weren't sure how to get the results into a structured format? You’re not alone—developers constantly ask, “How do I turn a scanned picture into usable data?” The good news is that Aspose.OCR makes this a piece of cake, and you can even **write JSON file C#**‑style with confidence scores included.

In this guide we’ll walk through a complete **aspose OCR C# tutorial** that covers everything from loading an image to exporting the recognized text as JSON. By the end you’ll have a runnable console app that **performs OCR on image**, converts the output to JSON (including confidence values), and saves it with a single line of code. No hidden steps, no external scripts—just pure C#.

## Prerequisites

Before we dive in, make sure you have:

- .NET 6.0 SDK or later (the code works with .NET Core and .NET Framework as well)
- Visual Studio 2022 (or any editor you like)
- A valid **Aspose.OCR for .NET** license or a free temporary license (the free trial works for testing)
- An image file (`input.png`) you want to process (any common format—PNG, JPG, BMP—will do)

That’s it. If you’re missing any of these, grab them now; the rest of the tutorial assumes they’re already in place.

## Step 1: Install the Aspose.OCR NuGet Package

First things first—add the library to your project. Open a terminal in the project folder and run:

```bash
dotnet add package Aspose.OCR
```

This pulls the latest version (as of April 2026 it’s 23.12) and adds the necessary DLLs to the `bin` folder. No extra configuration is required.

## Step 2: Initialize the OCR Engine (Perform OCR on Image)

Now we create an `OcrEngine` instance and tell it which language to use. English (`"en"`) is the most common, but you can swap it for `"fr"`, `"de"` or any supported language.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**Why we initialize here:** The `OcrEngine` holds all the configuration needed for the recognition process. Setting the language up‑front ensures the engine uses the correct character set, which dramatically improves accuracy.

## Step 3: Recognize the Image and Capture Confidence

With the engine ready, we feed it the image file. The `RecognizeImage` method returns an `OcrResult` object that contains both the extracted text and a confidence score for each word.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**What’s happening under the hood?** Aspose runs a neural‑network‑based recognizer that analyses each pixel block, matches it against its language model, and attaches a confidence value (0‑100) that tells you how sure it is about each word.

## Step 4: Convert the Result to JSON (OCR Image to JSON)

Aspose makes the conversion painless. By passing `includeConfidence: true` we get a JSON payload that looks like this:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

Here’s the code that produces the JSON string:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**Why include confidence?** If you plan to feed the data into downstream processes (e.g., validation, UI highlighting), knowing which words are shaky lets you decide whether to ask the user for confirmation.

## Step 5: Write the JSON File C#‑Style

Now we actually **write JSON file C#**. The `File.WriteAllText` method is atomic and works cross‑platform, making it perfect for console apps.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

That’s the entire workflow—five concise steps that **perform OCR on image**, transform the output to JSON, and persist it.

## Full Working Example

Below is the complete program you can copy‑paste into `Program.cs`. Make sure `input.png` lives in the same folder as the compiled binary or adjust the paths accordingly.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### Expected Output

When you run the program (`dotnet run`), you’ll see something like:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

And `output.json` will contain the structured JSON shown earlier, complete with confidence percentages for each word.

## Pro Tips & Edge Cases

- **Missing file handling:** Wrap the `RecognizeImage` call in a `try/catch` for `FileNotFoundException` if you expect dynamic paths.
- **Different languages:** Set `ocrEngine.Language = "fr"` for French, or load a custom language pack via `ocrEngine.LoadLanguage("custom.lang")`.
- **Large documents:** For multi‑page PDFs, convert each page to an image first (e.g., using `Aspose.PDF`) and loop through the OCR steps.
- **Performance tuning:** If you only need quick results, switch to `RecognitionMode.Fast`—you lose a bit of accuracy but gain speed.
- **JSON formatting:** Want pretty‑printed JSON? Use `JsonConvert.SerializeObject` from Newtonsoft with `Formatting.Indented` after deserializing the Aspose JSON string.

## Frequently Asked Questions

**Q: Does this work with .NET Framework?**  
A: Absolutely. The same NuGet package targets .NET Standard 2.0, so you can reference it from .NET Framework 4.6.1 and newer.

**Q: What if I need the confidence for the whole document, not per word?**  
A: The `OcrResult` also exposes `OverallConfidence`. You can add it manually to the JSON:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**Q: Can I stream the JSON directly to a web API?**  
A: Yes. Replace `File.WriteAllText` with an `HttpClient` POST that sends `jsonResult

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}