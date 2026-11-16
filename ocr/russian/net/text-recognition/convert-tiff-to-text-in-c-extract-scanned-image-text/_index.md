---
category: general
date: 2026-03-05
description: Конвертировать TIFF в текст на C# с помощью Aspose OCR — быстро извлекать
  текст из отсканированных изображений и узнать, как загрузить файл изображения в
  C# для обработки OCR.
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: ru
og_description: Конвертировать TIFF в текст на C# с использованием Aspose OCR. Узнайте
  полный процесс извлечения текста из отсканированных изображений и эффективной загрузки
  файлов изображений.
og_title: Преобразовать TIFF в текст на C# — извлечение текста из отсканированного
  изображения
tags:
- OCR
- C#
- Aspose
title: Конвертировать TIFF в текст на C# – извлечение текста из отсканированного изображения
url: /ru/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Конвертация TIFF в текст на C# – Извлечение текста из отсканированного изображения

Нужно **конвертировать TIFF в текст на C#**? Вы не одиноки в борьбе с многостраничными отсканированными изображениями, которые упорно отказываются становиться поисковыми строками.  
В этом руководстве мы пройдем полный, готовый к запуску решение, которое принимает файл TIFF, передаёт его в Aspose OCR и выводит обычный текст — без дополнительных сервисов, без скрытой магии.

> **Совет:** Если вы работаете с сканами высокого разрешения, включение обработки на GPU может сэкономить секунды на каждой странице.

Мы также покажем, как **извлекать текст из отсканированных изображений** и лучший способ **загружать файлы изображений в C#** в OCR‑движок, чтобы вы могли внедрить эту логику в любой .NET‑проект уже сегодня.

---

## Что вам понадобится

Перед тем как начать, убедитесь, что на вашей машине есть следующее:

| Требование | Причина |
|-------------|--------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | Современная среда выполнения, поддерживает `Span<T>` и асинхронный ввод‑вывод |
| Aspose.OCR for .NET (NuGet package `Aspose.OCR`) | OCR‑движок, который мы будем использовать |
| A valid Aspose OCR license file (`Aspose.OCR.lic`) | Без него вы столкнетесь с ограничениями оценки |
| A TIFF file (single‑ or multi‑page) to test | Пример: `scanned_multi_page.tif` |
| GPU with CUDA 11+ (optional) | Ускоряет распознавание при `EngineMode = Gpu` |

Если чего‑то не хватает, скачайте пакет NuGet сейчас:

```bash
dotnet add package Aspose.OCR
```

---

## Шаг 1: Настройте проект и импортируйте пространства имён

Создайте новое консольное приложение (или добавьте код в существующий проект). Первое, что мы делаем, — импортируем необходимые классы.

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **Почему это важно:** Импорт `Aspose.OCR.Image` предоставляет нам фабрику `ImageStream`, которая может читать файлы TIFF напрямую с диска или из потока. Пропуск этого шага вызовет ошибку компиляции.

---

## Шаг 2: Инициализируйте OCR‑движок и выберите режим обработки

OCR‑движок должен быть настроен **до** назначения любого изображения. Здесь мы решаем, запускать ли его на CPU или использовать GPU.

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*Если вы работаете на сервере без графической карты, измените `Gpu` на `Cpu` или `Auto`.*  
Режим движка влияет на распределение памяти и скорость; режим GPU может быть в 2‑3 раза быстрее на больших, высокоразрешающих TIFF.

---

## Шаг 3: Примените вашу лицензию Aspose OCR

Запуск без лицензии ограничивает вас несколькими страницами и водяными знаками. Загрузите лицензию заранее, чтобы все последующие операции были неограниченными.

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **Распространённая ошибка:** Размещение `SetLicense` после `Recognize()` заставит движок перейти в режим пробной версии для этого вызова.

---

## Шаг 4: Загрузите файл TIFF — обработка одно- и многостраничных изображений

Aspose OCR может читать многостраничные TIFF сразу, но вам нужно передать правильный поток. Вот надёжный шаблон, который работает в обоих случаях.

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### Зачем использовать `ImageStream.FromFile`?

- Он абстрагирует базовый `FileStream`, обрабатывая перечисление страниц TIFF внутри.  
- Он также работает с `MemoryStream`, поэтому вы можете загружать изображения из базы данных или веб‑API, не касаясь файловой системы.

### Пограничный случай: Очень большие TIFF

Если ваш TIFF превышает 200 МБ, рассмотрите загрузку постранично, чтобы избежать исключений out‑of‑memory:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## Шаг 5: Проверьте вывод

При запуске программы вы должны увидеть что‑то вроде:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

Если текст выглядит искажённым, проверьте следующее:

1. **Разрешение** — OCR работает лучше всего при 300 dpi и выше.  
2. **EngineMode** — Переключите на `Cpu`, если драйвер GPU устарел.  
3. **Лицензия** — Убедитесь, что путь к файлу лицензии правильный и файл доступен для чтения.

---

## Часто задаваемые вопросы (FAQ)

### Работает ли это с другими форматами изображений?

Абсолютно. `ImageStream.FromFile` поддерживает JPEG, PNG, BMP и даже PDF (через Aspose.PDF). Просто замените расширение файла.

### Что если мне нужно обрабатывать изображения, хранящиеся в базе данных?

Считайте BLOB в `MemoryStream` и передайте его в `ImageStream.FromStream(memoryStream)`. OCR‑движок обрабатывает его так же, как поток из файла.

### Можно ли запускать это на Linux?

Да — Aspose OCR кросс‑платформенный. Установите соответствующую среду выполнения .NET и убедитесь, что необходимые нативные библиотеки для GPU (если используется) доступны.

---

## Полный рабочий пример (готовый к копированию и вставке)

Ниже представлен весь код программы, готовый к компиляции. Замените `YOUR_DIRECTORY` и путь к файлу лицензии на ваши реальные пути.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

Сохраните как `Program.cs`, выполните `dotnet run` и наблюдайте за выводом текста

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}