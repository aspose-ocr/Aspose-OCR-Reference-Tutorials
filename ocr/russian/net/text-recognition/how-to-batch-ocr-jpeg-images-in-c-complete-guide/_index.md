---
category: general
date: 2026-02-22
description: Как выполнять пакетное OCR JPEG‑изображений в C# с помощью Aspose.OCR.
  Узнайте, как извлекать текст из JPG, конвертировать JPG в TXT и эффективно обрабатывать
  изображения пакетно.
draft: false
keywords:
- how to batch ocr
- extract text from jpg
- convert jpg to txt
- batch process images
- c# ocr example
language: ru
og_description: Как пакетно выполнять OCR JPEG‑изображений в C# с использованием Aspose.OCR.
  Этот учебник покажет, как извлекать текст из JPG, конвертировать JPG в TXT и пакетно
  обрабатывать изображения за считанные минуты.
og_title: Как выполнять пакетное OCR JPEG‑изображений в C# – Полное руководство
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Как пакетно выполнять OCR JPEG‑изображений в C# – Полное руководство
url: /ru/net/text-recognition/how-to-batch-ocr-jpeg-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как пакетно выполнять OCR JPEG‑изображений в C# – Полное руководство

Когда‑нибудь задавались вопросом **как пакетно выполнять OCR** папки, полной картинок, без написания отдельной программы для каждого файла? В этом руководстве мы покажем, как **пакетно выполнять OCR** JPEG‑файлов с помощью Aspose.OCR, чтобы **извлекать текст из jpg** и **конвертировать jpg в txt** всего несколькими строками кода.  

Если вы когда‑либо смотрели на каталог отсканированных счетов и думали: «Должен быть более быстрый способ», вы попали по адресу. Мы пройдем каждый шаг, объясним, почему каждый элемент важен, и даже добавим несколько профессиональных советов по работе с большими пакетами.

## Что вы создадите

К концу этого урока у вас будет небольшое консольное приложение, которое:

* Сканирует заданный каталог в поисках файлов `*.jpg`.  
* Отправляет каждое изображение в движок Aspose OCR (с ускорением GPU, если у вас есть подходящая видеокарта).  
* Записывает распознанный текст в файл `.txt`, который находится рядом с оригинальной картинкой.  

Никаких внешних сервисов, никакого ручного копирования‑вставки — только чистый C# и надёжная OCR‑библиотека.

### Предварительные требования

* .NET 6.0 или новее (код также работает на .NET Framework 4.8).  
* Visual Studio 2022 или любой редактор, поддерживающий C#.  
* Пакет Aspose.OCR NuGet (бесплатная пробная версия подходит для тестов).  

Если чего‑то не хватает, остановитесь сейчас и установите, остальные части руководства предполагают, что всё уже готово.

![Как выполнить пакетный OCR пример](/images/how-to-batch-ocr.png "диаграмма пакетного OCR")

## Шаг 1: Установите пакет Aspose.OCR NuGet

Первое, что нужно сделать — добавить OCR‑библиотеку в проект. Откройте терминал в папке решения и выполните:

```bash
dotnet add package Aspose.OCR
```

Или используйте UI менеджера пакетов NuGet в Visual Studio. Это скачает всё необходимое, включая бинарники с поддержкой GPU, если ваш компьютер её поддерживает.

> **Pro tip:** Если планируете запускать приложение на сервере без GPU, позже установите `UseGpu = false`; движок автоматически переключится на CPU.

## Шаг 2: Настройте OCR‑движок

Создание и настройка `OcrEngine` — это начало магии. Вы укажете, какой язык ожидать, использовать ли GPU и в каком формате выводить результат.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 2: Initialize and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most documents; change if you need another language.
    Language = Language.English,

    // Enable GPU for faster processing on supported hardware.
    UseGpu = true,

    // We only need plain text for our .txt files.
    OutputFormat = OutputFormat.Text
};
```

**Почему это важно:** Установка `Language` повышает точность, потому что движок может сузить набор символов. Включение `UseGpu` может сократить время обработки вдвое на современной видеокарте, что реально помогает при **пакетной обработке изображений**.

## Шаг 3: Распознайте все JPEG‑файлы в папке

Теперь Aspose возьмёт на себя тяжёлую работу. Статический метод `BatchProcessor.RecognizeFolder` проходит по каталогу, запускает OCR для каждого подходящего файла и возвращает коллекцию результатов.

```csharp
using System.Collections.Generic;

// ...

// Step 3: Run OCR on every *.jpg in the target directory
IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
    ocrEngine,
    @"C:\Images\Invoices",   // <-- replace with your folder path
    searchPattern: "*.jpg"); // Only JPEG files are processed
```

**Обработка граничных случаев:** Если в папке есть подпапки, можно добавить перегрузку с `SearchOption.AllDirectories` (или рекурсивно обходить вручную), чтобы не пропустить файлы.

## Шаг 4: Запишите каждый результат в соответствующий файл `.txt`

Объекты `OcrResult` содержат исходный путь к файлу и распознанный текст. Пройдитесь по ним, измените расширение и запишите вывод.

```csharp
using System.IO;

// ...

// Step 4: Persist OCR results as .txt files next to the source images
foreach (var result in ocrResults)
{
    // Change "image.jpg" → "image.txt"
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");

    // Save the extracted text
    File.WriteAllText(txtFilePath, result.Text);
}
```

И всё — каждый JPEG теперь имеет соседний текстовый файл, который можно передать в последующие процессы, поисковые индексы или просто архивировать.

## Шаг 5: Запустите приложение и проверьте вывод

Соберите и запустите программу:

```bash
dotnet run
```

Предположим, в папке находятся `invoice1.jpg` и `receipt2.jpg`; вы должны увидеть появившиеся `invoice1.txt` и `receipt2.txt` рядом с ними. Откройте любой из `.txt`‑файлов; вы увидите «сырой» OCR‑вывод, например:

```
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

Если текст выглядит искажённым, проверьте, что исходные изображения имеют высокий контраст и что свойство `Language` соответствует языку документа.

## Шаг 6: Продвинутые настройки (по желанию)

### a) Обработка низкокачественных сканов

Иногда JPEG‑файлы шумные. Можно предварительно обработать изображения с помощью Aspose.Imaging или любой другой библиотеки:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

// Example: increase contrast before OCR
using (var image = Image.Load(result.SourceFilePath))
{
    image.Contrast = 30; // boost contrast
    image.Save(result.SourceFilePath); // overwrite or save to temp file
}
```

### b) Параллелизация пакета

Если файлов много и процессор многопоточный, оберните цикл в `Parallel.ForEach`:

```csharp
Parallel.ForEach(ocrResults, result =>
{
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
    File.WriteAllText(txtFilePath, result.Text);
});
```

Только имейте в виду, что сам движок Aspose OCR не является потокобезопасным; понадобится отдельный экземпляр `OcrEngine` для каждого потока или использование конкурентной очереди.

### c) Логирование и обработка ошибок

Надёжное решение записывает ошибки, чтобы их можно было повторно обработать позже:

```csharp
try
{
    // OCR and write logic here
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {result.SourceFilePath}: {ex.Message}");
    // Optionally write to a log file
}
```

## Полный рабочий пример

Собрав всё вместе, получаем полную программу, которую можно скопировать‑вставить в новый консольный проект:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create and configure the OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = Language.English,
            UseGpu = true,
            OutputFormat = OutputFormat.Text
        };

        // 2️⃣ Recognize all JPEG images in the target folder
        IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
            ocrEngine,
            @"C:\Images\Invoices",   // <-- change to your directory
            searchPattern: "*.jpg");

        // 3️⃣ Write each OCR result to a matching .txt file
        foreach (var result in ocrResults)
        {
            string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
            File.WriteAllText(txtFilePath, result.Text);
        }

        Console.WriteLine("Batch OCR complete. Check the folder for .txt files.");
    }
}
```

Запустите её, наблюдайте вывод в консоли, а затем откройте несколько `.txt`‑файлов, чтобы убедиться, что шаг **извлечения текста из jpg** выполнен успешно.  

---

## Заключение

Мы только что рассмотрели, **как пакетно выполнять OCR** набора JPEG‑изображений в C# с помощью Aspose.OCR, превращая каждую картинку в поисковый файл `.txt`. Решение компактно, учитывает GPU и легко расширяется для обработки ошибок, предобработки изображений или параллельного выполнения.  

Если хотите идти дальше, рассмотрите следующие шаги:

* **Пакетно обрабатывать изображения** других форматов (`*.png`, `*.tif`), изменив `searchPattern`.  
* Объединить вывод с полнотекстовым поисковым движком, например Lucene.NET, для мгновенного поиска по документам.  
* Исследовать возможности Aspose по конвертации в PDF, чтобы напрямую создавать поисковые PDF из результатов OCR.  

Экспериментируйте — меняйте язык, отключайте GPU или передавайте текст в базу данных. Основной шаблон остаётся тем же, а теперь у вас есть надёжный фундамент для дальнейшего развития.

Счастливого кодинга, и пусть ваши OCR‑конвейеры будут быстрыми и точными!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}