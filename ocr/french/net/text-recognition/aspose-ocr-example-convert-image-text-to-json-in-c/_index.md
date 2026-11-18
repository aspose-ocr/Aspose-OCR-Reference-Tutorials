---
category: general
date: 2026-04-17
description: Apprenez un exemple Aspose OCR pour lire un fichier image en C#, extraire
  le texte d’une image en C# et écrire un fichier JSON en C#. Tutoriel OCR complet
  étape par étape en C#.
draft: false
keywords:
- aspose ocr example
- write json file c#
- read image file c#
- extract text image c#
- c# ocr tutorial
language: fr
og_description: Maîtrisez un exemple Aspose OCR pour lire une image, extraire le texte
  et écrire un fichier JSON en C#. Suivez ce tutoriel concis d'OCR en C#.
og_title: exemple Aspose OCR – Convertir le texte d'image en JSON en C#
tags:
- Aspose
- OCR
- C#
- JSON
title: exemple Aspose OCR – Convertir le texte d’image en JSON en C#
url: /fr/net/text-recognition/aspose-ocr-example-convert-image-text-to-json-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# aspose ocr example – Convert Image Text to JSON in C#

Vous avez déjà eu besoin d’un **aspose ocr example** qui non seulement lit une image mais génère aussi du JSON propre pour le traitement en aval ? Vous n’êtes pas seul. Dans de nombreux projets—automatisation de factures, numérisation de reçus, ou même archivage simple de documents—les développeurs rencontrent le même obstacle : « Comment obtenir le résultat OCR dans un format que mon API adore ? »

Bonne nouvelle ? Avec Aspose.OCR, vous pouvez le faire en quelques lignes, et je vais vous montrer exactement comment. À la fin de ce guide, vous saurez comment **read image file C#**, **extract text image C#**, et **write JSON file C#**—le tout enveloppé dans un tutoriel OCR C# propre et réutilisable.

## What You’ll Need

- .NET 6.0 ou version ultérieure (le code compile également avec .NET Core)  
- Package NuGet Aspose.OCR for .NET (`Install-Package Aspose.OCR`)  
- Une image (`input.jpg`) contenant du texte clair et lisible par machine  
- Un éditeur de texte ou Visual Studio (tout IDE convient)  

Pas de fichiers de configuration supplémentaires, pas de magie cachée—juste le SDK et une image.

## Step 1 – Read image file C# with Aspose.OCR

First thing’s first: you have to feed the OCR engine a valid image. Aspose.OCR expects an `OcrImage` object, which you can create directly from a file path.

```csharp
using Aspose.OCR;
using System.IO;

// Path to the source picture
string imagePath = @"C:\MyProject\Images\input.jpg";

// Load the image – this is the “read image file C#” part
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

*Why this matters:* Loading the image early lets you validate the file existence and catch format issues before the engine even starts crunching pixels. If the file is missing, `FromFile` throws a clear exception you can handle downstream.

## Step 2 – Initialize the Aspose OCR engine

Creating the engine is cheap, but you should wrap it in a `using` statement so resources are released promptly.

```csharp
// Create the OCR engine – it holds all the recognition settings
using var ocrEngine = new OcrEngine();
```

*Pro tip:* The default engine works well for most Latin‑based texts. If you need a different language, you can set `ocrEngine.Language = Language.YourLanguage;` before calling `Recognize`.

## Step 3 – Extract text image C# – Perform the recognition

Now the heavy lifting happens. The `Recognize` method returns an `OcrResult` object that contains the raw text, confidence scores, and bounding boxes for each word.

```csharp
// Run OCR – this is the “extract text image C#” step
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);
```

You’ll notice `ocrResult.Text` holds the plain string, while `ocrResult.Regions` gives you positional data if you ever need to highlight words in a UI.

## Step 4 – Write JSON file C# – Serialize the result

Serializing to JSON is straightforward with `System.Text.Json`. We’ll pretty‑print the output so it’s human‑readable.

```csharp
using System.Text.Json;

// Convert the OCR result to nicely formatted JSON
string json = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true });
```

*Why we use `System.Text.Json`*: It’s built into .NET, fast, and doesn’t require extra dependencies. If you prefer Newtonsoft, the code changes only a few lines.

## Step 5 – Persist the JSON to disk

Finally, write the string to a file. This completes the **write json file c#** portion.

```csharp
// Destination path for the JSON output
string jsonOutputPath = @"C:\MyProject\Output\ocrResult.json";

// Save the JSON – now you have a portable data file
File.WriteAllText(jsonOutputPath, json);

Console.WriteLine("OCR data saved as JSON.");
```

### Expected JSON output (sample)

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑01\nTotal: $1,234.56",
  "Regions": [
    {
      "BoundingBox": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Confidence": 0.98,
      "Text": "Invoice #12345"
    },
    {
      "BoundingBox": { "X": 10, "Y": 60, "Width": 150, "Height": 30 },
      "Confidence": 0.96,
      "Text": "Date: 2024‑03‑01"
    },
    {
      "BoundingBox": { "X": 10, "Y": 100, "Width": 180, "Height": 30 },
      "Confidence": 0.99,
      "Text": "Total: $1,234.56"
    }
  ]
}
```

*Note:* The exact numbers will differ based on your image, but the structure stays the same—perfect for feeding into APIs, databases, or front‑end visualizers.

## Full C# OCR tutorial – All steps combined

Below is the complete, copy‑and‑paste‑ready program that ties everything together. No missing pieces, no “see the docs” shortcuts.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\MyProject\Images\input.jpg";
        var ocrImage = OcrImage.FromFile(imagePath);

        // -------------------------------------------------
        // Step 2: Create and configure the OCR engine
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine();
        // Example: ocrEngine.Language = Language.English; // optional

        // -------------------------------------------------
        // Step 3: Perform OCR recognition
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // -------------------------------------------------
        // Step 4: Serialize the result to indented JSON
        // -------------------------------------------------
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // -------------------------------------------------
        // Step 5: Write the JSON to a file
        // -------------------------------------------------
        string jsonOutputPath = @"C:\MyProject\Output\output.json";
        File.WriteAllText(jsonOutputPath, json);

        // -------------------------------------------------
        // Step 6: Let the user know we’re done
        // -------------------------------------------------
        Console.WriteLine("OCR data saved as JSON.");
    }
}
```

### Running the code

1. Replace the two `@"C:\MyProject\…"` paths with your actual directories.  
2. Build the project (`dotnet build`) and run it (`dotnet run`).  
3. Open `output.json`—you should see a nicely structured representation of the image’s text.

## Common Questions & Edge Cases

**What if my image is blurry?**  
Aspose.OCR offers pre‑processing options like `ocrEngine.ImagePreprocessOptions.Deskew = true;`. Enable them before calling `Recognize` to improve accuracy.

**Can I limit the output to just the plain text?**  
Sure—simply serialize `ocrResult.Text` instead of the whole object:

```csharp
string plainJson = JsonSerializer.Serialize(
    new { Text = ocrResult.Text },
    new JsonSerializerOptions { WriteIndented = true });
```

**Do I need to handle multi‑page PDFs?**  
The example focuses on a single image, but you can loop through each page image, run the same steps, and aggregate results into a JSON array.

## Pro Tips & Gotchas

- **File paths:** Use `Path.Combine` to avoid hard‑coded backslashes, especially if you ever move to Linux.  
- **Memory:** For massive batches, reuse a single `OcrEngine` instance instead of creating a new one per image.  
- **JSON size:** If you only need the text, drop the `Regions` property to keep the payload tiny.  
- **Version check:** This tutorial was tested with Aspose.OCR 23.9.0; newer versions keep the same API surface, but always glance at the release notes for breaking changes.

![Exemple de sortie JSON OCR – exemple aspose ocr](https://example.com/sample-ocr-json.png "aperçu JSON de l'exemple aspose ocr")

## Conclusion

We’ve walked through a complete **aspose ocr example** that reads an image, extracts its text, and writes the result to a JSON file using pure C#. The solution is self‑contained, production‑ready, and easy to extend—whether you want to add language support, tweak confidence thresholds, or feed the JSON into a downstream service.

If you’re looking for the next step, try chaining this tutorial with a **C# OCR tutorial** that uploads the JSON to Azure Cognitive Search, or experiment with extracting tables from invoices. The sky’s the limit once you have the JSON in hand.

Got a twist you’d like to share? Drop a comment, fork the repo, or ping me on GitHub. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}