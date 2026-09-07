---
category: general
date: 2026-09-06
description: Конвертация OCR‑изображения в JSON в C# с использованием Aspose.OCR –
  пошаговое руководство по извлечению текста из изображения и получению JSON‑вывода.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: ru
lastmod: 2026-09-06
og_description: OCR изображение в JSON на C# с Aspose.OCR. Узнайте, как загрузить
  изображение для OCR, распознать текст с фотографии и преобразовать результат в JSON.
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: Преобразовать изображение OCR в JSON на C# – полное руководство по Aspose.OCR
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
title: Как преобразовать изображение OCR в JSON на C# с помощью Aspose.OCR
url: /ru/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как преобразовать изображение OCR в JSON на C# с Aspose.OCR

Если вам нужно **ocr image to json** в приложении .NET, это руководство покажет, как сделать это с помощью Aspose.OCR. Мы пройдем процесс загрузки изображения для OCR, распознавания текста с фотографии и преобразования результата в JSON, чтобы вы могли использовать данные в API или базах данных.

Извлечение текста из файлов изображений — распространенная задача для обработки счетов, сканирования чеков и архивных проектов. К концу этого урока вы сможете **convert image to text**, получить результат в виде обычного текста и создать структурированный JSON‑payload, сохраняющий информацию о разметке.

## Prerequisites

Прежде чем начать, убедитесь, что у вас есть:

- .NET 6.0 SDK или более поздняя версия  
- Visual Studio 2022 (или любой редактор, поддерживающий .NET)  
- Пакет NuGet Aspose.OCR (`Aspose.OCR`), добавленный в ваш проект  
- Пример изображения (`input.jpg`), помещенный в папку, к которой можно обратиться из кода  

Дополнительные OCR‑движки не требуются; Aspose.OCR выполняет всю тяжелую работу внутри.

## Step 1: Install the Aspose.OCR NuGet package

Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

Пакет содержит класс `Aspose.OCR.OcrEngine`, предоставляющий методы для **load image for ocr**, выбора языка и экспорта результата.

## Step 2: Create a new C# console project

Если у вас еще нет проекта, создайте его:

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

Добавьте необходимые директивы `using`:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## Step 3: Load the image and configure the OCR engine

Следующий код демонстрирует, как **load image for ocr**, установить язык и подготовить движок к обработке. В примере используется кириллица, но вы можете переключиться на `OcrLanguage.English`, `OcrLanguage.French` и т.д., в зависимости от исходного языка.

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

> **Почему это важно:** Установка правильного языка существенно повышает точность при **recognize text from photo**. Движок использует языковые словари и наборы символов.

## Step 4: Run the OCR process and retrieve results

Запустите OCR‑движок. Если процесс завершится успешно, вы сможете **extract text from image** в виде обычного текста, HTML или JSON. Aspose.OCR предоставляет метод `SaveJson`, который записывает структурированный результат в файл.

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

Типичный файл `output.json` выглядит так (отформатировано для удобства чтения):

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

JSON‑payload содержит текст каждой строки, оценку уверенности и прямоугольник, охватывающий строку на оригинальном фото. Это упрощает сопоставление результата OCR с элементами UI или полями базы данных.

## Step 5: Full source code for the demo

Ниже приведена полная, готовая к запуску программа, реализующая workflow **ocr image to json**. Скопируйте её в `Program.cs` и выполните `dotnet run`.

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

1. Поместите изображение с именем `input.jpg` в корень проекта.  
2. Выполните `dotnet run`.  
3. Посмотрите вывод в консоли и откройте `output.json`, чтобы увидеть структурированные данные.

## Pro tips and common pitfalls

| Situation | Recommendation |
|-----------|----------------|
| **Low‑resolution photos** | Increase DPI before processing or use `ocrEngine.Image = ImageStream.FromFile(path, 300)` to force 300 DPI. |
| **Mixed languages** | Set `ocrEngine.Language = OcrLanguage.Multilingual` and optionally supply a language list via `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }`. |
| **Large documents** | Process one page at a time to keep memory usage low; the engine supports multi‑page TIFFs. |
| **Incorrect characters** | Verify that the correct `OcrLanguage` is selected; using the wrong language reduces accuracy when you **convert image to text**. |
| **JSON missing fields** | Ensure you are using Aspose.OCR version 23.6 or later; older releases did not expose the `SaveJson` method. |

## Frequently asked questions

**Q: Можно ли получить результат OCR в виде массива байтов вместо файла?**  
A: Да. Используйте `ocrEngine.SaveJson(Stream)`, чтобы записать напрямую в `MemoryStream`, затем вызовите `stream.ToArray()`.

**Q: Поддерживает ли движок ввод PDF?**  
A: Aspose.OCR может принимать страницы PDF, предварительно преобразованные в изображения с помощью Aspose.PDF, но сам OCR‑движок работает только с растровыми изображениями. Сначала конвертируйте PDF в изображения, затем **load image for ocr**.

**Q: Как работать с письмами, пишущимися справа налево, например, арабским?**  
A: Установите `ocrEngine.Language = OcrLanguage.Arabic`. JSON будет включать правильное направление текста, которое можно отобразить в UI‑фреймворках, поддерживающих RTL.

## Conclusion

Теперь у вас есть полное решение для **ocr image to json** на C#. Загрузив изображение, настроив язык, запустив OCR‑движок и экспортировав результат в JSON, вы можете **extract text from image**, **convert image to text** и **recognize text from photo** в одном упрощённом процессе.  

Дальше вы можете:

- Интегрировать JSON‑вывод в Web API (`ASP.NET Core`)  
- Сохранять результат в NoSQL‑базе данных, такой как MongoDB  
- Добавить пост‑обработку для исправления типичных ошибок OCR  

Экспериментируйте с разными языками, форматами изображений и вариантами вывода, чтобы подобрать оптимальное решение для вашего проекта. Приятного кодинга!

## What Should You Learn Next?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [recognize text from image in C# – Complete Guide to OCR and JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Convert Image to Text in C# with Aspose OCR – Step‑by‑Step Guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}