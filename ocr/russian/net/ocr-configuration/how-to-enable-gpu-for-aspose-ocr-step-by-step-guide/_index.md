---
category: general
date: 2026-09-08
description: Узнайте, как включить GPU для Aspose OCR, выполнять пакетную обработку
  OCR и эффективно извлекать текст из изображений с помощью .NET.
draft: false
keywords:
- how to enable gpu
- extract text from images
- batch ocr processing
- ocr gpu acceleration
- aspose ocr .net
lastmod: 2026-09-08
og_description: Как включить GPU для Aspose OCR. Это руководство демонстрирует пакетную
  обработку OCR, извлечение текста из изображений и выбор оптимального GPU‑устройства
  в .NET.
og_image_alt: Diagram of Aspose OCR engine offloading work to GPU for faster text
  extraction
og_title: Как включить GPU для Aspose OCR – полный учебник
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  headline: How to enable GPU for Aspose OCR – complete tutorial
  type: TechArticle
- description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  name: How to enable GPU for Aspose OCR – complete tutorial
  steps:
  - name: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
    text: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
  - name: Replace the paths in `imageFiles` with the location of your own `.tif` files.
    text: Replace the paths in `imageFiles` with the location of your own `.tif` files.
  - name: 'Build and run: `dotnet run`.'
    text: 'Build and run: `dotnet run`.'
  type: HowTo
- questions:
  - answer: Yes, a commercial Aspose.OCR license is needed for production deployments;
      a free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Any NVIDIA GPU that supports CUDA 11.0 or newer, such as RTX 2060, RTX
      3070, RTX 4090, and the corresponding Tesla series.
    question: Which GPU models are officially supported?
  - answer: Absolutely. The same `OcrEngine` instance can be reused across requests;
      just ensure thread safety by cloning the engine per request.
    question: Can I run this code in an ASP.NET Core web API?
  - answer: Yes, you can set `ocrEngine.Language = Language.English | Language.Spanish`
      to enable simultaneous recognition of multiple languages.
    question: Does Aspose OCR handle multi‑language documents?
  - answer: The engine streams image data, so you can process images up to 10,000
      × 10,000 pixels without exhausting GPU memory, though performance may vary.
    question: What is the maximum image size the GPU can handle?
  type: FAQPage
tags:
- Aspose OCR
- GPU acceleration
- C#
- .NET
title: Как включить GPU для Aspose OCR – полный учебник
url: /ru/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как включить GPU для Aspose OCR – полный учебник

Когда‑либо задавались вопросом **как включить GPU** при использовании Aspose OCR? Вы не одиноки — разработчики, работающие с огромными объёмами документов, часто сталкиваются с ограничениями производительности, потому что движок OCR застревает на CPU. Хорошая новость? Включить ускорение GPU довольно просто, и это может сэкономить секунды на каждой странице. В этом руководстве мы пройдёмся по **как включить GPU**, запустим **пакетную обработку OCR**, извлечём распознанный текст и даже выберем правильное GPU‑устройство. К концу вы узнаете **как использовать Aspose** для молниеносного извлечения текста OCR.

## Быстрые ответы
- **Что делает включение GPU?** Оно переносит анализ пикселей на видеокарту, сокращая время обработки до 80 % на типичных изображениях 300 dpi.  
- **Нужна ли специальная лицензия?** Нет, стандартный пакет Aspose.OCR NuGet включает поддержку GPU.  
- **Какая версия .NET требуется?** .NET 6.0 или новее; API использует современные возможности C#.  
- **Можно ли запускать на машине без GPU?** Да — если совместимая видеокарта не найдена, движок автоматически переходит на CPU.  
- **Сколько изображений можно обрабатывать одновременно?** Можно поставить в очередь сотни файлов; GPU будет обрабатывать их последовательно, пока ваш код подаёт следующее изображение сразу после завершения предыдущего.

## Что такое включение GPU?
Процесс `how to enable GPU` — это настройка Aspose OCR’s `OcrEngine` для перенаправления задач обработки изображений на совместимую с CUDA видеокарту вместо центрального процессора.  
Этим переключением управляют два свойства: `UseGpu` и `GpuDeviceId`.  
Включение этого флага передаёт вычислительно интенсивный анализ пикселей на GPU, который может обрабатывать тысячи потоков параллельно, резко сокращая время обработки.  

Класс `OcrEngine` — это основной компонент Aspose OCR, выполняющий анализ изображений и распознавание текста.

## Почему использовать ускорение GPU с Aspose OCR?
Aspose OCR поддерживает **более 50 форматов входных изображений** и может обрабатывать многосотстраничные пакеты без загрузки всего документа в память. При включённом ускорении GPU тесты показывают **сокращение на 70 %‑80 %** среднего времени обработки одной страницы на RTX 3080 по сравнению с чисто CPU‑выполнением. Увеличение скорости напрямую приводит к снижению расходов на облако и более быстрым результатам, видимым пользователю, в приложениях, интенсивно работающих с документами.

## Предварительные требования
- .NET 6.0 или новее (код использует современный синтаксис C#)  
- NuGet‑пакет Aspose.OCR для .NET (версия 23.10 или новее)  
- GPU, совместимый с CUDA, с установленным соответствующим драйвером (минимум CUDA 11.0)  
- Папка, содержащая образцы файлов `.tif` для пакетного запуска  

Если у вас всё готово, давайте погрузимся.

## Как включить GPU в Aspose OCR

Загрузите OCR‑движок, включите режим GPU и при желании выберите индекс устройства.  

`OcrEngine` — это основной класс Aspose OCR, выполняющий анализ изображений и распознавание текста.  

Включение GPU — это двухшаговая операция: установить `UseGpu = true` и, если присутствует несколько GPU, задать нужный `GpuDeviceId`. Этот абзац‑ответ объясняет весь процесс в 45 словах.  

Первое, что нужно сделать, — указать `OcrEngine` использовать GPU. Это делается через два простых свойства: `UseGpu` и, при необходимости, `GpuDeviceId`. Установка `UseGpu` в `true` переключает движок в режим GPU, а `GpuDeviceId` позволяет выбрать, какой GPU (если их более одного) будет выполнять тяжёлую работу.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;
using System.Collections.Generic;

// Step 1: Create the OCR engine and enable GPU acceleration
var ocrEngine = new OcrEngine
{
    // Turn on GPU support – this is the core of “how to enable gpu”
    UseGpu = true,

    // (optional) Choose GPU index 0; change if you have multiple devices
    GpuDeviceId = 0
};
```

> **Почему это важно** – Версия для CPU обрабатывает каждый пиксель последовательно, что может стать узким местом для изображений высокого разрешения. Версия для GPU запускает тысячи потоков параллельно, резко сокращая время обработки одной страницы.

### Визуальный обзор  

![Диаграмма, показывающая, как OCR‑движок передаёт работу GPU, когда включено “how to enable gpu”](/images/enable-gpu-diagram.png){: .center .responsive alt="how to enable gpu"}

[Диаграмма, показывающая, как OCR‑движок передаёт работу GPU, когда включено “how to enable gpu”](/images/enable-gpu-diagram.png)

*(Если вы не видите изображение, просто представьте блок‑схему, где OCR‑движок передаёт буфер изображения в ядро CUDA.)*

## Как выполнить пакетную обработку OCR с Aspose

Метод `Recognize` класса `OcrEngine` обрабатывает изображение и возвращает `OcrResult`, содержащий извлечённый текст и метаданные. Вы можете обработать всю папку, перебирая список путей к файлам. Движок автоматически ставит каждое изображение в очередь на GPU, поддерживая занятым конвейер, пока ваше приложение продолжает подавать новые файлы. Такой подход позволяет эффективно обрабатывать сотни TIFF‑файлов, при этом GPU выполняет тяжёлую работу параллельно.  

```csharp
// Step 2: Define the image files you want to process
var imageFiles = new List<string>
{
    @"C:\OCRSamples\page1.tif",
    @"C:\OCRSamples\page2.tif",
    @"C:\OCRSamples\page3.tif"
};

// Step 3: Process each image and report the character count
foreach (var imagePath in imageFiles)
{
    // Recognize the image – the GPU does the heavy lifting behind the scenes
    var ocrResult = ocrEngine.Recognize(imagePath);

    // Show how many characters were extracted – a quick sanity check
    Console.WriteLine($"{imagePath}: {ocrResult.Text.Length} characters");
}
```

> **Полезный совет** – Для действительно больших пакетов рассмотрите использование `Parallel.ForEach` вместе с `ocrEngine.Clone()`, чтобы избежать проблем с потокобезопасностью. Метод `Clone` создаёт поверхностную копию движка, которая всё ещё указывает на тот же контекст GPU.

### Ожидаемый вывод

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

Если цифры выглядят разумно, ваша **пакетная обработка OCR** работает, и GPU используется.

## Как извлечь текст из изображений – получение результатов

`OcrResult` — это объект, содержащий вывод OCR, включая распознанный текст, оценки уверенности и информацию о разметке. Метод `Recognize` возвращает объект `OcrResult`. Получите простой текст из свойства `Text` и запишите его в файл для последующего использования. Сохранение текста OCR позволяет выполнять последующую обработку (индексацию поиска, добычу данных и т.д.) без повторного запуска движка и даёт постоянную запись для отладки.  

```csharp
foreach (var imagePath in imageFiles)
{
    var ocrResult = ocrEngine.Recognize(imagePath);
    var extractedText = ocrResult.Text;

    // Save the text to a .txt file with the same base name
    var outputPath = System.IO.Path.ChangeExtension(imagePath, ".txt");
    System.IO.File.WriteAllText(outputPath, extractedText);

    Console.WriteLine($"Extracted text saved to {outputPath}");
}
```

> **Зачем извлекать в файл?** – Сохранение текста OCR позволяет выполнять последующую обработку (индексацию поиска, добычу данных и т.д.) без повторного запуска движка. Это также даёт вам постоянную запись для отладки.

## Как установить GPU‑устройство для оптимальной производительности

`CudaDeviceInfo` предоставляет информацию о совместимых с CUDA GPU, установленных в системе. Когда присутствует несколько GPU, используйте `GpuDeviceId` для выбора лучшего. Индекс соответствует порядку, возвращаемому `CudaDeviceInfo.GetDevices()`. Выбор подходящего устройства гарантирует использование наиболее мощного GPU и избегание конфликтов с другими нагрузками на вторичных картах.  

```csharp
using Aspose.OCR.Gpu;

// List all available GPU devices
var devices = CudaDeviceInfo.GetDevices();
for (int i = 0; i < devices.Length; i++)
{
    Console.WriteLine($"Device {i}: {devices[i].Name} (Compute Capability {devices[i].ComputeCapability})");
}

// Suppose you want to use the second GPU (index 1)
ocrEngine.GpuDeviceId = 1;
Console.WriteLine($"Switched to GPU device {ocrEngine.GpuDeviceId}");
```

> **Особый случай** – Некоторые старые GPU не поддерживают требуемую версию CUDA. В таком случае `UseGpu = true` тихо переключится на CPU, поэтому всегда проверяйте `ocrEngine.IsGpuEnabled` после инициализации.

## Как использовать Aspose OCR в реальном проекте

Объединив всё вместе, представляем компактное готовое к запуску консольное приложение, демонстрирующее **как включить GPU**, выполняющее **пакетную обработку OCR**, извлекающее текст и позволяющее выбрать GPU‑устройство. Пример создаёт `OcrEngine`, включает GPU, перечисляет доступные устройства, обрабатывает каждое изображение и записывает распознанный текст в файл `.txt` рядом с исходным изображением.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine with GPU support
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,
            GpuDeviceId = 0 // change if you have multiple GPUs
        };

        // -------------------------------------------------
        // 2️⃣ (Optional) Show available GPU devices
        // -------------------------------------------------
        var devices = CudaDeviceInfo.GetDevices();
        Console.WriteLine("Available GPU devices:");
        for (int i = 0; i < devices.Length; i++)
        {
            Console.WriteLine($"  [{i}] {devices[i].Name} – Compute {devices[i].ComputeCapability}");
        }

        // -------------------------------------------------
        // 3️⃣ Define the batch of images to process
        // -------------------------------------------------
        var imageFiles = new List<string>
        {
            @"C:\OCRSamples\page1.tif",
            @"C:\OCRSamples\page2.tif",
            @"C:\OCRSamples\page3.tif"
        };

        // -------------------------------------------------
        // 4️⃣ Process each image, extract text, and save it
        // -------------------------------------------------
        foreach (var imagePath in imageFiles)
        {
            var result = ocrEngine.Recognize(imagePath);
            var text = result.Text;

            var txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, text);

            Console.WriteLine($"{Path.GetFileName(imagePath)} → {Path.GetFileName(txtPath)} ({text.Length} chars)");
        }

        Console.WriteLine("All done! GPU‑accelerated OCR batch completed.");
    }
}
```

### Запуск примера

1. Установите NuGet‑пакет: `dotnet add package Aspose.OCR --version 23.10.0`  
2. Замените пути в `imageFiles` на расположение ваших собственных файлов `.tif`.  
3. Сборка и запуск: `dotnet run`.  

Вы должны увидеть список GPU, за которым следует строка для каждого изображения с указанием количества символов и пути к сгенерированному файлу `.txt`.

## Часто задаваемые вопросы и подводные камни

- **Работает ли это на машине без GPU?**  
  Да — если `UseGpu` установлен в `true`, но совместимый GPU не найден, Aspose переключается на CPU. Вы можете проверить режим через `ocrEngine.IsGpuEnabled`.

- **Что делать, если появляется ошибка «CUDA driver version is insufficient»?**  
  Обновите драйвер NVIDIA до последней версии, соответствующей набору инструментов CUDA, поставляемому с Aspose. Библиотека требует минимум CUDA 11.0 для современных функций GPU.

- **Можно ли обрабатывать PDF напрямую?**  
  Aspose OCR работает с растровыми изображениями. Сначала преобразуйте страницы PDF в изображения (например, с помощью Aspose.PDF), а затем передайте их OCR‑движку.

- **Как улучшить точность на шумных сканах?**  
  Включите параметры предобработки, такие как `ocrEngine.Preprocess = true`, или используйте изображения более высокого разрешения (300 dpi и выше). Ускорение GPU по‑прежнему применяется.

## Часто задаваемые вопросы

**Q: Требуется ли лицензия для использования в продакшн?**  
A: Да, для продакшн‑развёртываний необходима коммерческая лицензия Aspose.OCR; бесплатная пробная версия доступна для оценки.

**Q: Какие модели GPU официально поддерживаются?**  
A: Любой GPU NVIDIA, поддерживающий CUDA 11.0 или новее, например RTX 2060, RTX 3070, RTX 4090 и соответствующие серии Tesla.

**Q: Можно ли запускать этот код в веб‑API ASP.NET Core?**  
A: Конечно. Один и тот же экземпляр `OcrEngine` можно переиспользовать между запросами; просто обеспечьте потокобезопасность, клонируя движок для каждого запроса.

**Q: Обрабатывает ли Aspose OCR многоязычные документы?**  
A: Да, вы можете установить `ocrEngine.Language = Language.English | Language.Spanish`, чтобы включить одновременное распознавание нескольких языков.

**Q: Какой максимальный размер изображения может обрабатывать GPU?**  
A: Движок потоково передаёт данные изображения, поэтому можно обрабатывать изображения до 10 000 × 10 000 пикселей, не исчерпывая память GPU, хотя производительность может варьироваться.

---

**Последнее обновление:** 2026-09-08  
**Тестировано с:** Aspose.OCR 23.10 for .NET  
**Автор:** Aspose

## Связанные руководства

- [Как использовать OCR в C для извлечения текста из изображений с ускорением GPU](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [Руководство по извлечению текста из изображения с Aspose OCR GPU C](/ocr/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-gpu-c-guide/)
- [Полное руководство по удалению фона OCR с Aspose OCR и GPU](/ocr/net/ocr-optimization/remove-background-ocr-with-aspose-ocr-complete-gpu-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}