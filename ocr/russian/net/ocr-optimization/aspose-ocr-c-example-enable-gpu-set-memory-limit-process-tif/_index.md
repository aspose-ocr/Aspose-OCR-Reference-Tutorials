---
category: general
date: 2026-06-03
description: Пример Aspose OCR на C#, показывающий, как установить ограничение памяти
  GPU, загрузить изображение для OCR и распознать текст из файлов TIF с полным кодом
  и советами.
draft: false
keywords:
- aspose ocr c# example
- set gpu memory limit
- load image for ocr
- recognize text from tif
- gpu acceleration asp ocr
- high‑resolution OCR c#
- asp ocr cuda setup
language: ru
og_description: 'Изучите полный пример Aspose OCR на C#: включите GPU, задайте ограничение
  памяти GPU, загрузите изображение для OCR и распознайте текст из файлов TIF. Полный
  код включён.'
og_title: Пример Aspose OCR на C# – ускорение с помощью GPU, ограничение памяти и
  обработка TIF
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  headline: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  type: TechArticle
- description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  name: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  steps:
  - name: Why set a memory limit?
    text: '- **Stability:** Prevents out‑of‑memory crashes when processing gigantic
      images. - **Co‑existence:** Allows other GPU‑heavy apps (e.g., TensorFlow models)
      to run side‑by‑side. - **Predictability:** Makes performance testing repeatable
      because the GPU won’t start swapping.'
  - name: Handling multi‑page TIFFs
    text: If your TIFF contains several pages, Aspose OCR will only read the first
      one by default. To process all pages, you can loop over `image.Pages` (available
      in newer SDK versions) and feed each page to the engine separately.
  - name: Why this works well with TIF
    text: '- **Lossless compression:** TIFF often stores raw pixel data, giving the
      OCR engine the highest fidelity. - **Multiple color spaces:** Aspose can handle
      grayscale, RGB, or even CMYK TIFFs without extra conversion code.'
  - name: Expected output
    text: 'Running the program on a clear, 300 dpi scan of a printed page typically
      yields something like:'
  - name: Quick checklist
    text: '- ✅ **Aspose OCR C# example** compiled without errors. - ✅ **GPU enabled**
      (`Enable = true`). - ✅ **GPU memory limit** set to 2048 MB. - ✅ **Image loaded**
      from a TIF file. - ✅ **Text recognized** and printed.'
  type: HowTo
tags:
- Aspose
- OCR
- C#
- GPU
title: Пример Aspose OCR на C# – включение GPU, установка ограничения памяти и обработка
  TIF‑изображений
url: /ru/net/ocr-optimization/aspose-ocr-c-example-enable-gpu-set-memory-limit-process-tif/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR C# Example – Включить GPU, установить ограничение памяти и обрабатывать TIF‑изображения

Задумывались ли вы когда‑нибудь, как выжать максимум производительности из кода **Aspose OCR C# example**, работая с огромными сканами TIFF? Вы не одиноки. Во многих реальных проектах — например, оцифровке архивов или извлечении данных из высокоразрешённых чеков — узким местом является не сам алгоритм OCR, а использование аппаратных ресурсов.

Вот в чём дело: Aspose OCR поддерживает ускорение с помощью GPU, но вам нужно явно указать, сколько памяти он может использовать, загрузить правильный тип изображения и, наконец, извлечь распознанный текст из файла .tif. Этот учебник проведёт вас через каждый шаг, от установки SDK до настройки параметров GPU, чтобы вы могли выполнять OCR на молниеносной скорости, не перегружая память вашего GPU.

Мы также добавим несколько сценариев «что если» — например, обработку многостраничных TIFF или переход на CPU, если GPU недоступен — чтобы у вас получилось надёжное решение, а не просто одноразовый фрагмент кода.

## Что вам понадобится

Прежде чем мы начнём, убедитесь, что на вашем компьютере есть следующее:

| Требование | Почему это важно |
|------------|-------------------|
| **.NET 6 SDK** (or later) | Aspose OCR ориентирован на .NET Standard 2.0+, поэтому любой современный .NET‑версии подходит. |
| **Aspose.OCR NuGet package** (`Install-Package Aspose.OCR`) | Основная библиотека, предоставляющая `OcrEngine`, `GpuSettings`, etc. |
| **CUDA 11+** (NVIDIA) **or ROCm 5+** (AMD) | Требуется для ускорения с помощью GPU; SDK проверит наличие совместимого драйвера во время выполнения. |
| A **GPU with at least 2 GB VRAM** (we’ll cap it at 2048 MB) | Без достаточного объёма памяти движок может тихо переключиться на CPU. |
| A **high‑resolution TIFF** image you want to process | Aspose OCR может читать практически любой растровый формат, но TIF часто используется для сканов. |
| Visual Studio 2022 (or any editor you like) | Для сборки и отладки проекта C#. |

Если чего‑то не хватает, код всё равно скомпилируется, но вы не увидите ожидаемого прироста производительности.

## Шаг 1: Создать движок Aspose OCR C# Example

Первое, что делается в каждом **Aspose OCR C# example**, — это создание экземпляра OCR‑движка. Представьте `OcrEngine` как режиссёра фильма — он координирует всё, от загрузки изображения до извлечения текста.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();
```

> **Pro tip:** Если вы планируете обрабатывать много изображений подряд, держите один `OcrEngine` живым. Пересоздание его для каждого изображения добавляет накладные расходы, которые могут затмить время OCR.

## Шаг 2: Установить ограничение памяти GPU (и включить ускорение)

Теперь переходим к части, которая часто ставит людей в тупик: **установить ограничение памяти GPU**. По умолчанию Aspose OCR пытается использовать столько видеопамяти, сколько может, что на общем рабочем месте может «голодать» другие приложения. Объект `GpuSettings` позволяет ограничить выделение.

```csharp
        // Step 2: Enable GPU acceleration (requires CUDA 11+ or ROCm 5+)
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,          // Turn on the GPU path
            DeviceId = 0,           // First GPU in the system (change if you have multiple)
            MemoryLimitMb = 2048    // Optional cap – 2 GB in this example
        };
```

### Почему устанавливать ограничение памяти?

- **Stability:** Предотвращает сбои из‑за нехватки памяти при обработке гигантских изображений.
- **Co‑existence:** Позволяет другим приложениям, использующим GPU (например, модели TensorFlow), работать одновременно.
- **Predictability:** Делает тестирование производительности воспроизводимым, поскольку GPU не будет начинать свопинг.

Если опустить `MemoryLimitMb`, Aspose выделит столько памяти, сколько посчитает нужным, что может быть приемлемо на выделенном сервере вывода, но рискованно на ноутбуке разработчика.

## Шаг 3: Загрузить изображение для OCR

Загрузка правильного формата файла — следующий важный шаг. Метод `OcrImage.FromFile` автоматически определяет тип изображения, но всё равно следует проверить, существует ли файл и поддерживается ли его вариант TIFF (например, сжатие LZW или CCITT‑G4).

```csharp
        // Step 3: Load the high‑resolution image to be processed
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);
```

### Обработка многостраничных TIFF

Если ваш TIFF содержит несколько страниц, Aspose OCR по умолчанию прочитает только первую. Чтобы обработать все страницы, можно перебрать `image.Pages` (доступно в более новых версиях SDK) и передавать каждую страницу движку отдельно.

```csharp
        foreach (var page in image.Pages)
        {
            var result = ocrEngine.Recognize(page);
            System.Console.WriteLine($"--- Page {page.Index + 1} ---");
            System.Console.WriteLine(result.Text);
        }
        return; // Skip the single‑image path below
```

Приведённый выше фрагмент демонстрирует шаблон **load image for OCR**, который работает как с одностраничными, так и с многостраничными файлами.

## Шаг 4: Распознать текст из TIF (или любого растра)

Теперь, когда изображение находится в памяти, мы просим Aspose выполнить свою магию. Метод `Recognize` возвращает `OcrResult`, который содержит простой текст, оценки уверенности и даже информацию о ограничивающих прямоугольниках, если она нужна.

```csharp
        // Step 4: Perform OCR recognition on the image
        var ocrResult = ocrEngine.Recognize(image);
```

### Почему это хорошо работает с TIF

- **Lossless compression:** TIFF часто хранит необработанные пиксельные данные, обеспечивая OCR‑движку наивысшую точность.
- **Multiple color spaces:** Aspose может работать с градациями серого, RGB или даже CMYK‑TIFF без дополнительного кода преобразования.

Если необходимо настроить языковые пакеты (например, французский или японский), установите `ocrEngine.Settings.Language = "fr"` перед вызовом `Recognize`.

## Шаг 5: Вывести распознанный текст

Наконец, выводим текст в консоль. В реальном приложении вы можете записать его в базу данных, JSON‑файл или передать строку в последующий конвейер NLP.

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Ожидаемый вывод

Запуск программы на чистом скане печатной страницы с разрешением 300 dpi обычно даёт примерно следующее:

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
...
```

Если изображение размыто или ограничение памяти GPU слишком низкое, вы можете увидеть искажённые символы или усечённый результат. Уменьшение `MemoryLimitMb` ниже объёма изображения (обычно ~1 ГБ для TIFF 6000×8000 пикселей) может привести к автоматическому переключению движка на CPU.

## Полный рабочий пример

Ниже представлен полный готовый к запуску пример программы. Скопируйте и вставьте его в новый проект Console App, замените `YOUR_DIRECTORY/large_photo.tif` на путь к вашему TIFF‑файлу и нажмите **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration and set a memory cap
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,
            DeviceId = 0,
            MemoryLimitMb = 2048 // 2 GB limit – adjust to your GPU size
        };

        // Step 3: Load the image (ensure the file exists)
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);

        // Step 4: Perform OCR on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 5: Output the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Быстрый чек‑лист

- ✅ **Aspose OCR C# example** скомпилирован без ошибок.  
- ✅ **GPU enabled** (`Enable = true`).  
- ✅ **GPU memory limit** установлен в 2048 MB.  
- ✅ **Image loaded** из TIF‑файла.  
- ✅ **Text recognized** и выведен.

## Распространённые подводные камни и как их избежать

| Симптом | Вероятная причина | Решение |
|---------|-------------------|---------|
| `System.DllNotFoundException: cudart64_110.dll` | Среда выполнения CUDA не установлена или версия не совпадает. | Установите CUDA 11.x (или 12.x), соответствующую вашему драйверу. |
| OCR returns empty string | Изображение слишком тёмное или DPI < 150. | Предобработайте с помощью `image.AdjustContrast()` или пересчитайте до 300 dpi. |
| Out‑of‑memory crash on GPU | `MemoryLimitMb` слишком низок для изображения. | Увеличьте ограничение или разбейте изображение на плитки с помощью `image.Crop`. |
| `Unsupported image format` error | TIFF использует экзотическое сжатие (например, JPEG‑2000). | Конвертируйте TIFF в поддерживаемый формат с помощью ImageMagick перед OCR. |

## Расширение демонстрации

Теперь, когда у вас есть надёжный **aspose ocr c# example**, вы можете захотеть исследовать:

- **Batch processing:** Перебор папки с TIF‑файлами, запись каждого результата в файл `.txt`.
- **Language packs:** `ocrEngine.Settings.Language = "es"` для испанского или загрузка пользовательских словарей.
- **Bounding boxes:** Используйте `ocrResult.Regions` для получения координат каждого слова — удобно для инструментов редактирования.
- **CPU fallback:** Оберните блок GPU в try/catch; при ошибке установите `ocrEngine.Settings.Gpu.Enable = false` и повторите попытку.

Эти расширения сохраняют основной шаблон, одновременно добавляя ценность для конкретных случаев использования‑

## Что следует изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Извлечение текста из изображения с помощью Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Извлечение текста из изображения – оптимизация OCR с Aspose.OCR для .NET](/ocr/english/net/ocr-optimization/)
- [Извлечение текста из изображения C# с выбором языка с использованием Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}