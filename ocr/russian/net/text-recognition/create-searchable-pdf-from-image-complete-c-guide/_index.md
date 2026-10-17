---
category: general
date: 2026-02-13
description: Создайте PDF с возможностью поиска из изображения с помощью Aspose.OCR.
  Узнайте, как преобразовать изображение в PDF, извлечь текст из изображения, встроить
  шрифты в PDF и распознать текст из PNG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- embed fonts in pdf
- recognize text from png
language: ru
og_description: Создайте PDF с возможностью поиска из изображения с помощью Aspose.OCR.
  Это руководство показывает, как преобразовать изображение в PDF, встроить шрифты
  и без труда извлечь текст из PNG.
og_title: Создание PDF с поиском из изображения – пошаговое руководство по C#
tags:
- C#
- OCR
- Aspose
- PDF generation
title: Создание поискового PDF из изображения – Полное руководство по C#
url: /ru/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из изображения – Полное руководство по C#

Когда‑нибудь вам нужно было **создать поисковый PDF** из отсканированного PNG, но вы не знали, с чего начать? Вы не одиноки. Во многих проектах — подумайте о цифровизации счетов или архивировании старых руководств — возможность превратить изображение в PDF, по которому действительно можно искать, меняет правила игры.  

В этом руководстве мы пройдем все шаги, чтобы **преобразовать изображение в PDF**, **извлечь текст из изображения**, встроить необходимые шрифты и в итоге получить полностью поисковый PDF‑файл. Никаких расплывчатых ссылок, только готовый, исполняемый пример, который вы можете скопировать‑вставить в Visual Studio уже сегодня.

> **Что вы получите:** консольное приложение C#, которое читает `input.png`, запускает OCR, встраивает шрифты, сохраняет оригинальное растровое изображение как фон и записывает `output.pdf`. К концу вы поймёте, *почему* каждая строка важна и как её настроить под свои сценарии.

---

## Требования

- .NET 6.0 SDK или новее (код также работает с .NET Framework 4.7+).  
- Aspose.OCR for .NET – можно установить через NuGet (`Install-Package Aspose.OCR`).  
- Пример PNG‑изображения (`input.png`) в папке, которой вы управляете.  
- Базовое знакомство с консольными проектами C# (если вы никогда не создавали их, откройте Visual Studio → **Create a new project** → **Console App** → **C#**).

> **Подсказка:** Aspose предлагает бесплатную пробную лицензию; просто поместите файл `.lic` рядом с исполняемым файлом, и библиотека будет работать без водяных знаков.

---

## Шаг 1: Настройка OCR‑движка – распознавание текста из PNG

Первое, что нам нужно, — OCR‑движок, способный действительно читать символы в PNG‑файле. Aspose.OCR делает это простым.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

// Initialize the OCR engine with English language support
OcrEngine ocrEngine = new OcrEngine
{
    // Primary language – you can add more if needed
    Language = OcrLanguage.English
};
```

**Почему это важно:**  
Установка `Language` сообщает движку, какой набор символов ожидать. Если пропустить этот шаг, движок использует общий режим, который может неправильно интерпретировать символы с диакритикой или цифры. Для многоязычных документов можно передать список через запятую, например `OcrLanguage.English | OcrLanguage.French`.

---

## Шаг 2: Загрузка и распознавание изображения – извлечение текста из изображения

Теперь, когда движок готов, передаём ему PNG, который нужно обработать.

```csharp
// Path to the source image; adjust as needed
string inputPath = @"YOUR_DIRECTORY/input.png";

// Perform OCR – this populates the engine's internal text representation
ocrEngine.RecognizeImage(inputPath);
```

**Что происходит «под капотом»?**  
`RecognizeImage` сканирует bitmap, определяет текстовые блоки и сохраняет результат в `ocrEngine`. Позже вы можете обратиться к `ocrEngine.Text`, если нужен просто сырой текст, но для поискового PDF мы позволим Aspose выполнить конвертацию напрямую.

> **Пограничный случай:** Если ваш PNG огромный (более 10 МБ), может не хватить памяти. В этом случае сначала уменьшите изображение или используйте `OcrEngine.RecognizeImage(Stream)`, чтобы передавать данные потоково.

---

## Шаг 3: Настройка параметров экспорта PDF – встраивание шрифтов в PDF

Поисковый PDF бесполезен, если шрифты не встроены; документ будет выглядеть некорректно на машинах без нужных гарнитур. Aspose позволяет переключать это через простой объект параметров.

```csharp
// Define how the searchable PDF should be built
SearchablePdfOptions pdfOptions = new SearchablePdfOptions
{
    // Guarantees the PDF renders correctly everywhere
    EmbedFonts = true,

    // Keeps the original raster image as a visual background
    KeepOriginalImage = true
};
```

**Зачем встраивать шрифты?**  
Когда `EmbedFonts` равно `true`, PDF содержит данные шрифта внутри файла. Это гарантирует, что любой просмотрщик — Chrome, Adobe Reader или мобильное приложение — отобразит текст точно так же, даже если в системе отсутствует данный шрифт.

**Когда стоит установить `KeepOriginalImage` в `false`?**  
Если вам нужен только извлечённый текст и вы хотите уменьшить размер файла, отключение этой опции удалит фон‑изображение, оставив «чистый» PDF только с текстом.

---

## Шаг 4: Экспорт в поисковый PDF – преобразование изображения в PDF

Имея результаты OCR и параметры PDF, последний шаг — однострочная команда, записывающая поисковый PDF на диск.

```csharp
// Destination path for the generated PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";

// Export the OCR result as a searchable PDF
ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created.");
```

**Что вы увидите:**  
Открыв `output.pdf` в любом просмотрщике, вы сможете выделять текст, копировать его и даже выполнить поиск (`Ctrl + F`), чтобы найти слова, которые изначально существовали только как пиксели в PNG.

---

## Полный рабочий пример

Ниже представлен полностью готовая программа, которую можно сразу собрать и запустить. Замените `YOUR_DIRECTORY` на путь к папке, содержащей `input.png`.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine – set language to English
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Recognize text from the PNG image
        string inputPath = @"YOUR_DIRECTORY/input.png";
        ocrEngine.RecognizeImage(inputPath);

        // 3️⃣ Prepare PDF options – embed fonts & keep raster background
        SearchablePdfOptions pdfOptions = new SearchablePdfOptions
        {
            EmbedFonts = true,
            KeepOriginalImage = true
        };

        // 4️⃣ Export to a searchable PDF file
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

        // 5️⃣ Notify the user
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**Ожидаемый вывод в консоли:**

```
Searchable PDF created.
```

Откройте `output.pdf` и попробуйте поискать слово, которое точно есть в `input.png`. Если оно подсвечивается, вы успешно **создали поисковый pdf** из изображения.

---

## Часто задаваемые вопросы и профессиональные советы

### «Можно ли обработать несколько изображений за один запуск?»

Конечно. Оберните логику распознавания и экспорта в цикл, например используя `Directory.GetFiles(..., "*.png")`. Не забудьте давать каждому PDF уникальное имя, например `Path.GetFileNameWithoutExtension(img) + ".pdf"`.

### «Что если документ содержит как английский, так и испанский текст?»

Установите свойство языка в комбинированный флаг:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Aspose тогда попытается определить символы обеих азбук.

### «PDF получился огромным — как его уменьшить?»

Два быстрых приёма:

1. Установите `pdfOptions.KeepOriginalImage = false`, чтобы убрать растровый фон.  
2. Используйте `pdfOptions.ImageCompression = ImageCompression.Jpeg;` (нужно добавить это свойство), чтобы сжать встроенное изображение.

### «Нужна ли лицензия для продакшн‑использования?»

Пробная версия подходит для тестов, но для коммерческого развертывания необходимо приобрести лицензию и зарегистрировать её в начале приложения:

```csharp
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

---

## Расширение решения

Теперь, когда вы знаете, как **создать поисковый PDF**, вы можете:

- **Добавить водяной знак** — использовать `PdfDocument` из Aspose.PDF для наложения текста после OCR.  
- **Пакетная обработка PDF** — объединять несколько поисковых PDF в один с помощью `PdfFileEditor`.  
- **Интеграция с Azure Blob Storage** — читать/писать потоки изображения и PDF напрямую из облака, избавляясь от локального ввода‑вывода.

Все эти расширения следуют одной схеме: получаем результат OCR, настраиваем следующую библиотеку и связываем операции цепочкой.

---

## Заключение

Вы только что узнали, как **создать поисковый PDF** из PNG‑изображения с помощью Aspose.OCR в C#. Инициализировав OCR‑движок, распознав текст, настроив `SearchablePdfOptions` для **встраивания шрифтов в PDF** и выполнив экспорт, вы получаете файл, визуально идентичный оригиналу и полностью поисковый.  

Далее экспериментируйте с пакетными конверсиями, разными языками или более сильным сжатием — что бы ни подходило вашему рабочему процессу. Если столкнётесь с нюансами, форумы Aspose и документация API — отличные ресурсы, но основные шаги выше покрывают около 90 % типовых сценариев.

Счастливого кодинга, и пусть ваши PDF всегда остаются поисковыми!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}