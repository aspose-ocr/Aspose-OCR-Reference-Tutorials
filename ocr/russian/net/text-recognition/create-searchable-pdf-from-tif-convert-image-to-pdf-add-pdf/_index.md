---
category: general
date: 2026-04-04
description: Создайте поисковый PDF из TIF‑изображения в C# – узнайте, как преобразовать
  изображение в PDF, добавить метаданные PDF и сгенерировать поисковый документ с
  помощью Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: ru
og_description: Создайте PDF с возможностью поиска из файла TIF с помощью C#. Преобразуйте
  изображение в PDF, добавьте метаданные PDF и получите документ, поддерживающий поиск,
  используя Aspose.OCR.
og_title: Создание поискового PDF из TIF – пошаговое руководство
tags:
- Aspose.OCR
- C#
- PDF generation
title: Создать поисковый PDF из TIF – преобразовать изображение в PDF, добавить метаданные
  PDF
url: /ru/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из TIF – Полный пошаговый пример на C#

Когда‑нибудь вам нужно было **создать поисковый PDF** из отсканированного счета, но вы не знали, как сохранить текст поисковым и упорядочить метаданные файла? Вы не одиноки. Во многих проектах автоматизации PDF должен быть как машинно‑читаемым, так и правильно помеченным информацией, такой как заголовок, автор и пороги уверенности.  

В этом руководстве мы пройдемся по полному решению, которое **преобразует изображение в PDF**, внедряет **метаданные PDF** и фильтрует результаты OCR с низкой уверенностью — все с помощью библиотеки Aspose.OCR. К концу вы получите готовый фрагмент кода, который можно вставить в любой .NET‑проект, а также несколько советов по обработке граничных случаев.

## Требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.6+)  
- NuGet‑пакет Aspose.OCR (`Install-Package Aspose.OCR`)  
- TIF‑изображение, которое вы хотите превратить в поисковый PDF (например, `input.tif`)  
- Базовые знания C# и Visual Studio (или вашей любимой IDE)

Никакие внешние сервисы не требуются — весь процесс выполняется локально.

## Шаг 1 – Настройка OCR‑движка (Создание ядра поискового PDF)

Первое, что нам нужно, — экземпляр `OcrEngine`, знающий, какой язык распознавать. В большинстве бизнес‑сценариев достаточно английского, но вы можете заменить `Language.English` на любой поддерживаемый язык.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Почему это важно:** OCR‑движок выполняет тяжёлую работу по преобразованию растровых пикселей в Unicode‑текст. Правильная установка языка повышает точность и уменьшает количество слов с низкой уверенностью, которые позже будут отфильтрованы.

> **Pro tip:** Если вы обрабатываете многоязычные документы, создайте несколько движков или используйте `Language.Multilingual`, чтобы Aspose автоматически определял язык.

## Шаг 2 – Загрузка TIF‑изображения (Создание PDF из TIF)

Теперь указываем движку исходный файл. Помощник `ImageStream.FromFile` читает изображение в поток, который может потреблять OCR‑движок.

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

Вы можете задаться вопросом: *«Можно ли подать JPEG или PNG вместо этого?»* Конечно — Aspose.OCR поддерживает большинство растровых форматов. Просто измените расширение файла, и всё готово.

## Шаг 3 – Настройка параметров PDF (Добавление метаданных в PDF)

Перед конвертацией мы создаём объект `PdfOptions`. Здесь мы **добавляем метаданные PDF**, такие как заголовок и автор, а также указываем движку отбрасывать слова, уверенность которых ниже порога.

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**Что происходит?**  
- `Title` и `Author` становятся частью словаря информации документа PDF, что упрощает индексацию в системах управления документами.  
- `MinConfidence` — это предохранитель: OCR часто ошибается с бледными символами; фильтрация их сохраняет чистый поисковый слой и улучшает последующее извлечение текста.

Если нужны пользовательские метаданные (например, `Subject`, `Keywords`), их можно задать через `PdfOptions.CustomProperties`.

## Шаг 4 – Преобразование изображения в поисковый PDF (Конвертация изображения в PDF)

После подготовки движка и параметров последний вызов выполняет конвертацию. Он записывает поисковый PDF на диск, внедряя слой текста OCR под оригинальным изображением.

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

После выполнения этой строки `output.pdf` будет содержать:
- Исходное TIF‑изображение в качестве визуального фона  
- Невидимый текстовый слой, который могут читать поисковые системы и операции копирования‑вставки  
- Метаданные, определённые ранее (заголовок, автор и т.д.)

### Ожидаемый результат

Откройте сгенерированный PDF в Adobe Reader или любом другом просмотрщике и попробуйте выделить текст. Вы сможете копировать предложения, соответствующие оригинальному скану. В диалоговом окне **Properties** документа будет отображён заголовок «Invoice #12345» и автор «MyCompany».

## Шаг 5 – Проверка фильтрации по уверенности (Зачем нужен MinConfidence)

Полезно убедиться, что слова с низкой уверенностью действительно удалены. Вы можете просмотреть скрытый текст PDF с помощью инструмента, например `pdftotext`:

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

Если слово не появляется, фильтр `MinConfidence` сработал как задумано. При необходимости отрегулируйте порог (например, `0.7f`) для более агрессивной или мягкой фильтрации.

## Шаг 6 – Обработка нескольких страниц (Создание поискового PDF из многостраничного TIF)

Многие счета приходят в виде многостраничных TIFF‑файлов. Aspose.OCR автоматически рассматривает каждый кадр как отдельную страницу. Просто укажите движку многостраничный файл; тот же вызов `ConvertToSearchablePdf` создаст многостраничный поисковый PDF.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**Edge case:** Если страница пустая, OCR может всё равно создать пустой текстовый слой, что безвредно. Однако вы можете пропускать пустые страницы, проверяя `ocrEngine.HasText` перед конвертацией.

## Шаг 7 – Сборка полного примера (Все шаги вместе)

Ниже представлен единый, готовый к запуску пример программы, объединяющий всё. Замените `YOUR_DIRECTORY` реальным путём к папке на вашем компьютере.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

Запустите программу (`dotnet run` или нажмите **F5** в Visual Studio) — вы увидите сообщение подтверждения. Сгенерированный PDF окажется рядом с исходным изображением, готовый к индексации или архивированию.

## Часто задаваемые вопросы и подводные камни

| Question | Answer |
|----------|--------|
| **Can I add a custom font to the searchable layer?** | The OCR layer uses Unicode; the visual appearance is driven by the underlying image, so no extra font embedding is required. |
| **What if my TIF is colored?** | Aspose.OCR automatically converts color images to grayscale for OCR, but you can keep the original colors in the PDF by setting `PdfOptions.PreserveColor = true`. |
| **Is the library thread‑safe?** | Each `OcrEngine` instance should be used by a single thread. For parallel processing, create a separate engine per thread. |
| **How do I encrypt the PDF?** | Use `PdfOptions.Security` to set a password and permissions after the OCR conversion. |

## Следующие шаги (Расширяем ваш PDF‑инструментарий)

- **Batch processing:** Loop over a folder of TIFFs and generate a searchable PDF for each.  
- **Post‑processing:** Use Aspose.PDF to merge the generated PDFs into a single master document.  
- **Advanced metadata:** Populate custom XMP fields for better integration with SharePoint or ECM systems.  

Все эти расширения опираются на основной шаблон, который мы только что рассмотрели: **create searchable PDF**, **convert image to PDF**, and **add PDF metadata**.

*Happy coding! If you run into any snags, drop a comment below or check the Aspose.OCR documentation for the latest API updates.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}