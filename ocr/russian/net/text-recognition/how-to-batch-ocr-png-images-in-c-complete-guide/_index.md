---
category: general
date: 2026-04-26
description: Как быстро выполнять пакетное OCR PNG‑изображений. Узнайте, как извлекать
  текст из PNG, конвертировать изображения в текст, записывать распознанный текст
  и читать каталог PNG с помощью Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: ru
og_description: Как пакетно выполнять OCR PNG‑изображений в C# с помощью Aspose OCR.
  Это руководство показывает, как извлекать текст из PNG, преобразовывать изображения
  в текст и эффективно записывать распознанный текст.
og_title: Как пакетно выполнять OCR PNG‑изображений в C# – пошагово
tags:
- OCR
- C#
- Aspose
title: Как пакетно выполнять OCR PNG‑изображений в C# — Полное руководство
url: /ru/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как пакетно выполнять OCR PNG‑изображений в C# – Полное руководство

Когда‑нибудь задумывались **как пакетно выполнять OCR** целой папки PNG‑файлов без написания отдельной программы для каждого изображения? Вы не одиноки, обрабатываете десятки скриншотов, отсканированных чеков или графики, которые нужно превратить в поисковый текст. В этом руководстве мы пошагово реализуем решение, которое **извлекает текст из PNG**, **преобразует изображения в текст** и **записывает распознанный текст** в отдельные файлы — всё это автоматически, читая директорию PNG.

К концу этого руководства у вас будет готовое консольное приложение C#, которое обрабатывает любое количество изображений за один запуск. Никаких дополнительных скриптов, никаких ручных копирований — только чистый код, который делает всю тяжёлую работу за вас.

## Что понадобится

- **.NET 6.0** или новее (код также работает на .NET Framework).  
- NuGet‑пакет **Aspose.OCR for .NET** (бесплатная trial‑версия подходит для тестов).  
- Папка с несколькими файлами *.png*, которые нужно распознать.  
- Visual Studio 2022 или любая другая IDE для C#.

Если всё это есть — можно сразу переходить к реализации.

## Шаг 1 – Подготовьте входную и выходную папки *(Read PNG Directory)*

Сначала указываем программе, где находятся изображения, и решаем, куда сохранять полученные *.txt*‑файлы. `Directory.GetFiles` возвращает удобный перечислимый список всех PNG‑файлов в директории.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Почему это важно:**  
- Шаблон `*.png` гарантирует, что будут обработаны только изображения, а посторонние документы игнорируются.  
- Автоматическое создание выходной папки избавляет от `DirectoryNotFoundException` позже.

> **Pro tip:** Если нужно поддержать другие форматы (JPEG, BMP), просто расширьте шаблон поиска или вызовите `Directory.EnumerateFiles` с несколькими расширениями.

## Шаг 2 – Инициализируйте OCR‑движок *(Convert Images to Text)*

Aspose.OCR поставляется с двумя типами движков: CPU‑ориентированным `OcrEngine` и GPU‑ускоренным `GpuOcrEngine`. Для большинства пакетных задач CPU‑движок более чем достаточен, но при наличии мощного GPU можно переключиться, заменив имя класса.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Почему это важно:**  
- Указание языка существенно повышает точность, потому что движок знает, какой набор символов ожидать.  
- Переход на `GpuOcrEngine` — это однострочное изменение, если вы сталкиваетесь с узкими местами при больших партиях.

## Шаг 3 – Создайте Batch Recogniser

Aspose предоставляет удобный `BatchRecognizer`, который принимает перечисление путей к файлам и последовательно отдает результаты. Это избавляет от необходимости загружать все изображения в память сразу — важный момент для больших папок.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Почему это важно:**  
- Пакетный распознаватель инкапсулирует логику цикла, позволяя сосредоточиться на том, что делать с каждым результатом, а не как безопасно итерировать.

## Шаг 4 – Выполните OCR для всех изображений и запишите результат *(Write Recognized Text)*

Теперь действительно запускаем OCR. Метод `Recognize` возвращает `IEnumerable<RecognitionResult>`, где каждый результат содержит извлечённый текст и другую метаинформацию.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Почему это важно:**  
- `File.WriteAllText` сохраняет текст в кодировке UTF‑8 по умолчанию, сохраняя специальные символы.  
- Инкрементальное именование (`out_0.txt`, `out_1.txt`) соответствует порядку обработки, что удобно для отладки.

> **Edge case:** Если какое‑то изображение не удалось распознать (например, файл повреждён), `RecognitionResult.Text` будет пустым. Можно добавить простую проверку внутри цикла и логировать такие случаи:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Шаг 5 – Соберите всё вместе – Полный рабочий пример

Ниже полностью готовая программа, которую можно скопировать в новый консольный проект. В ней присутствуют директивы `using`, проверка папок и небольшая консольная UI, чтобы знать, когда пакет завершён.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Ожидаемый вывод:**  
При запуске программа выводит примерно следующее:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

И вы увидите файлы `out_0.txt` … `out_11.txt` в выходной папке, каждый из которых содержит текстовую версию соответствующего изображения.

## Часто задаваемые вопросы и советы

| Question | Answer |
|----------|--------|
| *Can I OCR sub‑folders as well?* | Yes—replace `Directory.GetFiles` with `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`. |
| *What if I need a different language?* | Set `ocrEngine.Language = Language.Spanish;` (or any supported enum). |
| *How do I handle huge batches (thousands of files)?* | Consider processing in chunks or using `Parallel.ForEach` with a throttled degree of parallelism to avoid exhausting memory. |
| *Is the output always UTF‑8?* | `File.WriteAllText` defaults to UTF‑8 without BOM, which works for most Latin‑based languages. For Asian scripts you may need to set `Encoding.UTF8` explicitly. |
| *Can I get confidence scores?* | `RecognitionResult` exposes `Confidence`—you can log it alongside the text for quality control. |

## Визуальный обзор *(How to Batch OCR – Diagram)*

![Как выглядит процесс пакетного OCR: входная папка → OCR‑движок → batch recogniser → выходные txt‑файлы](https://example.com/diagram-how-to-batch-ocr.png "Как выглядит процесс пакетного OCR")

*Текст alt содержит основной ключевой запрос, удовлетворяя SEO‑требования к изображению.*

## Итоги

Мы только что рассмотрели **как пакетно выполнять OCR** директории PNG‑файлов с помощью Aspose.OCR, от чтения папки до записи каждого распознанного текста в отдельный файл. Решение полностью автономно, работает на любой современной .NET‑платформе и может быть расширено для GPU‑ускорения, поддержки нескольких языков или параллельной обработки.

Готовы к следующему шагу? Попробуйте заменить `Language.Latin` на другой язык или интегрировать вывод в поисковый индекс, чтобы ваши документы стали мгновенно доступными для поиска. Возможности безграничны, как только вы освоите пакетный OCR.

Удачной разработки, и пишите в комментариях, если возникнут сложности!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}