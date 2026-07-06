---
category: general
date: 2026-05-31
description: How to batch OCR in C# with Aspose OCR. Learn to convert images to text,
  extract text from images, and process multiple files efficiently.
draft: false
keywords:
- how to batch OCR
- convert images to text
- extract text from images
- OCR multiple files
- batch OCR processing
language: ru
og_description: Как пакетно выполнять OCR в C# с помощью Aspose OCR. Преобразуйте
  изображения в текст, извлекайте текст из изображений и легко обрабатывайте OCR нескольких
  файлов.
og_title: Как выполнять пакетное OCR в C# – Полное руководство по программированию
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  headline: How to Batch OCR in C# – Complete Programming Guide
  type: TechArticle
- description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  name: How to Batch OCR in C# – Complete Programming Guide
  steps:
  - name: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
    text: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
  - name: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
    text: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
  - name: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
    text: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- batch-processing
title: Как выполнять пакетное OCR в C# – Полное руководство по программированию
url: /ru/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять пакетное OCR в C# – Полное руководство по программированию

Задумывались ли вы когда‑нибудь **как выполнить пакетное OCR** целой папки отсканированных изображений без ручного открытия каждого файла? Вы не одиноки. Во многих реальных проектах — например, автоматизация обработки счетов или архивирование исторических фотографий — необходимо **конвертировать изображения в текст** массово, а делать это по одному занимает огромное количество времени.

В этом руководстве мы пройдемся по готовому к запуску консольному приложению на C#, которое берёт каждый PNG, JPG или TIFF в исходном каталоге, запускает Aspose OCR для каждого и сохраняет соответствующий файл *.txt* в папку вывода. К концу вы будете уверенно **извлекать текст из изображений**, обрабатывать **OCR нескольких файлов** и иметь надёжную основу для любой **пакетной обработки OCR**, которая может понадобиться позже.

## Что вы узнаете

- Настроить .NET‑проект с пакетом NuGet Aspose OCR.  
- Определить исходные и целевые папки для выполнения **batch OCR**.  
- Перечислить поддерживаемые типы изображений и передать их OCR‑движку.  
- Записать распознанный текст в отдельные файлы *.txt*, эффективно **конвертировать изображения в текст**.  
- Решать распространённые проблемы, такие как отсутствие папок, неподдерживаемые форматы и настройки производительности.  

Предыдущий опыт работы с Aspose не требуется; достаточно базовых знаний C# и Visual Studio, чтобы справиться.

---

![Диаграмма, показывающая поток пакетной обработки OCR от папки изображений к текстовому выводу – как выполнить пакетный OCR](/images/batch-ocr-flow.png){alt="диаграмма процесса пакетного OCR от папки изображений до вывода текста – как выполнить пакетный OCR"}

## Как выполнить пакетный OCR – настройка проекта

Прежде чем погрузиться в код, убедитесь, что у вас есть:

1. **.NET 6 SDK** (или новее) установлен — последняя версия среды выполнения обеспечивает лучшую производительность и нативную поддержку асинхронного ввода‑вывода.  
2. **Visual Studio 2022** (Community Edition подходит) или любой другой редактор по вашему выбору.  
3. Пакет **Aspose.OCR** NuGet. Установите его через консоль диспетчера пакетов:

   ```powershell
   Install-Package Aspose.OCR
   ```

Вот и всё. Остальная часть руководства предполагает, что пакет правильно подключён.

## Шаг 2: Подготовьте исходные и целевые папки (конвертировать изображения в текст)

Сначала нам нужны две папки: одна, содержащая исходные изображения, и другая, куда будут помещаться сгенерированные файлы *.txt*. Приведённый ниже код создаёт целевую папку, если она ещё не существует — никаких ручных действий не требуется.

```csharp
// Define where the images live and where the text files will go
string sourceFolder = @"C:\OCR\Batch";
string outputFolder = @"C:\OCR\BatchTxt";

// Ensure the output directory exists; CreateDirectory is idempotent
Directory.CreateDirectory(outputFolder);
```

> **Почему это важно:** Если пропустить вызов `CreateDirectory`, программа выбросит `DirectoryNotFoundException` в тот момент, когда попытается записать первый текстовый файл. Обработав это заранее, вы делаете процесс пакетного OCR надёжным.

## Шаг 3: Перечислите файлы изображений для OCR нескольких файлов

Далее мы собираем каждый файл, соответствующий поддерживаемым форматам. Использование LINQ делает код лаконичным и при этом читаемым.

```csharp
// Grab all PNG, JPG, and TIFF files from the source folder (non‑recursive)
var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
    .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));
```

> **Подсказка:** Если позже понадобится обрабатывать PDF или BMP, просто расширьте условие `Where`. Хранение фильтра в одном месте упрощает будущие изменения.

## Шаг 4: Запустите OCR‑движок для каждого изображения (как выполнить пакетный OCR)

Теперь суть: передача каждого изображения в Aspose OCR и извлечение распознанного текста. Цикл ниже создаёт новый экземпляр `OcrEngine` для каждого файла — это гарантирует, что память от предыдущего изображения будет освобождена перед обработкой следующего.

```csharp
foreach (var imagePath in imageFiles)
{
    // Initialize the OCR engine with the current image
    OcrEngine ocrEngine = new OcrEngine
    {
        Image = ImageStream.FromFile(imagePath)
    };

    // Perform recognition; Recognize() returns an OcrResult object
    OcrResult ocrResult = ocrEngine.Recognize();

    // Build the output .txt file path (same base name, .txt extension)
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    // Persist the extracted text
    File.WriteAllText(textFilePath, ocrResult.Text);

    Console.WriteLine($"Processed {Path.GetFileName(imagePath)} → {Path.GetFileName(textFilePath)}");
}
```

**Что происходит?**  

- `ImageStream.FromFile` загружает изображение в поток, который может читать Aspose.  
- `ocrEngine.Recognize()` запускает собственно алгоритм OCR, возвращая строку в `ocrResult.Text`.  
- `File.WriteAllText` записывает эту строку на диск, эффективно **извлекая текст из изображений**.  

### Обработка граничных случаев

- **Повреждённые изображения** — оберните вызов распознавания в `try/catch`, запишите ошибку в журнал и продолжите со следующим файлом.  
- **Большие партии** — рассмотрите асинхронную обработку файлов с помощью `Parallel.ForEach`, если у вас многопроцессорная машина.  
- **Разные языки** — установите `ocrEngine.Language = Language.English;` или любой другой поддерживаемый язык перед вызовом `Recognize()`.

## Шаг 5: Сохраните извлечённый текст (извлечь текст из изображений)

Предыдущий фрагмент уже сохраняет результат OCR, но давайте вынесем эту логику в вспомогательный метод. Это делает основной цикл чище и способствует повторному использованию.

```csharp
static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
{
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    File.WriteAllText(textFilePath, recognizedText);
}
```

Затем вы замените встроенный вызов `File.WriteAllText` на:

```csharp
SaveOcrResult(outputFolder, imagePath, ocrResult.Text);
```

> **Почему вынести это в метод?** Это разделяет обязанности — распознавание и сохранение — и даёт вам единое место для добавления пост‑обработки (например, обрезки пробелов или добавления временных меток).

## Полный рабочий пример — пакетная обработка OCR в C#

Собрав все части вместе, представляем автономную программу, которую вы можете скопировать и вставить в новый проект консольного приложения и сразу запустить.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Define source & destination folders
            string sourceFolder = @"C:\OCR\Batch";
            string outputFolder = @"C:\OCR\BatchTxt";

            // 2️⃣ Make sure the output folder exists
            Directory.CreateDirectory(outputFolder);

            // 3️⃣ Get all supported image files (convert images to text)
            var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
                .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));

            // 4️⃣ Process each image (how to batch OCR)
            foreach (var imagePath in imageFiles)
            {
                try
                {
                    // Initialise OCR engine for the current file
                    OcrEngine ocrEngine = new OcrEngine
                    {
                        Image = ImageStream.FromFile(imagePath)
                    };

                    // Run OCR – this extracts text from images
                    OcrResult result = ocrEngine.Recognize();

                    // 5️⃣ Save the result (extract text from images)
                    SaveOcrResult(outputFolder, imagePath, result.Text);

                    Console.WriteLine($"✅ {Path.GetFileName(imagePath)} processed.");
                }
                catch (Exception ex)
                {
                    // Gracefully handle problematic files
                    Console.WriteLine($"⚠️ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }

            Console.WriteLine("🎉 Batch OCR processing complete!");
        }

        // Helper to write the OCR output to a .txt file
        static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
        {
            string textFilePath = Path.Combine(outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, recognizedText);
        }
    }
}
```

### Ожидаемый вывод

При запуске программы консоль выведет строки, похожие на:

```
✅ invoice001.png processed.
✅ receipt123.jpg processed.
✅ map.tif processed.
🎉 Batch OCR processing complete!
```

Тем временем папка `C:\OCR\BatchTxt` будет содержать:

- `invoice001.txt`
- `receipt123.txt`
- `map.txt`

Каждый файл содержит текстовое представление исходного изображения, готовое для индексации, поиска или последующего анализа.

## Профессиональные советы и распространённые подводные камни (пакетная обработка OCR)

- **Управление памятью:** Aspose OCR освобождает буферы изображений после каждого вызова `Recognize()`, но если вы обрабатываете тысячи файлов, рассмотрите редкое вызовы `GC.Collect()` для снижения потребления памяти.  
- **Ускорение:** Используйте `OcrEngine.RecognizeAsync()` в .NET 6+ и запускайте несколько задач с помощью `Task

## Что изучать дальше?

- [Как выполнить пакетный OCR изображений со списком в Aspose.OCR для .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Извлечь текст из изображений с помощью OCR операции над папками](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Как выполнить OCR над архивными изображениями с Aspose.OCR для .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}