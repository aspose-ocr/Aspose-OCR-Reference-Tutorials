---
category: general
date: 2026-05-02
description: c# OCR‑урок, показывающий, как извлекать текст из изображения в c# и
  распознавать текст в PNG, а затем записывать отформатированный JSON с помощью JsonSerializer
  c#. Пошаговое руководство для разработчиков.
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: ru
og_description: c# OCR‑урок, демонстрирующий, как извлечь текст из изображения в c#
  и распознать текст в PNG, затем записать отформатированный JSON с помощью JsonSerializer
  c#. Полный, готовый к запуску пример.
og_title: c# OCR руководство – извлечение текста и экспорт в JSON с отступами
tags:
- OCR
- C#
- Aspose
- JSON
title: c# OCR tutorial – извлечение текста из изображений и экспорт в отформатированный
  JSON
url: /ru/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Извлечение текста из изображений и экспорт в отформатированный JSON

Когда‑нибудь вам нужен был **c# ocr tutorial**, который переводит изображение текста сразу в красиво отформатированный файл JSON? Вы не одиноки. Во многих проектах — подумайте о сканировании счетов, разборе чеков или даже простом извлечении текста из мемов — вы получаете PNG‑файл и задаётесь вопросом, как извлечь слова без написания собственного распознавателя.  

Это руководство предоставляет практическое решение: мы будем **extract text image c#** с помощью Aspose.OCR, **recognize png text**, а затем **write indented json** с помощью `JsonSerializer` в C#. К концу у вас будет автономное консольное приложение, которое можно добавить в любой .NET‑проект. Никаких расплывчатых ссылок «см. документацию», только полный пример, готовый к копированию и вставке.

## Что понадобится

- **.NET 6** (или любая современная версия .NET). Более старые фреймворки работают, но показанный синтаксис ориентирован на .NET 6+.
- **Aspose.OCR for .NET** – установить через NuGet: `dotnet add package Aspose.OCR`.
- Пример PNG‑изображения (`text.png`) с чётким, машинно‑читаемым текстом.
- IDE или редактор по вашему выбору — Visual Studio, VS Code, Rider и т.д.

> **Pro tip:** Если вы планируете обрабатывать множество изображений, рассмотрите возможность повторного использования одного экземпляра `OcrEngine` вместо создания нового для каждого файла. Это уменьшит накладные расходы и повысит пропускную способность.

## Шаг 1: Настройка проекта c# ocr tutorial

Сначала создайте консольный проект. Ниже приведённые команды создают структуру и подключают библиотеку OCR:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

Теперь откройте сгенерированный `Program.cs`. Позже мы заменим его содержимое полным примером, а пока просто убедитесь, что проект собирается:

```bash
dotnet build
```

Если ошибок нет, вы готовы продолжать.

## Шаг 2: Распознавание PNG‑текста из изображения

Сердцем любого **c# ocr tutorial** является сам OCR‑движок. Aspose.OCR скрывает низкоуровневые детали и предоставляет чистый класс `OcrEngine`. Ниже мы создаём движок, указываем ему PNG‑файл и просим распознать текст.

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

### Почему это работает

- **`RecognizeImage`** принимает множество форматов (PNG, JPEG, BMP). Мы специально **recognize png text**, потому что PNG сохраняет детали без потерь, что идеально для OCR.
- Возвращаемый `OcrResult` содержит не только простой текст, но и оценку уверенности для каждого глифа, что полезно, если позже понадобится отфильтровать символы с низкой уверенностью.

## Шаг 3: Запись отформатированного JSON с помощью JsonSerializer c#

Теперь, когда у нас есть `ocrResult`, следующий логичный шаг в нашем **c# ocr tutorial** — преобразовать этот объект в читаемый человеком JSON. Встроенный сериализатор `System.Text.Json` справляется с задачей, и мы настроим его на **write indented json** для наглядности.

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

### Правильное использование `JsonSerializer`

- Флаг `WriteIndented` — самый простой способ **write indented json** без подключения сторонних библиотек.
- Если понадобится имена свойств в camel‑case, добавьте `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` в параметры.
- Строку `jsonOutput` можно сохранить с помощью `File.WriteAllText("result.json", jsonOutput);` — удобный приём для реальных конвейеров.

## Шаг 4: Запуск и проверка вывода

Скомпилируйте и запустите программу:

```bash
dotnet run
```

При условии, что `text.png` содержит фразу *«Hello, OCR World!»*, вы должны увидеть что‑то вроде:

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

Этот JSON **отформатирован**, что упрощает чтение в логах или передачу в downstream‑сервисы.

### Особые случаи и советы

| Ситуация | Что делать |
|-----------|------------|
| **Изображение размыто** | Увеличьте `ocrEngine.Config.Dpi` (например, `ocrEngine.Config.Dpi = 300`) перед вызовом `RecognizeImage`. |
| **Неанглийский язык** | Установите `ocrEngine.Config.Language = OcrLanguage.German` (или любой поддерживаемый язык). |
| **Большая партия файлов** | Пройдите по директории, переиспользуя один экземпляр `OcrEngine`; сохраняйте каждый JSON‑результат с уникальным именем файла. |
| **Требуется только текст с высокой уверенностью** | Отфильтруйте `ocrResult.Lines`, где `Confidence` ≥ 0.95 перед сериализацией. |

## Полный рабочий пример (готовый к копированию и вставке)

Ниже представлен *полный* код программы, готовый к вставке в `Program.cs`. Он включает все шаги, обработку ошибок и комментарии, делающие код самодокументируемым.

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

Запустите код, проверьте консоль или сгенерированный файл `.json`, и вы увидите извлечённый текст вместе с оценками уверенности, всё аккуратно **отформатировано**.

## Заключение

Теперь у вас есть надёжный **c# ocr tutorial**, показывающий, как **extract text image c#**, **recognize png text** и **write indented json** с помощью `JsonSerializer`. Пример полностью готов, исполняем и содержит практические советы для реальных сценариев.  

Что дальше? Попробуйте заменить Aspose.OCR другим движком (например, Tesseract) и посмотрите, как изменится структура `OcrResult`, либо передайте JSON в downstream‑API, которое сохраняет OCR‑данные в базе данных. Вы также можете поэкспериментировать с параметрами **use jsonserializer c#**, например, с пользовательскими конвертерами для форматирования дат или обработки enum‑ов.

Счастливого кодинга, и пусть ваши OCR‑конвейеры всегда работают точно!  

---  

![c# ocr tutorial diagram](image.png "Диаграмма, иллюстрирующая поток OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}