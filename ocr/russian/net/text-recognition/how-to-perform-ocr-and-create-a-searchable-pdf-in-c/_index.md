---
category: general
date: 2026-02-14
description: Узнайте, как выполнять OCR на TIFF‑файле или изображении и преобразовать
  PDF с помощью OCR, чтобы создать PDF с возможностью поиска — пошаговое руководство
  на C#.
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: ru
og_description: Узнайте, как выполнять OCR на изображениях, конвертировать PDF с помощью
  OCR и создавать PDF с возможностью поиска с помощью Aspose OCR в кратком руководстве
  на C#.
og_title: Как выполнить OCR и создать PDF с возможностью поиска в C#
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: Как выполнить OCR и создать PDF с возможностью поиска в C#
url: /ru/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

translate everything else.

Let's produce the translated content.

Be careful with bullet points: maintain dash and spaces.

Also maintain blockquote >.

Let's produce.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить OCR и создать поисковый PDF в C#

Нуждались **выполнить OCR** на отсканированном документе, но не знали, как превратить результат в поисковый PDF? Вы не одиноки — многие разработчики сталкиваются с этой проблемой при работе с архивами TIFF старого формата или PDF, содержащими только изображения. Хорошая новость: с несколькими строками C# и библиотекой Aspose.OCR вы можете за считанные секунды преобразовать TIFF или любое изображение в полностью поисковый PDF.

В этом руководстве мы пройдём всё, что нужно знать: от установки библиотеки, загрузки многостраничного TIFF, до вызова `RecognizeToPdf`, чтобы **конвертировать PDF с помощью OCR** и **создать поисковый PDF**, который пользователи действительно смогут искать. К концу вы получите готовое консольное приложение, генерирующее поисковый PDF из источника‑изображения.

## Требования

- **.NET 6.0** или новее (код также работает на .NET Framework 4.7+).
- Действительная лицензия **Aspose.OCR** или временный ключ оценки (бесплатная пробная версия достаточна для тестов).
- Visual Studio 2022 (или любой другой редактор) с менеджером пакетов **NuGet**.
- Входной файл `input.tif`, помещённый в папку, которой вы управляете — многостраничные TIFF работают сразу.

> **Полезный совет:** Если вы работаете в Windows, скопируйте TIFF в ту же папку, где находится скомпилированный `.exe`, чтобы избежать проблем с путями.

## Шаг 1: Установить NuGet‑пакет Aspose.OCR

Откройте папку проекта в терминале и выполните:

```bash
dotnet add package Aspose.OCR
```

Это загрузит последнюю стабильную версию (по состоянию на февраль 2026 года это 23.10) и добавит все необходимые зависимости. После завершения восстановления вы увидите `Aspose.OCR` в разделе **Dependencies** в обозревателе решений.

## Шаг 2: Создать минимальное консольное приложение

Создайте новый консольный проект, если у вас его ещё нет:

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

Замените автоматически сгенерированный `Program.cs` полным кодом, показанным в **Шаге 3**. Программа будет:

1. Создавать экземпляр OCR‑движка.  
2. Загружать исходное изображение (или многостраничный TIFF).  
3. Выполнять OCR и записывать результат напрямую в поисковый PDF.  
4. Уведомлять пользователя об успешном завершении.

## Шаг 3: Полный рабочий код — от изображения к поисковому PDF

Ниже представлен **полный** исходный файл. Скопируйте‑вставьте его в `Program.cs`. Комментарии объясняют менее очевидные части.

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**Что вы увидите:** После запуска программы в целевой папке появится файл `searchable.pdf`. Откройте его в Adobe Reader или любом другом PDF‑просмотрщике и попробуйте поискать слово, которое есть в оригинальном TIFF. Текст будет найден мгновенно, подтверждая, что вы **создали поисковый PDF** из изображения.

### Запуск приложения

```bash
dotnet run
```

Если всё настроено правильно, вы получите:

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

Откройте PDF, нажмите `Ctrl+F`, введите слово из исходного файла и наблюдайте, как выделение перемещается к нужному месту.

## Шаг 4: Распространённые варианты и особые случаи

### Конвертация обычного PDF (только изображения) в поисковый PDF

Если ваш источник — PDF, содержащий отсканированные изображения вместо текста, вы всё равно можете использовать тот же метод — просто измените источник `ImageStream`:

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

Это решает задачу **convert pdf using OCR** без дополнительного кода.

### Обработка больших многостраничных документов

Для документов, превышающих несколько сотен страниц, рекомендуется:

- **Увеличить лимит памяти** (`Engine.MemoryLimit = 2_000; // MB`).  
- **Обрабатывать частями**: загружать подмножество страниц, записывать промежуточные PDF, а затем объединять их с помощью PDF‑библиотеки (например, Aspose.PDF).

### Работа с языками, отличными от английского

Aspose.OCR поддерживает множество языков «из коробки». Установите язык перед распознаванием:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Если вам нужен **tiff to searchable pdf** для нелатинского скрипта, убедитесь, что установлен соответствующий языковой пакет.

### Что делать, если полученный PDF пустой?

- Проверьте, что входной файл не повреждён.  
- Убедитесь, что у OCR‑движка есть действительная лицензия — в режиме оценки могут быть ограничения по количеству страниц.  
- Убедитесь, что разрешение изображения минимум 300 dpi; более низкое разрешение приводит к плохому распознаванию.

## Шаг 5: Программная проверка результата (по желанию)

Иногда требуется убедиться, что в PDF действительно есть текстовый слой. Можно воспользоваться Aspose.PDF для извлечения текста:

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

Если переменная `extracted` не пуста, вы успешно **создали searchable pdf**.

## Заключение

Мы рассмотрели **как выполнить OCR** на TIFF (или любом изображении) и без проблем **конвертировать PDF с помощью OCR**, получив **поисковый PDF**, который ведёт себя как обычный документ. Ключевые шаги:

1. Установить Aspose.OCR.  
2. Инициализировать `Engine`.  
3. Загрузить изображение через `ImageStream`.  
4. Вызвать `RecognizeToPdf`.  

Дальше вы можете экспериментировать с настройками языка, обработкой больших пакетов или комбинировать результат с другими задачами манипуляции PDF. Тот же подход работает для **tiff to searchable pdf**, **searchable pdf from image** и даже сканированных PDF.

Готовы к следующему вызову? Попробуйте внедрить OCR в веб‑API, чтобы пользователи могли загружать сканы и мгновенно получать поисковые PDF, или исследуйте OCR рукописных заметок с помощью расширенных настроек `OcrEngine`. Возможностей бесконечно — удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}