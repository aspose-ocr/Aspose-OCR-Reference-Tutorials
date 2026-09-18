---
category: general
date: 2026-01-10
description: Извлечение текста из изображения с помощью Aspose OCR в C#. Узнайте,
  как конвертировать текст отсканированного документа с пакетной обработкой и сохранять
  результаты.
draft: false
keywords:
- extract text from image
- convert scanned document text
- batch OCR processing
- Aspose OCR
- C# OCR tutorial
language: ru
og_description: Извлекать текст из изображения с помощью Aspose OCR в C#. Этот учебник
  показывает, как преобразовать текст отсканированного документа с использованием
  пакетной обработки.
og_title: Извлечение текста из изображения в C# – Полное руководство по Aspose OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Извлечение текста из изображения в C# – Полное руководство по Aspose OCR
url: /ru/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения – Полное руководство по Aspose OCR

Когда‑то вам нужно было **извлечь текст из изображения**, но вы не знали, с чего начать? Вы не одиноки; многие разработчики сталкиваются с этой проблемой при работе со сканированными PDF, многостраничными TIFF или фотографиями чеков. Хорошая новость в том, что с Aspose OCR вы можете **преобразовать текст сканированного документа** всего в несколько строк кода на C#.

В этом руководстве мы пройдем реальный сценарий: возьмём многостраничный TIFF, запустим пакетный OCR для каждой страницы и запишем один текстовый файл, содержащий содержимое всех страниц. К концу вы получите готовое консольное приложение, поймёте, почему каждый шаг важен, и узнаете, как адаптировать процесс для особых случаев, таких как защищённые паролем изображения или пользовательские языковые пакеты.

## Требования

- .NET 6.0 SDK или новее (код работает также с .NET Core и .NET Framework)  
- Visual Studio 2022 (или любой другой редактор)  
- Файл лицензии Aspose OCR (или используйте бесплатный режим оценки)  
- Многостраничный файл изображения (например, `multipage.tif`), размещённый в папке, к которой вы можете обратиться  

Дополнительные пакеты NuGet не требуются, кроме `Aspose.OCR`; мы установим его в первом шаге.

## Шаг 1 – Установить Aspose OCR и создать проект

Для начала создайте новый консольный проект и подключите библиотеку Aspose OCR.

```bash
dotnet new console -n ImageTextExtractor
cd ImageTextExtractor
dotnet add package Aspose.OCR
```

> **Pro tip:** Если у вас есть файл лицензии (`Aspose.OCR.lic`), скопируйте его в корень проекта. Библиотека автоматически подхватит его во время выполнения.

Зачем этот шаг? Установка пакета даёт доступ к `BatchProcessor`, `OcrEngine` и другим удобным классам, которые скрывают низкоуровневую работу с изображениями. Кроме того, вы получаете самые свежие OCR‑алгоритмы, которые поставляются с Aspose.

## Шаг 2 – Загрузить многостраничное изображение с помощью BatchProcessor

`BatchProcessor` создан именно для такого сценария: перебора каждой страницы многостраничного изображения без необходимости вручную разделять файлы.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System.Text;

// Step 2: Initialize the batch processor with the path to your TIFF
var batchProcessor = new BatchProcessor(@"YOUR_DIRECTORY\multipage.tif");

// Verify that pages were loaded
if (batchProcessor.Pages.Count == 0)
{
    Console.WriteLine("No pages found – double‑check the file path.");
    return;
}
```

`BatchProcessor` читает все страницы в память, предоставляя их через `batchProcessor.Pages`. Каждый объект страницы знает свой номер (`ocrPage.Number`), который мы позже используем для чётких заголовков.

## Шаг 3 – Подготовить StringBuilder для накопления результатов

Нужен один текстовый файл, содержащий вывод OCR всех страниц, разделённый заголовками. `StringBuilder` – самый эффективный способ конкатенировать строки в цикле.

```csharp
// Step 3: Create a StringBuilder to collect OCR results
var extractedText = new StringBuilder();
```

Почему именно `StringBuilder`? Конкатенация строк с помощью `+` внутри цикла создаёт новый объект строки на каждой итерации, что ухудшает производительность, особенно при работе с большими документами.

## Шаг 4 – Перебрать каждую страницу, выполнить OCR и добавить результаты

Теперь основной блок руководства: проход по каждой странице, распознавание текста и сохранение его с маркером страницы.

```csharp
// Step 4: Process each page individually
foreach (var ocrPage in batchProcessor.Pages)
{
    // Create a fresh OcrEngine for every page – this isolates settings
    var ocrEngine = new OcrEngine
    {
        Image = ocrPage
    };

    // Perform recognition
    ocrEngine.Recognize();

    // Append a clear header and the recognized text
    extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
    extractedText.AppendLine(ocrEngine.Text);
}
```

**Почему новый `OcrEngine` для каждой страницы?** Некоторые разработчики переиспользуют один движок, меняя его свойство `Image`, но это может сохранять настройки языка или предыдущие результаты, вызывая скрытые ошибки. Создание нового экземпляра гарантирует чистый старт.

### Обработка распространённых граничных случаев

- **Пустые страницы:** Если на странице нет распознаваемого текста, `ocrEngine.Text` будет пустой строкой. Можно вставить заполнитель, например “(Текст не обнаружен)”.
- **Выбор языка:** По умолчанию Aspose OCR использует английский. Чтобы обработать немецкий или французский, установите `ocrEngine.Language = Language.German;` перед вызовом `Recognize()`.
- **Совет по производительности:** Для огромных TIFF можно включить `ocrEngine.UseParallelProcessing = true;`, чтобы задействовать несколько ядер процессора.

## Шаг 5 – Записать объединённый вывод в текстовый файл

Наконец, сохраняем накопленную строку на диск.

```csharp
// Step 5: Save the result to a .txt file
string outputPath = @"YOUR_DIRECTORY\multipage_result.txt";
File.WriteAllText(outputPath, extractedText.ToString());

Console.WriteLine($"OCR complete! Results saved to {outputPath}");
```

Полученный файл `multipage_result.txt` будет выглядеть примерно так:

```
--- Page 1 ---
This is the first page of the scanned document.
It contains a title and some introductory text.

--- Page 2 ---
Continuation of the report.
Data tables and figures follow.
```

Теперь вы **извлекли текст из изображения** и эффективно **преобразовали текст сканированного документа** в поисковый, редактируемый формат.

## Бонус – Визуальный обзор (альтернативный текст изображения)

Ниже простая блок‑схема, иллюстрирующая процесс.  
*Alt text:* “Диаграмма, показывающая, как извлечь текст из изображения с помощью пакетной обработки Aspose OCR в C#”.

![Диаграмма потока OCR](placeholder-image-url.png)

*(Если вы публикуете это руководство на статическом сайте, замените заглушку реальным SVG или PNG.)*

## Часто задаваемые вопросы

**Работает ли это с PDF‑файлами?**  
Да, Aspose OCR может читать страницы PDF как изображения. Нужно сначала преобразовать PDF в изображения или использовать `PdfDocument` из `Aspose.PDF` и передать растровое изображение каждой страницы в `OcrEngine`.

**Что делать, если мой TIFF защищён паролем?**  
`BatchProcessor` не обрабатывает шифрование напрямую. Расшифруйте файл с помощью библиотеки, например `Aspose.Imaging`, перед передачей его в OCR‑конвейер.

**Можно ли выводить JSON вместо обычного текста?**  
Конечно. Замените логику `StringBuilder` на сериализатор JSON (например, `System.Text.Json`) и храните текст каждой страницы под ключом `pageNumber`.

## Полный рабочий пример

Ниже полная программа, которую можно скопировать в `Program.cs`. Включены все директивы `using`, обработка ошибок и комментарии.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Text;

namespace ImageTextExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            string inputImagePath = @"YOUR_DIRECTORY\multipage.tif";
            string outputTextPath = @"YOUR_DIRECTORY\multipage_result.txt";

            // 1️⃣ Load the multi‑page image
            var batchProcessor = new BatchProcessor(inputImagePath);
            if (batchProcessor.Pages.Count == 0)
            {
                Console.WriteLine("No pages detected – verify the file path.");
                return;
            }

            // 2️⃣ Prepare a StringBuilder for the final output
            var extractedText = new StringBuilder();

            // 3️⃣ Process each page
            foreach (var ocrPage in batchProcessor.Pages)
            {
                var ocrEngine = new OcrEngine
                {
                    Image = ocrPage,
                    // Uncomment to change language:
                    // Language = Language.German,
                    // UseParallelProcessing = true
                };

                // Run OCR
                ocrEngine.Recognize();

                // Append header and text
                extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
                // Guard against empty results
                string pageText = string.IsNullOrWhiteSpace(ocrEngine.Text)
                    ? "(No text detected on this page)"
                    : ocrEngine.Text;
                extractedText.AppendLine(pageText);
            }

            // 4️⃣ Write to file
            File.WriteAllText(outputTextPath, extractedText.ToString());

            Console.WriteLine($"✅ Extraction complete. File saved at: {outputTextPath}");
        }
    }
}
```

Запустите программу командой:

```bash
dotnet run
```

Вы увидите сообщение в консоли, подтверждающее успешное выполнение, а выходной файл будет содержать объединённые результаты OCR.

## Заключение

Мы продемонстрировали практический способ **извлечения текста из изображения** с помощью Aspose OCR, превращая любой многостраничный скан в обычный, поисковый текст. Используя `BatchProcessor` и чистую настройку `OcrEngine` для каждой страницы, вы надёжно **преобразуете текст сканированного документа**, сохраняя код простым и поддерживаемым.

Экспериментируйте: пробуйте разные языки, переключайтесь на вывод JSON или интегрируйте эту логику в веб‑API, обрабатывающий загрузки «на лету». Основной шаблон остаётся тем же — загрузить, распознать, накопить и сохранить.

Есть вопросы по OCR, лицензированию Aspose или работе с большими пакетами документов? Оставляйте комментарий ниже или изучайте официальную документацию Aspose для более глубокого погружения. Приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}