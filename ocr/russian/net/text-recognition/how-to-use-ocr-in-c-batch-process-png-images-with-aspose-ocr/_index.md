---
category: general
date: 2026-02-14
description: Как использовать OCR в C# для быстрого извлечения текста из PNG‑файлов.
  Узнайте, как выполнять пакетное распознавание изображений, обрабатывать несколько
  изображений и использовать Aspose OCR C# в одном руководстве.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: ru
og_description: Как использовать OCR в C# с Aspose OCR C#. Этот учебник показывает,
  как извлекать текст из PNG‑файлов, выполнять пакетное OCR изображений и эффективно
  обрабатывать несколько изображений.
og_title: Как использовать OCR в C# — пакетное извлечение текста из PNG
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Как использовать OCR в C# – пакетная обработка PNG‑изображений с помощью Aspose
  OCR
url: /ru/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

fine.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в C# – пакетная обработка PNG‑изображений с Aspose OCR

Когда‑нибудь задавались вопросом, **как использовать OCR**, чтобы извлечь текст из множества PNG‑файлов без написания отдельной процедуры для каждого? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужно **извлекать текст из PNG**‑ресурсов в масштабе, особенно когда изображения находятся в папке и требуется запускать OCR‑движок для каждого файла.

В этом руководстве мы пройдём через готовое, полностью рабочее решение, которое **пакетно распознаёт изображения**, **обрабатывает несколько изображений** параллельно и использует мощную библиотеку **Aspose OCR C#**. К концу вы получите один исполняемый файл, который читает любое количество PNG‑файлов, извлекает их текст и выводит результаты в консоль — всё это с помощью нескольких строк кода.

## Требования

- .NET 6.0 или новее (код работает также с .NET Core и .NET Framework)  
- Действительная лицензия Aspose.OCR for .NET (или бесплатная trial‑версия) — её можно получить на сайте Aspose.  
- Папка, содержащая PNG‑файлы, которые нужно прочитать.  
- Visual Studio 2022 (или любой совместимый с C# IDE).  

Дополнительные пакеты NuGet не требуются, кроме `Aspose.OCR`.

## Шаг 1: Как использовать OCR – Инициализация движка Aspose OCR

Первое, что вам понадобится, — экземпляр класса `Engine`. Этот объект абстрагирует подлежащую OCR‑технологию и может работать на CPU или GPU, в зависимости от вашего оборудования и лицензии.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Почему это важно:* Инициализация движка один раз и повторное его использование в разных потоках экономит память и избавляет от накладных расходов на многократную загрузку OCR‑моделей. Это также гарантирует одинаковые настройки для всех изображений.

## Шаг 2: Извлечение текста из PNG – Сбор путей к изображениям

Далее нам нужна коллекция путей к файлам. В реальном проекте вы, вероятно, будете считывать каталог динамически, но для наглядности перечислим несколько примеров.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*Подсказка:* Замените `YOUR_DIRECTORY` на абсолютный или относительный путь к вашим изображениям. Если файлов десятки, вместо ручного списка можно использовать `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`.

## Шаг 3: Пакетное OCR‑распознавание изображений – Параллельный запуск

Последовательная обработка изображений проста, но медленна. С помощью `Parallel.ForEach` мы можем **обрабатывать несколько изображений** одновременно, используя многопоточность процессора.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*Почему параллельно?* Каждый вызов OCR требует значительных ресурсов CPU, но независим от остальных, поэтому их одновременный запуск может существенно сократить общее время выполнения, особенно на машине с 4‑ядерным процессором и более.

## Шаг 4: Обработка нескольких изображений – Вывод извлечённого текста

Теперь, когда у нас есть коллекция объектов `OcrResult`, мы можем пройтись по ней и вывести распознанный текст. Обычно здесь сохраняют результат в базе данных или записывают в файлы, но вывод в консоль делает пример компактным.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Ожидаемый вывод в консоль (пример):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

Если какое‑то изображение не удаётся загрузить, Aspose бросит исключение; вы можете обернуть вызов `engine.Recognize` в блок `try/catch`, чтобы логировать ошибки без прерывания всей партии.

## Шаг 5: Полный рабочий пример – Все части вместе

Ниже представлен полный код программы, который можно скопировать в новый консольный проект C#. В нём присутствуют все `using`‑директивы и финальный цикл вывода.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### Запуск примера

1. Создайте новый проект **Console App** в Visual Studio.  
2. Добавьте пакет **Aspose.OCR** через NuGet (`Install-Package Aspose.OCR`).  
3. Замените `YOUR_DIRECTORY` на путь к папке с вашими PNG‑файлами.  
4. Скомпилируйте и запустите — вы должны увидеть извлечённый текст в консоли.

## Полезные советы и особые случаи

- **GPU‑ускорение:** Если у вас совместимая видеокарта и лицензия Aspose OCR, включите её через `EngineSettings` перед созданием движка. Это может сократить время обработки каждого изображения на несколько секунд.  
- **Большие файлы:** Для изображений размером более 10 МБ рекомендуется предварительно уменьшать их, чтобы снизить нагрузку на память.  
- **Поддержка языков:** По умолчанию движок предполагает английский. Установите `engine.Language = Language.French;` (или любой поддерживаемый язык), чтобы повысить точность распознавания неанглийского текста.  
- **Обработка ошибок:** `try/catch` внутри параллельного цикла гарантирует, что повреждённый файл не прервет всю партию. Вы также можете записывать ошибки в файл для последующего анализа.  
- **Хранение результатов:** Вместо вывода в консоль можно записать `result.Text` в файл `.txt` с помощью `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`.

## Заключение

Теперь вы знаете, **как использовать OCR** в C# для **извлечения текста из PNG**‑файлов, **пакетного OCR‑распознавания изображений** и **эффективной обработки нескольких изображений** с помощью Aspose OCR C#. Решение полностью автономно, работает параллельно и легко масштабируется до сотен и тысяч файлов с минимальными изменениями.

Готовы к следующему шагу? Попробуйте заменить вывод в консоль на генерацию CSV‑отчёта, поэкспериментировать с GPU‑ускорением или передать распознанный текст в поисковый индекс. Возможности безграничны, а основной шаблон — инициализировать один раз, запускать параллельно, аккуратно обрабатывать ошибки — будет полезен в любой конвейерной системе обработки изображений.

Удачной разработки и пусть ваши OCR‑задачи будут быстрыми и безошибочными!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}