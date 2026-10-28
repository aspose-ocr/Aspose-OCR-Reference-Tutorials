---
category: general
date: 2026-10-27
description: Пример OCR на C# для кириллицы показывает, как использовать библиотеку
  OCR на C# для извлечения кириллического текста из изображений с правильными настройками
  OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- c# example ocr cyrillic
- c# ocr library
- cyrillic language module
- image text extraction
- ocr settings
- recognition language
language: ru
lastmod: 2026-10-27
og_description: пример C# OCR кириллица демонстрирует, как настроить библиотеку OCR
  на C#, загрузить изображение и вывести распознанный кириллический текст с полным
  кодом.
og_image_alt: Diagram of c# example ocr cyrillic workflow showing image loading, OCR
  settings, and text output
og_title: пример OCR на C# для кириллицы – пошаговое руководство по извлечению кириллического
  текста
schemas:
- author: Aspose
  dateModified: '2026-10-27'
  description: c# example ocr cyrillic guide shows how to use a C# OCR library to
    extract Cyrillic text from images with proper OCR settings.
  headline: c# example ocr cyrillic – perform OCR on Cyrillic text
  type: TechArticle
tags:
- C#
- OCR
- Cyrillic
- Image Processing
- Example
title: c# пример OCR кириллицы – выполнить OCR для кириллического текста
url: /ru/net/ocr-settings/c-example-ocr-cyrillic-perform-ocr-on-cyrillic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# example ocr cyrillic – выполнение OCR на кириллическом тексте

Если вам нужен **c# example ocr cyrillic**, этот учебник проведёт вас через весь процесс. Вы узнаете, как настроить C# OCR‑библиотеку, загрузить изображение с кириллическими символами и получить обычный текст из движка распознавания.

OCR (optical character recognition) может работать с множеством алфавитов, но для кириллицы требуется отдельный языковой модуль. В этом руководстве рассматривается всё необходимое — от установки библиотеки до проверки результата — чтобы вы могли интегрировать извлечение кириллического текста в любой .NET‑проект.

## Prerequisites

Перед началом убедитесь, что у вас есть:

* .NET 6.0 или более новая версия  
* C# OCR‑библиотека, поддерживающая языковые модули (например, **IronOCR**, **Tesseract .NET** или коммерческий SDK)  
* Файл изображения, содержащий кириллический текст (в примере используется `cyrillic_sample.jpg`)  

Отдельный бинарный OCR‑движок не требуется; библиотека автоматически загрузит **cyrillic language module**, когда вы запросите его.

## Step 1: Load the image that contains Cyrillic text

Первый шаг — прочитать исходное изображение в память. Метод `Image.FromFile` создаёт объект `System.Drawing.Image`, который может обработать OCR‑движок.

```csharp
// Load the image file that holds Cyrillic characters
var sourceImage = Image.FromFile("YOUR_DIRECTORY/cyrillic_sample.jpg");

// Verify that the image was loaded successfully
if (sourceImage == null)
{
    throw new InvalidOperationException("Failed to load the image file.");
}
```

*Почему это важно*: Загрузка изображения как `System.Drawing.Image` даёт OCR‑движку прямой доступ к пиксельным данным, что повышает точность распознавания сложных скриптов, таких как кириллица.

## Step 2: Configure OCR settings to request the Cyrillic language module

OCR‑движки предоставляют объект настроек, где указывается целевой язык. Установка `Language` в `RecognitionLanguage.Cyrillic` инициирует загрузку **cyrillic language module**, если он ещё не присутствует.

```csharp
// Create OCR settings and request the Cyrillic language pack
var ocrSettings = new RecognitionSettings
{
    Language = RecognitionLanguage.Cyrillic   // activates the Cyrillic module
};

// Optional: adjust additional parameters for better accuracy
ocrSettings.Dpi = 300;               // higher DPI improves character detail
ocrSettings.EnableNoiseReduction = true;
```

*Почему это важно*: Без правильного языкового модуля движок будет рассматривать кириллические символы как неизвестные глифы, что приведёт к искажённому выводу. Перечисление `RecognitionLanguage` гарантирует использование корректного набора символов.

## Step 3: Run the OCR engine on the image with the specified settings

Теперь вызываем OCR‑движок, передавая как изображение, так и настроенные параметры. Метод `Recognize` возвращает объект результата, содержащий извлечённый текст.

```csharp
// Perform OCR using the image and the prepared settings
var ocrResult = OcrEngine.Recognize(sourceImage, ocrSettings);

// Verify that the OCR process succeeded
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    throw new InvalidOperationException("OCR did not return any text.");
}
```

*Почему это важно*: Вызов `OcrEngine.Recognize` объединяет **image text extraction** с языковой моделью, создавая Unicode‑текст, сохраняющий кириллические символы.

## Step 4: Output the recognized plain text to the console

Наконец, выводим извлечённый текст. В реальном приложении вы, вероятно, сохраните результат в базе данных или передадите его в другой сервис, но `Console.WriteLine` демонстрирует основной вывод.

```csharp
// Write the recognized Cyrillic text to the console
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

**Ожидаемый вывод** (пример):

```
Recognized text:
Пример текста на кириллице
```

Если вывод совпадает с содержимым оригинального изображения, ваш **c# example ocr cyrillic** работает корректно.

## Full, runnable example

Ниже представлена полная программа, которую можно скопировать, вставить и запустить после добавления ссылки на соответствующую OCR‑библиотеку.

```csharp
using System;
using System.Drawing;
using YourOcrLibrary;          // Replace with the actual namespace of your OCR SDK

class Program
{
    static void Main()
    {
        // Step 1: Load the image that contains Cyrillic text
        var sourceImage = Image.FromFile("YOUR_DIRECTORY/cyrillic_sample.jpg");
        if (sourceImage == null)
        {
            Console.Error.WriteLine("Unable to load image.");
            return;
        }

        // Step 2: Configure OCR settings to request the Cyrillic language module
        var ocrSettings = new RecognitionSettings
        {
            Language = RecognitionLanguage.Cyrillic,
            Dpi = 300,
            EnableNoiseReduction = true
        };

        // Step 3: Run the OCR engine on the image with the specified settings
        var ocrResult = OcrEngine.Recognize(sourceImage, ocrSettings);
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.Error.WriteLine("OCR failed to extract text.");
            return;
        }

        // Step 4: Output the recognized plain text to the console
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Pro tip**: При обработке пакета изображений переиспользуйте один экземпляр `OcrEngine`, чтобы снизить накладные расходы. Также экспериментируйте со значениями `Dpi` и `EnableNoiseReduction` для изображений с низким контрастом или фоновыми узорами.

## Common questions and edge cases

| Question | Answer |
|----------|--------|
| *What if the Cyrillic module does not download automatically?* | Убедитесь, что приложение имеет доступ к интернету и лицензия OCR‑библиотеки позволяет динамическую загрузку модулей. При необходимости можно скачать модуль вручную с сайта поставщика и указать SDK локальную папку. |
| *Can I recognize mixed‑language documents (e.g., Latin + Cyrillic)?* | Установите `Language = RecognitionLanguage.Multilingual` или передайте массив языков, если SDK это поддерживает. Движок будет переключаться между наборами символов по мере необходимости. |
| *How do I handle large images without exhausting memory?* | Перед передачей в `Recognize` уменьшите изображение до максимального размера 2000 px по самой длинной стороне. Для создания экономичной копии используйте `Image.GetThumbnailImage`. |
| *Is the output always Unicode?* | Современные OCR‑библиотеки возвращают строки в UTF‑8, сохраняющие кириллические символы. Если нужен иной набор кодировок, преобразуйте строку с помощью `Encoding.GetEncoding("windows-1251")`. |

## Conclusion

Теперь у вас есть **c# example ocr cyrillic**, который загружает изображение, настраивает **cyrillic language module**, запускает OCR‑движок и выводит распознанный текст. Этот сквозной процесс демонстрирует основные шаги **image text extraction** с использованием C# OCR‑библиотеки.

Дальше вы можете:

* Интегрировать код в веб‑API, принимающее загруженные изображения.  
* Расширить пример для обработки PDF, предварительно преобразовав каждую страницу в изображение.  
* Исследовать дополнительные **ocr settings**, такие как пользовательские словари или пороги уверенности.  

Экспериментируйте с различным качеством изображений и языковыми пакетами, чтобы точно настроить точность под ваш конкретный сценарий. Приятного кодинга!

## What Should You Learn Next?

Следующие учебники охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Perform OCR in C# – Recognize Cyrillic Text with Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [read text from png – extract Cyrillic text with Aspose OCR](/ocr/english/net/ocr-configuration/read-text-from-png-extract-cyrillic-text-with-aspose-ocr/)
- [Extract Text from Image in C# – Complete Aspose OCR Example](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-example/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}