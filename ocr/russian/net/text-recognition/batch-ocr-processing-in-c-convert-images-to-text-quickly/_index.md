---
category: general
date: 2026-06-25
description: Учебник по пакетной обработке OCR демонстрирует, как преобразовать изображения
  в текст и извлекать текст из изображений с помощью Aspose.OCR на C#. Изучите пошаговую
  реализацию.
draft: false
keywords:
- batch ocr processing
- convert images to text
- how to extract text from images
language: ru
og_description: Пакетная обработка OCR в C# позволяет быстро преобразовывать изображения
  в текст. Следуйте этому руководству, чтобы узнать, как извлекать текст из изображений
  с помощью Aspose.OCR.
og_title: Пакетная обработка OCR в C# — преобразование изображений в текст
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  headline: Batch OCR Processing in C# – Convert Images to Text Quickly
  type: TechArticle
- description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  name: Batch OCR Processing in C# – Convert Images to Text Quickly
  steps:
  - name: Expected Output
    text: 'When you run `dotnet run`, you’ll see something like:'
  - name: What image formats are supported?
    text: Aspose.OCR handles JPEG, PNG, TIFF, BMP, and GIF out of the box. If you
      encounter a format like WebP, convert it first or use a third‑party decoder.
  - name: Can I limit the OCR language to English only?
    text: 'Yes. Set the `Language` property on the `BatchRecognizer` before calling
      `Recognize`:'
  - name: How do I process thousands of files without blowing up memory?
    text: Break the list into smaller batches (e.g., 500 files each) and run the above
      routine in a loop. This keeps the in‑memory dictionary manageable and lets you
      log progress per batch.
  - name: What if I need the OCR results in a database instead of files?
    text: 'Replace the `File.WriteAllText` call with your preferred data‑access code.
      For example, using Dapper:'
  type: HowTo
tags:
- OCR
- Aspose
- C#
title: Пакетная обработка OCR в C# — быстрое преобразование изображений в текст
url: /ru/net/text-recognition/batch-ocr-processing-in-c-convert-images-to-text-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Пакетная обработка OCR в C# – Быстрое преобразование изображений в текст

Задумывались ли вы когда‑нибудь, как выполнить **batch OCR processing** целой папки сканов без написания отдельного цикла для каждого файла? Вы не одиноки. Во многих проектах — например, автоматизация обработки счетов, архивирование старых документов или даже простая личная утилита «фото‑в‑текст» — вам нужно **convert images to text** в больших объёмах.  

Хорошая новость? С Aspose.OCR вы можете сделать именно это в паре строк кода. Это руководство проведёт вас через полностью готовый к запуску пример, показывающий **how to extract text from images** с использованием batch OCR processing, объясняет, почему каждый элемент важен, и даёт советы, как избежать распространённых подводных камней.

## Что вы узнаете

- Настроить Aspose.OCR для пакетных операций.
- Настроить параллелизм для ускорения больших задач.
- Автоматически записывать результаты OCR в отдельные файлы `.txt`.
- Обрабатывать события прогресса, чтобы всегда знать, что происходит.
- Расширять код для пользовательской обработки ошибок или разных форматов вывода.

Предыдущий опыт работы с Aspose не требуется; достаточно базовых знаний C# и установленного .NET 6 (или новее).

---

## Шаг 1: Подготовьте проект для пакетной обработки OCR

Прежде чем погрузиться в код, убедитесь, что у вас установлен пакет Aspose.OCR NuGet. Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Используйте последнюю стабильную версию (по состоянию на июнь 2026 это 23.9), чтобы получить улучшения производительности и новейшую поддержку языков.

Создайте новое консольное приложение, если у вас его ещё нет:

```bash
dotnet new console -n BatchOcrApp
cd BatchOcrApp
```

Теперь вы готовы написать реальную логику пакетной обработки OCR.

## Шаг 2: Определите файлы изображений, которые нужно конвертировать

Первый элемент **batch OCR processing** — просто указать распознавателю, какие файлы обрабатывать. Вы можете задать список вручную, читать из каталога или даже получать пути из базы данных. Для наглядности мы используем статический список:

```csharp
// Step 2: List of image files to be processed
var imageFiles = new List<string>
{
    @"C:\Images\invoice1.jpg",
    @"C:\Images\receipt2.png",
    @"C:\Images\scan3.tif"
};
```

> **Why this matters:** Передавая коллекцию, `BatchRecognizer` может внутренне распределять работу по нескольким потокам, что является ядром быстрых операций **convert images to text**.

## Шаг 3: Создайте и настройте BatchRecognizer

Теперь переходим к сердцу руководства. Класс `BatchRecognizer` абстрагирует детали многопоточности. Вы можете настроить свойство `Parallelism` в соответствии с количеством ядер процессора или задать собственное значение, если хотите оставить некоторые ядра свободными для других задач.

```csharp
// Step 3: Initialise the BatchRecognizer with optional settings
var ocrBatch = new BatchRecognizer
{
    // Number of concurrent threads (default = Environment.ProcessorCount)
    Parallelism = 4,

    // Optional: Hook into progress events for real‑time feedback
    ProgressChanged = (s, e) =>
        Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
};
```

> **Explanation:** Установка `Parallelism = 4` сообщает библиотеке запускать четыре OCR‑задачи одновременно. На типичном ноутбуке с четырьмя ядрами это даёт хороший прирост скорости без перегрузки системы. Если вы работаете на сервере с множеством ядер, увеличьте это значение.

> **Edge case:** При обработке чрезвычайно больших изображений вы можете столкнуться с ограничениями памяти. В таком случае уменьшите параллелизм или обрабатывайте файлы небольшими порциями.

## Шаг 4: Запустите OCR и получите результаты

Вызов `Recognize` у `BatchRecognizer` возвращает словарь, где ключом является исходный путь к файлу, а значением — `OcrResult`, содержащий извлечённый текст, оценки уверенности и прочее.

```csharp
// Step 4: Execute batch OCR – returns a map of file → OcrResult
IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);
```

> **What you get:** Для каждого изображения `OcrResult.Text` содержит текстовое представление. Это именно то, что вам нужно, когда вы хотите **how to extract text from images** программным способом.

## Шаг 5: Сохраните каждый результат в файл .txt

В большинстве реальных сценариев необходимо сохранять вывод OCR для последующей обработки — возможно, передать его в поисковый индекс или привязать к записи в базе данных. Следующий цикл записывает файл `.txt` рядом с каждым исходным изображением, сохраняя оригинальное имя файла.

```csharp
// Step 5: Write each OCR result to a corresponding .txt file
foreach (var entry in ocrResults)
{
    string txtPath = Path.ChangeExtension(entry.Key, ".txt");
    File.WriteAllText(txtPath, entry.Value.Text);
    Console.WriteLine($"Saved OCR text to {txtPath}");
}
```

> **Tip:** Если вам нужен другой формат (JSON, CSV и т.д.), просто сериализуйте `entry.Value` как вам удобно. Объект `OcrResult` также предоставляет `Confidence` и `PageCount`, если эти метрики полезны.

## Шаг 6: Сигнализируйте о завершении и обрабатывайте ошибки корректно

Чистое завершение делает вашу утилиту более профессиональной. Пример кода уже выводит завершающую строку, но добавим блок try‑catch, чтобы отлавливать любые неожиданные исключения, такие как отсутствие файлов или неподдерживаемые форматы изображений.

```csharp
try
{
    // (All steps 2‑5 go here)
    Console.WriteLine("Batch OCR processing finished successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
}
```

> **Why wrap it:** При запуске программы на большой папке один повреждённый файл может прервать всю задачу. При правильной обработке ошибок вы можете записать проблему в журнал и продолжить обработку остальных файлов.

## Полный готовый к запуску пример

Ниже представлен полный код программы, который вы можете скопировать в `Program.cs`. Убедитесь, что пути к изображениям указывают на реальные файлы на вашем компьютере.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchExample
{
    static void Main()
    {
        try
        {
            // Step 2: Define the image files to be processed
            var imageFiles = new List<string>
            {
                @"C:\Images\invoice1.jpg",
                @"C:\Images\receipt2.png",
                @"C:\Images\scan3.tif"
            };

            // Step 3: Create a BatchRecognizer and configure optional settings
            var ocrBatch = new BatchRecognizer
            {
                // Set the degree of parallelism (default = Environment.ProcessorCount)
                Parallelism = 4,

                // Hook into progress events to monitor processing
                ProgressChanged = (s, e) =>
                    Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
            };

            // Step 4: Run OCR on the batch of images (returns file → OcrResult)
            IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);

            // Step 5: Write each OCR result to a corresponding .txt file
            foreach (var entry in ocrResults)
            {
                string txtPath = Path.ChangeExtension(entry.Key, ".txt");
                File.WriteAllText(txtPath, entry.Value.Text);
                Console.WriteLine($"Saved OCR text to {txtPath}");
            }

            // Step 6: Indicate that batch processing has completed
            Console.WriteLine("Batch OCR processing finished successfully.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
        }
    }
}
```

### Ожидаемый вывод

При запуске `dotnet run` вы увидите примерно следующее:

```
Processed 1/3 – C:\Images\invoice1.jpg
Saved OCR text to C:\Images\invoice1.txt
Processed 2/3 – C:\Images\receipt2.png
Saved OCR text to C:\Images\receipt2.txt
Processed 3/3 – C:\Images\scan3.tif
Saved OCR text to C:\Images\scan3.txt
Batch OCR processing finished successfully.
```

Каждый файл `.txt` теперь содержит текстовую версию соответствующего изображения — именно то, что нужно для масштабного **convert images to text**.

---

## Часто задаваемые вопросы и особые случаи

### Какие форматы изображений поддерживаются?

Aspose.OCR поддерживает JPEG, PNG, TIFF, BMP и GIF «из коробки». Если вы столкнётесь с форматом вроде WebP, сначала конвертируйте его или используйте сторонний декодер.

### Можно ли ограничить язык OCR только английским?

Да. Установите свойство `Language` у `BatchRecognizer` перед вызовом `Recognize`:

```csharp
ocrBatch.Language = "en";
```

Ограничение языка может улучшить точность и скорость, особенно если вас интересует **how to extract text from images** только на одном языке.

### Как обрабатывать тысячи файлов, не переполняя память?

Разбейте список на более мелкие партии (например, по 500 файлов) и запускайте вышеописанную процедуру в цикле. Это делает словарь в памяти управляемым и позволяет вести журнал прогресса по партиям.

### Что если мне нужны результаты OCR в базе данных, а не в файлах?

Замените вызов `File.WriteAllText` на ваш предпочтительный код доступа к данным. Например, используя Dapper:

```csharp
connection.Execute(
    "INSERT INTO OcrResults (FilePath, Text) VALUES (@Path, @Text)",
    new { Path = entry.Key, Text = entry.Value.Text });
```

---

## Заключение

Вы только что освоили **batch OCR processing** в C# с Aspose.OCR, узнали простой способ **convert images to text** и открыли несколько практических советов по эффективному **how to extract text from images**. Весь процесс — сбор путей к файлам, настройка `BatchRecognizer`, запуск OCR и сохранение результатов — помещается в одну простую для чтения программу.

Что дальше? Попробуйте увеличить `Parallelism` на многопроцессорном сервере, поэкспериментируйте с языковыми пакетами или добавьте пост‑обработку, например проверку орфографии. Вы также можете попробовать передавать извлечённый текст в Azure Cognitive Search, чтобы ваши отсканированные документы стали доступными для поиска за секунды.

Есть интересный вариант, которым хотите поделиться — возможно, OCR PDF‑файлов или обработка многостраничных TIFF? Оставьте комментарий ниже, и давайте продолжать обсуждение. Счастливого кодинга!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, опирающиеся на техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Извлечение текста из изображений с помощью операции OCR по папкам](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Как пакетно выполнять OCR изображений со списком в Aspose.OCR для .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Как извлекать текст из ZIP‑архивов с помощью Aspose.OCR для .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}