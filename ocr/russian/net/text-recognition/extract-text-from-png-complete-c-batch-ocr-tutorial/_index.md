---
category: general
date: 2026-04-26
description: Быстро извлекайте текст из PNG‑файлов с помощью C#. Узнайте, как преобразовать
  изображения в текст, читать PNG‑файлы, перебрать изображения и выполнять пакетное
  OCR за считанные минуты.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: ru
og_description: Быстро извлекайте текст из PNG‑файлов с помощью C#. Это руководство
  показывает, как преобразовать изображения в текст, читать PNG‑файлы, проходить по
  изображениям и выполнять пакетное OCR изображений.
og_title: Извлечение текста из PNG – Полный пакетный OCR‑урок на C#
tags:
- C#
- OCR
- Aspose
title: Извлечение текста из PNG – Полное руководство по пакетному OCR на C#
url: /ru/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из PNG – Полный C# Batch OCR Tutorial

Когда‑нибудь вам нужно было **извлечь текст из PNG** файлов, но вы не знали, с чего начать? Вы не одиноки — многие разработчики сталкиваются с этим, когда впервые пытаются выполнить OCR в папке со скриншотами. Хорошая новость в том, что с несколькими строками кода на C# и Aspose OCR вы можете преобразовать изображения в текст, читать PNG‑файлы, проходить по изображениям и пакетно обрабатывать всё за один раз.  

В этом руководстве мы пройдемся по готовому к запуску консольному приложению, которое делает именно это. К концу вы получите автономное решение, которое извлекает текст из каждого PNG в каталоге и сохраняет соответствующий файл `.txt` рядом с изображением. Никаких дополнительных скриптов, без ручного копирования‑вставки — только чистый код.

## Что понадобится

- **.NET 6 SDK** (или любая более новая версия .NET). Он бесплатный, быстрый и работает везде.
- **Aspose.OCR for .NET** (пакет NuGet). Библиотека включает ускорение GPU, если у вас совместимый графический процессор, но также автоматически переходит на CPU.
- Папка с несколькими **PNG‑изображениями**, которые вы хотите обработать.  
- Текстовый редактор или IDE — Visual Studio, VS Code, Rider — что вам больше нравится.

Это всё. Если у вас уже есть всё перечисленное, вы готовы начинать.

![пример извлечения текста из png](image.png "демонстрационный скриншот извлечения текста из png")

*Image alt text: “extract text from png using C# batch OCR”*

## Шаг 1 – Настройка проекта и установка Aspose.OCR

Сначала создайте новый консольный проект и подключите пакет Aspose OCR.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

Зачем нам консольное приложение? Это самый простой хост для пакетных задач, его можно запускать из командной строки или планировать с помощью планировщика задач. Если позже понадобится UI, вы просто перенесёте основную логику в библиотеку классов.

## Шаг 2 – Инициализация ускоренного GPU OCR‑движка (или резервный CPU)

Aspose предлагает `GpuOcrEngine`, который автоматически обнаруживает поддерживаемый GPU. Если он не найден, происходит переключение на обычный CPU‑движок — дополнительный код не требуется.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**Pro tip:** Если вы работаете на безголовом сервере без GPU, замените `GpuOcrEngine` на `OcrEngine`, и код будет вести себя точно так же.

## Шаг 3 – Проход по изображениям в целевом каталоге

Нужно **loop through images** и выбирать только PNG‑файлы. Метод `Directory.GetFiles` делает всю тяжёлую работу, а мы защитимся от пустой папки.

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

Обратите внимание на использование `SearchOption.TopDirectoryOnly`. Если позже понадобится рекурсия по подпапкам, просто переключитесь на `AllDirectories`. Это небольшое изменение позволяет **convert images to text** во всём дереве одним вызовом.

## Шаг 4 – Выполнение OCR и сохранение результата

Теперь начинается ядро процесса **batch OCR images**. Мы загружаем каждый PNG, вызываем `Recognize()`, и записываем извлечённую строку в файл `.txt` с тем же базовым именем.

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**Why wrap it in a try/catch?** В реальных пакетах изображений часто встречаются повреждённые файлы или PNG с редким цветовым профилем. Перехват исключения предотвращает падение всей операции и позволяет продолжать обработку остальных файлов.

## Шаг 5 – Запуск приложения и проверка вывода

Соберите и запустите приложение:

```bash
dotnet run
```

Вы должны увидеть в консоли журнал, похожий на:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

Откройте любой из сгенерированных файлов `.txt` — там будет ваш извлечённый текст. Если файл пустой, проверьте качество изображения; OCR работает лучше всего с чётким, контрастным текстом.

### Быстрый скрипт проверки (по желанию)

Если хотите убедиться, что каждому PNG сопоставлен текстовый файл, выполните эту крошечную однострочную команду PowerShell:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## Распространённые варианты и граничные случаи

| Situation | What to Change |
|-----------|----------------|
| **Non‑Latin languages** (e.g., Cyrillic) | Set `ocrEngine.Language = Language.Cyrillic;` |
| **Large image set (>10 000 files)** | Use `Parallel.ForEach` to speed up processing, but watch GPU memory usage. |
| **Need to keep original image order** | Sort `pngFiles` before the `foreach` (`Array.Sort(pngFiles);`). |
| **Running on a CI server without a GPU** | Replace `GpuOcrEngine` with `OcrEngine` to avoid GPU initialization errors. |
| **You only want to process files that contain a specific keyword** | After `result.Text` is retrieved, check `result.Text.Contains("Invoice")` before writing the file. |

Эти настройки позволяют адаптировать конвейер **convert images to text** под практически любую ситуацию, с которой вы можете столкнуться.

## Полный исходный код (готов к копированию)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

Сохраните этот файл как `Program.cs`, выполните `dotnet run` и наблюдайте за магией.

## Заключение

Теперь у вас есть **полное, готовое к продакшену решение для извлечения текста из PNG** файлов с помощью C#. В руководстве рассмотрено всё — от настройки проекта, инициализации ускоренного GPU OCR‑движка, **looping through images**, до **batch OCR images** и сохранения результатов в виде обычного текста.  

Если вам интересны дальнейшие шаги, попробуйте:

- **Convert images to text** for other formats (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}