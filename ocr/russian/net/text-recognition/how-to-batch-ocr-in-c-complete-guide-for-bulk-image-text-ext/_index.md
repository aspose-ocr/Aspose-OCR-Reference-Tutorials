---
category: general
date: 2026-04-04
description: Как выполнять пакетное OCR с Aspose.OCR в C#. Узнайте, как извлекать
  текст из изображений, экспортировать сводки в CSV и эффективно обрабатывать массовое
  OCR изображений.
draft: false
keywords:
- how to batch ocr
- extract text images
- how to export csv
- bulk image ocr
- batch ocr images
language: ru
og_description: Как выполнять пакетное OCR в C# с Aspose.OCR. Получите полное решение
  для извлечения текста из изображений и экспорта сводок в CSV.
og_title: Как выполнять пакетное OCR в C# – Полное пошаговое руководство
tags:
- OCR
- C#
- Aspose
- Automation
title: Как выполнять пакетное OCR в C# — Полное руководство по массовому извлечению
  текста из изображений
url: /ru/net/text-recognition/how-to-batch-ocr-in-c-complete-guide-for-bulk-image-text-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять пакетный OCR – Полнофункциональное руководство на C#

Вы когда‑нибудь задумывались **как выполнять пакетный OCR** для целой папки изображений без написания отдельной процедуры для каждого файла? Вы не одиноки. Во многих реальных проектах — например, обработка счетов, архивирование отсканированных книг или массовое оцифрование чеков — разработчикам нужен быстрый и надёжный способ извлекать текст из десятков и даже тысяч изображений.  

В этом руководстве мы пройдём через полностью готовый к запуску пример, показывающий **как выполнять пакетный OCR**, **извлекать текст из изображений** и **экспортировать сводку в CSV** с помощью Aspose.OCR. К концу вы получите одну программу на C#, способную принимать любую директорию с изображениями, преобразовывать их в поисковые текстовые файлы и выдавать аккуратный CSV‑отчёт о выполненной операции. Никаких загадок, только понятный код и практические советы.

## Что вы узнаете

- Настроить движок Aspose.OCR для английского (или любого поддерживаемого языка).  
- Обработать всю папку изображений за один проход — идеально для массового OCR.  
- Сохранить каждый результат OCR в файл `.txt`, при желании генерируя CSV‑файл, в котором перечислены имена исходных изображений и длина извлечённого текста.  
- Обработать типичные граничные случаи, такие как неподдерживаемые типы файлов, пустые папки и символы Unicode.  

**Prerequisites** – Вам нужен .NET 6+ (или .NET Framework 4.7.2+), Visual Studio 2022 или любой другой предпочитаемый IDE, а также действующая лицензия Aspose.OCR (бесплатная пробная версия подходит для демонстраций). Другие сторонние библиотеки не требуются.

![how to batch ocr diagram](https://example.com/ocr-flow.png "how to batch ocr flow diagram")

## Шаг 1: Установить Aspose.OCR и создать новый консольный проект

Чтобы начать, добавьте пакет Aspose.OCR из NuGet в ваш проект:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Если вы используете Visual Studio, вы также можете щёлкнуть правой кнопкой мыши по проекту → *Manage NuGet Packages* → поискать *Aspose.OCR* → установить.

Создайте новый консольный проект (`dotnet new console -n BulkOcrDemo`) и откройте `Program.cs`. Это будет место для всего нашего кода.

## Шаг 2: Инициализировать OCR‑движок – выбрать правильный язык

OCR‑движку необходимо знать, какой язык искать. Английский — самый распространённый, но вы можете заменить его на испанский, французский и т.д., изменив `Language.English`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

// Step 2: Set up the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // You can switch to Language.Spanish, Language.French, etc.
    Language = Language.English
};
```

**Why this matters:** Указание языка повышает точность, поскольку движок может применять словари и наборы символов, специфичные для языка. Если пропустить этот шаг, вы получите общую модель, которая может неправильно интерпретировать символы.

## Шаг 3: Определить пути к источнику, выводу и опциональному CSV

Нужны три папки:

| Путь | Назначение |
|------|------------|
| `sourceFolder` | Где находятся оригинальные изображения. |
| `outputFolder` | Где будет сохраняться каждый результат OCR (`.txt`). |
| `csvSummaryPath` | (Опционально) CSV‑файл, в котором фиксируются имена изображений и длина извлечённого текста. |

```csharp
// Step 3: Folder locations – update these to match your environment
string sourceFolder = @"C:\OcrDemo\Images\Bulk";
string outputFolder = @"C:\OcrDemo\Output\BulkResults";
string csvSummaryPath = Path.Combine(outputFolder, "summary.csv"); // optional
```

> **Tip:** Используйте `Path.Combine` для кросс‑платформенной совместимости; он автоматически вставляет правильный разделитель каталогов.

## Шаг 4: Запустить пакетный процессор

Aspose.OCR поставляется с удобным `BatchProcessor`, который делает всю тяжёлую работу. Он перебирает каждое поддерживаемое изображение (`.png`, `.jpg`, `.tif` и т.д.), запускает OCR и записывает результат.

```csharp
// Step 4: Process the entire folder
BatchProcessor.ProcessFolder(
    sourceFolder: sourceFolder,
    outputFolder: outputFolder,
    engine: ocrEngine,
    csvSummaryPath: csvSummaryPath);
```

### Что происходит «за кулисами»?

1. **File discovery** – Процессор сканирует `sourceFolder` в поиске файлов‑изображений.  
2. **OCR execution** – Каждое изображение передаётся в `ocrEngine`.  
3. **Text saving** – Распознанный текст записывается в файл `.txt` с тем же базовым именем в `outputFolder`.  
4. **CSV logging** – Если указан `csvSummaryPath`, процессор добавляет строку: `ImageName,CharactersExtracted,ProcessingTimeMs`.  

## Шаг 5: Добавить обработку ошибок и поддержку граничных случаев

Надёжный пакетный процесс должен выдерживать отсутствие файлов, неподдерживаемые форматы и пустые каталоги. Оберните вызов обработки в блок `try/catch` и предварительно проверьте входные данные.

```csharp
try
{
    // Validate folders
    if (!Directory.Exists(sourceFolder))
        throw new DirectoryNotFoundException($"Source folder not found: {sourceFolder}");

    Directory.CreateDirectory(outputFolder); // ensures output exists

    // Optional: clean previous CSV
    if (File.Exists(csvSummaryPath))
        File.Delete(csvSummaryPath);

    // Run the batch
    BatchProcessor.ProcessFolder(
        sourceFolder: sourceFolder,
        outputFolder: outputFolder,
        engine: ocrEngine,
        csvSummaryPath: csvSummaryPath);

    Console.WriteLine("✅ Batch OCR completed successfully!");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ An error occurred: {ex.Message}");
}
```

**Why add this?** Без валидации программа может молча завершиться с ошибкой, оставив пустую папку вывода без объяснения причин. Явные сообщения упрощают отладку.

## Шаг 6: Проверить результаты – чего ожидать

После завершения выполнения откройте `outputFolder`. Вы должны увидеть файл `.txt` для каждого изображения:

```
C:\OcrDemo\Output\BulkResults\invoice_001.txt
C:\OcrDemo\Output\BulkResults\receipt_2023-03-15.txt
...
```

Каждый файл содержит «сырой» вывод OCR — обычный текст, который можно передать в поисковые индексы, базы данных или дальнейшие NLP‑конвейеры.

Если вы указали `csvSummaryPath`, откройте `summary.csv`. Он будет выглядеть примерно так:

```
ImageName,CharactersExtracted,ProcessingTimeMs
invoice_001.png,1245,312
receipt_2023-03-15.jpg,378,98
...
```

CSV‑файл упрощает создание отчётов, обнаружение необычно коротких результатов (возможные ошибки сканирования) и передачу метрик в системы мониторинга.

## Шаг 7: Расширить решение – типичные варианты

### 7.1 Изменить формат вывода

Вместо простого `.txt` вы можете захотеть PDF или JSON. `BatchProcessor` позволяет задать пользовательский обратный вызов:

```csharp
BatchProcessor.ProcessFolder(
    sourceFolder,
    outputFolder,
    ocrEngine,
    csvSummaryPath,
    (imagePath, ocrResult) =>
    {
        // Example: save as JSON
        var json = System.Text.Json.JsonSerializer.Serialize(new { Text = ocrResult.Text });
        string jsonPath = Path.ChangeExtension(Path.Combine(outputFolder,
                              Path.GetFileNameWithoutExtension(imagePath)), ".json");
        File.WriteAllText(jsonPath, json);
    });
```

### 7.2 Обрабатывать несколько языков

Если ваша папка содержит документы на разных языках, можно определять язык для каждого изображения или выполнять два прохода:

```csharp
ocrEngine.Language = Language.Spanish; // first pass
BatchProcessor.ProcessFolder(...);
ocrEngine.Language = Language.English; // second pass
BatchProcessor.ProcessFolder(...);
```

### 7.3 Корректно пропускать повреждённые файлы

Добавьте фильтр внутри цикла (или используйте перегрузку, принимающую предикат), чтобы игнорировать файлы, вызывающие исключения:

```csharp
BatchProcessor.ProcessFolder(
    sourceFolder,
    outputFolder,
    ocrEngine,
    csvSummaryPath,
    filter: path => !Path.GetFileName(path).StartsWith("ignore_"));
```

## Полный рабочий пример

Ниже представлен полностью готовый `Program.cs`, который можно скопировать и вставить в новый консольный проект. Замените пути к папкам на свои.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BulkOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine – set language to English
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Define folders – adjust these for your environment
            string sourceFolder = @"C:\OcrDemo\Images\Bulk";
            string outputFolder = @"C:\OcrDemo\Output\BulkResults";
            string csvSummaryPath = Path.Combine(outputFolder, "summary.csv"); // optional

            try
            {
                // 3️⃣ Validate folders
                if (!Directory.Exists(sourceFolder))
                    throw new DirectoryNotFoundException($"Source folder not found: {sourceFolder}");

                Directory.CreateDirectory(outputFolder); // creates if missing

                // 4️⃣ Clean previous CSV (optional)
                if (File.Exists(csvSummaryPath))
                    File.Delete(csvSummaryPath);

                // 5️⃣ Run the batch OCR
                BatchProcessor.ProcessFolder(
                    sourceFolder: sourceFolder,
                    outputFolder: outputFolder,
                    engine: ocrEngine,
                    csvSummaryPath: csvSummaryPath);

                Console.WriteLine("✅ Batch OCR completed successfully!");
                Console.WriteLine($"📂 Text files are in: {outputFolder}");
                Console.WriteLine($"📄 CSV summary (if requested) at: {csvSummaryPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ An error occurred during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### Ожидаемый вывод в консоль

```
✅ Batch OCR completed successfully!
📂 Text files are in: C:\OcrDemo\Output\BulkResults
📄 CSV summary (if requested) at: C:\OcrDemo\Output\BulkResults\summary.csv
```

Откройте один из сгенерированных файлов `.txt`, и вы увидите извлечённый текст, готовый к дальнейшей обработке.

## Часто задаваемые вопросы

**Does this work with PDF inputs?**  
Aspose.OCR can handle PDF pages if you first convert them to images (e.g., using Aspose.PDF). The batch processor itself only looks for raster image formats.

**What if I need to process 10,000 images?**  
The built‑in `BatchProcessor` streams each file one at a time, so memory usage stays low. For massive workloads you might parallel‑process sub‑folders, but remember that OCR is CPU‑intensive—watch your machine’s core count.

**Can I change the OCR accuracy settings?**  
Yes. `ocrEngine` exposes properties like `Resolution` and `PreprocessOptions`. Tweaking them can improve results on low‑quality scans, at the cost of speed.

**How do I license Aspose.OCR for production?**  
Place your license file (`Aspose.OCR.lic`) in the executable directory and load it at startup:

```csharp
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

## Заключение

Теперь у вас есть **полное, готовое к продакшну решение для того, как выполнять пакетный OCR** с использованием C#. В руководстве рассмотрено всё: от установки Aspose.OCR, инициализации движка, обработки всей папки, экспорта CSV‑сводки

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}