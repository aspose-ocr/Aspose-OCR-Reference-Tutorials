---
category: general
date: 2026-03-13
description: Как исправить наклон изображения и повысить контраст для OCR. Узнайте,
  как удалить шум, извлечь текстовое изображение и получить надёжные результаты с
  Aspose OCR.
draft: false
keywords:
- how to deskew image
- extract text image
- how to remove noise
- how to boost contrast
- how to extract text
language: ru
og_description: Как исправить наклон изображения в C# и извлечь текст. Это руководство
  показывает, как удалить шум, повысить контраст и получить точные результаты OCR.
og_title: Как выпрямить изображение – Быстрый OCR с Aspose на C#
tags:
- OCR
- C#
- Image Processing
title: Как исправить наклон изображения и извлечь текст в C# — Полное руководство
url: /ru/net/ocr-optimization/how-to-deskew-image-and-extract-text-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как исправить наклон изображения и извлечь текст в C# – Полное руководство

Когда‑нибудь задавались вопросом **как исправить наклон изображения** перед передачей его в OCR‑движок? Вы не одни. Наклонённый скан может превратить идеальную задачу извлечения текста в угадайку, особенно если изображение также шумное или с низким контрастом. В этом руководстве мы пройдём по точным шагам, чтобы выпрямить, очистить и осветлить изображение, чтобы вы могли **надёжно извлечь текст из изображения**. По пути мы также рассмотрим **как удалить шум**, **как повысить контраст** и, наконец, **как извлечь текст** с помощью Aspose.OCR.

К концу этого руководства у вас будет готовая к запуску программа на C#, которая берёт наклонённый, пятнистый PNG, исправляет его и выводит распознанный текст в консоль. Никаких загадочных ссылок «см. документацию» — только полное, автономное решение, которое можно скопировать и вставить.

## Что понадобится

- **.NET 6.0** или новее (код также работает на .NET Framework 4.7+).  
- **Aspose.OCR for .NET** — установите через NuGet: `Install-Package Aspose.OCR`.  
- Пример изображения, которое повернуто, шумное или с низким контрастом (мы будем использовать `skewed_noisy.png`).  
- Любая IDE по вашему вкусу — Visual Studio, Rider или VS Code подойдёт.

Это всё. Никаких дополнительных нативных библиотек, никаких внешних сервисов.

![пример исправления наклона изображения](image-placeholder.png)

*(Текст alt изображения: пример исправления наклона изображения – до и после обработки)*

## Как исправить наклон изображения – Обзор

Суть **как исправить наклон изображения** проста: определить угол поворота и повернуть bitmap обратно к горизонтальной базовой линии. Aspose.OCR поставляется с `DeskewFilter`, который делает именно это. Но хороший OCR‑конвейер редко останавливается на исправлении наклона; вам также нужно **удалить шум**, **повысить контраст** и, наконец, **извлечь текст**. Ниже каждый из этих шагов разобран подробно.

### Почему важен конвейер предварительной обработки

Представьте, что вам нужно прочитать рукописную записку, отсканированную под небольшим углом, с пятнами от кофе по странице. Даже самый умный OCR‑движок споткнётся. Подавая чистое, выпрямленное изображение, вы даёте движку чёткий сигнал, что приводит к более высокой точности и меньшему количеству исправлений после обработки.

## Шаг 1: Загрузка изображения

Сначала нам нужен `ImageStream`, указывающий на исходный файл. Aspose.OCR умеет читать множество форматов (PNG, JPEG, TIFF), так что берите любой, который у вас есть.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the image from disk
ImageStream imageStream = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.png");
```

**Почему это важно:** Загрузка изображения в `ImageStream` даёт OCR‑движку единый способ доступа к пиксельным данным, независимо от исходного типа файла.

## Шаг 2: Создание конвейера предварительной обработки (исправление наклона, удаление шума, повышение контраста)

Здесь мы отвечаем на **как удалить шум**, **как повысить контраст** и, конечно, **как исправить наклон изображения** — все в одном `FilterPipeline`.

```csharp
// Create a pipeline to hold the filters
FilterPipeline preprocessingPipeline = new FilterPipeline();

// 1️⃣ Deskew – correct rotation up to 15 degrees
preprocessingPipeline.Add(new DeskewFilter { MaxAngleDegrees = 15 });

// 2️⃣ Despeckle – eliminate isolated dark/bright pixels (noise)
preprocessingPipeline.Add(new DespeckleFilter());

// 3️⃣ Contrast boost – make darks darker, lights lighter (Level 30 is a good start)
preprocessingPipeline.Add(new ContrastBoostFilter { Level = 30 });

// 4️⃣ Binarize – convert to pure black‑and‑white using Otsu’s method
preprocessingPipeline.Add(new BinarizeOtsuFilter());
```

### Как каждый фильтр помогает

| Filter | Назначение | Типичный сценарий использования |
|--------|------------|----------------------------------|
| **DeskewFilter** | Поворачивает изображение обратно к горизонтали. | Сканированные страницы, отклонённые на несколько градусов. |
| **DespeckleFilter** | Удаляет отдельные пятна, похожие на случайные символы. | Сканирование старых газет или низкокачественных копий. |
| **ContrastBoostFilter** | Усиливает разницу между передним планом и фоном. | Выцветшие чернила или изображения с низким контрастом. |
| **BinarizeOtsuFilter** | Создаёт чистое черно‑белое изображение, идеальное для OCR. | Любой случай, когда цвет не нужен для распознавания текста. |

**Pro tip:** Если ваше изображение сильно повернуто (более 15°), увеличьте `MaxAngleDegrees` до 30 или 45, но имейте в виду, что экстремальные углы могут вызвать артефакты интерполяции.

## Шаг 3: Настройка OCR‑движка

Теперь мы связываем изображение и конвейер, указываем Aspose, какой язык мы ожидаем, и создаём экземпляр `OcrEngine`.

```csharp
// Set up the OCR engine with the image, pipeline, and language
OcrEngine ocrEngine = new OcrEngine
{
    Image = imageStream,
    PreProcessingFilters = preprocessingPipeline,
    Language = Language.English      // Change if you need another language
};
```

**Почему мы задаём язык:** Указание `Language.English` сужает набор символов, которые ищет движок, что ускоряет обработку и уменьшает количество ложных срабатываний. Если нужна многоязычная поддержка, можно передать список через запятую (например, `Language.English | Language.French`).

## Шаг 4: Распознавание и извлечение текста

При полной подготовке фактическое распознавание сводится к единому вызову метода.

```csharp
// Perform the OCR operation
ocrEngine.Recognize();

// The recognized text is now available via the Text property
string extractedText = ocrEngine.Text;
Console.WriteLine(extractedText);
```

Эта строка выводит результат OCR непосредственно в консоль, что идеально подходит для быстрой проверки или передачи в другую систему.

## Ожидаемый вывод и проверка

Запуск полной программы на `skewed_noisy.png` должен дать примерно следующее:

```
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut
labore et dolore magna aliqua.
```

Если вывод выглядит искажённым, проверьте следующее:

1. **Диапазон углов:** Был ли исходный поворот больше, чем `MaxAngleDegrees`?  
2. **Уровень шума:** Сильно ли изображение покрыто пятнами? Рассмотрите возможность добавить второй `DespeckleFilter`.  
3. **Уровень контраста:** Для очень бледных чернил увеличьте `ContrastBoostFilter.Level` до 40‑50.

## Как удалить шум – Расширенные параметры

Иногда одного `DespeckleFilter` недостаточно, особенно при сканировании зернистой пленки. Aspose предлагает `MedianFilter`, который хорошо работает на текстурированных фонах.

```csharp
preprocessingPipeline.Add(new MedianFilter { KernelSize = 3 });
```

Добавьте его **перед** `DespeckleFilter` для наилучшего результата. Операция медианы сглаживает области, сохраняя границы, что помогает удерживать символы целыми.

## Как повысить контраст – Точная настройка

Если значение по умолчанию `Level = 30` оставляет некоторые символы бледными, можно последовательно применить несколько усилений контраста:

```csharp
preprocessingPipeline.Add(new ContrastBoostFilter { Level = 20 });
preprocessingPipeline.Add(new ContrastBoostFilter { Level = 20 });
```

Два умеренных усиления часто превосходят одно агрессивное, поскольку они избегают клиппинга экстремальных пикселей.

## Извлечение текста из изображения с помощью Aspose – Советы по пост‑обработке

После получения `ocrEngine.Text` вы, возможно, захотите:

- **Удалить пробелы**: `extractedText = extractedText.Trim();`
- **Нормализовать окончания строк**: `extractedText = extractedText.Replace("\r\n", "\n");`
- **Удалить не‑ASCII символы** (если ожидаете только английский): `extractedText = Regex.Replace(extractedText, @"[^\x00-\x7F]+", string.Empty);`

Эти шаги превращают сырые результаты OCR в чистые, пригодные для поиска строки — идеальны для индексации или передачи в последующий NLP‑конвейер.

## Распространённые проблемы и советы

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Текст наклонён после OCR | `DeskewFilter` max angle слишком мал | Увеличьте `MaxAngleDegrees`. |
| Много случайных символов | Шум не полностью удалён | Добавьте `MedianFilter` или увеличьте агрессивность `DespeckleFilter`. |
| Бледные буквы не распознаются | Контраст недостаточно сильный | Сложите два `ContrastBoostFilter` или повысите `Level`. |
| Производительность медленная на больших изображениях | Конвейер работает с изображением полного разрешения | Сначала уменьшите масштаб: `preprocessingPipeline.Add(new ResizeFilter { Width = 1200 });` |

**Помните:** Лучший OCR‑конвейер часто представляет собой компромисс между качеством изображения и временем обработки. Протестируйте несколько типовых образцов, прежде чем фиксировать настройки.

## Полный рабочий пример

Ниже приведена полностью готовая к копированию программа. Сохраните её как `Program.cs`, восстановите пакет NuGet и запустите.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source image that needs OCR
        // -------------------------------------------------
        ImageStream imageStream = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.png");

        // -------------------------------------------------
        // Step 2: Build a preprocessing pipeline
        // -------------------------------------------------
        FilterPipeline preprocessingPipeline = new FilterPipeline();

        // Deskew – fix rotation up to 15°
        preprocessingPipeline.Add(new DeskewFilter { MaxAngleDegrees = 15 });

        // Despeckle – remove isolated noise pixels
        preprocessingPipeline.Add(new DespeckleFilter());

        // Optional: Median filter for heavy grain
        // preprocessingPipeline.Add(new MedianFilter { KernelSize = 3 });

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}