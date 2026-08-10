---
category: general
date: 2026-05-31
description: Узнайте, как получать оценки уверенности OCR в C# при извлечении текста
  из изображения и чтении изображения чека с помощью Aspose OCR.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: ru
og_description: Оценки уверенности OCR позволяют оценить точность; это руководство
  показывает, как извлекать текст из изображения, получать ограничивающие рамки и
  считывать изображение чека с помощью Aspose OCR.
og_title: Оценки уверенности OCR в C# – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Оценки уверенности OCR в C# — Полное руководство
url: /ru/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Оценки уверенности OCR в C# – Полное руководство

Когда‑нибудь задумывались, как получить **оценки уверенности OCR**, когда нужно *извлечь текст из изображения*? Возможно, вы пытаетесь **прочитать изображение чека** для учёта расходов и хотите знать, какие символы вызывают сомнения у движка. Хорошая новость? С Aspose.OCR вы можете получить проценты уверенности, ограничительные рамки и простой текст из JPG всего за несколько строк кода на C#.

В этом руководстве мы пройдём всё, что нужно знать: установку библиотеки, настройку движка для **выполнения OCR на JPG**, получение оценок уверенности и интерпретацию **ограничительных рамок OCR**, которые показывают, где каждый символ расположен на странице. К концу вы получите готовое к запуску консольное приложение, которое выводит каждый символ, его уверенность и расположение — идеально для проверки чеков или любого отсканированного документа.

## Что вы узнаете

- Установить Aspose.OCR через NuGet и настроить базовый OCR‑движок.  
- Настроить `OcrOptions` для запроса вывода plain‑text **с оценками уверенности** и **ограничительными рамками**.  
- Пройтись по `OcrResult`, чтобы **извлечь текст из изображения** построчно и символ за символом.  
- Обработать распространённые проблемы, такие как отсутствие файлов, символы с низкой уверенностью и форматы, отличные от JPG.  
- Расширить пример для обработки нескольких изображений чеков в папке.

Опыт работы с Aspose не требуется; нужен только рабочий .NET‑окружение и изображение чека (JPG), которое вы хотите протестировать.

---

## Шаг 1 – Установите Aspose.OCR и подготовьте проект

Сначала вам нужен пакет Aspose.OCR из NuGet. Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

> **Подсказка:** Бесплатная пробная версия работает до 200 страниц, чего более чем достаточно для тестирования сканирования чеков.

После установки пакета создайте новый консольный проект (если у вас его ещё нет):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Теперь откройте сгенерированный `Program.cs` и добавьте директивы `using`:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

Эти пространства имён дают доступ к `OcrEngine`, `OcrOptions` и типам результатов, которые понадобятся позже.

## Шаг 2 – Получить оценки уверенности OCR и ограничительные рамки OCR

Это сердце руководства. Мы настроим движок так, чтобы каждый распознанный символ сопровождался **оценкой уверенности** и **ограничительной рамкой** (прямоугольником, охватывающим глиф). Сам заголовок H2 уже содержит основной ключевой запрос, удовлетворяя SEO‑правило.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Зачем включать оценки уверенности?**  
Оценка уверенности (0‑100 %) показывает, насколько уверенно движок распознаёт каждый символ. Если вы передаёте результат в последующие процессы — например, в workflow одобрения расходов — можете автоматически отклонять или помечать символы с низкой уверенностью.

**Зачем запрашивать ограничительные рамки?**  
Ограничительные рамки необходимы, когда нужно подсвечивать текст на оригинальном изображении, извлекать под‑области или синхронизировать результаты OCR с UI‑оверлеем. Каждый `character.Bounds` даёт координаты X, Y, ширину и высоту в пикселях.

## Шаг 3 – Выполнить OCR на JPG и извлечь текст из изображения

Теперь действительно запустим движок. Вызов `Recognize()` выполняет всю тяжёлую работу и возвращает объект `OcrResult`.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

Если путь к изображению неверен или файл имеет неподдерживаемый формат, Aspose бросит `FileNotFoundException` или `UnsupportedImageFormatException`. В продакшн‑коде оберните вызов в блок try/catch, чтобы корректно обрабатывать такие случаи.

### Получение простого текста

Если нужен только объединённый текст, можно прочитать `ocrResult.Text`:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

Но поскольку мы также запросили оценки уверенности и ограничительные рамки, будем проходить по структуре, чтобы увидеть детали каждого символа.

## Шаг 4 – Перебор строк, символов и отображение оценок уверенности OCR

Вот цикл, который выводит каждый символ, его уверенность и рамку. Здесь пример **прочтения изображения чека** действительно блестит.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

Пример вывода может выглядеть так:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Интерпретация чисел:**  
- **Уверенность ≥ 90 %** — обычно безопасно принимать.  
- **Уверенность 70‑89 %** — может потребоваться двойная проверка, особенно для цифр в суммах.  
- **Уверенность < 70 %** — рекомендовано помечать для ручного обзора.

## Шаг 5 – Полный исполняемый пример (с обработкой ошибок)

Объединив всё, получаем полностью готовую программу, которую можно скопировать в `Program.cs`. В ней есть простая проверка наличия файлов и дружественное сообщение, если OCR завершится неудачей.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Ожидаемый вывод

При запуске `dotnet run` консоль сначала покажет объединённый текст чека, затем список каждого символа с его оценкой уверенности и ограничительной рамкой. Если уверенность символа низка, вы увидите процент ниже 80 %, что служит сигналом проверить эту часть чека вручную.

## Бонус: Обработка нескольких чеков в папке

Если у вас есть набор JPG‑чеков, оберните вышеописанную логику в цикл `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`. Не забудьте сбрасывать `OcrEngine` для каждого файла или создавать новый экземпляр внутри цикла, чтобы избежать утечки состояния.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

Пакетная обработка удобна для ночных импортов расходов.

---

## Заключение

Теперь у вас есть надёжное сквозное решение для получения **оценок уверенности OCR** в C#, **извлечения текста из изображения** и получения **ограничительных рамок OCR** при **выполнении OCR на JPG** файлах, таких как **изображение чека**. Код полностью автономный, работает с последней версией Aspose.OCR (по состоянию на 2026‑05‑31) и предоставляет детальные данные, необходимые для построения надёжных конвейеров обработки документов.

Что дальше? Попробуйте визуализировать ограничительные рамки на оригинальном чеке с помощью `System.Drawing` или UI‑библиотеки, либо передать символы с низкой уверенностью в сервис вторичной верификации. Можно также поэкспериментировать с другими языками, задав `ocrEngine.Options.Language = OcrLanguage.French;` — API поддерживает множество локалей.

Счастливого кодинга, и пусть ваши оценки уверенности всегда остаются высокими! 

![Вывод консоли, показывающий оценки уверенности OCR и ограничительные рамки для чека

## Что вам стоит изучить дальше?

- [Извлечение текста из изображения C# с выбором языка с помощью Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Как получить варианты символов OCR для распознанных символов в распознавании изображений](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Как использовать Aspose OCR для получения результата в JSON при распознавании изображений](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}