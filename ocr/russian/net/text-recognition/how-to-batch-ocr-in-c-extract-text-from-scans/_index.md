---
category: general
date: 2026-05-06
description: Изучите, как выполнять пакетное распознавание текста (OCR) в C# и быстро
  извлекать текст из сканов с помощью Aspose OCR Batch. Следуйте полному пошаговому
  руководству с кодом, советами и обработкой крайних случаев.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: ru
og_description: Как выполнять пакетное OCR в C#? Это руководство покажет, как эффективно
  извлекать текст из сканов с помощью Aspose OCR, поддержки GPU и параллельной обработки.
og_title: Как выполнять пакетное OCR в C# – извлечение текста из сканов
tags:
- C#
- OCR
- Aspose
title: Как выполнять пакетное OCR в C# – извлекать текст из сканов
url: /ru/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять пакетное OCR в C# – извлечение текста из сканов

Когда‑нибудь задавались вопросом **как выполнить пакетное OCR**, имея папку, полную отсканированных PDF‑ов или JPEG‑ов? Вы не одиноки, глядя на гору изображений и думая: «Должен быть более быстрый способ вытянуть текст». В этом руководстве мы пройдём практическое решение, которое не только позволяет **извлекать текст из сканов**, но и ускоряется за счёт GPU‑ускорения и параллелизма.

Дело в том, что выполнять OCR по одному файлу за раз — огромный расход времени, особенно если у вас десятки или сотни страниц. К концу этого руководства у вас будет готовое к запуску консольное приложение C#, которое обрабатывает весь каталог одной командой, выдавая чистые текстовые файлы, готовые к индексации, поиску или чему‑угодно ещё.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

- **.NET 6.0 или новее** (код использует современные возможности C#).
- **Лицензия Aspose.OCR** (бесплатная пробная версия подходит для тестов).
- Машина с поддержкой GPU **если хотите включить `UseGpu`**; иначе библиотека будет работать на CPU.
- Базовые знания **консольных приложений C#**.

Никаких внешних сервисов, никаких скрытых файлов конфигурации — только SDK и папка с изображениями.

## Шаг 1: Установите NuGet‑пакет Aspose.OCR

Сначала добавьте библиотеку Aspose OCR в ваш проект. Откройте терминал в папке решения и выполните:

```bash
dotnet add package Aspose.OCR
```

Это загрузит `Aspose.OCR` и его пространство имён для пакетной обработки, которое мы будем использовать для **пакетного OCR** позже.

> **Совет:** Если вы работаете в Visual Studio, пакет можно добавить через UI NuGet Package Manager.

## Шаг 2: Создайте каркас консольного приложения

Настроим минимальное консольное приложение, которое будет хостить наш пакетный процессор. Создайте новый файл `Program.cs` и вставьте следующий каркас:

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll configure and run the OCR batch processor here.
        }
    }
}
```

Почему логика помещена в `Main`? Потому что консольное приложение даёт мгновенную обратную связь через `Console.WriteLine`, что идеально для быстрой проверки завершения **пакетного OCR** задания.

## Шаг 3: Настройте OcrBatchProcessor

Теперь к «мясу» решения. Мы создадим экземпляр `OcrBatchProcessor`, укажем входную папку, место для результатов и подправим несколько параметров производительности.

```csharp
// Step 3: Configure the OCR batch processor
var batch = new OcrBatchProcessor
{
    // Folder that contains the source images to be processed
    InputFolder = @"YOUR_DIRECTORY/Scans",

    // Folder where the OCR results will be saved
    OutputFolder = @"YOUR_DIRECTORY/OcrResults",

    // Specify the language of the documents (Spanish in this example)
    Language = OcrLanguage.Spanish,

    // Enable GPU acceleration for faster processing (if available)
    UseGpu = true,

    // Limit the number of concurrent OCR operations
    MaxDegreeOfParallelism = 4
};
```

### Почему эти настройки важны

| Настройка | Что делает | Когда может потребоваться изменить |
|----------|------------|------------------------------------|
| `InputFolder` | Путь к сканам, которые нужно обработать. | Используйте относительный путь для переносимости. |
| `OutputFolder` | Куда будет сохраняться извлечённый текст каждого изображения в виде файла `.txt`. | Укажите сетевой ресурс, если нужен централизованный хранитель. |
| `Language` | Языковая модель OCR; в примере выбрана испанская для демонстрации поддержки нескольких языков. | Переключите на `OcrLanguage.English` или любой поддерживаемый язык. |
| `UseGpu` | Переносит тяжёлые матричные вычисления на GPU. | Установите `false` на серверах без GPU. |
| `MaxDegreeOfParallelism` | Определяет, сколько изображений обрабатывается одновременно. | Уменьшите на слабых CPU, чтобы избежать перегрузки. |

## Шаг 4: Выполните пакетную операцию с обработкой ошибок

Запуск пакета сводится к вызову `Execute()`, но мы обернём его в блок try‑catch, чтобы вывести понятное сообщение в случае ошибки (например, отсутствие папки или неподдерживаемый формат изображения).

```csharp
try
{
    // Step 4: Run the batch OCR operation
    batch.Execute();

    // Step 5: Inform the user that processing has finished
    Console.WriteLine("Batch completed.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
}
```

Когда процессор завершит работу, в консоли появится **Batch completed.**, а для каждого исходного изображения будет создан соответствующий файл `.txt` в папке `OcrResults`. Имена файлов совпадают с оригиналами, что упрощает сопоставление с исходным сканом.

## Шаг 5: Проверьте вывод – чего ожидать

После выполнения программы откройте любой файл внутри `YOUR_DIRECTORY/OcrResults`. Вы должны увидеть обычный текст, извлечённый из соответствующего изображения, например:

```
Este es un documento de prueba.
Contiene varias líneas de texto.
```

Если вывод выглядит «крякозябрами», проверьте, что параметр `Language` соответствует языку ваших сканов. Aspose OCR поддерживает более 100 языков, так что вы можете заменить `OcrLanguage.Spanish` на нужный вам.

## Обработка граничных случаев и типичные подводные камни

### 1. GPU недоступен

Если в вашей машине нет совместимого GPU, `UseGpu = true` тихо переключится в режим CPU, но вы потеряете ускорение. Чтобы быть уверенным, можно явно проверять наличие GPU:

```csharp
if (!OcrBatchProcessor.IsGpuSupported)
{
    batch.UseGpu = false;
    Console.WriteLine("GPU not detected – falling back to CPU processing.");
}
```

### 2. Большие файлы, превышающие память

При работе с массивными TIFF‑ами или PDF‑ами рекомендуется предварительно разбить их на более мелкие изображения. Aspose OCR умеет обрабатывать многостраничные PDF, но потребление памяти растёт с количеством страниц. Простой предобработочный шаг с использованием `Aspose.Imaging` может нарезать документ на управляемые части.

### 3. Неизображения в папке ввода

Пакетный процессор игнорирует файлы, которые он не может распарсить, но лучше поддерживать папку в чистоте. Можно отфильтровать по расширению:

```csharp
batch.InputFolder = @"YOUR_DIRECTORY/Scans";
batch.FileFilter = file => file.EndsWith(".png", StringComparison.OrdinalIgnoreCase)
                         || file.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase);
```

*(Примечание: `FileFilter` — гипотетическое свойство; замените реальным API, если оно существует.)*

## Полный рабочий пример

Ниже полностью готовая к копированию и вставке программа. Замените `YOUR_DIRECTORY` на абсолютный путь к вашей машине.

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Configure the batch processor
            var batch = new OcrBatchProcessor
            {
                InputFolder = @"C:\MyScans",          // <-- change this
                OutputFolder = @"C:\OcrResults",     // <-- change this
                Language = OcrLanguage.Spanish,
                UseGpu = true,
                MaxDegreeOfParallelism = 4
            };

            // Optional: fall back to CPU if no GPU is found
            if (!OcrBatchProcessor.IsGpuSupported)
            {
                batch.UseGpu = false;
                Console.WriteLine("GPU not detected – using CPU.");
            }

            try
            {
                // Run the batch job
                batch.Execute();

                Console.WriteLine("Batch completed.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### Ожидаемый вывод в консоль

```
Batch completed.
```

А в `C:\OcrResults` вы найдёте файл `.txt` для каждого изображения из `C:\MyScans`.

## Заключение

Теперь у вас есть надёжный, готовый к продакшну способ **выполнять пакетный OCR** в C# и **извлекать текст из сканов** без необходимости открывать каждый файл вручную. Используя пакетный API Aspose, GPU‑ускорение и настраиваемый параллелизм, решение масштабируется от нескольких страниц до тысяч.

Что дальше? Попробуйте следующие идеи:

- **Интегрировать с поисковым индексом** (например, Elasticsearch), чтобы сделать извлечённый текст доступным для поиска.
- **Добавить пост‑обработку**: проверку орфографии, определение языка и т.д.
- **Обернуть консольное приложение в Windows Service** для постоянного мониторинга папки‑приёмника.

Экспериментируйте, меняйте уровень параллелизма или язык модели. Если возникнут проблемы, оставляйте комментарий ниже — удачного OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}