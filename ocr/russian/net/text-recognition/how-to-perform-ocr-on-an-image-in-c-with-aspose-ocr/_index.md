---
category: general
date: 2026-10-21
description: Узнайте, как выполнять OCR на JPG, извлекать текст из изображения и загружать
  изображение для OCR с использованием Aspose.OCR в C#. Полное пошаговое руководство.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from jpg
- load image for OCR
- perform OCR on image
language: ru
lastmod: 2026-10-21
og_description: Как выполнить OCR на изображении в C# с помощью Aspose.OCR. Следуйте
  этому руководству, чтобы загрузить изображение для OCR, распознать текст из JPG
  и извлечь текст из изображения.
og_image_alt: Screenshot showing how to perform OCR on a Cyrillic image in C#
og_title: Как выполнить OCR на изображении в C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to perform OCR on a JPG, extract text from image and load
    image for OCR using Aspose.OCR in C#. Complete step‑by‑step guide.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
- Image processing
- Text extraction
title: Как выполнить OCR изображения в C# с помощью Aspose.OCR
url: /ru/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить OCR на изображении в C# с Aspose.OCR

Если вам нужно **как выполнить OCR** на изображении, этот учебник покажет вам полное готовое решение. Вы узнаете, как загрузить изображение для OCR, распознать текст из JPG‑файлов и извлечь текст из изображения с помощью библиотеки Aspose.OCR.

Руководство охватывает всё — от установки пакета NuGet до работы с языковыми моделями и вывода распознанного результата. К концу вы сможете интегрировать OCR в любой проект .NET и обрабатывать кириллические или другие языковые тексты, не выходя из IDE.

## Что вам понадобится

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+)
- Visual Studio 2022 (или любой редактор C#)
- Доступ в Интернет для первого запуска (Aspose.OCR автоматически загружает языковую модель)
- Пример изображения, например `cyrillic_sample.jpg`, помещённый в папку, к которой можно обратиться из кода

## Шаг 1: Установить Aspose.OCR

Откройте менеджер пакетов NuGet и добавьте **Aspose.OCR** в ваш проект:

```bash
dotnet add package Aspose.OCR
```

Пакет содержит OCR‑движок, языковые модели и вспомогательные классы, необходимые для обработки изображений. Дополнительные DLL не требуются.

## Шаг 2: Создать OCR‑движок – как выполнить OCR

Первая реальная задача в **как выполнить OCR** — создать экземпляр движка. Этот объект управляет всей конвейерной обработкой распознавания.

```csharp
using Aspose.OCR;

// Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

`OcrEngine` лёгкий; вы можете переиспользовать один и тот же экземпляр для нескольких изображений, что повышает производительность при пакетной обработке.

## Шаг 3: Загрузить изображение для OCR

Перед распознаванием необходимо предоставить данные изображения. Шаг **load image for OCR** принимает множество форматов, но в этом примере используется JPEG‑файл.

```csharp
// Load the image you want to process
engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

`OcrImage.FromFile` читает файл в память и подготавливает его для движка. Если путь к файлу неверен, будет выброшено `ArgumentException`, поэтому убедитесь, что путь правильный.

## Шаг 4: Выбрать подходящий язык (необязательно, но рекомендуется)

Если ваше изображение содержит кириллические символы, установите язык `Cyrillic`. Необходимая модель будет загружена автоматически при первом запуске.

```csharp
// Choose the language model
engine.Language = OcrLanguage.Cyrillic;
```

Вы можете переключиться на другие языки (например, `OcrLanguage.English`), изменив это свойство. Библиотека поддерживает более 60 языков.

## Шаг 5: Распознать текст из JPG – как выполнить OCR на JPEG

Теперь вызовите метод `Recognize`. Это ядро **как выполнить OCR** и преобразует bitmap в Unicode‑текст.

```csharp
// Perform the recognition
engine.Recognize();
```

Метод блокирует выполнение до завершения процесса OCR. Для больших изображений рекомендуется выполнять его в фоновом потоке, чтобы UI оставался отзывчивым.

## Шаг 6: Извлечь текст из изображения

После распознавания движок сохраняет результат в свойстве `Text`. Это завершает шаг **extract text from image**.

```csharp
// Retrieve the extracted text
string extractedText = engine.Text;

// Output the recognized text to the console
Console.WriteLine(extractedText);
```

Вывод будет содержать точные символы, найденные на изображении, сохраняя разрывы строк и пунктуацию.

## Полный, исполняемый пример

Объединив все шаги, вы получаете одну программу, которую можно скопировать, вставить и запустить:

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image for OCR
        engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");

        // Step 3: Choose the language model (Cyrillic in this case)
        engine.Language = OcrLanguage.Cyrillic;

        // Step 4: Perform OCR on the image
        engine.Recognize();

        // Step 5: Extract text from image
        string extractedText = engine.Text;

        // Step 6: Output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

### Ожидаемый вывод

Если `cyrillic_sample.jpg` содержит фразу «Привет мир», консоль выведет:

```
=== OCR Result ===
Привет мир
```

Разные шрифты или качество изображения могут влиять на точность, но Aspose.OCR обычно достигает более 95 % распознавания на чётких отпечатках.

## Распространённые подводные камни и практические советы

- **Качество изображения имеет значение** – низкое разрешение или шумные JPEG‑файлы снижают точность. При необходимости предобработайте изображение (например, увеличьте контраст) с помощью `engine.Image.AdjustContrast()`.
- **Загрузка языковой модели** – при первом запуске модель загружается в `%USERPROFILE%\.Aspose\OCR`. Убедитесь, что процесс имеет права на запись.
- **Пакетная обработка** – переиспользуйте один экземпляр `OcrEngine` и меняйте только `engine.Image` между файлами. Это избавляет от повторной загрузки модели.
- **Потребление памяти** – большие изображения используют больше ОЗУ. Вызывайте `engine.Image.Dispose()` после каждого распознавания, если обрабатываете множество файлов в цикле.
- **Потокобезопасность** – `OcrEngine` не является потокобезопасным. Создавайте отдельный экземпляр для каждого потока при параллельной обработке.

## Заключение

Теперь вы знаете **как выполнить OCR** на JPEG, **загрузить изображение для OCR** и **извлечь текст из изображения** с помощью Aspose.OCR в C#. Полное решение демонстрирует настройку языка, распознавание текста из JPG и вывод результата, предоставляя надёжную основу для любого проекта по извлечению текста.

Далее изучайте связанные темы, такие как **perform OCR on image** пакетная обработка, интеграция OCR с ASP.NET Core API или преобразование извлечённого текста в поисковые PDF‑файлы. Экспериментируйте с разными языками и предобработкой изображений, чтобы максимизировать качество распознавания.

## Что следует изучить дальше?

Следующие учебники охватывают тесно связанные темы, опирающиеся на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающие освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как выполнить OCR в C# – Преобразовать изображение в текст с Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-text-with-aspose-oc/)
- [Как выполнить OCR в C# – Распознать текст с изображения](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/)
- [Как извлечь текст из изображения с помощью Aspose.OCR для .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}