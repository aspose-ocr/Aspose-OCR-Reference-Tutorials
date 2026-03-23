---
category: general
date: 2026-03-23
description: Создайте PDF с возможностью поиска из изображения с помощью Aspose OCR.
  Узнайте, как за несколько минут преобразовать TIFF в PDF с высоким уровнем сжатия
  и распознать текст на изображении.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- high compression pdf
- recognize image text
- searchable pdf from image
language: ru
og_description: Создайте PDF с возможностью поиска текста из изображения с помощью
  Aspose OCR. В этом руководстве показано, как преобразовать TIFF в PDF, добавить
  слой распознаваемого текста и применить высокое сжатие.
og_title: Создание PDF с возможностью поиска из изображения – Полное руководство по
  C#
tags:
- Aspose OCR
- C#
- PDF generation
title: Создание PDF с возможностью поиска из изображения — Полное руководство по C#
url: /ru/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из изображения – Полное руководство на C#

Когда‑то вам нужно **создать поисковый pdf** из отсканированного документа, но вы не знали, с чего начать? Вы не одиноки — многие разработчики сталкиваются с той же проблемой при преобразовании TIFF‑сканов в поисковые PDF. Хорошая новость? С Aspose OCR вы можете **конвертировать tiff в pdf**, добавить скрытый текстовый слой и даже уменьшить размер файла с помощью опций **high compression pdf**, всё это в нескольких строках C#.

В этом руководстве мы пройдём весь процесс: от установки нужных пакетов NuGet, загрузки TIFF‑изображения, распознавания текста и, наконец, экспорта поискового PDF. В конце у вас будет готовое консольное приложение, которое **recognize image text** и создаёт компактный, поисковый PDF, готовый к индексации. Никаких дополнительных инструментов, никаких ручных шагов OCR — только чистый код и небольшие пояснения.

## Предварительные требования и что понадобится

- **.NET 6+** (или .NET Framework 4.6+). API работает в обеих средах, но .NET 6 даёт последние улучшения рантайма.  
- **Visual Studio 2022** или любая другая IDE по вашему выбору.  
- Пакеты NuGet **Aspose.OCR** и **Aspose.OCR.Gpu** (пакет GPU необязателен, но ускоряет распознавание на поддерживаемом оборудовании).  
- Пример TIFF‑файла (например, `invoice.tif`), размещённый в папке, которой вы управляете.  

Если у вас уже есть всё перечисленное, отлично — переходите дальше. Если нет, шаг установки ниже покрывает всё необходимое.

## Шаг 1: Установите пакеты Aspose OCR

Для начала откройте папку проекта в терминале и выполните:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Эти команды загрузят как основной движок OCR, так и библиотеку ускорения GPU. Последняя не обязательна; при отсутствии совместимого GPU движок перейдёт в режим CPU.  

> **Pro tip:** При работе в продакшн‑окружении фиксируйте версии пакетов в вашем `csproj`, чтобы избежать неожиданных несовместимостей.

## Шаг 2: Настройте каркас проекта

Создайте новое консольное приложение (если у вас его ещё нет):

```bash
dotnet new console -n PdfExportDemo
cd PdfExportDemo
```

Замените автоматически сгенерированный `Program.cs` полным кодом, показанным ниже. Программа выполнит следующее:

1. Инициализирует `OcrEngine` с поддержкой GPU.  
2. Загружает TIFF‑изображение.  
3. Выполняет OCR и корректно завершает работу при ошибке.  
4. Настраивает **PdfExportOptions** для поискового слоя и **high compression**.  
5. Записывает выходной файл.

## Шаг 3: Напишите полный код (полный пример)

Ниже приведён *весь* исходный файл. Скопируйте‑вставьте его в `Program.cs`. Комментарии объясняют «почему» каждой строки, а не только «что».

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;

class PdfExport
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Initialise OCR engine with GPU acceleration.
        //    GpuMode.Enabled tells Aspose to use the GPU if one is present.
        //    If no compatible GPU exists, the engine automatically falls back
        //    to CPU mode—no extra code required.
        // ------------------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine(GpuMode.Enabled))
        {
            // ------------------------------------------------------------
            // 2️⃣ Load the source image.
            //    ImageStream.FromFile supports many formats; here we use TIFF.
            // ------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\invoice.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // ------------------------------------------------------------
            // 3️⃣ Perform OCR recognition.
            //    Recognize() returns false if the engine cannot read the image.
            //    Exiting early prevents us from creating an empty PDF.
            // ------------------------------------------------------------
            if (!ocrEngine.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return;
            }

            // ------------------------------------------------------------
            // 4️⃣ Configure PDF export options.
            //    IncludeTextLayer = true adds an invisible, searchable text layer.
            //    CompressionLevel = High reduces file size dramatically.
            // ------------------------------------------------------------
            PdfExportOptions pdfExportOptions = new PdfExportOptions
            {
                IncludeTextLayer = true,
                CompressionLevel = PdfCompression.High
            };

            // ------------------------------------------------------------
            // 5️⃣ Save the searchable PDF.
            //    The output will be a compact, searchable PDF ready for indexing.
            // ------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\invoice.pdf";
            ocrEngine.Save(outputPath, pdfExportOptions);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### Почему это работает

- **GPU‑ускорение** может сократить время распознавания с секунд до миллисекунд на современных видеокартах — удобно для массовой обработки.  
- **IncludeTextLayer** внедряет полученный OCR‑текст невидимым слоем, позволяя PDF‑просмотрщикам искать документ без изменения его визуального вида.  
- **High compression** использует Flate (ZIP)‑сжатие потока изображения, которое является без потерь, но значительно уменьшает размер файла — идеально для архивирования тысяч счетов.

## Шаг 4: Запустите приложение и проверьте результат

Откройте терминал в папке проекта и выполните:

```bash
dotnet run
```

Если всё настроено правильно, вы увидите:

```
Searchable PDF saved to: YOUR_DIRECTORY\invoice.pdf
```

Откройте `invoice.pdf` в любом PDF‑читалке (Adobe Acrobat, Edge или даже в браузере). Попробуйте поискать слово, которое точно есть в оригинальном TIFF, например «Total». Просмотрщик должен подсветить слово, хотя оно находится в изображении. Это и есть признак **searchable pdf**.

### Ожидаемый размер файла

Обычный отсканированный счёт (≈300 KB TIFF) часто уменьшается до **~80 KB** после применения `PdfCompression.High`. Точный размер зависит от сложности изображения, но вы заметите явное сокращение.

## Шаг 5: Частые варианты и граничные случаи

| Ситуация | Что изменить | Почему |
|-----------|----------------|-----|
| **Нет доступного GPU** | Заменить `new OcrEngine(GpuMode.Enabled)` на `new OcrEngine(GpuMode.Disabled)` | Предотвращает попытки инициализации GPU, что может вызвать небольшую задержку. |
| **Многостраничный TIFF** | `ocrEngine.Image = ImageStream.FromFile("multi.tif", PageRange.All);` | Загружает все кадры; Aspose обработает каждую страницу и создаст многостраничный PDF. |
| **Необходим язык OCR, отличный от английского** | `ocrEngine.Language = Language.French;` (или любой поддерживаемый язык) | Повышает точность для неанглийских документов. |
| **Нужен видимый текстовый слой вместо скрытого** | `pdfExportOptions.IncludeTextLayer = false;` и вручную добавить объекты `TextFragment`. | Полезно, когда хотите, чтобы OCR‑текст отображался как выделяемый поверх изображения. |
| **Ультра‑маленькие PDF** | Сочетать `PdfCompression.High` с `ImageResolution = 150` DPI до распознавания. | Более низкое DPI уменьшает объём данных изображения, дополнительно сокращая PDF за счёт потери визуального качества. |

> **Note:** Всегда тестируйте граничные случаи на небольшом наборе перед масштабированием в продакшн. Точность OCR может варьироваться в зависимости от качества изображения, шума и языка.

## Шаг 6: Советы для production‑готовых реализаций

1. **Логирование ошибок** — замените `Console.WriteLine` на полноценный фреймворк логирования (Serilog, NLog) для упрощения диагностики.  
2. **Пакетная обработка** — вынесите основную логику в метод, принимающий пути ввода/вывода, затем перебирайте каталог TIFF‑файлов.  
3. **Асинхронный ввод/вывод** — хотя сам Aspose OCR синхронный, загрузка и сохранение файлов могут быть асинхронными, чтобы не блокировать UI‑потоки.  
4. **Безопасность** — если вы предоставляете эту функцию через веб‑API, проверяйте пути файлов и ограничивайте их размер, чтобы избежать злоупотреблений.  
5. **Фиксация версий** — используйте точные номера версий (`<PackageReference Include="Aspose.OCR" Version="23.12.0" />`), чтобы гарантировать одинаковое поведение сборок.

## Заключение

Мы только что создали **полное, сквозное решение**, которое **create searchable pdf** из отсканированных изображений, **convert tiff to pdf**, и делает это с настройками **high compression pdf**, одновременно **recognize image text** с высокой точностью. Полученный **searchable pdf from image** лёгок, поисковый и готов к дальнейшим процессам, таким как индексация, архивирование или e‑discovery.

Есть партия счетов? Вставьте метод в цикл, укажите папку и позвольте Aspose OCR выполнить тяжёлую работу. Хотите поэкспериментировать с разными уровнями сжатия или языковыми пакетами? Код достаточно модульный, чтобы менять эти параметры за секунды.

---

*Готовы к следующему уровню?* Попробуйте добавить водяной знак, внедрить метаданные или даже собрать несколько OCR‑обработанных PDF в один документ. Пакет Aspose предлагает множество расширений — изучайте документацию и продолжайте движение вперёд. Приятного кодинга!

![Create searchable PDF from image example screenshot](https://example.com/images/create-searchable-pdf.png "create searchable pdf example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}