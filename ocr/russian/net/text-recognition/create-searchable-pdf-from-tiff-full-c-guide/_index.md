---
category: general
date: 2025-12-29
description: Создайте поисковый PDF из многостраничного TIFF и узнайте, как конвертировать
  TIFF в PDF, извлекать текст из TIFF и программно генерировать PDF.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- convert image to pdf
- how to generate pdf
- extract text from tiff
language: ru
og_description: Создайте поисковый PDF из многостраничного TIFF с помощью Aspose OCR.
  Узнайте, как конвертировать TIFF в PDF, извлекать текст из TIFF и генерировать PDF
  на C#.
og_title: Создание PDF с поиском из TIFF – пошаговый учебник по C#
tags:
- Aspose OCR
- C#
- PDF/A
- Document Automation
title: Создать поисковый PDF из TIFF – Полное руководство по C#
url: /ru/net/text-recognition/create-searchable-pdf-from-tiff-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из TIFF – Полное руководство C#

Когда‑то вам нужно было **создать поисковый PDF** из отсканированного TIFF, но вы не знали, с чего начать? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, когда им требуется документ PDF/A‑2b, который может индексироваться поисковыми системами. В этом руководстве мы пройдемся по точному коду, который вам нужен, объясним, почему каждая строка важна, и покажем, как **конвертировать tiff в pdf** без потери текста.

Мы также коснёмся связанных задач, таких как **конвертировать изображение в pdf**, ответим на вопрос **как сгенерировать pdf** в C#, и продемонстрируем, как **извлечь текст из tiff** с помощью Aspose.OCR. К концу вы получите готовый к запуску пример, который можно добавить в любой проект .NET.

---

## Что вы узнаете

- Настроить OCR‑движок с Aspose.OCR.  
- Загрузить многостраничный TIFF‑файл и выполнить распознавание текста.  
- Сохранить результат OCR в виде поискового PDF/A‑2b документа.  
- Обработать типичные подводные камни (большие файлы, использование памяти, настройки DPI).  
- Расширить решение для других форматов изображений или пакетной обработки.

**Требования**  
- .NET 6.0 или новее (код также работает на .NET Framework 4.8).  
- Действительная лицензия Aspose.OCR (или временный оценочный ключ).  
- Visual Studio 2022 или любой другой предпочитаемый IDE для C#.

---

## Шаг 1 – Установить пакет Aspose.OCR NuGet

Прежде чем мы сможем **создать поисковый pdf**, нам нужна OCR‑библиотека, которая выполнит всю тяжёлую работу.

```bash
dotnet add package Aspose.OCR
```

> **Полезный совет:** Если вы используете CI‑конвейер, зафиксируйте версию (например, `Aspose.OCR --version 23.10`), чтобы избежать неожиданных несовместимых изменений.

---

## Шаг 2 – Инициализировать OCR‑движок

Создание движка — первое, что делается, когда вы хотите **конвертировать tiff в pdf**. Движок хранит конфигурацию, такую как язык, разрешение и флаги производительности.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create an OCR engine instance – this object will be reused for every image.
var ocrEngine = new OcrEngine
{
    // Optional: set language to English (default is English + Latin).
    Language = Language.English,
    // Optional: improve speed for large files by limiting the max memory usage.
    // MaxMemoryUsage = 1024 * 1024 * 200 // 200 MB
};
```

*Почему это важно:* Инициализировать движок один раз и переиспользовать его снижает накладные расходы, особенно когда позже вы **конвертируете изображение в pdf** в пакетной задаче.

---

## Шаг 3 – Загрузить многостраничный TIFF

Aspose.OCR работает с классом `Image` из той же библиотеки. Загрузка многостраничного TIFF проста — достаточно указать путь к файлу.

```csharp
// Load the TIFF file from disk. Replace the path with your actual location.
var inputImage = Image.Load(@"C:\Docs\input.tif");

// If you need to work with a different format (PNG, JPEG), the same method works.
```

*Особый случай:* Некоторые TIFF‑файлы содержат сжатие, которое Aspose.OCR не может прочитать. Если возникнет исключение, попробуйте сначала конвертировать TIFF в несжатый формат (например, с помощью ImageMagick).

---

## Шаг 4 – Выполнить OCR и получить результат

Теперь мы действительно **извлекаем текст из tiff**. Метод `Recognize` возвращает `OcrResult`, содержащий как обычный текст, так и PDF‑представление.

```csharp
// Perform OCR on the loaded image.
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// The result includes recognized text (ocrResult.Text) and a PDF stream.
Console.WriteLine("Recognized characters: " + ocrResult.Text.Length);
```

*Что происходит «под капотом»?* Движок сканирует каждую страницу, запускает нейронную сеть для обнаружения символов и формирует слой поискового текста, который позже будет встроен в PDF.

---

## Шаг 5 – Сохранить как поисковый PDF/A‑2b

Наконец, мы **создаём поисковый pdf**, сохраняя результат OCR в формате PDF/A‑2b. PDF/A‑2b — это архивный стандарт, гарантирующий долговременную читаемость.

```csharp
// Save the OCR result as a searchable PDF/A‑2b file.
string outputPath = @"C:\Docs\output.pdf";
ocrResult.Save(outputPath, SaveFormat.PdfA2b);

Console.WriteLine($"Searchable PDF saved to: {outputPath}");
```

*Почему PDF/A‑2b?* В отличие от обычного PDF, PDF/A‑2b встраивает все шрифты и цветовые профили, обеспечивая одинаковый вид документа через годы — идеально для отраслей с жёсткими требованиями к соответствию.

---

## Полный рабочий пример

Ниже представлена полная программа, которую можно скопировать и вставить в консольное приложение. В ней собраны все шаги выше, плюс небольшая обработка ошибок.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Initialize OCR engine
                var ocrEngine = new OcrEngine
                {
                    Language = Language.English
                };

                // 2️⃣ Load the multi‑page TIFF
                string inputPath = @"C:\Docs\input.tif";
                var inputImage = Image.Load(inputPath);

                // 3️⃣ Recognize text
                OcrResult ocrResult = ocrEngine.Recognize(inputImage);
                Console.WriteLine($"Extracted {ocrResult.Text.Length} characters.");

                // 4️⃣ Save as searchable PDF/A‑2b
                string outputPath = @"C:\Docs\output.pdf";
                ocrResult.Save(outputPath, SaveFormat.PdfA2b);
                Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
            }
        }
    }
}
```

*Ожидаемый вывод:* После запуска вы увидите строку в консоли, подтверждающую количество символов, и ещё одну строку с путём к PDF. Открытие `output.pdf` в Adobe Acrobat позволит искать любое слово, присутствующее в оригинальном TIFF.

---

## Визуальный обзор

![Create searchable PDF from TIFF example](https://example.com/images/create-searchable-pdf.png "Create searchable PDF from TIFF example")

*Скриншот показывает PDF, открытый в Acrobat, с подсвеченным найденным текстом в строке поиска.*

---

## Часто задаваемые вопросы и советы

### 1. Что делать, если TIFF содержит много страниц (например, 500)?
Обработка огромного файла за один раз может исчерпать память. Разделите файл на более мелкие партии с помощью `Image.Split()` или сторонней библиотеки, затем перебирайте каждую партию тем же экземпляром `ocrEngine`.

### 2. Можно ли изменить вывод PDF на обычный PDF вместо PDF/A?
Конечно — замените `SaveFormat.PdfA2b` на `SaveFormat.Pdf`. Учтите, что вы потеряете гарантии долговременного архивирования.

### 3. Как **конвертировать изображение в pdf** без OCR (например, для не текстовых изображений)?
Используйте `Image.Save(outputPath, SaveFormat.Pdf)` напрямую. Слой OCR не будет добавлен, но изображение будет встроено как страница.

### 4. Поддерживает ли OCR языки, отличные от английского?
Да. Установите `ocrEngine.Language = Language.Spanish` (или любой поддерживаемый enum). При необходимости можно загрузить пользовательский языковой пакет.

### 5. Что насчёт DPI и качества изображения?
Большее DPI повышает точность, но увеличивает время обработки. Хорошее правило — 300 dpi для сканированных документов. Регулировать можно через `ocrEngine.Dpi = 300`.

---

## Расширение решения

- **Пакетная конверсия:** Оберните основную логику в `foreach`, который проходит по каталогу TIFF‑файлов.  
- **Облачная интеграция:** После сохранения загрузите сгенерированный PDF в Azure Blob Storage или Amazon S3.  
- **Внедрение метаданных:** Используйте Aspose.PDF для добавления заголовка, автора и пользовательских метаданных в поисковый PDF.

---

## Заключение

Мы только что **создали поисковый PDF** из многостраничного TIFF с помощью Aspose.OCR, рассмотрели, как **конвертировать tiff в pdf**, изучили способы **конвертировать изображение в pdf**, ответили на вопрос **как сгенерировать pdf** программно и показали, как эффективно **извлечь текст из tiff**. С полным примером кода вы можете добавить его в любой проект C# и начать генерировать файлы PDF/A‑2b, которые сразу же становятся поисковыми.

Что дальше? Попробуйте обработать пакет счетов‑фактур, поэкспериментируйте с различными настройками языков или объедините этот рабочий процесс с системой управления документами. Возможности безграничны, как только вы узнаете, как **создавать поисковый pdf** в масштабе.

Если у вас возникли трудности или есть идеи по улучшению, оставляйте комментарий. Приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}