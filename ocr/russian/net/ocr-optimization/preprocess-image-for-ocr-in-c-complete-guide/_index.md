---
category: general
date: 2026-06-16
description: Подготовьте изображение для OCR с помощью Aspose OCR в C#. Узнайте, как
  улучшить контраст изображения и удалить шум со сканированного изображения для точного
  извлечения текста.
draft: false
keywords:
- preprocess image for OCR
- enhance image contrast
- remove noise from scanned image
language: ru
og_description: Предобрабатывайте изображение для OCR с помощью Aspose OCR. Повышайте
  точность, улучшая контраст изображения и удаляя шум со сканированного изображения.
og_title: Предобработка изображения для OCR в C# – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Preprocess image for OCR using Aspose OCR in C#. Learn to enhance image
    contrast and remove noise from scanned image for accurate text extraction.
  headline: Preprocess Image for OCR in C# – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR using Aspose OCR in C#. Learn to enhance image
    contrast and remove noise from scanned image for accurate text extraction.
  name: Preprocess Image for OCR in C# – Complete Guide
  steps:
  - name: '**Heavy Salt‑and‑Pepper Noise** – Increase the aggressiveness of `DenoiseFilter`
      by passing a custom `DenoiseOptions` object (e.g., `new DenoiseFilter(new DenoiseOptions
      { Strength = 2 })`).'
    text: '**Heavy Salt‑and‑Pepper Noise** – Increase the aggressiveness of `DenoiseFilter`
      by passing a custom `DenoiseOptions` object (e.g., `new DenoiseFilter(new DenoiseOptions
      { Strength = 2 })`).'
  - name: '**Faded Ink on Yellow Paper** – Pair `ContrastEnhanceFilter` with a `BrightnessAdjustFilter`
      to lift the background tone before boosting contrast.'
    text: '**Faded Ink on Yellow Paper** – Pair `ContrastEnhanceFilter` with a `BrightnessAdjustFilter`
      to lift the background tone before boosting contrast.'
  - name: '**Colored Text** – Convert the image to grayscale first (`new GrayscaleFilter()`)
      because most OCR engines, including Aspose, work best on single‑channel data.'
    text: '**Colored Text** – Convert the image to grayscale first (`new GrayscaleFilter()`)
      because most OCR engines, including Aspose, work best on single‑channel data.'
  - name: '**Build** the console project (`dotnet build`).'
    text: '**Build** the console project (`dotnet build`).'
  - name: '**Run** (`dotnet run`). You should see something like:'
    text: '**Run** (`dotnet run`). You should see something like:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
title: Предобработка изображения для OCR в C# – Полное руководство
url: /ru/net/ocr-optimization/preprocess-image-for-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Предобработка изображения для OCR в C# – Полное руководство

Когда‑то задумывались, почему результаты OCR выглядят как набор бессвязных символов, хотя исходное фото довольно чёткое? На самом деле большинство OCR‑движков, включая Aspose OCR, ожидают чистое, правильно выровненное изображение. **Предобработка изображения для OCR** — первый шаг, превращающий смазанную, низкоконтрастную скан‑копию в чёткий, машинно‑читаемый текст.

В этом руководстве мы пройдём практический пример от начала до конца, который не только **предобрабатывает изображение для OCR**, но и показывает, как **повысить контраст изображения** и **удалить шум со сканированного изображения** с помощью встроенных фильтров Aspose. К концу вы получите готовое консольное приложение C#, которое обеспечивает гораздо более надёжные результаты распознавания.

---

## What You’ll Need

- **.NET 6.0 или новее** (код также работает с .NET Framework 4.6+)  
- **Aspose.OCR for .NET** – можно установить пакет NuGet `Aspose.OCR`  
- Пример изображения, страдающего от шума, наклона или плохого контраста (в демонстрации используется `skewed-photo.jpg`)  
- Любая удобная IDE – Visual Studio, Rider или VS Code подойдёт  

Никаких дополнительных нативных библиотек или сложных установок не требуется; всё находится внутри пакета Aspose.

---

## ## Preprocess Image for OCR – Step‑by‑Step Implementation

Ниже полный исходный файл, который нужно собрать. Скопируйте‑вставьте его в новый консольный проект и нажмите **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2: Add preprocessing filters to improve recognition.
        // 2a – Remove noise from scanned image.
        ocrEngine.Settings.Filters.Add(new DenoiseFilter()); // Reduces random speckles.
        // 2b – Correct skew (deskew) that often appears in photographed documents.
        ocrEngine.Settings.Filters.Add(new DeskewFilter()); // Straightens the baseline.
        // 2c – Enhance image contrast for better character separation.
        ocrEngine.Settings.Filters.Add(new ContrastEnhanceFilter()); // Boosts contrast.

        // Step 3: (Optional) Rotate the image if it was captured at an angle.
        // Negative values rotate clockwise, positive counter‑clockwise.
        ocrEngine.Settings.Filters.Add(new RotateFilter(-3)); // Small correction.

        // Step 4: Perform OCR on the image file.
        // Replace the path with the actual location of your test image.
        string extractedText = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed-photo.jpg");

        // Step 5: Display the recognized text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

### Почему каждый фильтр важен

| Filter | Что делает | Почему это помогает OCR |
|--------|------------|--------------------------|
| **DenoiseFilter** | Удаляет случайный пиксельный шум, часто появляющийся при съёмке при плохом освещении. | Шум может восприниматься как фрагменты глифов, искажая формы символов. |
| **DeskewFilter** | Определяет доминирующий угол строки текста и вращает изображение до 0°. | Наклонённые базовые линии заставляют OCR‑движок считать символы наклонёнными, что приводит к ошибкам распознавания. |
| **ContrastEnhanceFilter** | Увеличивает разницу между тёмным текстом и светлым фоном. | Более высокий контраст улучшает бинаризацию, используемую в большинстве OCR‑конвейеров. |
| **RotateFilter** (optional) | Применяет вручную заданный угол вращения. | Полезно, когда автоматическое исправление наклона недостаточно, например, при съёмке под небольшим углом. |

> **Pro tip:** Если ваш источник – отсканированный PDF, сначала экспортируйте страницу как изображение (например, с помощью `PdfRenderer`), а затем передайте её в ту же цепочку фильтров. Та же логика предобработки применима.

---

## ## Enhance Image Contrast Before OCR – Visual Confirmation

Один фильтр добавить — это одно, а увидеть результат — другое. Ниже простая иллюстрация «до‑и‑после» (замените её своими скриншотами при тестировании).

![Diagram of preprocess image for OCR pipeline](image.png){alt="Диаграмма конвейера предварительной обработки изображения для OCR"}

Слева показан сырой, шумный скан, справа — то же изображение после **повышения контраста**, **удаления шума со сканированного изображения** и исправления наклона. Обратите внимание, как символы становятся чёткими и изолированными — именно то, что требуется OCR‑движку.

---

## ## Remove Noise from Scanned Image – Edge Cases & Tips

Не каждый документ страдает от одного и того же типа шума. Ниже несколько сценариев и рекомендации по настройке конвейера:

1. **Сильный «соль‑и‑перец» шум** – Увеличьте агрессивность `DenoiseFilter`, передав пользовательский объект `DenoiseOptions` (например, `new DenoiseFilter(new DenoiseOptions { Strength = 2 })`).  
2. **Блеклая чернила на жёлтой бумаге** – Сочетайте `ContrastEnhanceFilter` с `BrightnessAdjustFilter`, чтобы сначала осветлить фон, а затем усилить контраст.  
3. **Цветной текст** – Сначала преобразуйте изображение в градации серого (`new GrayscaleFilter()`), потому что большинство OCR‑движков, включая Aspose, работают лучше с одно‑канальными данными.  

Порядок применения фильтров тоже имеет значение. На практике я ставлю `DenoiseFilter` **перед** `DeskewFilter`, так как более чистое изображение даёт алгоритму исправления наклона более надёжные данные о краях.

---

## ## Running the Demo & Verifying Output

1. **Соберите** консольный проект (`dotnet build`).  
2. **Запустите** (`dotnet run`). Вы должны увидеть что‑то вроде:

```
=== OCR RESULT ===
The quick brown fox jumps over the lazy dog.
```

Если вывод всё ещё содержит «мусорные» символы, проверьте правильность пути к изображению и убедитесь, что исходный файл не имеет слишком низкого разрешения (рекомендовано минимум 300 dpi для большинства задач OCR).

---

## Conclusion

Теперь у вас есть надёжный, готовый к продакшну шаблон для **предобработки изображения для OCR** в C#. С помощью цепочки `DenoiseFilter`, `DeskewFilter` и `ContrastEnhanceFilter` от Aspose — и при необходимости `RotateFilter` — вы можете **повысить контраст изображения**, **удалить шум со сканированного изображения** и значительно улучшить точность последующего извлечения текста.

Что дальше? Попробуйте передать очищенное изображение в другие пост‑обработки, такие как проверка орфографии, определение языка или передача сырого текста в конвейер обработки естественного языка. Вы также можете изучить `BinarizationFilter` от Aspose для бинарных рабочих процессов или переключиться на другой OCR‑движок (Tesseract, Microsoft OCR), используя ту же цепочку предобработки.

Есть сложное изображение, которое всё ещё отказывается работать? Оставьте комментарий, и мы разберёмся вместе. Приятного кодинга, и пусть ваши результаты OCR будут кристально чистыми!

## What Should You Learn Next?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}