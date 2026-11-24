---
category: general
date: 2026-06-16
description: Выполните OCR изображения с помощью Aspose OCR на C#. Узнайте пошагово,
  как получить результаты в формате JSON, работать с файлами и устранять распространённые
  проблемы.
draft: false
keywords:
- perform OCR on image
- Aspose OCR C#
- JSON result handling
- C# image recognition
- OCR engine configuration
language: ru
og_description: Выполните OCR изображения с помощью Aspose OCR на C#. Это руководство
  проведёт вас через вывод JSON, настройку движка и практические советы.
og_title: Выполнить OCR изображения в C# – Полный учебник Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Perform OCR on image using Aspose OCR in C#. Learn step‑by‑step how
    to get JSON results, handle files, and troubleshoot common issues.
  headline: Perform OCR on Image in C# with Aspose – Complete Programming Guide
  type: TechArticle
- questions:
  - answer: Aspose.OCR handles PNG, JPEG, BMP, TIFF, and GIF. If you need to work
      with PDFs, convert each page to an image first (Aspose.PDF can help).
    question: What image formats are supported?
  - answer: Yes – set `ocrEngine.Settings.ResultFormat = ResultFormat.Text;`. JSON
      is preferred when you need more metadata.
    question: Can I get plain text instead of JSON?
  - answer: Feed each page image to `RecognizeImage` in a loop and concatenate the
      results, or use `RecognizePdf` which returns a combined JSON structure.
    question: How do I handle multi‑page documents?
  - answer: For batch processing, reuse a single `OcrEngine` instance rather than
      creating a new one per image. Also, enable `RecognitionMode.Fast` if accuracy
      can be traded for speed.
    question: Performance concerns?
  - answer: Without a license, the output JSON will include a watermark field. Apply
      your license early in `Main` with `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.
    question: License warnings?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: Выполнить OCR изображения в C# с Aspose – Полное руководство по программированию
url: /ru/net/text-recognition/perform-ocr-on-image-in-c-with-aspose-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнение OCR на изображении в C# – Полное руководство по программированию

Когда‑нибудь вам нужно было **perform OCR on image** файлы, но вы не знали, как превратить сырые пиксели в пригодный текст? Вы не одиноки. Независимо от того, сканируете ли вы чеки, извлекаете данные из паспортов или оцифровываете старые документы, возможность **perform OCR on image** данных программно меняет правила игры для любого разработчика .NET.

В этом руководстве мы пройдем практический пример, который показывает, как именно **perform OCR on image** с помощью библиотеки Aspose.OCR, захватить результаты в JSON и сохранить их для последующей обработки. К концу вы получите готовое к запуску консольное приложение, понятные объяснения каждой настройки и несколько профессиональных советов, чтобы избежать распространенных ошибок.

## Prerequisites

Прежде чем начать, убедитесь, что у вас есть:

- .NET 6.0 SDK или более поздняя версия (можно скачать с сайта Microsoft).  
- Действующая лицензия Aspose.OCR или бесплатная пробная версия – библиотека работает без лицензии, но добавляет водяной знак.  
- Файл изображения (PNG, JPEG или TIFF), который вы хотите **perform OCR on image** – для этого руководства будем использовать `receipt.png`.  
- Visual Studio 2022, VS Code или любой другой предпочитаемый редактор.

Дополнительные пакеты NuGet, помимо `Aspose.OCR`, не требуются.

## Step 1: Set Up the Project and Install Aspose.OCR

Сначала создайте новый консольный проект и подключите библиотеку OCR.

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Если вы используете Visual Studio, можете добавить пакет через UI NuGet Package Manager. Он автоматически восстановит зависимости, избавив вас от ручного `dotnet restore` позже.

Теперь откройте `Program.cs` – заменим его содержимое кодом, который действительно **perform OCR on image**.

## Step 2: Create and Configure the OCR Engine

Ядром любого рабочего процесса Aspose OCR является класс `OcrEngine`. Ниже мы создаём его экземпляр и указываем движку выводить результаты в формате JSON – формате, который легко парсить позже.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonResultDemo
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2.2: Tell the engine we want JSON output.
        ocrEngine.Settings.ResultFormat = ResultFormat.Json;

        // Optional: tweak language or recognition speed.
        // ocrEngine.Settings.Language = Language.English; // default is English
        // ocrEngine.Settings.RecognitionMode = RecognitionMode.Fast; // or Accurate
```

**Почему устанавливать `ResultFormat` в JSON?**  
JSON независим от языка и может быть десериализован в строго типизированные объекты в C#, JavaScript, Python или любой другой среде, с которой вы работаете. Он также сохраняет оценки уверенности и координаты ограничивающих рамок, что удобно для последующей валидации.

## Step 3: Perform OCR on Image and Capture JSON

Теперь, когда движок готов, мы действительно **perform OCR on image**, вызывая `RecognizeImage`. Метод возвращает строку, содержащую JSON‑полезную нагрузку.

```csharp
        // Step 3: Perform OCR on the image and capture the JSON output.
        // Replace the path with the location of your own image file.
        string imagePath = "YOUR_DIRECTORY/receipt.png";
        string jsonResult = ocrEngine.RecognizeImage(imagePath);
```

> **Edge case:** Если изображение повреждено или путь указан неверно, `RecognizeImage` бросит `FileNotFoundException`. Оберните вызов в `try/catch`, если требуется более мягкая обработка ошибок.

## Step 4: Save the JSON Result for Further Processing

Сохранение вывода OCR позволяет передать его в базы данных, API или UI‑компоненты позже. Вот простой способ записать JSON на диск.

```csharp
        // Step 4: Save the JSON result for later use.
        string outputPath = "YOUR_DIRECTORY/receipt.json";
        File.WriteAllText(outputPath, jsonResult);
```

Если вы работаете в облачной среде, можете заменить `File.WriteAllText` вызовом к Azure Blob Storage или AWS S3 – строка JSON будет работать так же.

## Step 5: Notify the User and Clean Up

Небольшое сообщение в консоли подтверждает, что всё прошло успешно. В реальном приложении вы, возможно, будете логировать это в файл или отправлять в службу мониторинга.

```csharp
        // Step 5: Inform the user that the JSON file has been saved.
        Console.WriteLine("JSON result saved to " + outputPath);
    }
}
```

Это весь процесс! Запустите программу командой `dotnet run`, и вы увидите подтверждающее сообщение, а также файл `receipt.json`, содержащий примерно следующее:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $23.45",
          "Confidence": 0.98,
          "Rectangle": { "X": 120, "Y": 340, "Width": 150, "Height": 20 }
        }
      ]
    }
  ]
}
```

## Full, Runnable Example

Для полноты, вот *точный* файл, который можно скопировать‑вставить в `Program.cs`. Никаких частей не пропущено.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonResultDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2: Configure the engine to return results in JSON format.
        ocrEngine.Settings.ResultFormat = ResultFormat.Json;

        // Optional: adjust language or recognition mode if needed.
        // ocrEngine.Settings.Language = Language.English;
        // ocrEngine.Settings.RecognitionMode = RecognitionMode.Accurate;

        // Step 3: Perform OCR on the image and capture the JSON output.
        string imagePath = "YOUR_DIRECTORY/receipt.png";
        string jsonResult = ocrEngine.RecognizeImage(imagePath);

        // Step 4: Save the JSON result for further processing.
        string outputPath = "YOUR_DIRECTORY/receipt.json";
        File.WriteAllText(outputPath, jsonResult);

        // Step 5: Notify that the JSON file has been saved.
        Console.WriteLine($"JSON result saved to {outputPath}");
    }
}
```

> **Tip:** Замените `YOUR_DIRECTORY` на абсолютный путь или относительный от корня проекта. Использование `Path.Combine(Environment.CurrentDirectory, "receipt.png")` избавляет от жёстко заданных разделителей для Windows и Linux.

## Common Questions & Gotchas

- **Какие форматы изображений поддерживаются?**  
  Aspose.OCR работает с PNG, JPEG, BMP, TIFF и GIF. Если нужно обрабатывать PDF, сначала преобразуйте каждую страницу в изображение (может помочь Aspose.PDF).

- **Можно ли получить обычный текст вместо JSON?**  
  Да – установите `ocrEngine.Settings.ResultFormat = ResultFormat.Text;`. JSON предпочтителен, когда нужны дополнительные метаданные.

- **Как обрабатывать многостраничные документы?**  
  Передавайте каждое изображение страницы в `RecognizeImage` в цикле и объединяйте результаты, либо используйте `RecognizePdf`, который возвращает объединённую структуру JSON.

- **Беспокоит производительность?**  
  При пакетной обработке переиспользуйте один экземпляр `OcrEngine`, а не создавайте новый для каждого изображения. Также включите `RecognitionMode.Fast`, если допускаете снижение точности ради скорости.

- **Предупреждения о лицензии?**  
  Без лицензии в выходном JSON будет поле с водяным знаком. Примените лицензию сразу в `Main` с помощью `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.

## Visual Overview

Ниже представлена быстрая диаграмма, визуализирующая поток данных: файл изображения → OCR‑движок → JSON‑вывод → хранилище. Она помогает понять, где каждый шаг вписывается в более крупный конвейер.

![Выполнение OCR на изображении – схема рабочего процесса](https://example.com/ocr-workflow.png "Выполнение OCR на изображении")

*Alt text: Диаграмма, показывающая, как выполнять OCR на изображении с помощью Aspose OCR, преобразовывать результат в JSON и сохранять в файл.*

## Extending the Example

Теперь, когда вы знаете, как **perform OCR on image** и получить JSON‑payload, вы можете:

- **Разобрать JSON** с помощью `System.Text.Json` или `Newtonsoft.Json`, чтобы извлечь конкретные поля.  
- **Вставить текст в базу данных** для поисковых архивов.  
- **Интегрировать с веб‑API**, чтобы клиенты могли загружать изображения и мгновенно получать результаты OCR.  
- **Применить предварительную обработку изображений** (выравнивание, повышение контрастности) с помощью `Aspose.Imaging` для лучшей точности.

Все эти темы опираются на фундамент, который мы рассмотрели, и тот же экземпляр `OcrEngine` можно переиспользовать.

## Conclusion

Вы только что узнали, как **perform OCR on image** файлы в C# с помощью Aspose OCR, настроить движок для вывода JSON и сохранить результаты для последующего использования. Руководство охватило каждую строку кода, объяснило, почему важна каждая настройка, и указало на возможные крайние случаи в продакшене.

Отсюда экспериментируйте с разными языками (`ocrEngine.Settings.Language`), меняйте `RecognitionMode` или подключайте JSON к последующим аналитическим конвейерам. Возможности безграничны, когда вы сочетаете надёжный OCR с современными инструментами .NET.

Если это руководство оказалось полезным, поставьте звёздочку репозиторию Aspose.OCR на GitHub, поделитесь статьёй с коллегами или оставьте комментарий со своими советами. Счастливого кодинга!

## What Should You Learn Next?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом материале. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как использовать Aspose OCR для получения результата в формате JSON при распознавании изображений](/ocr/english/net/text-recognition/get-result-as-json/)
- [Как извлечь текст из изображения с помощью Aspose.OCR для .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Преобразовать изображение в текст – выполнить OCR на изображении по URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}