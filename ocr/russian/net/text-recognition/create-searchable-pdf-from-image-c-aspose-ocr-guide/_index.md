---
category: general
date: 2026-05-06
description: Создайте поисковый PDF из изображения с помощью Aspose OCR на C#. Узнайте,
  как преобразовать PNG в PDF, извлечь текст из изображения и сгенерировать поисковый
  PDF.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- convert png to pdf
- ocr image to pdf
language: ru
og_description: Создайте PDF с возможностью поиска из изображения с помощью Aspose
  OCR в C#. Этот пошаговый учебник показывает, как преобразовать PNG в PDF, извлечь
  текст из изображения и создать PDF с возможностью поиска.
og_title: Создание PDF с возможностью поиска из изображения – Руководство по Aspose
  OCR на C#
tags:
- Aspose
- C#
- OCR
- PDF
title: Создание поискового PDF из изображения — руководство по Aspose OCR на C#
url: /ru/net/text-recognition/create-searchable-pdf-from-image-c-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из изображения – руководство C# Aspose OCR

Когда‑нибудь вам нужно было **создать поисковый PDF** из отсканированного изображения, но вы не знали, с чего начать? Возможно, у вас есть PNG‑квитанция, JPEG‑контракт или любой битмап, который вы хотите превратить в PDF, по которому действительно можно искать. Это распространённая проблема, особенно когда вы работаете со старыми сканами, лежащими без дела в папке.

Хорошая новость в том, что с Aspose OCR вы можете **конвертировать изображение в PDF**, извлечь скрытый текст и получить полностью поисковый документ — всё это в нескольких строках C#. В этом руководстве мы также покажем, как **конвертировать png в PDF**, **извлекать текст из изображения**, а также рассмотрим крайний случай обработки многостраничных TIFF‑файлов. К концу вы получите автономное решение, которое можно внедрить в любой проект .NET.

## Что понадобится

- **.NET 6+** (код работает и на .NET Framework 4.6+)
- **Visual Studio 2022** или любую предпочитаемую IDE
- **Aspose.OCR** пакет NuGet (он автоматически подтягивает Aspose.PDF)
- Файл изображения (PNG, JPEG, BMP, TIFF), который вы хотите превратить в поисковый PDF

Никаких дополнительных лицензий, никаких внешних сервисов — только одна ссылка на NuGet и несколько минут кодинга.

## Шаг 1: Установите пакет Aspose.OCR из NuGet

Для начала добавьте библиотеку в ваш проект. Откройте консоль диспетчера пакетов и выполните:

```powershell
Install-Package Aspose.OCR
```

Эта единственная команда подтягивает как **Aspose.OCR**, так и сборку **Aspose.Pdf**, от которой она зависит, поэтому вы готовы как читать изображение, так и записывать PDF.

> **Pro tip:** Если вы используете .NET CLI, эквивалентная команда `dotnet add package Aspose.OCR`.

## Шаг 2: Инициализируйте OCR‑движок

Создание экземпляра `OcrEngine` — это вход в любую работу с OCR. Считайте его мозгом, который будет смотреть на ваше изображение и начинать «читать» символы.

```csharp
using Aspose.OCR;
using Aspose.Pdf;   // pulled in by the OCR package

// Create an OCR engine instance – this object holds configuration and state
var ocrEngine = new OcrEngine();
```

Вы можете задаться вопросом, *почему бы не вызвать статический метод?* Объектно‑ориентированный подход позволяет позже настраивать параметры (язык, разрешение и т.д.) без изменения общего потока.

## Шаг 3: Загрузите изображение, которое хотите конвертировать

Здесь мы **конвертируем изображение в PDF** по сути — передавая битмап в OCR‑движок. Замените `"YOUR_DIRECTORY/input.png"` реальным путём к вашему файлу.

```csharp
// Load the source image (PNG, JPEG, BMP, or multi‑page TIFF)
ocrEngine.SetImage("YOUR_DIRECTORY/input.png");
```

Если у вас сценарий **конвертировать png в pdf**, просто укажите PNG. Для многостраничных TIFF‑файлов Aspose.OCR автоматически будет рассматривать каждый кадр как отдельную страницу.

## Шаг 4: Запустите OCR и при желании получите текст

Вызов `Recognize()` выполняет тяжелую работу: он анализирует изображение, обнаруживает символы и возвращает структурированный результат. Вы можете сохранять текст для логирования, индексации поиска или отображения.

```csharp
// Perform OCR – this extracts the textual content from the image
var ocrResult = ocrEngine.Recognize();

// Optional: show the extracted text in the console
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

> **Почему извлекать текст?** Хотя мы внедрим его в конечный PDF, наличие сырой строки может быть полезным для валидации или аналитики.

## Шаг 5: Настройте параметры PDF для поискового документа

Aspose.PDF предоставляет специальный режим `PdfSaveOptions` под названием **CreateSearchablePdf**. Он указывает библиотеке внедрить OCR‑текст как невидимый слой позади изображения, делая PDF поисковым.

```csharp
// Prepare PDF save options – this tells Aspose to embed OCR text
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();
```

Если вам понадобится простой PDF только с изображением (без скрытого текста), можно переключиться на `PdfSaveOptions.CreatePdf()`. Но для нашей цели — **создать поисковый PDF** — режим поиска является главным.

## Шаг 6: Сохраните поисковый PDF на диск

Теперь мы связываем всё вместе. Метод `SavePdf` записывает изображение и скрытый текст в один файл.

```csharp
// Save the searchable PDF file
ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created successfully.");
```

На данном этапе у вас есть **поисковый PDF**, который можно открыть в Adobe Reader, ввести слово в поле поиска и мгновенно перейти к соответствующему месту — несмотря на то, что видимая страница всё ещё представляет собой оригинальное изображение.

## Полный рабочий пример

Собрав все части вместе, представляем готовое к запуску консольное приложение. Скопируйте‑вставьте его в новый проект C#, скорректируйте пути к файлам и нажмите **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf; // included automatically with Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image that contains the scanned document
        // Replace with your actual image path
        ocrEngine.SetImage("YOUR_DIRECTORY/input.png");

        // Step 3: Run the OCR process to extract text (optional but useful)
        var ocrResult = ocrEngine.Recognize();

        // Show extracted text – helpful for debugging
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("======================");

        // Step 4: Prepare to export the recognized content as a searchable PDF
        var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

        // Step 5: Save the searchable PDF to disk
        // Replace with your desired output path
        ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created successfully.");
    }
}
```

### Ожидаемый вывод

При запуске программы консоль выведет примерно следующее:

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑04‑30
Total: $1,250.00
...
======================
Searchable PDF created successfully.
```

А в `YOUR_DIRECTORY` вы найдёте `output.pdf`. Откройте его, нажмите **Ctrl F**, введите «Invoice», и вы сразу перейдёте к слову — несмотря на то, что страница выглядит как плоский скан.

## Обработка распространённых вариантов

### Конвертация нескольких изображений одновременно

Если у вас есть папка, полная PNG‑файлов, и вы хотите один поисковый PDF, пройдитесь по файлам в цикле и добавьте каждый как отдельную страницу:

```csharp
var allImages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
var ocrEngine = new OcrEngine();
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

foreach (var imgPath in allImages)
{
    ocrEngine.SetImage(imgPath);
    ocrEngine.Recognize(); // extracts text for the current page
    ocrEngine.SavePdf("temp_page.pdf", pdfOptions);

    // Merge temp_page.pdf into the final document (omitted for brevity)
}
```

Вы также можете использовать `PdfFileEditor` из Aspose.PDF для объединения временных PDF в один окончательный файл.

### Работа с низкокачественными сканами

Точность OCR снижается, когда DPI изображения ниже 150. Перед передачей изображения вы можете увеличить его масштаб:

```csharp
ocrEngine.ImageProcessingOptions.Dpi = 300; // forces 300 DPI for better recognition
```

### Выбор конкретного языка

Если ваш документ не на английском, задайте язык перед вызовом `Recognize()`:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, etc.
```

Эти настройки гарантируют, что **извлекать текст из изображения** работает надёжно в разных сценариях.

## Визуальный результат

![Поисковый PDF, созданный с помощью Aspose OCR – создать поисковый PDF](https://example.com/images/searchable-pdf.png)

*На скриншоте выше показан PDF, где изображение видно, но текстовый слой можно искать.*

## Заключение

Теперь у вас есть полное, готовое к продакшену решение для **создания поисковых PDF** файлов из любого изображения с помощью Aspose OCR и C#. Мы рассмотрели, как **конвертировать изображение в PDF**, **извлекать текст из изображения**, а также коснулись крайних случаев **конвертировать png в pdf** и **ocr image to pdf**. Код полностью автономный, работает на любой среде .NET и может быть расширен для пакетной обработки или поддержки пользовательских языков.

Что дальше? Попробуйте добавить водяной знак, зашифровать PDF или передать извлечённый текст в поисковый индекс, например Elasticsearch. Возможности безграничны, и тот же шаблон — загрузить → распознать → сохранить — будет полезен для любого OCR‑ориентированного рабочего процесса.

Если столкнётесь с проблемами или хотите поделиться интересным кейсом, оставьте комментарий ниже. Счастливого кодинга и наслаждайтесь превращением упорных сканов в поисковое золото!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}