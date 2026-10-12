---
category: general
date: 2026-10-11
description: Узнайте, как выполнять OCR изображения в C# с помощью Aspose.OCR, включая
  установку System.Drawing.Common и извлечение текста из JPG‑файлов.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: ru
lastmod: 2026-10-11
og_description: Выполните OCR изображения в C# с использованием Aspose.OCR. Это руководство
  показывает, как установить System.Drawing.Common, загрузить изображение для OCR
  и извлечь текст из JPG.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: Распознавание текста на изображении в C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Как выполнить OCR изображения в C# с помощью Aspose.OCR
url: /ru/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить OCR изображения в C# с использованием Aspose.OCR

Если вам нужно **perform OCR on image** файлы в .NET приложении, это руководство покажет полное решение. С помощью Aspose.OCR вы можете быстро **recognize text from picture** файлы, такие как JPG, и отобразить результат в окне консоли.

Вы узнаете, как:

* **install System.Drawing.Common package** – библиотека, предоставляющая класс `Image`,
* **load image for OCR** – чтение JPEG или PNG в память,
* настроить языковую модель,
* **perform OCR on image** и, наконец,
* **extract text from JPG** и вывести его.

Шаги написаны для .NET 6+, но они также работают с .NET Framework 4.6.1 и более поздними версиями.

---

## Необходимые условия

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | Обеспечивает среду выполнения для консольного приложения на C#. |
| Visual Studio 2022 (or any IDE) | Облегчает добавление пакетов NuGet и запуск программы. |
| Internet connection (first run only) | Aspose.OCR автоматически загружает языковой модуль. |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | Используется для демонстрации **extract text from JPG**. |

---

## Шаг 1: Установить пакет System.Drawing.Common

Пакет NuGet `System.Drawing.Common` предоставляет класс `Image`, который вы будете **load image for OCR**. Откройте консоль диспетчера пакетов и выполните:

```powershell
Install-Package System.Drawing.Common
```

> **Совет:** Target `net6.0-windows` or add `<UseWindowsForms>true</UseWindowsForms>` to the project file if you encounter platform‑specific warnings on Linux/macOS.

---

## Шаг 2: Добавить пакет Aspose.OCR NuGet

Aspose.OCR содержит OCR‑движок и языковые модели. Установите его с помощью:

```powershell
Install-Package Aspose.OCR
```

Пакет лёгкий; необходимые языковые данные (например, кириллица) загружаются при первом задании `OcrEngine.Language`.

---

## Шаг 3: Как загрузить изображение для OCR

Загрузка изображения — первый конкретный шаг перед тем, как вы сможете **perform OCR on image**. Метод `Image.FromFile` читает любой формат, поддерживаемый GDI+, включая JPG, PNG, BMP и TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*Если файл не существует, будет выброшено `FileNotFoundException` — оберните вызов в блок try/catch для продакшн‑кода.*

---

## Шаг 4: Настроить движок и **perform OCR on image**

Создайте экземпляр `OcrEngine`, выберите языковую модель, назначьте загруженное изображение и вызовите `Recognize()`.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

Метод `Recognize()` возвращает объект `OcrResult`, содержащий извлечённый текст, оценки уверенности и ограничивающие рамки. Языковой модуль загружается автоматически при первом использовании, поэтому дополнительные файлы не требуются.

---

## Шаг 5: **Extract text from JPG** и вывести его

Теперь вы можете **recognize text from picture** и вывести результат. Свойство `Text` объекта `OcrResult` содержит обычную строку.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Ожидаемый вывод консоли

```
Recognized text:
Пример текста на кириллице
```

Если исходное изображение содержит английский текст, вывод будет английским предложением, которое вы разместили на картинке.

---

## Пограничные случаи и рекомендации по лучшим практикам

| Situation | Recommendation |
|-----------|----------------|
| **Large images ( > 5 MB )** | Измените размер изображения до ≤ 2000 px по самой длинной стороне перед OCR, чтобы уменьшить использование памяти и повысить скорость. |
| **Multiple languages in one picture** | Вызовите `ocrEngine.AddLanguage(OcrLanguage.English)` в дополнение к кириллице, затем установите `ocrEngine.Language = OcrLanguage.Multilingual`. |
| **Low‑contrast scans** | Увеличьте контраст с помощью `System.Drawing.Graphics` перед передачей битмапа в движок. |
| **Running on Linux/macOS** | Убедитесь, что нативная зависимость `libgdiplus` установлена (`sudo apt-get install -y libgdiplus`). |
| **Repeated OCR calls** | Повторно используйте тот же экземпляр `OcrEngine` и заменяйте только `ocrEngine.Image`, чтобы избежать повторной загрузки модуля. |

---

## Полная, исполняемая программа

Ниже представлено полное консольное приложение, включающее все предыдущие шаги. Скопируйте код в новый проект C# консоли, замените путь к изображению и запустите его.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Running the program** выводит распознанную строку в консоль, подтверждая, что вы успешно **performed OCR on image** и **extracted text from JPG**.

---

## Заключение

Теперь вы знаете, как **perform OCR on image** файлы в C# с использованием Aspose.OCR, начиная с установки требуемого **System.Drawing.Common package**, до **loading image for OCR**, выбора подходящего языка и, наконец, **extracting text from JPG**. Этот сквозной пример предоставляет надёжную основу для создания более продвинутых конвейеров обработки документов, таких как пакетная обработка папок с изображениями или интеграция OCR в веб‑API.

### Что дальше?

* Исследуйте **recognize text from picture** в PDF, сначала преобразовав каждую страницу в изображение.
* Экспериментируйте со свойствами `OcrEngine` `Resolution`, `Threshold` и `MaxProcessingTime`, чтобы точно настроить точность на шумных сканах.
* Скомбинируйте вывод OCR с библиотекой обработки естественного языка, чтобы автоматически классифицировать извлечённый контент.

Не стесняйтесь адаптировать код для других форматов изображений, добавить обработку ошибок или интегрировать его в более крупные приложения. Приятного кодинга!

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, основанные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Extract Text from Image in C# – Complete Aspose OCR Guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}