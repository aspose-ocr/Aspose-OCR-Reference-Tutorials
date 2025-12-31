---
category: general
date: 2025-12-30
description: Создайте поисковый PDF из изображения на C# — узнайте, как конвертировать
  TIFF в PDF, извлекать текст из изображения и автоматизировать создание PDF.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- convert tiff to pdf
- extract text from image
- how to create pdf
language: ru
og_description: Создайте PDF с возможностью поиска из изображения с помощью Aspose
  OCR на C#. Это руководство показывает, как преобразовать TIFF в PDF, извлечь текст
  и обеспечить соответствие PDF/A‑1b.
og_title: Создание поискового PDF из TIFF – пошаговое руководство на C#
tags:
- Aspose OCR
- C#
- PDF generation
title: Создание PDF с возможностью поиска из TIFF – Полное руководство по C#
url: /ru/net/text-recognition/create-searchable-pdf-from-tiff-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из TIFF – Полное руководство на C#  

Когда‑нибудь вам нужно было **создать поисковый PDF** из отсканированного TIFF, но вы не знали, с чего начать? Вы не одиноки. Многие разработчики сталкиваются с этой проблемой, когда им нужны поисковые PDF для архивирования или соответствия требованиям, и хорошая новость в том, что решение удивительно простое с Aspose OCR.  

В этом руководстве мы пройдем процесс преобразования изображения в PDF, извлечения текста из изображения и доработки результата, чтобы он соответствовал стандарту PDF/A‑1b. К концу вы сможете **convert tiff to pdf**, **extract text from image**, и точно знать **how to create pdf** файлы, которые одновременно являются поисковыми и готовыми к архивированию.  

## Что понадобится  

- .NET 6 (или любую актуальную версию .NET) — код работает как на .NET Core, так и на .NET Framework.  
- Пакет NuGet Aspose.OCR — установите его с помощью `dotnet add package Aspose.OCR`.  
- Пример файла TIFF (`input.tif`), который вы хотите превратить в поисковый PDF.  
- Среда разработки (Visual Studio, VS Code, Rider… подойдёт любая).  

Это всё. Никаких дополнительных SDK, внешних сервисов и скрытых шагов настройки.  

![Create searchable PDF example](image-placeholder.png "Create searchable PDF preview")  

## Шаг 1 – Инициализация OCR‑движка и загрузка английской модели  

Прежде чем мы сможем превратить изображение в поисковый текст, OCR‑движку необходимо знать, какой язык искать. Aspose OCR поставляется с языковыми пакетами, которые можно загружать по требованию.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Load the English language model (you can swap this for other languages)
ocrEngine.LoadLanguage(LanguageModel.English);
```  

**Почему это важно:** Загрузка правильной языковой модели значительно повышает точность распознавания. Если пропустить этот шаг, движок переходит к общей модели, что часто приводит к искажённому тексту — особенно в TIFF с низким разрешением.  

## Шаг 2 – Распознавание текста из исходного изображения (необязательно, но полезно)  

Выполнение OCR возвращает объект `OcrResult`, который вы можете исследовать, записать в журнал или даже сохранить как обычный текст. Этот шаг необязателен, если вам нужен только конечный PDF, но он полезен для отладки.  

```csharp
// Perform OCR on the input TIFF
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/input.tif");

// Dump the raw text to the console (useful for validation)
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```  

**Совет:** Если извлечённый текст выглядит некорректно, рассмотрите предобработку изображения (выравнивание, удаление шумов) перед передачей его в движок. Aspose OCR также предоставляет утилиты улучшения изображения, которые можно использовать здесь.  

## Шаг 3 – Настройка экспортёра поискового PDF  

Теперь мы указываем Aspose, как должен выглядеть конечный PDF. `SearchablePdfExporter` позволяет задать путь вывода, соответствие PDF/A и несколько других параметров.  

```csharp
var pdfExporter = new SearchablePdfExporter
{
    // Where the searchable PDF will be saved
    OutputPath = "YOUR_DIRECTORY/output.pdf",

    // Enforce PDF/A‑1b compliance – ideal for long‑term archiving
    PdfACompliance = PdfACompliance.PdfA1b
};
```  

**Почему PDF/A‑1b?** Многие отрасли (юридическая, медицинская, финансовая) требуют PDF, соответствующие архивным стандартам. Установка `PdfACompliance` гарантирует встраивание шрифтов, независимость цветов от устройств и прохождение файла проверками.  

## Шаг 4 – Экспорт результата OCR напрямую в поисковый PDF  

Когда движок и экспортёр готовы, основная работа сводится к одной строке. Экспортёр внутри создаёт страницу PDF, накладывает распознанный текст как невидимый слой и записывает файл.  

```csharp
// Export the OCR result to a searchable PDF
pdfExporter.Export(ocrEngine, "YOUR_DIRECTORY/input.tif");

// Confirmation message
Console.WriteLine("Searchable PDF created at YOUR_DIRECTORY/output.pdf");
```  

**Что происходит под капотом?**  
1. Оригинальный TIFF встраивается как растровое изображение.  
2. Текст, полученный OCR, размещается сверху, скрыт, но доступен для выделения.  
3. Добавляются метаданные (например, язык), чтобы PDF‑читалки могли индексировать текст.  

## Шаг 5 – Проверка результата (ручная проверка + программная валидация)  

Всегда полезно убедиться, что PDF действительно является поисковым.  

```csharp
// Quick sanity check: open the PDF and try to extract its text
using var pdfReader = new Aspose.Pdf.Facades.PdfConverter();
pdfReader.BindPdf("YOUR_DIRECTORY/output.pdf");
var extracted = pdfReader.ExtractText();
Console.WriteLine("Text extracted from the PDF:");
Console.WriteLine(extracted);
```  

Если вы можете копировать‑вставлять текст из просмотрщика PDF или увидеть его в выводе консоли выше, вы успешно справились.  

## Пограничные случаи и распространённые варианты  

### Преобразование других форматов изображений  

Тот же код работает с PNG, JPEG, BMP — просто измените расширение файла в вызовах `Recognize` и `Export`. Дополнительная настройка не требуется.  

### Многостраничные TIFF‑файлы  

Aspose OCR автоматически обрабатывает каждую страницу многостраничного TIFF, а экспортёр собирает их в многостраничный PDF. Если нужно пропустить страницу, отфильтруйте `ocrResult.Pages` перед экспортом.  

### Языки, отличные от английского  

Замените `LanguageModel.English` на `LanguageModel.Spanish`, `LanguageModel.French` и т.д., либо загрузите пользовательский языковой пакет. Не забудьте скорректировать метаданные PDF, если вы нацеливаетесь на конкретную локаль.  

### Сокращение размера PDF  

Если TIFF‑файлы имеют высокое разрешение, полученный PDF может быть объёмным. Вы можете понизить разрешение изображения перед OCR:  

```csharp
ocrEngine.ImageProcessingOptions = new ImageProcessingOptions
{
    Dpi = 150 // Lower DPI reduces size, but test for acceptable quality
};
```  

### Работа с PDF, защищёнными паролем  

Если нужно защитить вывод, оберните `SearchablePdfExporter` в API шифрования Aspose.Pdf после экспорта:  

```csharp
var pdfDoc = new Aspose.Pdf.Document("YOUR_DIRECTORY/output.pdf");
pdfDoc.Encrypt("userPassword", "ownerPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save("YOUR_DIRECTORY/output_protected.pdf");
```  

## Полный рабочий пример  

Ниже представлен полный готовый к копированию и вставке пример программы, включающий все шаги и необязательные настройки, обсуждённые выше.  

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Export;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Initialize OCR engine and load language model
        // -----------------------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // Optional: lower DPI to shrink output size (adjust as needed)
        // ocrEngine.ImageProcessingOptions = new ImageProcessingOptions { Dpi = 150 };

        // -----------------------------------------------------------------
        // 2️⃣ Recognize text from the source TIFF
        // -----------------------------------------------------------------
        const string inputPath = @"YOUR_DIRECTORY/input.tif";
        var ocrResult = ocrEngine.Recognize(inputPath);
        Console.WriteLine("Extracted text from image:");
        Console.WriteLine(ocrResult.Text);

        // -----------------------------------------------------------------
        // 3️⃣ Configure the searchable PDF exporter
        // -----------------------------------------------------------------
        var pdfExporter = new SearchablePdfExporter
        {
            OutputPath = @"YOUR_DIRECTORY/output.pdf",
            PdfACompliance = PdfACompliance.PdfA1b // archival compliance
        };

        // -----------------------------------------------------------------
        // 4️⃣ Export OCR result to searchable PDF
        // -----------------------------------------------------------------
        pdfExporter.Export(ocrEngine, inputPath);
        Console.WriteLine("Searchable PDF created successfully.");

        // -----------------------------------------------------------------
        // 5️⃣ Verify by extracting text from the generated PDF
        // -----------------------------------------------------------------
        using var converter = new PdfConverter();
        converter.BindPdf(@"YOUR_DIRECTORY/output.pdf");
        var extractedFromPdf = converter.ExtractText();
        Console.WriteLine("Text extracted from the PDF:");
        Console.WriteLine(extractedFromPdf);
    }
}
```  

**Ожидаемый результат:**  
- Консоль выводит необработанный OCR‑текст из TIFF.  
- Файл `output.pdf` появляется в `YOUR_DIRECTORY`.  
- Открытие `output.pdf` в Adobe Reader позволяет выделять и копировать текст, подтверждая, что он поисковый.  

## Итоги  

Мы рассмотрели всё, что нужно для **create searchable PDF** файлов из TIFF‑изображений с помощью Aspose OCR на C#. От инициализации OCR‑движка, извлечения текста, настройки соответствия PDF/A до проверки конечного документа — каждый шаг подробно объяснён. Теперь вы также знаете, как **convert image to pdf**, **convert tiff to pdf**, **extract text from image**, и более общий вопрос **how to create pdf** с поисковыми слоями.  

## Что изучать дальше  

- **Batch processing:** Оберните логику в цикл, чтобы автоматически обрабатывать десятки изображений.  
- **Custom fonts:** Встраивание корпоративных шрифтов для согласованного брендинга.  
- **Cloud integration:** Сохраняйте PDF напрямую в Azure Blob Storage или AWS S3 после создания.  
- **UI front‑end:** Создайте простое приложение WinForms/WPF, позволяющее пользователям перетаскивать изображения для мгновенного преобразования.  

Не стесняйтесь экспериментировать с различными языковыми моделями, настройками DPI и уровнями PDF/A. API достаточно гибок, чтобы подстроиться под почти любой рабочий процесс, который вы можете представить.  

---  

*Счастливого кодинга, и пусть ваши PDF всегда будут поисковыми!*  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}