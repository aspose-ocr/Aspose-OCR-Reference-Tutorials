---
category: general
date: 2026-04-17
description: Изучите пример Aspose OCR для чтения файлов изображений на C#, извлечения
  текста из изображения на C# и записи JSON‑файла на C#. Полный пошаговый учебник
  по OCR на C#.
draft: false
keywords:
- aspose ocr example
- write json file c#
- read image file c#
- extract text image c#
- c# ocr tutorial
language: ru
og_description: Освойте пример Aspose OCR для чтения изображения, извлечения текста
  и записи JSON‑файла с помощью C#. Следуйте этому краткому руководству по OCR на
  C#.
og_title: пример aspose ocr – преобразовать текст изображения в JSON на C#
tags:
- Aspose
- OCR
- C#
- JSON
title: пример aspose ocr – преобразовать текст изображения в JSON на C#
url: /ru/net/text-recognition/aspose-ocr-example-convert-image-text-to-json-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# aspose ocr example – Преобразование текста изображения в JSON на C#

Когда‑нибудь вам нужен был **aspose ocr example**, который не только читает изображение, но и выдаёт аккуратный JSON для дальнейшей обработки? Вы не одиноки. Во многих проектах — автоматизация счетов, сканирование чеков или даже простое архивирование документов — разработчики сталкиваются с одной и той же проблемой: «Как получить результат OCR в формате, который любит мой API?»

Хорошие новости? С Aspose.OCR это можно сделать в паре строк кода, и я покажу, как именно. К концу этого руководства вы узнаете, как **read image file C#**, **extract text image C#** и **write JSON file C#** — всё в чистом, переиспользуемом C# OCR‑уроке.

## Что понадобится

- .NET 6.0 или новее (код также компилируется с .NET Core)  
- Aspose.OCR for .NET NuGet package (`Install-Package Aspose.OCR`)  
- Изображение (`input.jpg`) с чётким, машинно‑читаемым текстом  
- Текстовый редактор или Visual Studio (подойдёт любой IDE)  

Никаких дополнительных файлов конфигурации, никаких скрытых магий — только SDK и картинка.

## Шаг 1 – Чтение файла изображения C# с помощью Aspose.OCR

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

## Шаг 2 – Инициализация движка Aspose OCR

Creating the engine is cheap, but you should wrap it in a `using` statement so resources are released promptly.

```csharp
// Create the OCR engine – it holds all the recognition settings
using var ocrEngine = new OcrEngine();
```

*Pro tip:* The default engine works well for most Latin‑based texts. If you need a different language, you can set `ocrEngine.Language = Language.YourLanguage;` before calling `Recognize`.

## Шаг 3 – Извлечение текста из изображения C# – Выполнение распознавания

Now the heavy lifting happens. The `Recognize` method returns an `OcrResult` object that contains the raw text, confidence scores, and bounding boxes for each word.

```csharp
// Run OCR – this is the “extract text image C#” step
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);
```

You’ll notice `ocrResult.Text` holds the plain string, while `ocrResult.Regions` gives you positional data if you ever need to highlight words in a UI.

## Шаг 4 – Запись JSON файла C# – Сериализация результата

Serializing to JSON is straightforward with `System.Text.Json`. We’ll pretty‑print the output so it’s human‑readable.

```csharp
using System.Text.Json;

// Convert the OCR result to nicely formatted JSON
string json = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true });
```

*Why we use `System.Text.Json`*: It’s built into .NET, fast, and doesn’t require extra dependencies. If you prefer Newtonsoft, the code changes only a few lines.

## Шаг 5 – Сохранение JSON на диск

Finally, write the string to a file. This completes the **write json file c#** portion.

```csharp
// Destination path for the JSON output
string jsonOutputPath = @"C:\MyProject\Output\ocrResult.json";

// Save the JSON – now you have a portable data file
File.WriteAllText(jsonOutputPath, json);

Console.WriteLine("OCR data saved as JSON.");
```

### Ожидаемый вывод JSON (пример)

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

## Полный C# OCR tutorial – Все шаги вместе

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

### Запуск кода

1. Replace the two `@"C:\MyProject\…"` paths with your actual directories.  
2. Build the project (`dotnet build`) and run it (`dotnet run`).  
3. Open `output.json`—you should see a nicely structured representation of the image’s text.

## Часто задаваемые вопросы и особые случаи

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

## Профессиональные советы и подводные камни

- **File paths:** Use `Path.Combine` to avoid hard‑coded backslashes, especially if you ever move to Linux.  
- **Memory:** For massive batches, reuse a single `OcrEngine` instance instead of creating a new one per image.  
- **JSON size:** If you only need the text, drop the `Regions` property to keep the payload tiny.  
- **Version check:** This tutorial was tested with Aspose.OCR 23.9.0; newer versions keep the same API surface, but always glance at the release notes for breaking changes.

![Пример вывода OCR JSON – пример aspose ocr](https://example.com/sample-ocr-json.png "предпросмотр JSON aspose ocr example")

## Заключение

We’ve walked through a complete **aspose ocr example** that reads an image, extracts its text, and writes the result to a JSON file using pure C#. The solution is self‑contained, production‑ready, and easy to extend—whether you want to add language support, tweak confidence thresholds, or feed the JSON into a downstream service.

If you’re looking for the next step, try chaining this tutorial with a **C# OCR tutorial** that uploads the JSON to Azure Cognitive Search, or experiment with extracting tables from invoices. The sky’s the limit once you have the JSON in hand.

Got a twist you’d like to share? Drop a comment, fork the repo, or ping me on GitHub. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}