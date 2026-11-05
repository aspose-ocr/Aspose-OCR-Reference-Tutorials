---
category: general
date: 2026-05-06
description: Извлеките текст из изображения с помощью Aspose OCR в C#. Узнайте, как
  конвертировать JPG в текст, установить язык OCR и эффективно считывать текст из
  JPG.
draft: false
keywords:
- extract text from image
- convert jpg to text
- image to text c#
- read text from jpg
- set OCR language
language: ru
og_description: Извлеките текст из изображения в C# с помощью Aspose OCR. Это руководство
  показывает, как преобразовать JPG в текст, установить язык OCR и прочитать текст
  из JPG.
og_title: Извлечение текста из изображения в C# – Полный учебник
tags:
- OCR
- C#
- Aspose
title: Извлечение текста из изображения в C# – пошаговое руководство
url: /ru/net/text-recognition/extract-text-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения в C# – Полное пошаговое руководство

Когда‑нибудь вам нужно было **извлечь текст из изображения**, но вы не знали, какую библиотеку выбрать? Вы не одиноки — разработчики постоянно задают вопрос: «Как преобразовать JPG в текст, не отправляя данные в облако?» Хорошая новость в том, что Aspose OCR предоставляет полностью офлайн‑решение, работающее прямо внутри вашего .NET приложения.

В этом руководстве мы пройдем всё, что вам нужно знать: от установки пакета Aspose OCR NuGet, до **установки языка OCR** для русского текста, и, наконец, **чтения текста из JPG**‑файлов. К концу вы получите переиспользуемый фрагмент кода, который можно вставить в любой проект C# и сразу начать извлекать текст из изображений.

> **Что вы получите в результате**  
> • Чёткий, готовый к запуску пример, который **извлекает текст из изображения**.  
> • Знание того, как **преобразовать JPG в текст** с помощью движка Aspose OCR.  
> • Советы по настройке **установки языка OCR** для многоязычных сценариев.  
> • Обработку граничных случаев для нечитаемых изображений и отсутствующих языковых пакетов.

## Prerequisites

Перед тем как приступить, убедитесь, что у вас есть:

| Требование | Почему это важно |
|------------|------------------|
| .NET 6.0 или новее (любой современный .NET runtime) | Aspose OCR нацелен на .NET Standard 2.0+, поэтому более новые рантаймы обеспечивают лучшую производительность. |
| Visual Studio 2022 (или VS Code с C#‑расширениями) | Удобная IDE помогает быстро отлаживать процесс OCR. |
| Доступ в Интернет **один раз** для загрузки пакета Aspose OCR NuGet | После первой установки вы можете включить **офлайн‑ресурсы**, чтобы избежать дальнейших загрузок. |
| Пример JPG‑изображения (`input.jpg`), содержащего русский текст (или любой другой язык, который планируете использовать) | В руководстве используется русский пример, но вы можете заменить его на любой установленный языковой пакет. |

Если что‑то из этого вам незнакомо, не паникуйте. Установка NuGet‑пакета сводится к одной команде, а остальные шаги одинаковы для всех форматов изображений, поддерживаемых Aspose.

## Overview of the Solution

На высоком уровне процесс выглядит так:

1. **Создать** `OcrEngine` с офлайн‑ресурсами, чтобы библиотека не пыталась скачивать языковые данные во время выполнения.  
2. **Установить** нужный язык (например, русский) с помощью перечисления `OcrLanguage`.  
3. **Вызвать** `RecognizeImage` для локального JPG‑файла.  
4. **Вывести** извлечённую строку в консоль или передать её в ваш рабочий процесс.

Ниже представлена быстрая схема, иллюстрирующая поток данных:

![Extract text from image using Aspose OCR in C#](https://example.com/placeholder-image.png){.align-center alt="extract text from image using Aspose OCR in C#"}

*Диаграмма носит лишь иллюстративный характер; реальную работу выполняет код.*

## Extract Text from Image – Core Concepts

Прежде чем писать код, разберём несколько концепций, которые часто ставят разработчиков в тупик:

- **OfflineResources** — при значении `true` Aspose OCR ищет уже загруженные языковые пакеты. Это устраняет шаг «автоскачивания», который может замедлять запуск в продакшн‑средах.  
- **OcrLanguage** — перечисление, содержащее десятки идентификаторов языков (`English`, `Russian`, `Japanese`, …). Выбор правильного языка значительно повышает точность, так как движок может применять языко‑специфические эвристики.  
- **Качество изображения** — OCR работает лучше всего с изображениями с высоким контрастом и без шума. Если результаты «мутные», рассмотрите предварительную обработку (например, бинаризацию) перед передачей изображения в движок.

Понимание этих моментов поможет решить, когда **устанавливать язык OCR** вручную, а когда полагаться на автоопределение, и почему **преобразование JPG в текст** — это не просто однострочная операция.

## Step 1: Install Aspose OCR NuGet Package

Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

*Pro tip:* После первой установки добавьте `-v latest`, чтобы всегда получать новейшую стабильную сборку. Размер пакета около 15 МБ, что приемлемо для большинства настольных и серверных развертываний.

## Step 2: Convert JPG to Text – Initialize the Engine

Теперь, когда библиотека установлена, создадим `OcrEngine`, работающий в офлайн‑режиме.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine with offline resources.
        // This prevents the SDK from trying to download language data at runtime.
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            OfflineResources = true   // <-- crucial for production stability
        });

        // Step 2.2: Choose the language pack you need.
        // Here we use Russian; replace with OcrLanguage.English for English text.
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 2.3: Perform OCR on a local JPG file.
        // The file path can be absolute or relative to the executable.
        var result = ocrEngine.RecognizeImage("YOUR_DIRECTORY/input.jpg");

        // Step 2.4: Output the extracted text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(result.Text);
    }
}
```

### Почему это важно

- **Офлайн‑режим** гарантирует детерминированное время старта — никаких неожиданных сетевых запросов при развертывании на закрытом сервере.  
- **Установка языка** (`OcrLanguage.Russian`) сообщает движку использовать русский набор символов, что повышает точность распознавания с ~70 % до >95 % для чистых изображений.  
- Метод `RecognizeImage` принимает любой формат изображения, поддерживаемый Aspose (`.jpg`, `.png`, `.tiff`, …). Поэтому мы можем **читать текст из JPG** без дополнительных шагов конвертации.

## Step 3: Set OCR Language – Handling Multiple Languages

Иногда требуется обрабатывать документы, содержащие несколько языков (например, русский и английский). Aspose OCR позволяет указать массив *резервных* языков:

```csharp
// Example: Russian primary, English secondary
ocrEngine.Language = OcrLanguage.Russian;
ocrEngine.AdditionalLanguages = new[] { OcrLanguage.English };
```

Когда основной язык не распознаёт символ, движок автоматически проверяет дополнительный список. Эта техника особенно полезна для счетов, где кириллические названия компаний смешаны с английскими кодами товаров.

> **Примечание:** Языковые пакеты должны находиться в папке `Resources` вашего проекта. Если возникнет `FileNotFoundException`, скачайте недостающий пакет с портала Aspose и разместите его рядом с исполняемым файлом.

## Step 4: Read Text from JPG – Common Pitfalls & Fixes

Даже при правильном языковом пакете могут возникнуть следующие проблемы:

| Проблема | Типичный симптом | Быстрое решение |
|----------|------------------|-----------------|
| Низкий контраст | Искажённый или пустой вывод | Примените простой фильтр повышения контраста через `System.Drawing` перед OCR. |
| Повернутое изображение | Текст отображается боком | Установите `ocrEngine.ImageRotation = OcrRotation.Rotate90;` (или 180/270) перед вызовом `RecognizeImage`. |
| Большой размер файла | Медленное распознавание, высокий расход памяти | Измените размер изображения до максимум 2000 px по длинной стороне; качество OCR останется высоким. |

Ниже компактный помощник, который изменяет размер и улучшает изображение перед передачей его в движок:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

static string PreprocessAndRead(string jpgPath)
{
    // Load the original image
    using var original = new Bitmap(jpgPath);

    // Resize while preserving aspect ratio (max 2000px)
    int maxDim = 2000;
    int newWidth, newHeight;
    if (original.Width > original.Height)
    {
        newWidth = maxDim;
        newHeight = original.Height * maxDim / original.Width;
    }
    else
    {
        newHeight = maxDim;
        newWidth = original.Width * maxDim / original.Height;
    }

    using var resized = new Bitmap(original, new Size(newWidth, newHeight));

    // Optional: increase contrast (simple linear stretch)
    var contrast = new ImageAttributes();
    float[][] matrix = {
        new float[] {1.2f, 0, 0, 0, 0},
        new float[] {0, 1.2f, 0, 0, 0},
        new float[] {0, 0, 1.2f, 0, 0},
        new float[] {0, 0, 0, 1, 0},
        new float[] {0, 0, 0, 0, 1}
    };
    contrast.SetColorMatrix(new ColorMatrix(matrix));

    using var graphics = Graphics.FromImage(resized);
    graphics.DrawImage(resized, new Rectangle(0, 0, newWidth, newHeight), 0, 0, newWidth, newHeight, GraphicsUnit.Pixel, contrast);

    // Save to a temporary file (Aspose OCR works with file paths)
    string tempPath = Path.GetTempFileName() + ".jpg";
    resized.Save(tempPath, ImageFormat.Jpeg);

    // Run OCR
    var engine = new OcrEngine(new OcrEngineSettings { OfflineResources = true });
    engine.Language = OcrLanguage.Russian;
    var res = engine.RecognizeImage(tempPath);
    File.Delete(tempPath); // clean up
    return res.Text;
}
```

Теперь вы можете вызвать `Console.WriteLine(PreprocessAndRead("YOUR_DIRECTORY/input.jpg"));` и получить более чистый результат.

## Full Working Example – All Steps in One File

Ниже представлен *полный* пример программы, который можно скопировать в `Program.cs`. Он включает заметки по установке, конфигурацию языка, предобработку и обработку ошибок.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        string imagePath = "YOUR_DIRECTORY/input.jpg";

        try
        {

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}