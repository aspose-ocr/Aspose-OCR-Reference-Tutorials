---
category: general
date: 2026-01-12
description: c# OCR‑урок, показывающий, как распознавать текст на изображении, извлекать
  текст из изображения в C# и генерировать файл OCR из изображения в PDF с оценками
  уверенности.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: ru
og_description: Изучите полный учебник по OCR на C#, чтобы распознавать текст на изображениях,
  извлекать текст из изображений на C# и создавать PDF‑документы OCR из изображений
  с указанием уровня уверенности.
og_title: c# OCR учебник – Преобразование изображений в PDF с возможностью поиска
tags:
- OCR
- C#
- PDF
title: c# OCR учебник – Превратите изображения в поисковые PDF
url: /ru/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Преобразование изображений в поисковые PDF

Задумывались ли вы когда‑нибудь, как **распознавать текст на изображениях** в проекте C# без поиска сторонних сервисов? Вы не одиноки. Во многих реальных приложениях — например, сканерах счетов, трекерах чеков или многоязычных архивов документов — разработчикам нужен надёжный OCR‑движок, работающий локально и выдающий оценки уверенности.  

Этот **c# ocr tutorial** проведёт вас через всё необходимое: от загрузки изображения, выбора языковых моделей, включения ускорения GPU до сохранения результата в виде поискового PDF. К концу у вас будет готовый к запуску пример кода, который извлекает текст, сообщает уверенность OCR и при желании создаёт файл *image to pdf ocr* — всё за минуту кодинга.

## Что вы построите

- Загрузить многоязычное изображение (`sample_multi_lang.jpg` используется как пример).  
- Выбрать языковые модели арабского, хинди и русского (можно добавить другие).  
- Включить обработку на GPU, если ваш компьютер поддерживает её.  
- Получить необработанный результат OCR **с оценками уверенности**.  
- Сериализовать результат в красиво отформатированный JSON **или** записать поисковый PDF.  

Без внешних веб‑сервисов, без скрытой магии — только Aspose.OCR для .NET, несколько строк C# и чёткое объяснение **почему** каждая строка важна.

## Требования

- .NET 6.0 или новее (код компилируется на .NET Core и .NET Framework).  
- Visual Studio 2022 (или любая другая IDE).  
- Лицензия Aspose.OCR для .NET (бесплатная пробная версия подходит для тестирования).  
- Опционально: GPU, совместимый с CUDA, если хотите ускорить распознавание.  

> **Pro tip:** Если у вас нет GPU, просто установите `UseGpu = false` и движок переключится на CPU без каких‑либо изменений кода.

## Шаг 1: Установите необходимые пакеты NuGet

Откройте **Package Manager Console** и выполните:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

Эти три пакета предоставляют OCR‑движок, ускорение GPU и удобный JSON‑сериализатор для вывода оценок уверенности.

## Шаг 2: Настройте структуру проекта

Создайте новый консольный проект (`dotnet new console -n AsposeOcrDemo`) и замените сгенерированный `Program.cs` кодом ниже.  
Вся логика находится внутри класса `Program`; единственный дополнительный тип — небольшая extension‑метод, который форматирует результат OCR в JSON.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### Почему этот код работает

1. **GPU toggle** – `GpuOcrEngine` использует CUDA‑ядра; тернарный оператор делает переключение простым.  
2. **Automatic language download** – `AutoDownloadResources = true` гарантирует, что модели арабского, хинди и русского будут загружены при первом запуске приложения.  
3. **Confidence scores** – `result.Words` содержит `Confidence` для каждого распознанного слова; extension‑метод форматирует их в чистый JSON‑объект.  
4. **Searchable PDF** – `result.Pdf` уже полностью поисковый PDF, поэтому мы просто записываем массив байтов на диск. Дополнительные библиотеки не требуются.  

## Шаг 6: Запустите пример

Откройте терминал, перейдите в папку проекта и выполните:

```bash
dotnet run
```

Если вы выбрали вывод **JSON**, вы увидите что‑то вроде:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

Если вы переключились на **PDF**, консоль выведет путь, и вы найдете поисковый PDF рядом с исходным изображением.

## Часто задаваемые вопросы и особые случаи

- **Что делать, если языковая модель недоступна?**  
  OCR‑движок бросает понятное исключение `ResourceNotFoundException`. Поскольку мы установили `AutoDownloadResources = true`, отсутствующая модель загружается автоматически при первом запуске, поэтому исключение редко появляется в продакшене.

- **Могу ли я обрабатывать пакет изображений?**  
  Конечно. Оберните вызов `engine.Recognize` в цикл `foreach` по директории файлов. Тот же `OcrResultExtensions` работает для каждого изображения.

- **Нужна ли лицензия для GPU?**  
  Нет. Бесплатная пробная версия работает как на CPU, так и на GPU. Полная лицензия убирает водяной знак пробной версии и снимает ограничения по количеству страниц.

- **Насколько точны оценки уверенности?**  
  Оценки варьируются от 0.0 (нет уверенности) до 1.0 (полная уверенность). На практике всё выше 0.90 считается надёжным для последующей обработки; при необходимости можно отфильтровать слова с более низкой уверенностью.

## Шаг 7: Следующие шаги (расширьте ваш OCR‑инструментарий)

1. **Add more languages** – просто добавьте `LanguageModel.French` (или любую поддерживаемую модель) в массив `Languages`.  
2. **Combine OCR with PDF/A conversion** – Aspose.PDF может встроить слой OCR в документ, соответствующий PDF/A‑2b, для архивирования.  
3. **Integrate with Azure Functions** – оберните логику в безсерверный endpoint для обработки загрузок в реальном времени.  
4. **Fine‑tune confidence thresholds** – используйте `result.Words.Where(w => w.Confidence < 0.85)`, чтобы пометить сомнительные слова для ручного обзора.  

### TL;DR

Этот **c# ocr tutorial** показывает, как:

- Загрузить изображение и выбрать несколько языковых моделей.  
- Включить ускорение GPU одним логическим флагом.  
- Получить результаты OCR **с оценками уверенности** и сериализовать их в JSON.  
- При желании записать поисковый PDF (**image to pdf ocr**).  

Всё это возможно с помощью всего нескольких строк кода, бесплатной пробной версии Aspose.OCR и приведённого выше кода. Попробуйте, измените список языков, и у вас будет готовый к продакшену OCR‑конвейер за считанные минуты.

![c# ocr tutorial example image](https://example.com/placeholder-image.jpg "c# ocr tutorial example image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}