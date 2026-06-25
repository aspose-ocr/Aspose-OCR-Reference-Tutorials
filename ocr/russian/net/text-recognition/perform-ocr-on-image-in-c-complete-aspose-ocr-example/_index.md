---
category: general
date: 2026-06-25
description: Выполнить OCR изображения с помощью C# и Aspose OCR, затем в C# записать
  JSON‑файл и сохранить его, предоставив чёткий пошаговый пример.
draft: false
keywords:
- perform ocr on image
- c# write json file
- save json file c#
- aspose ocr example
- load image for ocr
language: ru
og_description: Выполните OCR изображения с помощью C# и Aspose OCR, затем сохраните
  результат в формате JSON. Полное, готовое к запуску руководство для разработчиков.
og_title: Распознавание текста на изображении в C# – Полный пример Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on image using C# and Aspose OCR, then c# write json file
    and save json file c# with a clear, step‑by‑step example.
  headline: Perform OCR on Image in C# – Complete Aspose OCR Example
  type: TechArticle
- questions:
  - answer: It builds a platform‑independent path, preventing “file not found” errors
      on Windows vs. Linux.
    question: Why use `Path.Combine`?
  - answer: The engine scans the bitmap, applies language‑specific classifiers, and
      builds a hierarchical result object containing pages, blocks, lines, and words.
    question: What happens under the hood?
  - answer: Human‑readable output makes debugging easier, especially when you later
      feed the JSON into other services.
    question: Why pretty‑print?
  - answer: Wrap the write in a try/catch and surface a clear message—this helps in
      Docker containers where the working directory may be mounted read‑only.
    question: What if the folder is read‑only?
  type: FAQPage
tags:
- C#
- Aspose OCR
- JSON
- Image Processing
title: Выполнить OCR изображения в C# — Полный пример Aspose OCR
url: /ru/net/text-recognition/perform-ocr-on-image-in-c-complete-aspose-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнить OCR на изображении в C# – Полный пример Aspose OCR

Когда‑то вам нужно **выполнить OCR на изображении** из консольного приложения C#, но вы не знали, как извлечь текст и сохранить его в удобном виде? Вы не одиноки. Во многих автоматизированных конвейерах — например, при оцифровке счетов или многоязычном архивировании документов — возможность превратить картинку в индексируемый текст и затем **c# write json file** становится настоящим ускорителем продуктивности.

В этом руководстве мы пройдём сквозной **aspose ocr example**, который загружает изображение, извлекает символы, формирует результат в красиво отформатированном JSON и, наконец, **save json file c#** на диск. К концу вы получите автономную программу, которую можно добавить в любой проект .NET.

![Perform OCR on image example](perform-ocr-on-image.png "Screenshot showing OCR result – perform ocr on image")

## Что вы получите

- **Load image for OCR** с помощью `OcrImage.FromFile` из Aspose.OCR.  
- **Perform OCR on image** одним вызовом метода.  
- Преобразование результата распознавания в красиво отформатированную строку JSON.  
- **Save JSON file C#** с помощью `File.WriteAllText`.  
- Понимание типичных подводных камней (отсутствие пакета NuGet, неподдерживаемые форматы изображений, работа с Unicode).

Никаких внешних сервисов, никаких облачных ключей — только чистый C# код, работающий локально.

---

## Шаг 1: Настройка проекта и добавление Aspose.OCR

Прежде чем **perform OCR on image**, нам нужны нужные библиотеки.

1. Откройте Visual Studio (или ваш любимый IDE) и создайте новое **Console App (.NET 6 или новее)**.  
2. Откройте NuGet Package Manager и установите `Aspose.OCR`:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Если вы таргетируете .NET Framework, тот же пакет работает, но убедитесь, что у вас минимум .NET 4.6.2.

> **Why this matters:** Aspose.OCR включает языковые пакеты и высокопроизводительный движок, поэтому вам не нужно поставлять отдельные OCR‑бинарники.

---

## Шаг 2: Загрузка изображения для OCR

Движку нужен экземпляр `OcrImage`. Здесь и происходит **load image for OCR**.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Create the OCR engine
        var ocrEngine = new OcrEngine();

        // 👉 Load the image you want to recognize
        var imagePath = Path.Combine(Environment.CurrentDirectory, "multi_lang.png");
        var image = OcrImage.FromFile(imagePath);

        // Continue with recognition...
```

- **Почему использовать `Path.Combine`?** Он формирует кроссплатформенный путь, предотвращая ошибки «file not found» в Windows и Linux.  
- **Поддерживаемые форматы:** PNG, JPEG, BMP, TIFF. Если передать PDF, Aspose.OCR бросит `NotSupportedException`.

---

## Шаг 3: Выполнение OCR на изображении

Теперь основная операция. Одна строка делает всю тяжёлую работу.

```csharp
        // Perform OCR recognition on the image
        var ocrResult = ocrEngine.Recognize(image);
```

- **Что происходит под капотом?** Движок сканирует битмап, применяет языковые классификаторы и формирует иерархический объект результата, содержащий страницы, блоки, строки и слова.  
- **Edge case:** Если изображение пустое или слишком шумное, `ocrResult` может содержать пустое поле `Text`. Проверьте `ocrResult.IsEmpty`, чтобы избежать проблем.

---

## Шаг 4: Преобразование результата в JSON (c# write json file)

`OcrResult` из Aspose.OCR уже умеет сериализоваться. Мы запросим у него *pretty‑printed* JSON‑строку.

```csharp
        // Convert the recognition result to a nicely formatted JSON string
        string jsonResult = ocrResult.ToJson(prettyPrint: true);
```

- **Почему pretty‑print?** Человекочитаемый вывод упрощает отладку, особенно когда позже передаёте JSON в другие сервисы.  
- **Альтернатива:** Если нужен компактный payload для передачи по сети, установите `prettyPrint: false`.

---

## Шаг 5: Сохранение JSON‑файла C# – сохранение результата

Наконец, записываем JSON на диск. Это часть **save json file c#** в руководстве.

```csharp
        // Define where the JSON will be saved
        var jsonPath = Path.Combine(Environment.CurrentDirectory, "result.json");

        // Write the JSON string to the file system
        File.WriteAllText(jsonPath, jsonResult);

        // Inform the user
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

- **Примечание по кодировке:** `WriteAllText` по умолчанию использует UTF‑8, что сохраняет любые Unicode‑символы, извлечённые из многоязычных изображений.  
- **Что если папка только для чтения?** Оберните запись в `try/catch` и выведите понятное сообщение — это помогает в Docker‑контейнерах, где рабочий каталог может быть смонтирован только для чтения.

---

## Полный рабочий пример

Собрав всё вместе, получаем полную программу, которую можно скопировать в `Program.cs` и запустить сразу (при условии, что `multi_lang.png` находится рядом с исполняемым файлом).

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Step 1: Create OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        var imagePath = Path.Combine(Environment.CurrentDirectory, "multi_lang.png");
        var image = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR on image
        var ocrResult = ocrEngine.Recognize(image);

        // Optional: guard against empty results
        if (ocrResult == null || ocrResult.IsEmpty)
        {
            Console.WriteLine("No text recognized. Check the image quality.");
            return;
        }

        // Step 4: Convert result to pretty‑printed JSON
        string jsonResult = ocrResult.ToJson(prettyPrint: true);

        // Step 5: Save JSON file C#
        var jsonPath = Path.Combine(Environment.CurrentDirectory, "result.json");
        File.WriteAllText(jsonPath, jsonResult);

        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### Ожидаемый вывод

При запуске программы вы увидите примерно следующее:

```
JSON saved to C:\Projects\OcrDemo\result.json
```

Открытие `result.json` покажет структурированный документ:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Lines": [
            {
              "Words": [
                { "Text": "Hello", "Confidence": 0.98 },
                { "Text": "World", "Confidence": 0.97 }
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

Точное содержание зависит от исходного изображения, но схема JSON остаётся постоянной — это идеально для последующей обработки (например, загрузки в ElasticSearch или NoSQL‑хранилище).

---

## Часто задаваемые вопросы и подводные камни

| Question | Answer |
|----------|--------|
| **Do I need a license?** | Aspose.OCR работает в режиме оценки до 20 страниц. Для продакшна понадобится файл лицензии (`Aspose.OCR.lic`). |
| **What languages are supported?** | English, French, German, Spanish, Chinese, Japanese, Arabic и многие другие. Установите `ocrEngine.Language = Language.English;` для ограничения или `ocrEngine.Language = Language.All;` для автоопределения. |
| **Can I process PDFs directly?** | Not with Aspose.OCR alone. Pair it with Aspose.PDF to rasterize pages into images first. |
| **Why is the JSON empty?** | Usually a low‑contrast image. Try increasing contrast or using `ocrEngine.Config.PreprocessOptions` to enhance the bitmap. |
| **Is the JSON schema stable?** | Yes, Aspose guarantees backward compatibility for the `ToJson` output across minor releases. |

---

## Расширение примера

Теперь, когда вы знаете, как **perform OCR on image** и **save json file c#**, вы можете:

- **Batch process** папку изображений (`Directory.GetFiles(..., "*.png")`).  
- **Upload the JSON** в REST‑API с помощью `HttpClient`.  
- **Insert the text** в базу данных для поисковых архивов.  
- **Add image preprocessing** (deskew, binarization) через `ocrEngine.Config.PreprocessOptions`.

Все эти задачи следуют одной схеме: загрузить → распознать → сериализовать → сохранить.

---

## Заключение

Мы только что завершили лаконичный **aspose ocr example**, демонстрирующий, как **perform OCR on image**, преобразовать результат в **pretty‑printed JSON** и **save JSON file C#** всего несколькими строками кода. Подход прост, не требует внешних сервисов и может быть расширен под любые производственные сценарии.

Попробуйте, поиграйте с настройками языка и наблюдайте, как улучшается точность OCR. Если возникнут проблемы, обратитесь к документации Aspose.OCR или оставьте комментарий ниже — приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, развивая техники, показанные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}