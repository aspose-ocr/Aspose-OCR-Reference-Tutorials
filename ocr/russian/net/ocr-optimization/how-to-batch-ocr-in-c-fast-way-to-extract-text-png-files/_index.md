---
category: general
date: 2026-04-03
description: Узнайте, как выполнять пакетное распознавание OCR с помощью Aspose.OCR
  в C#. Это руководство покажет, как извлекать текст из PNG‑изображений и эффективно
  преобразовывать изображения в текст.
draft: false
keywords:
- how to batch ocr
- extract text png
- convert images to text
- Aspose OCR
- C# parallel processing
language: ru
og_description: Узнайте, как выполнять пакетное OCR в C# для извлечения текста из
  PNG‑изображений и преобразования изображений в текст с помощью Aspose.OCR. Включён
  полный код.
og_title: Как выполнять пакетное OCR в C# – Быстрое руководство
tags:
- OCR
- C#
- Aspose
title: Как выполнять пакетное OCR в C# – быстрый способ извлечения текста из PNG‑файлов
url: /ru/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить Batch OCR в C# – Быстрый способ извлечения текста из PNG‑файлов

Задумывались ли вы когда‑нибудь **как выполнить batch OCR** целой папки скриншотов без написания цикла для каждого файла? Вы не одиноки. Во многих проектах — например, оцифровка счетов или архивирование отсканированных чеков — вы получаете десятки, иногда сотни PNG‑файлов, из которых нужно извлечь текст. Хорошая новость? С Aspose.OCR вы можете **извлекать текст из PNG** изображений параллельно, и весь процесс можно уместить в несколько строк C#.

В этом руководстве мы пройдемся по полному, готовому к запуску примеру, который покажет, как **convert images to text** с помощью пакетного процессора. Мы рассмотрим предварительные требования, объясним, почему важна каждая строка, и даже добавим несколько pro‑tips, чтобы вы не столкнулись с распространёнными подводными камнями.

## Требования

- **.NET 6.0** (или новее), установленный на вашем компьютере. Более старые среды работают, но последняя обеспечивает лучшую производительность и поддержку async.
- Пакет **Aspose.OCR for .NET**. Вы можете установить его через NuGet: `dotnet add package Aspose.OCR`.
- Папка, полная **PNG**‑изображений, которые вы хотите обработать. В дальнейшем мы будем ссылаться на неё как `YOUR_DIRECTORY`.
- Умеренный объём ОЗУ — пакетный OCR может потреблять много памяти при высокой параллельности, но использование `Environment.ProcessorCount` делает процесс безопасным.

> **Pro tip:** Если вы используете CI/CD конвейер, добавьте файл лицензии Aspose как секрет, чтобы избежать ограничения в 20 страниц бесплатной оценки.

А теперь приступим.

## Шаг 1: Настройте Batch OCR Processor (Primary Keyword in Header)

Первое, что вам нужно — это экземпляр `BatchOcrProcessor`. Этот класс абстрагирует логику потоков и позволяет сосредоточиться на том, что делать с каждым изображением.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Create a batch OCR processor and tell it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };
```

**Why this matters:**  
- `Engine = new OcrEngine()` дает вам свежий OCR‑движок для каждого потока, избегая конфликтов.  
- `MaxDegreeOfParallelism = Environment.ProcessorCount` автоматически масштабируется под количество ядер, обеспечивая максимальную пропускную способность без ручной настройки.

## Шаг 2: Подключите события прогресса (Helps Track Extraction)

Отслеживание прогресса критично при обработке сотен файлов. Событие `ProgressChanged` срабатывает после завершения каждого файла, позволяя записать статус.

```csharp
        // Subscribe to progress updates so we know which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");
```

**Why you’ll love it:**  
- Обратная связь в реальном времени не даёт задуматься, «зависло ли приложение».  
- Если понадобится пауза или отмена, у вас уже есть точка доступа к `e.Current` и `e.Total`.

## Шаг 3: Определите сканирование папки и шаблон файлов (Extract Text PNG)

Теперь мы указываем процессору, где искать и какие файлы обрабатывать. Шаблон `"*.png"` гарантирует, что будут обрабатываться только PNG‑изображения.

```csharp
        // Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"YOUR_DIRECTORY",          // folder containing the images
            "*.png",                    // file pattern
            (imagePath, ocrText) =>     // callback for each processed file
            {
                // Step 4 is inside this callback – see next section
            });
```

**Why this is key:**  
- Использование glob‑шаблона делает код гибким; замените `*.png` на `*.jpg`, если позже понадобится обрабатывать JPEG.  
- Обратный вызов получает как путь к изображению, так и распознанный текст, предоставляя полный контроль над дальнейшими действиями.

## Шаг 4: Сохраните распознанный текст рядом с исходником (Convert Images to Text)

Внутри обратного вызова мы запишем результат OCR в файл `.txt`, который будет находиться рядом с оригинальным PNG. Это самый простой способ **convert images to text** для последующей обработки.

```csharp
                // Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
```

**Why we choose a side‑by‑side `.txt` file:**  
- Связь между файлами очевидна — откройте PNG, откройте TXT, сравните.  
- Нет необходимости в базе данных или дополнительном слое хранения в небольших проектах.

## Шаг 5: Завершите с дружелюбным сообщением о завершении

Аккуратное сообщение в консоли сообщает, когда всё завершено.

```csharp
        // Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

При запуске программы вы увидите вывод вроде:

```
Processed 1/27: C:\Images\invoice1.png
Processed 2/27: C:\Images\invoice2.png
...
Batch processing completed.
```

Каждый PNG теперь имеет соседний файл `.txt` с извлечённым текстом.

## Полный рабочий пример (Все шаги вместе)

Ниже представлен весь код, который можно скопировать‑вставить в новый консольный проект. Ничего не пропущено — просто замените `YOUR_DIRECTORY` на абсолютный путь к вашим изображениям.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create a batch OCR processor and configure it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 2: Subscribe to progress updates to see which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");

        // Step 3: Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"C:\MyImages",          // folder containing the images
            "*.png",                // file pattern
            (imagePath, ocrText) => // callback for each processed file
            {
                // Step 4: Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
            });

        // Step 5: Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

### Ожидаемый результат

- Для каждого `image.png` в `C:\MyImages` рядом появляется `image.txt`.  
- Консоль выводит строки прогресса, облегчая мониторинг больших пакетов.  
- Нет ручных циклов или управления потоками — `BatchOcrProcessor` делает всё за вас.

## Часто задаваемые вопросы и особые случаи

### Что если мои изображения не PNG?

Просто измените второй аргумент в `ProcessFolder` на `"*.jpg"` или `"*.*"`, чтобы включить все файлы. OCR‑движок работает с большинством растровых форматов.

### Сколько памяти это потребляет?

`BatchOcrProcessor` загружает по одному изображению на каждый поток. При `Environment.ProcessorCount`, скажем, 8 ядер, одновременно будет находиться в памяти восемь изображений. Если возникнут исключения OutOfMemory, уменьшите степень параллелизма:

```csharp
MaxDegreeOfParallelism = 4; // or any number that fits your machine
```

### Можно ли настроить язык OCR?

Конечно. После создания движка задайте его свойство `Language`:

```csharp
Engine = new OcrEngine { Language = Language.English };
```

Aspose поддерживает множество языков; при необходимости добавьте соответствующий пакет NuGet.

### Как обрабатывать ошибки?

Обёрните обратный вызов в блок try/catch и фиксируйте сбои. Процессор продолжит работу со следующим файлом, не позволяя одной повреждённой картинке прервать весь запуск.

```csharp
(imagePath, ocrText) =>
{
    try
    {
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, ocrText);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {imagePath}: {ex.Message}");
    }
}
```

## Pro Tips для масштабирования

- **Chunk the folder**: Если у вас десятки тысяч файлов, разбейте их на подпапки и запускайте несколько пакетных задач последовательно.  
- **Use a cloud VM**: Машина с большим количеством ядер (например, 32‑core) завершит работу значительно быстрее. Не забудьте скорректировать ограничения лицензии.  
- **Post‑process the text**: После извлечения вы можете запускать регулярные выражения для получения номеров счетов или дат. Файлы `.txt` идеально подходят в качестве входных данных для таких конвейеров.

## Заключение

Теперь у вас есть надёжный, готовый к продакшну рецепт **how to batch OCR** каталога PNG‑файлов, **extract text PNG** файлов и **convert images to text** с помощью Aspose.OCR в C#. Пример самодостаточен, объясняет «почему» каждой строки и содержит советы по работе с большими объёмами или другими типами файлов.

Готовы к следующему шагу? Попробуйте изменить обратный вызов, чтобы отправлять результаты в базу данных, или добавить предобработку изображений (например, выравнивание) перед OCR. Этот шаблон легко масштабируется, так что вы сможете адаптировать его под любую задачу пакетной обработки.

Happy coding, and may your OCR pipelines be fast and error‑free!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}