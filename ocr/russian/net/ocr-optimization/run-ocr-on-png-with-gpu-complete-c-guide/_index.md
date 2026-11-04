---
category: general
date: 2026-01-02
description: Быстро выполнять OCR на PNG с помощью Aspose OCR и поддержки GPU. Узнайте,
  как распознавать текст на изображении, извлекать текст из изображения и устанавливать
  ограничение памяти GPU.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: ru
og_description: Запускайте OCR для PNG эффективно, используя Aspose OCR и ускорение
  на GPU. Этот учебник покажет, как распознавать текст на изображении, извлекать текст
  из изображения и управлять использованием памяти GPU.
og_title: Запуск OCR на PNG с помощью GPU – Полное руководство по C#
tags:
- OCR
- C#
- GPU
title: Запуск OCR на PNG с использованием GPU – Полное руководство по C#
url: /ru/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Запуск OCR на PNG с GPU – Полное руководство на C#

Когда‑то вам нужно **запустить OCR на PNG**‑файлах, но вы сталкиваетесь с проблемой производительности? Вы не одиноки. Во многих реальных конвейерах один высоко‑разрешённый PNG может «задушить» OCR‑движок, работающий только на CPU, превращая быструю проверку в минутную задержку.  

Хорошая новость в том, что Aspose OCR поставляется с GPU‑расширениями, позволяющими **распознавать текст из изображений** за доли времени. В этом руководстве мы пошагово покажем, как **запустить OCR на PNG** с помощью C#, как **извлекать текст из изображения**, а также как **установить ограничение памяти GPU**, чтобы оставаться в рамках вашего аппаратного бюджета.

Мы также разберём «как» и «почему» каждого шага, чтобы у вас было прочное ментальное представление — а не просто готовый кусок кода.

## Что вы узнаете

- Какие предварительные условия нужны для использования поддержки GPU в Aspose OCR.  
- Как загрузить PNG в `Bitmap` и передать его OCR‑движку.  
- Как настроить `GpuDevice` и `GpuMemoryLimitMb` для оптимальной производительности.  
- Как **распознавать текст из изображения** и получить результат в виде простого текста.  
- Советы по работе с типичными проблемами, такими как GPU с небольшим объёмом памяти или многополосные PNG‑файлы.  

К концу этого руководства вы сможете **запускать OCR на PNG**‑файлах на скорости GPU и уверенно управлять объёмом памяти ваших OCR‑задач.

![Диаграмма, показывающая запуск OCR на PNG с ускорением GPU](run-ocr-on-png-diagram.png "пример запуска OCR на PNG")

## Предварительные требования

Прежде чем погрузиться в детали, убедитесь, что у вас есть:

1. .NET 6.0 или новее (код работает и с .NET Core, и с .NET Framework).  
2. NVIDIA‑GPU с поддержкой CUDA (в примере используется устройство с индексом 0).  
3. Пакет NuGet Aspose.OCR и его GPU‑расширения (`Aspose.OCR.Extensions`).  
4. Пример PNG (`input.png`), размещённый в папке, доступной из вашего проекта.  

Если что‑то из этого вам незнакомо, не переживайте — мы укажем альтернативы, где это уместно.

---

## Шаг 1 – Установите Aspose OCR и GPU‑расширения

Первое дело. Без нужных библиотек остальной код не скомпилируется.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

Пакет `Aspose.OCR.Extensions` подтягивает нативные CUDA‑бинарники, необходимые для ускорения на GPU.  
*Совет:* Если у вас машина без GPU, проект всё равно можно собрать; просто позже задайте `PreferGpu = false`.

---

## Шаг 2 – Загрузите PNG, который хотите обработать

Теперь мы действительно **запускаем OCR на PNG**, загружая его в `Bitmap`. Шаг прост, но стоит отметить: `Bitmap` ожидает путь к файлу, поэтому убедитесь, что путь корректен относительно исполняемого файла.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

Если PNG необычно большой (например, более 5000 px по одной из сторон), имеет смысл сначала уменьшить его, чтобы не исчерпать память GPU. Именно здесь позже пригодится опция **установить ограничение памяти GPU**.

---

## Шаг 3 – Создайте и настройте OCR‑движок для работы с GPU

Это сердце руководства: настройка OCR‑движка для **распознавания текста из изображения** с использованием GPU. Две свойства ключевые:

- `GpuDevice` – выбирает, какое CUDA‑устройство использовать.  
- `GpuMemoryLimitMb` – ограничивает объём памяти GPU, который может выделить движок.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**Зачем ограничивать память?** Некоторые GPU делят память с дисплеем или одновременно обслуживают несколько задач. Ограничивая выделение, вы предотвращаете падения из‑за нехватки памяти, особенно при параллельной обработке множества PNG‑файлов.

---

## Шаг 4 – Задайте параметры распознавания (язык и предпочтение GPU)

Объект `RecognitionOptions` сообщает движку, какой язык искать и следует ли **предпочитать GPU** даже для небольших изображений. Для большинства английских документов этого достаточно, но вы можете заменить `Language.English` на любой поддерживаемый язык.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

Если понадобится **извлекать текст из изображения** на другом языке, просто измените перечисление `Language`. Библиотека поддерживает десятки языков «из коробки».

---

## Шаг 5 – Запустите OCR и получите результат

Когда всё настроено, остаётся один вызов, который действительно **запускает OCR на PNG** и возвращает богатый объект результата.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

`OcrResult` содержит не только простой текст (`ocrResult.Text`), но и оценки уверенности, ограничивающие рамки и даже оригинальное изображение с подсвеченными словами — полезно для отладки или визуализации извлечения.

**Ожидаемый вывод** (для примера PNG с надписью «Hello World»):

```
=== OCR Output ===
Hello World
```

Если текст выглядит искажённым, проверьте, что PNG не повреждён и что ограничение памяти GPU не слишком низкое для данного размера изображения.

---

## Шаг 6 – Обработка граничных случаев и рекомендации

### GPU с небольшим объёмом памяти

Если появляется исключение вроде `CudaException: out of memory`, уменьшите `GpuMemoryLimitMb` или разбейте PNG на плитки перед обработкой. Тилдинг можно выполнить с помощью `Graphics.DrawImage` на клоне `Bitmap`.

### Обработка нескольких PNG в пакете

При обработке папки PNG переиспользуйте один экземпляр `OcrEngine` — инициализация один раз экономит переключения контекста GPU.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### Переход на CPU

Если GPU недоступен, просто задайте `PreferGpu = false`. Движок автоматически переключится на CPU без изменения кода.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Полный рабочий пример

Ниже полная программа, которую можно скопировать в новый консольный проект. В ней собраны все шаги выше, плюс несколько проверок безопасности.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Сохраните файл как `Program.cs`, выполните `dotnet run`, и вы увидите извлечённый текст в консоли.

---

## Заключение

Мы продемонстрировали, как **запускать OCR на PNG**‑файлах с помощью GPU‑расширений Aspose OCR, как **распознавать текст из изображения** и как **извлекать текст из изображения**, контролируя **установку ограничения памяти GPU**. Настраивая `GpuDevice` и `GpuMemoryLimitMb`, вы сохраняете приложение быстрым и стабильным даже на скромных GPU.

Дальше вы можете:

- Поэкспериментировать с другими языками (`Language.French`, `Language.Spanish`).  
- Интегрировать шаг OCR в более крупный конвейер обработки документов.  
- Добавить пост‑обработку, такую как проверка орфографии или извлечение сущностей, чтобы улучшить «сырой» текст.  

Помните, важен не только код, но и понимание, почему каждое настройка имеет значение. Когда вы знаете, как **установить ограничение памяти GPU** и когда переключаться на CPU, вы создаёте OCR‑решения, которые масштабируются без проблем.

Есть вопросы о конкретном размере PNG, многополосных TIFF‑файлах или ошибках GPU? Оставляйте комментарий ниже, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}