---
category: general
date: 2026-03-17
description: Извлекать текст из PNG с помощью Aspose OCR в C#. Научитесь считывать
  текст с изображения, обрабатывать OCR чеков и создавать OCR‑движок с ускорением
  на GPU.
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: ru
og_description: Извлекать текст из PNG с помощью Aspose OCR. Это руководство показывает,
  как считывать текст с изображения, обрабатывать OCR чеков и эффективно создавать
  OCR‑движок.
og_title: Извлечь текст из PNG – Читать текст с изображения с помощью OCR
tags:
- OCR
- CSharp
- Aspose
title: Извлечь текст из PNG – Читать текст с изображения с помощью OCR
url: /ru/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из PNG – Чтение текста из изображения с помощью OCR

Когда‑нибудь вам нужно было **извлечь текст из PNG**, но вы не были уверены, какая библиотека даст надёжные результаты? Вы не одиноки — разработчики постоянно спрашивают: «Как прочитать текст из файлов изображений, например чеков, без написания собственного нейронного сетевого решения?» Хорошая новость в том, что Aspose OCR делает всю тяжёлую работу за вас, и вы даже можете задействовать GPU для ускорения.

В этом руководстве мы пройдём всё, что нужно для **обработки OCR чеков**, от установки пакета NuGet до создания OCR‑движка, который понимает ваш PNG‑файл. К концу вы получите автономное консольное приложение, которое читает изображение чека, выводит распознанный текст и показывает, как настроить движок под разные сценарии. Без внешних документов, только чистый код и понятные объяснения.

## Prerequisites

- .NET 6.0 SDK (или любая современная версия .NET)  
- Visual Studio 2022 или VS Code с расширениями C#  
- Поддерживаемый GPU NVIDIA с последним драйвером (необязательно, но рекомендуется для режима GPU)  
- Пакет **Aspose.OCR** NuGet (`dotnet add package Aspose.OCR`)  

Если у вас нет GPU, пример всё равно можно запустить в режиме CPU — просто пропустите строки конфигурации GPU.

## Step 1: Install Aspose.OCR and Set Up the Project

Сначала создайте новый консольный проект и подключите библиотеку Aspose OCR.

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Почему это важно: пакет `Aspose.OCR` содержит OCR‑движок, загрузчики изображений и опциональную поддержку GPU. Добавление его через NuGet гарантирует, что вы получите последнюю стабильную версию (на март 2026 года это 23.10).

## Step 2: Import Namespaces and Create the OCR Engine

Теперь откройте **Program.cs** и добавьте необходимые директивы `using`. Затем создайте экземпляр движка.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**Pro tip:** Если вы столкнётесь с `System.DllNotFoundException` на машинах без GPU, просто закомментируйте две строки, где задаются `EngineMode` и `GpuDeviceId`. Движок автоматически переключится на CPU.

## Step 3: Load the PNG Image You Want to Extract Text From

Aspose OCR может читать изображения напрямую из пути к файлу, потока или даже массива байтов. Для этой демонстрации мы загрузим локальное изображение чека.

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Обратите внимание, как мы проверяем наличие файла. В реальных приложениях, вероятно, следует показывать пользователю дружелюбное сообщение вместо простого завершения программы.

## Step 4: Perform the OCR Recognition

Само извлечение текста происходит одним вызовом метода. Движок возвращает объект `OcrResult`, содержащий сырую строку, оценки уверенности и информацию о разметке.

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

Почему мы проверяем `ocrResult.Text`: иногда PNG низкого качества возвращает пустую строку, и лучше уведомить пользователя, чем молча ничего не выводить.

## Step 5: Output the Recognized Text

Наконец, выведите извлечённую строку в консоль. При желании её можно записать в файл, базу данных или передать в другой сервис.

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Когда вы запустите программу (`dotnet run`), вы увидите примерно следующее:

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

Это **полное решение для извлечения текста из PNG** файлов с помощью Aspose OCR, и вы только что научились **читать текст из изображения**, похожего на чек.

## Optional: Fine‑Tuning the OCR Engine (Advanced)

Если требуется более высокая точность для определённых шрифтов или шумного фона, рассмотрите возможность изменения следующих параметров:

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

Эти настройки особенно полезны, когда вы **обрабатываете OCR чеков** в пакетных заданиях, где некоторые сканы далеки от идеала.

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **GPU driver missing** | Движок пытается загрузить CUDA, но не может найти DLL. | Установите последний драйвер NVIDIA или переключитесь в режим CPU, удалив строку `EngineMode.Gpu`. |
| **Incorrect image path** | `ImageStream.FromFile` бросает исключение, если файл не найден. | Всегда проверяйте путь (см. Шаг 3) или используйте `Path.Combine` для кросс‑платформенной надёжности. |
| **Low confidence on blurry receipts** | OCR‑движок не может различить символы. | Включите `EnableImagePreprocessing` и, при необходимости, увеличьте DPI изображения перед передачей в движок. |
| **Memory leak in long‑running services** | Каждый `OcrEngine` удерживает неуправляемые ресурсы. | Освобождайте движок после использования: `using var ocrEngine = new OcrEngine();` |

## Full Working Example (Copy‑Paste)

Ниже представлен **полный код программы**, который можно вставить в `Program.cs`. В нём все необязательные настройки закомментированы для лёгкой активации.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Сохраните, запустите `dotnet run`, и вы увидите содержимое чека, выведенное в консоль.

![пример извлечения текста из png](receipt.png "пример извлечения текста из png")

*На изображении выше показан пример PNG‑чека, который может обработать код.*

## Recap

Мы рассмотрели, как **извлекать текст из PNG** файлов с помощью Aspose OCR, продемонстрировали, как **читать текст из изображения**, и прошли полный конвейер **обработки OCR чеков**, включающий опциональное ускорение GPU. Создавая **OCR‑движок** самостоятельно, вы получаете полный контроль над конфигурацией, производительностью и обработкой ошибок.

## What to Explore Next?

- **Пакетная обработка**: пройтись по каталогу PNG‑чеков и записать каждый результат в CSV‑файл.  
- **Интеграция с Azure Functions**: превратить это консольное приложение в безсерверный эндпоинт, принимающий загрузку изображений.  
- **Поддержка нескольких языков**: заменить `Language.English` на `Language.Spanish` или добавить собственные словари.  
- **Постобработка**: использовать регулярные выражения для извлечения полей, таких как общая сумма, дата или ИНН, из сырой OCR‑строки.

Экспериментируйте — OCR оказывается удивительно гибким инструментом, когда знаете, какие настройки менять. Если возникнут проблемы, оставьте комментарий ниже или обратитесь к справочнику Aspose OCR API для более глубокого изучения.

Happy coding, and enjoy turning those stubborn PNG receipts into searchable text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}