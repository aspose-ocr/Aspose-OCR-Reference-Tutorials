---
category: general
date: 2026-02-19
description: Узнайте, как выполнять пакетное OCR с помощью Aspose.OCR в C#. Это руководство
  покажет, как эффективно извлекать текст из изображений и конвертировать изображения
  в txt.
draft: false
keywords:
- how to batch ocr
- extract text from images
- convert images to txt
- Aspose OCR batch processing
- C# image to text conversion
language: ru
og_description: Как выполнять пакетное OCR с Aspose.OCR на C#. Извлекайте текст из
  изображений и конвертируйте их в txt за несколько простых шагов.
og_title: Как выполнять пакетное OCR в C# – быстрое преобразование изображений в текст
tags:
- OCR
- C#
- Aspose
title: Как выполнять пакетное OCR в C# — быстро извлекать текст из изображений
url: /ru/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять пакетное OCR в C# – Полное пошаговое руководство

Когда‑нибудь задавались вопросом **how to batch OCR** целой папки изображений без написания отдельной программы для каждого файла? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужно извлечь текст из десятков — а иногда и тысяч — отсканированных страниц, чеков или скриншотов. Хорошая новость? С Aspose.OCR вы можете автоматизировать весь процесс, **extract text from images**, и **convert images to txt** всего несколькими строками.

В этом руководстве мы пройдем через полностью готовый к запуску пример, который показывает, как именно настроить OCR batch processor, настроить предобработку, управлять параллелизмом и записывать каждый результат в файл `.txt`. К концу вы получите автономное консольное приложение, которое можно добавить в любой проект .NET.

## Что понадобится

- .NET 6.0 или новее (код работает также на .NET Core и .NET Framework)
- NuGet‑пакет Aspose.OCR для .NET (`Aspose.OCR`)  
- Папка, заполненная файловыми изображениями (`.png`, `.jpg` и т.д.), которые нужно обработать
- Умеренный объём ОЗУ; в демонстрации используется 4 параллельных потока, но вы можете изменить это

Никаких внешних сервисов, никаких скрытых файлов конфигурации — только чистый C# код, который вы можете скомпилировать и запустить уже сегодня.

![Diagram illustrating how to batch ocr processing flow](/images/how-to-batch-ocr-flow.png "how to batch ocr flow diagram")

## Шаг 1: Установите Aspose.OCR и настройте проект

Сначала добавьте пакет Aspose.OCR в ваш проект:

```bash
dotnet add package Aspose.OCR
```

Почему это важно: Aspose.OCR включает OCR‑движок, языковые данные и утилиты предобработки, поэтому вам не понадобятся сторонние бинарные файлы. После установки пакета создайте новое консольное приложение (или добавьте код в существующее) и подключите необходимые пространства имён:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
```

Эти директивы `using` предоставляют доступ к классам batch processor и удобным вспомогательным средствам ввода‑вывода.

## Шаг 2: Настройте OCR Batch Processor

Теперь мы создадим экземпляр `OcrBatchProcessor` и укажем, какой язык искать, как очищать изображения и сколько потоков запускать параллельно. Это ядро эффективного **how to batch ocr**.

```csharp
// Step 2: Create and configure the OCR batch processor
var ocrBatch = new OcrBatchProcessor
{
    // Language selection – English is the most common, but you can change it
    Language = Language.English,

    // Preprocessing improves accuracy; Deskew removes rotation
    Preprocessing = new PreprocessingOptions
    {
        Deskew = DeskewAdvanced.Enable()
    },

    // Parallelism – adjust based on your CPU/GPU capabilities
    MaxDegreeOfParallelism = 4
};
```

**Зачем включать Deskew?** Многие отсканированные документы не выровнены идеально; алгоритм deskew вращает их обратно к прямой базовой линии, что часто повышает точность распознавания на 10‑15 %.

## Шаг 3: Подключите обратный вызов результата для сохранения текстовых файлов

Batch processor генерирует событие для каждого обработанного изображения. Мы подпишемся на `ResultProcessed`, чтобы записывать каждый результат OCR в файл `.txt` — фактически **convert images to txt** на лету.

```csharp
// Step 3: Register a callback to save each OCR result as a text file
ocrBatch.ResultProcessed += (sender, args) =>
{
    // Change the original file extension to .txt
    string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");

    // Write the recognized text to the new file
    File.WriteAllText(txtPath, args.Result.Text);

    // Inform the console for debugging / progress monitoring
    Console.WriteLine($"Processed: {args.ImagePath}");
};
```

Быстрый совет: если нужно сохранить оригинальную структуру папок, вы можете изменить `txtPath`, включив подпапки или отдельный каталог вывода.

## Шаг 4: Запустите пакетную обработку вашей папки с изображениями

Осталось лишь указать процессору папку, содержащую изображения, из которых вы хотите **extract text from images**. Метод `ProcessFolder` рекурсивно сканирует подпапки, так что вы можете разместить целое дерево сканов, а библиотека справится с остальным.

```csharp
// Step 4: Run the batch on all image files in the target folder
ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
```

При запуске программы вы увидите вывод в консоль, похожий на:

```
Processed: C:\Path\To\Your\Images\invoice1.png
Processed: C:\Path\To\Your\Images\receipt_2024.jpg
...
```

Каждое изображение теперь имеет соседний файл `.txt` с извлечённым текстом.

## Полный рабочий пример

Объединив всё вместе, представляем полный код программы, который можно скопировать и вставить в `Program.cs`:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR batch processor
        var ocrBatch = new OcrBatchProcessor
        {
            Language = Language.English,
            Preprocessing = new PreprocessingOptions
            {
                Deskew = DeskewAdvanced.Enable()
            },
            // Step 2: Define the level of parallelism (adjust for your CPU/GPU)
            MaxDegreeOfParallelism = 4
        };

        // Step 3: Register a callback to save each OCR result as a text file
        ocrBatch.ResultProcessed += (sender, args) =>
        {
            string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");
            File.WriteAllText(txtPath, args.Result.Text);
            Console.WriteLine($"Processed: {args.ImagePath}");
        };

        // Step 4: Run the batch on all image files in the target folder
        ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
    }
}
```

### Ожидаемый вывод

- Для каждого `*.png` или `*.jpg` в исходном каталоге появляется соответствующий файл `*.txt` рядом с ним.
- Консоль выводит строку для каждого файла, предоставляя живую обратную связь.
- Если изображение нельзя прочитать (повреждённый файл, неподдерживаемый формат), Aspose.OCR записывает ошибку в журнал, но продолжает обработку остальных — благодаря встроенной надёжности batch engine.

## Часто задаваемые вопросы и особые случаи

### Что если нужно обрабатывать PDF вместо изображений?

Aspose.OCR может принимать страницы PDF как изображения внутри, но сначала потребуется преобразовать PDF в растровые изображения (например, с помощью Aspose.PDF). После получения PNG тот же пакетный код будет работать без изменений.

### Можно ли менять язык «на лету»?

Да. Свойство `Language` принимает любое значение перечисления `Language` (Spanish, French, Chinese и т.д.). Если у вас многоязычные документы, рассмотрите возможность выполнения двух проходов — по одному для каждого языка — или используйте `Language.AutoDetect`.

### Как ограничить пакетную обработку определёнными типами файлов?

`ProcessFolder` принимает необязательный `SearchOption` и `string[] extensions`. Пример:

```csharp
ocrBatch.ProcessFolder(@"C:\Images", new[] { ".png", ".tif" });
```

### Что насчёт ускорения с помощью GPU?

Aspose.OCR поддерживает GPU через конфигурацию `OcrEngine`, но основной параметр параллелизма по‑прежнему `MaxDegreeOfParallelism` в batch processor. Если у вас совместимый GPU, включите его в настройках движка перед созданием `OcrBatchProcessor`.

### Как обрабатывать очень большие папки (десятки тысяч файлов)?

- Осторожно увеличивайте `MaxDegreeOfParallelism`; слишком много потоков может исчерпать память.
- Используйте отдельный каталог вывода, чтобы избежать захламления.
- Периодически сбрасывайте логи на диск, чтобы предотвратить рост потребления памяти.

## Профессиональные советы для OCR высокого качества

- **Важен DPI**: Изображения с 300 DPI и выше дают наилучшую точность. Если ваши сканы имеют более низкое разрешение, рассмотрите масштабирование с бикубическим фильтром перед обработкой.
- **Уменьшение шума**: Включите `Preprocessing.NoiseRemoval`, если исходные изображения зернистые.
- **Именование файлов**: Держите имена файлов короткими и буквенно‑цифровыми; специальные символы могут сбивать логику пути в обратном вызове.
- **Логирование**: Замените `Console.WriteLine` на полноценный логгер (например, `Serilog`) для производственных нагрузок.

## Следующие шаги

Теперь, когда вы освоили **how to batch OCR**, вы можете:

- **Extract text from images** и передать результат в поисковый индекс (например, Elasticsearch) для полнотекстового поиска.
- **Convert images to txt**, а затем выполнить обработку естественного языка (NLP) для автоматической классификации документов.
- Поэкспериментировать с **different language packs** или пользовательскими словарями для отраслевой терминологии.

Если вас интересует пост‑обработка, ознакомьтесь с руководствами «Разбор вывода OCR с помощью регулярных выражений» или «Сохранение результатов OCR в базе данных SQL».

---

**Счастливого кодинга!** Не стесняйтесь менять параллелизм, добавлять дополнительные шаги предобработки или упаковать всё в Windows‑service для непрерывного мониторинга. Возможности безграничны, когда вы сочетаете пакетные возможности Aspose.OCR с небольшим .NET‑вдохновением.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}