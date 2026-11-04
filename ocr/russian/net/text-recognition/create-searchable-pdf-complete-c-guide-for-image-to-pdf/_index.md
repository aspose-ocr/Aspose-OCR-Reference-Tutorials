---
category: general
date: 2026-04-08
description: Быстро создавайте поисковые PDF и изучайте, как сжимать изображения в
  PDF, внедрять шрифты в PDF и распознавать текст на изображениях в C# с помощью Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- compress pdf images
- embed fonts pdf
- image to searchable pdf
- recognize text image
language: ru
og_description: Быстро создавайте поисковые PDF с Aspose.OCR. Узнайте, как сжимать
  изображения в PDF, встраивать шрифты в PDF и распознавать текст на изображениях
  в одном руководстве.
og_title: Создание PDF с возможностью поиска – Полное руководство по C#
tags:
- Aspose.OCR
- C#
- PDF Generation
title: Создание PDF с возможностью поиска – Полное руководство C# по преобразованию
  изображений в PDF
url: /ru/net/text-recognition/create-searchable-pdf-complete-c-guide-for-image-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF – Полное руководство C#

Нужно **create searchable pdf** из отсканированного изображения? Вы не единственный, кто уставился на огромный PNG и задумался, как превратить его в лёгкий, текстово‑поисковый документ. Хорошая новость в том, что с Aspose.OCR вы можете сделать это в паре строк, а также узнаете, как **compress PDF images**, **embed fonts PDF** и **recognize text image** без усилий.

В этом руководстве мы пройдем весь процесс: от загрузки изображения, запуска OCR, настройки параметров сохранения PDF до окончательной записи поискового PDF на диск. К концу вы получите готовый к использованию метод, который можно вставить в любой .NET‑проект, а также несколько профессиональных советов для сложных случаев, с которыми вы можете столкнуться позже.

## Что понадобится

- **.NET 6+** (код также работает на .NET Framework 4.7, но мы будем целиться в .NET 6 для современного синтаксиса).  
- **Aspose.OCR for .NET** – установить через NuGet: `Install-Package Aspose.OCR`.  
- Файл изображения (PNG, JPEG, TIFF), содержащий текст, который вы хотите сделать поисковым.  
- Небольшая доля любопытства – остальное описано ниже.

> **Pro tip:** Если вы планируете обрабатывать десятки страниц, рассмотрите возможность повторного использования одного экземпляра `OcrEngine`, чтобы избежать накладных расходов на многократную загрузку языковых данных.

## Шаг 1: Настройка OCR‑движка – Recognize Text Image

Первое, что нам нужно, — OCR‑движок, способный считывать символы из исходного битмапа. Aspose.OCR позволяет указать язык (English, French и т.д.) и возвращает объект `OcrResult`, содержащий как исходный текст, так и данные изображения.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

public static OcrResult LoadAndRecognize(string imagePath)
{
    // Initialize the OCR engine – “en” is the ISO code for English.
    var ocrEngine = new OcrEngine { Language = "en" };

    // Recognize the image and get the result.
    OcrResult result = ocrEngine.RecognizeImage(imagePath);

    // Quick sanity check – throw if nothing was detected.
    if (string.IsNullOrWhiteSpace(result.Text))
        throw new InvalidOperationException("No text was recognized in the image.");

    return result;
}
```

**Почему это важно:**  
- Указание языка значительно повышает точность; движок загружает языковые словари в фоновом режиме.  
- `OcrResult` хранит не только извлечённую строку, но и базовый битмап, который мы позже внедрим в PDF, чтобы документ визуально оставался идентичным оригинальному скану.

## Шаг 2: Настройка параметров сохранения PDF – Compress PDF Images & Embed Fonts

Поисковый PDF по сути является обычным PDF с невидимым текстовым слоем поверх отсканированного изображения. Если игнорировать сжатие, итоговый файл может стать огромным. Класс `PdfSaveOptions` предоставляет тонкую настройку качества изображений, встраивания шрифтов и их подмножества.

```csharp
public static PdfSaveOptions GetPdfSaveOptions()
{
    return new PdfSaveOptions
    {
        // Reduce file size by compressing the raster image.
        CompressImages = true,

        // ImageQuality ranges from 0 (worst) to 100 (best). 75 is a good balance.
        ImageQuality = 75,

        // Embedding fonts ensures the text layer looks the same on any machine.
        EmbedFonts = true,

        // Subsetting keeps only the glyphs we actually use – another size saver.
        FontSubset = true
    };
}
```

**Почему стоит embed fonts PDF:**  
Когда PDF открывается на системе, где отсутствует точный шрифт, использованный в OCR‑слое, текст может отображаться некорректно. Встраивание гарантирует визуальную идентичность на всех платформах, что критично для юридических или архивных документов.

## Шаг 3: Сохранение результата как поискового PDF – Image to Searchable PDF

Теперь объединяем всё: берём `OcrResult`, применяем наши `PdfSaveOptions` и записываем файл. Метод `SaveAsSearchablePdf` делает всю тяжёлую работу — создаёт скрытый текстовый оверлей, соответствующий результату OCR, при этом сохраняет оригинальное изображение.

```csharp
public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
{
    // Step 1: Recognize the image.
    OcrResult ocrResult = LoadAndRecognize(inputImage);

    // Step 2: Prepare PDF options.
    PdfSaveOptions pdfOptions = GetPdfSaveOptions();

    // Step 3: Write the searchable PDF.
    ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);

    Console.WriteLine($"Searchable PDF created at: {outputPdf}");
}
```

### Полный рабочий пример

Ниже представлена автономная консольная программа, которую можно скопировать в новый .NET‑консольный проект. Предполагается, что изображение находится в папке `YOUR_DIRECTORY`, расположенной рядом с исполняемым файлом.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

class Program
{
    static void Main()
    {
        string inputPath = "YOUR_DIRECTORY/input.png";
        string outputPath = "YOUR_DIRECTORY/output.pdf";

        try
        {
            CreateCompressedSearchablePdf(inputPath, outputPath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // --- Methods from the previous steps -------------------------------------------------
    public static OcrResult LoadAndRecognize(string imagePath)
    {
        var ocrEngine = new OcrEngine { Language = "en" };
        OcrResult result = ocrEngine.RecognizeImage(imagePath);
        if (string.IsNullOrWhiteSpace(result.Text))
            throw new InvalidOperationException("OCR did not detect any text.");
        return result;
    }

    public static PdfSaveOptions GetPdfSaveOptions()
    {
        return new PdfSaveOptions
        {
            CompressImages = true,
            ImageQuality = 75,
            EmbedFonts = true,
            FontSubset = true
        };
    }

    public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
    {
        OcrResult ocrResult = LoadAndRecognize(inputImage);
        PdfSaveOptions pdfOptions = GetPdfSaveOptions();
        ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);
        Console.WriteLine("Searchable PDF created.");
    }
}
```

Запуск программы создаст `output.pdf`, который можно открыть в Adobe Reader, Foxit или любом другом PDF‑просмотрщике и сразу искать слова, изначально присутствующие только в изображении.

## Шаг 4: Проверка результата – работает ли поиск?

После генерации файла откройте его и используйте встроенный поиск (Ctrl + F). Если вы находите такие слова, как «invoice», «date» или «total», вы успешно создали **searchable PDF**.  

Если поиск ничего не возвращает:

1. **Проверьте точность OCR** – возможно, исходное изображение имеет низкое разрешение. Рассмотрите возможность увеличения DPI перед OCR (Aspose позволяет задать `Resolution` у движка).  
2. **Убедитесь в встраивании шрифтов** – откройте свойства PDF и посмотрите раздел *Fonts*; там должен отображаться встроенный шрифт.  
3. **Проверьте сжатие изображения** – слишком низкое значение `ImageQuality` может сделать визуальный слой нечитаемым, что иногда сбивает последующие инструменты.

## Общие варианты и граничные случаи

| Сценарий | Что изменить | Почему |
|----------|--------------|--------|
| **Multi‑page TIFF** | Пройтись по каждому кадру, вызвать `RecognizeImage` для каждой страницы, затем использовать `PdfSaveOptions` с `AppendMode = true`. | Сохраняет каждую отсканированную страницу как отдельную поисковую страницу. |
| **Non‑English language** | Изменить `Language = "fr"` (или другой соответствующий ISO‑код) и при необходимости предоставить пользовательский словарь. | Улучшает распознавание символов с диакритикой и специфических для языка глифов. |
| **Very large images** | Уменьшить масштаб битмапа перед OCR (`ocrEngine.Image = Image.FromFile(...).GetThumbnailImage(...)`). | Снижает потребление памяти и ускоряет OCR без значительной потери точности. |
| **Need OCR confidence** | Обратиться к `ocrResult.RecognizedWords` и проверить свойство `Confidence`. | Позволяет помечать слова с низкой уверенностью для последующего ручного контроля. |

## Советы по производительности

- **Повторно используйте `OcrEngine`** при обработке пакета файлов — он кэширует языковые данные.  
- **Параллелизуйте** шаг распознавания с помощью `Parallel.ForEach`, если у вас многопроцессорная машина, но сохраняйте записи PDF последовательно, чтобы избежать конфликтов доступа к файлам.  
- **Настройте `ImageQuality`**: 85‑90 дает почти без потерь изображения, а 60‑70 обычно достаточно для текстовых документов.

## Заключение

Мы рассмотрели всё, что нужно для **create searchable pdf** из изображений с помощью Aspose.OCR, а также узнали, как **compress pdf images**, **embed fonts pdf** и эффективно **recognize text image**. Полный пример кода готов к вставке в любой C#‑проект, а дополнительные советы помогут адаптировать решение к большим объёмам или другим языкам.

Готовы к следующему шагу? Попробуйте добавить водяной знак, объединить несколько поисковых PDF‑файлов или интегрировать эту процедуру в веб‑API, чтобы пользователи могли загружать сканы и мгновенно получать поисковые PDF. Возможностей бесконечно много, а с фундаментальными знаниями их легко реализовать.

Счастливого кодинга, и пусть ваши PDF остаются маленькими, поисковыми и идеально отрисованными!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}