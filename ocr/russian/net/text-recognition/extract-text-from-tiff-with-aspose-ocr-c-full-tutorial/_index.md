---
category: general
date: 2026-01-09
description: Извлечение текста из файлов TIFF с помощью Aspose OCR в C#. Узнайте,
  как получить первые 50 символов каждого результата в этом пошаговом руководстве.
draft: false
keywords:
- extract text from tiff
- get first 50 characters
- aspose ocr c# tutorial
language: ru
og_description: Извлеките текст из TIFF с помощью Aspose OCR в C#. Это руководство
  показывает, как получить первые 50 символов каждого результата OCR, шаг за шагом.
og_title: Извлечение текста из TIFF с помощью Aspose OCR – Полное руководство по C#
tags:
- Aspose OCR
- C#
- TIFF processing
title: Извлечение текста из TIFF с помощью Aspose OCR C# – Полный учебник
url: /ru/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-c-full-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из TIFF – Полный учебник по Aspose OCR C# Tutorial

Когда‑нибудь вам нужно было **извлечь текст из TIFF** изображений, но вы не знали, какую библиотеку выбрать? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда пытаются получить поисковый текст из многостраничных TIFF, особенно когда важна производительность.

В этом **aspose ocr c# tutorial** мы пройдем готовый к запуску пример, который не только извлекает полный текст, но и показывает, как **получить первые 50 символов** каждой страницы для быстрых превью. К концу вы получите автономную программу, которую можно добавить в любой проект .NET.

## Что понадобится

- .NET 6 (или любая современная версия .NET) – код компилируется как под .NET Core, так и под .NET Framework.  
- Действующая лицензия Aspose.OCR for .NET (можно начать с бесплатной пробной версии).  
- Папка, содержащая один или несколько файлов `.tif`, которые нужно обработать.  
- Visual Studio, VS Code или любой другой IDE по вашему выбору – пример написан на чистом C#, поэтому выбор редактора не важен.

> **Pro tip:** Если вы работаете на CI‑сервере, добавьте пакет NuGet Aspose.OCR (`Aspose.OCR`) в файл проекта; библиотека полностью управляемая и не имеет нативных зависимостей.

## Шаг 1: Установите пакет NuGet Aspose OCR

Для начала подключим движок OCR к проекту. Откройте терминал в папке решения и выполните:

```bash
dotnet add package Aspose.OCR
```

## Шаг 2: Инициализируйте движок OCR

Теперь создаём экземпляр `OcrEngine`. Считайте его «мозгом», который будет читать каждую страницу TIFF.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: tweak recognition settings if you know the language
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300; // higher DPI can improve accuracy
```

Почему мы создаём движок только один раз? Потому что `RecognizeImages` может принимать коллекцию путей к файлам, позволяя движку переиспользовать внутренние буферы и значительно ускоряя пакетную обработку.

## Шаг 3: Соберите все файлы TIFF одним вызовом

Вместо того чтобы вручную перебирать каталог, позволим .NET выполнить тяжёлую работу. Метод `Directory.GetFiles` возвращает `IEnumerable<string>`, который мы можем сразу передать в вызов OCR.

```csharp
            // Step 3: Collect all TIFF images from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }
```

> **What if my images are JPEG or PNG?** Просто измените шаблон поиска (`"*.jpg"` или `"*.*"`). Aspose OCR работает со всеми распространёнными растровыми форматами.

## Шаг 4: Запустите OCR на всей коллекции

Вот волшебная строка, которая обрабатывает каждый файл одним запросом. Метод возвращает словарь, где ключ — путь к файлу, а значение — объект `OcrResult`, содержащий распознанный текст.

```csharp
            // Step 4: Perform OCR on the entire collection in one call
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);
```

Почему пакетная обработка? Она уменьшает накладные расходы на повторную загрузку движка OCR, а на многопроцессорных машинах Aspose внутренне параллелит работу, обеспечивая заметный прирост скорости.

## Шаг 5: Показать превью – получить первые 50 символов

В большинстве UI‑сценариев нужен лишь фрагмент, а не весь документ. Мы извлечём первые 50 символов (или меньше, если страница короткая) и выведем их рядом с именем файла.

```csharp
            // Step 5: Display each file name with a preview of the recognized text
            foreach (var entry in ocrResults) // entry.Key = file path, entry.Value = OcrResult
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;
                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));

                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

Строка `Math.Min(50, fullText.Length)` гарантирует, что мы не превысим границы строки — небольшая защита, предотвращающая `ArgumentOutOfRangeException`, когда результат OCR короче 50 символов.

### Ожидаемый вывод в консоль

Если у вас есть два TIFF‑файла (`invoice1.tif` и `receipt2.tif`), консоль может вывести:

```
invoice1.tif → Invoice Number: 2025-07-14 Date: 07/14/...
receipt2.tif → Store: QuickMart Total: $23.45 Date: ...
```

Каждая строка заканчивается многоточием (`...`), указывающим, что превью — это лишь начало более длинного текстового блока.

## Шаг 6: Обработка граничных случаев и распространённых подводных камней

### Пустые или повреждённые файлы

Если файл не может быть прочитан, `RecognizeImages` всё равно возвращает запись с пустым свойством `Text`. Вы можете отфильтровать их:

```csharp
if (string.IsNullOrWhiteSpace(fullText))
{
    Console.WriteLine($"{fileName} → (No recognizable text)");
    continue;
}
```

### Большие партии

Обработка тысяч TIFF может потреблять много памяти. В таких случаях используйте перегрузку, принимающую `Stream` для каждого изображения, либо обрабатывайте список небольшими порциями:

```csharp
var batches = imageFiles.Chunk(100); // .NET 6+ extension
foreach (var batch in batches)
{
    var batchResults = ocrEngine.RecognizeImages(batch);
    // handle batchResults...
}
```

### Поддержка языков и шрифтов

Если ваши документы содержат нелатинские символы, задайте язык перед вызовом `RecognizeImages`:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.MultiLanguage
```

Эта небольшая настройка может значительно повысить точность.

## Шаг 7: Полный рабочий пример (готов к копированию и вставке)

Ниже полный код программы, который можно вставить в новый консольный проект (`dotnet new console`) и запустить без изменений (только замените `YOUR_DIRECTORY/Batch` на реальный путь).

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: set language or DPI for better accuracy
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300;

            // Collect all TIFF files from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }

            // Perform OCR on the entire collection
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);

            // Show a preview – get first 50 characters of each result
            foreach (var entry in ocrResults)
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;

                if (string.IsNullOrWhiteSpace(fullText))
                {
                    Console.WriteLine($"{fileName} → (No recognizable text)");
                    continue;
                }

                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));
                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

Запустите программу командой `dotnet run`. Вы должны увидеть короткое превью для каждого TIFF‑файла, подтверждающее, что вы успешно **извлекли текст из TIFF** изображений с помощью Aspose OCR.

## Часто задаваемые вопросы (FAQ)

**Q: Работает ли это с многостраничными TIFF?**  
A: Да. Aspose OCR рассматривает каждую страницу как отдельное изображение, поэтому многостраничный TIFF даёт одну объединённую строку на файл. При необходимости её можно разбить позже.

**Q: Насколько точен OCR «из коробки»?**  
A: Для чистых сканов высокого разрешения (300 DPI и выше) можно ожидать более 95 % точности для английского текста. Предобработка (выравнивание, бинаризация) может повысить её ещё больше.

**Q: Могу ли я вывести результаты в CSV‑файл?**  
A: Конечно. Замените `Console.WriteLine` на `StreamWriter` и записывайте строки `fileName,preview`. Не забудьте экранировать запятые в тексте превью.

## Следующие шаги и связанные темы

- **Persist OCR results** – Сохраните полный текст в базе данных для поисковых архивов.  
- **Combine with PDF conversion** – Используйте Aspose.PDF, чтобы внедрить извлечённый текст обратно в поисковые PDF‑файлы.  
- **Batch processing on Azure Functions** – Масштабируйте обработку OCR с помощью Azure Functions без управления серверами.  

Все эти расширения опираются на основную идею **извлечения текста из TIFF** эффективно, при этом позволяя вам **получать первые 50 символов** для быстрых UI‑превью.

---

*Счастливого кодинга! Если столкнётесь с какими‑либо проблемами, оставьте комментарий ниже — я постараюсь помочь вам настроить OCR‑конвейер.*

![Extract text from TIFF using Aspose OCR](https://example.com/images/extract-text-from-tiff.png "Extract text from TIFF using Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}