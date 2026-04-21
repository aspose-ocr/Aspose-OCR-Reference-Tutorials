---
category: general
date: 2026-03-13
description: Как использовать OCR в C# для извлечения текста из сканов. Узнайте, как
  преобразовать TIFF в текст с помощью Aspose OCR, ускорения на GPU и пошагового кода.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: ru
og_description: Как использовать OCR в C# для извлечения текста из сканов. Это руководство
  показывает, как преобразовать TIFF в текст с помощью Aspose OCR и ускорения на GPU.
og_title: Как использовать OCR в C# – быстро извлекать текст из сканов
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Как использовать OCR в C# – быстро извлекать текст из сканов
url: /ru/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

with markdown formatting.

Proceed.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в C# – Быстро извлекать текст из сканов

Когда‑нибудь задумывались **как использовать OCR**, чтобы извлечь читаемый текст из кучи отсканированных TIFF‑файлов? Вы не одиноки. Во многих реальных проектах — будь то оцифровка счетов, архивирование исторических документов или просто создание поисковых PDF — разработчикам нужен надёжный способ **извлекать текст из сканов** без лишних усилий.

Хорошая новость? С Aspose OCR и несколькими строками C# вы сможете конвертировать TIFF в текст за считанные секунды, даже на скромном рабочем месте. Ниже вы найдёте полностью готовый пример, а также объяснение каждого выбора, чтобы вы могли адаптировать его под свой рабочий процесс.

## Что вам понадобится

Прежде чем погрузиться в детали, убедитесь, что у вас есть следующее:

| Требование | Почему это важно |
|------------|------------------|
| .NET 6+ (или .NET Framework 4.7+) | Пакет NuGet Aspose OCR нацелен на современные .NET‑рантаймы. |
| Visual Studio 2022 (или любая IDE) | Предоставляет IntelliSense и удобную отладку. |
| GPU с поддержкой CUDA и драйвер (опционально) | Позволяет установить `ocrEngine.UseGpu = true` для заметного ускорения при обработке больших пакетов. |
| Папка с TIFF‑изображениями, которые нужно обработать | В этом руководстве используются файлы `*.tif`, но вы можете изменить шаблон. |
| NuGet‑пакет Aspose.OCR (`Install-Package Aspose.OCR`) | Основная библиотека, выполняющая всю тяжёлую работу. |

Если чего‑то не хватает, установите это сейчас — нет смысла продолжать чтение, только чтобы позже столкнуться с отсутствующей зависимостью.

## Обзор решения

На высоком уровне программа делает три вещи:

1. **Создаёт OCR‑движок** и при желании включает ускорение GPU.  
2. **Итерирует каждый TIFF‑файл** в каталоге, запускает распознавание и сохраняет полученный простой текст.  
3. **Записывает текст** в файл `.txt`, расположенный рядом с исходным изображением.

И всё. Код преднамеренно небольшой, но демонстрирует лучшие практики: явный выбор языка, правильное освобождение ресурсов и обработку ошибок для самых распространённых граничных случаев.

![Пример использования OCR в C#](/images/how-to-use-ocr-csharp.png "Иллюстрация того, как использовать OCR в C# для извлечения текста из сканов")

## Шаг 1: Инициализация OCR‑движка (Как использовать OCR)

Первое, что вам нужно — это экземпляр `OcrEngine`. Этот объект является шлюзом ко всей функциональности Aspose OCR. По умолчанию он работает на CPU, но установка `UseGpu = true` заставляет библиотеку перенести тяжёлые матричные вычисления на видеокарту — при условии, что у вас установлен драйвер с поддержкой CUDA.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Почему это важно:**  
- **GPU‑ускорение** может сократить время обработки до 70 % для сканов высокого разрешения.  
- **Явный выбор языка** предотвращает угадывание движком и повышает точность, особенно для нелатинских скриптов.

## Шаг 2: Указать движку место сканов (Преобразование TIFF в текст)

Далее мы сообщаем программе, где искать изображения. Использование `Directory.GetFiles` с фильтром `*.tif` упрощает логику и исключает случайный захват файлов другого типа, например `.jpg` или `.png`.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Примечание о граничном случае:** Если каталог пуст, цикл ниже просто не выполнится, что полностью приемлемо. Позже вы увидите дружелюбное сообщение «No files found».

## Шаг 3: Обработать каждый TIFF‑файл (Извлечение текста из сканов)

Теперь сердце программы: загрузка изображения, запуск OCR и сохранение результата. Вспомогательный метод `ImageStream.FromFile` передаёт файл напрямую в память, что эффективнее, чем сначала загружать `Bitmap`.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Почему мы оборачиваем каждую итерацию в `try/catch`:**  
Обработка партии документов часто сопряжена с проблемами; повреждённый TIFF или сбой памяти не должны прерывать весь процесс. Блок `catch` фиксирует проблему и переходит к следующему файлу, делая конвейер надёжным.

### Ожидаемый вывод

Для каждого `example.tif` вы найдёте соседний `example.txt` с содержимым примерно такого вида:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

Если OCR‑движок не сможет прочитать строку, он просто оставит пустую строку или выведет некорректный символ — приложение не упадёт.

## Шаг 4: Очистка и освобождение ресурсов (Лучшие практики)

`OcrEngine` реализует `IDisposable`, поэтому вежливо освобождать нативные ресурсы, когда они больше не нужны. В небольшом консольном приложении можно полагаться на сборщик мусора, но явное освобождение — полезный навык.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Полный рабочий пример (Готов к копированию)

Ниже представлен полностью готовый к запуску код, который можно вставить в новый проект Console App. Он компилируется «как есть», при условии, что вы добавили NuGet‑пакет Aspose.OCR.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### Быстрый чек‑лист

- **GPU‑флаг** — удалите или установите `false`, если у вас нет драйвера CUDA.  
- **Язык** — замените `Language.English` на любой другой поддерживаемый язык.  
- **Шаблон файлов** — измените `"*.tif"` на `"*.png"` или `"*.*"`, если ваши сканы в другом формате.  

## Распространённые ошибки и профессиональные советы (c# OCR tutorial)

| Проблема | Как избежать |
|----------|--------------|
| **Out‑of‑memory errors** при больших партиях | Обрабатывать файлы небольшими порциями или вызывать `GC.Collect()` после каждых 50 файлов (обычно не требуется). |
| **GPU не обнаружен**, но `UseGpu = true` | Движок тихо переходит на CPU, но вы можете проверить `ocrEngine.IsGpuAvailable` после создания. |
| **Неправильный языковой пакет** приводит к искажённому выводу | Всегда явно задавайте `ocrEngine.Language`; по умолчанию может быть `Language.Unknown`. |
| **Путь к файлу содержит Unicode‑символы** | Используйте `Path.GetFullPath` для нормализации или добавьте префикс `@"\\?\"` в Windows, если путь превышает лимит |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}