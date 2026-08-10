---
category: general
date: 2026-02-19
description: Создайте поисковый PDF из изображения на C# с использованием Aspose OCR.
  Узнайте, как извлечь текст из изображения и преобразовать его в PDF с возможностью
  поиска.
draft: false
keywords:
- create searchable pdf
- extract text from image
- image to searchable pdf
- ocr image c#
- searchable pdf from image
language: ru
og_description: Создайте PDF с возможностью поиска из изображения на C# с помощью
  Aspose OCR. Этот учебник пошагово показывает, как извлечь текст из изображения и
  создать PDF с возможностью поиска.
og_title: Создание поискового PDF из изображения в C# – Полное руководство
tags:
- C#
- OCR
- PDF
title: Создание поискового PDF из изображения в C# – Полное руководство
url: /ru/net/text-recognition/create-searchable-pdf-from-image-in-c-complete-guide/
---

them unchanged.

Now produce final content with all translations and placeholders.

Check for any missed items: The blockquote "Quick note" and "Pro tip" kept bold. The table headers translated. All code block placeholders kept.

Make sure to preserve markdown formatting exactly.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из изображения в C# – Полное руководство

Когда‑нибудь вам нужно было **create searchable PDF** из отсканированного контракта, но вы не знали, с чего начать? Вы не одиноки; многие разработчики сталкиваются с этой проблемой, когда впервые работают с OCR‑ориентированными процессами. Хорошая новость в том, что с несколькими строками C# и Aspose OCR вы можете за секунды превратить любой растровый файл (TIFF, JPEG, PNG…) в поисковый PDF.  

В этом руководстве мы пройдем весь процесс — от установки библиотеки, извлечения текста из изображения, до записи окончательного файла **image to searchable PDF**. По пути мы также коснёмся того, как **extract text from image** для других сценариев, и почему «скрытый текстовый слой» важен для последующих поисковых систем.

> **Quick note:** Весь код ниже готов к запуску; вам не нужно искать дополнительные фрагменты или внешнюю документацию.

## Что понадобится

Прежде чем погрузиться, убедитесь, что у вас есть следующие предварительные требования:

| Требование | Зачем это нужно |
|--------------|----------------|
| .NET 6 SDK (or later) | Современные возможности языка и лучшая производительность |
| Visual Studio 2022 (or VS Code) | IDE с IntelliSense упрощает работу |
| Aspose.OCR NuGet package | Предоставляет OCR‑движок и запись PDF |
| A sample image (`input.tif`) | Исходный файл, который вы преобразуете в поисковый PDF |

Если у вас уже есть .NET‑проект, вы можете пропустить шаг «Create a new project» и сразу перейти к установке NuGet.

## Шаг 1: Установить пакет Aspose OCR NuGet

Сначала — добавьте библиотеку, которая делает всю тяжёлую работу.

```bash
dotnet add package Aspose.OCR
```

Эта однострочная команда подтягивает основной OCR‑движок, записыватель PDF и все нативные зависимости. В Visual Studio вы также можете щёлкнуть правой кнопкой по проекту → **Manage NuGet Packages** → найти *Aspose.OCR* и нажать **Install**.

> **Pro tip:** Держите пакет в актуальном состоянии. На сегодняшний день (фев 2026) версия 23.9 — последняя и включает улучшения производительности для высокоразрешённых TIFF.

## Шаг 2: Настроить каркас проекта

Создайте простое консольное приложение, если у вас его ещё нет:

```bash
dotnet new console -n PdfDemo
cd PdfDemo
```

Откройте `Program.cs` (или `PdfDemo.cs`, если предпочитаете именованный класс) и удалите код по умолчанию «Hello World». Мы заменим его полным, исполняемым примером, который **creates searchable PDF** из изображения.

## Шаг 3: Инициализировать OCR‑движок – «Extract Text from Image»

OCR‑движок должен знать, на каком языке вы сканируете. Для большинства английских контрактов вы укажете `Language.English`. Если у вас многоязычные документы, Aspose поддерживает языковые пакеты, которые можно загрузить позже.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;

class PdfDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine and set the language to English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // 2️⃣ Perform OCR on the input image – this is where we **extract text from image**
        OcrResult ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/input.tif");

        // 3️⃣ Write the OCR result to a searchable PDF (image + hidden text layer)
        PdfResultWriter.Write(ocrResult, @"YOUR_DIRECTORY/contract_searchable.pdf");

        // 4️⃣ Notify that the PDF has been created
        Console.WriteLine("Searchable PDF created.");
    }
}
```

### Почему мы инициализируем движок таким образом

* **Language selection** указывает распознавателю, какой набор символов ожидать, что значительно повышает точность.  
* **`RecognizeImage`** возвращает `OcrResult`, содержащий как оригинальный битмап, так и извлечённый Unicode‑текст. Это двойное представление и позволяет выполнить конверсию **image to searchable PDF** позже.

## Шаг 4: Записать скрытый текстовый слой – генерация **Image to Searchable PDF**

`PdfResultWriter` принимает `OcrResult` и создаёт PDF, где каждая страница отображает оригинальное растровое изображение **плюс** невидимый текстовый слой. Поисковые системы (и просмотрщики PDF) могут индексировать этот скрытый текст, делая документ поисковым.

```csharp
// Inside Main, after OCR succeeds
PdfResultWriter.Write(ocrResult, @"YOUR_DIRECTORY/contract_searchable.pdf");
```

Внутри Aspose внедряет текст с помощью атрибута PDF *ActualText*. Если открыть полученный файл в Adobe Acrobat и выполнить выделение текста, вы увидите, что можно скопировать скрытые слова, хотя они отображаются как часть изображения.

## Шаг 5: Проверить результат

Запустите программу:

```bash
dotnet run
```

Вы должны увидеть:

```
Searchable PDF created.
```

Перейдите в `YOUR_DIRECTORY` и откройте `contract_searchable.pdf`. Попробуйте выделить слово — если выделение охватывает невидимый текст, вы успешно **create searchable pdf** из исходного изображения.

### Быстрая проверка

*Откройте PDF в извлекателе текста (например, Adobe Reader → Edit → Copy). Если вы можете вставить читаемый текст, скрытый слой работает.* Если получаются искажённые символы, проверьте, что исходное изображение имеет достаточное разрешение (300 dpi — хорошая отправная точка).

## Шаг 6: Обработка распространённых граничных случаев

### Сканирование с низким разрешением

Если ваш TIFF ниже 200 dpi, точность OCR может пострадать. Масштабирование изображения перед распознаванием (с помощью `System.Drawing` или `ImageSharp`) часто даёт лучшие результаты.

```csharp
using System.Drawing;

// Load, upscale, then feed to OCR
Bitmap lowRes = new Bitmap(@"YOUR_DIRECTORY/input.tif");
Bitmap highRes = new Bitmap(lowRes, new Size(lowRes.Width * 2, lowRes.Height * 2));
highRes.Save(@"YOUR_DIRECTORY/upscaled.tif");
```

### Многостраничные документы

При работе с многостраничными TIFF, перебирайте каждый кадр:

```csharp
using System.Drawing.Imaging;

// Assume input.tif contains multiple frames
using (Image multiPage = Image.FromFile(@"YOUR_DIRECTORY/input.tif"))
{
    int pageCount = multiPage.GetFrameCount(FrameDimension.Page);
    for (int i = 0; i < pageCount; i++)
    {
        multiPage.SelectActiveFrame(FrameDimension.Page, i);
        string tempPath = $@"YOUR_DIRECTORY/page_{i}.tif";
        multiPage.Save(tempPath, ImageFormat.Tiff);

        OcrResult pageResult = ocrEngine.RecognizeImage(tempPath);
        PdfResultWriter.Write(pageResult, $@"YOUR_DIRECTORY/page_{i}_searchable.pdf");
    }
}
```

Затем вы можете объединить отдельные PDF, используя Aspose.PDF или любую другую PDF‑библиотеку.

## Полный рабочий пример (Все шаги в одном файле)

Ниже представлен полный, автономный код программы, который вы можете скопировать‑вставить в `Program.cs`. Он охватывает установку, OCR, генерацию PDF и простой обработчик ошибок.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;

class PdfDemo
{
    static void Main()
    {
        // Path to the source image – adjust to your environment
        const string inputPath = @"YOUR_DIRECTORY/input.tif";
        const string outputPath = @"YOUR_DIRECTORY/contract_searchable.pdf";

        try
        {
            // 👉 Step 1: Initialize OCR engine (English language)
            OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

            // 👉 Step 2: Run OCR – this **extracts text from image**
            Console.WriteLine("Running OCR on image...");
            OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

            // 👉 Step 3: Convert OCR result to a searchable PDF
            Console.WriteLine("Creating searchable PDF...");
            PdfResultWriter.Write(ocrResult, outputPath);

            Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

### Ожидаемый результат

* Файл с именем `contract_searchable.pdf` появляется в вашем каталоге.  
* Открывая его в любом просмотрщике PDF, вы видите оригинальное сканирование, но при выделении текста копируются реальные слова.  
* Поиск по документу (Ctrl + F) мгновенно находит извлечённые термины.

## Часто задаваемые вопросы

**Q: Работает ли это с другими языками?**  
A: Абсолютно. Замените `Language.English` на `Language.French`, `Language.German` и т.д., или загрузите пользовательский языковой пакет из Aspose.

**Q: Что если мне нужен полностью текстовый PDF?**  
A: После OCR вы можете пропустить изображение и использовать `PdfResultWriter.WriteTextOnly(ocrResult, path)` (доступно в новых версиях Aspose).

**Q: Можно ли внедрить шрифты для улучшения отображения?**  
A: Да. Записыватель PDF автоматически внедряет набор стандартных шрифтов, но вы можете предоставить пользовательский объект `PdfSaveOptions`, если нужны корпоративные шрифты.

## Итоги

Мы только что **create searchable pdf** из изображения с помощью C# и Aspose OCR, охватив всё от **extract text from image** до конечного файла **image to searchable pdf**. Этот фрагмент готов к продакшн‑использованию, и теперь у вас есть надёжная база для обработки больших пакетов, разных языков или даже интеграции процесса в веб‑API.

### Что дальше?

* Попробуйте конвертировать всю папку сканов в один объединённый поисковый PDF.  
* Поэкспериментируйте с функциями шифрования Aspose PDF, чтобы

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}