---
category: general
date: 2025-12-29
description: Как использовать OCR в C# для извлечения текста из изображений, отображения
  количества символов и повышения производительности с помощью ускорения на GPU, используя
  Aspose OCR.
draft: false
keywords:
- how to use OCR
- extract text image
- display character count
- gpu acceleration ocr
- c# ocr aspose
language: ru
og_description: Как использовать OCR в C# для извлечения текста из изображений, отображения
  количества символов и ускорения обработки с помощью GPU, используя Aspose OCR.
og_title: Как использовать OCR в C# – быстрое извлечение текста с помощью GPU
tags:
- OCR
- C#
- Aspose
- GPU
title: Как использовать OCR в C# — извлечение текста из изображений с ускорением на
  GPU
url: /ru/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в C# – Полное руководство

Когда‑нибудь задумывались **как использовать OCR** в проекте .NET без написания тысяч строк кода? Может быть, вы отсканировали огромный TIFF‑файл и вам нужен текст быстро, или просто хотите подсчитать символы для отчётной панели. В любом случае, вы попали по адресу. В этом руководстве мы пройдёмся по извлечению текста из изображения, отображению количества символов и ускорим процесс с помощью **GPU acceleration OCR** – всё это с библиотекой **C# Aspose OCR**.

Мы также добавим второстепенные темы, которые вы, возможно, ищете: **extract text image**, **display character count** и трюки **c# ocr aspose**. К концу вы получите готовое к запуску консольное приложение, которое быстро обработает большие сканы.

---

## Что вы узнаете

- Настроить Aspose OCR в проекте C# (без загадок NuGet).  
- Включить **GPU acceleration OCR** для больших файлов.  
- Загрузить изображение и **извлечь текст из изображения**.  
- **Отобразить количество символов** и время обработки.  
- Обработать распространённые проблемы, такие как отсутствие драйверов GPU или неподдерживаемые форматы изображений.

> **Требования:** .NET 6+ (или .NET Framework 4.7.2) и совместимый GPU. Если у вас нет GPU, код автоматически переключится в режим CPU.

![Как использовать OCR с ускорением GPU в C#](ocr-gpu.png "пример использования OCR с показом использования GPU")

*Image alt text: как использовать OCR иллюстрация с ускорением GPU*

## Шаг 1: Установить Aspose OCR и подготовить проект

### Почему это важно

Прежде чем вы сможете **использовать OCR**, библиотеку необходимо подключить. Aspose OCR поставляется в виде единого пакета NuGet, который включает нативные бинарники как для CPU, так и для GPU, поэтому вам не придётся вручную искать DLL‑файлы.

```csharp
// In your terminal or Package Manager Console
dotnet add package Aspose.OCR
```

> **Pro tip:** Если вы нацеливаетесь на .NET Framework, используйте UI NuGet в Visual Studio, чтобы избежать конфликтов версий.

### Полный скелет проекта

Создайте новое консольное приложение и вставьте следующий `Program.cs`. Он содержит все необходимые `using`‑директивы, так что вам не придётся угадывать, что импортировать.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing; // optional, for advanced pre‑processing

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Call the helper that does the heavy lifting
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            // Step 2: Create and configure the OCR engine (see next section)
        }
    }
}
```

Сохраните файл, восстановите пакеты, и вы готовы к следующему шагу.

---

## Шаг 2: Как использовать движок OCR с ускорением GPU

### Почему включать GPU?

Обработка многомегапиксельного TIFF на CPU может занимать секунды или даже минуты. Путь **GPU acceleration OCR** переносит пиксельные операции на видеокарту, резко сокращая время — часто до доли от исходного.

```csharp
static void RunOcr(string imagePath)
{
    // Create an OCR engine instance
    var ocrEngine = new OcrEngine();

    // Enable GPU acceleration – if a compatible device is found
    ocrEngine.UseGpu = true;
    ocrEngine.GpuDeviceId = 0; // 0 = first GPU; change if you have multiple

    // Optional sanity check – fall back to CPU if GPU init fails
    try
    {
        // This call forces the engine to initialize GPU resources
        ocrEngine.InitializeGpu();
        Console.WriteLine("✅ GPU acceleration enabled.");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
        ocrEngine.UseGpu = false;
    }

    // Load the image (this also validates format)
    var inputImage = Image.Load(imagePath);
    
    // Perform OCR – the heavy lifting happens here
    var ocrResult = ocrEngine.Recognize(inputImage);

    // Step 3: Display results (character count & processing time)
    DisplayResult(ocrResult);
}
```

> **Почему это работает:** `UseGpu` переключает внутренний конвейер. `InitializeGpu()` принудительно проверяет драйверы заранее, чтобы вы могли обнаружить проблемы до длительного вызова `Recognize`.

---

## Шаг 3: Извлечь текст из изображения и отобразить количество символов

Теперь, когда движок работает, давайте **извлечь текст из изображения** и показать, сколько символов было распознано. Это часть, которую большинство разработчиков пропускают, но она критична для валидации и последующего анализа.

```csharp
static void DisplayResult(OcrResult ocrResult)
{
    // The raw OCR text
    string extractedText = ocrResult.Text;

    // Character count – includes spaces and line breaks
    int charCount = extractedText.Length;

    // Processing time in milliseconds (provided by Aspose)
    long processingMs = ocrResult.ProcessingTime;

    // Output to console – easy to pipe to a file or logger
    Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
    Console.WriteLine("----- Begin OCR Text -----");
    Console.WriteLine(extractedText);
    Console.WriteLine("------ End OCR Text ------");
}
```

**Ожидаемый вывод** (пример для сканирования из 2‑х страниц):

```
✅ GPU acceleration enabled.
🖋️ Extracted 12,345 characters in 842 ms
----- Begin OCR Text -----
Lorem ipsum dolor sit amet, consectetur...
... (rest of the page) ...
------ End OCR Text ------
```

Если GPU недоступен, вы увидите предупреждение и тот же результат, только медленнее.

---

## Шаг 4: Обработка больших файлов и граничных случаев

### Что если изображение огромное?

Aspose OCR может потоково обрабатывать страницы, но всё равно требуется достаточный объём ОЗУ. Хорошая практика — уменьшать DPI, несущественное для распознавания, перед обработкой:

```csharp
// Optional pre‑processing: downscale to 300 DPI if original > 600 DPI
if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
{
    inputImage = inputImage.Resize(0.5, 0.5); // 50% reduction
    Console.WriteLine("🔎 Image downscaled for faster OCR.");
}
```

### Отсутствие драйверов GPU?

`try/catch` вокруг `InitializeGpu()` уже ловит большинство проблем, но вы также можете запросить доступные устройства:

```csharp
var gpuInfo = GpuDeviceManager.GetDevices();
if (gpuInfo.Count == 0)
{
    Console.WriteLine("⚡ No GPU detected – defaulting to CPU.");
    ocrEngine.UseGpu = false;
}
```

### Неподдерживаемые форматы изображений?

Aspose поддерживает TIFF, PNG, JPEG, BMP и несколько экзотических форматов. Если вы получите `UnsupportedFormatException`, сначала конвертируйте файл с помощью инструмента вроде ImageMagick или встроенного метода `Image.Save` в PNG.

---

## Шаг 5: Итоги – Полный рабочий пример

Скопируйте‑вставьте всю программу ниже в `Program.cs`. Это автономный демонстрационный пример, который можно запустить сразу (только замените путь).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust the path to point at your scanned TIFF or JPEG
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,
                GpuDeviceId = 0
            };

            try
            {
                ocrEngine.InitializeGpu();
                Console.WriteLine("✅ GPU acceleration enabled.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
                ocrEngine.UseGpu = false;
            }

            var inputImage = Image.Load(imagePath);

            // Optional downscale for gigantic files
            if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
            {
                inputImage = inputImage.Resize(0.5, 0.5);
                Console.WriteLine("🔎 Image downscaled for faster OCR.");
            }

            var ocrResult = ocrEngine.Recognize(inputImage);
            DisplayResult(ocrResult);
        }

        static void DisplayResult(OcrResult ocrResult)
        {
            string extractedText = ocrResult.Text;
            int charCount = extractedText.Length;
            long processingMs = ocrResult.ProcessingTime;

            Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
            Console.WriteLine("----- Begin OCR Text -----");
            Console.WriteLine(extractedText);
            Console.WriteLine("------ End OCR Text ------");
        }
    }
}
```

Запустите его командой `dotnet run` и наблюдайте, как консоль выводит **character count** и текст OCR. Это весь цикл **how to use OCR** от начала до конца.

---

## Заключение

Мы только что рассмотрели **how to use OCR** в C# для **extract text from images**, **display character count** и ускорения всего конвейера с помощью **GPU acceleration OCR** используя библиотеку **c# ocr aspose**. Ключевые выводы:

1. Установить Aspose OCR через NuGet и подключить правильные пространства имён.  
2. Включить GPU, но всегда иметь резервный режим CPU.  
3. Загрузить изображение, при необходимости уменьшить масштаб, затем вызвать `Recognize`.  
4. Получить `ocrResult.Text` и `ocrResult.ProcessingTime`, чтобы **отобразить количество символов** и метрики производительности.  

Отсюда вы можете развивать проект — сохранять текст в базе данных, отправлять его в поисковый индекс или выполнять определение языка над извлечённой строкой. Если нужно обрабатывать PDF, просто передавайте каждую страницу как изображение; тот же код будет работать.

**Next steps** you might explore:

- Использовать **extract text image** из многостраничных PDF с помощью `PdfConverter`.  
- Настройка параметров OCR (языковые пакеты, подавление шума) для повышения точности.  
- Масштабирование решения в Azure Functions или AWS Lambda с GPU‑поддержкой.  

Попробуйте, сломайте, а затем улучшите. Так создаются реальные OCR‑проекты. Приятного кодинга и пусть ваши сканы всегда читаются!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}