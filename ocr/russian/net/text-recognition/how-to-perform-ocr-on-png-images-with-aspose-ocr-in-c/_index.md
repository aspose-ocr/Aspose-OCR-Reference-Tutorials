---
category: general
date: 2026-11-26
description: Узнайте, как выполнять OCR для PNG‑файлов, преобразовывать PNG в текст
  и извлекать кириллический текст с помощью Aspose.OCR — пошаговое руководство для
  разработчиков.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: ru
lastmod: 2026-11-26
og_description: Как выполнять OCR на PNG‑файлах и извлекать кириллический текст с
  помощью Aspose.OCR в C#. Следуйте этому полному руководству, чтобы преобразовать
  PNG в текст.
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Как выполнять OCR на PNG‑изображениях с Aspose.OCR – руководство по C#
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: Как выполнить OCR для PNG‑изображений с помощью Aspose.OCR в C#
url: /ru/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR на PNG‑изображениях с Aspose.OCR в C#

Если вам нужно **how to perform OCR** на PNG‑файле, это руководство покажет точные шаги по конвертации PNG в текст с помощью Aspose.OCR. Независимо от того, извлекаете ли вы кириллический текст из отсканированных документов или просто распознаёте текст на скриншотах PNG, решение работает сразу из коробки и требует всего несколько строк кода на C#.

В этом руководстве вы узнаете, как:

* **load image for OCR** из локальной папки,
* настроить движок для **extract Cyrillic text**,
* **recognize text from PNG** и получить чистую строку,
* обрабатывать распространённые подводные камни, такие как отсутствие языковых модулей и большие изображения.

Никакого предварительного опыта работы с Aspose.OCR не требуется — достаточно среды разработки .NET и PNG‑изображения, которое вы хотите обработать.

## Требования

Перед началом убедитесь, что у вас есть:

* .NET 6.0 (или новее) установлен.
* Лицензированная или пробная копия **Aspose.OCR for .NET**. Вы можете получить бесплатную пробную версию на сайте Aspose.
* Visual Studio 2022 (или любая IDE, поддерживающая .NET).
* PNG‑файл, содержащий текст, который вы хотите извлечь (в примере используется `sample_image.png`).

## Шаг 1: Установить пакет Aspose.OCR NuGet

Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

Пакет включает ядро OCR‑движка и все языковые модули. Когда вы запрашиваете язык, которого нет локально, Aspose.OCR автоматически загружает необходимый модуль.

## Шаг 2: Создать экземпляр OCR‑движка (how to perform OCR)

Первый практический шаг в любом OCR‑рабочем процессе — создать экземпляр движка. Этот объект управляет всеми последующими операциями, такими как загрузка изображения и выполнение распознавания.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**Why this matters:** Класс `OcrEngine` инкапсулирует OCR‑конвейер. Создание единственного экземпляра и его повторное использование для нескольких изображений уменьшает нагрузку на память и повышает производительность.

## Шаг 3: Загрузить изображение для OCR – указать исходный PNG‑файл

Загрузка изображения — это момент, когда вы **load image for OCR**. Aspose.OCR принимает несколько типов входных данных; самым простым является `ImageStream.FromFile`.

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **Pro tip:** Используйте абсолютный путь или `Path.Combine`, чтобы избежать ошибок выполнения в разных средах.

### Обработка больших изображений

Если PNG больше 2 МБ, рассмотрите возможность уменьшения его размеров перед распознаванием, чтобы ускорить обработку:

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## Шаг 4: Настроить язык – extract Cyrillic text

По умолчанию Aspose.OCR предполагает английский язык. Чтобы **extract Cyrillic text**, установите свойство `Language` в `Language.Cyrillic`. Требуемый модуль будет загружен автоматически при первом запуске кода.

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

Если необходимо распознавать несколько языков (например, английский и кириллический), их можно комбинировать:

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### Пограничный случай: Отсутствующий языковой модуль

Если загрузка не удалась (например, в офлайн‑среде), движок бросит `OcrException`. Перехватите его, чтобы обеспечить плавный откат:

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## Шаг 5: Выполнить операцию распознавания (recognize text from PNG)

Теперь, когда изображение и язык заданы, вы можете **recognize text from PNG**. Метод `Recognize` запускает OCR‑конвейер синхронно.

```csharp
// Run OCR
ocrEngine.Recognize();
```

**Why it works:** Внутри Aspose.OCR выполняет предобработку (бинаризацию, удаление шума) перед передачей изображения в нейронный распознаватель, настроенный под выбранный язык.

## Шаг 6: Получить и отобразить распознанный текст (convert PNG to text)

После распознавания извлечённая строка доступна через свойство `Text`. Это финальный шаг в **convert PNG to text**.

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### Ожидаемый вывод

Если `sample_image.png` содержит кириллическую фразу «Привет мир», консоль выведет:

```
=== OCR Result ===
Привет мир
```

Вывод может включать переносы строк и пунктуацию точно так же, как они выглядят на изображении. При необходимости вы можете постобработать строку с помощью `String.Trim()`, `Regex` или других утилит очистки текста.

## Шаг 7: Необязательно – Сохранить результат в файл

Сохранение результата OCR позволяет дальнейшую обработку (например, индексацию, перевод). Вот быстрый способ записать текст в файл UTF‑8:

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## Распространённые подводные камни и как их избежать

| Проблема | Симптом | Решение |
|----------|----------|--------|
| **Missing language module** | `OcrException` on `Language = Language.Cyrillic` | Убедитесь, что есть подключение к интернету при первом запуске, либо предварительно загрузите модули через офлайн‑пакет Aspose. |
| **Blurry or low‑contrast image** | Плохая точность, много символов «?». | Предобработайте изображение: увеличьте контраст, примените резкость или преобразуйте в градации серого перед передачей в движок. |
| **Very large PNG** | Длительное время обработки, возможное `OutOfMemoryException` | Уменьшите размер, как показано в Шаге 3, либо разбейте многостраничное изображение на отдельные плитки. |
| **Non‑UTF‑8 characters** | Искажённый вывод | Убедитесь, что консоль или запись в файл использует кодировку UTF‑8 (`Encoding.UTF8`). |

## Полный, исполняемый пример

Ниже приведена полная программа, включающая все шаги выше. Скопируйте её в новый консольный проект и запустите после корректировки путей к файлам.

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### Как это работает

1. **Engine creation** – подготавливает OCR‑конвейер.  
2. **Image loading** – поддерживает как оригинальные PNG, так и уменьшенные версии для производительности.  
3. **Language selection** – демонстрирует **extract Cyrillic text**, обрабатывая отсутствие модулей.  
4. **Recognition** – основной вызов **recognize text from PNG**.  
5. **Result handling** – показывает **convert PNG to text** и записывает результат в файл.

Запустите программу командой `dotnet run`. Если всё настроено правильно, вы увидите распознанный текст, выведенный в консоль, и сохранённый в `ocr_output.txt`.

## Заключение

В этом руководстве вы узнали **how to perform OCR** на PNG‑файлах с помощью Aspose.OCR для .NET, охватив всё от **load image for OCR** до **extract Cyrillic text** и **convert PNG to text**. Полный, исполняемый пример демонстрирует стандартный рабочий процесс, типичные пограничные случаи и практические советы, которые делают ваш OCR‑конвейер надёжным.

**Следующие шаги**

* Исследуйте **recognize text from PNG** с дополнительными языками (Arabic, Chinese), комбинируя флаги `Language`.  
* Интегрируйте результат OCR с Azure Cognitive Search для создания поисковых архивов документов.  
* Поэкспериментируйте с настройками `OcrEngine` в Aspose.OCR, такими как `Resolution

## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Download Aspose.OCR Model and Extract Text from PNG in C#](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [How to Perform OCR in C# – Recognize Cyrillic Text with Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [How to Batch OCR in C# – Fast Way to Extract Text PNG Files](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}