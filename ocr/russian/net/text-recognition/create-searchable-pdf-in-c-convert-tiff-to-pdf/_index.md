---
category: general
date: 2026-02-17
description: Создайте поисковый PDF из многостраничного TIFF в C# с использованием
  Aspose OCR. Узнайте, как за несколько минут преобразовать TIFF в PDF и записать
  PDF в файл.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- write pdf to file
- ocr engine c#
- convert multi page tiff
language: ru
og_description: Создайте поисковый PDF из многостраничного TIFF с помощью Aspose OCR
  на C#. Это руководство показывает, как преобразовать TIFF в PDF и записать PDF в
  файл.
og_title: Создание PDF с поиском в C# – Конвертация TIFF в PDF
tags:
- Aspose OCR
- C#
- PDF generation
title: Создание PDF с поиском в C# – конвертация TIFF в PDF
url: /ru/net/text-recognition/create-searchable-pdf-in-c-convert-tiff-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF в C# – Конвертация TIFF в PDF

Когда‑нибудь вам нужно было **create searchable PDF** из отсканированного документа, но вы не знали, с чего начать? Вы не одиноки. Во многих проектах офисной автоматизации требуется превратить многостраничный TIFF в PDF, который можно искать, копировать и индексировать.  

В этом руководстве мы пройдем полный готовый к запуску пример, который покажет, как **create searchable PDF** с помощью Aspose OCR, как **convert tiff to pdf**, и как **write pdf to file** на диск. К концу вы поймёте весь конвейер, почему каждый элемент важен и на что обратить внимание, работая с **ocr engine c#** в сценарии **convert multi page tiff**.

## Что вы построите

- Загрузить многостраничное TIFF‑изображение с диска.  
- Выполнить OCR на каждой странице с использованием `OcrEngine` из Aspose OCR.  
- Передать полученный поисковый PDF в память.  
- Сохранить PDF в файл одним вызовом `WriteAllBytes`.  

Никаких внешних сервисов, никаких сложных командных утилит — только чистый C#‑код, который можно вставить в любое консольное приложение .NET.

> **Pro tip:** Aspose OCR — коммерческая библиотека, но бесплатная пробная версия отлично подходит для обучения. Убедитесь, что установили действующую лицензию, если планируете использовать её в продакшене.

## Предварительные требования

- .NET 6.0 SDK (или любая современная версия .NET).  
- Visual Studio 2022 или VS Code — подойдёт ваша любимая IDE.  
- NuGet‑пакет Aspose.OCR (`dotnet add package Aspose.OCR`).  
- Многостраничный TIFF‑файл (`multi_page.tif`) в известной папке.

Вот и всё. Дополнительная конфигурация не требуется.

![Create searchable PDF example](https://example.com/create-searchable-pdf.png){: .align-center alt="Create searchable PDF example"}

## Шаг 1 – Инициализация OCR Engine (ocr engine c#)

Прежде чем обработать изображение, нам нужен экземпляр `OcrEngine`. Этот объект хранит все настройки OCR и выполняет тяжёлую работу «за кулисами».

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;
using System;
using System.IO;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

Зачем создавать новый движок при каждом запуске? Движок кэширует внутренние ресурсы; его освобождение после использования освобождает нативную память, что критично при работе с большими многостраничными TIFF‑файлами.

## Шаг 2 – Загрузка многостраничного TIFF (convert multi page tiff)

Aspose OCR может читать поток TIFF напрямую, поэтому просто указываем путь к файлу на диске.

```csharp
        // Step 2: Load the multi‑page TIFF image to be processed
        ImageStream tiffImage = ImageStream.FromFile("YOUR_DIRECTORY/multi_page.tif");
```

Если ваш TIFF находится в потоке (например, из базы данных), замените `FromFile` на `FromStream`. Движок автоматически определяет количество страниц, поэтому такой подход работает для **convert multi page tiff** без дополнительного цикла.

## Шаг 3 – Подготовка MemoryStream для PDF (write pdf to file)

Мы не пишем сразу на диск, потому что потоковая передача позволяет проверить размер PDF, зашифровать его или отправить по HTTP перед сохранением.

```csharp
        // Step 3: Prepare a memory stream that will hold the generated PDF
        using (MemoryStream pdfMemoryStream = new MemoryStream())
        {
```

Блок `using` гарантирует, что поток будет освобождён, предотвращая утечки файловых дескрипторов — проблема, с которой можно столкнуться в длительно работающих сервисах.

## Шаг 4 – Запуск OCR и сохранение как поискового PDF (create searchable pdf)

Теперь основная операция: передать TIFF в `SaveAsSearchablePdf`. Метод выполняет OCR постранично и записывает PDF с невидимым текстовым слоем.

```csharp
            // Step 4: Run OCR on the image and write the searchable PDF into the memory stream
            ocrEngine.SaveAsSearchablePdf(tiffImage, pdfMemoryStream);
```

Внутри Aspose создаёт страницу PDF для каждого кадра TIFF, запускает OCR‑движок и накладывает распознанный текст. Это точный механизм, который превращает отсканированный документ в вывод **create searchable pdf**.

## Шаг 5 – Запись PDF на диск (write pdf to file)

Наконец, сбрасываем буфер памяти в физический файл.

```csharp
            // Step 5: Save the PDF from the memory stream to a file on disk
            File.WriteAllBytes("YOUR_DIRECTORY/result.pdf", pdfMemoryStream.ToArray());
        }
```

`WriteAllBytes` атомарен на большинстве платформ, что означает отсутствие частично записанных файлов даже при сбое процесса. Если нужно добавить данные к существующему PDF, рассмотрите использование Aspose.PDF.

## Шаг 6 – Сообщение подтверждения

Краткое сообщение в консоли сообщает, что всё прошло успешно.

```csharp
        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created.");
    }
}
```

Запустите программу, укажите реальный TIFF, и вы найдёте `result.pdf` рядом с исходным файлом. Откройте его в любом PDF‑просмотрщике и попробуйте выделить текст — вы увидите слой OCR в действии.

## Обработка граничных случаев и распространённых подводных камней

| Situation | What to Do |
|-----------|------------|
| **Very large TIFF (hundreds of MB)** | Увеличьте лимит памяти процесса или обрабатывайте страницы пакетами: загружайте один кадр за раз, вызывайте `SaveAsSearchablePdf` с `PdfSaveOptions`, который добавляет к существующему потоку. |
| **OCR language not English** | Установите `ocrEngine.Language = Language.Spanish;` (или любой поддерживаемый язык) перед вызовом `SaveAsSearchablePdf`. |
| **Missing license** | Пробная версия добавляет водяной знак. Зарегистрируйте лицензию с помощью `License license = new License(); license.SetLicense("Aspose.OCR.lic");`. |
| **Corrupt TIFF file** | Оберните `ImageStream.FromFile` в try/catch и запишите детали `Aspose.OCR.Exception`. |
| **Need searchable PDF without images** | Используйте `PdfSaveOptions` → `RemoveImages = true`, чтобы уменьшить размер вывода. |

Эти рекомендации делают решение достаточно надёжным для производственных нагрузок.

## Полный рабочий пример (все шаги вместе)

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;
using System;
using System.IO;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: set language if needed
        // ocrEngine.Language = Language.English;

        // Step 2: Load the multi‑page TIFF image to be processed
        ImageStream tiffImage = ImageStream.FromFile("YOUR_DIRECTORY/multi_page.tif");

        // Step 3: Prepare a memory stream that will hold the generated PDF
        using (MemoryStream pdfMemoryStream = new MemoryStream())
        {
            // Step 4: Run OCR on the image and write the searchable PDF into the memory stream
            ocrEngine.SaveAsSearchablePdf(tiffImage, pdfMemoryStream);

            // Step 5: Save the PDF from the memory stream to a file on disk
            File.WriteAllBytes("YOUR_DIRECTORY/result.pdf", pdfMemoryStream.ToArray());
        }

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**Expected result:** `result.pdf` появляется в `YOUR_DIRECTORY`. При открытии он показывает каждую оригинальную страницу TIFF плюс скрытый, выделяемый текстовый слой — именно то, что нужно для **create searchable pdf** из отсканированных изображений.

## Итоги

Мы рассмотрели всё, что нужно для **create searchable PDF** в рамках рабочего процесса **convert tiff to pdf**, включая как **write pdf to file**, роль **ocr engine c#** и особые нюансы источника **convert multi page tiff**. Код автономный, работает на .NET 6+ и может быть адаптирован под веб‑API или фоновые сервисы с минимальными изменениями.

### Что дальше?

- **Add password protection** с помощью `PdfSaveOptions`, если PDF содержит конфиденциальные данные.  
- **Compress the output**, настроив `PdfSaveOptions.CompressionLevel`.  
- **Integrate with ASP.NET Core**, чтобы обслуживать PDF напрямую в браузерах.  
- **Explore Azure Functions** для безсерверных OCR‑конвейеров.

Не стесняйтесь экспериментировать — меняйте входной формат, пробуйте разные языки OCR или передавайте PDF в систему управления документами. Возможности безграничны, когда вы знаете, как **convert tiff to pdf** и **write pdf to file** программно.

Счастливого кодинга, и пусть ваши PDF всегда будут поисковыми!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}