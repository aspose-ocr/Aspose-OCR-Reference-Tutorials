---
category: general
date: 2026-03-21
description: 'Учебник по OCR на C#: Узнайте, как извлекать текст из изображения, сканировать
  счета и загружать изображение в C# с использованием Aspose OCR и ускорением на GPU.'
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- ocr invoice scanning
- how to ocr image
- load image in c#
language: ru
og_description: 'c# OCR tutorial: Пошаговое руководство по извлечению текста из изображения,
  выполнению OCR‑сканирования счетов и изучению того, как выполнять OCR изображения
  в C# с использованием ускорения GPU.'
og_title: c# OCR tutorial – Извлечение текста из изображений с помощью Aspose OCR
tags:
- OCR
- C#
- Image Processing
title: c# OCR tutorial – Извлечение текста из изображений с помощью Aspose OCR
url: /ru/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Извлечение текста из изображений с помощью Aspose OCR

Когда‑то задавались вопросом, как **c# OCR tutorial** решить реальную задачу, например превратить отсканированный счёт в редактируемый текст? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужно *extract text from image* файлы, и в итоге пишут хрупкие парсеры, которые ломаются уже при первом шумном скане.

Дело в том, что Aspose.OCR делает весь процесс простым, особенно если включить ускорение GPU. В этом руководстве вы увидите, **how to ocr image** файлы в C#, правильно загрузить изображение в c#, и даже обработать типичные нюансы сканирования счетов без потери волос.

К концу этого урока у вас будет готовое консольное приложение, которое читает TIFF‑счёт, запускает OCR на GPU и выводит чистый текст. Никакой магии, только надёжный код, который можно скопировать‑вставить и адаптировать.

---

## Что понадобится

- **.NET 6.0** (или новее) – текущая LTS‑версия, так что вы будете в будущем.
- **Aspose.OCR for .NET** NuGet‑пакет – версия 23.10 (на момент написания).
- **GPU‑подключённый компьютер** (необязательно, но рекомендуется) – при отсутствии совместимого GPU код автоматически переключится на CPU.
- Пример изображения, например `large_invoice.tif`. Поддерживается любой из форматов (PNG, JPEG, TIFF, PDF).

Если пакет NuGet ещё не установлен, выполните:

```bash
dotnet add package Aspose.OCR
```

Теперь, когда мы обсудили предварительные требования, перейдём к реальным шагам.

---

## Шаг 1: Создать новый консольный проект и добавить Aspose.OCR

Сначала создайте чистое консольное приложение, чтобы урок был самодостаточным.

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Используйте флаг `-n`, чтобы задать проекту осмысленное имя; это упрощает работу с решением, когда вы начнёте добавлять новые модули.

Файл `Program.cs`, который создаёт Visual Studio, будет нашей площадкой. Откройте его и удалите строку `Console.WriteLine` по умолчанию – мы заменим её на логику OCR.

---

## Шаг 2: Load Image in C# – The Right Way

Загрузка изображения может выглядеть тривиально, но неправильный подход приводит к утечкам памяти или блокировке файла. Класс `System.Drawing.Image` подходит для большинства сценариев, однако его необходимо обернуть в блок `using`, чтобы гарантировать освобождение ресурсов.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 2: Load the image you want to OCR.
            // Replace the path with the actual location of your invoice file.
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // The using statement ensures the image gets disposed automatically.
            using var inputImage = Image.FromFile(imagePath);
            
            // Continue to the OCR engine setup…
        }
    }
}
```

Обратите внимание на комментарий `// 👉 Step 2:` – он отражает нумерацию шагов в нашем руководстве и помогает тем, кто позже будет просматривать код.

---

## Шаг 3: Initialize the OCR Engine with GPU Acceleration

Aspose.OCR позволяет выбрать режим обработки при создании объекта. `OcrEngineMode.Gpu` указывает библиотеке использовать видеокарту, если она обнаружена; иначе она тихо переходит на CPU, и вам не нужно писать дополнительную логику переключения.

```csharp
// 👉 Step 3: Create the OCR engine.
// The constructor argument selects GPU mode; it's the fastest option for large invoices.
var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);
```

> **Почему GPU?**  
> OCR для высокоразрешённых счетов может сильно нагружать процессор. Перенос вычислений на GPU сокращает время выполнения с нескольких секунд до доли секунды, особенно при пакетной обработке.

---

## Шаг 4: Run OCR and Extract Text from Image

Теперь происходит магия. Вызовите `Recognize` и получите обычный текст. Aspose возвращает объект `OcrResult`, содержащий сырой текст, оценки уверенности и даже ограничивающие рамки каждого символа, если они понадобятся позже.

```csharp
// 👉 Step 4: Perform the OCR operation.
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Display the extracted text.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

При запуске программы вы должны увидеть что‑то вроде:

```
=== OCR Output ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

Если вывод выглядит искажённым, проверьте, что изображение имеет высокий контраст и что язык OCR установлен правильно (по умолчанию – English). Вы также можете подправить `ocrEngine.Settings` для повышения точности, но значения по умолчанию подходят для большинства печатных счетов.

---

## Шаг 5: Handling OCR Invoice Scanning Edge Cases

Счета бывают разными — некоторые многостраничные, другие содержат таблицы или рукописные заметки. Ниже несколько быстрых настроек, которые можно применить без полной переделки конвейера.

### 5.1 Multi‑Page PDFs or TIFFs

Если исходный файл содержит несколько страниц, нужно пройтись по каждой и собрать результаты.

```csharp
using var multiPageImage = Image.FromFile(@"C:\Invoices\multi_page_invoice.tif");

// Aspose can split multi‑page TIFFs into separate images.
for (int i = 0; i < multiPageImage.GetFrameCount(FrameDimension.Page); i++)
{
    multiPageImage.SelectActiveFrame(FrameDimension.Page, i);
    using var page = (Image)multiPageImage.Clone();
    var pageResult = ocrEngine.Recognize(page);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

### 5.2 Low‑Resolution Scans

Если DPI ниже 150, увеличьте изображение перед передачей в движок. Это значительно улучшает распознавание символов.

```csharp
// Simple nearest‑neighbor scaling – replace with a better algorithm if needed.
var highRes = new Bitmap(inputImage, new Size(inputImage.Width * 2, inputImage.Height * 2));
var highResResult = ocrEngine.Recognize(highRes);
Console.WriteLine(highResResult.Text);
```

### 5.3 Custom Language Packs

По умолчанию Aspose использует английский. Для других языков скачайте соответствующий языковой пакет с сайта Aspose и зарегистрируйте его:

```csharp
ocrEngine.Settings.Language = OcrLanguage.Spanish; // example for Spanish invoices
```

Эти настройки делают ваше решение **ocr invoice scanning** достаточно надёжным для производственной нагрузки.

---

## Полный рабочий пример

Ниже полностью готовая к запуску программа, включающая все описанные шаги. Скопируйте её в `Program.cs`, поправьте путь к файлу и нажмите **F5**.

```csharp
// ---------------------------------------------------------------
// Complete c# OCR tutorial – Aspose OCR with GPU acceleration
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialize the OCR engine (GPU mode)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);

            // -----------------------------------------------------------------
            // Step 2: Load the image you want to process
            // -----------------------------------------------------------------
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // Using ensures the image is disposed properly.
            using var inputImage = Image.FromFile(imagePath);

            // -----------------------------------------------------------------
            // Step 3: Run OCR and extract plain text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);

            // -----------------------------------------------------------------
            // Step 4: Output the result
            // -----------------------------------------------------------------
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);

            // -----------------------------------------------------------------
            // Optional: Demonstrate handling a multi‑page TIFF (comment out if not needed)
            // -----------------------------------------------------------------
            // HandleMultiPageTiff(@"C:\Invoices\multi_page_invoice.tif", ocrEngine);
        }

        // ---------------------------------------------------------------
        // Helper for multi‑page TIFFs – shows how to iterate pages
        // ---------------------------------------------------------------
        static void HandleMultiPageTiff(string path, OcrEngine engine)
        {
            using var multiPage = Image.FromFile(path);
            int pageCount = multiPage.GetFrameCount(FrameDimension.Page);

            for (int i = 0; i < pageCount; i++)
            {
                multiPage.SelectActiveFrame(FrameDimension.Page, i);
                using var page = (Image)multiPage.Clone();
                var result = engine.Recognize(page);
                Console.WriteLine($"\n--- Page {i + 1} ---");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

**Ожидаемый вывод** (усечённый для краткости):

```
=== OCR Output ===
Invoice #98765
Date: 02/28/2026
Bill To: Acme Corp.
Subtotal: $2,500.00
Tax (8%): $200.00
Total: $2,700.00
...
```

Запустите программу и убедитесь, что консоль выводит текст, который виден на счёте. Если получаете пустые строки, проверьте правильность пути к изображению и отсутствие повреждений файла.

---

## Часто задаваемые вопросы (FAQ)

**Q: Работает ли это на Linux?**  
A: Да. Aspose.OCR кроссплатформенный. Достаточно установить .NET runtime для Linux, и тот же NuGet‑пакет будет работать. Ускорение GPU требует совместимой с CUDA видеокарты и соответствующего драйвера.

**Q: Что если нет GPU?**  
A: Конструктор `OcrEngineMode.Gpu` автоматически переходит на CPU, если совместимый GPU не найден. Вы всё равно получите точные результаты; просто процесс займет немного больше времени.

**Q: Можно ли распознавать рукописные заметки?**  
A: Стандартные модели Aspose ориентированы на печатный текст. Для рукописного ввода нужен специализированный модуль или иной сервис (например, Azure Form Recognizer). Тем не менее, тот же код можно попробовать – просто ожидайте более низкие оценки уверенности.

---

## Заключение

Вы только что завершили **c# OCR tutorial**, который показывает, как *extract text from image* файлы, выполнять **ocr invoice scanning** и понимать **how to o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}