---
category: general
date: 2026-02-27
description: Создайте поисковый PDF из отсканированного PDF за секунды с помощью Aspose
  OCR. Узнайте, как конвертировать отсканированный PDF, выполнять OCR‑конвертацию
  PDF и без усилий извлекать текст из PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- ocr convert pdf
- extract text from pdf
- convert image pdf
language: ru
og_description: Создайте PDF с возможностью поиска мгновенно. Этот учебник показывает,
  как конвертировать отсканированный PDF, выполнять OCR‑конвертацию PDF и извлекать
  текст из PDF с помощью Aspose OCR.
og_title: Создание PDF с поисковым индексом – Краткое руководство по Aspose OCR
tags:
- Aspose OCR
- C#
- PDF processing
title: Создать поисковый PDF из отсканированных изображений с помощью Aspose OCR
url: /ru/net/text-recognition/create-searchable-pdf-from-scanned-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из отсканированных изображений с помощью Aspose OCR

Когда‑нибудь вам нужно было **создать поисковый PDF** из бумажного счета‑фактуры, но вы не знали, с чего начать? С Aspose OCR вы можете **создать поисковый PDF** всего в несколько строк C# — без внешних сервисов, без ручного копирования‑вставки.  

В этом руководстве мы пройдем всё, что нужно, чтобы **convert scanned pdf** файлы в полностью поисковые PDF, объясним, почему каждый шаг важен, и даже покажем, как **extract text from pdf**, если вам нужны сырые строки вместо PDF‑вывода. К концу у вас будет переиспользуемый фрагмент кода, решающий распространённую проблему «PDF только с изображениями», а также несколько советов для особых случаев.

![создание поискового pdf с помощью Aspose OCR](image-placeholder.png "создание поискового pdf с помощью Aspose OCR")

## Что понадобится

- .NET 6.0 или новее (API работает на .NET Core, .NET Framework и .NET 5+)
- Visual Studio 2022 (или любой другой редактор по вашему выбору)
- Пакет NuGet Aspose OCR (`Aspose.OCR`) — мы установим его в первом шаге
- Отсканированный PDF‑файл (только изображения), который вы хотите превратить в **searchable PDF**

И всё—никаких дополнительных OCR‑движков, никаких проблем с лицензией для пробного запуска.  

Теперь давайте погрузимся.

## Шаг 1: Установите библиотеку Aspose OCR (и быстрый совет)

Прежде чем любой код выполнится, библиотеку необходимо подключить. Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

**Совет:** Если вы используете Package Manager в Visual Studio, найдите “Aspose.OCR” и нажмите **Install**. Бесплатная пробная версия работает до 20 страниц, что идеально для тестирования.

Установка пакета даёт вам доступ к `OcrEngine`, `OcrLanguage` и `OcrOutputFormat` — трем классам, которые мы будем использовать для **ocr convert pdf**.

## Шаг 2: Настройте OCR‑движок (Создание поискового PDF – основные параметры)

Движку необходимо знать, какой язык распознавать и в каком формате выводить результат. В нашем случае нам нужен PDF на английском языке, который будет поисковым.

```csharp
using Aspose.OCR;
using System;

// Step 2: Set up the OCR engine
var ocrEngine = new OcrEngine
{
    // Choose the language of the source document
    Language = OcrLanguage.English,

    // Tell Aspose we want a searchable PDF as the result
    OutputFormat = OcrOutputFormat.SearchablePdf
};
```

Зачем явно задавать `Language`? Точность OCR резко падает, когда движок угадывает язык, особенно в документах, содержащих цифры или смешанные скрипты. Привязав его к английскому, мы получаем более чистый текстовый слой, что, в свою очередь, улучшает шаг **extract text from pdf** позже.

## Шаг 3: Преобразуйте отсканированный PDF в поисковый PDF

Теперь, когда движок готов, укажите ему исходный файл и путь для записи результата. Этот один вызов делает всю тяжелую работу: растеризует каждую страницу, запускает OCR и записывает новый PDF с невидимым текстовым слоем.

```csharp
// Step 3: Perform the conversion
ocrEngine.RecognizePdf(
    @"C:\Docs\invoice_scanned.pdf",   // input – image‑only PDF
    @"C:\Docs\invoice_searchable.pdf" // output – searchable PDF
);
```

Если исходный PDF содержит несколько страниц, Aspose OCR обрабатывает их последовательно, сохраняя оригинальное расположение. Выходной файл можно открыть в любом PDF‑просмотрщике; вы заметите, что теперь можно выделять и искать слова, которые ранее были лишь изображениями.

### Проверка результата (Извлечение текста из PDF)

Чтобы быть полностью уверенным, что конвертация прошла успешно, вы можете программно извлечь текст:

```csharp
using Aspose.Pdf;           // Add Aspose.PDF if you also need text extraction
using System.Text;

// Load the newly created searchable PDF
var doc = new Document(@"C:\Docs\invoice_searchable.pdf");
var sb = new StringBuilder();

foreach (Page page in doc.Pages)
{
    // Extract the hidden text layer
    sb.Append(page.Text);
}

Console.WriteLine("Extracted text:\n" + sb.ToString());
```

Этот фрагмент кода показывает, как после шага OCR **extract text from pdf**, что удобно для индексации или передачи содержимого в поисковую систему. Обратите внимание, что для этой части нужен отдельный пакет `Aspose.PDF`; это лёгкое дополнение.

## Шаг 4: Обработка распространённых особых случаев при **Convert Image PDF**

Хотя базовый процесс работает для большинства PDF, реальные файлы могут бросать неожиданные проблемы:

| Ситуация | Почему происходит | Как решить |
|-----------|----------------|------------------|
| **Повернутые страницы** | Сканеры иногда автоматически поворачивают страницы на 90°. | Установите `ocrEngine.RotatePages = true` перед вызовом `RecognizePdf`. |
| **Смешанные языки** | Счета могут содержать французские или немецкие термины. | Используйте `OcrLanguage.Multilingual` или комбинируйте несколько языков с помощью `|` (например, `OcrLanguage.English | OcrLanguage.French`). |
| **Большие файлы (> 100 страниц)** | Ограничения бесплатной пробной версии могут остановить обработку посередине файла. | Приобретите лицензию или разбейте PDF на части с помощью `Aspose.Pdf` перед OCR. |
| **Сканы с низким разрешением** | Текст становится размытым, точность OCR падает. | Увеличьте DPI, используя `ocrEngine.ImageResolution = 300` (по умолчанию 200). |

Учет этих сценариев гарантирует, что ваш конвейер **ocr convert pdf** останется надёжным в продакшене.

## Шаг 5: Автоматизируйте весь процесс (оберните его в метод)

Если вы создаёте сервис обработки счетов, вам, вероятно, понадобится переиспользуемый метод. Ниже компактная версия, принимающая пути ввода и вывода, обрабатывающая вращение и возвращающая извлечённый текст.

```csharp
using Aspose.OCR;
using Aspose.Pdf;
using System;
using System.Text;

public static class PdfSearchableHelper
{
    /// <summary>
    /// Converts an image‑only PDF to a searchable PDF and returns the hidden text.
    /// </summary>
    /// <param name="inputPath">Path to the scanned PDF.</param>
    /// <param name="outputPath">Path where the searchable PDF will be saved.</param>
    /// <returns>All extracted text as a single string.</returns>
    public static string ConvertAndExtract(string inputPath, string outputPath)
    {
        // 1️⃣ Initialize OCR engine
        var ocr = new OcrEngine
        {
            Language = OcrLanguage.English,
            OutputFormat = OcrOutputFormat.SearchablePdf,
            RotatePages = true,            // fixes rotated scans automatically
            ImageResolution = 300          // improve accuracy on low‑res scans
        };

        // 2️⃣ Perform conversion
        ocr.RecognizePdf(inputPath, outputPath);

        // 3️⃣ Load result and pull out hidden text
        var doc = new Document(outputPath);
        var sb = new StringBuilder();

        foreach (Page page in doc.Pages)
            sb.Append(page.Text);

        return sb.ToString();
    }
}
```

Теперь вы можете вызвать:

```csharp
string extracted = PdfSearchableHelper.ConvertAndExtract(
    @"C:\Docs\contract_scanned.pdf",
    @"C:\Docs\contract_searchable.pdf");

Console.WriteLine("OCR completed. Extracted text length: " + extracted.Length);
```

Это полностью готовый рабочий процесс **convert image pdf** → **searchable PDF**, упакованный в один метод, который можно добавить в любой сервис ASP.NET Core или консольное приложение.

## Часто задаваемые вопросы (FAQ)

**В: Работает ли это на macOS/Linux?**  
**О: Да, безусловно. Среда выполнения .NET 6 и Aspose OCR кросс‑платформенные, поэтому один и тот же код работает в Windows, macOS и Linux‑контейнерах.**

**В: Что если мне нужен только текст и меня не интересует поисковый PDF?**  
**О: Пропустите шаг `OutputFormat` и установите `OutputFormat = OcrOutputFormat.Text`. Движок сразу вернёт обычный текст.**

**В: Могу ли я сохранить метаданные оригинального PDF?**  
**О: Да. После конвертации вы можете скопировать метаданные из исходного объекта `Document` в новый, используя `doc.Info.Title`, `doc.Info.Author` и т.д.**

**В: Есть ли ограничение на количество страниц?**  
**О: Бесплатная пробная версия ограничивает документ 20 страницами. Полная лицензия снимает это ограничение.**

## Заключение

Теперь вы знаете, как **create searchable PDF**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}