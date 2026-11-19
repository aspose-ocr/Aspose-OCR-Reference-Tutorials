---
category: general
date: 2026-09-13
description: Как выполнять пакетное OCR с Aspose OCR GPU на C# с использованием .NET.
  Узнайте, как распознавать текст на изображениях, извлекать текст из файлов TIFF
  и ускорять обработку с поддержкой GPU.
draft: false
keywords:
- aspose ocr gpu
- process multiple images
- how to batch ocr
- install aspose ocr
lastmod: 2026-09-13
og_description: Как выполнять пакетное OCR с Aspose OCR GPU на C# с использованием
  .NET. Это руководство показывает, как распознавать текст на изображениях, извлекать
  текст из файлов TIFF и использовать ускорение GPU для высокопроизводительной обработки.
og_image_alt: Screenshot of Aspose OCR GPU batch processing console output in C#
og_title: Как выполнять пакетное OCR с Aspose OCR GPU на C# с использованием .NET
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: How to batch OCR with Aspose OCR GPU in C# using .NET. Learn to recognize
    text from images, extract text from TIFF files, and accelerate processing with
    GPU support.
  headline: How to batch OCR with Aspose OCR GPU in C# using .NET
  type: TechArticle
- questions:
  - answer: Yes, as long as the server has a CUDA‑compatible GPU and the appropriate
      driver libraries installed; no display is required.
    question: Can I run the GPU version on a headless Linux server?
  - answer: Absolutely. The engine treats each page as a separate image and returns
      concatenated text, preserving page order.
    question: Does Aspose OCR support multi‑page TIFF files out of the box?
  - answer: Benchmarks show Aspose OCR achieves ≥ 96 % character accuracy on clean
      printed documents and ≥ 90 % on low‑contrast scans, matching leading SaaS providers
      while keeping data on‑premises.
    question: How accurate is the OCR output compared with cloud services?
  - answer: The library imposes no hard limit; practical limits are driven by available
      disk space and GPU memory. Processing 10 000 pages on an RTX 3080 typically
      stays under 2 GB of GPU memory.
    question: Is there a limit to the number of files I can process in one run?
  - answer: Yes, set `ocrEngine.Language = OcrLanguage.Spanish` (or any supported
      language) before calling `Recognize`. The engine supports 30+ languages, including
      Arabic, Chinese, and Hindi.
    question: Can I customize the language model for non‑English scripts?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
title: Как выполнять пакетное OCR с Aspose OCR GPU на C# с использованием .NET
url: /ru/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять пакетное OCR с Aspose OCR GPU на C# с использованием .NET

Если вам нужно **batch OCR** сотни отсканированных страниц быстро, движок Aspose OCR GPU предоставляет быстрый, надёжный способ распознавать текст из изображений и файлов TIFF за один запуск. В этом руководстве вы увидите, как настроить проект .NET, включить ускорение GPU и обработать всю папку изображений, не написав ни одной строки шаблонного кода.

## Быстрые ответы
- **Что означает “batch OCR”?** Это автоматизированная обработка множества файлов изображений за одну операцию, возвращающая извлечённый текст для каждого файла.  
- **Могу ли я использовать версию GPU на любой машине?** Да, при условии, что система имеет совместимый с CUDA GPU и установлен соответствующий драйвер.  
- **Нужна ли лицензия для разработки?** Бесплатная пробная лицензия подходит для тестирования; коммерческая лицензия требуется для продакшна.  
- **Какие версии .NET поддерживаются?** .NET 6.0 и более новые полностью поддерживаются; .NET 5 также работает с небольшими корректировками.  
- **Является ли движок потокобезопасным для параллельных запусков?** CPU‑движок потокобезопасен; GPU‑движок требует один экземпляр на поток или контролируемую параллельную стратегию.

## Что такое Aspose OCR GPU?
Движок `Aspose.OCR` GPU — это высокопроизводительная OCR‑библиотека, которая переносит работу по анализу изображений на графическую карту с поддержкой CUDA, обеспечивая до 4‑х раз более высокую пропускную способность по сравнению с чистой обработкой на CPU. Она поддерживает широкий спектр форматов изображений, предоставляет встроенные языковые модели и может быть интегрирована в любое приложение .NET с минимальными изменениями кода.

## Почему использовать Aspose OCR GPU для пакетной обработки?
Aspose OCR поддерживает **более 30 форматов изображений** (включая PNG, JPEG, BMP и многостраничные TIFF) и может обрабатывать файлы размером до **2 ГБ** каждый, не загружая весь документ в память. При включённом ускорении GPU типичные 300‑dpi TIFF‑страницы обрабатываются менее чем за 0,2 секунды на страницу на современной карте RTX 3080.

## Предварительные требования
- .NET 6.0 SDK (или новее), установленный на вашей машине разработки.  
- NuGet‑пакет Aspose.OCR для .NET — выберите пакет `Aspose.OCR.Gpu`, если у вас совместимый GPU, иначе установите `Aspose.OCR`.  
- Папка, содержащая изображения, которые вы хотите обработать (TIFF, PNG, JPEG и т.д.).  
- Visual Studio 2022, Rider или любой редактор, способный собирать .NET консольные приложения.

> **Pro tip:** Убедитесь, что установлен CUDA 11+ и `nvidia-smi` сообщает, что ваш GPU «совместим». Библиотека автоматически переключится на CPU, если не найдёт подходящий GPU.

## Как настроить проект и установить Aspose OCR
Создайте новое .NET консольное приложение, добавьте NuGet‑пакет Aspose OCR и восстановите зависимости. Это подготовит лёгкий проект, который можно компилировать и запускать на любой платформе, поддерживающей .NET 6 или новее. После установки пакета вы можете напрямую ссылаться на классы OCR в коде, включая пакетную обработку без дополнительной конфигурации.

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

Если у вас есть лицензия с поддержкой GPU, установите вместо этого пакет, специфичный для GPU. Эта версия содержит нативные привязки CUDA, позволяющие движку работать на графической карте, обеспечивая описанное ранее ускорение.

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

Ваш проект теперь ссылается на библиотеку OCR, необходимую для **batch OCR**.

## Как инициализировать OCR‑движок (CPU или GPU)
Класс `OcrEngine` является основной точкой входа для выполнения OCR‑операций. Он абстрагирует подлежащий аппаратный уровень и предоставляет простой API как для выполнения на CPU, так и на GPU. Загрузите OCR‑движок и укажите, использовать ли GPU:

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

**Почему это важно:** Установка `UseGpu` позволяет Aspose выбрать самый быстрый путь выполнения. Когда совместимый GPU присутствует, движок работает на графической карте; иначе он переключается на CPU без ошибки, гарантируя, что ваш пакетный процесс не завершится сбоем из‑за отсутствия оборудования.

## Как собрать файлы для обработки
Сбор целевых изображений — первый шаг в любой пакетной работе. Сформируйте список путей файлов, соответствующих поддерживаемым расширениям, затем передайте этот список в OCR‑цикл. Такой подход упрощает код и облегчает добавление фильтрации позже.

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

**Примечание о краевых случаях:** Если ваша папка содержит смешанные форматы, замените шаблон поиска на `"*.*"` и отфильтруйте по расширению внутри цикла. Это сохраняет гибкость пакетной обработки и предотвращает пропуск файлов.

## Как обработать каждое изображение и показать предварительный просмотр
Для каждого файла вызовите OCR‑движок, получите распознанный текст и отобразите короткий фрагмент в консоли. Предпросмотр помогает убедиться, что пакет работает корректно, без открытия каждого выходного файла.

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

**Что вы увидите:** Для каждого изображения консоль выводит первые 100 символов распознанного текста, подтверждая, что пакет успешно завершён без ручного открытия каждого файла.

## Как сохранить результаты OCR (необязательно, но удобно)
Сохранение полного вывода OCR позволяет последующее индексирование, AI‑анализ или конвертацию в поисковые PDF. Запишите текст в файл `.txt`, расположенный рядом с исходным изображением, используя то же базовое имя для простой корреляции.

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

Теперь у каждого изображения есть сопутствующий текстовый файл, содержащий полный вывод OCR, готовый для поисковых систем, языковых моделей или пользовательских аналитических конвейеров.

## Как запустить демонстрацию и проверить вывод
Соберите и запустите консольное приложение, чтобы увидеть работу пакетного процесса. Шаг сборки компилирует код, а шаг выполнения обрабатывает каждое изображение в целевой папке и выводит строки предварительного просмотра в консоль. Если вы включили необязательный шаг сохранения, вы также найдете файл `.txt` для каждого исходного изображения.

1. Соберите проект: `dotnet build`.  
2. Запустите программу: `dotnet run --project GpuBatchDemo.csproj`.

Вы должны увидеть строки предварительного просмотра в консоли и, если вы добавили необязательный шаг, серию файлов `.txt` рядом с вашими исходными изображениями.

## Распространённые подводные камни и способы их устранения
| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| **Empty `ocrResult.Text`** | Изображение слишком тёмное или низкое DPI | Предобработайте изображения (увеличьте контраст, масштабируйте) или включите `ocrEngine.Settings.PreprocessImage = true`. |
| **GPU error “CUDA driver version is insufficient”** | Устаревший драйвер | Обновите драйвер GPU или установите `UseGpu = false`, чтобы принудительно использовать CPU. |
| **Exception “File not found”** | Неправильный разделитель пути в Linux/macOS | Используйте `Path.Combine` или прямые слэши (`/`). |

## Как масштабировать процесс за пределы нескольких файлов
Когда вы переходите от десятков к тысячам изображений, рассмотрите следующие стратегии: использовать параллельную обработку с отдельными экземплярами движка на каждый поток, загружать изображения пакетами управляемого размера и вести журнал прогресса в файл для лёгкого восстановления. Эти приёмы снижают потребление памяти и поддерживают высокую пропускную способность.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **Remember:** Память GPU общая для всего процесса. Запуск слишком большого количества параллельных GPU‑задач может перегрузить память и фактически замедлить пакет. Начинайте с 2‑4 потоков и контролируйте загрузку GPU.

## Часто задаваемые вопросы

**Q: Можно ли запустить версию GPU на безголовом сервере Linux?**  
A: Да, при условии, что сервер имеет совместимый с CUDA GPU и установлены соответствующие драйверные библиотеки; дисплей не требуется.

**Q: Поддерживает ли Aspose OCR многостраничные TIFF‑файлы из коробки?**  
A: Абсолютно. Движок рассматривает каждую страницу как отдельное изображение и возвращает объединённый текст, сохраняя порядок страниц.

**Q: Насколько точен вывод OCR по сравнению с облачными сервисами?**  
A: Тесты показывают, что Aspose OCR достигает ≥ 96 % точности символов на чистых печатных документах и ≥ 90 % на сканах с низким контрастом, сопоставимо с ведущими SaaS‑провайдерами, при этом данные остаются локальными.

**Q: Есть ли ограничение на количество файлов, которые можно обработать за один запуск?**  
A: Библиотека не накладывает жёсткого ограничения; практические ограничения зависят от доступного дискового пространства и памяти GPU. Обработка 10 000 страниц на RTX 3080 обычно занимает менее 2 ГБ памяти GPU.

**Q: Можно ли настроить языковую модель для неанглийских скриптов?**  
A: Да, установите `ocrEngine.Language = OcrLanguage.Spanish` (или любой поддерживаемый язык) перед вызовом `Recognize`. Движок поддерживает более 30 языков, включая арабский, китайский и хинди.

## Заключение
Теперь у вас есть полное решение «сквозного» **batch OCR с Aspose OCR GPU на C#**. Руководство охватило настройку проекта, активацию GPU, перечисление файлов, обработку каждого изображения, необязательное сохранение результатов и техники масштабирования для больших нагрузок. С этой базой вы можете передавать вывод OCR в поисковые индексы, к большим языковым моделям или создавать пользовательские конвейеры обработки документов.

Готовы к следующему вызову? Попробуйте объединить текст OCR с Aspose .PDF для создания поисковых PDF, либо интегрировать вывод с Azure Cognitive Search для мгновенного полнотекстового поиска по тысячам отсканированных документов.

---

**Последнее обновление:** 2026-09-13  
**Тестировано с:** Aspose.OCR 24.5 for .NET (CPU & GPU packages)  
**Автор:** Aspose  

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```
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

## Связанные руководства

- [Как использовать OCR в C# для извлечения текста из изображений с ускорением GPU](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [Распознавание текста с изображения с ускоренным Aspose OCR GPU на C](/ocr/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}