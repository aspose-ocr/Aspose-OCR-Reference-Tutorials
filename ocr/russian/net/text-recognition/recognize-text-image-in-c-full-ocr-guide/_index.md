---
category: general
date: 2026-06-06
description: распознавание текста на изображении с помощью C# OCR – пошаговый пример
  OCR на C#, который извлекает текст из сканов и преобразует скан в текст за считанные
  минуты.
draft: false
keywords:
- recognize text image
- c# ocr example
- extract text scan
- convert scan to text
- image to text c#
language: ru
og_description: Распознавайте текст на изображении с помощью C# OCR. Изучите практический
  пример OCR на C#, который извлекает текст из сканов, преобразует скан в текст и
  обрабатывает реальные изображения.
og_title: распознавание текста на изображении в C# – Полный учебник по OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text image using C# OCR – a step‑by‑step c# ocr example that
    extracts text from scans and convert scan to text in minutes.
  headline: recognize text image in C# – Full OCR Guide
  type: TechArticle
- questions:
  - answer: The `Windows.Media.Ocr` namespace is Windows‑only. On Linux or macOS you’d
      swap it for TesseractSharp or IronOcr—both expose a similar `Engine.Recognize`
      method, so the surrounding code stays virtually unchanged.
    question: Does this work on .NET Core on Linux?
  - answer: Handwriting recognition is still experimental. For best results, stick
      to printed fonts or consider a cloud service like Azure Cognitive Services if
      you need high accuracy.
    question: How accurate is the built‑in OCR for handwritten notes?
  - answer: 'Not out of the box. Convert each PDF page to an image first (using `PdfSharp`
      or `Ghostscript`) and then feed the bitmap to the OCR engine. --- ## Conclusion
      You now have a complete, production‑ready **c# ocr example** that can **recognize
      text image** files, **extract text scan** contents, and **co'
    question: Can I process PDFs directly?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: Распознавание текста на изображении в C# – Полное руководство по OCR
url: /ru/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание текста на изображении в C# – Полный учебник по OCR

Когда‑нибудь задумывались, как **распознавать текст на изображении** напрямую со сканированной фотографии с помощью C#? Вы не одиноки. Будь то оцифровка старых чеков, извлечение данных из визитной карточки или просто преобразование низкокачественного скана в редактируемый текст — возможность извлекать текст из изображения — полезный навык, который должен быть у каждого разработчика.

В этом руководстве мы пройдём через **пример OCR на C#**, который загружает картинку, запускает оптическое распознавание символов и выводит результат в консоль. К концу вы сможете **извлекать текст из сканов**, **преобразовывать скан в текст** и даже подстроить процесс под шумные изображения. Никаких сторонних сервисов — только встроенный API Windows.Media.Ocr (или любой совместимый OcrEngine) и несколько строк кода.

## Что вы узнаете

* Как настроить проект C# для OCR.  
* Точный код, необходимый для **распознавания текста на изображении**.  
* Советы по работе с низкокачественными сканами и многостраничными документами.  
* Способы превратить пример в переиспользуемую библиотеку для ваших приложений.

### Предварительные требования

* .NET 6.0 или новее (API также работает на .NET 5+).  
* Visual Studio 2022 (Community‑edition подходит) или любая удобная IDE.  
* Пример изображения, например `lowres_scan.jpg`, помещённый в папку, к которой вы можете обратиться.  
* Базовое знакомство с async/await — вызовы OCR асинхронны в Windows API.

> **Pro tip:** Если вы работаете не на Windows, замените пространство имён `Windows.Media.Ocr` на кроссплатформенную библиотеку, например TesseractSharp; остальная логика останется той же.

---

## Шаг 1: Настройка **распознавания текста на изображении** с помощью OCR‑движка

Сначала нам нужен экземпляр OCR‑движка. Класс `OcrEngine` — точка входа для любой операции **image to text c#**.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Create the OCR engine – default language is English.
        OcrEngine engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));
        if (engine == null)
        {
            Console.WriteLine("Failed to create OcrEngine. Make sure you are on Windows 10 version 1809 or later.");
            return;
        }

        // Continue with the rest of the pipeline...
```

**Почему это важно:** Движок абстрагирует тяжёлую работу по распознаванию шаблонов. Явное создание позволяет управлять настройками языка, что необходимо, когда позже понадобится **извлекать текст из сканов** на других языках.

## Шаг 2: Загрузка файла изображения — ядро **преобразования скана в текст**

Далее читаем изображение с диска и превращаем его в `SoftwareBitmap`, формат, который ожидает OCR‑движок.

```csharp
        // Load the image file into a SoftwareBitmap.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "lowres_scan.jpg");
        using (FileStream fs = new FileStream(imagePath, FileMode.Open, FileAccess.Read))
        {
            // Decode the image (supports JPEG, PNG, BMP, etc.).
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Optional: upscale low‑resolution images for better accuracy.
            SoftwareBitmap upscaled = SoftwareBitmap.Convert(bitmap, bitmap.BitmapPixelFormat, bitmap.BitmapAlphaMode);
            // Pass the bitmap to OCR.
            await RecognizeAsync(engine, upscaled);
        }
    }
```

**Зачем это делаем:** Передача сырого файлового потока в OCR часто даёт плохие результаты, особенно с низкокачественными сканами. Преобразование в `SoftwareBitmap` позволяет менять DPI, глубину цвета и даже применять фильтры перед распознаванием.

## Шаг 3: Выполнение операции **распознавания текста на изображении**

Теперь вызываем метод `RecognizeAsync` движка. Здесь происходит магия.

```csharp
    private static async Task RecognizeAsync(OcrEngine engine, SoftwareBitmap bitmap)
    {
        // Run OCR – this returns an OcrResult object.
        OcrResult result = await engine.RecognizeAsync(bitmap);

        // The Result contains a collection of lines and words.
        Console.WriteLine("=== OCR Output ===");
        foreach (var line in result.Lines)
        {
            Console.WriteLine(line.Text);
        }

        // For a quick **image to text c#** check, also output the raw string.
        Console.WriteLine("\nFull Text:\n" + result.Text);
    }
}
```

**Что вы увидите:** Если `lowres_scan.jpg` содержит фразу «Hello World», консоль выведет:

```
=== OCR Output ===
Hello World

Full Text:
Hello World
```

Это весь **пример OCR на C#** в действии — всего четыре логических шага, но они охватывают всё от загрузки файла до финального вывода.

## Шаг 4: Обработка граничных случаев — когда скан не идеален

В реальном мире изображения не всегда чёткие. Ниже несколько корректировок, которые можно внести без полной переделки программы:

| Проблема | Быстрое решение |
|----------|-----------------|
| **Очень низкое DPI (≤ 72)** | Увеличить bitmap с помощью `BitmapTransform` перед распознаванием. |
| **Наклонённый текст** | Применить трансформацию вращения (`SoftwareBitmap.Rotate`), чтобы выпрямить страницу. |
| **Несколько языков** | Создать `OcrEngine.TryCreateFromLanguage(new OcrLanguage("en-fr"))` и установить `engine.Language` соответственно. |
| **Большие файлы** | Обрабатывать изображение по плиткам (`engine.RecognizeAsync(tileBitmap)`) и конкатенировать результаты. |

Эти настройки позволяют вашему процессу **извлечения текста из сканов** оставаться надёжным даже при работе с шумными чеками или фотографиями, снятыми под углом.

## Шаг 5: Превращение примера в переиспользуемый помощник (по желанию)

Если планируете **преобразовывать скан в текст** в нескольких частях приложения, оберните логику в небольшую утилит‑класс:

```csharp
public static class OcrHelper
{
    private static readonly OcrEngine _engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));

    public static async Task<string> ImageToTextAsync(string filePath)
    {
        using var fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        var decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
        var bitmap = await decoder.GetSoftwareBitmapAsync();

        var result = await _engine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

Теперь достаточно вызвать:

```csharp
string text = await OcrHelper.ImageToTextAsync("YOUR_DIRECTORY/lowres_scan.jpg");
Console.WriteLine(text);
```

**Почему это удобно:** Помощник изолирует “трубопровод” OCR, позволяя сосредоточиться на бизнес‑логике — идеальный вариант **примера OCR на C#**, который будет использоваться в разных проектах.

---

![пример распознавания текста на изображении](https://example.com/ocr-demo.png "Скриншот вывода OCR консольного приложения, показывающий результат распознавания текста на изображении")

*Alt text:* **пример распознавания текста на изображении** из консольного приложения OCR на C#.

---

## Часто задаваемые вопросы

**В: Работает ли это на .NET Core в Linux?**  
О: Пространство имён `Windows.Media.Ocr` доступно только в Windows. На Linux или macOS замените его на TesseractSharp или IronOcr — обе библиотеки предоставляют похожий метод `Engine.Recognize`, поэтому окружающий код практически не меняется.

**В: Насколько точен встроенный OCR для рукописных заметок?**  
О: Распознавание рукописного текста всё ещё экспериментальное. Для лучших результатов используйте печатные шрифты или обратитесь к облачному сервису, например Azure Cognitive Services, если нужна высокая точность.

**В: Можно ли обрабатывать PDF‑файлы напрямую?**  
О: Не напрямую. Сначала преобразуйте каждую страницу PDF в изображение (с помощью `PdfSharp` или `Ghostscript`), а затем передайте bitmap в OCR‑движок.

---

## Заключение

Теперь у вас есть полностью готовый к использованию **пример OCR на C#**, который может **распознавать текст на изображении**, **извлекать текст из сканов** и **преобразовывать скан в текст** всего в несколько строк кода. Понимая поток — создание движка, загрузка изображения, асинхронное распознавание и обработка результата — вы сможете адаптировать эту схему к любому проекту C#, где нужно превращать картинки в поисковые строки.

Готовы к следующему шагу? Попробуйте добавить простой UI с WinForms или WPF, поэкспериментировать с разными языками или сохранить вывод в базу данных для поисковых архивов. Возможности безграничны, когда вы владеете техникой **image to text c#**.

Счастливого кодинга, и пусть ваши сканы всегда будут чёткими!

## Что изучать дальше?

Следующие учебники охватывают смежные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}