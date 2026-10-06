---
category: general
date: 2026-02-28
description: Создайте PDF с возможностью поиска в C#, объединяя изображения вертикально.
  Узнайте, как вертикально складывать изображения и конвертировать отсканированные
  страницы PDF с помощью Aspose OCR.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: ru
og_description: Создайте поисковый PDF в C# путем вертикального объединения изображений.
  Это руководство показывает, как вертикально складывать изображения и преобразовывать
  отсканированные страницы в PDF с помощью Aspose OCR.
og_title: Создание PDF с возможностью поиска в C# – вертикальное объединение изображений
tags:
- Aspose OCR
- C#
- PDF generation
title: Создание поискового PDF в C# – вертикальное объединение изображений
url: /ru/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF в C# – объединение изображений вертикально

Когда‑нибудь вам нужно было **создать поисковый PDF** из нескольких отсканированных PNG, но вы не знали, с чего начать? Вы не одни. Во многих проектах автоматизации документов главная боль — превратить стопку файлов‑изображений в один аккуратный, поисковый PDF, который можно индексировать и делиться.

В этом руководстве мы пройдем полный, готовый к запуску пример, который покажет вам **как вертикально укладывать изображения**, **как объединять изображения вертикально**, и в конце **конвертировать отсканированные страницы в PDF** в единый поисковый документ с использованием GPU‑ускоренного движка Aspose.OCR. К концу у вас будет автономная программа, которую можно добавить в любое решение .NET.

> **Что вы узнаете**
> - Инициализировать OCR‑движок с поддержкой GPU.
> - Обрабатывать пакет изображений параллельно.
> - **Объединять изображения вертикально**, имитируя многостраничное сканирование.
> - Экспортировать поисковый PDF и подробный JSON‑отчет для последующего анализа.

## Необходимые условия

- .NET 6+ (код компилируется с .NET 6, .NET 7 или .NET 8)
- NuGet‑пакет Aspose.OCR (`Install-Package Aspose.OCR`)
- Машина с поддержкой GPU, если вы хотите оставить настройку `ProcessingMode.Gpu` (CPU‑резерв работает тоже)
- Папка с несколькими отсканированными PNG/JPEG файлами (в демо используются `page1.png`, `page2.png`, `page3.png`)

Никаких внешних сервисов, никаких скрытых файлов конфигурации — только чистый C#.

## Шаг 1 – Настройка OCR‑движка для **создания поискового PDF**

Сначала мы создаём `OcrEngine`, включаем ускорение GPU, выбираем английский язык и добавляем пару фильтров предварительной обработки. Эти фильтры повышают точность, выравнивая наклонённые страницы (`DeskewFilter`) и удаляя шум (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Почему это важно:** OCR‑движок выполняет основную работу по распознаванию текста. Включение `ProcessingMode.Gpu` может сократить время распознавания вдвое на современной видеокарте, а фильтры уменьшают типичные артефакты сканирования, которые иначе приводили бы к искажённому выводу.

## Шаг 2 – Настройка пакетного процессора для эффективного **конвертирования отсканированных страниц PDF**

Обрабатывать каждую страницу по отдельности приемлемо для нескольких изображений, но в реальных проектах часто задействованы десятки или сотни страниц. `OcrBatchProcessor` из Aspose.OCR позволяет выполнять распознавания параллельно, резко ускоряя шаг **конвертирования отсканированных страниц pdf**.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Совет:** Если у вас машина только с CPU, установите `ProcessingMode = ProcessingMode.Cpu`. Пакетный процессор всё равно будет учитывать `MaxDegreeOfParallelism`, так что вы можете настроить его, чтобы не перегружать систему.

## Шаг 3 – Запуск OCR на пакете и сбор результатов

Теперь мы действительно распознаём текст. Метод `Recognize` возвращает список объектов `OcrResult`, каждый из которых содержит как оригинальное изображение, так и извлечённый текст.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

На данном этапе у вас есть всё, что нужно для **создания поискового PDF**: изображения (по‑прежнему в памяти) и связанные текстовые слои.

## Шаг 4 – **Объединить изображения вертикально** и создать поисковый PDF

Большинство отсканированных документов — это многостраничные PDF, поэтому нам нужно сшить отдельные изображения страниц в одно длинное изображение, имитирующее физическую стопку. Aspose.OCR предоставляет `Image.CombineVertical` именно для этой цели.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

Полученный файл (`combined_searchable.pdf`) содержит выделяемый, поисковый текст под каждым изображением страницы — именно то, что нужно для **создания поискового PDF** из отсканированных источников.

![Пример создания поискового PDF](/images/create-searchable-pdf.png "пример создания поискового pdf")

**Почему вертикальное объединение?** Многие OCR‑библиотеки рассматривают каждое изображение как отдельную страницу. Объединяя их, мы сохраняем порядок страниц в PDF, одновременно используя один проход OCR для всего документа.

## Шаг 5 – Экспорт подробного JSON для первой страницы (отлично для последующих рабочих процессов)

Иногда требуется не только PDF; возможно, вы хотите передать данные OCR в базу данных или конвейер машинного обучения. Aspose.OCR позволяет сериализовать каждый `OcrResult` в JSON, сохраняя ограничивающие рамки, оценки уверенности и многое другое.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Ожидаемый фрагмент JSON (усечённый):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

Теперь вы можете передать этот JSON в любую последующую систему — будь то индексация текста в Elasticsearch или передача в пользовательскую аналитическую панель.

---

## Как **вертикально укладывать изображения** – краткое резюме

Если вам интересно **как вертикально укладывать изображения** без Aspose, вы можете использовать `System.Drawing` для создания нового bitmap и отрисовки каждой страницы одну за другой. Однако встроенный в Aspose `Image.CombineVertical` обрабатывает DPI, формат пикселей и управление памятью за вас, делая его самым надёжным выбором для продакшн‑кода.

### Альтернатива: использование `System.Drawing` (просто из любопытства)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

Ручной подход работает, но вы теряете удобство автоматической обработки DPI и возможность напрямую передать результат обратно в `RecognizeToPdf`. Оставайтесь с `CombineVertical`, если только у вас нет очень специфических требований.

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|--------|
| **Ошибки нехватки памяти** при обработке десятков сканов высокого разрешения | Каждое изображение остаётся в памяти до записи PDF | Освобождайте объекты `Image` сразу после использования (`using` блоки) или уменьшайте разрешение изображений перед объединением |
| **Мусорный текст** после OCR | Наклонённые сканы или низкий контраст | Сохраняйте `DeskewFilter` и `DenoiseFilter`; при необходимости добавьте `ContrastFilter` |
| **Отсутствует поисковый слой** | Использован `Recognize` вместо `RecognizeToPdf` | Убедитесь, что вызываете `ocrEngine.RecognizeToPdf` для объединённого изображения |
| **Неудача резервного режима GPU** на машинах без подходящих драйверов | `ProcessingMode.Gpu` бросает исключение | Обёрните создание движка в try/catch и переключитесь на `ProcessingMode.Cpu` |

## Следующие шаги – расширение рабочего процесса

Теперь, когда вы знаете, как **создавать поисковый PDF**, вы можете захотеть:

- **Пакетно обрабатывать целые папки** с помощью `Directory.GetFiles` и цикла `foreach`.
- **Добавлять водяные знаки** к каждой странице перед объединением (используйте `ImageProcessor` из Aspose.Imaging).
- **Разбивать поисковый PDF обратно на отдельные страницы**, если позже понадобятся PDF‑файлы по отдельным страницам (`PdfDocument.Split` из Aspose.PDF).
- **Интегрировать с Azure Blob Storage**, чтобы получать изображения из облака и отправлять готовый PDF обратно.

Все эти расширения естественно опираются на те же основные концепции: настройка OCR, работа с изображениями и экспорт PDF.

## Заключение

Мы рассмотрели всё, что нужно для **создания поискового PDF** из набора отсканированных изображений в C#. Инициализировав GPU‑поддерживаемый `OcrEngine`, запустив параллельный пакет с `OcrBatchProcessor`, **объединив изображения вертикально** и, наконец, вызвав `RecognizeToPdf`, вы получаете аккуратный, поисковый документ, готовый к архивированию или индексации. Дополнительный экспорт JSON предоставляет полную видимость результатов OCR, открывая возможности для аналитики или пользовательских рабочих процессов.

Попробуйте, экспериментируйте с разными фильтрами, и наблюдайте, как ваш конвейер автоматизации документов становится гораздо плавнее. Если столкнётесь с какими‑либо странностями, оставьте комментарий — приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}