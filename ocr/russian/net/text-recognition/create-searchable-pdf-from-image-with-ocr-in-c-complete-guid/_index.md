---
category: general
date: 2026-05-21
description: Создайте PDF с возможностью поиска из изображения, используя Aspose OCR
  в C#. Преобразуйте изображение в PDF, задайте разрешение PDF и внедрите исходное
  изображение.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- set pdf resolution
- pdf with embedded image
language: ru
og_description: Создайте PDF с возможностью поиска из изображения, используя Aspose
  OCR в C#. Узнайте, как преобразовать изображение в PDF, установить разрешение PDF
  и внедрить оригинальное изображение.
og_title: Создать PDF с возможностью поиска из изображения с OCR в C#
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Create searchable PDF from an image using Aspose OCR in C#. Convert
    image to PDF, set PDF resolution, and embed the original image.
  headline: Create Searchable PDF from Image with OCR in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- Aspose
- C#
- PDF
title: Создание поискового PDF из изображения с OCR в C# — Полное руководство
url: /ru/net/text-recognition/create-searchable-pdf-from-image-with-ocr-in-c-complete-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из изображения с OCR в C# – Полное руководство

Когда‑то вам нужно **создать поисковый PDF** из отсканированных счетов, чеков или рукописных заметок? Вы не одиноки — разработчики постоянно сталкиваются с этой задачей при построении конвейеров управления документами. Хорошая новость: с Aspose.OCR вы можете **преобразовать изображение в PDF**, встроить оригинальную картинку и даже задать выходное DPI, всё в паре строк кода C#.

В этом руководстве мы пройдем весь процесс превращения обычного PNG в **поисковый PDF**. Вы увидите, как **OCR изображение в PDF**, **установить разрешение PDF** и сохранить исходную графику внутри файла. К концу вы получите готовый фрагмент кода, который можно вставить в любой .NET‑проект.

## Требования

- .NET 6.0 или новее (API работает с .NET Core и .NET Framework)
- Лицензия Aspose.OCR или бесплатный оценочный ключ
- Пример изображения (например, `invoice.png`), размещённый там, где приложение сможет его прочитать
- Visual Studio, Rider или любой другой редактор

Никаких дополнительных пакетов NuGet помимо `Aspose.OCR` не требуется — всё остальное входит в базовую библиотеку классов .NET.

<img src="/images/searchable-pdf-example.png" alt="Create searchable PDF example in C#" />

## Шаг 1: Инициализация OCR‑движка — сердце процесса

Первым делом нам нужен экземпляр `OcrEngine`, и нужно указать, какой язык распознавать. Английский подходит для большинства счетов, но вы можете подменить его любой величиной из перечисления `OcrLanguage`.

```csharp
using Aspose.OCR;

// Step 1 – create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English   // Change if you need another language
};
```

**Почему это важно:** Движок — это рабочая лошадка, которая читает пиксельные данные и превращает их в поисковый текст. Указание языка заранее значительно повышает точность, особенно для нелатинских скриптов.

## Шаг 2: Загрузка исходного изображения — с диска в память

Далее указываем движку файл изображения, которое нужно обработать. Aspose предоставляет удобный помощник `ImageStream.FromFile`, скрывающий детали работы с `FileStream`.

```csharp
using Aspose.OCR;

// Step 2 – load the image containing the text
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");
```

**Подсказка:** Если ваше изображение находится в облачном бакете или приходит из HTTP‑запроса, вы также можете передать `MemoryStream` в `ImageStream.FromStream`. OCR‑движок не интересуется, откуда берутся байты.

## Шаг 3: Настройка параметров сохранения PDF — встраивание изображения и установка разрешения

Теперь сообщаем Aspose, как должен выглядеть итоговый PDF. Два параметра критичны для **поискового PDF**:

1. `EmbedOriginalImage = true` — сохраняет отсканированную картинку внутри PDF, обеспечивая визуальную точность.
2. `OutputResolution = 300` — задаёт DPI поискового слоя; 300 DPI — оптимальный вариант для большинства задач OCR.

```csharp
using Aspose.OCR.Pdf;   // PDF‑specific options

// Step 3 – define how the PDF should be saved
var pdfOptions = new PdfSaveOptions
{
    EmbedOriginalImage = true,   // Keeps the original image inside the PDF
    OutputResolution = 300       // DPI of the searchable PDF (set PDF resolution)
};
```

**Зачем эти настройки?** Встраивание оригинального изображения (`pdf with embedded image`) гарантирует, что документ будет выглядеть точно как скан, а слой OCR‑текста делает его поисковым. При необходимости можно уменьшить `OutputResolution` (например, 150 DPI) для более лёгкого файла или увеличить (600 DPI) для большей точности.

## Шаг 4: Сохранение результата — от OCR‑движка к поисковому PDF

Наконец, вызываем `Save`, указывая путь к выходному файлу и только что созданный `PdfSaveOptions`. Эта единственная строка делает всю тяжёлую работу: запускает OCR, создаёт скрытый текстовый слой и записывает PDF на диск.

```csharp
// Step 4 – generate the searchable PDF
ocrEngine.Save("YOUR_DIRECTORY/invoice_searchable.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created.");
```

**Что вы получаете:** Файл `invoice_searchable.pdf`, который выглядит как оригинальный `invoice.png`, но может быть проиндексирован Windows Search, инструментом Find в Adobe Reader или любой системой полнотекстового поиска.

## Шаг 5: Проверка результата — быстрые проверки

После выполнения кода откройте PDF в Adobe Acrobat (или любом другом просмотрщике) и попробуйте найти слово, которое точно присутствует в счёте, например «Total». Если поиск находит термин, вы успешно **ocr image to PDF**.

Можно также посмотреть размер файла: поскольку мы **встраиваем оригинальное изображение**, PDF будет больше, чем чисто текстовый, но компромисс оправдан визуальной точностью.

## Распространённые проблемы и профессиональные советы

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Пустой PDF** | `ocrEngine.Image` не установлен или путь неверный | Проверьте путь к файлу и убедитесь, что изображение загружается без исключений |
| **Низкая точность поиска** | Слишком низкое `OutputResolution` или неверный язык | Увеличьте `OutputResolution` до 300‑600 DPI и задайте правильный `OcrLanguage` |
| **Файл слишком большой** | `EmbedOriginalImage = true` при сканах высокого разрешения | Перед подачей в движок уменьшите разрешение исходного изображения или установите `EmbedOriginalImage = false`, если нужен только поисковый текст |
| **Лицензионные исключения** | Используется бесплатная пробная версия без ключа | Получите временный лицензионный ключ на сайте Aspose и вызовите `License license = new License(); license.SetLicense("Aspose.OCR.lic");` перед созданием движка |

## Полный рабочий пример — копировать, вставлять, запускать

Ниже представлено самостоятельное консольное приложение, которое можно сразу собрать. Замените `YOUR_DIRECTORY` реальной папкой на вашем компьютере.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑specific options

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the source image (convert image to PDF later)
            string inputPath = @"YOUR_DIRECTORY\invoice.png";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Set PDF options – embed image & set PDF resolution
            var pdfOptions = new PdfSaveOptions
            {
                EmbedOriginalImage = true,
                OutputResolution = 300 // DPI – you can change this to set PDF resolution
            };

            // 4️⃣ Save as searchable PDF
            string outputPath = @"YOUR_DIRECTORY\invoice_searchable.pdf";
            ocrEngine.Save(outputPath, pdfOptions);

            Console.WriteLine("Searchable PDF created at:");
            Console.WriteLine(outputPath);
        }
    }
}
```

**Ожидаемый вывод** (в консоли):

```
Searchable PDF created at:
C:\Your\Path\YOUR_DIRECTORY\invoice_searchable.pdf
```

Откройте полученный PDF и проверьте функцию поиска — вуаля, вы только что **создали поисковый PDF** из изображений.

## Заключение

Мы рассмотрели всё, что нужно для **создания поискового PDF** с помощью Aspose OCR в C#. От загрузки изображения и настройки **PDF с встраиваемым изображением**, до **установки разрешения PDF** и окончательного **сохранения результата OCR** — весь конвейер укладывается в несколько строк кода.

Что дальше? Попробуйте пакетную обработку десятков счетов, поэкспериментируйте с различными языками или интегрируйте код в ASP.NET Core API, обрабатывающее загрузки «на лету». Вы также можете добавить водяные знаки или цифровые подписи — обе функции поддерживаются Aspose.PDF для дальнейшего укрепления документов.

Есть вопросы о граничных случаях, лицензировании или оптимизации производительности? Оставляйте комментарий ниже, и счастливого кодинга!

## Похожие руководства

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}