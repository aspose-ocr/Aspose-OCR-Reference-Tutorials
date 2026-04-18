---
category: general
date: 2026-04-17
description: Извлеките текст из изображения с помощью Aspose OCR на C#. Узнайте, как
  считывать текст из PNG, преобразовывать изображение в текст и загружать изображение
  для OCR за считанные минуты.
draft: false
keywords:
- extract text from image
- read text from png
- convert image to text
- c# image to text
- load image for ocr
language: ru
og_description: Извлеките текст из изображения с помощью Aspose OCR в C#. Этот учебник
  показывает, как читать текст из PNG, преобразовывать изображение в текст и эффективно
  загружать изображение для OCR.
og_title: Извлечение текста из изображения в C# – Полное руководство по Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: Извлечение текста из изображения в C# – преобразование изображения в текст
  с помощью Aspose OCR
url: /ru/net/text-recognition/extract-text-from-image-in-c-c-image-to-text-using-aspose-oc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения в C# – Полное руководство по Aspose OCR

Когда‑нибудь вам нужно было **извлечь текст из изображения**, но вы не знали, какую библиотеку выбрать? Вы не одиноки. Многие разработчики сталкиваются с этой проблемой, когда у них есть скриншот PNG, отсканированный счет‑фактура или многоязычный знак, и они хотят превратить пиксели в поисковый текст.  

В этом руководстве мы пройдем практическое решение, которое позволяет **читать текст из PNG**, **преобразовать изображение в текст** и **загружать изображение для OCR** с помощью Aspose OCR — всё в чистом, современном C#. К концу вы получите готовую к запуску программу, которую можно добавить в любой проект .NET.

## Что вы узнаете

- Как загрузить файл изображения для OCR (шаг «load image for OCR»)  
- Как настроить Aspose OCR для определённой группы языков  
- Как извлечь распознанную строку и вывести её в консоль  
- Советы по работе с несколькими языками, большими файлами и управлением памятью  

## Предварительные требования

- .NET 6+ SDK (или .NET Core 3.1+ – API одинаковый)  
- Visual Studio 2022, VS Code или любой предпочитаемый IDE  
- NuGet‑пакет **Aspose.OCR** (установить с помощью `dotnet add package Aspose.OCR`)  

Если у вас есть всё это, давайте начнём.

![Extract text from image using Aspose OCR in C#](https://example.com/aspsoe-ocr-demo.png "extract text from image using Aspose OCR")

## Шаг 1 – Загрузка изображения для OCR

Первое, что нужно сделать, — предоставить движку OCR что‑то для чтения. Aspose OCR работает с различными форматами, но PNG часто используется для скриншотов и отсканированных графических файлов.

```csharp
using Aspose.OCR;

// Replace with the actual path to your PNG file
string imagePath = @"C:\Images\sample.png";

// OcrImage.FromFile handles PNG, JPEG, BMP, TIFF, etc.
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

> **Почему это важно:** Правильная загрузка изображения гарантирует, что движок видит точные пиксельные данные, которые вы ожидаете. Если передать повреждённый поток, распознавание завершится без ошибок.

## Шаг 2 – Создание и настройка OCR‑движка

Далее создайте экземпляр `OcrEngine`. При желании можно задать группу языков; для большинства западных алфавитов работает значение по умолчанию, но если вы работаете с кириллицей, арабским или азиатскими символами, стоит указать язык заранее.

```csharp
// The using statement guarantees proper disposal of native resources.
using var ocrEngine = new OcrEngine();

// Example: set language to Cyrillic if your PNG contains Russian or Ukrainian text.
// OcrLanguage.Cyrillic covers several Slavic languages.
ocrEngine.Language = OcrLanguage.Cyrillic;

// If you need to support multiple languages, you can combine flags:
 // ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

> **Полезный совет:** Установка языка ограничивает набор символов, которые ищет движок, что ускоряет распознавание и повышает точность.

## Шаг 3 – Выполнение OCR и извлечение текста

Теперь происходит основная работа. Вызовите `Recognize` с изображением, которое вы загрузили ранее, а затем прочитайте свойство `Text` из результата.

```csharp
// Run OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);

// The recognized string is available via the Text property
string extractedText = ocrResult.Text;

// Output the result to the console (or write to a file, DB, etc.)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(extractedText);
```

### Ожидаемый вывод

Если `sample.png` содержит фразу «Hello, World!», вы увидите:

```
=== OCR Output ===
Hello, World!
```

Если изображение более сложное (например, многострочный чек), движок сохраняет разрывы строк, предоставляя готовый к обработке блок текста.

## Шаг 4 – Объединение всего в полном приложении

Ниже представлено полное, автономное консольное приложение, которое вы можете скопировать и вставить в новый проект C#. Оно включает обработку ошибок и комментарии, объясняющие каждую часть.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Load the image you want to recognize
                // Change the path to point at your own PNG file.
                var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.png");

                // 2️⃣ Create an OCR engine instance (disposed automatically)
                using var ocrEngine = new OcrEngine();

                // 3️⃣ Choose the language group.
                // Cyrillic works for Russian, Ukrainian, Bulgarian, etc.
                // For English only, you could use OcrLanguage.English.
                ocrEngine.Language = OcrLanguage.Cyrillic;

                // 4️⃣ Perform OCR
                var ocrResult = ocrEngine.Recognize(ocrImage);

                // 5️⃣ Output the recognized text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Simple error handling – in production you’d log this.
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

Запустите программу (`dotnet run` из папки проекта) и наблюдайте, как консоль выводит извлечённую строку. Это весь процесс **extract text from image** в менее чем 30 строк кода.

## Шаг 5 – Распространённые варианты и граничные случаи

### Чтение текста из PNG и других форматов

Хотя в примере используется PNG, Aspose OCR также поддерживает JPEG, BMP, TIFF и GIF. Просто измените расширение файла; тот же вызов `OcrImage.FromFile` будет работать без изменений.

### Преобразование изображения в текст в Web API

Если нужно предоставить эту функцию через HTTP‑endpoint, вы можете принимать загрузку `IFormFile`, преобразовать поток в `OcrImage` с помощью `OcrImage.FromStream` и вернуть строку в виде JSON. Основная логика OCR остаётся неизменной.

```csharp
// Example snippet inside an ASP.NET Core controller action
[HttpPost("api/ocr")]
public async Task<IActionResult> OcrUpload(IFormFile file)
{
    using var stream = file.OpenReadStream();
    var ocrImage = OcrImage.FromStream(stream);
    using var engine = new OcrEngine { Language = OcrLanguage.English };
    var result = engine.Recognize(ocrImage);
    return Ok(new { text = result.Text });
}
```

### Обработка больших изображений

Большие изображения с высоким разрешением могут потреблять много памяти. Практический подход — уменьшить масштаб изображения перед передачей его в движок:

```csharp
// Reduce resolution to 150 DPI (good trade‑off between speed and accuracy)
ocrEngine.ImagePreprocessing = ImagePreprocessingOptions.AutoResize;
ocrEngine.Dpi = 150;
```

### Многоязычные документы

Если документ содержит смесь английского и кириллицы, объедините флаги языков:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

Движок попытается распознать символы из обоих наборов.

### Освобождение ресурсов

Оператор `using` вокруг `OcrEngine` гарантирует освобождение нативных ресурсов. Пропуск этого может привести к утечкам памяти, особенно в длительно работающих сервисах.

## Профессиональные советы для надёжного OCR

- **Чистые изображения выигрывают:** Предобрабатывайте изображения (выравнивание, шумоподавление) с помощью библиотек, таких как **ImageSharp**, перед OCR.  
- **Размер шрифта важен:** Текст меньше 10 px часто пропускается; рассмотрите возможность увеличения масштаба изображения.  
- **Проверьте `ocrResult.Confidence`:** Объект `OcrResult` также предоставляет оценку уверенности для каждого слова — используйте её, чтобы помечать фрагменты с низкой уверенностью для ручной проверки.  
- **Пакетная обработка:** Для десятков файлов переиспользуйте один экземпляр `OcrEngine`, чтобы избежать повторных накладных расходов на инициализацию.

## Заключение

Вы только что узнали, как **извлечь текст из изображения** в C# с помощью Aspose OCR, охватив всё от **load image for OCR** до **convert image to text** и **read text from PNG**. Полный, исполняемый пример показывает точный код, который вам нужен, объясняет, зачем нужен каждый шаг, и предлагает практические варианты для реальных сценариев.

Готовы к следующему вызову? Попробуйте передать извлечённую строку в поисковый индекс, перевести её с помощью Azure Cognitive Services или создать поисковый PDF с тем же текстовым слоем. Возможностей бесконечно много, и теперь у вас есть прочная база для любого проекта **c# image to text**.

Не стесняйтесь экспериментировать, настраивать параметры языка или интегрировать этот фрагмент в более крупное приложение. Если возникнут проблемы, оставьте комментарий ниже — приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}