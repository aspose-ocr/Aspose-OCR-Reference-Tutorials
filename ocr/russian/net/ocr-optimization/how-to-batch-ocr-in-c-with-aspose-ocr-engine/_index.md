---
category: general
date: 2026-01-01
description: Как выполнять пакетное распознавание OCR с помощью Aspose OCR Engine
  в C#. Научитесь распознавать текст на изображениях и извлекать текст из файлов TIFF
  с ускорением на GPU.
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from TIFF
language: ru
og_description: Как выполнять пакетное OCR в C# с помощью Aspose OCR Engine. Это руководство
  показывает, как распознавать текст на изображениях и эффективно извлекать текст
  из файлов TIFF.
og_title: Как выполнить пакетное OCR в C# – Полное руководство Aspose
tags:
- OCR
- C#
- Aspose
- GPU
title: Как пакетно выполнять OCR в C# с помощью движка Aspose OCR
url: /ru/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять пакетное OCR в C# с Aspose OCR Engine

Когда‑нибудь задавались вопросом **как выполнять пакетное OCR**, когда у вас есть десятки отсканированных документов, лежащих в папке? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, переходя от распознавания одного изображения к обработке целой коллекции. Хорошая новость в том, что Aspose OCR делает это проще простого, независимо от того, работаете ли вы на CPU или используете ускорение GPU.

В этом руководстве мы пройдем полный, готовый к запуску пример, который **распознает текст с изображений** и даже **извлекает текст из TIFF**‑файлов пакетно. Никаких расплывчатых «см. документацию» обходных путей — только автономное решение, которое вы можете скопировать‑вставить и запустить уже сегодня.

## Предварительные требования

Перед тем как начать, убедитесь, что у вас есть:

* .NET 6.0 или новее (код нацелен на .NET 6, но .NET 5 тоже работает).
* NuGet‑пакет Aspose.OCR для .NET (доступны версии для CPU и GPU; установите ту, которая соответствует вашему оборудованию).
* Папка с несколькими образцами файлов TIFF или PNG, которые вы хотите обработать.
* Visual Studio 2022 или любая другая IDE по вашему выбору.

> **Pro tip:** Если планируете использовать версию с GPU, убедитесь, что драйвер видеокарты обновлен, а CUDA 11+ установлен. При отсутствии совместимого GPU движок автоматически переключится на CPU.

## Шаг 1 – Настройка проекта и установка Aspose.OCR

### H2: Создайте новое консольное приложение и добавьте Aspose.OCR

Откройте терминал (или консоль диспетчера пакетов в Visual Studio) и выполните:

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

Если у вас есть лицензия с поддержкой GPU, добавьте вместо этого пакет GPU:

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

Вот и всё — ваш проект теперь ссылается на OCR‑библиотеку, которую мы будем использовать для **пакетного OCR**.

## Шаг 2 – Инициализация OCR‑движка (CPU или GPU)

### H2: Как выполнять пакетное OCR – Инициализация движка

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**Почему это важно:** Переключая `UseGpu`, вы позволяете Aspose выбрать самый быстрый путь. Если GPU недоступен, движок тихо переключается обратно на CPU, поэтому ваш пакетный процесс никогда не падает из‑за отсутствующего оборудования.

## Шаг 3 – Сбор файлов для обработки

### H2: Распознавание текста с изображений – Формирование списка файлов

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**Примечание о граничных случаях:** Если у вас смешанный набор форматов, измените шаблон поиска на `"*.*"` и отфильтруйте по расширению внутри цикла. Это сохраняет гибкость пакетной обработки.

## Шаг 4 – Обработка каждого изображения и предварительный просмотр

### H2: Извлечение текста из TIFF – Проход по файлам

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**Что вы увидите:** Для каждого TIFF консоль выводит что‑то вроде:

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```

Этот предварительный просмотр подтверждает, что пакет успешно завершён, без необходимости открывать каждый файл вручную.

## Шаг 5 – Сохранение результатов (необязательно, но удобно)

### H3: Сохранение OCR‑вывода в текстовые файлы

Если вам нужен полный текст для последующей обработки, добавьте следующий код внутри цикла `foreach`:

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

Теперь каждый TIFF получает сопутствующий файл `.txt` с полным результатом OCR — идеально для индексации, поиска или передачи в языковую модель.

## Шаг 6 – Запуск демо и проверка

1. Сборка проекта: `dotnet build`.
2. Запуск: `dotnet run --project GpuBatchDemo.csproj`.

Вы должны увидеть строки предварительного просмотра в консоли, а (если вы добавили необязательный шаг) серию файлов `.txt` рядом с исходными изображениями.

### H3: Распространённые ошибки и способы их исправления

| Симптом | Вероятная причина | Решение |
|---------|-------------------|---------|
| **Empty `ocrResult.Text`** | Изображение слишком тёмное или низкое DPI | Предобработайте изображения (увеличьте контраст, масштабируйте) или установите `ocrEngine.Settings.PreprocessImage = true`. |
| **GPU error “CUDA driver version is insufficient”** | Устаревший драйвер | Обновите драйвер GPU или установите `UseGpu = false`, чтобы принудительно использовать CPU. |
| **Exception “File not found”** | Неправильный разделитель пути в Linux/macOS | Используйте `Path.Combine` или прямые слеши (`/`). |

## Шаг 7 – Масштабирование (больше нескольких файлов)

Когда количество TIFF переходит от десятков к тысячам, учитывайте:

* **Параллельная обработка:** Оберните `foreach` в `Parallel.ForEach` (убедитесь, что экземпляр движка потокобезопасен; иначе создавайте отдельный экземпляр на каждый поток).
* **Пакетный ввод/вывод:** Читайте изображения партиями, чтобы не исчерпать ОЗУ.
* **Логирование:** Записывайте прогресс в лог‑файл; это помогает возобновить работу после сбоя.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **Remember:** Память GPU общая, поэтому запуск слишком большого количества параллельных GPU‑задач может фактически замедлить процесс. Сначала протестируйте с небольшим числом потоков.

## Полный рабочий пример (готовый к копированию)

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

Запуск этой программы **распознает текст с изображений**, **извлечёт текст из TIFF** и продемонстрирует **как выполнять пакетное OCR** эффективно.

## Заключение

У вас теперь есть надёжный сквозной пример **как выполнять пакетное OCR** в C# с использованием OCR‑движка Aspose. Руководство охватывало всё: от настройки проекта, переключения ускорения GPU, формирования списка файлов, обработки каждого изображения и сохранения результатов. Независимо от того, извлекаете ли вы текст из TIFF‑файлов или любого другого формата, тот же шаблон применим — просто замените расширения файлов.

Готовы к следующему шагу? Попробуйте интегрировать вывод OCR в поисковый индекс, передать текст в большую языковую модель или поэкспериментировать с параллельной обработкой, чтобы сократить время обработки огромных пакетов. Возможности безграничны, а у вас уже есть фундамент для дальнейшего развития.

Есть вопросы или хотите поделиться своими приёмами пакетного OCR? Оставьте комментарий ниже — happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}