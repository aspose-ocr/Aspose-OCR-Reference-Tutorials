---
category: general
date: 2026-06-22
description: Распознавание текста с изображения с помощью Aspose OCR в C#. Узнайте,
  как автоматически исправлять наклон изображения, предобрабатывать его для OCR и
  включать автоматическое исправление наклона в лаконичном примере OCR на C#.
draft: false
keywords:
- recognize text from image
- auto deskew image
- preprocess image for ocr
- c# ocr example
- enable auto deskew
language: ru
og_description: Распознавание текста с изображения с помощью Aspose OCR в C#. Это
  руководство показывает, как автоматически исправлять наклон изображения, предварительно
  обрабатывать изображение для OCR и включать автоматическое исправление наклона в
  практическом примере OCR на C#.
og_title: Распознавание текста с изображения в C# – Полный пример OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  headline: Recognize Text from Image in C# – Full OCR Example
  type: TechArticle
- description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  name: Recognize Text from Image in C# – Full OCR Example
  steps:
  - name: 1. Low Contrast or Dark Backgrounds
    text: 'Aspose.OCR offers an extra flag `PreprocessingOptions.ContrastEnhancement`.
      Add it to the `Preprocessing` line:'
  - name: 2. Non‑English Documents
    text: Swap `OcrLanguage.English` for `OcrLanguage.Spanish`, `OcrLanguage.French`,
      etc. The engine auto‑loads the appropriate language model.
  - name: 3. Large Images
    text: 'Processing a 5 MP photo can be memory‑hungry. Scale it down first:'
  - name: 4. Getting Bounding Boxes
    text: 'If you need the exact location of each word (e.g., for a UI overlay), iterate
      over `result.Regions`:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Распознавание текста с изображения в C# – Полный пример OCR
url: /ru/net/ocr-optimization/recognize-text-from-image-in-c-full-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Распознавать текст с изображения в C# – Полный пример OCR

Когда‑то задавались вопросом, как **распознавать текст с изображения** в приложении C# без мучений из‑за размытых сканов? Вы не одиноки. Будь то оцифровка чеков, извлечение данных из форм или просто эксперименты с AI‑поддерживаемыми трюками над изображениями, получение чистых результатов OCR зависит от правильной предобработки — подумайте об автоматическом выравнивании изображения и уменьшении шума.  

В этом руководстве мы пройдём через **пример c# ocr**, использующий библиотеку Aspose.OCR для **автоматического выравнивания изображения**, автоматической коррекции наклона фотографий и **предобработки изображения для OCR** всего в несколько строк кода. К концу вы получите исполняемую программу, выводящую распознанный текст прямо в консоль.

## Что вы узнаете

- Как установить и подключить пакет Aspose.OCR через NuGet.  
- Настройка `OcrEngine` с поддержкой английского языка.  
- Включение **автоматического выравнивания изображения** и других параметров предобработки в один шаг.  
- Запуск движка на реальном фото и обработка результата.  
- Советы по работе с краевыми случаями, такими как сильно повернутые изображения или сканы с низким контрастом.

> **Требования** – Вам нужен .NET 6 (или новее) и базовое понимание C#. Предыдущий опыт работы с OCR не требуется.

---

## ## Распознавать текст с изображения – Установите пакет Aspose.OCR

Прежде чем писать код, библиотеку нужно добавить в проект. Откройте терминал в папке решения и выполните:

```bash
dotnet add package Aspose.OCR
```

Эта команда скачает последнюю стабильную версию Aspose.OCR, которая включает движок OCR, языковые пакеты и утилиты предобработки, необходимые нам.  

*Совет:* Если вы целитесь в .NET Framework, а не в .NET Core, используйте UI менеджер пакетов NuGet в Visual Studio — просто найдите “Aspose.OCR” и нажмите **Install**.

---

## ## Распознавать текст с изображения – Инициализируйте OCR‑движок

Теперь, когда пакет готов, можно создать движок. Первый шаг — указать, какой язык ожидать. В большинстве случаев достаточно английского, но библиотека поддерживает десятки языков «из коробки».

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine and set the language to English
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,

            // Step 2: Enable preprocessing to automatically deskew and denoise the image
            Preprocessing = PreprocessingOptions.AutoDeskew | PreprocessingOptions.Denoise
        };
```

**Почему это важно:**  
- `Language = OcrLanguage.English` сообщает движку, какой набор символов использовать, что значительно повышает точность.  
- Свойство `Preprocessing` объединяет два флага — `AutoDeskew` и `Denoise`. Этот шаг **автоматического выравнивания изображения** вращает картинку обратно к горизонтальной базовой линии, а `Denoise` удаляет зернистые артефакты, которые иначе запутали бы OCR‑движок.  

Если пропустить предобработку, часто будет получаться искажённый вывод на сканированных чеках или фотографиях, снятых под углом.

---

## ## Распознавать текст с изображения – Передайте изображение в движок

С готовым движком следующий шаг — передать ему файл изображения. Aspose.OCR принимает путь или `Stream`, поэтому вы можете работать с локальными файлами, встроенными ресурсами или даже изображениями, загруженными из интернета.

```csharp
        // Step 3: Recognize text from the input image
        var result = engine.RecognizeImage(@"YOUR_DIRECTORY/skewed_photo.jpg");
```

**Примечание о краевых случаях:**  
- Если изображение **сильно повернуто** (> 45°), `AutoDeskew` всё равно постарается, но может потребоваться предварительно повернуть его вручную с помощью `System.Drawing` или `ImageSharp` перед передачей в движок.  
- Для **многостраничных PDF** используйте `engine.RecognizePdf`; те же флаги предобработки применяются.

---

## ## Распознавать текст с изображения – Вывод результата

Наконец, выводим извлечённый текст. Объект `result` содержит не только простой текст — он также предоставляет оценки уверенности, ограничивающие рамки и оригинальное изображение с подсвеченными областями. Для быстрой демонстрации достаточно вывести `result.Text`.

```csharp
        // Step 4: Output the recognized text to the console
        System.Console.WriteLine(result.Text);
    }
}
```

При запуске программы вы должны увидеть что‑то вроде:

```
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!
```

Если вывод выглядит «мусором», проверьте, что исходное изображение чёткое, хорошо освещённое, и что **предобработка изображения для OCR** действительно включена (см. флаги `Preprocessing` выше).  

---

## ## Распознавать текст с изображения – Обработка распространённых подводных камней

### 1. Низкий контраст или тёмный фон
Aspose.OCR предлагает дополнительный флаг `PreprocessingOptions.ContrastEnhancement`. Добавьте его в строку `Preprocessing`:

```csharp
Preprocessing = PreprocessingOptions.AutoDeskew |
                PreprocessingOptions.Denoise |
                PreprocessingOptions.ContrastEnhancement
```

### 2. Документы не на английском
Замените `OcrLanguage.English` на `OcrLanguage.Spanish`, `OcrLanguage.French` и т.д. Движок автоматически загрузит соответствующую языковую модель.

### 3. Большие изображения
Обработка фотографии в 5 МП может сильно расходовать память. Сначала уменьшите её:

```csharp
engine.Image = ImageProcessor.Resize(@"YOUR_DIRECTORY/skewed_photo.jpg", 1024, 768);
```

### 4. Получение ограничивающих рамок
Если нужны точные координаты каждого слова (например, для наложения в UI), пройдитесь по `result.Regions`:

```csharp
foreach (var region in result.Regions)
{
    System.Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

---

## ## Распознавать текст с изображения – Полный рабочий пример

Ниже представлен **полный, готовый к копированию** код, включающий все вышеописанные приёмы. Сохраните его как `Program.cs`, замените `YOUR_DIRECTORY` на папку с тестовым изображением и запустите `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,
            // Enable auto deskew, denoise, and contrast enhancement
            Preprocessing = PreprocessingOptions.AutoDeskew |
                            PreprocessingOptions.Denoise |
                            PreprocessingOptions.ContrastEnhancement
        };

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/skewed_photo.jpg";

        // Recognize the image
        var result = engine.RecognizeImage(imagePath);

        // Output plain text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // Optional: print bounding boxes for each detected region
        Console.WriteLine("=== Detected Regions ===");
        foreach (var region in result.Regions)
        {
            Console.WriteLine($"{region.Text}  -->  {region.Bounds}");
        }
    }
}
```

**Ожидаемый вывод в консоль** (при условии, что изображение содержит простой чек):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!

=== Detected Regions ===
Invoice #12345  -->  {X=12,Y=34,Width=250,Height=20}
Date: 2026-06-01  -->  {X=12,Y=60,Width=200,Height=18}
Total: $256.78  -->  {X=12,Y=86,Width=180,Height=18}
Thank you for your business!  -->  {X=12,Y=112,Width=300,Height=22}
```

Если текст выводится чисто, поздравляем — вы успешно **распознали текст с изображения** с автоматическим выравниванием и предобработкой!

---

## ## Распознавать текст с изображения – Следующие шаги и связанные темы

- **Пакетная обработка:** Оберните вызов движка в цикл `foreach`, чтобы обработать десятки фотографий за один проход.  
- **Конверсия PDF:** Используйте `engine.RecognizePdf` для многостраничных документов, затем объедините результаты.  
- **Пользовательские словари:** Передайте список слов в `engine.CustomWords`, чтобы повысить точность в предметных областях (например, медицинские коды).  
- **Тонкая настройка производительности:** Кешируйте экземпляр `OcrEngine`, если обрабатываете много изображений; создание движка — самая дорогая операция.  

Эти расширения естественно используют те же концепции — **предобработка изображения для OCR**, **включение автоматического выравнивания**, и **распознавание текста с изображения** — так что вы сможете переиспользовать изученные шаблоны кода.

---

## Заключение

Мы только что прошли через **пример c# ocr**, показывающий, как **распознавать текст с изображения** с помощью Aspose.OCR, автоматически выравнивая и уменьшая шум на картинке. Включив `AutoDeskew` (функцию **автоматического выравнивания изображения**) и добавив несколько флагов предобработки, вы значительно повышаете надёжность OCR без написания единой строки кода для обработки изображений.

Теперь вы можете взять этот скелет, подставить свои изображения и начать извлекать данные из счетов, удостоверений личности или любых других бумажных документов. Сложный скан? Попробуйте дополнительные параметры предобработки, о которых мы говорили, или поэкспериментируйте с пользовательскими языковыми пакетами. Возможности безграничны.

Если это руководство помогло вам решить проблему, оставьте комментарий, поделитесь результатами или напишите мне на GitHub — happy coding!

## Что следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы вы могли освоить дополнительные возможности API и исследовать альтернативные подходы в своих проектах.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}