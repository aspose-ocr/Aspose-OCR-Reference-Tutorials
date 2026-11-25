---
category: general
date: 2026-06-22
description: Узнайте, как распознавать текстовые изображения и извлекать текст из
  высокоразрешённых OCR‑счетов с помощью Aspose OCR. Включает настройку языка OCR
  и ускорение с помощью GPU.
draft: false
keywords:
- recognize text image
- extract text image
- high resolution ocr
- process invoice ocr
- set ocr language
language: ru
og_description: распознавать текст на изображении с помощью Aspose OCR в C#. Этот
  учебник показывает, как извлекать текст из изображений высокоразрешённых счетов,
  задавать язык OCR и повышать производительность.
og_title: Распознавание текста на изображении с помощью Aspose OCR – Полное руководство
  по C#
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to recognize text image and extract text image from high
    resolution OCR invoices using Aspose OCR. Includes set OCR language and GPU acceleration.
  headline: recognize text image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Learn how to recognize text image and extract text image from high
    resolution OCR invoices using Aspose OCR. Includes set OCR language and GPU acceleration.
  name: recognize text image with Aspose OCR – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 SDK or later (the code also works on .NET Framework 4.7+). -
      A valid Aspose.OCR NuGet package (free trial works fine). - A high‑resolution
      image of an invoice (e.g., `high_res_invoice.png`). - Basic familiarity with
      C# and Visual Studio or your favorite IDE.'
  - name: 1. Image Quality Matters
    text: Even the fastest GPU can’t fix a blurry scan. Aim for at least **300 dpi**
      for invoices; lower resolutions cause missed characters. If you can’t control
      the source, consider pre‑processing with a sharpening filter before sending
      the image to Aspose.
  - name: 2. Memory Consumption on Very Large Files
    text: A 5000 × 7000 pixel PNG can consume several hundred megabytes of RAM. If
      you hit `OutOfMemoryException`, split the invoice into pages or downscale slightly
      (e.g., to 250 dpi) before OCR.
  - name: 3. Fallback to CPU When GPU Fails
    text: If the GPU driver crashes, Aspose will silently revert to CPU. To ensure
      you’re always using the GPU, check `ocrEngine.ProcessingMode` after initialization
      and log a warning if it isn’t `ProcessingMode.Gpu`.
  - name: 4. Multi‑Language Documents
    text: 'When an invoice contains both English and Spanish, you can enable **multiple
      languages**:'
  type: HowTo
tags:
- Aspose OCR
- C#
- Image Processing
title: Распознавание текста на изображении с помощью Aspose OCR – Полное руководство
  по C#
url: /ru/net/text-recognition/recognize-text-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание текста на изображении с Aspose OCR – Полное руководство C#

Когда‑то вам нужно было **recognize text image**, но результаты получались размытыми или ужасно медленными? Вы не одиноки. Будь то сканирование высоко‑разрешённого счёта или извлечение данных из отсканированного контракта, получение чистого, надёжного вывода имеет решающее значение. В этом руководстве мы пройдём через полностью готовый к запуску пример, который **recognize text image** из файла высокого разрешения, **extract text image**, а также **set OCR language** для максимальной точности — всё это с использованием ускорения GPU.

Мы также добавим несколько полезных приёмов: как эффективно **process invoice OCR**, почему стоит использовать **high resolution OCR**, и что делать, если GPU недоступен. К концу вы получите одну программу на C#, которая превращает размытый PNG в поисковый текст мгновенно.

## Что вы узнаете

- Как создать экземпляр `OcrEngine` с Aspose OCR.  
- Как включить **GPU acceleration** для молниеносного **high resolution OCR**.  
- Как использовать **set OCR language** для выбора английского (или любого другого поддерживаемого языка).  
- Как **extract text image** из файла счёта высокого разрешения.  
- Как измерять время обработки, чтобы доказать прирост производительности.  
- Как обрабатывать сценарии отката, когда GPU отсутствует.

### Предварительные требования

- .NET 6.0 SDK или новее (код также работает на .NET Framework 4.7+).  
- Действительный пакет Aspose.OCR NuGet (пробная версия подходит).  
- Изображение счёта высокого разрешения (например, `high_res_invoice.png`).  
- Базовые знания C# и Visual Studio или вашей любимой IDE.

---

## Шаг 1: Установите Aspose.OCR и подготовьте проект

Сначала добавьте библиотеку Aspose OCR в ваш проект. Откройте терминал в папке решения и выполните:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Держите пакет обновлённым; новые версии улучшают поддержку GPU и языковые модели.

Создайте новое консольное приложение, если у вас его ещё нет:

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
```

Теперь у вас чистый старт для **recognize text image**.

## Шаг 2: Инициализируйте OCR‑движок (включите GPU)

Сердце процесса — `OcrEngine`. По умолчанию он работает на CPU, но для **high resolution OCR** больших сканов счётов GPU может сократить время выполнения на несколько секунд.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // Enable GPU processing – dramatically speeds up high‑resolution OCR
    ProcessingMode = ProcessingMode.Gpu
};
```

> **Почему GPU?** Изображение высокого разрешения может содержать миллионы пикселей. GPU обрабатывает их параллельно, превращая 5‑секундную задачу на CPU в субсекундную на большинстве современных видеокарт.

Если на целевой машине нет совместимого GPU, Aspose автоматически переключится в режим CPU. Вы можете обнаружить такой откат так:

```csharp
if (ocrEngine.ProcessingMode != ProcessingMode.Gpu)
{
    Console.WriteLine("GPU not available – using CPU fallback.");
}
```

## Шаг 3: **set OCR language** – выберите правильный словарь

Aspose OCR поставляется с базовыми языками; английский установлен по умолчанию, но вы можете явно задать его. Это важно, потому что языковая модель влияет на сегментацию символов и поиск в словаре.

```csharp
// Step 3: Explicitly set the language to English (core language)
ocrEngine.Language = OcrLanguage.English;
```

> **Edge case:** Если нужно читать французский счёт, просто замените `OcrLanguage.English` на `OcrLanguage.French`. Тот же вызов **set OCR language** работает для любого поддерживаемого языка.

## Шаг 4: **recognize text image** – обработайте изображение высокого разрешения

Теперь мы действительно **recognize text image**. Укажите движку путь к PNG (или TIFF) высокого разрешения, который хотите обработать. Путь может быть абсолютным или относительным; просто убедитесь, что файл существует.

```csharp
// Step 4: Recognize the image and capture the result
string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);
```

Объект `OcrResult` содержит как извлечённый текст, так и информацию о времени, которую мы выведем дальше.

## Шаг 5: **extract text image** – покажите результаты и время обработки

Наконец, выведите OCR‑текст и время, затраченное на обработку. Это момент, когда вы можете убедиться, что **process invoice OCR** отработал как ожидалось.

```csharp
// Step 5: Output processing time and extracted text
Console.WriteLine($"GPU OCR time: {ocrResult.ProcessingTimeMs} ms");
Console.WriteLine("=== Extracted Text Start ===");
Console.WriteLine(ocrResult.Text);
Console.WriteLine("=== Extracted Text End ===");
```

Запуск программы должен дать что‑то вроде:

```
GPU OCR time: 312 ms
=== Extracted Text Start ===
Invoice #12345
Date: 2024‑04‑15
Total: $1,250.00
...
=== Extracted Text End ===
```

Вот и всё — ваш рабочий процесс **extract text image** завершён.

---

## Бонус: Обработка распространённых проблем

### 1. Качество изображения имеет значение

Даже самый быстрый GPU не исправит размытый скан. Стремитесь к минимуму **300 dpi** для счётов; более низкое разрешение приводит к пропуску символов. Если вы не контролируете источник, рассмотрите предобработку с помощью фильтра резкости перед передачей изображения в Aspose.

### 2. Потребление памяти при очень больших файлах

PNG‑изображение 5000 × 7000 пикселей может потреблять несколько сотен мегабайт ОЗУ. Если возникает `OutOfMemoryException`, разбейте счёт на страницы или слегка уменьшите масштаб (например, до 250 dpi) перед OCR.

### 3. Откат на CPU при сбое GPU

Если драйвер GPU падает, Aspose тихо переходит на CPU. Чтобы убедиться, что вы всегда используете GPU, проверьте `ocrEngine.ProcessingMode` после инициализации и запишите предупреждение, если он не `ProcessingMode.Gpu`.

### 4. Документы с несколькими языками

Когда счёт содержит и английский, и испанский, можно включить **multiple languages**:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Движок попытается распознать символы из любого из указанных языков.

---

## Полный рабочий пример

Ниже представлен **complete, runnable program**, включающий каждый обсуждённый шаг. Скопируйте‑вставьте его в `Program.cs`, замените путь к изображению и нажмите **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 2: Create an OCR engine instance and enable GPU acceleration
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu // Fast high‑resolution OCR
        };

        // Verify GPU availability (optional but helpful)
        if (ocrEngine.ProcessingMode != ProcessingMode.Gpu)
        {
            Console.WriteLine("GPU not detected – falling back to CPU processing.");
        }

        // Step 3: Set the OCR language (set OCR language for better accuracy)
        ocrEngine.Language = OcrLanguage.English; // Change as needed

        // Step 4: Recognize text from a high‑resolution invoice image
        string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // Step 5: Display processing time and the extracted text
        Console.WriteLine($"GPU OCR time: {ocrResult.ProcessingTimeMs} ms");
        Console.WriteLine("=== Extracted Text Start ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("=== Extracted Text End ===");
    }
}
```

**Ожидаемый вывод** (время будет зависеть от оборудования):

```
GPU OCR time: 287 ms
=== Extracted Text Start ===
Invoice #98765
Date: 2024‑03‑22
Amount Due: $2,340.00
...
=== Extracted Text End ===
```

Запустите его на нескольких разных счётах, чтобы увидеть, как время обработки остаётся менее полусекунды даже на скромном GPU.

---

## Заключение

Вы только что узнали, как **recognize text image** с помощью Aspose OCR, **extract text image** из изображения счёта высокого разрешения и **set OCR language** для оптимальных результатов — всё это с использованием ускорения GPU для **high resolution OCR**. Показанный код готов к продакшн‑использованию, включает логику отката и может быть расширен для обработки многостраничных PDF, разных языков или даже потоков с камеры в реальном времени.

Что дальше?

- Преобразовать извлечённый текст в структурированный JSON‑объект счёта.  
- Добавить предобработку изображения (выравнивание, бинаризация) для повышения точности на низкокачественных сканах.  
- Интегрировать вызов OCR в ASP.NET Core API, чтобы ваш веб‑сервис мог обрабатывать счёта по запросу.

Есть вопросы по **process invoice OCR** или нужна помощь с настройкой языковых пакетов? Оставляйте комментарий ниже, и удачной разработки!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом гиде. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}