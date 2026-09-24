---
category: general
date: 2026-02-09
description: быстро извлекать текст из изображений с помощью C#, задавая максимальный
  уровень параллелизма для пакетного OCR — научитесь конвертировать отсканированные
  страницы, обрабатывать OCR нескольких изображений и эффективно считывать текст из
  PNG.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: ru
og_description: Извлекать текст из изображений в C#, задавая максимальную параллельность.
  Этот учебник показывает, как конвертировать отсканированные страницы, выполнять
  OCR нескольких изображений и считывать текст из PNG с помощью Aspose OCR.
og_title: Извлечение текста из PNG‑изображений с помощью C# – Полное руководство по
  пакетному OCR
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: Извлечение текста из PNG‑изображений с помощью C# – пакетное OCR с использованием
  Aspose OCR
url: /ru/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# извлечение текстовых изображений из PNG с C# – пакетный OCR с использованием Aspose OCR

Когда‑то вам нужно было **извлечь текстовые изображения** из папки со сканированными PNG, но возник вопрос «как сделать это быстро?». Вы не одиноки. Во многих реальных проектах разработчики вынуждены **устанавливать максимальную параллельность**, чтобы десятки страниц обрабатывались за секунды, а не за минуты.  

В этом руководстве мы пройдем полный, готовый к запуску пример, который **конвертирует отсканированные страницы**, выполняет **многократный OCR изображений** и, наконец, **чтение текста из PNG** без лишних усилий. Никаких расплывчатых «см. документацию» ссылок — только код, который можно скопировать‑вставить, объяснения, почему каждая строка важна, и советы, как избежать типичных подводных камней.

> **Pro tip:** Если вы уже используете Aspose OCR в других местах, вы заметите тот же класс `OcrEngine`, но мы изменим его конфигурацию для настоящей параллельной обработки.

---

## Что понадобится

- **.NET 6+** (или .NET Framework 4.6+). API работает одинаково, но более новые среды дают лучшую работу с потоками.  
- **Aspose.OCR for .NET** – установить через NuGet: `Install-Package Aspose.OCR`.  
- Папка, содержащая несколько PNG‑сканов (`page1.png`, `page2.png`, …).  
- IDE или редактор, с которым вам удобно работать (Visual Studio, Rider, VS Code…).

И всё. Никаких внешних сервисов, никаких облачных ключей, только чистая локальная обработка.

---

## extract text images – Установка максимальной параллельности для пакетного OCR

Когда вы запускаете OCR для нескольких файлов, движок по умолчанию использует один поток. Это безопасно, но ужасно медленно. Настраивая `MaxDegreeOfParallelism`, вы указываете движку, сколько потоков он может создавать одновременно.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Почему 4?**  
Четыре — оптимальное значение для большинства современных ноутбуков: достаточно ядер, чтобы загрузить процессор, но не настолько много, чтобы «голодать» другие процессы. Если вы запускаете это на сервере с 16 ядрами, поднимите число до 12‑14 для заметного ускорения.

---

## Convert scanned pages – Формирование коллекции ImageStream

Aspose ожидает каждое изображение в виде `ImageStream`. Помощник `FromFile` читает файл, держит его в памяти и передаёт движку OCR. Вы также можете передать `MemoryStream`, если изображения приходят из базы данных или HTTP‑ответа.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Крайний случай:** Если какой‑то файл отсутствует или повреждён, `FromFile` бросит `FileNotFoundException`. Оберните создание в `try/catch`, если ожидаете ненадёжный ввод.

---

## multiple image ocr – Выполнение пакетного OCR

Теперь происходит тяжёлая работа. `RecognizeBatch` порождает до указанного количества потоков, обрабатывает каждое изображение и возвращает список объектов `OcrResult`.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

За кулисами каждый поток загружает своё изображение, запускает нейронную сеть и извлекает обычный текст. Порядок результатов соответствует порядку входного списка, так что вы можете безопасно сопоставлять страницу 1 → результат 0 и т.д.

---

## read png text – Вывод извлечённого содержимого

Наконец, мы проходим по результатам и выводим обычный текст в консоль. Здесь же вы можете перенаправить вывод в файл, базу данных или даже в downstream‑службу NLP.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Ожидаемый вывод в консоль

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

Если видите пустые секции, проверьте, что PNG‑файлы не полностью белые — OCR требует контраст.

---

## Практические советы и типичные подводные камни

| Ситуация | Что делать |
|-----------|------------|
| **Нагрузка на память** при больших пакетах | Обрабатывать изображения порциями по 10‑20 файлов, затем вызывать `GC.Collect()`, если замечаете всплески. |
| **Неправильное определение языка** | Установите `ocrEngine.Configuration.Language = OcrLanguage.English;` (или ваш целевой язык) перед вызовом `RecognizeBatch`. |
| **Низкая производительность несмотря на параллелизм** | Убедитесь, что ваш SSD не ограничивает I/O; предварительно загрузите все файлы в память (как мы делаем с `ImageStream.FromFile`). |
| **Отсутствуют символы** | Увеличьте `ocrEngine.Configuration.DPI = 300;` для обработки изображений более высокого разрешения. |

---

## Расширение примера – От PNG к PDF или DOCX

Если в дальнейшем понадобится **конвертировать отсканированные страницы** в поисковые PDF, просто передайте `ocrResults[i].PlainText` в PDF‑библиотеку (например, Aspose.PDF) и наложите текст как невидимый слой. Трюк с параллельностью работает и там.

---

## Полный исходный код (готов к копированию)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Сохраните как `BatchExample.cs`, запустите `dotnet run` и наблюдайте, как консоль заполняется текстом, который ранее был скрыт внутри PNG‑сканов.

---

## Визуальное резюме

![пример извлечения текстовых изображений](images/ocr-batch.png){alt="пример извлечения текстовых изображений"}

Диаграмма показывает поток: **PNG‑файлы → коллекция ImageStream → OcrEngine (max parallelism) → OCR‑результаты → Консоль / downstream‑хранилище**.

---

## Заключение

Теперь у вас есть надёжный сквозной рецепт, как **извлекать текстовые изображения** в C# с **установкой максимальной параллельности**, **конвертацией отсканированных страниц**, обработкой **многократного OCR изображений** и **чтением текста из PNG** эффективно. Код автономный, объяснения покрывают как «как», так и «почему», а советы избавят от типичных головных болей.

Что дальше? Попробуйте заменить список PNG‑файлов на динамический цикл `Directory.GetFiles`, поэкспериментировать с разным числом потоков или передать вывод в поисковый PDF. Та же схема масштабируется на сотни страниц без почти какого‑либо дополнительного кода.

Есть вопросы или сложный крайний случай? Оставляйте комментарий ниже, и happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}