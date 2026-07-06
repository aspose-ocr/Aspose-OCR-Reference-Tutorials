---
category: general
date: 2026-03-18
description: Создайте PDF с возможностью поиска с помощью Aspose OCR на C#. Преобразуйте
  изображение в PDF, добавьте слой OCR‑текста и запишите байты PDF в файл за несколько
  простых шагов.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- add ocr text layer
- write pdf bytes to file
language: ru
og_description: Быстро создавайте поисковые PDF с помощью Aspose OCR в C#. Узнайте,
  как преобразовать изображение в PDF, добавить слой OCR‑текста и записать байты PDF
  в файл.
og_title: Создайте поисковый PDF из изображения – Быстрое руководство по OCR на C#
tags:
- OCR
- PDF
- C#
- Aspose
title: Создание PDF с поиском из изображения с OCR – руководство по C#
url: /ru/net/text-recognition/create-searchable-pdf-from-image-with-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF с поисковым индексом из изображения с OCR – Руководство на C#

Когда‑нибудь нужно **создать PDF с поисковым индексом** из отсканированного изображения? С Aspose OCR это делается в несколько строк, без тяжёлых библиотек. В этом руководстве мы **преобразуем изображение в PDF**, наложим **слой текста OCR** и, наконец, **запишем байты PDF в файл**, получив документ PDF/A‑2b, соответствующий стандартам, который пользователи действительно смогут искать.

Если задаётесь вопросом, зачем нужен PDF с поисковым индексом вместо простого файла‑изображения, подумайте о пользовательском опыте: такой PDF позволяет копировать, выделять и индексировать текст — идеально для архивов, юридических документов или любых процессов, где позже понадобится извлечение текста. Поехали.

## Что понадобится

- .NET 6 или новее (код также работает на .NET Framework 4.7+)
- NuGet‑пакет Aspose.OCR (`Aspose.OCR` версии 23.10 или новее)
- Растровое изображение (`.png`, `.jpg` и т.п.), которое хотите превратить в PDF с поисковым индексом
- Базовые знания C# — ничего сложного, только основы

Вот и всё. Никаких внешних инструментов, никаких дополнительных конвертеров. Вся тяжёлая работа выполняется движком Aspose OCR.

## Создание PDF с поисковым индексом – Обзор

Прежде чем перейти к коду, опишем процесс:

1. **Создать** экземпляр OCR‑движка — этот объект умеет считывать текст с изображений.  
2. **Загрузить** исходное изображение — мы передадим `ImageStream` движку.  
3. **Настроить** параметры сохранения PDF/A‑2b — это указывает Aspose внедрить распознанный текст как скрытый слой.  
4. **Запустить** OCR и **получить** байты получившегося PDF.  
5. **Записать** эти байты на диск, получив окончательный PDF‑файл с поисковым индексом.

Каждый из этих шагов соответствует одной‑двум строкам C#, поэтому весь процесс выглядит как небольшой скрипт, а не масштабный проект.

## Шаг 1: Преобразование изображения в PDF – Загрузка изображения

Первое, что нужно: предоставить OCR‑движку материал для чтения. Вспомогательный метод `ImageStream.FromFile` загружает файл в поток, который может обработать Aspose.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

// 1️⃣ Load the source image you want to turn into a searchable PDF
ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
```

> **Совет:** Держите разрешение изображения ≥ 300 dpi; точность OCR резко падает при низком разрешении сканов.

## Шаг 2: Распознавание текста и добавление слоя OCR‑текста

Теперь создаём OCR‑движок и заставляем его распознать текст. Волшебство происходит, когда мы комбинируем результат распознавания с `PdfSaveOptions`, у которых `IncludeTextLayer = true`. Этот флаг заставляет Aspose внедрить извлечённые символы как невидимый слой текста, благодаря чему PDF становится поисковым.

```csharp
// 2️⃣ Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// 3️⃣ Set up PDF/A‑2b save options – includes the hidden text layer
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
{
    PdfCompliance = PdfCompliance.PdfA2b, // ensures PDF/A‑2b compliance
    IncludeTextLayer = true               // this is the key for searchable PDFs
};
```

Почему PDF/A‑2b? Это архивный формат по ISO‑стандарту, гарантирующий долговременное хранение и, что важно для нас, требующий наличия поискового текстового слоя. Если архивная совместимость не нужна, можно убрать `PdfCompliance`, но это не стоит дополнительных усилий.

## Шаг 3: Запись байтов PDF в файл – Сохранение результата

С готовым движком и установленными параметрами мы запускаем распознавание и сразу просим Aspose вернуть PDF в виде `byte[]`. Затем сохраняем эти байты на диск с помощью `File.WriteAllBytes`. Просто, но эффективно.

```csharp
// 4️⃣ Perform OCR on the image and get the PDF bytes
byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

// 5️⃣ Write the PDF/A‑2b file to the output location
System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
Console.WriteLine("PDF/A‑2b file created – you now have a searchable PDF!");
```

Строка `Console.WriteLine` необязательна, но даёт мгновенную обратную связь при запуске программы из терминала.

## Полный рабочий пример

Объединив всё вместе, получаем полностью готовую к запуску программу. Скопируйте её в новый консольный проект, замените `YOUR_DIRECTORY` реальным путём и нажмите **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

class PdfA2bDemo
{
    static void Main()
    {
        // Step 1: Load the source image
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");

        // Step 2: Create OCR engine and configure PDF/A‑2b options
        OcrEngine ocrEngine = new OcrEngine();
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
        {
            PdfCompliance = PdfCompliance.PdfA2b,
            IncludeTextLayer = true
        };

        // Step 3: Recognize and save as PDF bytes
        byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

        // Step 4: Write the bytes to a searchable PDF file
        System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
        Console.WriteLine("PDF/A‑2b file created.");
    }
}
```

### Ожидаемый результат

- В указанной папке появится файл `output.pdf`.  
- Откройте его в Adobe Acrobat Reader или любом PDF‑просмотрщике и попробуйте выделить текст — если копирование работает, вы успешно **создали PDF с поисковым индексом**.  
- Документ также пройдёт проверку на соответствие PDF/A‑2b, поскольку мы использовали соответствующий флаг совместимости.

## Часто задаваемые вопросы и особые случаи

**Что делать, если изображение содержит несколько страниц?**  
Оберните каждую страницу в отдельный `ImageStream` и передайте их последовательно в `OcrEngine`. Aspose автоматически объединит страницы в один PDF.

**Можно ли изменить язык OCR?**  
Конечно. Установите `ocrEngine.Language = Language.English;` (или любой поддерживаемый язык) перед вызовом `Recognize`.

**Как управлять потреблением памяти при работе с огромными файлами?**  
Если обрабатываете сканы гигабайтного размера, лучше сразу писать результат в `FileStream`, а не держать весь `byte[]` в памяти:

```csharp
using (var file = new FileStream("output.pdf", FileMode.Create))
{
    ocrEngine.Recognize(image).Save(pdfSaveOptions, file);
}
```

**Нужна ли лицензия?**  
Aspose предлагает бесплатную пробную версию без водяных знаков. Для продакшн‑использования приобретите лицензию, чтобы убрать баннер оценки и открыть полный набор функций.

## Советы для повышения точности OCR

- **Предобработайте** изображение: исправьте наклон, удалите шум и увеличьте контраст.  
- **Используйте** без потерь форматы, такие как PNG; артефакты JPEG могут сбивать движок.  
- **Избегайте** цветных фонов; чистый белый фон даёт наилучший результат.

## Следующие шаги

Теперь, когда вы умеете **создавать PDF с поисковым индексом**, можно:

- **Пакетно обрабатывать** папку изображений с помощью `Directory.GetFiles`.  
- **Извлекать** скрытый текст позже через API `PdfDocument` для индексации.  
- **Комбинировать OCR** с цифровыми подписями, создавая защищённые архивы.  

Все эти задачи опираются на тот же базовый шаблон: загрузка, распознавание, настройка, сохранение.

---

*Готовы превратить свои отсканированные архивы в PDF с поисковым индексом? Возьмите код, укажите путь к изображениям и позвольте Aspose выполнить всю тяжёлую работу. Приятного кодинга!*

![Создание PDF с поисковым индексом пример](/images/create-searchable-pdf.png "Иллюстрация PDF с поисковым индексом, сгенерированного из изображения")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}