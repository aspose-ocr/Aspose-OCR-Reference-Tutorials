---
category: general
date: 2026-11-14
description: Узнайте, как распознавать изображение в текст с помощью Aspose OCR на
  C#. Это пошаговое руководство также охватывает извлечение текста из JPG и эффективное
  преобразование изображения в текст.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize image to text
- extract text from jpg
- perform OCR on image
- convert image to text
- recognize text from image
language: ru
lastmod: 2026-11-14
og_description: Распознавайте изображение в текст с помощью Aspose OCR на C#. Следуйте
  этому полному руководству, чтобы извлечь текст из JPG, выполнить OCR на изображении
  и преобразовать изображение в текст.
og_image_alt: Screenshot of C# code that recognize image to text using Aspose OCR
og_title: Распознавание изображения в текст с помощью Aspose OCR – руководство по
  C#
schemas:
- author: Aspose
  dateModified: '2026-11-14'
  description: Learn how to recognize image to text using Aspose OCR in C#. This step‑by‑step
    guide also covers how to extract text from jpg and convert image to text efficiently.
  headline: How to recognize image to text with Aspose OCR in C#
  type: TechArticle
- description: Learn how to recognize image to text using Aspose OCR in C#. This step‑by‑step
    guide also covers how to extract text from jpg and convert image to text efficiently.
  name: How to recognize image to text with Aspose OCR in C#
  steps:
  - name: Large images
    text: Large files increase memory usage and processing time. Resize the image
      to a maximum of 2000 px on the longest side before calling `RecognizeImage`.
  - name: Missing language model
    text: If the required language pack cannot be downloaded (e.g., offline environment),
      the engine throws `IOException`. Wrap the call in a try‑catch block and provide
      a fallback language.
  - name: Asynchronous processing
    text: For UI applications, avoid blocking the UI thread. Wrap the recognition
      call in `Task.Run`.
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Как распознать изображение в текст с помощью Aspose OCR в C#
url: /ru/net/text-recognition/how-to-recognize-image-to-text-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как распознать изображение в текст с помощью Aspose OCR на C#

Если вам нужно распознать изображение в текст в приложении .NET, это руководство покажет точные шаги, необходимые для этого. Вы увидите, как извлекать текст из jpg‑файлов, выполнять OCR над данными изображения и преобразовывать изображение в текст с минимальным количеством кода.

В руководстве рассматривается всё: от установки пакета Aspose.OCR через NuGet до безопасной обработки результата OCR. Внешние сервисы не требуются, код работает на .NET 6 и выше.

## Установить пакет Aspose OCR

Прежде чем писать код, добавьте библиотеку Aspose.OCR в ваш проект. Пакет содержит все языковые модели и автоматически загружает необходимые файлы во время выполнения.

```bash
dotnet add package Aspose.OCR
```

Эта команда добавляет последнюю стабильную версию **Aspose.OCR** в ваш `csproj`. Шаг гарантирует, что вы сможете вызвать `OcrEngine` без ручного управления DLL‑файлами.

## Создать и настроить движок OCR

Создание движка OCR — первое программное действие, которое необходимо выполнить. Движок управляет загрузкой изображения, выбором языка и распознаванием.

```csharp
using Aspose.OCR;

// Step 1: Instantiate the OCR engine (required modules are downloaded automatically)
OcrEngine ocrEngine = new OcrEngine();
```

`OcrEngine` — основной класс, который выполняет тяжёлую работу. Его создание инициирует лёгкую инициализацию; библиотека загружает языковые пакеты только при выборе языка.

## Выбрать языковую модель (извлечение текста из jpg)

Выбор правильной языковой модели влияет на точность. Для кириллического текста задайте `OcrLanguage.Cyrillic`. При первом выборе языка, который не кэширован локально, Aspose загрузит модель в фоновом режиме.

```csharp
// Step 2: Choose the language model – triggers download if needed
ocrEngine.Language = OcrLanguage.Cyrillic;
```

Если вы работаете с латинскими скриптами, замените `Cyrillic` на `English` или другое значение перечисления. Тот же код **perform OCR on image** независимо от языка.

## Распознать текст из JPG‑файла (преобразовать изображение в текст)

Теперь можно передать файл изображения движку. Метод `RecognizeImage` принимает путь к файлу, поток или `Bitmap`. Здесь мы используем JPEG, потому что это распространённый формат сканированных документов.

```csharp
// Step 3: Recognize text from the image file
OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/cyrillic-sample.jpg");
```

Метод возвращает объект `OcrResult`, содержащий исходную строку, оценки уверенности и необязательную информацию о разметке. Этот вызов **recognize text from image** в одну строку.

## Вывести результат OCR (извлечение текста из jpg)

После распознавания выведите найденный текст в консоль или передайте его другому компоненту.

```csharp
// Step 4: Display the recognized text
Console.WriteLine(ocrResult.Text);
```

Типичный вывод в консоль выглядит так:

```
Пример текста на кириллице
```

Если изображение не содержит читаемых символов, `ocrResult.Text` будет пустой строкой. Всегда проверяйте это условие перед дальнейшей обработкой.

## Обработать распространённые граничные случаи

### Большие изображения

Большие файлы увеличивают использование памяти и время обработки. Перед вызовом `RecognizeImage` измените размер изображения до максимума 2000 px по самой длинной стороне.

```csharp
using System.Drawing;

// Load, resize, then recognize
using (Bitmap original = new Bitmap("YOUR_DIRECTORY/large-sample.jpg"))
{
    int maxDim = 2000;
    int width = original.Width;
    int height = original.Height;

    if (width > maxDim || height > maxDim)
    {
        float scale = Math.Min((float)maxDim / width, (float)maxDim / height);
        int newWidth = (int)(width * scale);
        int newHeight = (int)(height * scale);
        using (Bitmap resized = new Bitmap(original, newWidth, newHeight))
        {
            OcrResult result = ocrEngine.RecognizeImage(resized);
            Console.WriteLine(result.Text);
        }
    }
    else
    {
        OcrResult result = ocrEngine.RecognizeImage(original);
        Console.WriteLine(result.Text);
    }
}
```

### Отсутствие языковой модели

Если требуемый языковой пакет не может быть загружен (например, в офлайн‑среде), движок бросит `IOException`. Оберните вызов в блок try‑catch и предоставьте запасной язык.

```csharp
try
{
    ocrEngine.Language = OcrLanguage.Cyrillic;
    OcrResult result = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(result.Text);
}
catch (IOException ex)
{
    Console.WriteLine($"Language model download failed: {ex.Message}");
    // Fallback to English
    ocrEngine.Language = OcrLanguage.English;
    OcrResult fallback = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(fallback.Text);
}
```

### Асинхронная обработка

Для UI‑приложений избегайте блокировки UI‑потока. Оберните вызов распознавания в `Task.Run`.

```csharp
await Task.Run(() =>
{
    OcrResult asyncResult = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(asyncResult.Text);
});
```

## Практические советы для надёжного OCR

- **Предобрабатывать изображения**: Применяйте преобразование в градации серого и усиление контраста, чтобы улучшить точность при **perform OCR on image** при плохом освещении.
- **Выбирать правильный язык**: Всегда задавайте `ocrEngine.Language` перед распознаванием. По умолчанию установлен English, что приводит к низкой точности для кириллических или азиатских скриптов.
- **Проверять вывод**: Используйте регулярные выражения, чтобы убедиться, что распознанный текст соответствует ожидаемым шаблонам (например, даты, идентификаторы) перед сохранением.
- **Кешировать языковые пакеты**: Первая загрузка может занять несколько секунд. Разверните необходимые пакеты вместе с приложением, если нужен мгновенный старт.

## Полный пример

Ниже приведена автономная программа, демонстрирующая весь рабочий процесс — от установки пакета до вывода результата OCR.

```csharp
// -----------------------------------------------------------
// Recognize image to text with Aspose OCR – complete example
// -----------------------------------------------------------
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1. Create the OCR engine (modules are downloaded automatically)
        OcrEngine ocrEngine = new OcrEngine();

        // 2. Select the language model – triggers download if missing
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 3. Recognize text from a JPG file (convert image to text)
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/cyrillic-sample.jpg");

        // 4. Output the recognized string (extract text from jpg)
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Ожидаемый вывод в консоль**

```
Recognized text:
Пример текста на кириллице
```

Запуск программы на другом изображении (например, английском счете) требует лишь изменить перечисление `Language` и путь к файлу. Тот же код **recognize text from image** без изменений.

## Заключение

Теперь вы знаете, как распознать изображение в текст с помощью Aspose OCR на C#. Руководство охватило установку библиотеки, создание и настройку движка OCR, преобразование изображения в текст и обработку типичных граничных случаев. Имея эту основу, вы можете **extract text from jpg**, **perform OCR on image** любые данные любого размера и интегрировать результат в более крупные .NET‑процессы.

Далее изучайте расширенные возможности, такие как:

- **Многостраничный PDF OCR** (используйте `PdfInput` вместо JPG)
- **Пользовательский белый список символов** для повышения точности числовых кодов
- **Сохранение результатов OCR в поисковые PDF** с помощью `OcrEngine.Save`.

Экспериментируйте с различными языковыми моделями и методами предобработки изображений, чтобы достичь наилучшего уровня распознавания для вашего домена. Приятного кодинга!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [распознать текст из изображения в C# – пошаговое руководство Aspose OCR](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-step-by-step-aspose-ocr-guide/)
- [распознать текст из изображения с Aspose OCR – полный асинхронный гид для C#](/ocr/english/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-async-g/)
- [распознать текст из изображения в C# – полный учебник Aspose OCR](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}