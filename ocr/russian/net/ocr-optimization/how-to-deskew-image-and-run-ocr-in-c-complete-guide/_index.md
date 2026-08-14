---
category: general
date: 2026-03-07
description: Узнайте, как исправлять наклон изображения, повышать контраст и извлекать
  текст из сканированного документа с помощью Aspose OCR. Выполните OCR изображения
  с полным примером на C# и легко загрузите изображение для OCR.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: ru
og_description: Узнайте, как исправлять наклон изображения, повышать контраст и извлекать
  текст из сканированного документа с помощью Aspose OCR в C#. Выполните OCR изображения
  с пошаговым кодом.
og_title: Как исправить наклон изображения и выполнить OCR в C# – Полное руководство
tags:
- C#
- OCR
- Image Processing
title: Как исправить наклон изображения и выполнить OCR в C# – Полное руководство
url: /ru/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выровнять изображение и выполнить OCR в C# – Полное руководство

Если вы когда‑нибудь задавались вопросом **как выровнять изображение** перед запуском OCR, вы попали по адресу. В этом руководстве мы пройдёмся по повышению контраста, загрузке изображения для OCR и, наконец, **извлечению текста из сканированного документа** с помощью Aspose OCR.  

Независимо от того, оцифровываете ли вы старые чеки, очищаете сканированные контракты или просто нуждаетесь в надёжном способе чтения текста с наклонённого фото, нижеописанные шаги покрывают всё необходимое. Без лишних слов — только рабочий пример, который можно скопировать‑вставить в Visual Studio.  

## Что вы получите

К концу этого руководства вы сможете:

* Исправить наклон до 30° (это и есть **как выровнять изображение**).  
* Увеличить контраст изображения для более чётких контуров символов (**как повысить контраст**).  
* Загрузить вашу картинку в OCR‑движок (**загрузить изображение для OCR**).  
* Запустить процесс распознавания и **извлечь текст из сканированного документа**.  

Всё это работает с последним пакетом Aspose.OCR .NET NuGet (v23.11 на момент написания).  

---

![Пример выравнивания изображения](/images/deskew-example.png "как выровнять изображение")

*На изображении выше показан сканированный документ до и после выравнивания.*

## Требования

* .NET 6.0 или новее (код также работает на .NET Framework 4.7+).  
* Visual Studio 2022 (или любой другой IDE для C#).  
* Пакет Aspose.OCR NuGet – установить через `dotnet add package Aspose.OCR`.  

Вот и всё. Никаких внешних сервисов, никаких API‑ключей.

---

## Как выровнять изображение с помощью Aspose OCR

Первым делом мы создаём **ImageProcessingPipeline** и добавляем `DeskewFilter`. Фильтр автоматически определяет доминирующий угол строки текста и вращает изображение обратно к горизонтали.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**Почему это важно:**  
Наклонённый скан сбивает с толку OCR‑движок, потому что символы больше не выровнены по базовой линии. `DeskewFilter` анализирует гистограмму изображения, находит угол и вращает его, что значительно повышает точность распознавания.

> **Полезный совет:** Если вы знаете, что ваши документы никогда не наклонены более чем на 15°, задайте `MaxAngle = 15`, чтобы ускорить обработку.

---

## Как повысить контраст для лучшего распознавания

После выравнивания следующим шагом является выделение текста. `ContrastBoostFilter` растягивает диапазон интенсивности пикселей, что особенно полезно для выцветших отпечатков.

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**Почему это помогает:**  
Сканы с низким контрастом дают сероватые символы, которые бинаризатор может принять за фон. Повышение контраста делает тёмные пиксели темнее, а светлые — светлее, предоставляя `BinarizationFilter` более чистое полотно.

---

## Выполнение OCR на изображении – загрузка файла

Теперь, когда изображение предварительно обработано, нам нужно **загрузить изображение для OCR**. Aspose предлагает удобный вспомогательный метод `ImageStream.FromFile`.

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Если ваше изображение находится в потоке (например, загружено через веб‑API), используйте `ImageStream.FromStream(yourStream)`. Движок поддерживает BMP, JPEG, PNG, TIFF и многие другие форматы.

---

## Запуск процесса распознавания и извлечение текста из сканированного документа

Когда всё настроено, вызов `Recognize()` выполняет основную работу. После вызова распознанный текст доступен через `ocrEngine.Text`.

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**Ожидаемый вывод** (пример простого счёта‑фактуры):

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

Если вывод выглядит искажённым, проверьте порядок шагов в конвейере — сначала выравнивание, затем шумоподавление, повышение контраста и, наконец, бинаризация. Их перестановка может ухудшить результаты.

---

## Распространённые проблемы и особые случаи

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Пустой результат** | Изображение слишком тёмное или слишком светлое для метода бинаризации по умолчанию. | Увеличьте `ContrastBoostFilter.Strength` или переключитесь на `BinarizationMethod.Otsu`. |
| **Частичный пропуск текста** | После шумоподавления остаётся шум. | Используйте `DenoiseLevel.Medium` для менее шумных изображений или добавьте второй `DenoiseFilter`. |
| **Неправильное направление вращения** | Документ имеет смешанную ориентацию (например, фото повернутой страницы). | Установите `DeskewFilter.MaxAngle` ниже и предварительно поверните изображение с помощью `ImageProcessor.Rotate`. |
| **Замедление производительности** | Большая партия изображений высокого разрешения. | Уменьшите размер изображений (`ImageProcessor.Resize`) перед конвейером или обрабатывайте их параллельно (`Parallel.ForEach`). |

---

## Полный рабочий пример (готов к копированию)

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Сохраните этот файл как `Program.cs`, выполните `dotnet run` и наблюдайте, как консоль выводит результат **извлечения текста из сканированного документа**.  

---

## Следующие шаги и смежные темы

* **Пакетная обработка** – оберните описанную логику в цикл для обработки десятков файлов.  
* **Пользовательские языковые пакеты** – если нужно распознавать нелатинские скрипты, загрузите языковую модель через `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;`.  
* **PDF‑вывод** – комбинируйте Aspose.PDF с OCR, чтобы внедрить поисковый текст непосредственно в PDF‑файл.  
* **Тонкая настройка производительности** – экспериментируйте с порядком `ImageProcessingPipeline`; иногда шумоподавление перед выравниванием даёт более быстрые результаты на шумных фотографиях.  

Все эти темы опираются на основные концепции, которые мы рассмотрели: **как выровнять изображение**, **как повысить контраст**, **загрузить изображение для OCR**, **выполнить OCR на изображении** и, наконец, **извлечь текст из сканированного документа**.

---

## Итоги

Мы только что продемонстрировали полный, готовый к использованию способ **как выровнять изображение** и выполнить OCR в C#. Соединяя фильтр выравнивания, шаг шумоподавления, повышение контраста и бинаризацию, вы получаете чистый ввод, позволяющий Aspose OCR надёжно **извлекать текст из сканированного документа**.  

Запустите код, подберите параметры фильтров под свои документы, и вы увидите, как быстро повышается точность распознавания. Есть вопросы? Оставляйте комментарий, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}