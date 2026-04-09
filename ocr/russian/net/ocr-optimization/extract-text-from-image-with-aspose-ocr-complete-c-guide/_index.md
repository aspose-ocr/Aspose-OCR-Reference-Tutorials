---
category: general
date: 2026-04-08
description: Извлечение текста из изображения с помощью Aspose OCR в C#. Узнайте,
  как предварительно обрабатывать изображение для OCR и как предобрабатывать изображение,
  чтобы повысить точность.
draft: false
keywords:
- extract text from image
- preprocess image for ocr
- how to preprocess image
- Aspose OCR C#
- image preprocessing techniques
language: ru
og_description: Извлечение текста из изображения с помощью Aspose OCR в C#. Это руководство
  показывает, как предварительно обработать изображение для OCR и как подготовить
  его для получения наилучших результатов.
og_title: Извлечение текста из изображения с помощью Aspose OCR – Полное руководство
  по C#
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Извлечение текста из изображения с помощью Aspose OCR – Полное руководство
  по C#
url: /ru/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения с помощью Aspose OCR – Полное руководство на C#

Когда‑то вам нужно **извлечь текст из изображения**, но результаты полны ошибок? Вы не одиноки — большинство разработчиков сталкиваются с этой проблемой, когда исходная картинка наклонена, зашумлена или имеет низкий контраст. Хорошая новость в том, что небольшая предобработка может превратить дрожащий снимок в чистый источник для OCR, а Aspose OCR делает всё это простым делом.

В этом руководстве мы пройдём реальный пример, показывающий **как предобрабатывать изображение для OCR** с помощью встроенных фильтров Aspose OCR, а затем **извлечём текст из изображения** всего несколькими строками C#. К концу вы получите готовую к запуску программу, поймёте, зачем нужен каждый фильтр, и узнаете, как настроить конвейер под свои особые случаи.

## Что понадобится

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+)
- Пакет NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Пример изображения, которое наклонено, зашумлено или имеет низкий контраст (например, `skewed_noisy.jpg`)
- Любая IDE — Visual Studio, Rider или VS Code подойдёт

Никаких дополнительных нативных библиотек, никаких веб‑сервисов, только чистый C#.

## Шаг 1: Настройка OCR‑движка – отправная точка для извлечения текста

Первым делом создаём экземпляр `OcrEngine` и указываем, какой язык искать. Английский — самый распространённый, но вы можете заменить `"en"` на `"fr"`, `"de"` и т.д.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void PreprocessAndOcr()
    {
        // 1️⃣ Initialize the OCR engine – this is where we define the language.
        var ocrEngine = new OcrEngine { Language = "en" };
```

**Почему это важно:** Движок хранит внутренние словари и языковые эвристики. Если не задать язык явно, Aspose по умолчанию использует английский, но явное указание избавляет от неожиданностей при переключении локали.

## Шаг 2: Сборка конвейера предобработки – как предобрабатывать изображение для лучших результатов

Теперь добавляем фильтры. Представьте их как мини‑фото‑редактор, который запускается автоматически перед шагом OCR. Три фильтра ниже покрывают самые распространённые проблемы:

| Фильтр | Что исправляет | Когда использовать |
|--------|----------------|---------------------|
| `DeskewFilter` | Поворачивает изображение обратно в горизонтальное положение | Снимки, сделанные под углом |
| `DenoiseFilter` | Уменьшает случайные пятна и зернистость | Снимки при плохом освещении или отсканированные документы |
| `ContrastStretchFilter` | Усиливает контраст, делая тёмный текст более заметным | Выцветшие отпечатки или «размытые» скриншоты |

```csharp
        // 2️⃣ Add preprocessing steps – this is the core of “how to preprocess image”.
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast
```

**Совет:** Порядок имеет значение. Сначала Deskew, затем Denoise, и в конце ContrastStretch. Если поменять их местами, вы можете усилить шум вместо того, чтобы убрать его.

## Шаг 3: Запуск OCR – наконец извлекаем текст из изображения

Когда конвейер готов, передаём движку путь к вашему файлу. Aspose автоматически применит фильтры, а затем запустит алгоритм распознавания.

```csharp
        // 3️⃣ Recognize text from the pre‑processed image.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Если файл не найден, вы получите чёткое `FileNotFoundException`. Поэтому мы советуем использовать абсолютные пути во время разработки, а затем переключаться на относительные пути или значения из конфигурации в продакшене.

## Шаг 4: Вывод результата – смотрим, что получилось

Объект `OcrResult` содержит «сырой» текст, оценки уверенности и даже ограничивающие рамки каждого слова. Для быстрой демонстрации просто выведем текст в консоль.

```csharp
        // 4️⃣ Output the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

При запуске программы вы должны увидеть что‑то вроде:

```
=== OCR Output ===
Invoice Number: 2023-0456
Date: 03/15/2024
Total: $1,234.56
```

Если вывод выглядит «мусором», проверьте качество изображения или поэкспериментируйте с дополнительными фильтрами (например, `BinarizationFilter` для бинарных изображений).

## Полный рабочий пример – скопируйте, вставьте и запустите

Ниже полностью самодостаточная программа. Просто замените `YOUR_DIRECTORY/skewed_noisy.jpg` на реальный путь к вашему тестовому изображению.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void Main()
    {
        PreprocessAndOcr();
    }

    public static void PreprocessAndOcr()
    {
        // Step 1: Create OCR engine and set language
        var ocrEngine = new OcrEngine { Language = "en" };

        // Step 2: Build preprocessing pipeline
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast

        // Step 3: Recognize text from the pre‑processed image
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // Step 4: Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Ожидаемый вывод** — консоль напечатает текстовое представление того, что находится на изображении. Если на картинке простой знак «OpenAI», вы увидите именно это слово без лишних символов.

## Пограничные случаи и настройка конвейера

### 1️⃣ Очень тёмные изображения

Если фильтра контраста недостаточно, добавьте перед ним `BrightnessCorrectionFilter`:

```csharp
ocrEngine.Preprocess.Add(new BrightnessCorrectionFilter(30)); // increase brightness by 30%
```

### 2️⃣ Документы на нескольких языках

Установите `Language = "en+fr"` (Aspose поддерживает коды языков, разделённые запятыми) и добавьте `LanguageDetectionFilter`, если хотите, чтобы движок автоматически определял язык.

### 3️⃣ Большие PDF, преобразованные в изображения

Обрабатывать PDF‑документ в тысячу страниц по одной картинке может быть медленно. Используйте `Parallel.ForEach` для одновременного распознавания нескольких изображений, но помните, что `OcrEngine` не потокобезопасен — создавайте отдельный экземпляр на каждый поток.

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine { Language = "en" };
    // add same filters...
    var result = engine.RecognizeImage(path);
    // store result...
});
```

### 4️⃣ Получение ограничивающих рамок

Если нужны координаты каждого слова (например, для подсветки), изучите `ocrResult.Regions`. Каждый регион содержит координаты `Rectangle`, которые можно передать в UI‑оверлей.

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

## Распространённые подводные камни (и как их избежать)

- **Пропуск шага Deskew** — даже наклон в 2 градуса может снизить уверенность на 20 %. Всегда добавляйте `DeskewFilter`, если источник не идеально выровнен.
- **Использование JPEG с сильным сжатием** — артефакты сжатия выглядят как шум; переключитесь на PNG или TIFF для лучшего OCR.
- **Жёстко закодированные пути** — относительные пути работают локально, но в CI/CD‑конвейерах лучше читать расположение изображения из конфигурации или переменных окружения.

## Тестирование вашей настройки

1. Запустите программу с чистым, высококонтрастным изображением. Вы должны получить почти идеальный текст.
2. Подмените его шумным, наклонным фото. Убедитесь, что вывод улучшился после добавления трёх фильтров.
3. Поочерёдно отключайте каждый фильтр, чтобы увидеть его влияние — это поможет понять, *почему* нужен каждый шаг.

## Заключение

Мы продемонстрировали, как **извлечь текст из изображения** с помощью Aspose OCR, и показали практический способ **предобрабатывать изображение для OCR**, который работает в большинстве реальных сценариев. Соединяя `DeskewFilter`, `DenoiseFilter` и `ContrastStretchFilter`, вы даёте движку чистый холст, что резко повышает точность.

Отсюда вы можете исследовать более продвинутые фильтры, работать с многостраничными документами или интегрировать результаты OCR в поисковый индекс. Что бы вы ни выбрали, основной шаблон — инициализация, предобработка, распознавание и потребление — остаётся тем же.

Готовы к следующему уровню? Попробуйте добавить `BinarizationFilter` для чёрно‑белых сканов или подключить вывод к базе данных для поисковых PDF. Приятного кодинга, и пусть каждое изображение, переданное в Aspose, возвращает чёткий, читаемый текст!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}