---
category: general
date: 2026-02-17
description: Как выполнять пакетное OCR нескольких PDF и изображений в C# с использованием
  Aspose OCR. Узнайте, как извлекать текст из PDF, конвертировать PDF в текст и распознавать
  текст на изображениях.
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: ru
og_description: Как пакетно выполнять OCR нескольких документов в C# с помощью Aspose
  OCR. Получите пошаговый код для извлечения текста из PDF, преобразования PDF в текст
  и распознавания текста на изображениях.
og_title: Как пакетно выполнять OCR файлов в C# – Полное руководство
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: Как пакетно выполнять OCR файлов в C# – Полный пример кода
url: /ru/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

** formatting.

Proceed.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как пакетно выполнять OCR файлов в C# – Полное руководство

Когда‑нибудь задумывались **как пакетно выполнять OCR** для множества PDF‑файлов и сканированных изображений, не пиша отдельный цикл для каждого файла? Вы не одиноки. Большинство разработчиков сталкиваются с этой проблемой, когда нужно извлечь текст из десятков страниц за один раз. Хорошая новость? С Aspose OCR вы можете передать коллекцию файлов в один движок и позволить ему выполнить всю тяжелую работу.  

В этом руководстве мы пройдем практическое решение, которое позволяет **извлекать текст из pdf**, **конвертировать pdf в текст** и **распознавать текст с изображений** в одном пакетном запуске. К концу вы получите готовое консольное приложение, которое выводит результат OCR для каждой страницы, и поймёте, почему каждый шаг выполнен именно так, чтобы вы могли адаптировать его под свои проекты.

## Предварительные требования – Что нужно перед началом

- **.NET 6.0 или новее** (код также работает на .NET Framework, но рекомендуется .NET 6+)
- **NuGet‑пакет Aspose.OCR** – установите его командой `dotnet add package Aspose.OCR`
- Пара образцов файлов: многостраничный PDF (`doc1.pdf`) и отсканированный TIFF (`doc2.tif`). Поместите их в папку, к которой сможете обратиться, например, `C:\OCRSamples`.
- Базовые знания C# – вы должны быть уверены в работе с `using` и коллекциями.

> Pro tip: Если у вас нет лицензии, Aspose предлагает бесплатный временный ключ, который снимает ограничение в 100 страниц во время разработки.

## Шаг 1: Создание проекта и импорт пространств имён

Сначала создайте новый консольный проект (или добавьте к существующему) и подключите необходимые пространства имён.

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **Почему это важно:** Импорт `Aspose.OCR.Image` предоставляет удобный метод `ImageStream.FromFile`, который автоматически разбивает PDF‑страницы на отдельные потоки изображений. Это и есть «секретный соус», делающий пакетную обработку простой.

## Шаг 2: Инициализация OCR‑движка

Движок – это «рабочая лошадка», которая взаимодействует с базовым OCR‑модулем. Для всей партии достаточно одного экземпляра.

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Объяснение:** Повторное использование одного `OcrEngine` снижает нагрузку на память и ускоряет обработку, потому что нативные библиотеки остаются загруженными между страницами.

## Шаг 3: Формирование списка потоков изображений

Здесь мы собираем каждый документ, который хотим обработать. `ImageStream.FromFile` достаточно умен, чтобы разбить PDF на отдельные страницы, так что трёхстраничный PDF превращается в три отдельных потока «за кулисами».

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **Пограничный случай:** Если у вас смешанные PDF, TIFF, JPEG или PNG, просто добавьте их в тот же список – Aspose автоматически определит формат.

## Шаг 4: Выполнение пакетной операции OCR

Теперь передаём список движку. `RecognizeBatch` возвращает коллекцию объектов `OcrResult`, по одному на каждую страницу.

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **Зачем пакетно?** Выполнение OCR постранично в ручном цикле заставляет движок переинициализироваться каждый раз, что может удвоить время обработки. `RecognizeBatch` держит движок «разогретым» и отдает результаты по мере их готовности.

## Шаг 5: Вывод распознанного текста

Наконец, проходим по результатам и выводим текст каждой страницы в консоль. Здесь вы можете заменить `Console.WriteLine` на запись в файл, вставку в базу данных или любое другое последующее действие.

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### Ожидаемый вывод в консоль

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Если запустить программу с образцовыми файлами, вы увидите блок текста для каждой страницы, подтверждая, что вы успешно **извлекли текст из отсканированного pdf** за один проход.

## Обработка распространённых проблем

| Проблема | Почему возникает | Быстрое решение |
|----------|------------------|-----------------|
| **Ошибки «Out‑of‑memory»** | Большие PDF генерируют множество изображений высокого разрешения. | Ограничьте DPI при загрузке PDF: `ocrEngine.Settings.ImageDpi = 200;` |
| **Неправильные символы** | Исходный скан низкого качества или использует неподдерживаемый язык. | Явно задайте язык: `ocrEngine.Language = Language.English;` |
| **Частичные результаты** | Список пакета содержит повреждённый файл. | Оберните `RecognizeBatch` в `try/catch` и логируйте `e.Message` для проблемного файла. |
| **Узкое место в производительности** | Выполнение в одном потоке на многопроцессорной машине. | Используйте `Parallel.ForEach` с отдельными экземплярами `OcrEngine` для каждого потока (продвинутый уровень). |

## Бонус: Сохранение результатов OCR в текстовые файлы

Если хотите сохранять отдельный `.txt`‑файл для каждой страницы, просто добавьте небольшую запись внутри цикла:

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

Теперь вы превратили **конвертацию pdf в текст** в аккуратную папку с обычными текстовыми файлами — идеально для последующей индексации или поиска.

## Полный рабочий пример

Ниже полностью готовая к копированию и вставке программа. Нет скрытых зависимостей, нет внешних скриптов.

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

Запустите `dotnet run` из папки проекта и наблюдайте, как консоль заполняется извлечённым текстом. Это и есть **как пакетно выполнять OCR** для коллекции документов всего в несколько строк C#.

## Что мы рассмотрели – Краткое резюме

- Настроили консольное .NET‑приложение и установили Aspose.OCR.  
- Создали один экземпляр `OcrEngine` для повышения эффективности.  
- Сформировали список объектов `ImageStream`, которые автоматически разбивают PDF на страницы.  
- Выполнили `RecognizeBatch` для **извлечения текста из pdf** и других форматов изображений за один проход.  
- Вывели результаты и при желании сохранили их в отдельные `.txt`‑файлы, завершив процесс **конвертации pdf в текст**.  

## Следующие шаги и смежные темы

- **Масштабирование**: Используйте `Parallel.ForEach` с пулом объектов `OcrEngine` для одновременной обработки сотен файлов.  
- **Языковые пакеты**: Замените `Language.English` на `Language.French` или загрузите пользовательский словарь, когда нужно **распознавать текст с изображений** на других языках.  
- **Постобработка**: Пропустите вывод OCR через проверку орфографии или парсер естественного языка, чтобы повысить точность распознавания сканированных контрактов.  
- **Альтернативные библиотеки**: Сравните Aspose OCR с Tesseract.NET, если ищете открытый вариант — обе могут **извлекать текст из отсканированного pdf**, но различаются лицензией и точностью «из коробки».

---

![how to batch OCR example](alt="пример пакетного OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}