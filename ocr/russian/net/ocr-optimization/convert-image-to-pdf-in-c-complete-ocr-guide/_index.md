---
category: general
date: 2026-09-13
description: Узнайте, как преобразовать отсканированную страницу в PDF на C# с использованием
  Aspose OCR. Это руководство показывает image preprocessing, распознавание Korean
  текста и создание searchable PDF.
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Узнайте, как преобразовать отсканированную страницу в PDF на C# с
  Aspose OCR. Учебник охватывает image preprocessing, GPU‑accelerated OCR для Korean
  текста и генерацию searchable PDF за несколько минут.
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: Как преобразовать отсканированную страницу в PDF на C# с OCR
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: Как преобразовать отсканированную страницу в PDF на C# с OCR
url: /ru/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как преобразовать отсканированную страницу в PDF на C# с OCR

Если вам нужно **преобразовать отсканированную страницу в PDF**, сохранив возможность поиска текста, вы попали по адресу. В этом руководстве мы покажем, как использовать Aspose OCR для **preprocess image for OCR**, **recognize Korean text image**, и, наконец, **create searchable PDF image** — всё из простого консольного приложения C#.

## Быстрые ответы
- **Какая библиотека обрабатывает OCR?** Aspose.OCR for .NET  
- **Можно ли использовать GPU?** Да — включите ускорение GPU для обработки до 2× быстрее  
- **Нужен ли мне пакет корейского языка?** Он загружается автоматически при первом использовании  
- **Будет ли результат доступен для поиска?** Сгенерированный PDF содержит невидимый текстовый слой  
- **Какие версии .NET поддерживаются?** .NET 6.0 и новее (включая .NET Core и .NET Framework)

## Требования

- **.NET 6.0 или новее** — работает на .NET Core, .NET Framework и .NET 5/6+  
- **Aspose.OCR for .NET** пакет NuGet (`Aspose.OCR`) — пробные ключи бесплатны на сайте Aspose  
- Пример изображения с корейскими символами, например `korean_book_page.jpg`  
- Ваш любимый IDE (Visual Studio 2022, VS Code, Rider и т.д.)

> **Полезный совет:** Храните изображения в папке `Resources/`, чтобы пути оставались одинаковыми на разных машинах.

## Обзор процесса

1. Инициализировать OCR‑движок с поддержкой GPU.  
2. Добавить фильтры **preprocess image for OCR**, такие как выравнивание (deskew) и подавление шума (denoise).  
3. Скачать и загрузить корейскую языковую модель (обрабатывается автоматически).  
4. Запустить OCR на изображении.  
5. Экспортировать результат с помощью **SearchablePdfExporter** для **create searchable PDF image**.  
6. (Опционально) Сериализовать вывод OCR в JSON для последующих конвейеров.

Ниже мы подробно рассмотрим каждый шаг, объясним *почему* он важен и предоставим точный код, который вы можете скопировать‑вставить.

## Как работает преобразование отсканированной страницы в PDF?

`OcrEngine` — основной класс в Aspose.OCR, выполняющий оптическое распознавание символов на изображениях.  
`SearchablePdfExporter` создаёт PDF, содержащий оригинальное изображение и невидимый текстовый слой для поиска.  
`RecognitionResult` хранит текст и данные о достоверности, возвращённые OCR‑движком.

Загрузите изображение с помощью `new OcrEngine()` и вызовите `engine.Recognize("korean_book_page.jpg")`, затем передайте `RecognitionResult` в `SearchablePdfExporter.Export`. Этот двухшаговый процесс считывает битмап, извлекает Unicode‑текст и встраивает оба элемента в один PDF, где текстовый слой невидим, но доступен для поиска. GPU‑ускорение сокращает время распознавания примерно вдвое, а фильтры выравнивания и подавления шума повышают точность до 15 % на шумных сканах.

## Преобразование изображения в PDF — полный рабочий процесс

Следующий фрагмент представляет *полную* программу. Создайте новый консольный проект (`dotnet new console -n OcrPdfDemo`) и замените автоматически сгенерированный `Program.cs` кодом, показанным в заполнителе.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### Почему это работает

- **GPU‑ускорение** сокращает время распознавания примерно вдвое по сравнению с режимом только CPU.  
- **Deskew** и **Denoise** — классические техники *preprocess image for OCR*; они исправляют типичные дефекты сканирования, которые иначе приводят к пропуску символов движком.  
- **Загрузка языковой модели** необходима для **recognize Korean text image** — без корейской модели движок будет использовать общий латинский алфавит и выдавать мусор.  
- **SearchablePdfExporter** объединяет оригинальный битмап и невидимый текстовый слой, предоставляя результат **create searchable pdf image**, который можно индексировать в любом PDF‑просмотрщике.

## Почему это работает

- **GPU‑ускорение** сокращает время распознавания примерно вдвое по сравнению с режимом только CPU.  
- **Deskew** и **Denoise** — классические техники *preprocess image for OCR*; они исправляют типичные дефекты сканирования, которые иначе приводят к пропуску символов движком.  
- **Загрузка языковой модели** необходима для **recognize Korean text image** — без корейской модели движок будет использовать общий латинский алфавит и выдавать мусор.  
- **SearchablePdfExporter** объединяет оригинальный битмап и невидимый текстовый слой, предоставляя результат **create searchable pdf image**, который можно индексировать в любом PDF‑просмотрщике.

## Предобработка изображения для OCR — советы и приёмы

`DeskewFilter` исправляет вращение отсканированных страниц.  
`ContrastFilter` регулирует контраст изображения для повышения точности OCR.  
`BinarizationFilter` преобразует изображение в чёрно‑белое на основе порога, уменьшая фоновой шум.  
`OrientationFilter` обнаруживает и исправляет смешанные портретные и альбомные страницы.  

| Проблема | Дополнительный фильтр | Как добавить |
|----------|----------------------|--------------|
| Низкий контраст | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Сильный фоновой шум | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Смешанная ориентация (портрет и альбом) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Примечание:** Добавление слишком большого количества фильтров может замедлить обработку. Тестируйте каждое изменение на одной странице перед масштабированием.

## Распознавание корейского текста на изображении — распространённые подводные камни

Корейские скрипты содержат слоги Hangul, которые визуально плотные. Если вы замечаете искажённый вывод:

1. **Убедитесь, что языковая модель полностью загружена** — проверьте консоль на наличие сообщения вроде “Downloading Korean model…”.  
2. **Увеличьте `MaxAngle`** в `DeskewFilter`, если ваши сканы повернуты более чем на 12°.  
3. **Увеличьте память GPU**, задав `ocrEngine.GpuMemoryLimit = 2048;` (значение в МБ).  

`LanguageModel.Korean` загружает корейские языковые данные для OCR, обеспечивая точное распознавание Hangul.  

Эти настройки напрямую влияют на успех **recognize Korean text image**.

## Создание поискового PDF‑изображения — проверка результата

После завершения программы откройте `korean_page.pdf` в любом PDF‑просмотрщике (Adobe Acrobat Reader, Foxit, даже Chrome). Вы должны иметь возможность:

- **Выделять текст** мышью так же, как в нативном PDF.  
- **Искать** корейские слова с помощью встроенного поля поиска.  

Если текстовый слой пуст, проверьте, что метод `Export` получил правильный путь к изображению и что результат OCR содержит непустой `RecognitionResult.Text`.

## Полный JSON‑вывод — чего ожидать

Консоль выводит красиво отформатированный JSON‑payload. Обрезанный пример выглядит так:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## Устранение неполадок и FAQ

**Q: My PDF is huge compared to the original image.**  
**A:** Экспортер встраивает оригинальный битмап в его нативном разрешении. Если размер важен, уменьшите изображение *до* распознавания:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: The OCR returns empty strings.**  
**A:** Убедитесь, что путь к изображению правильный и файл не повреждён. Также проверьте, что драйвер GPU обновлён; старые драйверы могут вызывать тихие сбои.

**Q: Can I process multiple pages in a loop?**  
**A:** Конечно. Оберните шаги 4‑6 в цикл `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` и измените путь вывода PDF соответственно.

## Заключение

Мы только что **преобразовали изображение в PDF**, сохранив поисковый текст, благодаря мощному конвейеру Aspose OCR. Выполняя **preprocess image for OCR**, вы повышаете точность; используя **recognize Korean text image**, вы работаете со сложными скриптами; а применяя **create searchable pdf image**, получаете портативный, индексируемый документ.

Скачайте код, укажите свои сканы и экспериментируйте с дополнительными фильтрами или языковыми моделями. Та же схема работает для китайского, японского или любого языка на основе латиницы — просто замените `LanguageModel.Korean` на соответствующий enum.

Есть дополнительные вопросы? Оставьте комментарий, и удачной разработки!

---

**Последнее обновление:** 2026-09-13  
**Тестировано с:** Aspose.OCR 24.11 for .NET  
**Автор:** Aspose

## Связанные руководства

- [Создать поисковый PDF из отсканированных файлов с использованием Aspose Ocr](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [Конвейер предобработки OCR: как распознать текст с изображения](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Распознать текст с изображения с помощью Aspose Ocr: полное руководство C](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}