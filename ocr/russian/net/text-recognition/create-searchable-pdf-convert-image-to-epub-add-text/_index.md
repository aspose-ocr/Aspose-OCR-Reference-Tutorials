---
category: general
date: 2026-03-13
description: Создайте PDF с возможностью поиска из любого изображения с помощью Aspose
  OCR. Узнайте, как преобразовать изображение в EPUB, добавить поисковый текст и сгенерировать
  PDF с возможностью поиска на C#.
draft: false
keywords:
- create searchable pdf
- convert image to epub
- ocr image to pdf
- add searchable text
- generate searchable pdf
language: ru
og_description: Создайте PDF с возможностью поиска из любого изображения с помощью
  Aspose OCR. В этом руководстве показано, как преобразовать изображение в EPUB, добавить
  поисковый текст и сгенерировать PDF с возможностью поиска на C#.
og_title: Создать PDF с поисковым текстом – преобразовать изображение в EPUB и добавить
  текст
tags:
- Aspose OCR
- C#
- PDF
- EPUB
title: Создать PDF с поиском – преобразовать изображение в EPUB и добавить текст
url: /ru/net/text-recognition/create-searchable-pdf-convert-image-to-epub-add-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF – Конвертация изображения в EPUB и добавление текста

Хотите **создать поисковый PDF** из отсканированного чека или любого изображения? В этом руководстве мы покажем, как создать поисковый PDF с помощью Aspose OCR, а также **конвертировать изображение в EPUB** и **добавить слои поискового текста** — всё в одном проекте C#.

Если вы когда‑нибудь сталкивались с PDF‑файлами, которые выглядят красиво, но их нельзя искать, вы не одиноки. Хорошая новость в том, что скрытый текстовый слой может превратить плоское изображение в полностью поисковый документ, и Aspose делает это почти без усилий.

## Что вы узнаете

* Как инициализировать движок Aspose OCR и задать язык.  
* Точные шаги для **конвертации изображения в EPUB** для распространения электронных книг.  
* Как настроить PDF‑writer, чтобы вывод содержал скрытый, поисковый текстовый слой.  
* Советы по обработке крайних случаев, таких как многостраничные чеки или неанглийские языки.  

Всё, что вам понадобится заранее, — это среда разработки .NET (Visual Studio 2022 или новее) и пакет Aspose OCR NuGet. Никаких внешних сервисов, никаких сложных файлов конфигурации — только чистый C#, который вы можете скопировать‑вставить и запустить.

## Требования

| Требование | Почему это важно |
|-------------|-------------------|
| .NET 6.0+   | Aspose OCR ориентирован на .NET Standard 2.0+, поэтому .NET 6 предоставляет последние улучшения среды выполнения. |
| Aspose.OCR NuGet package | Предоставляет классы `OcrEngine`, `EpubWriter` и `PdfWriter`, используемые в коде. |
| An image file (e.g., `receipt.jpg`) | Исходный файл, на котором будет выполнен OCR. Любое растровое изображение (PNG, JPEG, BMP) подходит. |
| Basic C# knowledge | Вы будете читать и изменять фрагменты кода, а не изучать язык с нуля. |

Вы можете установить пакет с помощью следующей команды:

```bash
dotnet add package Aspose.OCR
```

> **Совет:** Если вы используете Visual Studio, UI менеджера пакетов NuGet делает то же самое — просто найдите “Aspose.OCR”.

## Шаг 1 — Создание поискового PDF с помощью Aspose OCR

Первое, что нам нужно, — это экземпляр `OcrEngine`, который знает, какой язык распознавать. По умолчанию используется английский, но вы можете заменить его на французский, немецкий и т.д., задав `ocrEngine.Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialise the OCR engine and set the language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English          // Change this if your document isn’t English
};
```

Зачем сначала инициализировать движок? Движок хранит модель распознавания в памяти, поэтому создание его один раз и повторное использование для нескольких изображений экономит и ЦП, и ОЗУ. В больших пакетных заданиях вы бы держали один и тот же экземпляр активным на протяжении всей обработки.

## Шаг 2 — Загрузка изображения и выполнение OCR

Далее мы указываем движку файл, который нужно обработать. `ImageStream.FromFile` читает изображение в формат, понятный OCR‑движку.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Run the recognition engine – this populates the internal text buffer
ocrEngine.Recognize();
```

> **Что если изображение многостраничное?**  
> Aspose OCR умеет работать с многостраничными TIFF‑файлами из коробки. Просто передайте путь к TIFF‑файлу; движок автоматически пройдётся по каждой странице.

## Шаг 3 — Конвертация изображения в EPUB

Если вам также нужна версия отсканированного документа в виде e‑book, Aspose делает это в одну строку. `EpubWriter` использует тот же экземпляр `OcrEngine`, что означает повторное использование результатов OCR без дополнительной обработки.

```csharp
// Export the recognised content to an ePub file
EpubWriter epubWriter = new EpubWriter();
epubWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt.epub");
```

Зачем экспортировать в EPUB? EPUB — это формат с переупорядочиваемым содержимым, идеальный для мобильных читалок. Текст OCR становится выделяемым, а оригинальное изображение остаётся фоном, сохраняя внешний вид исходного скана.

## Шаг 4 — Добавление поискового текстового слоя в PDF

Теперь переходим к части, которая действительно **создаёт поисковый PDF**. Включив `AddSearchableTextLayer`, PDF‑writer встраивает невидимый текстовый слой, отражающий результаты OCR. Пользователи могут искать, копировать или выделять текст так же, как в обычном PDF.

```csharp
// Configure PDF writer to include a hidden searchable text layer
PdfWriter pdfWriter = new PdfWriter
{
    AddSearchableTextLayer = true   // Enables the hidden text layer for searchability
};

// Save the OCR result as a searchable PDF
pdfWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt_searchable.pdf");
```

> **Распространённая ошибка:** Если забыть установить `AddSearchableTextLayer`, получится PDF, выглядящий так же, но без поискового текста. Всегда проверяйте этот флаг, когда нужен поисковый документ.

## Шаг 5 — Полный рабочий пример

Объединив всё вместе, представляем автономное консольное приложение, которое вы можете добавить в новый проект .NET и сразу запустить.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace OcrToPdfAndEpub
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the source image
            string imagePath = "YOUR_DIRECTORY/receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            ocrEngine.Recognize();

            // 4️⃣ Convert to EPUB (optional but handy)
            EpubWriter epubWriter = new EpubWriter();
            string epubPath = "YOUR_DIRECTORY/receipt.epub";
            epubWriter.Save(ocrEngine, epubPath);
            Console.WriteLine($"EPUB saved to {epubPath}");

            // 5️⃣ Create searchable PDF
            PdfWriter pdfWriter = new PdfWriter
            {
                AddSearchableTextLayer = true
            };
            string pdfPath = "YOUR_DIRECTORY/receipt_searchable.pdf";
            pdfWriter.Save(ocrEngine, pdfPath);
            Console.WriteLine($"Searchable PDF saved to {pdfPath}");
        }
    }
}
```

### Ожидаемый результат

* `receipt.epub` — файл EPUB, который можно открыть в Calibre, Apple Books или любом e‑reader.  
* `receipt_searchable.pdf` — PDF, в котором можно нажать **Ctrl + F** и найти любое слово, присутствующее в оригинальном изображении.

Если открыть PDF в Adobe Acrobat и посмотреть **File → Properties → Description**, вы увидите скрытый текстовый поток во вкладке **Fonts**, подтверждающий наличие поискового слоя.

## Часто задаваемые вопросы и особые случаи

**В: Работает ли это с неанглийскими языками?**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}