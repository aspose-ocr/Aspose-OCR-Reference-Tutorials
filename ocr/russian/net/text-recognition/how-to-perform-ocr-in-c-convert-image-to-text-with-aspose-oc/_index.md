---
category: general
date: 2026-05-21
description: Как выполнить OCR в C# с помощью Aspose OCR — научитесь преобразовывать
  изображение в текст, считывать текст из JPG и загружать изображение для OCR быстро
  и надёжно.
draft: false
keywords:
- how to perform OCR
- convert image to text
- read text from jpg
- how to extract text from image
- load image for OCR
language: ru
og_description: Как выполнить OCR в C# с помощью Aspose OCR. Это руководство показывает,
  как преобразовать изображение в текст, прочитать текст из JPG и загрузить изображение
  для OCR пошагово.
og_title: Как выполнить OCR в C# – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: How to perform OCR in C# using Aspose OCR – learn to convert image
    to text, read text from jpg, and load image for OCR quickly and reliably.
  headline: How to Perform OCR in C# – Convert Image to Text with Aspose OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Как выполнить OCR в C# – преобразовать изображение в текст с помощью Aspose
  OCR
url: /ru/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-text-with-aspose-oc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR в C# – Полное руководство

Когда‑нибудь задавались вопросом **как выполнять OCR** в приложении C# без борьбы с низкоуровневой обработкой изображений? Вы не одиноки. Многие разработчики нуждаются в надёжном способе **преобразовать изображение в текст**, особенно при работе со сканированными документами или фотографиями чеков. В этом руководстве мы пройдём по точным шагам загрузки изображения для OCR, запуска движка распознавания и, наконец, чтения извлечённого текста — всё с помощью Aspose OCR.

Мы также рассмотрим, как **читать текст из jpg** файлов, обсудим нюансы **как извлечь текст из изображения**, и предоставим вам быструю шпаргалку для сценариев **загрузки изображения для OCR**. К концу вы получите готовый к запуску пример, который можно добавить в любой проект .NET.

## Требования

- .NET 6.0 или новее (код работает как на .NET Core, так и на .NET Framework)
- Visual Studio 2022 или любая предпочитаемая IDE
- Файл лицензии Aspose OCR for .NET (необязательно, но рекомендуется для полного режима функций)
- Пример изображения (например, `sample.jpg`), размещённый в известной папке
- Доступ к Интернету для загрузки пакета NuGet `Aspose.OCR`

Если что‑то из этого вам незнакомо, не паникуйте — каждое требование будет рассмотрено по ходу.

## Шаг 1 – Установить Aspose OCR через NuGet

Первое, что вам нужно, — библиотека Aspose OCR. Откройте консоль диспетчера пакетов и выполните:

```powershell
Install-Package Aspose.OCR
```

Или, если вы используете CLI:

```bash
dotnet add package Aspose.OCR
```

> **Совет:** Добавление пакета восстанавливает все зависимости, так что вам не придётся вручную искать дополнительные DLL.

## Шаг 2 – Загрузить изображение для OCR

Теперь, когда библиотека подключена, нам нужно **загрузить изображение для OCR**. Этот шаг критичен, потому что движок ожидает объект `ImageStream`, а не простой путь к файлу.

```csharp
using Aspose.OCR;

// Assume the image lives in the same folder as the executable
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");

// Create an ImageStream from the file
ImageStream imgStream = ImageStream.FromFile(imagePath);
```

Обратите внимание, как мы формируем полный путь с помощью `AppDomain.CurrentDomain.BaseDirectory`. Это делает код надёжным независимо от того, запускаете ли вы его из Visual Studio, консоли или опубликованного exe. Кроме того, класс `ImageStream` поддерживает множество форматов, так что вы можете легко **читать текст из jpg**, **png** или **bmp** файлов.

## Шаг 3 – Как выполнить OCR на загруженном изображении

Это сердце руководства — **как выполнить OCR** с использованием движка Aspose. Мы также установим язык на английский; при необходимости вы можете заменить `OcrLanguage.English` на другой поддерживаемый язык.

```csharp
// Step 3: Create an OCR engine and specify the language
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    Image = imgStream // assign the previously loaded image
};

// Optionally, apply your license to unlock the full feature set
var license = new License();
license.SetLicense(@"YOUR_DIRECTORY\Aspose.OCR.NET.lic");

// Run the recognition process
ocrEngine.Recognize();
```

Зачем мы задаём свойство `Image` перед вызовом `Recognize()`? Движку нужен корректный источник изображения; иначе он бросит `NullReferenceException`. Присвоив `ImageStream`, подготовленный на Шаге 2, мы гарантируем плавное выполнение.

## Шаг 4 – Получить и отобразить извлечённый текст (Преобразовать изображение в текст)

После завершения работы движка распознанный текст находится в свойстве `Text`. Здесь и происходит магия **преобразования изображения в текст**.

```csharp
// Step 4: Get the recognized text
string extractedText = ocrEngine.Text;

// Display it in the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);
```

Типичный вывод может выглядеть так:

```
=== OCR Result ===
Invoice #12345
Date: 2026-04-30
Total: $1,250.00
Thank you for your business!
```

Если изображение размыто или содержит сложные шрифты, вы можете увидеть искажённые символы. В таком случае стоит отрегулировать свойство `Resolution` движка или предварительно обработать изображение (например, бинаризация) перед передачей в OCR.

## Шаг 5 – Продвинуто: Как извлечь текст из изображения с пользовательскими настройками

Иногда настройки по умолчанию недостаточны. Ниже несколько настроек, которые помогают, когда **как извлечь текст из изображения** становится сложной задачей.

```csharp
// Increase DPI for better accuracy on low‑resolution images
ocrEngine.Image = ImageStream.FromFile(imagePath);
ocrEngine.Image.DpiX = 300;
ocrEngine.Image.DpiY = 300;

// Enable auto‑rotate if the image might be skewed
ocrEngine.AutoRotate = true;

// Restrict recognition to a specific character set (e.g., digits only)
ocrEngine.RecognitionSettings.Characters = "0123456789.-";
```

Эти корректировки могут значительно улучшить результаты при работе с чеками, формами или отсканированными таблицами. Помните, **как выполнять OCR** — это не универсальное решение; часто требуется экспериментировать с настройками в зависимости от исходного материала.

## Шаг 6 – Распространённые подводные камни при чтении текста из JPG файлов

Даже с надёжной библиотекой разработчики сталкиваются с препятствиями. Ниже несколько, с которыми вы можете столкнуться, пытаясь **читать текст из jpg**:

| Проблема | Почему происходит | Быстрое решение |
|----------|-------------------|-----------------|
| **Низкий контраст** | Сжатие JPG может выравнивать цвета, делая текст неразличимым от фона. | Предобработайте изображение фильтрами повышения контраста (например, `ImageSharp` или `System.Drawing`). |
| **Неправильная ориентация** | Телефоны иногда сохраняют метаданные ориентации вместо поворота пикселей. | Установите `ocrEngine.AutoRotate = true` или вручную поверните изображение перед OCR. |
| **Большой размер файла** | Очень высокоразрешённые JPG занимают много памяти и замедляют распознавание. | Уменьшите масштаб изображения до разумного DPI (например, 300) перед загрузкой. |

Учитывая эти моменты, вы сэкономите часы отладки, когда позже будете **загружать изображение для OCR** в продакшене.

## Шаг 7 – Итоговый код: пример в одном файле

Ниже полная, исполняемая программа, объединяющая всё. Скопируйте её в новый консольный проект и нажмите **F5**.

```csharp
using System;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣  Set up license (optional but recommended)
        // -------------------------------------------------
        var license = new License();
        // Replace with your actual license path or comment out for trial mode
        license.SetLicense(@"YOUR_DIRECTORY\Aspose.OCR.NET.lic");

        // -------------------------------------------------
        // 2️⃣  Load the image you want to process
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");
        ImageStream imgStream = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣  Create OCR engine – this is where we **perform OCR**
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            Image = imgStream,
            AutoRotate = true   // helpful for photos taken at odd angles
        };

        // -------------------------------------------------
        // 4️⃣  Run recognition
        // -------------------------------------------------
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 5️⃣  Retrieve and display the result – **convert image to text**
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

**Ожидаемый вывод** (при условии, что `sample.jpg` содержит чёткий английский текст):

```
=== OCR Result ===
Hello, world!
This is a sample image for OCR testing.
```

Если вы видите пустой вывод, дважды проверьте путь к изображению и убедитесь, что файл не повреждён.

## Заключение

Теперь вы знаете **как выполнять OCR** в C# с помощью Aspose OCR, от установки пакета до **загрузки изображения для OCR**, запуска движка и, наконец, **преобразования изображения в текст**. Руководство также охватывало практические советы по **чтению текста из jpg** файлов и ответило на распространённый вопрос **как извлечь текст из изображения**, когда настройки по умолчанию не справляются.

Что дальше? Попробуйте передавать движку PDF (преобразовав каждую страницу в изображение), экспериментировать с многоязычным распознаванием или интегрировать шаг OCR в более крупный конвейер обработки документов. Возможности безграничны, и с прочным фундаментом, который вы только что построили, вы сможете решить любую задачу по извлечению текста.

Не стесняйтесь оставить комментарий, если столкнётесь с проблемой или обнаружите хитрый приём — удачной разработки!

![Пример выполнения OCR](/images/ocr-example.png "Как выполнить OCR в C# – визуальный обзор")

## Связанные руководства

- [Извлечение текста из изображения C# с выбором языка с помощью Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Преобразовать изображение в текст — выполнить OCR на изображении из URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Как выполнить OCR изображения — выполнить OCR на изображении в распознавании изображений OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}