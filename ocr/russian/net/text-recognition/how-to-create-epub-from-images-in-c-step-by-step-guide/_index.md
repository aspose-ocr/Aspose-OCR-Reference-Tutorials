---
category: general
date: 2026-03-07
description: Как создать ePub из отсканированных изображений с помощью Aspose OCR
  — узнайте, как преобразовать изображение в ePub, извлечь текст из изображения, добавить
  автора в ePub и загрузить изображение для OCR.
draft: false
keywords:
- how to create epub
- convert image to epub
- extract text from image
- add author to epub
- load image for ocr
language: ru
og_description: Как создать ePub из отсканированных изображений в C#. Этот учебник
  показывает, как преобразовать изображение в ePub, извлечь текст из изображения,
  добавить автора в ePub и загрузить изображение для OCR.
og_title: Как создать ePub из изображений на C# – Полное руководство
tags:
- C#
- Aspose OCR
- ePub
- Document Conversion
title: Как создать ePub из изображений на C# – пошаговое руководство
url: /ru/net/text-recognition/how-to-create-epub-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать ePub из изображений на C# – Полное руководство

Когда‑нибудь задумывались **как создать ePub** из набора отсканированных страниц? Возможно, у вас есть несколько PNG‑файлов классического романа, и вы хотите превратить их в удобный ePub, который можно читать на любом устройстве. Хорошая новость: с помощью Aspose OCR вы можете **загрузить изображение для OCR**, извлечь текст и затем **конвертировать изображение в ePub** всего в несколько строк кода C#.

В этом руководстве мы пройдем весь конвейер: загрузка изображения, извлечение текста, добавление метаданных (да, мы **добавим автора в epub**), и, наконец, запись ePub‑файла, соответствующего стандартам. К концу вы получите готовый к публикации ePub и полное понимание каждого шага, чтобы адаптировать код для многостраничных книг, пользовательских шрифтов или даже DRM‑свободного распространения.

## Что вам понадобится

- **.NET 6** или новее (API также работает с .NET Standard 2.0+)  
- **Aspose.OCR for .NET** – можно скачать бесплатную пробную версию с сайта Aspose.  
- Отсканированное изображение, например `book_page.png`, размещённое где‑нибудь на диске.  
- Любая удобная IDE (Visual Studio, Rider или VS Code – в скриншотах я использую Visual Studio).

Дополнительные пакеты NuGet не требуются; Aspose.OCR уже содержит всё необходимое для экспорта в ePub.

---

![Как создать ePub из отсканированного изображения](/images/how-to-create-epub.png "Как создать ePub из отсканированного изображения с помощью Aspose OCR")

## Шаг 1 – Создание проекта и установка Aspose.OCR

Сначала создайте новое консольное приложение:

```bash
dotnet new console -n OcrToEpubDemo
cd OcrToEpubDemo
```

Установите пакет Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

И всё – библиотека поставляется с поддержкой OCR и экспорта в ePub, так что дополнительных зависимостей не требуется.

## Шаг 2 – Загрузка изображения для OCR

Прежде чем **извлечь текст из изображения**, нужно передать движку OCR файл для чтения. Помощник `ImageStream.FromFile` делает это элементарно:

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Load the PNG (or JPG, TIFF, etc.) you want to process
// This is the “load image for OCR” step.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book_page.png");
```

> **Совет:** Если ваше изображение находится во встроенном ресурсе, используйте `ImageStream.FromResource` вместо `FromFile`.

## Шаг 3 – Извлечение текста из изображения

Теперь движок действительно читает пиксели и преобразует их в строки Unicode. За это отвечает метод `Recognize`.

```csharp
// Run the OCR process – this will fill ocrEngine.RecognitionResult
ocrEngine.Recognize();

// Optional: inspect the raw text
string rawText = ocrEngine.RecognitionResult.Text;
Console.WriteLine("Extracted text (first 200 chars):");
Console.WriteLine(rawText.Substring(0, Math.Min(200, rawText.Length)));
```

Зачем вызывать `Recognize` отдельно? Это позволяет просмотреть необработанный результат OCR, настроить параметры языка или даже выполнить проверку орфографии перед созданием ePub.

## Шаг 4 – Настройка параметров экспорта ePub (Добавление автора в ePub)

Создание качественного ePub – это не просто выгрузка текста; нужны правильные метаданные. Класс `EpubExportOptions` предоставляет удобный способ **добавить автора в ePub**, задать название и решить, включать ли оригинальные изображения.

```csharp
var epubExportOptions = new EpubExportOptions
{
    Title = "Scanned Book",          // Title shown in eReader libraries
    Author = "Unknown",              // This is where we “add author to epub”
    IncludeImages = true             // Embeds the original PNGs for visual fidelity
};
```

Если у вас несколько страниц, вы можете продолжать вызывать `ocrEngine.Image = …` и `ocrEngine.Recognize()` внутри цикла; каждый вызов добавит содержимое новой страницы в тот же документ ePub.

## Шаг 5 – Конвертация изображения в ePub и экспорт

После извлечения текста и настройки метаданных последний шаг – однострочник, который сохраняет ePub‑файл на диск:

```csharp
// Export the recognized content to an ePub file
ocrEngine.ExportToEpub("YOUR_DIRECTORY/book.epub", epubExportOptions);

// Confirmation for the user
Console.WriteLine("ePub created.");
```

Полученный `book.epub` открывается в Calibre, Apple Books или любом совместимом читалке. Поскольку мы задали `IncludeImages = true`, оригинальный PNG будет отображаться как отдельная страница‑картинка, сохраняя внешний вид отсканированного источника.

## Полный рабочий пример

Объединив всё вместе, получаем полностью готовую к запуску программу:

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // This is the “load image for OCR” step.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book_page.png");

        // Step 3: Run the OCR recognition – we now “extract text from image”
        ocrEngine.Recognize();

        // (Optional) Print a snippet of the extracted text
        string snippet = ocrEngine.RecognitionResult.Text.Substring(0,
            Math.Min(200, ocrEngine.RecognitionResult.Text.Length));
        Console.WriteLine("Extracted text preview:");
        Console.WriteLine(snippet);
        Console.WriteLine();

        // Step 4: Set up ePub export options – we “add author to epub” here
        var epubExportOptions = new EpubExportOptions
        {
            Title = "Scanned Book",
            Author = "Unknown",
            IncludeImages = true   // embed the original images in the ePub
        };

        // Step 5: Export the recognized content – this is how we “convert image to epub”
        ocrEngine.ExportToEpub("YOUR_DIRECTORY/book.epub", epubExportOptions);

        // Step 6: Inform the user that the ePub has been created
        Console.WriteLine("ePub created.");
    }
}
```

### Ожидаемый вывод

```
Extracted text preview:
Chapter 1
It was a bright cold day in April, and the...
 
ePub created.
```

Откройте `book.epub` в любимом читалке, и вы увидите титульную страницу, строку автора (даже если она будет «Unknown») и отсканированное изображение рядом с выделяемым текстом.

## Часто задаваемые вопросы и особые случаи

### Что делать, если язык OCR не английский?

Aspose.OCR поддерживает более 70 языков. Просто задайте свойство `Language` перед вызовом `Recognize`:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

### Как обрабатывать многостраничные книги?

Оберните логику загрузки/распознавания в цикл `foreach`:

```csharp
string[] pages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
foreach (var pagePath in pages)
{
    ocrEngine.Image = ImageStream.FromFile(pagePath);
    ocrEngine.Recognize();
}
ocrEngine.ExportToEpub("YOUR_DIRECTORY/full_book.epub", epubExportOptions);
```

Каждая итерация добавляет вновь распознанный текст в тот же ePub, сохраняя порядок страниц.

### Можно ли исключить оригинальные изображения?

Конечно – установите `IncludeImages = false` в `EpubExportOptions`. Полученный ePub будет состоять только из текcта, что значительно уменьшит размер файла.

### Что насчёт пользовательских шрифтов или стилей?

Экспортер ePub от Aspose.OCR позволяет задать CSS‑стили через свойство `Css` в `EpubExportOptions`. Так можно задать конкретный шрифт, межстрочный интервал или отступы.

## Заключение

Теперь вы знаете **как создать ePub** из отсканированного изображения с помощью Aspose OCR на C#. В руководстве рассмотрены все этапы: **загрузка изображения для OCR**, **извлечение текста из изображения**, **добавление автора в epub** и, наконец, **конвертация изображения в epub** одной вызванной функцией экспорта. Имея полный пример кода, вы сможете расширить решение для пакетной обработки целых библиотек, добавления пользовательской обложки или интеграции рабочего процесса в веб‑API.

Готовы к следующему вызову? Попробуйте конвертировать PDF в ePub или поэкспериментировать с порогами уверенности OCR, чтобы улучшить точность на шумных сканах. Возможности безграничны, когда объединяете мощный OCR с гибкой генерацией ePub.

Счастливого кодинга и приятного чтения вашего только‑что созданного ePub!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}