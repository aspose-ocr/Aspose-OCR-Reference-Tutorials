---
category: general
date: 2026-01-02
description: Извлекать текст из изображения с помощью Aspose OCR в C#. Узнайте, как
  быстро и надёжно преобразовать изображение в формат JSONL.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: ru
og_description: Извлекайте текст из изображения с помощью Aspose OCR и преобразуйте
  его в формат JSONL. Полный пошаговый учебник на C# для разработчиков.
og_title: Извлечение текста из изображения – преобразование в JSONL на C#
tags:
- C#
- OCR
- Aspose
- JSONL
title: Извлечение текста из изображения и преобразование в JSONL – руководство по
  C#
url: /ru/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения и преобразование в JSONL – Полный C#‑урок

Когда‑то вам нужно **извлечь текст из изображения**, но вы не знали, какая библиотека даст чистый, структурированный результат? Вы не одиноки. Во многих проектах по обработке чеков или оцифровке документов узким местом является превращение растрового изображения в поисковый текст *и* в машинно‑читаемый формат.  

Хорошие новости? С Aspose OCR вы можете **извлечь текст из изображения** и, используя несколько строк кода, **преобразовать изображение в JSONL** для последующего анализа. Это руководство проведёт вас через весь процесс — от загрузки PNG до записи файла JSON‑Lines, который можно передать в конвейер данных.

> **Подсказка:** Если вы уже используете .NET 6 или новее, тот же код работает без дополнительной конфигурации.

## Требования — Что понадобится

- **.NET 6 SDK** (или любая современная версия .NET)
- **Aspose.OCR** NuGet‑пакет  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** для сериализации  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- Пример изображения (например, `receipt.png`) в папке, к которой есть доступ.
- Любая IDE или редактор — Visual Studio, VS Code, Rider и т.д.

Никакой громоздкой настройки, никаких внешних сервисов, только несколько NuGet‑пакетов.

![Извлечение текста из изображения с помощью C#](https://example.com/assets/ocr-sample.png)

*Alt text: извлечение текста из изображения с помощью C# и Aspose OCR*

## Шаг 1: Загрузите изображение, которое хотите обработать  

Первое, что делаете, когда хотите **извлечь текст из изображения**, — передаёте OCR‑движку растровый битмап. Использовать `System.Drawing.Bitmap` просто и подходит для большинства растровых форматов.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **Почему это важно:** Загрузка изображения как `Bitmap` даёт OCR‑движку прямой доступ к пикселям, что повышает скорость распознавания и точность по сравнению с потоковой передачей сырых байтов.

## Шаг 2: Настройте Aspose OCR для вывода в формате JSON‑Lines  

Aspose OCR позволяет указать язык, формат вывода и несколько параметров производительности. Здесь мы запрашиваем **JSON‑Lines** (один JSON‑объект на строку), потому что это идеально подходит для построчной обработки позже.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **Совет профи:** Если нужны многоязычные чеки, установите `Language = Language.Multilingual` или передайте массив значений `Language`.

## Шаг 3: Запустите OCR и получите результат  

Теперь мы действительно **извлекаем текст из изображения**. Метод `Recognize` возвращает объект `OcrResult`, содержащий коллекцию `OcrLine`, каждая из которых представляет одну строку распознанного текста вместе с ограничивающим прямоугольником.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

На этом этапе `ocrResult.Lines` содержит всё, что нужно — сырой текст, оценки уверенности и координаты.

## Шаг 4: Сериализуйте строки в JSON‑Lines  

Мы превратим коллекцию в красиво отформатированную JSON‑строку. Хотя JSON‑Lines обычно компактны, добавление отступов упрощает просмотр файла во время разработки.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

Переменная `jsonLines` будет выглядеть примерно так (усечено для краткости):

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

Каждая строка заканчивается символом новой строки, образуя настоящий **JSONL** (JSON‑Lines) файл.

## Шаг 5: Запишите JSON‑Lines на диск  

Наконец, сохраняем результат, чтобы другие сервисы — такие как Spark, Logstash или простой Bash‑скрипт — могли потреблять его построчно.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

Открыв `receipt.jsonl`, вы увидите один JSON‑объект на каждой строке, готовый к потоковой передаче.

## Шаг 6: Проверьте экспорт  

Быстрая проверка спасёт часы отладки позже. Считаем первые несколько строк обратно и выведем их в консоль.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

Типичный вывод в консоли:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

Если вы видите что‑то похожее, поздравляем — вы успешно **извлекли текст из изображения** и **преобразовали изображение в JSONL**.

## Распространённые ошибки и способы их избежать  

| Проблема | Почему происходит | Как исправить |
|----------|-------------------|---------------|
| **Пустой вывод** | Неправильный путь к изображению или файл недоступен. | Проверяйте `File.Exists(imagePath)` перед созданием битмапа. |
| **Низкие оценки уверенности** | Изображение размытое или с низким контрастом. | Предобрабатывайте изображение (например, `Bitmap.RotateFlip`, `Graphics.Clear`) или увеличьте DPI. |
| **Неправильный язык** | OCR по умолчанию использует английский, а чек на другом языке. | Установите `options.Language = Language.Spanish` (или нужный enum). |
| **JSONL выглядит как один массив JSON** | Вы использовали `Formatting.None` без обработки переводов строк. | Убедитесь, что каждый сериализованный объект заканчивается `Environment.NewLine`. |

## Полный рабочий пример  

Ниже полностью готовая к запуску программа. Вставьте её в консольный проект и нажмите **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**Ожидаемый результат:** Файл `receipt.jsonl`, содержащий один JSON‑объект на строку, каждый с полями `Text`, `Confidence` и `BoundingBox`. Теперь его можно передать в любой аналитический конвейер, принимающий JSONL.

## Следующие шаги — выход за рамки базового OCR  

- **Пакетная обработка:** Оберните логику в цикл `foreach` для обработки целых папок чеков.  
- **Параллелизм:** Используйте `Parallel.ForEach` для ускорения на многоядерных системах при работе с тысячами изображений.  
- **Постобработка:** Отбрасывайте строки с низкой уверенностью (`Confidence < 0.9`) перед сохранением.  
- **Интеграция:** Отправляйте JSONL напрямую в Azure Blob Storage или AWS S3 с помощью соответствующих SDK.  
- **Альтернативные форматы:** Переключите `OutputFormat` на `PlainText` или `Xml`, если ваш downstream‑сервис предпочитает их.

## Заключение  

Теперь у вас есть надёжное сквозное решение для **извлечения текста из изображения** и **преобразования изображения в JSONL** с помощью Aspose OCR на C#. В уроке рассмотрены все шаги от загрузки битмапа до проверки результата, а также несколько практических советов для повышения надёжности конвейера.

Попробуйте на своих чеках, счетах или сканированных формах — наблюдайте, как OCR‑движок превращает пиксели в поисковый, построчно‑структурированный данные за секунды. Если встретите крайние случаи (например, наклонённые сканы или многоязычный текст), вернитесь к разделу *RecognitionOptions* и подкорректируйте язык или предобработку.

Удачной разработки, и пусть ваши конвейеры данных всегда остаются чистыми!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}