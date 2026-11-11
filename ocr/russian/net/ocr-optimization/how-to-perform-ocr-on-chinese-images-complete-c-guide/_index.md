---
category: general
date: 2026-03-07
description: Как выполнять OCR на китайских изображениях с помощью Aspose OCR. Узнайте,
  как извлекать китайский текст, конвертировать изображение в ePub и повышать точность
  OCR в одном руководстве.
draft: false
keywords:
- how to perform OCR
- extract chinese text
- convert image to epub
- how to improve OCR
- recognize simplified chinese
language: ru
og_description: Как выполнять OCR на китайских изображениях с помощью Aspose OCR.
  Получите пошаговый код для извлечения китайского текста, улучшения OCR и экспорта
  в ePub.
og_title: Как выполнить OCR на китайских изображениях – Полное руководство по C#
tags:
- OCR
- C#
- Aspose
title: Как выполнить OCR на китайских изображениях – полное руководство по C#
url: /ru/net/ocr-optimization/how-to-perform-ocr-on-chinese-images-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR на китайских изображениях – Полное руководство C#

Когда‑нибудь задавались вопросом **как выполнять OCR** на картинке, содержащей китайские символы? Вы не одиноки. Во многих приложениях — сканирование чеков, оцифровка учебников или создание многоязыкового поискового движка — получение чистого текста из изображения является решающей функцией.

В этом руководстве мы пройдём реальное решение, которое **извлекает китайский текст**, сохраняет результат в файл обычного текста и даже **преобразует изображение в ePub** для электронных читалок. По пути мы обсудим **как улучшить точность OCR**, почему стоит включать режим GPU и что нужно сделать, чтобы **правильно распознавать упрощённый китайский**.

К концу руководства у вас будет полностью рабочая программа на C#, несколько практических советов и чёткое представление о дальнейших шагах (например, добавление определения языка или пакетной обработки). Никакой внешней документации не требуется — всё, что нужно, находится здесь.

## Что понадобится

- .NET 6+ (или .NET Core 3.1 с Aspose OCR for .NET)  
- Действительная лицензия Aspose OCR for .NET (бесплатная trial‑версия подходит для экспериментов)  
- Файл изображения, содержащий упрощённые китайские символы (например, `chinese_sample.jpg`)  
- Visual Studio 2022 или любой другой редактор C#

Если чего‑то не хватает, установите NuGet‑пакет сейчас:

```bash
dotnet add package Aspose.OCR
```

Вот и всё — никаких дополнительных нативных библиотек, никакого COM‑interop, только один .NET‑пакет.

## Как выполнить OCR – настройка движка Aspose OCR

Первое, что нужно сделать, — создать и настроить OCR‑движок. Этот шаг критичен, потому что параметры движка определяют **насколько хорошо OCR работает** с китайскими символами и насколько быстро он работает.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;

// Step 1: Initialise the OCR engine with Chinese‑specific settings
var ocrEngine = new OcrEngine
{
    Settings =
    {
        // Primary language – Simplified Chinese
        Language = Language.ChineseSimplified,

        // Use GPU when available for a noticeable speed boost
        EngineMode = EngineMode.Gpu,

        // Build a processing pipeline to clean up the image first
        ImageProcessing = new ImageProcessingPipeline()
            .Add(new DeskewFilter()) // Fix rotation
            .Add(new BinarizationFilter
            {
                Method = BinarizationMethod.Sauvola // Improves contrast for Chinese glyphs
            })
    }
};
```

**Почему это важно:**  
- **Language = ChineseSimplified** указывает Aspose загрузить набор символов для упрощённого китайского, что значительно снижает количество ошибок распознавания.  
- **EngineMode.Gpu** может сократить время обработки вдвое на современном GPU, но при отсутствии GPU плавно переходит на CPU.  
- **DeskewFilter** удаляет наклон, который часто появляется, когда пользователи делают фото телефоном.  
- **Sauvola binarization** создаёт высококонтрастное чёрно‑белое изображение, классический приём для повышения точности OCR на плотных скриптах, таких как китайский.

> **Pro tip:** Если вы работаете с фотографиями при плохом освещении, добавьте `ContrastFilter` перед бинаризацией. Это не обязательно для нашего примера, но часто избавляет от головной боли.

![Диаграмма конвейера OCR](ocr-pipeline.png "Диаграмма конвейера OCR")  

> *Alt text:* Диаграмма конвейера OCR

## Извлечение китайского текста из изображения

Теперь, когда движок готов, загружаем изображение и позволяем движку выполнить свою магию. Это ядро **extract chinese text**.

```csharp
// Step 2: Load the image you want to recognize
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/chinese_sample.jpg");

// Step 3: Run the recognition process
ocrEngine.Recognize();

// Step 4: Grab the recognized string
string recognizedText = ocrEngine.Text;

// Optional: Write the text to a .txt file for later analysis
File.WriteAllText(@"YOUR_DIRECTORY/out.txt", recognizedText);
```

**Что вы должны увидеть:**  
Если `chinese_sample.jpg` содержит фразу «中华人民共和国», файл `out.txt` будет содержать именно эти символы — без лишних пробелов и без искажённых латинских букв.

### Распространённые подводные камни

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| Отсутствуют символы | Изображение слишком шумное | Добавьте `MedianFilter` перед бинаризацией |
| Неправильный язык | `Language` установлен на `English` | Убедитесь, что `Language = Language.ChineseSimplified` |
| Медленная обработка | GPU не включён | Проверьте, что на машине установлен совместимый драйвер CUDA |

## Преобразование изображения в ePub

Многие разработчики спрашивают: *«Можно ли превратить отсканированную страницу в читаемую электронную книгу?»* Конечно — Aspose OCR поставляется с экспортёром ePub. Это удовлетворяет требование **convert image to epub**.

```csharp
// Step 5: Export the OCR result as an ePub file
ocrEngine.ExportToEpub(
    @"YOUR_DIRECTORY/out.epub",
    new EpubExportOptions { Title = "Chinese Sample" });
```

Сгенерированный `out.epub` будет содержать извлечённый китайский текст, корректно закодированный в UTF‑8, и его можно открыть в Kindle, Apple Books или любом ePub‑читалке.

**Почему ePub?**  
- Формат переходит в потоковый режим, поэтому читатели могут менять размер шрифта без нарушения разметки.  
- Текст остаётся поисковым, что удобно для последующей индексации.

## Как улучшить OCR – практические приёмы

Даже при надёжном конвейере иногда появляются ошибки распознавания. Ниже быстрый чек‑лист **how to improve OCR** для китайских документов:

1. **Предобработка изображения** — используйте `GaussianBlurFilter` для сглаживания пятен, затем `ContrastFilter` для усиления краёв.  
2. **Установите более высокое DPI** — если вы контролируете процесс сканирования, стремитесь к 300 dpi или выше; изображения низкого разрешения теряют детали штрихов.  
3. **Включите определение языка** — Aspose может автоматически определять язык; добавьте резервный вариант упрощённого китайского, если определение не удалось.  
4. **Тонкая настройка бинаризации** — замените `Sauvola` на `Otsu`, если фон равномерно светлый.  
5. **Пакетная обработка** — обрабатывайте несколько страниц параллельно с помощью `Parallel.ForEach`, чтобы задействовать многоядерные процессоры.

```csharp
// Example: Adding a Gaussian blur before binarization
ocrEngine.Settings.ImageProcessing
    .Add(new GaussianBlurFilter { Radius = 1.2 })
    .Add(new BinarizationFilter { Method = BinarizationMethod.Otsu });
```

## Распознавание упрощённого китайского – крайние случаи

Фраза **recognize simplified Chinese** часто ставит в тупик новичков, потому что тот же OCR‑движок может работать и с традиционным китайским, японским или корейским. Чтобы всё было предсказуемо:

- **Явно задайте язык** (как мы сделали в Шаге 1).  
- **Избегайте страниц со смешанными языками**; если страница сочетает упрощённый китайский с английским, рассмотрите два прохода: один с `Language.ChineseSimplified`, другой с `Language.English`.  
- **Проверьте результат** — после распознавания выполните простую регулярку, чтобы убедиться, что все символы находятся в диапазоне Unicode `\u4E00‑\u9FFF`.

```csharp
bool IsSimplifiedChinese(string text)
{
    return System.Text.RegularExpressions.Regex.IsMatch(
        text, @"^[\u4E00-\u9FFF\s]+$");
}
```

Если проверка не прошла, вы можете записать страницу в журнал для ручного просмотра.

## Полный рабочий пример

Собрав всё вместе, получаем один файл, который можно скопировать в новый консольный проект (`Program.cs`). Он включает все шаги, необязательные настройки и финальную строку статуса.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine – Chinese‑specific settings
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Settings =
            {
                Language = Language.ChineseSimplified,
                EngineMode = EngineMode.Gpu,
                ImageProcessing = new ImageProcessingPipeline()
                    .Add(new DeskewFilter())
                    .Add(new BinarizationFilter
                    {
                        Method = BinarizationMethod.Sauvola
                    })
            }
        };

        // -------------------------------------------------
        // 2️⃣ Load image and run recognition
        // -------------------------------------------------
        string imgPath = @"YOUR_DIRECTORY/chinese_sample.jpg";
        ocrEngine.Image = ImageStream.FromFile(imgPath);
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 3️⃣ Save plain‑text output
        // -------------------------------------------------
        string txtPath = @"YOUR_DIRECTORY/out.txt";
        File.WriteAllText(txtPath, ocrEngine.Text);
        Console.WriteLine($"✅ Text saved to {txtPath}");

        // -------------------------------------------------
        // 4️⃣ Export to ePub
        // -------------------------------------------------
        string epubPath = @"YOUR_DIRECTORY/out.epub";
        ocrEngine.ExportToEpub(epubPath,
            new EpubExportOptions { Title = "Chinese Sample" });
        Console.WriteLine($"✅ ePub generated at {epubPath}");

        // -------------------------------------------------
        // 5️⃣ Quick verification – length and charset
        // -------------------------------------------------
        Console.WriteLine($"Done – extracted text length: {ocrEngine.Text.Length}");
        Console.WriteLine($"Contains only Simplified Chinese? " +
                          $"{IsSimplifiedChinese(ocrEngine.Text)}");
    }

    // Helper to ensure only Simplified Chinese characters were extracted
    static bool IsSimplifiedChinese(string text)
    {
        return System.Text.RegularExpressions.Regex.IsMatch(
            text, @"^[\u4E00-\u9FFF\s]+$");
    }
}
```

**Ожидаемый вывод в консоли (пример):**

```
✅ Text saved to C:\Images\out.txt
✅ ePub generated at C:\Images\out.epub
Done – extracted text length: 128
Contains only Simplified Chinese? True
```

Запустите программу, откройте `out.txt` или `out.epub`, и вы увидите чистые, поисковые китайские символы, готовые к дальнейшей обработке.

## Заключение

Мы только что рассмотрели **how to perform OCR** на китайских изображениях от начала до конца, показали, как **extract Chinese text**, **convert the result to an ePub**, и применили несколько практических советов.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}