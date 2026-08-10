---
category: general
date: 2026-03-21
description: Как упростить пакетное OCR в C# — научитесь извлекать текст из изображений,
  преобразовывать изображения в текст и сохранять OCR как текст с настройками языка.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: ru
og_description: Пакетное OCR в C# позволяет извлекать текст из изображений, преобразовывать
  изображения в текст и сохранять OCR в виде текста, при этом легко задавать язык
  OCR.
og_title: Как выполнять пакетное OCR в C# – быстрое руководство
tags:
- OCR
- C#
- Aspose
title: Как выполнять пакетное OCR в C# – быстро извлекать текст из изображений
url: /ru/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять пакетный OCR в C# – Быстро извлекать текст из изображений

Задумывались ли вы когда‑нибудь **как выполнить пакетный OCR**, когда у вас есть сотни изображений, лежащих в папке? Вы не одиноки — разработчики постоянно спрашивают, как извлечь текст из изображений без написания цикла для каждого файла. Хорошая новость в том, что Aspose.OCR предоставляет чистый, готовый к параллельной обработке способ **преобразовать изображения в текст** всего в несколько строк кода C#.

В этом руководстве мы пройдемся по полному, готовому к запуску примеру, который покажет, как **сохранить OCR как текст**, выбрать правильный язык и включить параллельную обработку для ускорения. К концу вы получите автономное решение, которое можно добавить в любой проект .NET.

## Что понадобится

- .NET 6 или новее (API работает с .NET Core и .NET Framework)
- Aspose.OCR для .NET (пакет NuGet `Aspose.OCR`)
- Папка с изображениями, которые нужно обработать (PNG, JPEG, TIFF и т.д.)
- Небольшой интерес к параллельному программированию (необязательно, но полезно)

Никаких дополнительных сервисов, никаких облачных ключей — только чистый код C#, который работает локально.

---

![диаграмма процесса пакетного OCR](placeholder.png){alt="диаграмма процесса пакетного OCR"}

## Шаг 1: Настройте проект и установите Aspose.OCR

Для начала создайте консольное приложение (или используйте существующее) и добавьте пакет Aspose.OCR:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Если вы используете Visual Studio, щелкните правой кнопкой мыши по проекту → *Manage NuGet Packages* → найдите *Aspose.OCR* и установите последнюю стабильную версию.

Это даст вам доступ к `OcrBatchProcessor`, `OcrEngineSettings` и перечислению `Language`.

## Шаг 2: Определите папки ввода и вывода

Пакетному процессору необходимо знать, где находятся исходные изображения и куда следует записывать извлечённые текстовые файлы. Держите пути абсолютными или относительными к корню проекта — просто убедитесь, что папки существуют перед запуском кода.

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

> **Почему это важно:** Если папка вывода отсутствует, процессор выбросит исключение, прервав весь пакет. Создание её заранее гарантирует плавный запуск.

## Шаг 3: Настройте параметры OCR (включая язык)

Здесь вы **устанавливаете язык OCR** для всего пакета. Aspose.OCR поддерживает десятки языков; по умолчанию — английский, но вы можете переключиться на французский, испанский и т.д., изменив значение перечисления `Language`.

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

Если вам понадобится обрабатывать разные языки для каждого изображения, вы позже сможете переопределить эту настройку для отдельного файла — подробнее об этом позже.

## Шаг 4: Создайте объект `OcrBatchProcessor`

Теперь мы связываем всё вместе. `OcrBatchProcessor` позволяет указать папку ввода, папку вывода, формат вывода, параметры параллелизма и общие настройки, которые мы только что создали.

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

> **Зачем параллелизм?** Когда у вас есть десятки или сотни изображений, обработка их по одному может быть мучительно медленной. Установка `MaxDegreeOfParallelism` в 4 позволяет среде выполнения использовать четыре ядра процессора одновременно, резко сокращая общее время на типичной рабочей станции.

## Шаг 5: Запустите пакетную операцию

После настройки процессора выполнение сводится к единому вызову метода. Библиотека автоматически обрабатывает перечисление файлов, OCR и запись результатов.

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

Когда консоль выведет *“Batch OCR completed.”*, вы найдете файл `.txt` рядом с каждым оригинальным изображением в папке `BatchResults`. Каждый текстовый файл содержит необработанные символы, извлечённые из исходного изображения — именно то, что нужно для **извлечения текста из изображений** для последующей обработки.

### Ожидаемый вывод

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

Откройте любой из этих файлов, и вы увидите простое текстовое представление содержимого изображения.

## Шаг 6: Проверьте результаты (необязательно)

Хорошая привычка — дважды проверить несколько файлов, чтобы убедиться, что OCR работает как ожидалось. Быстрый способ — прочитать первую строку каждого сгенерированного файла и вывести её в консоль:

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

Если вы заметите искажённые символы, рассмотрите возможность смены настройки `Language` или корректировки качества изображения (например, увеличить DPI, преобразовать в градации серого).

## Расширенные варианты и граничные случаи

### 1. Переопределение языка для отдельного файла
Иногда пакет содержит многоязычные документы. Вы можете проверять имя каждого изображения и назначать язык «на лету»:

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. Разные форматы вывода
Если вам нужны поисковые PDF вместо простого текста, измените `OutputFormat`:

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

Это **преобразует изображения в текст** внутри PDF‑контейнера, сохраняя оригинальное расположение.

### 3. Обработка больших изображений
Очень высокое разрешение изображений может перегрузить память. Чтобы процесс оставался лёгким, включите понижение разрешения изображения:

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. Журналирование ошибок
Процессор бросает исключения для нечитаемых файлов. Оберните `Execute` в try/catch и запишите проблемные имена файлов в журнал:

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## Полный рабочий пример

Объединив всё вместе, представляем полностью готовую к копированию и вставке программу:

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

Сохраните это как `Program.cs`, соберите проект и запустите `dotnet run`. Вы увидите вывод консоли, подтверждающий завершение, а затем короткий предварительный просмотр извлечённого текста.

---

## Заключение

Мы только что рассмотрели **как выполнять пакетный OCR** в C# с помощью Aspose.OCR, показав, как **извлекать текст из изображений**, **преобразовывать изображения в текст** и **сохранять OCR как текст**, одновременно **устанавливая язык OCR** в соответствии с вашим содержимым. Пример полностью рабочий, включает параллельную обработку для ускорения и предоставляет возможности для продвинутых сценариев, таких как переопределение языка для отдельного файла или вывод в PDF.

Готовы к следующему шагу? Попробуйте заменить `OcrOutputFormat.PlainText` на `SearchablePdf` и посмотрите, насколько просто генерировать поисковые PDF. Или поэкспериментируйте с различными значениями `MaxDegreeOfParallelism`, чтобы выжать каждый последний миллисекунд на многопроцессорной машине.

Если возникнут проблемы, дважды проверьте пути к папкам, убедитесь, что изображения читаются, и проверьте, что значение перечисления языка соответствует тексту на ваших картинках. Счастливого кодинга, и пусть ваши пакетные OCR будут быстрыми и точными!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}