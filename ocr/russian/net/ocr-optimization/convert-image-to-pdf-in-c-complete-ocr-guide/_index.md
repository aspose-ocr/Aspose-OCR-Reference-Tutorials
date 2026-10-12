---
category: general
date: 2025-12-30
description: Конвертировать изображение в PDF с помощью Aspose OCR на C#. Узнайте,
  как предварительно обработать изображение для OCR, распознать корейский текст на
  изображении и быстро создать поисковый PDF‑изображение.
draft: false
keywords:
- convert image to pdf
- preprocess image for ocr
- recognize korean text image
- create searchable pdf image
language: ru
og_description: Конвертировать изображение в PDF с помощью Aspose OCR. Этот учебник
  показывает, как предварительно обработать изображение для OCR, распознать корейский
  текст на изображении и создать PDF с возможностью поиска.
og_title: Преобразовать изображение в PDF на C# – Полное руководство по OCR
tags:
- C#
- OCR
- Aspose
- PDF
title: Преобразовать изображение в PDF на C# – Полное руководство по OCR
url: /ru/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование изображения в PDF на C# – Полное руководство по OCR

Когда‑нибудь вам нужно было **convert image to PDF**, но также хотелось, чтобы текст внутри был доступен для поиска? Вы не одиноки. Многие разработчики сталкиваются с тем же самым при работе со сканированными страницами, особенно написанными на корейском. Хорошая новость в том, что с Aspose OCR вы можете **preprocess image for OCR**, **recognize Korean text image**, и наконец **create searchable PDF image** всего в нескольких строках.

В этом руководстве мы пройдем весь конвейер — от загрузки исходного JPEG‑файла страницы корейской книги, очистки его, извлечения текста и упаковки всего в поисковый PDF. К концу вы получите готовое к запуску консольное приложение C#, которое можно добавить в любой проект .NET.

## Что понадобится

- **.NET 6.0 or later** (код работает как на .NET Core, так и на .NET Framework)  
- **Aspose.OCR for .NET** NuGet package (`Aspose.OCR`) – бесплатные пробные ключи доступны на сайте Aspose.  
- Пример изображения, содержащего корейский текст (например, `korean_book_page.jpg`).  
- Среда разработки по вашему выбору (Visual Studio, VS Code, Rider — я использую VS 2022).

> **Pro tip:** Храните файлы изображений в отдельной папке, например `Resources/`, чтобы путь оставался одинаковым на разных машинах.

## Обзор процесса

1. **Initialize the OCR engine** с поддержкой GPU для ускорения.  
2. **Add preprocessing filters** (deskew, denoise) для повышения точности распознавания.  
3. **Download and load the Korean language model** – Aspose делает это автоматически при необходимости.  
4. **Run the recognition** на входном изображении.  
5. **Export the result as a searchable PDF** с помощью встроенного экспортера.  
6. **Optionally, serialize the result to JSON** для дальнейшего анализа или логирования.

Ниже мы разберём каждый шаг, объясним *почему* он важен и предоставим точный код, который можно скопировать‑вставить.

---

## ## Преобразование изображения в PDF – Полный рабочий процесс

Следующий фрагмент — *полная* программа. Не стесняйтесь создать новый консольный проект (`dotnet new console -n OcrPdfDemo`) и заменить автоматически сгенерированный `Program.cs` этим кодом.

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

- **GPU acceleration** сокращает время распознавания примерно вдвое по сравнению с режимом только CPU.  
- **Deskew** и **Denoise** — классические техники *preprocess image for OCR*; они исправляют типичные дефекты сканирования, которые иначе заставляют движок пропускать символы.  
- **Language model loading** необходима для **recognize Korean text image** – без корейской модели движок переходит к общему латинскому алфавиту и выдаёт мусор.  
- **SearchablePdfExporter** объединяет оригинальный bitmap и невидимый текстовый слой, предоставляя результат **create searchable pdf image**, который можно индексировать в любом PDF‑просмотрщике.

---

## ## Предобработка изображения для OCR – Советы и приёмы

Хотя два добавленных фильтра обычно достаточны, вы можете столкнуться с упорными изображениями. Вот несколько дополнительных шагов, которые можно попробовать:

| Проблема | Дополнительный фильтр | Как добавить |
|-------|-------------------|------------|
| Низкий контраст | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Сильный шум фона | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Смешанная ориентация (портрет & ландшафт) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Note:** Добавление слишком большого количества фильтров может замедлить обработку. Тестируйте каждое изменение на одной странице перед масштабированием.

---

## ## Распознавание корейского текста на изображении – Распространённые подводные камни

Корейские скрипты содержат слоги Хангыль, которые визуально плотные. Если вы замечаете искажённый вывод:

1. **Ensure the language model is fully downloaded** – проверьте консоль на наличие сообщения вроде “Downloading Korean model…”.  
2. **Increase the `MaxAngle`** в `DeskewFilter`, если ваши сканы повернуты более чем на 12°.  
3. **Boost GPU memory** установив `ocrEngine.GpuMemoryLimit = 2048;` (значение в МБ).

Эти настройки напрямую влияют на успешность **recognize Korean text image**.

---

## ## Создание поискового PDF изображения – Проверка результата

После завершения программы откройте `korean_page.pdf` в любом PDF‑просмотрщике (Adobe Acrobat Reader, Foxit, даже Chrome). Вы должны иметь возможность:

- **Select text** мышью, как если бы это был нативный PDF.  
- **Search** корейские слова, используя встроенную строку поиска.

Если слой текста пустой, дважды проверьте, что метод `Export` получил правильный путь к изображению и что результат OCR содержит непустой `RecognitionResult.Text`.

---

## ## Полный JSON‑вывод – Что ожидать

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

---

## ## Устранение неполадок и FAQ

**Q: Мой PDF огромный по сравнению с оригинальным изображением.**  
A: Экспортер встраивает оригинальный bitmap в его нативном разрешении. Если размер важен, уменьшите изображение *до* распознавания:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: OCR возвращает пустые строки.**  
A: Убедитесь, что путь к изображению правильный и файл не повреждён. Также проверьте, что драйвер GPU обновлён; старые драйверы могут вызывать тихие сбои.

**Q: Можно ли обрабатывать несколько страниц в цикле?**  
A: Конечно. Оберните шаги 4‑6 в цикл `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` и измените путь к выходному PDF соответственно.

---

## ## Заключение

Мы только что **converted image to PDF**, сохранив поисковый текст, благодаря мощному конвейеру Aspose OCR. Путём **preprocess image for OCR** вы повышаете точность; **recognize Korean text image** позволяет работать со сложными скриптами; а **create searchable pdf image** даёт портативный, индексируемый документ.

Скачайте код, укажите свои сканы и экспериментируйте с дополнительными фильтрами или языковыми моделями. Та же схема работает для китайского, японского или любого языка на основе латиницы — просто замените `LanguageModel.Korean` на соответствующий enum.

Есть ещё вопросы? Оставьте комментарий, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}