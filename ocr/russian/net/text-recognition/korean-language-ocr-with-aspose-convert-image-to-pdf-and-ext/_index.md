---
category: general
date: 2026-05-28
description: Учебник по OCR корейского языка с использованием Aspose в C#. Узнайте,
  как загрузить изображение из потока, извлечь простой текст, преобразовать изображение
  в PDF и экспортировать PDF с возможностью поиска.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: ru
og_description: OCR корейского языка в C# с использованием Aspose. Пошаговое руководство
  по загрузке изображения из потока, извлечению простого текста, конвертации изображения
  в PDF и экспорту поискового PDF.
og_title: OCR корейского языка – преобразование изображения в PDF и извлечение текста
  (руководство C#)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'OCR корейского языка с Aspose: преобразование изображения в PDF и извлечение
  текста на C#'
url: /ru/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR корейского языка с Aspose: преобразование изображения в PDF и извлечение текста на C#

Когда‑то задумывались, как выполнить **OCR корейского языка** на изображении, не отправляя его в облако? Вы не одиноки. Будь то оцифровка уличных знаков, обработка чеков или построение многоязычного поискового индекса — возможность распознавать корейские символы локально экономит время, деньги и избавляет от проблем с конфиденциальностью.

В этом руководстве мы пройдём полный, готовый к запуску пример, показывающий, как **загрузить изображение из потока**, **извлечь простой текст**, **преобразовать изображение в PDF** и, наконец, **экспортировать поисковый PDF** — всё с помощью Aspose.OCR и нескольких строк C#. Никаких внешних сервисов, никакой скрытой магии — только чистый .NET‑код, который можно вставить в любое консольное приложение.

## Что вы получите

- Рабочую консольную программу, читающую JPEG‑файл через файловый поток.  
- Корейский текст, извлечённый как обычные Unicode‑строки.  
- Подробный JSON‑отчёт о выполнении OCR для отладки или аналитики.  
- Поисковый PDF, который можно открыть в любом PDF‑просмотрщике и действительно выделять корейские слова.  

**Требования**  
- .NET 6.0 или новее (код также работает на .NET Framework 4.7+).  
- NuGet‑пакет Aspose.OCR for .NET (`Install-Package Aspose.OCR`).  
- Папка, содержащая `korean_sign.jpg`, и доступное для записи место для выходных файлов.  

Если всё уже готово, отлично — приступим.

## Шаг 1: Инициализация OCR‑движка для корейского языка

Первое, что нужно — экземпляр `OcrEngine`. Включение GPU (если он есть) ускоряет распознавание в разы, а отключение автоматической загрузки ресурсов заставляет библиотеку использовать офлайн‑языковые пакеты, которые вы предоставляете.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Почему это важно:**  
> *GPU‑ускорение* может сократить время обработки с секунд до миллисекунд при больших партиях. Установка `AutomaticResourceDownload` в `false` гарантирует работу демо в офлайн‑режиме — критически важное требование для многих корпоративных сред.

## Шаг 2: Загрузка изображения из потока

Чтение изображения через поток даёт гибкость: файлы можно брать с диска, сетевых ресурсов или даже из кэша в памяти. Здесь мы открываем локальный JPEG‑файл, но тот же шаблон работает с любым `Stream`.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Pro tip:** Если вам нужно обрабатывать изображения, загруженные через веб‑API, просто замените `File.OpenRead` на `IFormFile.OpenReadStream()` — остальное остаётся неизменным.

## Шаг 3: Выбор корейского языка и применение предобработки

Aspose.OCR поддерживает несколько шагов предобработки, которые очищают изображение перед распознаванием. Для корейских знаков обычно хватает выравнивания (deskew) и шумоподавления (denoise).

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **Что происходит под капотом?**  
> Фильтр `Deskew` выравнивает наклонённый текст, а `Denoise` удаляет зернистость, которая может сбить классификатор символов. Пропуск этих шагов часто приводит к искажённому выводу, особенно на фотографиях низкого разрешения.

## Шаг 4: Асинхронное извлечение простого текста

Настал момент истины — попросить движок распознать символы и вернуть чистую строку. Использование `RecognizeAsync` сохраняет отзывчивость UI, если вы внедряете этот код в настольное или веб‑приложение.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

При запуске программы вы должны увидеть что‑то вроде:

```
OCR complete. Extracted text:
서울시청
```

> **Зачем async?**  
> OCR может быть ресурсоёмким. Асинхронное выполнение не блокирует ваш поток, что особенно удобно в ASP.NET Core, где голодание потоков — реальная проблема.

## Шаг 5: Получение подробного результата распознавания и сохранение в JSON

Иногда нужен не только сырой текст — возможно, вам нужны оценки уверенности, ограничивающие рамки (bounding boxes) или оригинальные данные изображения. Метод `RecognizeDetailed` возвращает объект `RecognitionResult`, который можно сериализовать в JSON для последующего анализа.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

Открытие `korean_ocr.json` покажет структуру, похожую на:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **Когда это полезно?**  
> Если вы строите поисковый индекс, значения уверенности позволяют отфильтровать низкокачественные результаты. Если нужно подсвечивать текст в UI, ограничивающие рамки — ваш план.

## Шаг 6: Преобразование изображения в PDF и экспорт поискового PDF

Aspose делает переход от растрового к векторному формату простым. Установив `OutputFormat` в `SearchablePdf`, библиотека встраивает оригинальное изображение и накладывает невидимый слой текста с результатами OCR. Полученный PDF можно искать, копировать и индексировать, как любой нативный PDF.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

Откройте `korean_searchable.pdf` в Adobe Reader или любом PDF‑просмотрщике, нажмите **Ctrl+F**, введите корейское слово и увидите, как документ мгновенно переходит к нужному месту. Это и есть сила поискового PDF.

> **Дополнительный совет:** Если нужен только визуальный PDF без скрытого текстового слоя, переключите `OutputFormat` на `Pdf`.

## Полный рабочий пример

Ниже полный код программы — скопируйте, вставьте, замените `YOUR_DIRECTORY` реальным путём и нажмите **F5**.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Ожидаемый вывод в консоль

```
OCR complete. Extracted text:
서울시청
```

И вы найдёте три новых файла рядом с исходным изображением:

- `korean_ocr.json` — полные данные распознавания.  
- `korean_searchable.pdf` — PDF, по которому можно выполнять поиск.  
- (по желанию) любые промежуточные логи, которые вы решите добавить.

## Часто задаваемые вопросы и особые случаи

**Что делать, если нет GPU?**  
Установите `EnableGpu = false`; откат на CPU полностью приемлем для небольших партий.

**Можно ли обрабатывать несколько изображений за один запуск?**  
Конечно. Оберните основную логику в цикл `foreach (var file in Directory.GetFiles(...))` и переassign `ocrEngine.Image` на каждой итерации.

**Как работать с другими языками вместе с корейским?**  
Aspose.OCR позволяет задать `Language = Language.AutoDetect` или комбинировать языки побитовым ИЛИ (например, `Language.Korean | Language.English`).

**Что если уверенность OCR низкая?**  
Исследуйте `detailedResult.Pages[0].Words` и отфильтруйте элементы с `Confidence < 0.7`. Также можно подправить предобработку — попробуйте добавить `PreprocessFilter.ContrastEnhancement`.

## Подведение итогов

Вы только что увидели, как выполнить **OCR корейского языка** от начала до конца: от **загрузки изображения из потока** до **извлечения простого текста**, затем **преобразования изображения в PDF** и, наконец, **экспорта поискового PDF**. Подход модульный, поэтому вы можете менять источник изображения, формат вывода или передавать JSON в любую downstream‑конвейерную систему.

Что дальше


## Похожие руководства

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}