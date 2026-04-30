---
category: general
date: 2026-04-29
description: Быстро выполняйте пакетное распознавание изображений с помощью Aspose
  OCR на C#. Узнайте, как извлекать текст из файлов JPG, читать текст со сканов и
  обрабатывать список изображений параллельно.
draft: false
keywords:
- batch OCR images
- extract text from jpg
- read text from scans
- parallel OCR processing
- process image list
language: ru
og_description: Быстро выполняйте пакетное OCR изображений с Aspose OCR. В этом руководстве
  показано, как извлекать текст из JPG, считывать текст со сканов и обрабатывать список
  изображений параллельно.
og_title: Пакетное OCR изображений в C# – Параллельный OCR JPG‑сканов
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Пакетное OCR изображений в C# – Параллельное OCR JPG‑сканов
url: /ru/net/ocr-optimization/batch-ocr-images-in-c-parallel-ocr-of-jpg-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Пакетное OCR изображений в C# – Параллельное OCR JPG‑сканов

Когда‑нибудь вам нужно было **batch OCR images**, но вы не знали, как масштабировать работу на несколько файлов? Вы не одиноки — разработчики часто сталкиваются с проблемой, когда пытаются читать текст из сканов по одному. Хорошая новость в том, что с Aspose OCR вы можете **extract text from jpg** файлы, **read text from scans**, и **process image list** элементы параллельно, используя всего несколько строк C#.

В этом руководстве мы пройдем полный, готовый к запуску пример, который точно показывает, как это сделать. К концу вы получите автономное консольное приложение, которое распознает папку с JPEG‑сканами, выводит текст каждой страницы и сообщает, сколько времени заняла каждая операция. Никаких внешних документов, никаких неполных фрагментов кода — только полное решение, которое вы можете вставить в Visual Studio и запустить.

## Что понадобится

- **.NET 6.0** или новее (код также компилируется на .NET Framework 4.6+).
- **Aspose.OCR** пакет NuGet (`Install-Package Aspose.OCR`)
- Небольшой набор JPG‑файлов или отсканированных изображений, которые вы хотите обработать
- Любая IDE по вашему выбору; я использую Visual Studio 2022, но VS Code тоже отлично подходит

Вот и всё. Если у вас уже есть пакет NuGet, вы готовы к работе.

## Шаг 1 – Инициализация OCR Engine (Batch OCR Images Setup)

Первое, что мы делаем, — создаём экземпляр `OcrEngine` и указываем, какой язык искать. В большинстве случаев достаточно английского, но вы можете заменить `OcrLanguage.English` на любой поддерживаемый язык.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine and set the language to English
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };
```

*Почему это важно:* Инициализация движка один раз и повторное его использование для всех изображений гораздо эффективнее, чем создание нового экземпляра для каждого файла. Это также позволяет Aspose делить внутренние ресурсы, что необходимо для **parallel OCR processing**.

## Шаг 2 – Формирование списка изображений (Process Image List)

Далее мы определяем коллекцию путей к файлам, которые хотим передать в пакетный распознаватель. Вы можете генерировать этот список динамически с помощью `Directory.GetFiles`, но для наглядности мы зададим несколько записей вручную.

```csharp
        // Step 2: Define the image files that will be processed
        var imagePaths = new List<string>
        {
            @"YOUR_DIRECTORY/page1.jpg",
            @"YOUR_DIRECTORY/page2.jpg",
            @"YOUR_DIRECTORY/page3.jpg"
        };
```

*Подсказка:* Если у вас тысячи сканов, рассмотрите использование `Directory.EnumerateFiles` с фильтром, например `*.jpg`, чтобы не загружать весь список в память сразу.

## Шаг 3 – Запуск пакетного распознавания (Parallel OCR Processing)

Теперь переходим к сути: вызов `BatchRecognize`. Метод принимает аргумент `maxDegreeOfParallelism`, который определяет, сколько потоков Aspose запустит. По умолчанию используется четыре потока, но вы можете увеличить их количество, если ваш процессор имеет больше ядер.

```csharp
        // Step 3: Run batch recognition (4 parallel threads by default)
        var recognitionResults = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);
```

*Что происходит под капотом?* Aspose разбивает коллекцию `imagePaths` на части, передаёт каждую часть отдельному потоку и агрегирует результаты. Это самый эффективный способ **extract text from jpg** файлов, когда у вас есть **process image list**, который можно обрабатывать одновременно.

## Шаг 4 – Вывод результатов (Read Text from Scans)

Наконец, мы проходим по коллекции `recognitionResults` и выводим текст каждого файла и время обработки. Объект `OcrResult` также предоставляет имя исходного файла, что полезно при необходимости вести журнал или сохранять результат.

```csharp
        // Step 4: Output the results for each image
        foreach (var result in recognitionResults)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

**Ожидаемый вывод (пример):**

```
File: C:\Scans\page1.jpg
Time: 1.34s
The quick brown fox jumps over the lazy dog.
----------------------------------------
File: C:\Scans\page2.jpg
Time: 1.27s
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----------------------------------------
File: C:\Scans\page3.jpg
Time: 1.41s
Invoice #12345
Total: $1,250.00
----------------------------------------
```

Обратите внимание, как каждый блок показывает имя файла, длительность OCR и извлечённый текст. Это именно та информация, которая нужна, когда вы **reading text from scans** в производственном конвейере.

## Обработка распространённых граничных случаев

| Ситуация | На что обратить внимание | Быстрое решение |
|-----------|-------------------|-----------|
| **Missing file** | `FileNotFoundException` выбрасывается внутри `BatchRecognize` | Проверьте пути с помощью `File.Exists` перед добавлением в `imagePaths`. |
| **Unsupported format** | Aspose обрабатывает только растровые изображения (JPG, PNG, BMP, TIFF). | Сначала преобразуйте PDF в изображения (используйте Aspose.PDF) или пропустите эти файлы. |
| **Memory pressure** | Очень большие изображения могут перегрузить ОЗУ при работе многих потоков. | Уменьшите `maxDegreeOfParallelism` или измените размер изображений перед OCR. |
| **Non‑English text** | Язык, установленный как English, пропустит другие скрипты. | Измените `Language = OcrLanguage.French` (или используйте многократную комбинацию). |

Эти советы делают ваш пакетный процесс надёжным, особенно когда вы **processing an image list**, полученный из пользовательских загрузок или сканированного архива.

## Профессиональный совет – Настройка параллелизма

Если запускать это на машине с 8‑ядерным процессором, увеличьте параллелизм до 6 или 8 и наблюдайте рост скорости. Однако помните, что каждый поток также потребляет память для bitmap. Хорошее практическое правило:

```csharp
int cores = Environment.ProcessorCount;
int maxThreads = Math.Max(1, cores - 1); // leave one core free for UI/OS
```

Подставьте `maxThreads` в `BatchRecognize` для динамической, учитывающей возможности машины конфигурации.

## Полный рабочий пример (готов к копированию и вставке)

Ниже полный код программы, готовый к компиляции. Просто замените `YOUR_DIRECTORY` на путь к папке с вашими JPG‑сканами.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine – English language
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };

        // 2️⃣ Build the list of image files to process
        var imagePaths = new List<string>();
        string folder = @"C:\Scans"; // <-- change this
        foreach (var file in Directory.EnumerateFiles(folder, "*.jpg"))
        {
            imagePaths.Add(file);
        }

        if (imagePaths.Count == 0)
        {
            Console.WriteLine("No JPG files found in the specified folder.");
            return;
        }

        // 3️⃣ Run batch OCR – let the library use 4 threads (adjust as needed)
        var results = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);

        // 4️⃣ Output each result
        foreach (var result in results)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

> **Примечание:** Строка `using System.IO;` необходима для вспомогательного класса `Directory`. Код выводит дружелюбное сообщение, если JPG‑файлы не найдены, предотвращая тихий сбой.

## Заключение

Мы только что продемонстрировали чистый процесс **batch OCR images**, который **extracts text from jpg** файлы, **reads text from scans**, и эффективно **processes an image list** с помощью **parallel OCR processing**. Полный, исполняемый пример показывает, как именно настроить движок, передать ему коллекцию файлов и обработать результаты — всё это при контроле использования памяти и количества потоков.

Готовы к следующему шагу? Попробуйте сменить язык на французский, добавить конвертацию PDF‑в‑изображения или сохранять OCR‑текст в базе данных. Схема остаётся той же: инициализировать один раз, передать список и позволить Aspose выполнять тяжёлую работу параллельно.

Есть вопросы или хотите поделиться своими доработками? Оставьте комментарий ниже, и удачной разработки! 

![Batch OCR images processing flow](https://example.com/placeholder.png "Diagram illustrating batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}