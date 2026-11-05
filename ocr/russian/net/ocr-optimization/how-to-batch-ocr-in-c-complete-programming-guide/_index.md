---
category: general
date: 2026-03-13
description: Как быстро и надёжно выполнять пакетное OCR, изучая извлечение текста
  из TIFF‑файлов с помощью Aspose.OCR. Следуйте этому пошаговому руководству.
draft: false
keywords:
- how to batch OCR
- extract text from tiff
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: ru
og_description: Узнайте, как выполнять пакетное OCR в C# и извлекать текст из файлов
  TIFF с помощью Aspose.OCR. Это руководство охватывает настройку, код и рекомендации
  по лучшим практикам.
og_title: Как пакетно выполнять OCR в C# – Полное руководство по программированию
tags:
- OCR
- C#
- Aspose
- Batch processing
title: Как выполнять пакетное OCR в C# – Полное руководство по программированию
url: /ru/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять пакетное OCR в C# – Полное руководство по программированию

Когда‑то задумывались **как выполнять пакетное OCR** огромного количества отсканированных счетов без написания отдельного скрипта для каждого файла? Вы не одиноки. Во многих реальных проектах проблема заключается не в точности OCR, а в огромном объёме изображений — часто TIFF‑файлов, которые нужно превратить в поисковый текст.  

В этом руководстве мы покажем, **как выполнять пакетное OCR** с помощью `BatchProcessor` из Aspose.OCR, а также научим **извлекать текст из tiff**‑файлов за один чистый запуск. К концу вы получите готовое консольное приложение, которое обрабатывает всю папку, использует необязательное ускорение GPU и сохраняет результаты в виде простого текста там, где вам нужно.

## Что понадобится

- **.NET 6+** (или .NET Framework 4.7.2, если предпочитаете классический рантайм)  
- **Aspose.OCR for .NET** — пакет можно установить через NuGet командой `dotnet add package Aspose.OCR`.  
- Папка с изображениями **TIFF**, которые нужно прочитать (в примере используется папка `Invoices`).  
- Необязательно: GPU, поддерживающий DirectX 11 или CUDA, если хотите ускорить процесс.  

Никаких дополнительных сервисов, никаких облачных ключей — только локальный C#‑проект и библиотека Aspose.

## Шаг 1: Создайте проект и установите Aspose.OCR

Сначала создайте консольное приложение.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Если вы работаете в Windows и планируете использовать ускорение GPU, убедитесь, что установлен последний драйвер видеокарты. Иначе флаг `UseGpu = true` автоматически переключится на процессор.

## Шаг 2: Создайте конфигурацию BatchProcessor

Теперь настроим `BatchProcessor`. Это ядро **как выполнять пакетное OCR** — вы указываете Aspose, какой язык ожидать, какие фильтры предобработки применить и использовать ли GPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 2: Configure the batch processor
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                // Primary language – English works for most invoices
                Language = Language.English,

                // Set to true if you have a compatible GPU; otherwise false
                UseGpu = true,

                // Optional pre‑processing to improve OCR accuracy
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),   // straightens tilted scans
                    new DespeckleFilter() // removes speckles and noise
                }
            };
```

**Почему такие настройки?**  
- `Language = Language.English` указывает движку использовать модель английского языка, которая гораздо точнее общей модели.  
- `UseGpu` может сократить время обработки вдвое на хорошей видеокарте, но безопасно оставить `false`, если у вас ноутбук без GPU.  
- Конвейер фильтров имитирует то, что делает человек: выравнивает страницу и удаляет шум перед передачей в OCR‑движок.

## Шаг 3: Укажите папку с вашими TIFF‑файлами

Следующий элемент **как выполнять пакетное OCR** — указать библиотеке, где находятся исходные файлы. Поддерживаются шаблоны, поэтому можно захватить все файлы `.tif` за один проход.

```csharp
            // -------------------------------------------------
            // Step 3: Add the folder containing TIFF images
            // -------------------------------------------------
            // Replace YOUR_DIRECTORY with the actual path on your machine
            batchProcessor.AddFolder(@"C:\Data\Invoices", "*.tif");
```

> **Edge case:** Если в папке смешанные расширения (`.tiff`, `.tif`, `.png`), вызовите `AddFolder` несколько раз или используйте `*.*` и отфильтруйте позже в коде.

## Шаг 4: Выберите место для сохранения результатов OCR

Возможно, вы задаётесь вопросом: «Куда сохраняется извлечённый текст?» Это третий столп **как выполнять пакетное OCR** — определение места и формата вывода. Мы будем сохранять файлы простого текста рядом с оригиналами.

```csharp
            // -------------------------------------------------
            // Step 4: Define output folder and format
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;
```

Если нужен JSON или XML вместо простого текста, просто замените `OutputFormat.PlainText` на `OutputFormat.Json` или `OutputFormat.Xml`. Библиотека выполнит конвертацию за вас.

## Шаг 5: Запустите пакетную задачу и отобразите результаты

Наконец, запускаем задачу. Метод `Execute` блокирует выполнение, пока не обработаются все файлы, после чего можно проверить `ProcessedCount` для подтверждения успеха.

```csharp
            // -------------------------------------------------
            // Step 5: Execute the batch job
            // -------------------------------------------------
            batchProcessor.Execute();

            // Simple verification output
            Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
            Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
        }
    }
}
```

### Ожидаемый вывод

При запуске программы в консоли появится примерно следующее:

```
Batch completed. Processed files: 42
Check C:\Data\Output for .txt files containing extracted text.
```

В папке `Output` вы найдёте по одному файлу `.txt` для каждого исходного TIFF, названному так же, как оригинальное изображение (например, `Invoice_001.txt`). Откройте любой файл — увидите «сырой» OCR‑текст, готовый к индексации поиска или дальнейшему извлечению данных.

## Обработка распространённых проблем

### 1. GPU недоступен

Если `UseGpu = true`, но совместимое устройство не найдено, Aspose тихо переключится на процессор. Чтобы обработать это явно, можно перехватить `DeviceNotFoundException`:

```csharp
try
{
    batchProcessor.Execute();
}
catch (DeviceNotFoundException)
{
    Console.WriteLine("GPU not detected – switching to CPU mode.");
    batchProcessor.UseGpu = false;
    batchProcessor.Execute();
}
```

### 2. Не‑TIFF файлы в той же папке

Когда в папке смешанные типы, отфильтруйте их программно:

```csharp
var tiffFiles = Directory.GetFiles(@"C:\Data\Invoices", "*.*")
                         .Where(f => f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase) ||
                                     f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));

foreach (var file in tiffFiles)
    batchProcessor.AddFile(file);
```

### 3. Большие файлы, превышающие память

Для огромных многопстраничных TIFF‑файлов включите потоковую обработку:

```csharp
batchProcessor.EnableMemoryManagement = true; // reduces RAM footprint
```

## Pro Tips для лучшей точности при **извлечении текста из tiff**

- **Разрешение имеет значение** — стремитесь к 300 dpi и выше. При меньшем разрешении OCR‑движок может пропускать символы.  
- **Цвет vs. градации серого** — преобразуйте цветные сканы в градации серого перед OCR; `DeskewFilter` уже делает это «под капотом», но можно добавить `ColorDepthReductionFilter` для дополнительного ускорения.  
- **Постобработка** — после получения простого текста запустите проверку орфографии или очистку с помощью регулярных выражений, чтобы исправить типичные ошибки OCR (например, «0» vs «O»).

## Полный рабочий пример (готовый к копированию)

Ниже полностью программа, которую можно собрать и запустить. Просто замените шаблонные пути на свои каталоги.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Configure the batch processor (how to batch OCR)
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                Language = Language.English,
                UseGpu = true, // set false if no GPU
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),
                    new DespeckleFilter()
                },
                EnableMemoryManagement = true // helps with huge TIFFs
            };

            // -------------------------------------------------
            // Add source TIFF files
            // -------------------------------------------------
            string sourceFolder = @"C:\Data\Invoices";
            batchProcessor.AddFolder(sourceFolder, "*.tif");

            // -------------------------------------------------
            // Optional: add only TIFFs if folder contains other images
            // -------------------------------------------------
            var extraTiffs = Directory.GetFiles(sourceFolder, "*.*")
                                      .Where(f => f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));
            foreach (var file in extraTiffs)
                batchProcessor.AddFile(file);

            // -------------------------------------------------
            // Define where results go
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;

            // -------------------------------------------------
            // Execute the batch job
            // -------------------------------------------------
            try
            {
                batchProcessor.Execute();
                Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
                Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
            }
            catch (DeviceNotFoundException)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
                batchProcessor.UseGpu = false;
                batchProcessor.Execute();
                Console.WriteLine($"Batch completed (CPU). Processed files: {batchProcessor.ProcessedCount}");
            }
        }
    }
}
```

Скомпилируйте и запустите:

```bash
dotnet run
```

Теперь у вас есть аккуратный набор файлов `.txt` — каждый из них является результатом **извлечения текста из tiff** через полностью автоматизированный пакетный процесс.

## Заключение

Мы прошли весь путь **как выполнять пакетное OCR** в C# от начала до конца, охватив всё, что нужно для эффективного **извлечения текста из tiff** файлов. Ключевые выводы:

1. Используйте `BatchProcessor` из Aspose.OCR, чтобы не писать повторяющиеся циклы.  
2. Применяйте фильтры предобработки (выравнивание, удаление шума) для повышения точности.  
3. Включайте ускорение GPU, когда это возможно, но всегда имейте резервный вариант на CPU.  
4. Сохраняйте результаты в предсказуемой структуре папок, чтобы последующие задачи могли автоматически их использовать.

Дальше вы можете:

- Передавать простой текст в **поисковый индекс** (например, Elasticsearch), делая счета доступными для поиска.  
- Конвертировать вывод в **JSON** и подавать его в модель машинного обучения, извлекающую позиции строк.  
- Добавить **обработку ошибок** для повреждённых TIFF‑файлов или проблем с правами доступа.

Попробуйте сами,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}