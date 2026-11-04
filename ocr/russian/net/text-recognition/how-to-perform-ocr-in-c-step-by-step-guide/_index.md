---
category: general
date: 2026-02-14
description: Как выполнять OCR в C# с помощью Aspose.OCR – научитесь извлекать текст
  из изображения, загружать изображение из файла и быстро запускать OCR на изображении.
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image from file
- recognize text from jpg
- run OCR on image
language: ru
og_description: Как выполнить OCR в C# с помощью Aspose.OCR. Это руководство показывает,
  как извлекать текст из изображения, загружать изображение из файла и эффективно
  выполнять OCR на изображении.
og_title: Как выполнить OCR в C# — Полный учебник по программированию
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Как выполнить OCR в C# — пошаговое руководство
url: /ru/net/text-recognition/how-to-perform-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR в C# – Полный программный учебник

Когда‑нибудь задумывались **как выполнять OCR** на фотографии, которую только что сделали на телефон? Возможно, вам нужно извлечь текст уличного знака из JPEG для навигационного приложения, или у вас есть пакет отсканированных контрактов, и вы хотите превратить их в поисковый текст. Короче говоря, вы хотите *извлечь текст из изображения* без отправки чего‑либо в облако.

Хорошая новость в том, что всё это можно делать локально с помощью Aspose.OCR для .NET. В этом учебнике мы пройдем процесс загрузки изображения из файла, распознавания текста из JPG и, наконец, **run OCR on image** файлов полностью офлайн. К концу у вас будет готовый фрагмент кода, который выводит распознанный арабский текст в консоль.

> **Что вы получите:** автономную, исполняемую программу на C#, объяснения, почему каждая строка важна, и советы по обработке распространенных граничных случаев, таких как отсутствие ресурсов или неподдерживаемые языки.

## Требования

Прежде чем погрузиться, убедитесь, что у вас есть:

| Требование | Причина |
|-------------|--------|
| .NET 6.0 or later (or .NET Framework 4.7+) | Aspose.OCR нацелен на .NET Standard 2.0, поэтому любой современный рантайм подходит. |
| Visual Studio 2022 (or VS Code with C# extension) | IDE упрощает управление пакетами NuGet и запуск консольного приложения. |
| Aspose.OCR NuGet package (`Aspose.OCR`) | Это библиотека, которая действительно выполняет работу OCR. |
| A folder containing the offline OCR resources (download from Aspose) | Офлайн‑ресурсы позволяют избежать любых HTTP‑запросов во время распознавания. |
| An image file (e.g., `arabic_sign.jpg`) | Мы будем использовать JPEG, содержащий арабский текст, но любой язык подходит. |

Если чего‑то не хватает, получите это сейчас — нет смысла начинать учебник и столкнуться с отсутствующей зависимостью на полпути.

## Шаг 1: Установить Aspose.OCR и подготовить ресурсы

Сначала добавьте пакет Aspose.OCR в ваш проект:

```bash
dotnet add package Aspose.OCR
```

После установки пакета загрузите **offline OCR resource bundle** с сайта Aspose. Распакуйте его в папку на вашем компьютере, например:

```
C:\OCRResources\
```

> **Почему это важно:** Загрузка ресурсов один раз при запуске устраняет сетевую задержку и делает ваше решение GDPR‑дружественным, поскольку ничего не покидает машину.

## Шаг 2: Создать OCR Engine и указать ему папку ресурсов

Теперь мы создадим экземпляр класса `Engine` и укажем ему, где находятся ресурсы. Это сердце **how to perform OCR** локально.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Step 2: Initialize the OCR engine with the offline resource folder
Engine ocrEngine = new Engine
{
    // Replace with the path you used in the previous step
    ResourceFolder = @"C:\OCRResources"
};

// Load the resources into memory – this prevents any hidden HTTP calls
ocrEngine.LoadResources();
```

> **Совет:** Оберните вызов `LoadResources` в блок try‑catch, если ожидаете, что путь к папке может быть неверным. Исключение точно укажет, какой файл отсутствует.

## Шаг 3: Загрузить изображение из файла

Далее нам нужно **load image from file**, чтобы движок мог его проанализировать. Aspose.OCR работает со своим обёрткой `ImageStream`.

```csharp
// Step 3: Load the JPEG you want to recognize
ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");
```

Если ваше изображение находится в другом месте, просто измените путь. Класс `ImageStream` абстрагирует работу с базовым битмапом, так что вам не нужно беспокоиться о совместимости с GDI+.

## Шаг 4: Распознать текст из JPG с использованием языковых настроек

Теперь наступает ядро **how to perform OCR** — фактическое распознавание символов. Мы запросим распознавание арабского, но вы можете заменить `Language.Arabic` на любой другой поддерживаемый язык.

```csharp
// Step 4: Run OCR specifying the desired language (Arabic in this example)
OcrResult ocrResult = ocrEngine.Recognize(
    image,
    new OcrOptions { Language = Language.Arabic }
);
```

> **Почему указывать язык?** OCR‑движок использует словари и модели символов, специфичные для языка. Указание правильного языка значительно повышает точность, особенно для скриптов со сложными формами, таких как арабский.

## Шаг 5: Показать извлечённый текст

Наконец, давайте **extract text from image** и выведем его. Это самый простой способ убедиться, что OCR прошёл успешно.

```csharp
// Step 5: Output the recognized text to the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrResult.Text);
```

Когда вы запустите программу, вы должны увидеть в консоли арабскую фразу, которая была на знаке. Если вывод выглядит искажённым, проверьте, что выбран правильный язык и что папка ресурсов содержит файлы данных для арабского.

## Полный рабочий пример

Ниже представлен полный, готовый к компиляции код, который объединяет все шаги. Скопируйте и вставьте его в новый консольный проект (`dotnet new console`) и нажмите **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Configure the OCR engine with offline resources
            // -------------------------------------------------
            Engine ocrEngine = new Engine
            {
                ResourceFolder = @"C:\OCRResources" // <-- change to your folder
            };
            ocrEngine.LoadResources(); // Loads language packs, fonts, etc.

            // -------------------------------------------------
            // Step 2: Load the image you want to process
            // -------------------------------------------------
            ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");

            // -------------------------------------------------
            // Step 3: Recognize text – specify language to improve accuracy
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(
                image,
                new OcrOptions { Language = Language.Arabic } // Change as needed
            );

            // -------------------------------------------------
            // Step 4: Output the result
            // -------------------------------------------------
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Ожидаемый вывод (пример):**

```
=== OCR Result ===
مطار القاهره الدولي
```

Если заменить изображение на английский знак и установить `Language.English`, тот же код выведет английский текст. Это демонстрирует, насколько гибок **run OCR on image**.

## Extract Text from Image – Обработка распространённых сценариев

### 1. Несколько страниц или многокадровые изображения

Некоторые форматы изображений (например, TIFF) могут содержать несколько страниц. Чтобы **extract text from image** в таких случаях, перебирайте каждый кадр:

```csharp
for (int i = 0; i < image.FramesCount; i++)
{
    image.CurrentFrame = i;
    OcrResult pageResult = ocrEngine.Recognize(image, new OcrOptions { Language = Language.English });
    Console.WriteLine($"Page {i + 1}: {pageResult.Text}");
}
```

### 2. Низкокачественные изображения

Точность OCR резко падает ниже 70 dpi. Если вы получаете размытые результаты, сначала попробуйте увеличить масштаб изображения:

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;

// Load as Bitmap, resize, then wrap back into ImageStream
Bitmap bmp = new Bitmap(@"C:\OCRResources\lowres.jpg");
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
ImageStream highResStream = ImageStream.FromBitmap(highRes);
```

### 3. Отсутствует языковой пакет

Если вы получаете исключение вроде *«Language data not found»*, проверьте, что соответствующие файлы `.dat` находятся в вашем `ResourceFolder`. Aspose поставляет отдельный zip‑архив для каждого языка.

## Run OCR on Image – Советы по производительности

- **Кешировать Engine:** Создание нового `Engine` для каждого изображения добавляет накладные расходы. Держите один экземпляр живым для пакетной обработки.
- **Параллелить безопасно:** `Engine` потокобезопасен для операций только чтения после `LoadResources`. Вы можете запускать несколько задач, каждая из которых вызывает `Recognize` для разных изображений.
- **Освобождать после использования:** Хотя `Engine` реализует `IDisposable`, сборщик .NET в конечном итоге очистит ресурсы. Явный вызов `ocrEngine.Dispose()` в блоке `using` — хорошая привычка.

```csharp
using (Engine ocrEngine = new Engine { ResourceFolder = @"C:\OCRResources" })
{
    ocrEngine.LoadResources();
    // run recognitions here
}
```

## Recognize Text from JPG – Критические случаи, на которые стоит обратить внимание

| Ситуация | Что проверить | Исправление |
|-----------|---------------|-----|
| **Corrupted JPEG** | `ImageStream.FromFile` бросает `FileNotFoundException` или `ArgumentException`. | Проверьте целостность файла, возможно, пересохраните изображение в графическом редакторе. |
| **Unsupported language** | Перечисление `Language` не содержит ваш целевой язык. | Обновите Aspose.OCR до последней версии; новые языки добавляются регулярно. |
| **Mixed‑script images** (e.g., English + Arabic) | Один язык может пропустить вторичный скрипт. | Запустите OCR дважды с разными языковыми настройками и объедините результаты. |

## Итоги – Теперь вы знаете, как выполнять OCR в C#

В этом руководстве мы рассмотрели **how to perform OCR** с помощью Aspose.OCR, от установки пакета NuGet до вывода распознанного текста. Вы научились **load image from file**, **extract text from image**, **recognize text from jpg** и безопасно **run OCR on image** в готовом к продакшену виде.

### Что дальше?

- **Экспериментировать с другими форматами файлов** вроде PNG или BMP — просто измените расширение файла.
- **Интегрировать с базой данных** для хранения результатов OCR в поисковых архивах.
- **Комбинировать с компьютерным зрением** (например, обнаруживать области текста перед OCR) для ускорения.

Не стесняйтесь менять языковые настройки, пакетно обрабатывать папки или подключать вывод к веб‑API. OCR — это строительный блок; реальная сила проявляется, когда вы вплетаете его в более крупные рабочие процессы.

Счастливого кодинга, и пусть ваши изображения всегда будут кристально чистыми!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}