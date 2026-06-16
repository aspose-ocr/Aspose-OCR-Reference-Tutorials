---
category: general
date: 2026-05-02
description: c# ocr tutorial that shows how to extract text image c# and recognize
  png text, then write indented json using JsonSerializer c#. Step‑by‑step guide for
  developers.
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: en
og_description: c# ocr tutorial that demonstrates how to extract text image c# and
  recognize png text, then write indented json with JsonSerializer c#. Complete, runnable
  example.
og_title: c# ocr tutorial – Extract Text and Export as Indented JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: c# ocr tutorial – Extract Text from Images and Export as Indented JSON
url: /net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Extract Text from Images and Export as Indented JSON

Ever needed a **c# ocr tutorial** that goes from a picture of text straight to a nicely formatted JSON file? You're not the only one. In many projects – think invoice scanning, receipt parsing, or even simple meme‑text extraction – you end up with a PNG file and wonder how to pull the words out without writing a custom recognizer.  

This guide gives you a hands‑on solution: we’ll **extract text image c#** using Aspose.OCR, **recognize png text**, and then **write indented json** with `JsonSerializer` in C#. By the end you’ll have a self‑contained console app that you can drop into any .NET solution. No vague “see the docs” links, just a complete, copy‑and‑paste‑ready example.

## What You’ll Need

- **.NET 6** (or any recent .NET version). Older frameworks work, but the syntax shown targets .NET 6+.
- **Aspose.OCR for .NET** – install via NuGet: `dotnet add package Aspose.OCR`.
- A sample PNG image (`text.png`) containing clear, machine‑readable text.
- An IDE or editor of your choice – Visual Studio, VS Code, Rider, etc.

> **Pro tip:** If you plan to process many images, consider re‑using a single `OcrEngine` instance rather than creating a new one per file. It reduces overhead and improves throughput.

## Step 1: Set Up a c# ocr tutorial Project

First, spin up a console project. The following commands create the scaffolding and pull in the OCR library:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

Now open the generated `Program.cs`. We’ll replace its contents with the full example later, but for now just make sure the project builds:

```bash
dotnet build
```

If you see no errors, you’re ready to move on.

## Step 2: Recognize PNG Text from an Image

The heart of any **c# ocr tutorial** is the OCR engine itself. Aspose.OCR abstracts away the low‑level details and gives you a clean `OcrEngine` class. Below we create the engine, point it at a PNG file, and ask it to recognize the text.

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### Why This Works

- **`RecognizeImage`** accepts many formats (PNG, JPEG, BMP). We specifically **recognize png text** because PNG preserves lossless detail, which is ideal for OCR.
- The returned `OcrResult` contains not only the plain text but also a per‑glyph confidence score, useful if you need to filter low‑confidence characters later.

## Step 3: Write Indented JSON with JsonSerializer c#

Now that we have `ocrResult`, the next logical step in our **c# ocr tutorial** is to turn that object into human‑readable JSON. The built‑in `System.Text.Json` serializer does the job, and we’ll configure it to **write indented json** for clarity.

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### Using `JsonSerializer` Correctly

- The `WriteIndented` flag is the simplest way to **write indented json** without pulling in third‑party libraries.
- If you ever need camel‑case property names, add `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` to the options.
- The `jsonOutput` string can be saved with `File.WriteAllText("result.json", jsonOutput);` – a handy tweak for real‑world pipelines.

## Step 4: Run and Verify the Output

Compile and run the program:

```bash
dotnet run
```

Assuming `text.png` contains the phrase *“Hello, OCR World!”*, you should see something like:

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

That JSON is **indented**, making it easy to read in logs or to hand‑off to downstream services.

### Edge Cases & Tips

| Situation | What to Do |
|-----------|------------|
| **Image is blurry** | Increase `ocrEngine.Config.Dpi` (e.g., `ocrEngine.Config.Dpi = 300`) before calling `RecognizeImage`. |
| **Non‑English language** | Set `ocrEngine.Config.Language = OcrLanguage.German` (or any supported language). |
| **Large batch of files** | Loop over a directory, reusing the same `OcrEngine` instance; store each JSON result with a unique filename. |
| **Need only high‑confidence text** | Filter `ocrResult.Lines` where `Confidence` ≥ 0.95 before serialization. |

## Full Working Example (Copy‑Paste Ready)

Below is the *entire* program, ready to drop into `Program.cs`. It includes all the steps, error handling, and comments that make the code self‑explanatory.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

Run the code, inspect the console or the generated `.json` file, and you’ll see the extracted text along with confidence scores, all neatly **indented**.

## Conclusion

You now have a solid **c# ocr tutorial** that shows how to **extract text image c#**, **recognize png text**, and **write indented json** using `JsonSerializer`. The example is complete, runnable, and includes practical tips for real‑world scenarios.  

Next steps? Try swapping out Aspose.OCR for another engine (e.g., Tesseract) and see how the `OcrResult` shape changes, or feed the JSON into a downstream API that stores OCR data in a database. You could also experiment with **use jsonserializer c#** options like custom converters for date formatting or enum handling.

Happy coding, and may your OCR pipelines be ever accurate!  

---  

![c# ocr tutorial diagram](image.png "Diagram illustrating OCR flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}