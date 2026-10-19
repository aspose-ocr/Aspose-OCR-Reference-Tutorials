---
category: general
date: 2026-04-01
description: Узнайте, как быстро распознавать текст из PNG‑файлов, задав идентификатор
  GPU‑устройства и включив ускорение GPU в Aspose OCR. Пошаговое руководство на C#.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: ru
og_description: Быстро распознавайте текст из PNG‑файлов, задав идентификатор GPU‑устройства.
  Следуйте этому полному руководству по C#, чтобы включить ускорение GPU с помощью
  Aspose OCR.
og_title: Распознавание текста из PNG – ускоренный GPU‑технологией учебник Aspose
  OCR
tags:
- C#
- OCR
- GPU
- Aspose
title: Распознавание текста из PNG с Aspose OCR – пакетный демонстрационный пример
  с ускорением GPU
url: /ru/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание текста из png – Полный C# GPU‑ускоренный пакетный учебник

Когда‑нибудь вам нужно было **распознавать текст из png** изображений, но процесс оказался мучительно медленным? Вы не одиноки. Большинство разработчиков начинают с простого вызова OCR, а затем смотрят на консоль, которая ползёт, как улитка, когда папка содержит десятки скриншотов.  

Хорошая новость? Aspose OCR может переложить тяжёлую работу на вашу видеокарту, и всего парой строк вы можете **set gpu device id**, чтобы выбрать именно нужный GPU. В этом руководстве мы пройдём полный, готовый к запуску пример, который собирает все PNG из папки, включает GPU‑ускорение, выбирает первый GPU и выводит количество символов для каждого файла.

К концу вы получите автономную программу, которую можно вставить в любой .NET‑проект, и поймёте, почему включение GPU имеет значение, как обрабатывать граничные случаи и что можно настроить для ещё лучшей производительности.

## Что понадобится

- **.NET 6.0** или новее (код также компилируется с .NET Core).  
- Пакет **Aspose.OCR** из NuGet – установите его командой `dotnet add package Aspose.OCR`.  
- Машина с совместимым с CUDA GPU (обычно NVIDIA) и соответствующим драйвером.  
- Папка, заполненная **PNG**‑изображениями, которые нужно обработать.  

Если что‑то из этого вам незнакомо, не паникуйте. Ниже указаны точные команды, которые вам потребуются, а также мы обсудим, что делать, если GPU отсутствует.

## Шаг 1: Инициализация OCR‑движка и включение GPU‑ускорения  

Первое, что нужно сделать, — создать экземпляр `OcrEngine` и включить поддержку GPU. Этот флаг сообщает Aspose использовать нативные библиотеки CUDA под капотом.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Почему это важно:** Без `UseGpuAcceleration` каждое изображение обрабатывается на CPU, что может быть в разы медленнее, особенно для PNG‑файлов высокого разрешения. Включение флага также подготавливает движок к принятию конкретного GPU‑устройства позже.

## Шаг 2: Установить ID GPU‑устройства (необязательно, но рекомендуется)  

Если в вашей рабочей станции более одного GPU, вы можете выбрать, какой использовать. ID устройств начинаются с **0**, так что `0` выбирает первый GPU, `1` — второй и т.д.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Pro tip:** При работе на общем сервере явная установка ID GPU‑устройства может предотвратить захват ресурсов другими процессами. Если эту строку опустить, Aspose выберет устройство по умолчанию, что обычно нормально для однографического окружения.

## Шаг 3: Сбор всех PNG‑файлов из папки пакета  

Далее нам нужно найти каждый PNG, который вы хотите обработать OCR‑ом. Метод `Directory.GetFiles` делает всю тяжёлую работу.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Edge case:** Если папка пуста, `imageFiles` будет пустым массивом. Мы обработаем это позже, выведя дружелюбное сообщение.

## Шаг 4: Обработать каждое изображение и вывести количество распознанных символов  

Теперь основной цикл. Для каждого PNG вызываем `Recognize`, затем печатаем имя файла и длину извлечённого текста.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**What you’ll see:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

Если изображение не содержит текста, счёт будет `0`. Это полностью нормально для скриншотов, состоящих только из графики.

## Шаг 5: Запустить программу и проверить использование GPU  

Соберите файл (`dotnet build`) и запустите его (`dotnet run`). Пока консоль прокручивается, откройте ваш инструмент мониторинга GPU (например, NVIDIA Smi), чтобы увидеть кратковременный всплеск загрузки GPU для каждого изображения. Если активности нет, проверьте следующее:

1. Установлен драйвер CUDA.  
2. `UseGpuAcceleration` установлен в `true`.  
3. Правильный `GpuDeviceId` соответствует физическому GPU.

Если GPU недоступен, Aspose автоматически переключится на CPU, но вы потеряете преимущество в скорости.

## Общие варианты и советы  

| Ситуация | Что изменить |
|-----------|----------------|
| **Different image format** (e.g., JPEG) | Change the search pattern to `*.jpg` or `*.*` and Aspose will still recognise the text. |
| **Batch size is huge** (thousands of files) | Process in chunks to avoid memory pressure: split `imageFiles` into smaller arrays. |
| **Need the actual text, not just length** | Replace `ocrResult.Text.Length` with `ocrResult.Text` in the `WriteLine`. |
| **Running on a headless server** | Ensure the server has a GPU driver; otherwise, set `UseGpuAcceleration = false` to avoid unnecessary errors. |
| **Multiple GPUs, want to balance load** | Loop over `ocrEngine.GpuDeviceId = i % gpuCount` inside the `foreach` to rotate devices. |

## Ожидаемый вывод и проверка  

Когда всё работает, консоль выводит имя каждого файла, за которым следует количество символов, как показано выше. Чтобы двойной проверкой убедиться в правильности OCR‑вывода, вы можете временно вывести сам текст:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

Просто не забудьте удалить или закомментировать эту строку для больших пакетов; вывод тысяч строк может перегрузить ваш терминал.

## Полный рабочий пример (готовый к копированию)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

Сохраните этот файл как `GpuBatchDemo.cs`, выполните `dotnet add package Aspose.OCR`, затем `dotnet run`. Вы должны увидеть почти мгновенный вывод количества символов для каждого PNG благодаря GPU‑ускорению.

## Заключение  

Теперь вы знаете, как **распознавать текст из png** файлов эффективно, включив GPU‑ускорение и явно **set gpu device id** в Aspose OCR. Полный, готовый к копированию код обрабатывает поиск папки, проверки граничных случаев и даёт мгновенную обратную связь о производительности OCR.  

Следующие шаги? Попробуйте заменить вызов `Recognize` на `ocrEngine.RecognizeAsync`, если нужен неблокирующий процесс, или поэкспериментировать с различными вариантами предобработки изображений (например, бинаризация), которые предоставляет Aspose. Вы также можете передать результаты OCR в базу данных или поисковый индекс для решения задачи полнотекстового поиска.

Есть вопросы по обработке многостраничных PDF или хотите сравнить Aspose OCR с Tesseract? Оставьте комментарий или изучите наши другие учебники по **batch OCR C#**, **OCR performance tips** и **GPU‑driven image processing**. Happy coding!  

![Вывод консоли, показывающий количество распознанных символов для PNG‑файлов – распознавание текста из png с использованием GPU‑ускорения](image-placeholder.png "пример вывода распознавания текста из png")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}