---
category: general
date: 2026-07-05
description: распознавание текста с изображения с помощью C# OCR — пошаговое руководство
  с полным примером OCR на C#, загрузка изображения для OCR и извлечение текста из
  изображения за несколько минут.
draft: false
keywords:
- recognize text from image
- c# ocr example
- c# image to text
- load image for OCR
- extract text from image
language: ru
og_description: распознавать текст с изображения в C# с практическим руководством.
  Узнайте пример OCR на C#, как загрузить изображение для OCR и быстро извлечь текст
  из изображения.
og_title: Распознать текст с изображения с помощью C# OCR – Полный пример
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: recognize text from image using C# OCR – a step‑by‑step guide with
    a full c# ocr example, load image for OCR and extract text from image in minutes.
  headline: recognize text from image with C# OCR – Complete Example
  type: TechArticle
- description: recognize text from image using C# OCR – a step‑by‑step guide with
    a full c# ocr example, load image for OCR and extract text from image in minutes.
  name: recognize text from image with C# OCR – Complete Example
  steps:
  - name: 1️⃣ Image Size & Quality
    text: 'OCR accuracy drops sharply on blurry or tiny pictures. A good rule of thumb:
      **minimum 300 dpi** for printed documents, and at least **800 px** on the longest
      side for photos. If you can’t control the source, consider up‑scaling with a
      bicubic algorithm before feeding it to the engine.'
  - name: 2️⃣ Multiple Languages
    text: If your image mixes scripts (e.g., English and Thai), set the language to
      `OcrLanguage.Multi` or pass an array of languages if the library supports it.
  - name: 3️⃣ Memory Management
    text: When processing many images in a loop, remember to dispose of streams and
      engine instances to avoid memory leaks.
  - name: 4️⃣ Error Reporting
    text: Wrap the OCR call in a try/catch block. Some engines throw `OcrException`
      when the language pack fails to download.
  - name: Got questions?
    text: Feel free to drop a comment—whether you’re stuck on a language pack, need
      help with image pre‑processing, or just want to share your success story. Happy
      coding, and enjoy turning pictures into searchable text!
  type: HowTo
tags:
- C#
- OCR
- Image Processing
title: Распознавание текста с изображения с помощью C# OCR – Полный пример
url: /ru/net/text-recognition/recognize-text-from-image-with-c-ocr-complete-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание текста с изображения с помощью C# OCR – Полный пример

Когда‑нибудь вам нужно было **распознавать текст с изображения**, но вы не знали, какую библиотеку C# выбрать? Вы не одиноки — разработчики постоянно спрашивают: «Как превратить фотографию вывески в редактируемый текст?» Хорошая новость в том, что всего несколькими строками кода вы можете запустить полностью рабочий **c# ocr example**.

В этом руководстве мы пройдем всё, что нужно для **распознавания текста с изображения**: установка OCR‑пакета, загрузка изображения, запуск движка и, наконец, вывод результата. К концу вы сможете взять любой bitmap (отсканированный счёт, фотографию уличной вывески — как вам угодно) и извлечь чистые, пригодные для поиска строки.

---

## Что понадобится

- **.NET 6** или новее (код работает на .NET Core, .NET Framework и .NET 5+)
- Последняя версия пакета NuGet **Microsoft Cognitive Services Vision** *или* пакета **IronOCR** — оба предоставляют API в стиле `OcrEngine`. Приведённые ниже фрагменты кода ориентированы на общий интерфейс `OcrEngine`, который реализует большинство библиотек.
- Файл изображения, который вы хотите обработать (в примере мы используем `thai_sign.png`).
- Редактор кода — подойдёт Visual Studio, VS Code или Rider.

Вот и всё. Никаких тяжёлых OCR‑SDK, никаких внешних сервисов, только несколько ссылок NuGet и несколько строк кода C#.

## Шаг 1: Настройте проект для **распознавания текста с изображения**

Сначала создайте консольное приложение (или небольшую утилиту WPF/WinForms) и добавьте OCR‑пакет. Для целей этого руководства будем считать, что вы используете **IronOCR**, поскольку он поставляется с простым классом `OcrEngine`.

```bash
dotnet new console -n ImageToTextDemo
cd ImageToTextDemo
dotnet add package IronOcr
```

> **Совет:** Если вы предпочитаете Azure Computer Vision, замените `IronOcr` на `Microsoft.Azure.CognitiveServices.Vision.ComputerVision` и соответственно скорректируйте код — оба предоставляют одинаковый высокоуровневый рабочий процесс.

## Шаг 2: Загрузите изображение для OCR

Прежде чем движок сможет **распознавать текст с изображения**, ему нужен источник. Помощник `ImageStream.FromFile` (или `File.ReadAllBytes` для чистого .NET) выполняет основную работу.

```csharp
using IronOcr;

// ...

// Step 2: Load the image you want to process
var imagePath = Path.Combine(Environment.CurrentDirectory, "thai_sign.png");

// Verify the file exists – a tiny sanity check that saves hours of debugging
if (!File.Exists(imagePath))
{
    Console.Error.WriteLine($"❌ Image not found: {imagePath}");
    return;
}

// IronOCR can read directly from a file path, but we’ll demonstrate the stream approach
using var imageStream = new FileStream(imagePath, FileMode.Open, FileAccess.Read);
var ocrImage = OcrInput.FromStream(imageStream);
```

Обратите внимание на комментарий “**load image for OCR**” — он отражает вторичное ключевое слово и напоминает, зачем мы оборачиваем файл в поток. Если вы получаете изображения из веб‑API, просто замените `FileStream` на `MemoryStream`, построенный из HTTP‑ответа.

## Шаг 3: Создайте и настройте OCR‑движок

Теперь мы запускаем движок, который действительно будет **распознавать текст с изображения**. Установка языка необязательна, но значительно повышает точность, если вы знаете используемый скрипт.

```csharp
// Step 3: Create an OCR engine instance
var engine = new OcrEngine();

// Optional: tell the engine which language to expect.
// Here we use Thai as in the original snippet; change it to English, Chinese, etc.
engine.Language = OcrLanguage.Thai; // triggers language data download on first use
```

Если вы используете другую библиотеку, свойство может называться `DefaultLanguage` или `Language`. Идея остаётся той же: выберите правильный языковой пакет **прежде чем извлекать текст из изображения**.

## Шаг 4: Выполните распознавание — ядро **распознавания текста с изображения**

После загрузки изображения и настройки движка фактический вызов OCR представляет собой одну строку.

```csharp
// Step 4: Run the OCR process
var result = engine.Read(ocrImage);
```

Метод `Read` возвращает объект `OcrResult`, содержащий извлечённую строку, оценки уверенности и даже ограничивающие рамки, если позже понадобится выделить текст. Здесь происходит магия — ваша программа наконец **распознаёт текст с изображения**.

## Шаг 5: Выведите распознанный текст

Наконец, выведите результат в консоль или передайте его в другую систему (база данных, поисковый индекс и т.д.). Свойство `Text` содержит очищенную строку.

```csharp
// Step 5: Show the extracted text
Console.WriteLine("📝 Recognized text:");
Console.WriteLine(result.Text);
```

Типичный вывод для примера тайской вывески может выглядеть так:

```
📝 Recognized text:
สวัสดีประเทศไทย
```

Если уверенность низкая, вы можете проверить `result.Confidence` и решить, стоит ли повторить попытку с изображением более высокого разрешения.

## Обработка распространённых граничных случаев

### 1️⃣ Размер и качество изображения

Точность OCR резко падает на размытых или маленьких изображениях. Хорошее правило: **минимум 300 dpi** для печатных документов и как минимум **800 px** по длинной стороне для фотографий. Если вы не можете контролировать источник, рассмотрите возможность увеличения масштаба с помощью бикубического алгоритма перед передачей в движок.

### 2️⃣ Несколько языков

Если ваше изображение содержит несколько скриптов (например, английский и тайский), установите язык в `OcrLanguage.Multi` или передайте массив языков, если библиотека это поддерживает.

```csharp
engine.Language = OcrLanguage.Multi; // or new[] { OcrLanguage.Thai, OcrLanguage.English }
```

### 3️⃣ Управление памятью

При обработке множества изображений в цикле не забывайте освобождать потоки и экземпляры движка, чтобы избежать утечек памяти.

```csharp
using var engine = new OcrEngine(); // ensures Dispose is called
```

### 4️⃣ Отчёт об ошибках

Обёрните вызов OCR в блок try/catch. Некоторые движки бросают `OcrException`, когда не удаётся загрузить языковой пакет.

```csharp
try
{
    var result = engine.Read(ocrImage);
    Console.WriteLine(result.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❗ OCR failed: {ex.Message}");
}
```

## Полный рабочий пример

Ниже представлен полный готовый к копированию и вставке код программы, который **распознаёт текст с изображения** с использованием описанных выше шагов. Сохраните его как `Program.cs` в проекте, созданном ранее.

```csharp
using System;
using System.IO;
using IronOcr;

class Program
{
    static void Main()
    {
        // 1️⃣ Define the image path
        var imagePath = Path.Combine(Environment.CurrentDirectory, "thai_sign.png");
        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"❌ Image not found: {imagePath}");
            return;
        }

        // 2️⃣ Load the image (load image for OCR)
        using var imageStream = new FileStream(imagePath, FileMode.Open, FileAccess.Read);
        var ocrInput = OcrInput.FromStream(imageStream);

        // 3️⃣ Create and configure the OCR engine
        using var engine = new OcrEngine();
        engine.Language = OcrLanguage.Thai; // download on first use

        // 4️⃣ Perform recognition (recognize text from image)
        var result = engine.Read(ocrInput);

        // 5️⃣ Output the extracted text (extract text from image)
        Console.WriteLine("📝 Recognized text:");
        Console.WriteLine(result.Text);
    }
}
```

**Ожидаемый вывод в консоль**

```
📝 Recognized text:
สวัสดีประเทศไทย
```

Запустите его командой `dotnet run`. Если всё настроено правильно, вы увидите напечатанную тайскую фразу, подтверждая, что приложение может **распознавать текст с изображения** за считанные секунды.

## Визуальный обзор

![Diagram illustrating the recognize text from image pipeline: load image → configure OCR engine → run recognition → get extracted text](/images/ocr-pipeline.png)

*Текст alt:* *иллюстрация конвейера распознавания текста с изображения*

## Итоги и дальнейшие шаги

Мы только что создали **c# ocr example**, который загружает изображение, настраивает язык, запускает движок и выводит извлечённую строку — по сути полный рабочий процесс **c# image to text**. Теперь вы знаете, как **загрузить изображение для OCR**, как **извлечь текст из изображения**, и как справляться с наиболее распространёнными подводными камнями.

Хотите пойти дальше? Попробуйте следующие идеи:

- **Batch processing:** Обойдите папку с PDF‑файлами или фотографиями и сохраняйте каждый результат в базе данных.
- **Bounding‑box visualization:** Используйте коллекцию `result.Words` для рисования прямоугольников вокруг обнаруженного текста.
- **Hybrid approaches:** Скомбинируйте OCR с регулярными выражениями, чтобы извлекать номера телефонов, даты или суммы счетов.
- **Cloud services:** Замените локальный движок на Azure Computer Vision, если вам нужна масштабируемость.

### Есть вопросы?

Не стесняйтесь оставить комментарий — будь то проблемы с языковым пакетом, нужна помощь с предобработкой изображений или просто хотите поделиться своей историей успеха. Приятного кодинга и наслаждайтесь превращением картинок в поисковый текст!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, основанные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Извлечение текста из изображения C# с выбором языка с помощью Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Как выполнить извлечение текста из изображения из потока с использованием Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Извлечение текста из изображения — оптимизация OCR с Aspose.OCR для .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}