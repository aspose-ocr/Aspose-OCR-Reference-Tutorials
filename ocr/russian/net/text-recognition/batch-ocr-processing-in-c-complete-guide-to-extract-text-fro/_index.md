---
category: general
date: 2026-06-16
description: Пакетная обработка OCR в C# позволяет быстро преобразовывать изображения
  в текст. Узнайте, как извлекать текст из изображений с помощью Aspose.OCR, используя
  пошаговый код.
draft: false
keywords:
- batch OCR processing
- extract text from images
- convert images to text
language: ru
og_description: Пакетная обработка OCR в C# преобразует изображения в текст. Следуйте
  этому руководству, чтобы извлечь текст из изображений с помощью Aspose.OCR.
og_title: Пакетная обработка OCR в C# – извлечение текста из изображений
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  headline: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  type: TechArticle
- description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  name: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  steps:
  - name: Expected Output
    text: 'Assuming you have three images (`invoice1.png`, `receipt2.jpg`, `form3.tif`)
      in the input folder, the output folder will contain:'
  - name: What if some images fail to process?
    text: '`OcrBatchProcessor` logs errors to the console by default and continues
      with the next file. For production use, you can subscribe to the `OnError` event
      to collect failed filenames and retry later.'
  - name: Can I process PDFs directly?
    text: Yes. Aspose.OCR treats each page of a PDF as an image internally. Just point
      `InputFolder` to a directory containing PDFs, and the processor will extract
      text from every page—effectively **convert images to text** even when the source
      is a PDF.
  - name: How do I handle multi‑language documents?
    text: Set `Language` to `OcrLanguage.Multilingual` or specify a list of languages
      if the library version supports it. The engine will attempt to recognize characters
      from all provided languages, which is handy for international invoices.
  - name: What about memory consumption?
    text: The batch processor streams each image, so memory usage stays low even with
      thousands of files. However, enabling a high `MaxDegreeOfParallelism` on a memory‑constrained
      machine could cause spikes. Monitor your RAM and adjust the thread count accordingly.
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: Пакетная обработка OCR в C# – Полное руководство по извлечению текста из изображений
url: /ru/net/text-recognition/batch-ocr-processing-in-c-complete-guide-to-extract-text-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Пакетная обработка OCR в C# – Полное руководство по извлечению текста из изображений

Когда‑то задумывались, как выполнить **пакетную обработку OCR** в C# без написания отдельного цикла для каждой картинки? Вы не одиноки. Когда у вас десятки — а иногда и сотни отсканированных чеков, счетов или рукописных заметок, вручную передавать каждый файл в OCR‑движок быстро превращается в кошмар.  

Хорошие новости? С Aspose.OCR вы можете *преобразовать изображения в текст* одной аккуратной операцией. В этом руководстве мы пройдем весь рабочий процесс: от установки библиотеки до запуска готовой к продакшену пакетной задачи, которая **извлекает текст из изображений** и сохраняет результаты в нужном вам формате.

> **Что вы получите:** готовое консольное приложение, которое обрабатывает всю папку, записывает файлы простого текста (или JSON, XML, HTML, PDF) рядом с оригиналами и показывает, как настроить параллелизм для максимальной пропускной способности.

## Требования

- .NET 6.0 SDK или новее (код работает как с .NET Core, так и с .NET Framework)
- Visual Studio 2022, VS Code или любой другой редактор C#
- Лицензия Aspose.OCR NuGet (бесплатный пробный период подходит для оценки)
- Папка с файлами изображений (`.png`, `.jpg`, `.tif` и т.д.), которые вы хотите **преобразовать изображения в текст**

Если все пункты отмечены, приступаем.

![Diagram illustrating batch OCR processing flow](batch-ocr-workflow.png "Batch OCR processing flow")

## Шаг 1: Установите Aspose.OCR через NuGet

Сначала добавьте пакет Aspose.OCR в ваш проект. Откройте терминал в каталоге проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

Или, если вы работаете в Visual Studio, щелкните правой кнопкой мыши *Dependencies → Manage NuGet Packages*, найдите **Aspose.OCR** и нажмите *Install*. Эта одна строка подтянет всё необходимое для **пакетной обработки OCR**.

> **Совет:** Держите версию пакета актуальной; последняя версия (по состоянию на июнь 2026) добавляет поддержку новых форматов изображений и улучшает многоязычную точность.

## Шаг 2: Создайте скелет консольного приложения

Создайте новое консольное приложение C# (если ещё не сделали) и замените сгенерированный `Program.cs` следующим скелетом. Обратите внимание на директиву `using Aspose.OCR;` в начале — это пространство имён, которое предоставляет класс `OcrBatchProcessor`.

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // We'll fill this in later.
    }
}
```

На данный момент файл — лишь заглушка, но это чистая отправная точка для нашей логики **пакетной обработки OCR**.

## Шаг 3: Инициализируйте OcrBatchProcessor

`OcrBatchProcessor` — это движок, который сканирует папку, запускает OCR для каждого поддерживаемого изображения и записывает результат. Создать его так просто:

```csharp
// Step 3: Create an OCR batch processor instance
var ocrBatchProcessor = new OcrBatchProcessor();
```

Зачем использовать пакетный процессор вместо API для одиночного изображения? Класс пакета автоматически обрабатывает перечисление файлов, журналирование ошибок и даже параллельное выполнение, что экономит время на написание циклов и позволяет сосредоточиться на точности.

## Шаг 4: Укажите входные и выходные папки

Сообщите процессору, откуда читать изображения и куда сохранять результаты. Замените пути‑заполнители реальными каталогами на вашем компьютере.

```csharp
// Step 4: Configure the input folder containing images to process
ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

// Step 5: Set the folder where OCR results will be saved
ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";
```

Обе папки должны существовать до запуска приложения; иначе вы получите `DirectoryNotFoundException`. Создать их программно можно, но для ясности пример оставлен простым.

## Шаг 5: Выберите формат вывода

Aspose.OCR может выдавать простой текст, JSON, XML, HTML или даже PDF. Для большинства сценариев **извлечения текста из изображений** достаточно простого текста, но при желании можно переключиться на другой формат.

```csharp
// Step 6: Choose the desired output format (e.g., plain text)
ocrBatchProcessor.OutputFormat = ResultFormat.Text;   // alternatives: Json, Xml, Html, Pdf, etc.
```

Если нужны структурированные данные для последующей обработки, `ResultFormat.Json` — хороший выбор. Библиотека автоматически обернёт текст каждой страницы в JSON‑объект, сохраняя информацию о разметке.

## Шаг 6: Установите язык и параллелизм

Точность OCR зависит от правильной языковой модели. Английский подходит для большинства западных документов, но вы можете выбрать любой поддерживаемый язык (Arabic, Chinese и т.д.). Кроме того, можно задать количество потоков — по умолчанию до четырёх.

```csharp
// Step 7: Specify the language for OCR recognition
ocrBatchProcessor.Language = OcrLanguage.English;

// Step 8: Define the level of parallelism (up to 4 concurrent threads)
ocrBatchProcessor.MaxDegreeOfParallelism = 4;
```

**Почему параллелизм важен:** Если у вас процессор с четырьмя ядрами, установка `MaxDegreeOfParallelism` в `4` может сократить время обработки примерно на 75 %. На ноутбуке с двумя ядрами безопаснее установить `2`. Поэкспериментируйте, чтобы найти оптимальное значение для вашего железа.

## Шаг 7: Запустите пакетную задачу

Теперь происходит основная работа. Одна строка запускает весь конвейер, обрабатывая каждое изображение во входной папке и записывая результаты в выходную.

```csharp
// Step 9: Execute the batch processing of all supported image files
ocrBatchProcessor.Execute();

Console.WriteLine("Batch OCR completed.");
```

Когда консоль выведет *Batch OCR completed.*, рядом с каждым оригиналом появится файл `.txt` (или в выбранном вами формате). Имена файлов совпадают с исходными, что упрощает сопоставление OCR‑результатов с изображениями.

## Полный рабочий пример

Собрав всё вместе, получаем полную программу, которую можно скопировать в `Program.cs` и сразу запустить:

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create an OCR batch processor instance
        var ocrBatchProcessor = new OcrBatchProcessor();

        // Step 2: Configure the input folder containing images to process
        ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

        // Step 3: Set the folder where OCR results will be saved
        ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";

        // Step 4: Choose the desired output format (plain text is default)
        ocrBatchProcessor.OutputFormat = ResultFormat.Text; // alternatives: Json, Xml, Html, Pdf, etc.

        // Step 5: Specify the language for OCR recognition
        ocrBatchProcessor.Language = OcrLanguage.English;

        // Step 6: Define the level of parallelism (up to 4 concurrent threads)
        ocrBatchProcessor.MaxDegreeOfParallelism = 4;

        // Step 7: Execute the batch processing of all supported image files
        ocrBatchProcessor.Execute();

        Console.WriteLine("Batch OCR completed.");
    }
}
```

### Ожидаемый вывод

Предположим, в входной папке находятся три изображения (`invoice1.png`, `receipt2.jpg`, `form3.tif`). В выходной папке появятся:

```
invoice1.txt
receipt2.txt
form3.txt
```

Каждый файл `.txt` содержит «сырые» символы, извлечённые из соответствующего изображения. Откройте любой файл в Notepad — увидите текстовое представление исходного скана.

## Часто задаваемые вопросы и особые случаи

### Что делать, если некоторые изображения не удаётся обработать?

`OcrBatchProcessor` по умолчанию выводит ошибки в консоль и продолжает работу со следующим файлом. Для продакшена можно подписаться на событие `OnError`, собрать имена неудавшихся файлов и повторить попытку позже.

```csharp
ocrBatchProcessor.OnError += (sender, args) =>
{
    Console.WriteLine($"Failed on {args.FileName}: {args.Exception.Message}");
};
```

### Можно ли обрабатывать PDF‑файлы напрямую?

Да. Aspose.OCR рассматривает каждую страницу PDF как изображение. Просто укажите `InputFolder`, содержащий PDF‑файлы, и процессор извлечёт текст со всех страниц — фактически **преобразует изображения в текст**, даже если источник — PDF.

### Как работать с многоязычными документами?

Установите `Language` в `OcrLanguage.Multilingual` или задайте список языков, если версия библиотеки это поддерживает. Движок попытается распознать символы всех указанных языков, что удобно для международных счетов.

### Что насчёт потребления памяти?

Пакетный процессор потоково читает каждое изображение, поэтому использование памяти остаётся низким даже при тысячах файлов. Однако высокий `MaxDegreeOfParallelism` на машине с ограниченной ОЗУ может вызвать всплески. Следите за RAM и при необходимости уменьшайте количество потоков.

## Советы для повышения точности

- **Предобработка изображений**: удаляйте шум, исправляйте наклон и переводите в градации серого перед OCR. Aspose.OCR предлагает `ImagePreprocessOptions`, которые можно прикрепить к `ocrBatchProcessor`.
- **Выбирайте правильный формат**: если нужна сохранность разметки, `ResultFormat.Html` или `Pdf` сохранят переносы строк и базовое оформление.
- **Проверяйте результаты**: реализуйте простую пост‑обработку, которая проверяет пустые файлы вывода — они часто указывают на неудачное распознавание.

## Следующие шаги

Теперь, когда вы освоили **пакетную обработку OCR** для **извлечения текста из изображений**, вы можете:

- **Интегрировать с базой данных** — хранить каждый результат OCR вместе с метаданными для поиска.
- **Добавить пользовательский интерфейс** — создать небольшое WPF или WinForms приложение, позволяющее пользователям перетаскивать папки.
- **Масштабировать** — запускать пакетную задачу в Azure Functions или AWS Lambda для облачной обработки.

Все эти темы опираются на те же базовые концепции, которые мы рассмотрели, так что вы готовы расширять своё решение.

---

**Счастливого кодинга!** Если возникнут проблемы или появятся идеи по улучшению, оставляйте комментарий ниже. Давайте поддерживать диалог и делать автоматизацию OCR ещё более гладкой.


## Что изучать дальше?


В следующих руководствах рассматриваются тесно связанные темы, которые развивают техники, продемонстрированные в этом гайде. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}