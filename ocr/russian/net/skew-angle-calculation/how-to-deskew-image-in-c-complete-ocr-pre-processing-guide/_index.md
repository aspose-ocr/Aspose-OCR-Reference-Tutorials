---
category: general
date: 2026-01-10
description: Как исправить наклон изображения и улучшить результаты OCR с помощью
  Aspose.OCR. Узнайте, как предварительно обрабатывать изображение для OCR, удалять
  шум со скана и распознавать текст со скана.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from scan
- how to use ocr
- remove noise from scan
language: ru
og_description: Как исправить наклон изображения и повысить точность OCR. Это руководство
  показывает, как предварительно обработать изображение для OCR, удалить шум со сканированного
  документа и распознать текст с помощью Aspose.OCR.
og_title: Как исправить наклон изображения в C# — Полное руководство по предобработке
  OCR
tags:
- OCR
- C#
- Image Processing
title: Как выпрямить изображение в C# – Полное руководство по предобработке OCR
url: /ru/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как исправить наклон изображения в C# – Полное руководство по предобработке OCR

Вы когда‑нибудь задумывались **как исправить наклон изображения** перед тем, как передать его OCR‑движку? Вы не одиноки. Сканированные документы часто наклонены, шумные или с низким контрастом, и это мешает любой попытке распознавания текста.  

В этом руководстве мы пройдем полный, готовый к запуску пример, который **предобрабатывает изображение для OCR**, удаляет шум со скана и, наконец, **распознает текст со скана** с помощью библиотеки Aspose.OCR. К концу вы получите чёткое представление о **том, как использовать OCR** в C#, сохраняя код коротким и лаконичным.

> **Совет:** Даже небольшое вращение (5‑10°) может снизить точность OCR на 30 % и более. Исправление наклона — первый шаг, который нельзя пропускать.

## Что понадобится

- **.NET 6+** (код работает и на .NET Framework, но .NET 6 — текущий LTS)
- **Aspose.OCR for .NET** – можно получить из NuGet (`Install-Package Aspose.OCR`)
- Пример TIFF/PNG/JPEG, который повернут или шумный (в примере мы используем `noisy_rotated.tif`)
- Любая IDE по вашему выбору – Visual Studio, Rider или VS Code подойдёт

Вот и всё. Никаких дополнительных библиотек, никаких внешних сервисов.

## Шаг 1 – Загрузка исходного изображения (Почему это важно)

Прежде чем мы сможем **исправить наклон изображения**, нам нужно прочитать его в Aspose `ImageStream`. Этот объект абстрагирует ввод‑вывод файлов и предоставляет OCR‑движку единый интерфейс.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the original scan – replace the path with your own file
var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");

// Quick sanity check – make sure the image loaded
if (sourceImage == null)
{
    Console.WriteLine("Failed to load the image. Check the path and file permissions.");
    return;
}
```

*Почему сначала загрузка?* Потому что все последующие фильтры работают с изображением в памяти. Если файл не может быть прочитан, весь конвейер рушится.

## Шаг 2 – Создание конвейера предобработки (исправление наклона + удаление шума + контраст)

Надёжный OCR‑рабочий процесс обычно связывает несколько фильтров. Здесь мы **предобрабатываем изображение для OCR** и, что важнее, **автоматически исправляем наклон изображения**.

```csharp
// Create a pipeline that will run three filters in order
var preprocessPipeline = new PreprocessPipeline()
{
    // 1️⃣ DeskewFilter – detects rotation up to 30° and corrects it
    new DeskewFilter { MaxAngle = 30 },

    // 2️⃣ DenoiseFilter – smooths out speckles while keeping edges
    new DenoiseFilter { Strength = 0.8 },

    // 3️⃣ ContrastBoostFilter – makes faint characters pop
    new ContrastBoostFilter { Level = 1.3 }
};
```

**Почему именно эти три?**  
- **DeskewFilter** автоматически решает проблему “как исправить наклон изображения”; не нужно угадывать угол.  
- **DenoiseFilter** решает задачу “удалить шум со скана”, иначе появляются фантомные символы.  
- **ContrastBoostFilter** помогает OCR‑движку различать тёмный текст и светлый фон, классическая проблема при *предобработке изображения для OCR*.

## Шаг 3 – Применение конвейера (видим трансформацию)

Теперь мы действительно запускаем фильтры. Возвращённый `processedImage` — это то, что мы передадим OCR‑движку.

```csharp
// Apply all filters – the result is a cleaned‑up bitmap
var processedImage = preprocessPipeline.Apply(sourceImage);

// Optional: Save the cleaned image for visual verification
processedImage.Save("cleaned_output.tif");
Console.WriteLine("Image preprocessing complete – cleaned_output.tif saved.");
```

Если открыть `cleaned_output.tif`, вы заметите, что текст прямой, менее зернистый и с более высоким контрастом. Эта визуальная проверка полезна, когда вы *удаляете шум со скана* и хотите убедиться, что исправление наклона сработало.

## Шаг 4 – Создание и настройка OCR‑движка (как использовать OCR)

Имея чистое изображение, мы создаём экземпляр `OcrEngine`. Это ядро **того, как использовать OCR** с Aspose.

```csharp
// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    // Assign the pre‑processed image
    Image = processedImage,

    // Optional: Set language (English is default)
    // Language = Language.English,
    
    // Enable automatic page segmentation (helps with multi‑column scans)
    AutoPageSegmentation = true
};
```

*Зачем устанавливать `AutoPageSegmentation`?* Потому что многие сканы содержат таблицы или несколько колонок. Включение этой опции позволяет движку интеллектуально разбивать страницу, улучшая окончательный результат **распознавания текста со скана**.

## Шаг 5 – Запуск процесса распознавания (наконец распознаём текст)

Теперь момент истины: мы просим движок прочитать текст.

```csharp
// Kick off the OCR process
ocrEngine.Recognize();

// Retrieve the plain‑text result
string recognizedText = ocrEngine.Text;

// Show the output in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

Если всё прошло гладко, вы увидите чистый блок текста, соответствующий оригинальному документу. Это результат правильного **исправления наклона изображения**, **удаления шума** и **предобработки изображения для OCR**.

## Шаг 6 – Полный рабочий пример (готов к копированию и вставке)

Ниже полная программа, готовая к компиляции. Просто замените путь к файлу, и всё готово.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");
        if (sourceImage == null)
        {
            Console.WriteLine("Unable to load image. Check the path.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Build the preprocessing pipeline
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
        {
            new DeskewFilter { MaxAngle = 30 },          // how to deskew image
            new DenoiseFilter { Strength = 0.8 },       // remove noise from scan
            new ContrastBoostFilter { Level = 1.3 }      // improves OCR accuracy
        };

        // -------------------------------------------------
        // 3️⃣ Apply the pipeline
        // -------------------------------------------------
        var processedImage = preprocessPipeline.Apply(sourceImage);
        processedImage.Save("cleaned_output.tif");
        Console.WriteLine("Preprocessing finished – cleaned_output.tif saved.");

        // -------------------------------------------------
        // 4️⃣ Configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Image = processedImage,
            AutoPageSegmentation = true   // how to use OCR effectively
        };

        // -------------------------------------------------
        // 5️⃣ Recognize text from scan
        // -------------------------------------------------
        ocrEngine.Recognize();
        string result = ocrEngine.Text;

        Console.WriteLine("\n=== Recognized Text ===");
        Console.WriteLine(result);
    }
}
```

**Ожидаемый вывод** (усечённый для краткости):

```
=== Recognized Text ===
This is a sample scanned document.
It contains several lines of text,
and the OCR engine has correctly read them.
```

Если вывод выглядит искажённым, дважды проверьте, что исходное изображение не повернуто более чем на 30°, или увеличьте `DeskewFilter.MaxAngle`.

## Часто задаваемые вопросы (крайние случаи и варианты)

| Вопрос | Ответ |
|----------|--------|
| **Что если мой скан повернут на 45°?** | `DeskewFilter` ограничен `MaxAngle`. Увеличьте его (например, `MaxAngle = 60`) или предварительно поверните изображение с помощью графической библиотеки перед передачей в конвейер. |
| **Могу ли я обрабатывать PDF постранично?** | Да. Преобразуйте каждую страницу PDF в изображение (например, с помощью `Aspose.Pdf`) и запустите тот же конвейер для каждого битмапа. |
| **Мой документ на французском – нужно ли что‑то менять?** | Установите `ocrEngine.Language = Language.French;` или загрузите пользовательский языковой пакет. Остальная часть конвейера остаётся без изменений. |
| **Можно ли сохранить оригинальное разрешение?** | `PreprocessPipeline` работает с оригинальным битмапом, сохраняет DPI. Просто избегайте вызова `ImageStream.Resize`, если только не требуется уменьшить масштаб для производительности. |
| **Как повышение контраста влияет на цветные сканы?** | `ContrastBoostFilter` работает с каждым каналом; он безопасен для черно‑белых и цветных изображений, но вы также можете сначала преобразовать в градации серого с помощью `new GrayscaleFilter()`. |

## Пример изображения (визуальная подсказка)

![пример исправления наклона изображения](/images/deskew-example.png)

*На картинке показан «до/после» 12° повернутого, шумного скана, который был исправлен и очищен.*

## Заключение

Мы рассмотрели **как исправить наклон изображения** с помощью Aspose.OCR, продемонстрировали полный конвейер **предобработки изображения для OCR**, показали, как **удалять шум со скана**, и, наконец, **распознавать текст со скана** несколькими строками C#. Объединяя `DeskewFilter`, `DenoiseFilter` и `ContrastBoostFilter`, вы получаете чистый битмап, позволяющий OCR‑движку выполнять свою работу без застревания на артефактах.  

Следующие шаги? Попробуйте экспериментировать с различными силами фильтров, добавить `BinarizationFilter` для чисто черно‑белого вывода или передать очищенное изображение в последующий NLP‑конвейер. Та же схема работает с чеками, паспортами и историческими документами.  

Есть дополнительные вопросы о **том, как использовать OCR** в других языках или фреймворках? Оставляйте комментарий, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}