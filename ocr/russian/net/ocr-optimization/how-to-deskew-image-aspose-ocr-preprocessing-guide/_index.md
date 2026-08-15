---
category: general
date: 2026-04-29
description: как исправить наклон изображения и повысить точность OCR с помощью Aspose
  OCR — узнайте, как удалить шум, повысить контраст изображения и извлечь текст из
  изображений.
draft: false
keywords:
- how to deskew image
- remove noise from image
- boost image contrast
- extract text from image
- improve ocr accuracy
language: ru
og_description: как исправить наклон изображения и улучшить точность OCR. Этот учебник
  показывает, как удалить шум с изображения, повысить контрастность изображения и
  извлечь текст из изображения с помощью Aspose OCR.
og_title: Как исправить наклон изображения – Полное руководство по Aspose OCR
tags:
- Aspose OCR
- C#
- Image preprocessing
title: Как выпрямить изображение – руководство по предобработке OCR Aspose
url: /ru/net/ocr-optimization/how-to-deskew-image-aspose-ocr-preprocessing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# как исправить наклон изображения – Полное руководство по Aspose OCR

Когда‑нибудь задавались вопросом **как исправить наклон изображения** перед передачей его в OCR‑движок? Вы не одиноки. Кривой скан или фотография, сделанная под углом, могут испортить распознавание текста, оставив вас с искажённым выводом.  

В этом руководстве мы пройдём полный, сквозной процесс, который не только **как исправить наклон изображения**, но и **удалить шум с изображения**, **повысить контраст изображения**, а в конце **извлечь текст из изображения** с помощью Aspose OCR. К концу вы увидите, как **повысить точность OCR** без необходимости копаться в документации.

> **Что вы получите:** готовое к запуску консольное приложение на C#, чёткое объяснение каждого шага предобработки и несколько практических советов, которые можно сразу скопировать в свои проекты.

## Требования

- .NET 6.0 или новее (код работает и с .NET Core, и с .NET Framework)  
- NuGet‑пакет Aspose.OCR (`Install-Package Aspose.OCR`)  
- Пример изображения, которое наклонено, зашумлено или имеет низкий контраст (например, `skewed_noisy.jpg`)  
- Visual Studio, VS Code или любой другой редактор C#, который вам нравится  

Дополнительные нативные библиотеки не требуются – Aspose обрабатывает всё в процессе.

---

## Как исправить наклон изображения с Aspose OCR

Первое, что нам нужно, – фильтр исправления наклона, который корректирует угол поворота. Aspose OCR поставляется с `FilterDeskew`, который анализирует базовые линии текста и вращает битмап соответствующим образом.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that will later recognize text.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build an image‑processing pipeline.
        //    The order matters: deskew → denoise → contrast boost.
        ImageProcessingPipeline processingPipeline = new ImageProcessingPipeline();
        processingPipeline.Add(new FilterDeskew());          // ✅ how to deskew image
        processingPipeline.Add(new FilterDenoise());         // ✅ remove noise from image
        processingPipeline.Add(new FilterContrastBoost());   // ✅ boost image contrast

        // 3️⃣ Load your source picture.
        var sourceImage = OcrEngine.LoadImage(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Apply the pipeline – the image is now straight, cleaner, and sharper.
        var processedImage = processingPipeline.Apply(sourceImage);

        // 5️⃣ Run OCR on the cleaned‑up bitmap.
        var ocrResult = ocrEngine.Recognize(processedImage);

        // 6️⃣ Print the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Почему мы начинаем с исправления наклона:**  
Если строки текста не горизонтальны, OCR‑движок будет пытаться интерпретировать наклонные символы как другие глифы, что резко снижает **повысить точность OCR**. Исправление наклона выравнивает базовые линии, предоставляя распознавателю чистый холст.

> *Совет профессионала:* Если угол поворота известен заранее (например, все сканы повернуты на 90°), можно обойтись без фильтра и повернуть изображение вручную – это небольшое ускорение.

---

## Удалить шум с изображения – Очистка скана

Шум проявляется в виде случайных чёрных или белых пятен (классический «соль‑перец») и может сбить с толку сегментацию символов. `FilterDenoise` применяет медианный фильтр, который сглаживает шум, сохраняя при этом границы.

```csharp
// Inside the pipeline we already added FilterDenoise.
// If you need a custom strength, you can instantiate it like:
var denoise = new FilterDenoise { Strength = 2 }; // 1‑3 are typical values
processingPipeline.Add(denoise);
```

**Когда стоит менять силу фильтра:**  
- **Strength = 1** – Лёгкая зернистость, быстрая обработка.  
- **Strength = 3** – Очень зашумлённые сканы (например, факсимильные документы).  

Слишком большая сила может размыть тонкие штрихи, что может *повредить* **повысить точность OCR**. Протестируйте несколько значений на репрезентативном образце.

---

## Повысить контраст изображения – Выделить слабые символы

Изображения с низким контрастом (например, выцветшие чеки) часто заставляют OCR‑движок пропускать лёгкие глифы. `FilterContrastBoost` растягивает гистограмму так, что тёмные пиксели становятся темнее, а светлые — светлее.

```csharp
var contrast = new FilterContrastBoost { ContrastLevel = 1.5f }; // 1.0 = no change
processingPipeline.Add(contrast);
```

**Почему контраст важен:**  
Более высокий контраст улучшает отношение сигнал‑к‑шуму, облегчая нейронному распознавателю Aspose различать «I» и «l». Однако чрезмерное усиление может привести к насыщению изображения, превращая плавные градиенты в резкие границы, похожие на артефакты. Стремитесь к балансу; 1.5‑2.0 – хорошая отправная точка.

---

## Извлечь текст из изображения – Финальный шаг OCR

Теперь, когда изображение прямое, чистое и яркое, OCR‑движок может выполнять свою работу. Метод `Recognize` возвращает объект `OcrResult`, содержащий необработанный текст, оценки уверенности и даже ограничивающие рамки, если они нужны.

```csharp
var ocrResult = ocrEngine.Recognize(processedImage);
Console.WriteLine(ocrResult.Text);
```

**Пример вывода** (при условии, что исходное изображение содержит «Invoice #12345»):

```
=== OCR Output ===
Invoice #12345
Date: 04/28/2026
Total: $1,234.56
```

Если вы видите пропущенные символы, проверьте конвейер предобработки – возможно, изображению всё ещё нужен более сильный шумоподавитель или иной уровень контраста.  

> *Частый вопрос:* «Что если нужно распознавать язык, отличный от английского?»  
> Просто задайте `ocrEngine.Language = Language.English;` на другой поддерживаемый язык (например, `Language.French`). Шаги предобработки остаются теми же.

---

## Повысить точность OCR – Дополнительные настройки

Даже при идеальном конвейере несколько дополнительных параметров могут ещё больше **повысить точность OCR**:

| Совет | Когда использовать | Как |
|------|--------------------|-----|
| **Бинаризация** | Очень тёмные или очень светлые сканы | `processingPipeline.Add(new FilterBinarize());` |
| **Изменение размера изображения** | Маленькие шрифты (<10 pt) | `processedImage = OcrEngine.Resize(processedImage, 2.0);` |
| **Указание набора символов** | Известный алфавит (только цифры и т.п.) | `ocrEngine.Characters = "0123456789";` |
| **Многостраничные PDF** | Пакетная обработка | Перебирайте каждую страницу и переиспользуйте один и тот же конвейер. |

Помните: каждый дополнительный фильтр увеличивает время обработки, поэтому включайте только действительно нужные.

---

## Полный рабочий пример (готов к копированию)

Ниже представлен весь код программы, готовый к компиляции. Замените `YOUR_DIRECTORY` на путь к папке, где находится `skewed_noisy.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Build preprocessing pipeline
        ImageProcessingPipeline pipeline = new ImageProcessingPipeline();
        pipeline.Add(new FilterDeskew());                     // how to deskew image
        pipeline.Add(new FilterDenoise { Strength = 2 });    // remove noise from image
        pipeline.Add(new FilterContrastBoost { ContrastLevel = 1.8f }); // boost image contrast

        // Load source image
        var sourcePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        var sourceImage = OcrEngine.LoadImage(sourcePath);

        // Apply pipeline
        var cleanImage = pipeline.Apply(sourceImage);

        // Perform OCR
        var result = ocrEngine.Recognize(cleanImage);

        // Output
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

**Ожидаемый результат:** чистый, выпрямленный текст, выведенный в консоль, с гораздо меньшим количеством ошибок распознавания по сравнению с передачей исходного файла напрямую в `ocrEngine.Recognize`.

---

## Заключение

Мы рассмотрели **как исправить наклон изображения**, как **удалить шум с изображения**, как **повысить контраст изображения** и, наконец, как **извлечь текст из изображения** с помощью Aspose OCR. Последовательное применение этих фильтров даст заметный прирост **повысить точность OCR**, особенно на низкокачественных сканах.

Готовы к следующему вызову? Попробуйте обработать многостраничный PDF тем же конвейером или поэкспериментируйте с пользовательскими порогами бинаризации. Принципы те же – выпрямить, очистить, осветлить, затем распознать.

Есть вопросы или странный кейс? Оставляйте комментарий, будем разбираться вместе. Приятного кодинга!  

![пример исправления наклона изображения](deskew-example.png "пример исправления наклона изображения")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}