---
category: general
date: 2026-01-15
description: c# OCR‑урок, показывающий, как распознавать текст на изображении, извлекать
  текст из счета и преобразовывать изображение в текст с помощью Aspose OCR на GPU.
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- extract text from invoice
- convert image to text
- load image for ocr
language: ru
og_description: c# OCR‑урок, который учит распознавать текст на изображении, извлекать
  текст из счета и преобразовывать изображение в текст с помощью Aspose OCR на GPU.
og_title: c# OCR учебник – Быстрое распознавание текста на GPU
tags:
- OCR
- C#
- Aspose
- GPU
title: c# OCR‑урок – Распознавание текста с изображения с ускорением GPU
url: /ru/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Распознавание текста на изображении с ускорением GPU

Когда‑нибудь вам нужен был **c# ocr tutorial**, который действительно справляется с задачей без бесконечных попыток и ошибок? Возможно, вы смотрите на высоко‑разрешённый счёт и задаётесь вопросом, как **extract text from invoice** файлы за считанные секунды. Хорошая новость в том, что вам не придётся изобретать велосипед — Aspose.OCR предоставляет чистый, GPU‑ускоренный API, который делает всю тяжёлую работу за вас.

В этом руководстве мы пройдём полный, готовый к запуску пример, показывающий, как **recognize text from image** файлы, **convert image to text**, и как справиться с наиболее распространёнными подводными камнями. К концу вы получите автономную программу, способную читать любую фотографию документа, от чеков до отсканированных контрактов, и выводить чистый, индексируемый текст.

## Что вы узнаете

- Как установить и добавить ссылку на пакет Aspose.OCR NuGet.
- Как настроить OCR‑движок для работы на GPU с молниеносной производительностью.
- Правильный способ **load image for ocr** с использованием `OcrImage.FromFile`.
- Как вызвать `Recognize` с нужным языком и получить результат.
- Советы по работе с многостраничными PDF, сканами с низким контрастом и обработкой ошибок.

Предыдущий опыт работы с Aspose не требуется; достаточно рабочей среды разработки .NET (Visual Studio 2022 или VS Code) и скромного GPU (даже интегрированный GPU Intel подойдёт).

## Шаг 1 – Установка Aspose.OCR и подготовка проекта

Во‑первых, вам нужна библиотека Aspose.OCR. Самый простой способ — через NuGet.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Если вы нацелены на .NET 6 или новее, пакет автоматически загрузит нативные GPU‑бинарники для Windows, Linux и macOS. Дополнительные DLL копировать не нужно.

После добавления пакета откройте файл проекта (`*.csproj`) и проверьте ссылку:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.12.0" />
</ItemGroup>
```

Теперь у вас есть всё необходимое, чтобы начать кодировать.

## Шаг 2 – Создание OCR‑движка с поддержкой GPU (c# ocr tutorial)

Сердцем **c# ocr tutorial** является `OcrEngine`. Установив `Engine = Engine.Gpu`, мы говорим Aspose использовать видеокарту вместо процессора.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine with GPU acceleration.
            var ocrEngine = new OcrEngine
            {
                Engine = Engine.Gpu // GPU acceleration is selected; the library auto‑detects the device.
            };

            // The rest of the steps are broken out into separate methods for clarity.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            PerformOcr(ocrEngine, imagePath);
        }
    }
}
```

> **Why GPU?** GPU может обрабатывать тысячи пикселей параллельно, сокращая время OCR с секунд до долей секунды на больших изображениях с высоким DPI.

## Шаг 3 – Загрузка изображения для OCR (load image for ocr)

Корректная загрузка изображения важнее, чем может показаться. `OcrImage.FromFile` поддерживает PNG, JPEG, BMP, TIFF и даже страницы PDF. Он также считывает DPI изображения, что влияет на точность.

```csharp
static void PerformOcr(OcrEngine engine, string filePath)
{
    // Step 3: Load the image you want to recognize.
    // The FromFile method automatically detects the format.
    var image = OcrImage.FromFile(filePath);

    // Optional: Pre‑process the image for better results.
    // For example, you can increase contrast or convert to grayscale.
    image = ImagePreprocessor.AdjustContrast(image, 1.2);
    image = ImagePreprocessor.ConvertToGrayscale(image);
    
    // Continue to recognition...
    RecognizeAndDisplay(engine, image);
}
```

**Note:** Если вы работаете с PDF, можно извлечь каждую страницу как `OcrImage` и передавать их по одной.

## Шаг 4 – Распознавание текста на изображении (recognize text from image)

Теперь происходит магия. Мы просим движок распознать английский текст, но можно указать любой язык, поддерживаемый Aspose (Spanish, German, Chinese и т.д.).

```csharp
static void RecognizeAndDisplay(OcrEngine engine, OcrImage image)
{
    // Step 4: Perform OCR on the image using the desired language.
    var result = engine.Recognize(image, Language.English);

    // Step 5: Output the recognized text.
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(result.Text);
}
```

Свойство `result.Text` содержит обычную строку. Если нужен уровень уверенности для каждого слова, можно изучить `result.Regions`.

### Ожидаемый вывод

```
=== OCR RESULT ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,234.56
Thank you for your business!
```

Если изображение размыто, вы можете увидеть искажённые символы — здесь помогает предобработка из Шага 3.

## Шаг 5 – Извлечение текста из счёта – реальный пример

Предположим, у вас есть папка с отсканированными счётами, и вы хотите извлечь общую сумму. Ниже представлено быстрое расширение предыдущего кода, использующее простое регулярное выражение.

```csharp
using System.Text.RegularExpressions;

static void ExtractTotalAmount(string ocrText)
{
    // Look for a pattern like "$1,234.56"
    var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
    if (match.Success)
        Console.WriteLine($"Detected total: {match.Value}");
    else
        Console.WriteLine("Total amount not found.");
}
```

Вы бы вызвали `ExtractTotalAmount(result.Text);` сразу после вывода результата OCR. Это демонстрирует, насколько просто **extract text from invoice** файлы, когда у вас уже есть исходная строка.

## Шаг 6 – Конвертация изображений в текст пакетно (convert image to text)

Обработка одного файла подходит для демонстрации, но в продакшн‑коде часто нужно обрабатывать десятки или сотни изображений. Вот компактный цикл, обрабатывающий всю директорию:

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    foreach (var file in Directory.EnumerateFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly)
                                 .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
    {
        Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
        var img = OcrImage.FromFile(file);
        var res = engine.Recognize(img, Language.English);
        Console.WriteLine(res.Text);
        ExtractTotalAmount(res.Text); // optional invoice extraction
    }
}
```

Вызов `ProcessFolder(ocrEngine, @"C:\Invoices")` **convert image to text** для каждого поддерживаемого файла в папке, используя GPU для ускорения.

## Пограничные случаи и распространённые подводные камни

| Ситуация | Почему происходит | Быстрое решение |
|-----------|-------------------|-----------------|
| **Скан с низким контрастом** | OCR не может различить передний план и фон. | Увеличьте контраст (`ImagePreprocessor.AdjustContrast`) или примените адаптивное пороговое преобразование. |
| **Многостраничный PDF** | `OcrImage.FromFile` читает только первую страницу. | Используйте `PdfDocument` для извлечения каждой страницы как `OcrImage` и перебирайте их. |
| **Неподдерживаемый язык** | Язык по умолчанию установлен как English. | Передайте `Language.Spanish` или любое поддерживаемое значение enum. |
| **GPU не обнаружен** | Отсутствуют нативные бинарники или драйвер устарел. | Убедитесь, что драйвер GPU обновлён; переустановите пакет NuGet с флагом `-runtime`. |
| **Недостаток памяти при больших изображениях** | Память GPU ограничена. | Уменьшите размер изображения (`image = ImagePreprocessor.Resize(image, 2000, 0)`). |

## Полный рабочий пример

Ниже представлен полный код программы, который вы можете скопировать и вставить в новое консольное приложение. Он включает все вспомогательные методы, обсуждавшиеся выше.

```csharp
using System;
using System.IO;
using System.Linq;
using System.Text.RegularExpressions;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize GPU‑accelerated OCR engine.
            var ocrEngine = new OcrEngine { Engine = Engine.Gpu };

            // 2️⃣ Define the path to a single image or a folder.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            // string folderPath = @"C:\Invoices";

            // Uncomment one of the following lines:
            PerformOcr(ocrEngine, imagePath);
            // ProcessFolder(ocrEngine, folderPath);
        }

        // -------------------------------------------------
        // Load image, preprocess, recognize, and display.
        // -------------------------------------------------
        static void PerformOcr(OcrEngine engine, string filePath)
        {
            var image = OcrImage.FromFile(filePath);
            image = ImagePreprocessor.AdjustContrast(image, 1.2);
            image = ImagePreprocessor.ConvertToGrayscale(image);

            var result = engine.Recognize(image, Language.English);
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);

            ExtractTotalAmount(result.Text);
        }

        // -------------------------------------------------
        // Bulk processing of a folder.
        // -------------------------------------------------
        static void ProcessFolder(OcrEngine engine, string folderPath)
        {
            foreach (var file in Directory.EnumerateFiles(folderPath, "*.*")
                                          .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
            {
                Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
                var img = OcrImage.FromFile(file);
                var res = engine.Recognize(img, Language.English);
                Console.WriteLine(res.Text);
                ExtractTotalAmount(res.Text);
            }
        }

        // -------------------------------------------------
        // Simple regex to pull the total amount from an invoice.
        // -------------------------------------------------
        static void ExtractTotalAmount(string ocrText)
        {
            var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
            if (match.Success)
                Console.WriteLine($"Detected total: {match.Value}");
            else
                Console.WriteLine("Total amount not found.");
        }
    }
}
```

**Run it** (` 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}