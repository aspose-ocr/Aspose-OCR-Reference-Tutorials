---
category: general
date: 2026-04-06
description: Распознавать текст на изображении с помощью Aspose OCR в C#. Узнайте,
  как извлекать текст, загружать файл изображения в C# и записывать JSON в C# с простым
  пошаговым примером.
draft: false
keywords:
- recognize image text
- how to extract text
- write json in c#
- load image file c#
language: ru
og_description: распознавание текста на изображении с помощью Aspose OCR в C#. Это
  руководство показывает, как быстро извлечь текст, загрузить файл изображения в C#
  и записать JSON в C#.
og_title: Распознавание текста на изображении в C# – Полное пошаговое руководство
tags:
- OCR
- C#
- Aspose
title: Распознавание текста на изображении в C# – Полное руководство с экспортом в
  JSON
url: /ru/net/text-recognition/recognize-image-text-in-c-full-guide-with-json-export/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание текста на изображении в C# – Полное пошаговое руководство

Когда‑нибудь вам нужно было **распознавать текст на изображении** со сканированного чека, но вы не знали, какую библиотеку выбрать? Вы не одиноки. Во многих реальных приложениях — трекерах расходов, обработчиках счетов, даже инструментах доступности — извлечение слов из картинки является первой преградой.  

В этом руководстве мы пройдем практическое решение, которое **распознает текст на изображении** с помощью библиотеки Aspose OCR, показывает **как извлечь текст**, демонстрирует **загрузку файла изображения c#** корректно и, наконец, **записывает json в c#**, чтобы вы могли сохранять или передавать результаты. К концу вы получите готовое к запуску консольное приложение, которое преобразует любой PNG в аккуратный JSON‑payload.

---

## Что понадобится

- **.NET 6+** (код работает и с .NET Framework 4.8, но .NET 6 — оптимальный вариант).
- **Aspose.OCR for .NET** пакет NuGet. Установите его командой `dotnet add package Aspose.OCR`.
- Пример изображения (`input.png`), размещённый в месте, доступном вашему приложению.  
- Visual Studio 2022 или любой другой редактор по вашему выбору — никаких сложных трюков IDE не требуется.

> Подсказка: храните файлы изображений в папке `Resources` внутри проекта; это упрощает пути и избавляет от ошибок «file not found».

## Шаг 1: распознавание текста на изображении – Загрузка файла изображения

Прежде чем движок OCR сможет выполнить свою магию, необходимо **загрузить файл изображения c#** безопасно. Метод `Image.FromFile` бросает исключение, если путь неверен или файл имеет неподдерживаемый формат, поэтому мы защитим его.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // Verify the image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // Load the image – this is the “load image file c#” step
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // Continue to OCR...
        }
    }
}
```

*Почему это важно*: загрузка изображения внутри блока `using` гарантирует своевременное освобождение неуправляемых ресурсов GDI+, предотвращая утечки памяти в длительно работающих сервисах.

## Шаг 2: Как извлечь текст с помощью Aspose OCR

Теперь, когда bitmap находится в памяти, мы передаём его **движку распознавания текста на изображении**. `OcrEngine` от Aspose прост в использовании: создаём экземпляр, вызываем `Recognize`, и получаем объект `OcrResult`, содержащий исходный текст, оценки уверенности и даже ограничивающие рамки.

```csharp
// Inside the using block from Step 1
var ocrEngine = new OcrEngine();

// Perform OCR – this is the core “how to extract text” operation
OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

// Quick sanity check
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("⚠️ No text detected. Try a clearer image.");
    return;
}
Console.WriteLine("✅ OCR succeeded. Extracted text:");
Console.WriteLine(ocrResult.Text);
```

*Объяснение*: метод `Recognize` запускает встроенную нейронную сеть. Он лучше всего работает с изображениями высокого контраста, 300 DPI. Если подать размытое фото, уверенность падает — рассмотрите предобработку (выравнивание, бинаризация) для продакшн‑кода.

## Шаг 3: Запись JSON в C# – Экспорт результата OCR

Большинство API ожидают JSON, поэтому мы **запишем json в c#** с помощью `JsonExport` от Aspose. Библиотека сериализует весь `OcrResult`, сохраняет информацию о строках и значения уверенности.

```csharp
// Still inside the same using block
string jsonResult = JsonExport.ToJson(ocrResult);

// Persist the JSON to disk
File.WriteAllText(outputPath, jsonResult);
Console.WriteLine($"💾 JSON written to {outputPath}");
```

### Ожидаемый вывод JSON

```json
{
  "Text": "Total: $12.34\r\nDate: 2026-04-01\r\n...",
  "Words": [
    { "Text": "Total", "Confidence": 0.98, "Rectangle": { "X": 10, "Y": 15, "Width": 50, "Height": 12 } },
    { "Text": "$12.34", "Confidence": 0.96, "Rectangle": { "X": 70, "Y": 15, "Width": 45, "Height": 12 } }
    // … more words …
  ]
}
```

*Почему JSON?* Он независим от языка, легко десериализуется и сохраняет подробные метаданные OCR, которые могут понадобиться для последующей валидации.

## Шаг 4: Полная, исполняемая программа

Собрав все части вместе, представляем полный консольный пример. Скопируйте‑вставьте, восстановите пакеты NuGet и нажмите **F5**.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Configuration – adjust these paths as needed
        // -------------------------------------------------
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // -------------------------------------------------
        // Validate input file
        // -------------------------------------------------
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // -------------------------------------------------
        // Load image (load image file c#)
        // -------------------------------------------------
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // -------------------------------------------------
            // Initialize OCR engine and recognize text
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("⚠️ No text detected. Try a clearer image.");
                return;
            }

            Console.WriteLine("✅ OCR succeeded. Sample output:");
            Console.WriteLine(ocrResult.Text.Substring(0, Math.Min(100, ocrResult.Text.Length)) + "...");

            // -------------------------------------------------
            // Convert result to JSON (write json in c#)
            // -------------------------------------------------
            string jsonResult = JsonExport.ToJson(ocrResult);
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"💾 JSON written to {outputPath}");
        }
    }
}
```

Запустите программу и откройте `Resources/output.json` — вы увидите аккуратно структурированное представление JSON всего, что распознал движок.

## Обработка распространённых граничных случаев

| Ситуация | Что делать | Почему |
|-----------|------------|-----|
| **Изображение равно null или повреждено** | Оберните `Image.FromFile` в try/catch и запишите исключение в журнал. | Предотвращает падение приложения и предоставляет понятное сообщение об ошибке. |
| **Низкие оценки уверенности** | Проверьте `ocrResult.Words[i].Confidence`. Если ниже 0.75, рассмотрите предобработку (увеличьте DPI, резкость). | Повышает надёжность последующих процессов, таких как извлечение суммы. |
| **Большие файлы (>10 МБ)** | Уменьшите масштаб изображения перед OCR (`receiptImage = new Bitmap(receiptImage, new Size(width/2, height/2))`). | Снижает нагрузку на память и ускоряет распознавание. |
| **Документы на нескольких языках** | Установите `ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;` | Позволяет движку обнаруживать символы обоих языков. |

## Бонус: Визуализация результата OCR (опционально)

Если вы хотите увидеть, где каждое слово расположено на изображении, вы можете нарисовать ограничивающие рамки:

```csharp
using (Graphics g = Graphics.FromImage(receiptImage))
{
    foreach (var word in ocrResult.Words)
    {
        var rect = new Rectangle(word.Rectangle.X, word.Rectangle.Y,
                                 word.Rectangle.Width, word.Rectangle.Height);
        g.DrawRectangle(Pens.Red, rect);
    }
    receiptImage.Save(Path.Combine("Resources", "annotated.png"));
}
```

Полученный `annotated.png` покажет красные прямоугольники вокруг каждого распознанного слова — удобно для отладки.

## Заключение

Мы только что **распознали текст на изображении** в C# от начала до конца: загрузка файла изображения, вызов Aspose OCR для **извлечения текста**, и наконец **запись json в c#**, чтобы данные могли перемещаться куда угодно. Полный пример работает сразу, а дополнительные советы помогут вам справиться с размытыми чеками, большими файлами или многоязычными сканами.

Что дальше? Попробуйте заменить Aspose на другой движок (Tesseract, Microsoft OCR) и сравнить оценки уверенности, либо передать JSON в базу данных для отчётов о расходах. Вы также можете расширить консольное приложение в ASP .NET Core Web API, принимающий загрузку изображений и мгновенно возвращающий JSON.

Есть вопросы о масштабировании, обработке ошибок или интеграции с Azure Functions? Оставьте комментарий или напишите мне на GitHub. Счастливого кодинга, и пусть ваш OCR всегда будет чётким! 

![Скриншот вывода OCR в JSON – пример распознавания текста на изображении](https://example.com/ocr-example.png "пример распознавания текста на изображении")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}