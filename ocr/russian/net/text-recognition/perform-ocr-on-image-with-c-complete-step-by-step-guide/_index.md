---
category: general
date: 2026-05-21
description: Выполнить OCR на изображении с помощью C#. Узнайте, как загрузить изображение
  для OCR, извлечь текст из PNG и распознать текст на изображении с помощью небольшого
  примера кода.
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: ru
og_description: Быстро выполнять OCR изображения на C#. Это руководство показывает,
  как загрузить изображение для OCR, извлечь текст из PNG и распознать текст с учётом
  разметки в HTML‑выводе.
og_title: Распознавание текста на изображении с помощью C# – Полный учебный курс.
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: Выполните OCR изображения с помощью C# — полное пошаговое руководство
url: /ru/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполняем OCR на изображении с C# – Полное пошаговое руководство

Когда‑то задавались вопросом, как **выполнять OCR на изображении** без громоздких графических интерфейсов? Вы не одиноки. Будь то оцифровка чеков, извлечение данных из отсканированных форм или простая конверсия PNG в поисковый текст — несколько строк C# справятся с задачей.

В этом руководстве мы пройдем процесс загрузки изображения для OCR, распознавания текста с изображения и, наконец, извлечения текста из PNG в чистый HTML. К концу вы получите готовое к запуску консольное приложение, которое **выполняет OCR на изображении** и сохраняет оригинальное расположение элементов.

## Что вы создадите

- Минимальная консольная программа, читающая PNG (или любое поддерживаемое изображение)  
- Использует OCR‑движок для **распознавания текста с изображения**  
- Сохраняет результат в виде HTML с учётом разметки, встраивая оригинальную картинку  
- Показано, как **загружать изображение для OCR**, **извлекать текст из PNG** и обрабатывать типичные крайние случаи  

> **Требования**  
> - .NET 6.0 SDK или новее (можно также целиться в .NET Framework 4.7+)  
> - Совместимая с NuGet OCR‑библиотека — в примере используется *Aspose.OCR*, но подойдёт любая библиотека с похожим API  
> - Базовые знания C# (ничего сложного)  

Есть всё? Отлично — приступаем.

## Выполняем OCR на изображении – полный разбор кода

Ниже представлен **полный, готовый к запуску** код. Скопируйте его в новый консольный проект (`dotnet new console`) и нажмите **F5**.

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **Ожидаемый вывод**  
> ```
> HTML with layout saved.
> ```  
> После выполнения вы найдёте `form.html` рядом с вашим PNG. Откройте его в браузере — увидите точно такой же макет, но теперь текст можно выделять и искать.

### Загрузка изображения для OCR

Строка `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` — это место, где мы **загружаем изображение для OCR**. Помощник `ImageStream` абстрагирует детали формата файла, так что вы можете передать JPEG, BMP или TIFF без изменения кода.  

**Почему не просто передать `Bitmap`?**  
Потому что многие OCR‑SDK ожидают поток, содержащий также метаданные DPI. Использование встроенного загрузчика библиотеки гарантирует, что движок видит изображение точно так, как оно отображается на экране, что повышает точность.

#### Совет профессионала
Если вы обрабатываете пакет файлов, оберните шаг загрузки в `try/catch` и логируйте любые `FileNotFoundException`. Это предотвратит падение всей партии из‑за отсутствия одного файла.

### Извлечение текста из PNG

После завершения `engine.Recognize()` OCR‑движок хранит распознанный текст внутри. Вы можете получить его как строку, если нужен только «сырой» текст:

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

Это самый быстрый способ **извлечь текст из PNG**, когда вас не интересует разметка. Для большинства задач ввода данных достаточно простого текста — просто не забудьте удалить переносы строк, если планируете импортировать в CSV.

### Распознавание текста с изображения

Вызов `Recognize()` делает всю тяжёлую работу. Под капотом движок:

1. Нормализует изображение (выравнивает, удаляет шум)  
2. Делит его на строки и слова  
3. Запускает нейронный классификатор, обученный на миллионах глифов  

Поскольку мы задали `Language = OcrLanguage.English`, движок использует англоязычные словари, что значительно снижает количество ложных срабатываний. Если нужна поддержка нескольких языков, просто передайте массив языков:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### Вывод HTML с учётом разметки

Большинство разработчиков останавливаются на простом тексте, но `HtmlSaveOptions`, которые мы использовали, позволяют **выполнять OCR на изображении** и сохранять визуальную структуру. Важны два флага:

- `PreserveLayout = true` — сохраняет колонки, таблицы и отступы.  
- `EmbedImages = true` — вставляет оригинальный PNG как Base64‑закодированный элемент `<img>`, делая HTML автономным.

Если нужен более лёгкий файл, установите `EmbedImages = false`, и HTML будет ссылаться на оригинальный PNG на диске.

#### Крайний случай: большие файлы

Для изображений более 5 МБ встраивание может сильно увеличить размер HTML. В таких ситуациях переключитесь на внешние ссылки на изображения и рассмотрите предварительное сжатие PNG с помощью `ImageProcessor.Compress`.

## Распространённые подводные камни и советы

| Симптом | Возможная причина | Решение |
|--------|-------------------|--------|
| Иероглифы вместо текста | Неправильный язык или отсутствует языковой пакет | Установите нужные языковые файлы и правильно задайте `engine.Language` |
| Нет текста в выводе | Изображение слишком тёмное или низкого разрешения | Предобработайте с `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` |
| Разметка в HTML испорчена | `PreserveLayout` оставлен по умолчанию `false` | Установите `PreserveLayout = true` в `HtmlSaveOptions` |
| Медленная обработка множества страниц | Движок переинициализируется для каждого файла | Переиспользуйте один экземпляр `OcrEngine` и меняйте только `engine.Image` в цикле |

### Масштабирование на несколько файлов

Если нужно **выполнять OCR на изображении** файлов в папке, оберните основную логику в простой цикл:

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

Обратите внимание, что **загружаем изображение для OCR** внутри цикла, но сохраняем те же объекты `engine` и `htmlOptions`. Это уменьшает нагрузку на память и ускоряет пакетную обработку.

## Выход за пределы: экспорт в PDF или DOCX

Тот же `engine` может сохранять в другие форматы:

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

Если ваша downstream‑система ожидает поисковые PDF, это меняется одной строкой — отдельный конвертер не нужен.

## Заключение

Мы показали, как **выполнять OCR на изображении** с помощью C#, от загрузки картинки до **извлечения текста из PNG** и, наконец, **распознавания текста с изображения** в HTML с учётом разметки. Полный пример готов к запуску, и теперь вы знаете, почему каждый шаг важен, как адаптировать его под разные языки и какие подводные камни могут возникнуть.

Дальше попробуйте заменить английский язык на другой, поэкспериментировать с `PreserveLayout = false` для более лёгкого HTML, либо направить вывод простого текста в базу данных для поисковых архивов. Возможности безграничны, когда у вас есть надёжный OCR‑движок и несколько строк C#.

Есть вопросы по обработке многостраничных TIFF, или хотите узнать, как интегрировать это в ASP.NET Core API? Оставляйте комментарий ниже, и happy coding!

## Связанные руководства

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}