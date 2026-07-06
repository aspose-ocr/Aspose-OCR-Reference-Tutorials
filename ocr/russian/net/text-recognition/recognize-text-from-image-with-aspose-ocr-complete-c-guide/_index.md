---
category: general
date: 2026-05-25
description: распознавать текст на изображении с помощью Aspose OCR в C#. Узнайте,
  как загрузить изображение для OCR, установить язык OCR, создать движок OCR и извлечь
  текст из TIFF.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- set OCR language
- create OCR engine
language: ru
og_description: распознавать текст на изображении с помощью Aspose OCR в C#. Этот
  учебник показывает, как создать OCR‑движок, загрузить изображение для OCR, установить
  язык OCR и извлечь текст из TIFF.
og_title: Распознавание текста на изображении с помощью Aspose OCR – Полное руководство
  по C#
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: recognize text from image using Aspose OCR in C#. Learn how to load
    image for OCR, set OCR language, create OCR engine and extract text from TIFF.
  headline: recognize text from image with Aspose OCR – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Remove the `GpuDevice` line; the engine will automatically switch to CPU
      mode. Performance will be slower but the results remain accurate.
    question: What if my GPU isn’t detected?
  - answer: Absolutely—`Image.FromFile` works with any format supported by System.Drawing,
      so you can **load image for OCR** regardless of extension.
    question: Can I process PNG or JPEG files?
  - answer: Increase `ocrEngine.PreprocessOptions.Dpi` before calling `Recognize`.
      Higher DPI gives the engine more pixels to work with, improving accuracy.
    question: How do I handle low‑resolution scans?
  - answer: The `GpuMemoryLimit` property caps GPU usage. If you hit the limit, the
      engine will fallback to CPU for the remaining pages.
    question: Is there a limit to the size of the TIFF?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
- Text Extraction
title: Распознавание текста с изображения с помощью Aspose OCR – Полное руководство
  по C#
url: /ru/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание текста с изображения с помощью Aspose OCR – Полное руководство на C#

Когда‑то вам нужно **распознать текст с изображения**, но вы не знали, какая библиотека обеспечит и скорость, и точность? Вы не одиноки. Во многих проектах по обработке счетов или архивированию главная боль — получить чистый, индексируемый текст из TIFF‑файлов без написания собственного парсера.

Дело в том, что Aspose OCR for .NET делает весь этот конвейер простым как раз. В этом руководстве мы пройдёмся по всему, что нужно — установке пакета, **созданию OCR‑движка**, загрузке TIFF, установке языка OCR и, наконец, **извлечению текста из TIFF**. К концу вы получите готовое консольное приложение, которое может **распознавать текст с изображения** мгновенно.

## Требования

- .NET 6.0 или новее (код работает и с .NET Core, и с .NET Framework)
- Visual Studio 2022 (или любая другая IDE)
- NuGet‑пакет Aspose.OCR (для поддержки GPU требуется дополнение `Aspose.OCR.Gpu`)
- GPU с поддержкой CUDA, если хотите дополнительную скорость (необязательно, но рекомендуется)

> **Pro tip:** Если у вас нет GPU, просто уберите строку `GpuDevice`, и движок автоматически переключится на CPU.

## Шаг 1: Установить Aspose OCR и создать OCR‑движок

Сначала добавьте необходимые пакеты через NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu   # optional GPU support
```

Теперь мы можем **создать OCR‑движок**. Этот объект — сердце процесса; в нём хранится конфигурация, такая как устройство выполнения и ограничения памяти.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU support
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine (GPU‑enabled)
        var ocrEngine = new OcrEngine
        {
            // 0 = first GPU in the system; change if you have multiple cards
            GpuDevice = new GpuDevice(0),
            // Optional: cap GPU memory usage to 1024 MB
            GpuMemoryLimit = 1024
        };
```

**Почему это важно:** Привязав движок к GPU, вы резко сокращаете время, необходимое для **распознавания текста с изображения**, особенно при обработке больших пакетов высокоразрешённых TIFF‑файлов.

## Шаг 2: Загрузить изображение для OCR

Далее нам нужно **загрузить изображение для OCR**. Aspose.OCR работает с `System.Drawing.Image`, поэтому любой формат, поддерживаемый GDI+ (включая многостраничный TIFF), подходит.

```csharp
        // Step 2: Load the image you want to process
        // Replace the path with the location of your TIFF file
        var imagePath = @"C:\Invoices\invoice_batch.tif";
        Image image = Image.FromFile(imagePath);
```

Если вы работаете с многостраничным TIFF, можете перебрать страницы с помощью `image.SelectActiveFrame`, но в большинстве случаев достаточно одного вызова.

## Шаг 3: Установить язык OCR

Движок не знает, на каком языке вы сканируете, автоматически. **Установите язык OCR** перед запуском распознавания; иначе вы получите кучу искажённого вывода.

```csharp
        // Step 3: Tell the engine which language to expect
        ocrEngine.Language = OcrLanguage.English; // change to .German, .French, etc. as needed
```

> **Did you know?** Переключение языков во время выполнения дешево — вы даже можете обработать документ с несколькими языками, меняя это свойство между страницами.

## Шаг 4: Выполнить распознавание – распознать текст с изображения

Теперь самая интересная часть: действительно **распознать текст с изображения**. Метод `Recognize` возвращает обычную строку со всеми найденными символами.

```csharp
        // Step 4: Run OCR and capture the output
        string recognizedText = ocrEngine.Recognize(image);
```

Если нужны оценки уверенности или ограничивающие рамки, можно использовать перегрузку, возвращающую объект `OcrResult`, но для большинства задач извлечения достаточно простой строки.

## Шаг 5: Извлечь текст из TIFF (и обработать многостраничные файлы)

Когда источник — TIFF, содержащий несколько страниц, вам придётся повторять шаги 2‑4 для каждого кадра. Ниже быстрый цикл, который **извлекает текст из TIFF** постранично:

```csharp
        // Optional: process multi‑page TIFFs
        var totalFrames = image.GetFrameCount(FrameDimension.Page);
        for (int i = 0; i < totalFrames; i++)
        {
            image.SelectActiveFrame(FrameDimension.Page, i);
            string pageText = ocrEngine.Recognize(image);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
```

Код выше выводит извлечённый текст для каждой страницы, что упрощает передачу результатов в базу данных или поисковый индекс.

## Шаг 6: Отобразить или сохранить извлечённый текст

Наконец, **отобразим извлечённый текст** и, при желании, запишем его в файл для дальнейшей обработки.

```csharp
        // Step 6: Output the result to console
        Console.WriteLine("=== Full OCR Result ===");
        Console.WriteLine(recognizedText);

        // Optional: Save to a .txt file
        System.IO.File.WriteAllText(@"C:\Invoices\extracted_text.txt", recognizedText);
    }
}
```

Запуск программы должен вывести распознанные символы и создать `extracted_text.txt` рядом с исходным TIFF.

---

## Часто задаваемые вопросы и особые случаи

- **Что делать, если мой GPU не обнаружен?**  
  Удалите строку `GpuDevice`; движок автоматически переключится в режим CPU. Производительность будет ниже, но результаты останутся точными.

- **Можно ли обрабатывать PNG или JPEG?**  
  Конечно — `Image.FromFile` работает с любым форматом, поддерживаемым System.Drawing, так что вы можете **загрузить изображение для OCR** независимо от расширения.

- **Как работать с низкокачественными сканами?**  
  Увеличьте `ocrEngine.PreprocessOptions.Dpi` перед вызовом `Recognize`. Более высокий DPI даёт движку больше пикселей для анализа, повышая точность.

- **Есть ли ограничение на размер TIFF?**  
  Свойство `GpuMemoryLimit` ограничивает использование GPU. Если лимит будет превышен, движок переключится на CPU для оставшихся страниц.

---

## Заключение

Теперь у вас есть полностью готовый, готовый к продакшену фрагмент кода, который **распознаёт текст с изображения** с помощью Aspose OCR в C#. В руководстве рассмотрены создание OCR‑движка, **загрузка изображения для OCR**, **установка языка OCR** и **извлечение текста из TIFF** — всё с использованием ускорения GPU для повышения скорости.  

Дальше вы можете:

- Поэкспериментировать с разными языками (`OcrLanguage.Spanish`, `OcrLanguage.ChineseSimplified` и т.д.).
- Интегрировать вывод в индексируемый ElasticSearch.
- Добавить постобработку (проверка орфографии, очистка с помощью regex) для улучшения качества данных.

Попробуйте на своей партии счетов, поиграйте с ограничениями памяти и наблюдайте, как растёт производительность OCR. Приятного кодинга!

## Похожие руководства

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}