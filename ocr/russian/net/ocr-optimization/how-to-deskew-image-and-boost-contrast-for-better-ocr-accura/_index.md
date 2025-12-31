---
category: general
date: 2025-12-30
description: Как быстро исправить наклон изображения и узнать, как повысить контраст
  при извлечении текста из изображения для улучшения точности OCR.
draft: false
keywords:
- how to deskew image
- how to boost contrast
- extract text from image
- recognize text image
- improve ocr accuracy
language: ru
og_description: Как быстро исправить наклон изображения и узнать, как повысить контраст
  при извлечении текста из изображения для улучшения точности OCR.
og_title: Как исправить наклон изображения и увеличить контраст для лучшей точности
  OCR.
tags:
- OCR
- C#
- Image Processing
title: Как выпрямить изображение и увеличить контраст для лучшей точности OCR.
url: /ru/net/ocr-optimization/how-to-deskew-image-and-boost-contrast-for-better-ocr-accura/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как исправить наклон изображения и повысить контраст для лучшей точности OCR

Когда‑то задавались вопросом **как исправить наклон изображения** полученного со сканера или смартфона?  
Вы не одиноки — большинство разработчиков сталкиваются с этой проблемой, когда исходное фото слегка наклонено или шумно, и результат OCR превращается в неразборчивый набор символов.  

Хорошая новость: с помощью нескольких строк C# вы можете выпрямить изображение, очистить фон и даже увеличить контраст, чтобы движок считывал текст как профессионал. В этом руководстве мы также покажем, как **извлекать текст из изображения** и **распознавать текст на изображении** с помощью Aspose.OCR, постоянно держая в фокусе **повышение точности OCR**.

## Что понадобится

- **.NET 6.0** или новее (код также компилируется на .NET Framework 4.7+)  
- NuGet‑пакет **Aspose.OCR** (версия 23.12 или новее) — установить через `dotnet add package Aspose.OCR`  
- Пример изображения, которое одновременно повернуто и шумно (например, `noisy_rotated.jpg`)  
- Visual Studio, VS Code или любая другая IDE  

И всё — никаких дополнительных нативных библиотек, без тяжёлых привязок OpenCV. Чистый управляемый код.

---

## Шаг 1: Создайте проект и подключите пространства имён

Сначала создайте новое консольное приложение и подключите необходимые пространства имён. Этот шаг — фундамент для всего, что будет дальше.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later
        }
    }
}
```

**Почему это важно:**  
`Aspose.OCR` предоставляет класс `OcrEngine`, а `Aspose.OCR.Filters` — удобные фильтры предобработки, такие как `DeskewFilter` и `ContrastBoostFilter`. Подключив их сразу, код становится аккуратнее, а компилятор знает, что мы собираемся использовать.

---

## Шаг 2: Инициализируйте OCR‑движок и добавьте фильтр выравнивания

Теперь мы действительно **как исправить наклон изображения**. `DeskewFilter` автоматически определяет угол поворота (до заданного максимума) и вращает bitmap обратно в горизонтальное положение.

```csharp
// Inside Main()
var ocrEngine = new OcrEngine();

// Deskew: correct up to 15 degrees of rotation
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
```

**Что происходит «под капотом»?**  
Фильтр сканирует изображение в поисках самой длинной горизонтальной строки текста, оценивает наклон и применяет обратное вращение. Ограничивая `MaxAngle` до 15°, мы избегаем пере‑коррекции уже почти прямых изображений.

> **Совет:** Если ваши исходные изображения могут быть перевёрнуты вверх ногами, увеличьте `MaxAngle` до 180° — фильтр всё равно найдёт правильную ориентацию.

---

## Шаг 3: Уменьшите шум с помощью фильтра Denoise

Шумный скан может запутать даже самый умный OCR‑движок. Добавление `DenoiseFilter` сглаживает пятна, не стирая мелкие детали.

```csharp
// Denoise: strength ranges from 0 (off) to 1 (max)
ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });
```

**Зачем это нужно:**  
Шум создаёт ложные контуры, которые OCR воспринимает как символы. Значение силы `0.7` подходит для большинства отсканированных документов; при необходимости подгоняйте его под очень чистые или очень грязные входные данные.

---

## Шаг 4: Повышение контраста — «Как повысить контраст» в действии

Здесь мы отвечаем на вторичный запрос **how to boost contrast**. `ContrastBoostFilter` усиливает разницу между тёмным текстом и светлым фоном, делая буквы более выразительными.

```csharp
// Contrast boost: level > 1 increases contrast
ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });
```

**Логика:**  
Более высокий контраст снижает вероятность пропуска слабых штрихов. Уровень `1.3` хорошо работает для типичных чёрно‑на‑белых документов; для цветных фотографий может потребоваться `1.5` и выше.

---

## Шаг 5: Запустите OCR и извлеките текст

После предобработки изображения мы наконец **извлекаем текст из изображения** с помощью метода `Recognize`. Метод возвращает объект `OcrResult`, содержащий сырую строку и оценки уверенности.

```csharp
// Perform OCR on the prepared image
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/noisy_rotated.jpg");

// Output the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Что вы получаете:**  
`ocrResult.Text` содержит текстовое представление всего, что движок смог прочитать. Если нужна уверенность на уровне слов, изучите `ocrResult.Regions` — каждый регион имеет свойство `Confidence`.

---

## Полный рабочий пример (готов к копированию)

Ниже полностью готовая программа, которую можно вставить в `Program.cs`. Убедитесь, что путь к изображению указывает на реальный файл в вашей системе.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Deskew – correct up to 15° rotation
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

            // 3️⃣ Denoise – smooth out speckles (strength 0.7)
            ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });

            // 4️⃣ Contrast boost – make text pop (level 1.3)
            ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });

            // 5️⃣ Recognize the image
            var imagePath = @"YOUR_DIRECTORY\noisy_rotated.jpg";
            var ocrResult = ocrEngine.Recognize(imagePath);

            // 6️⃣ Show the result
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Ожидаемый вывод (пример):**

```
=== OCR Output ===
Invoice #12345
Date: 2024-09-30
Total Amount: $1,250.00
Thank you for your business!
```

Если результат выглядит «мусором», проверьте качество изображения, подкорректируйте `Strength` или `Level`, либо увеличьте `MaxAngle` для более агрессивного выравнивания.

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если изображение перевёрнуто вверх ногами?

Установите `MaxAngle = 180` в `DeskewFilter`. Фильтр обнаружит поворот на 180° и правильно его исправит.

### Мой документ цветной (например, отсканированная форма с синими выделениями).  

Попробуйте добавить `ColorFilter` перед повышением контраста или вручную преобразовать изображение в градации серого:

```csharp
ocrEngine.Filters.Add(new GrayscaleFilter());
```

### Нужно обработать множество файлов пакетно.

Обёрните логику OCR в цикл `foreach`, проходящий по директории:

```csharp
foreach (var file in Directory.GetFiles(@"C:\Scans", "*.jpg"))
{
    var result = ocrEngine.Recognize(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

### Как узнать уверенность OCR?

Изучите `ocrResult.Regions`:

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"Text: {region.Text} – Confidence: {region.Confidence:P2}");
}
```

Более высокие значения уверенности (близкие к 100 %) обычно означают, что шаги предобработки прошли успешно.

---

## Советы для максимизации точности OCR

| Совет | Почему это помогает |
|------|----------------------|
| **Используйте без потерь форматы изображений** (PNG, TIFF) | Сжатие JPEG может размыть контуры, ухудшая распознавание. |
| **Держите DPI ≥ 300** | Больше пикселей на символ — больше данных для движка. |
| **Обрезайте лишние поля** | Снижает шум и ускоряет обработку. |
| **Применяйте бинарный порог** (чёрное/белое) после повышения контраста для чисто текстовых документов | Упрощает изображение до двух цветов, что нравится большинству OCR‑движков. |
| **Сначала тестируйте на небольшом наборе** | Позволяет точно подобрать `Strength` и `Level` перед масштабированием. |

---

## Заключение

Мы прошли путь от **как исправить наклон изображения** через **как повысить контраст** к полной цепочке **извлечения текста из изображения** с помощью Aspose.OCR. Соединяя `DeskewFilter`, `DenoiseFilter` и `ContrastBoostFilter` перед вызовом `Recognize`, вы заметите ощутимый прирост **повышения точности OCR** для большинства реальных сканов.

Запустите код, подгоните параметры фильтров под свои документы, и вы будете получать чистый текст даже из самых «грязных» фотографий. Хотите идти дальше? Добавьте словари для конкретных языков или передайте результат в проверку орфографии для пост‑обработки.

Удачной разработки, и пусть ваши результаты OCR всегда будут кристально чистыми! 

--- 

![пример выравнивания изображения](deskew_example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap >}}
{{< blocks/products/products-backtop-button >}}