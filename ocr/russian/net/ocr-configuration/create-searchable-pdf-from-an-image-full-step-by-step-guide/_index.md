---
category: general
date: 2026-06-06
description: Узнайте, как создавать поисковые PDF и преобразовывать изображения в
  PDF с OCR. Включает добавление слоёв, настройки сжатия и полный код на C#.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- how to ocr image
- how to add layer
- how to set compression
language: ru
og_description: Создайте поисковый PDF из изображения с помощью OCR. Это руководство
  показывает, как добавить скрытый текстовый слой, установить сжатие и преобразовать
  изображение в PDF.
og_title: Создайте PDF с возможностью поиска – Полный учебник по C#
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  headline: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  name: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - The
      Aspose.OCR and Aspose.Pdf NuGet packages (or any equivalent library that offers
      `OcrEngine` and `PdfSaveOptions`). - A sample image, e.g., `invoice.png`, placed
      in a folder you can reference. - A basic understanding of C# syntax'
  - name: Full Working Example
    text: 'Putting it all together, here’s the complete, ready‑to‑run program:'
  - name: Pro tip
    text: If you need to **convert image to PDF** without OCR (just a plain image
      PDF), set `AddTextLayer = false`. The same `PdfSaveOptions` still lets you control
      compression, which is handy for archiving scanned documents that don’t need
      searchability.
  type: HowTo
tags:
- OCR
- PDF
- C#
- Aspose
title: Создание поискового PDF из изображения – полное пошаговое руководство
url: /ru/net/ocr-configuration/create-searchable-pdf-from-an-image-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF – Полный C#‑урок

Когда‑нибудь задумывались, как **создать поисковый PDF** из отсканированного счета без часов работы в графическом инструменте? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужно превратить изображение в PDF, который выглядит как оригинал и позволяет пользователям копировать или искать текст.  

В этом руководстве мы пошагово пройдем процесс **преобразования изображения в PDF**, запустим OCR, добавим скрытый текстовый слой и даже настроим параметры сжатия. К концу вы получите готовый фрагмент кода C#, который можно вставить в любой проект .NET.

## Что вы узнаете

- Настроить OCR‑движок и понять **как выполнять OCR изображения**.
- Использовать опцию **как добавить слой** для внедрения поискового текстового наложения.
- Применить **как задать сжатие** для более мелких PDF‑файлов, сжатых ZIP‑ом.
- Превратить обычную картинку в **создание поискового pdf** процесс, который можно автоматизировать.
- Распространённые подводные камни и профессиональные советы, чтобы ваши PDF‑файлы оставались чёткими и быстрыми.

### Предварительные требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+).
- Пакеты NuGet Aspose.OCR и Aspose.Pdf (или любая эквивалентная библиотека, предоставляющая `OcrEngine` и `PdfSaveOptions`).
- Пример изображения, например `invoice.png`, размещённый в папке, к которой вы можете обратиться.
- Базовое понимание синтаксиса C# — глубоких знаний OCR не требуется.

> **Pro tip:** Если вы используете Visual Studio, установите пакеты через консоль диспетчера пакетов:  
> `Install-Package Aspose.OCR`  
> `Install-Package Aspose.Pdf`

---

![Пример создания поискового PDF, показывающий изображение счета, преобразованное в PDF с скрытым текстовым слоем](/images/create-searchable-pdf.png)

## Шаг 1: Инициализация OCR‑движка – **how to ocr image**

Сначала нам нужен OCR‑движок, способный читать английский текст с нашей картинки. Класс `OcrEngine` — точка входа; вы просто задаёте язык и позже передаёте ему изображение.

```csharp
using Aspose.OCR;
using Aspose.Pdf;

// Create and configure the OCR engine
OcrEngine engine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

*Почему это важно:* Инициализация движка с правильным языком значительно повышает точность. Если пропустить этот шаг, вы можете получить искажённые символы.

## Шаг 2: Загрузка изображения – **convert image to pdf**

Теперь указываем движку файл, который нужно обработать. `ImageStream.FromFile` считывает байты и подготавливает их к OCR.

```csharp
// Load the image you want to turn into a searchable PDF
engine.Image = ImageStream.FromFile(@"C:\Docs\invoice.png");
```

Также можно загрузить из `MemoryStream`, если изображение поступает из веб‑запроса или базы данных.

## Шаг 3: Запуск распознавания OCR – **how to ocr image**

После загрузки изображения тяжёлая работа происходит одним вызовом. Метод `Recognize` возвращает `OcrResult`, содержащий как извлечённый текст, так и оригинальный битмап.

```csharp
// Perform OCR on the loaded image
OcrResult ocrResult = engine.Recognize();
```

*Что происходит в фоне:* Движок анализирует каждый пиксель, определяет символы и формирует строку Unicode. Он также сохраняет позиционные данные, необходимые позже для скрытого текстового слоя.

## Шаг 4: Настройка параметров сохранения PDF – **how to add layer** & **how to set compression**

Здесь происходит магия поискового PDF. Мы создаём объект `PdfSaveOptions`, который указывает Aspose.Pdf, как встроить оригинальное изображение, добавить скрытый текстовый слой и сжать итоговый файл.

```csharp
// Set up PDF options for a searchable PDF
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    IncludeImage = true,          // Keep the original image in the PDF
    AddTextLayer = true,          // Add a hidden text layer with OCR results
    Compression = PdfCompression.Zip   // Use ZIP compression for smaller size
};
```

- **IncludeImage** гарантирует визуальное соответствие оригинальному скану.
- **AddTextLayer** создаёт невидимый слой, который браузеры и PDF‑просмотрщики могут индексировать для поиска.
- **Compression** уменьшает размер файла без потери качества; ZIP — хороший вариант по умолчанию для большинства документов.

## Шаг 5: Сохранение результата – **create searchable pdf**

Наконец, сохраняем результат OCR на диск, используя только что определённые параметры. Метод `Save` принимает путь назначения и экземпляр `PdfSaveOptions`.

```csharp
// Save the OCR result as a searchable PDF
ocrResult.Save(@"C:\Docs\invoice_searchable.pdf", pdfOptions);
```

Когда откроете `invoice_searchable.pdf` в Adobe Reader или любом современном просмотрщике, вы увидите оригинальное изображение, но теперь сможете выделять, копировать и искать текст так, как если бы это был нативный PDF.

### Полный рабочий пример

Объединив всё вместе, получаем полностью готовую к запуску программу:

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine engine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the source image
            string imagePath = @"C:\Docs\invoice.png";
            engine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            OcrResult result = engine.Recognize();

            // 4️⃣ Configure PDF options (layer + compression)
            PdfSaveOptions pdfOptions = new PdfSaveOptions
            {
                IncludeImage = true,
                AddTextLayer = true,
                Compression = PdfCompression.Zip
            };

            // 5️⃣ Save as searchable PDF
            string pdfPath = @"C:\Docs\invoice_searchable.pdf";
            result.Save(pdfPath, pdfOptions);

            Console.WriteLine($"Searchable PDF created at: {pdfPath}");
        }
    }
}
```

**Ожидаемый вывод** (в консоли):  
`Searchable PDF created at: C:\Docs\invoice_searchable.pdf`

Откройте полученный файл, нажмите **Ctrl F**, введите слово, которое видите в счёте, и наблюдайте, как просмотрщик мгновенно переходит к нему. Это и есть суть **create searchable pdf** в действии.

## Распространённые ошибки и как их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| Текст не ищется | `AddTextLayer` оставлен `false` или используется устаревшая версия Aspose | Убедитесь, что `AddTextLayer = true` и обновите до последней версии NuGet |
| PDF огромный (мегабайты) | Сжатие установлено в `PdfCompression.None` | Переключите на `PdfCompression.Zip` или `PdfCompression.Jpeg` для изображений |
| Искажённые символы | Неправильный язык или изображение низкого разрешения | Правильно задайте `engine.Language` и используйте изображения минимум 300 dpi |
| Скрытый слой не виден в некоторых просмотрщиках | PDF создан с нестандартной версией PDF | Используйте `PdfSaveOptions.PdfVersion = PdfVersion.PDF_1_7` (по умолчанию) или обновите просмотрщик |

### Pro tip

Если нужно **convert image to PDF** без OCR (просто PDF с изображением), установите `AddTextLayer = false`. Те же `PdfSaveOptions` позволяют управлять сжатием, что удобно для архивирования сканов, которым не требуется поиск.

## Расширение решения

- **Несколько страниц**: Пройдитесь по списку файлов изображений, каждый раз задавая `engine.Image = ...` и собирайте результаты в один PDF с помощью агрегирования `PdfDocument`.
- **Разные языки**: Измените `engine.Language = OcrLanguage.Spanish` (или любой поддерживаемый язык) для обработки многоязычных счетов.
- **Пользовательское сжатие**: Для цветных изображений `PdfCompression.Jpeg` с настройкой качества (`pdfOptions.JpegQuality = 80`) может ещё сильнее уменьшить размер файлов.

## Заключение

Мы рассмотрели всё, что нужно для **create searchable PDF** из изображений с помощью C#. От инициализации OCR‑движка, загрузки картинки, распознавания, настройки скрытого текстового слоя до задания сжатия — каждый шаг играет важную роль в получении быстрого, поискового документа.  

Теперь вы можете автоматизировать обработку счетов, архивировать контракты или построить утилиту массового сканирования, превращающую стопки бумаги в мгновенно‑поисковые PDF.  

Готовы к следующему вызову? Попробуйте добавить водяные знаки, объединять несколько поисковых PDF или вынести эту логику в Web API, чтобы вся организация могла загружать изображения и получать поисковые PDF «на лету».

---

*Если этот гид оказался полезным, поставьте ⭐, поделитесь им с коллегами или оставьте комментарий со своими доработками. Счастливого кодинга!*


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом материале. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}