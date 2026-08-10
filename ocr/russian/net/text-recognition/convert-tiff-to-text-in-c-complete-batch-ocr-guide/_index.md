---
category: general
date: 2026-05-25
description: Конвертировать TIFF в текст с помощью Aspose.OCR на C#. Узнайте о пакетном
  преобразовании изображений в текст и эффективно извлекайте текст из файлов TIFF.
draft: false
keywords:
- convert tiff to text
- extract text from tiff
- batch image to text conversion
- convert scanned images txt
language: ru
og_description: Конвертировать TIFF в текст с помощью Aspose.OCR. Это руководство
  демонстрирует пакетное преобразование изображений в текст и показывает, как извлечь
  текст из файлов TIFF за несколько строк кода на C#.
og_title: Преобразование TIFF в текст на C# – Полное руководство по пакетному OCR
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  headline: Convert TIFF to Text in C# – Complete Batch OCR Guide
  type: TechArticle
- description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  name: Convert TIFF to Text in C# – Complete Batch OCR Guide
  steps:
  - name: '**Create** an OCR engine set for English.'
    text: '**Create** an OCR engine set for English.'
  - name: '**Collect** every TIFF file from the target folder.'
    text: '**Collect** every TIFF file from the target folder.'
  - name: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
    text: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
  - name: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
    text: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
  type: HowTo
tags:
- C#
- OCR
- Aspose
- TIFF
title: Конвертация TIFF в текст на C# – Полное руководство по пакетному OCR.
url: /ru/net/text-recognition/convert-tiff-to-text-in-c-complete-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Конвертация TIFF в текст на C# – Полное руководство по пакетному OCR

Когда‑нибудь вам нужно было **конвертировать TIFF в текст**, но вы не знали, с чего начать? Вы не одиноки — многие разработчики сталкиваются с пакетным OCR при работе со сканированными документами. В этом руководстве мы пройдем практическое решение, которое **извлекает текст из TIFF** файлов с помощью Aspose.OCR, и сделаем это параллельно, чтобы большие папки обрабатывались за секунды.

Мы также коснёмся лучших практик **batch image to text conversion**, так что к концу у вас будет переиспользуемый фрагмент кода, который преобразует целый каталог сканированных изображений в аккуратные файлы *.txt* — идеально подходит для индексации, поиска или передачи в последующий анализ.

## Что понадобится

- **.NET 6.0** или новее (код также компилируется на .NET Framework)  
- NuGet‑пакет **Aspose.OCR for .NET** (`Install-Package Aspose.OCR`)  
- Папка, содержащая один или несколько файлов *.tif* (классический формат сканирования TIFF)  
- Ваш любимый IDE (Visual Studio, VS Code, Rider — что угодно)

Вот и всё. Никаких внешних сервисов, никаких API‑ключей, только чистый C# и Aspose.

![Скриншот обработки TIFF‑файла и полученного текстового файла](/images/ocr-result.png "Результат OCR, показывающий вывод конвертированного TIFF в текст")

*(Alt text: Скриншот, показывающий конвертированный TIFF в текстовый вывод на экране)*

## Шаг 1: Настройка OCR‑движка — Конвертация TIFF в текст

Прежде всего, нам нужен экземпляр `OcrEngine`, который знает, что должен читать английские символы. Движок — сердце конвертации; правильная настройка обеспечивает надёжные результаты.

```csharp
using Aspose.OCR;
using System.IO;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Create an OCR engine configured for English – this is the core of convert TIFF to text
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };
```

*Почему это важно:*  
Aspose.OCR поддерживает десятки языков. Если вы работаете с многоязычными сканами, просто измените `OcrLanguage.English` на соответствующее значение enum. Оставление языка неопределённым заставляет движок переходить в режим автоопределения, что может быть медленнее и менее точно.

## Шаг 2: Сбор всех TIFF‑файлов — Эффективное извлечение текста из TIFF

Далее мы получаем каждый файл *.tif* из указанной вами папки. Использование `Directory.GetFiles` даёт нам чистый массив, который мы можем передать пакетному процессору.

```csharp
        // Locate every TIFF in the input folder – adjust the path to your own directory
        string inputFolder = @"C:\Scans\Batch";
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif", SearchOption.TopDirectoryOnly);

        if (tiffFiles.Length == 0)
        {
            System.Console.WriteLine("No TIFF files found. Check the folder path.");
            return;
        }
```

*Полезный совет:* Флаг `SearchOption.AllDirectories` можно использовать, если ваши сканы находятся в подпапках. Просто помните, что более глубокая рекурсия может увеличить использование памяти во время пакетного шага.

## Шаг 3: Выполнение параллельного OCR — Пакетное преобразование изображения в текст

Теперь самая интересная часть. Aspose.OCR поставляется со статическим помощником `BatchOcr.RecognizeAll`, который принимает массив путей к файлам, движок и подсказку `parallelism`. Мы запустим четыре потока, что на современном четырёхъядерном ноутбуке даёт почти линейное ускорение.

```csharp
        // Run OCR on all files in parallel (4 threads by default)
        // The result is a dictionary where Key = file path, Value = extracted text
        Dictionary<string, string> ocrResults = BatchOcr.RecognizeAll(tiffFiles, ocrEngine, parallelism: 4);
```

*Почему параллелизм?*  
Сканирование пакета высокоразрешённых TIFF может сильно нагружать CPU. Распределяя работу по нескольким потокам, мы загружаем все ядра, значительно сокращая общее время выполнения. Если запускать это на сервере с большим количеством ядер, увеличьте значение `parallelism` соответственно.

## Шаг 4: Запись вывода — Конвертация сканированных изображений в TXT‑файлы

Наконец мы проходим по словарю и записываем каждый фрагмент текста в файл *.txt*, который имеет то же базовое имя, что и оригинал. Это тот момент, когда **convert scanned images txt** становится реальностью.

```csharp
        // Save each recognized text to a .txt file with the same base name as the source TIFF
        foreach (var kvp in ocrResults)
        {
            string sourcePath = kvp.Key;
            string extractedText = kvp.Value;

            // Change extension from .tif to .txt
            string txtPath = Path.ChangeExtension(sourcePath, ".txt");

            // Write the text – UTF‑8 ensures all characters are preserved
            File.WriteAllText(txtPath, extractedText);
            System.Console.WriteLine($"Saved: {txtPath}");
        }

        System.Console.WriteLine("Batch conversion complete!");
    }
}
```

### Что делает код, простыми словами

1. **Create** OCR‑движок, настроенный на английский.  
2. **Collect** каждый TIFF‑файл из целевой папки.  
3. **Run** `BatchOcr.RecognizeAll` с четырьмя потоками, преобразуя каждое изображение в строку.  
4. **Loop** по результатам, заменяя расширение `.tif` на `.txt` и записывая строку на диск.

Это весь процесс **convert TIFF to text** в менее чем 50 строк кода.

## Обработка граничных случаев — Когда всё идёт не гладко

- **Missing or corrupted TIFFs** – `BatchOcr` бросит `OcrException`. Оберните вызов в `try / catch`, если нужна плавная деградация.  
- **Non‑English documents** – измените `OcrLanguage.English` на `OcrLanguage.Spanish`, `OcrLanguage.French` и т.д., или используйте `OcrLanguage.AutoDetect`.  
- **Very large images** – рассмотрите возможность снижения DPI перед OCR (`ocrEngine.ImagePreprocessing.Dpi = 200`), чтобы сэкономить память, хотя может пострадать точность.  
- **Output encoding** – если вам нужна определённая кодовая страница (например, Windows‑1252), передайте её в `File.WriteAllText(txtPath, extractedText, Encoding.GetEncoding(1252))`.

## Профессиональные советы для надёжных пакетных конвертаций

- **Log failures**: создайте `List<string> failedFiles` и добавляйте в него любой файл, который бросает исключение; после цикла запишите список в лог.  
- **Reuse the engine**: тот же экземпляр `OcrEngine` можно переиспользовать для множества файлов; не создавайте его внутри цикла.  
- **Validate the result**: быстрая проверка `if (string.IsNullOrWhiteSpace(extractedText))` может пометить сканы, которые пусты или нечитаемы.  
- **Combine with PDF**: если ваш источник — многостраничный PDF, сначала конвертируйте каждую страницу в TIFF (это делает Aspose.PDF), а затем запустите этот пакет.

## Следующие шаги — Выход за пределы простой конвертации

Теперь, когда вы можете **extract text from TIFF** файлы пакетно, вы можете захотеть:

- Передать файлы *.txt* в поисковый индекс (Elasticsearch, Azure Cognitive Search).  
- Запустить определение языка для каждого результата, чтобы направлять документы в локально‑специфичные конвейеры.  
- Создать поисковые PDF, наложив OCR‑текст обратно на оригинальные изображения (снова Aspose.PDF).

Все эти сценарии основаны на одной основной идее: **batch image to text conversion** — строительный блок для более крупных систем обработки документов.

---

### Заключение

Вы только что узнали, как **convert TIFF to text** с помощью Aspose.OCR, обрабатывать всю папку параллельно и сохранять каждый результат в чистый файл *.txt*. Решение лёгкое, полностью настраиваемое и готово к продакшн‑использованию — будь то оцифровка старых счетов, архивирование сканированных контрактов или обеспечение работы поискового движка.  

Попробуйте, настройте степень параллелизма и начните подавать эти только что созданные текстовые файлы в любой необходимый вам рабочий процесс. Приятного OCR!

---

## Связанные руководства

- [Извлечение текста из изображений с помощью OCR‑операции в папках](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Извлечение текста из изображения — оптимизация OCR с Aspose.OCR для .NET](/ocr/english/net/ocr-optimization/)
- [Извлечение текста из изображения C# с выбором языка с помощью Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}