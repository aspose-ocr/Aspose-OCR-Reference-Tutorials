---
category: general
date: 2026-05-06
description: Узнайте, как исправлять наклон изображения и извлекать текст из него
  с помощью Aspose OCR — пошаговое руководство по повышению точности OCR и удалению
  шума с изображения.
draft: false
keywords:
- how to deskew image
- extract text from image
- how to use OCR
- improve OCR accuracy
- how to denoise image
language: ru
og_description: Узнайте, как выпрямить изображение и извлечь текст из него с помощью
  Aspose OCR. Этот учебник показывает, как удалить шум с изображения и улучшить точность
  OCR.
og_title: Как выпрямить изображение в C# – Полное руководство по OCR
tags:
- OCR
- C#
- Image Processing
title: Как выпрямить изображение в C# – Полное руководство по OCR
url: /ru/net/ocr-optimization/how-to-deskew-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как исправить наклон изображения в C# – Полное руководство по OCR

Когда‑то вам нужно было **исправить наклон изображения** перед запуском OCR, но вы не знали, какие фильтры применить? Вы не одиноки — многие разработчики сталкиваются с тем же, когда исходное фото слегка наклонено или шумно. Хорошая новость? С несколькими строками C# и Aspose.OCR вы можете выпрямить, очистить и наконец извлечь текст из изображения с впечатляющей точностью.

В этом руководстве мы пройдем всё необходимое: загрузим наклонённую картинку, применим фильтры выравнивания и подавления шума, усилим контраст и, наконец, получим текст. К концу вы поймёте **как использовать OCR**, увидите, **как улучшить точность OCR**, и получите готовый к запуску пример кода, который можно вставить в любой .NET‑проект.

## Что понадобится

- .NET 6 или новее (API работает с .NET Core и .NET Framework)
- Aspose.OCR for .NET (бесплатная пробная версия или лицензия) — её можно установить через NuGet командой `Install-Package Aspose.OCR`
- Пример изображения, которое наклонено и слегка шумно (например, `skewed_noisy.jpg`)
- Visual Studio, VS Code или любой другой редактор по вашему выбору

Дополнительные нативные библиотеки не требуются; Aspose обрабатывает всё внутри.

## Шаг 1: Создайте проект и установите Aspose.OCR

### Создайте новое консольное приложение

```bash
dotnet new console -n DeskewOcrDemo
cd DeskewOcrDemo
```

### Добавьте пакет Aspose.OCR

```bash
dotnet add package Aspose.OCR
```

Вот и всё — ваш проект теперь ссылается на движок OCR и встроенные фильтры, которые нам понадобятся.

## Шаг 2: Загрузите изображение, которое хотите обработать

Мы начнём с создания экземпляра `OcrEngine` и укажем ему файл, который нужно очистить.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 2: Load the image you want to process
        var ocrEngine = new OcrEngine();
        ocrEngine.SetImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // The rest of the pipeline will be added next…
    }
}
```

> **Почему это важно:** Загрузка изображения — первый шаг для любого последующего фильтра. Если путь указан неверно, весь конвейер завершится без ошибок, поэтому проверьте расположение файла.

## Шаг 3: Сформируйте конвейер обработки — выравнивание, подавление шума, затем усиление контраста

Здесь происходит магия. Мы добавим три фильтра в точном порядке, который даёт наилучшие результаты OCR:

1. **DeskewFilter** — выпрямляет изображение.
2. **MedianDenoiseFilter** — удаляет случайные пятна без размытия краёв.
3. **ContrastStretchFilter** — усиливает разницу между текстом и фоном.

```csharp
        // Step 3: Build a processing pipeline – deskew, denoise, then enhance contrast
        ocrEngine.Filters.Add(new DeskewFilter());               // how to deskew image
        ocrEngine.Filters.Add(new MedianDenoiseFilter());        // how to denoise image
        ocrEngine.Filters.Add(new ContrastStretchFilter());      // improve OCR accuracy
```

> **Совет:** Порядок имеет решающее значение. Сначала выравнивание, потому что наклонённое изображение может сбить с толку фильтр шумоподавления. После того как изображение стало прямым, медианный фильтр убирает зернистость, а затем контраст делает буквы более заметными.

## Шаг 4: Запустите распознавание OCR

Теперь позволим Aspose выполнить тяжёлую работу. Метод `Recognize` возвращает объект `OcrResult`, содержащий извлечённую строку и некоторые метрики уверенности.

```csharp
        // Step 4: Run the OCR recognition
        var ocrResult = ocrEngine.Recognize();

        // Optional: check confidence (0‑100). Higher means more reliable.
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

> **Как использовать OCR:** Вызов `Recognize` внутри применяет все добавленные фильтры, а затем запускает движок OCR. Вам не нужно вызывать каждый фильтр вручную; конвейер делает это за вас.

## Шаг 5: Выведите распознанный текст

Наконец, выводим текст в консоль. В реальных приложениях, скорее всего, вы запишете его в файл, базу данных или передадите другому сервису.

```csharp
        // Step 5: Output the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Полный, готовый к запуску пример

Объединив всё вместе, получаем полную программу, которую можно скопировать в `Program.cs`:

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to process
        ocrEngine.SetImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 3️⃣ Build a processing pipeline – deskew, denoise, then enhance contrast
        ocrEngine.Filters.Add(new DeskewFilter());               // how to deskew image
        ocrEngine.Filters.Add(new MedianDenoiseFilter());        // how to denoise image
        ocrEngine.Filters.Add(new ContrastStretchFilter());      // improve OCR accuracy

        // 4️⃣ Run the OCR recognition
        var ocrResult = ocrEngine.Recognize();

        // 5️⃣ Show confidence and extracted text
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Запустите её командой:

```bash
dotnet run
```

Вы увидите оценку уверенности, за которой следует текстовая версия того, что было на оригинальном фото.

## Проверка результата — чего ожидать

Если исходное изображение, к примеру, содержит строку печатного счёта:

```
Invoice #12345
Total: $1,250.00
Date: 2024‑04‑30
```

После выполнения конвейера консоль выведет что‑то вроде:

```
Confidence: 96%
=== Extracted Text ===
Invoice #12345
Total: $1,250.00
Date: 2024-04-30
```

Высокое значение уверенности (обычно выше 90 %) указывает на то, что шаги **исправления наклона изображения** и **подавления шума изображения** помогли OCR‑движку чётко увидеть символы.

## Часто задаваемые вопросы и особые случаи

### Что делать, если изображение повернуто более чем на 45 градусов?

`DeskewFilter` автоматически определяет угол до ±45°. Для больших вращений предварительно поверните изображение с помощью `ocrEngine.Filters.Add(new RotateFilter(angle))` перед выравниванием.

### У меня низкая уверенность — что ещё попробовать?

- Добавьте **BinarizationFilter**, чтобы принудительно преобразовать изображение в чёрно‑белое.
- Увеличьте радиус **MedianDenoiseFilter**: `new MedianDenoiseFilter(3)`.
- Используйте изображение более высокого разрешения (300 dpi и выше).

### Можно ли обрабатывать несколько изображений в цикле?

Конечно. Просто вынесите создание движка за пределы цикла, вызывайте `SetImage` для каждого файла и переиспользуйте одну и ту же коллекцию фильтров.

```csharp
foreach (var file in Directory.GetFiles("images", "*.jpg"))
{
    ocrEngine.SetImage(file);
    var result = ocrEngine.Recognize();
    // handle result...
}
```

### Работает ли это с PDF?

Aspose.OCR может читать страницы PDF как изображения, но для извлечения каждой страницы в виде bitmap понадобится библиотека Aspose.PDF.

## Советы для максимальной точности OCR

1. **Обрезайте лишние рамки** — лишние пустые области могут запутать OCR‑движок.
2. **Используйте однородный фон** — чистый белый или светло‑серый работает лучше всего.
3. **Избегайте экстремального освещения** — тени создают ложные контуры, которые фильтр шумоподавления может не полностью убрать.
4. **Тестируйте на реальных образцах** — синтетические данные выглядят чисто; в продакшене изображения часто содержат артефакты.

## Заключение

Мы рассмотрели **как исправить наклон изображения**, **как подавить шум изображения**, а также полный процесс **как использовать OCR** с Aspose для **извлечения текста из изображения** и **повышения точности OCR**. Пример кода полностью готов, его можно запускать и адаптировать под пакетную обработку, интеграцию в UI или облачные сервисы.

Что дальше? Попробуйте заменить `MedianDenoiseFilter` на `GaussianDenoiseFilter` и сравните оценки уверенности, либо передайте извлечённый текст в парсер естественного языка для автоматического заполнения форм. Возможности безграничны, как только вы освоите конвейер предобработки.

Счастливого кодинга, и пусть ваши результаты OCR будут кристально чистыми! 

--- 

![пример исправления наклона изображения](/images/deskew-example.png "пример исправления наклона изображения")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}