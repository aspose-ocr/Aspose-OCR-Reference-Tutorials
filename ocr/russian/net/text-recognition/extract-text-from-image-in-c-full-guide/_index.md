---
category: general
date: 2026-03-23
description: Извлеките текст из изображения с помощью Aspose OCR в C# и узнайте, как
  добавить консольный логгер для обратной связи в реальном времени.
draft: false
keywords:
- extract text from image
- add console logger
language: ru
og_description: Извлеките текст из изображения с помощью Aspose OCR и добавьте консольный
  логгер для мониторинга процесса. Пошаговое руководство на C#.
og_title: Извлечение текста из изображения в C# – Полное руководство по программированию
tags:
- OCR
- C#
- logging
title: Извлечение текста из изображения в C# – Полное руководство
url: /ru/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения в C# – Полное руководство

Нужно **извлечь текст из изображения** быстро и надёжно? С Aspose OCR вы можете сделать именно это в несколько строк кода C#.  
Мы также покажем, как **добавить консольный логгер**, чтобы вы могли наблюдать за процессом работы OCR‑движка прямо в терминале.

Представьте, что у вас есть отсканированный чек, рукописная записка или страница PDF, сохранённая как PNG. Вы хотите получить сырые символы без открытия громоздкого UI. Это руководство проведёт вас через готовое решение «копировать‑вставить», которое работает сегодня с .NET 6+ и последней библиотекой Aspose OCR.

К концу этого руководства вы сможете:

* Загрузить файл изображения и запустить OCR для **извлечения текста из изображения**.  
* Подключить консольный логгер к Aspose AI, чтобы видеть, что делает библиотека «за кулисами».  
* Применить встроенный пост‑процессор проверки орфографии для исправления ошибок OCR.  

> **Prerequisites** – Рабочая среда разработки .NET (Visual Studio 2022, VS Code или Rider), .NET 6 SDK или новее и лицензия Aspose OCR (или бесплатная пробная версия). Другие сторонние пакеты не требуются.

---

## Что вам понадобится

| Пункт | Почему это важно |
|------|-------------------|
| **Aspose.OCR** NuGet‑пакет | Предоставляет класс `OcrEngine`, который непосредственно читает изображение. |
| **Aspose.OCR.AI** NuGet‑пакет | Даёт вам фреймворк пост‑процессора `AsposeAI`, включая проверку орфографии. |
| **Microsoft.Extensions.Logging** (необязательно) | Поставляет интерфейс `ILogger` для шага **add console logger**. |
| **Входное изображение** (`input.png`) | Исходный файл, из которого мы будем **extract text from image**. |

Вы можете установить пакеты через терминал:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

---

## Шаг 1 – Extract Text from Image с Aspose OCR

Первое, что мы делаем, – передаём изображение OCR‑движку. Этот блок выполняет всю тяжёлую работу и возвращает сырую строку, которая может всё ещё содержать опечатки.

```csharp
using Aspose.OCR;
using System;

class OcrDemo
{
    static string PerformOcr(string imagePath)
    {
        // Initialise the OCR engine
        using (OcrEngine ocr = new OcrEngine())
        {
            // Load the image – replace with your own path if needed
            ocr.Image = ImageStream.FromFile(imagePath);

            // Run recognition; if it fails we return an empty string
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }

            // The engine populates the Text property with the recognised characters
            string rawText = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + rawText);
            return rawText;
        }
    }
}
```

**Почему это работает:** `OcrEngine` абстрагирует все низкоуровневые операции предобработки изображения (бинаризация, коррекция наклона и т.д.). Когда `Recognize()` возвращает `true`, свойство `Text` уже содержит наиболее вероятные символы.  

> **Tip:** Если ваше изображение большое, рассмотрите возможность масштабировать его до ≤ 2000 px по самой длинной стороне перед передачей в движок. Это ускорит обработку без потери точности.

---

## Шаг 2 – Add Console Logger для получения данных в реальном времени

Теперь добавляем часть **add console logger**. Логирование — это не только отладка; оно даёт вам видимость загрузок моделей, шагов AI‑процессора и любых предупреждений, которые может выдавать библиотека.

```csharp
using Microsoft.Extensions.Logging;
using System;

public class ConsoleLogger : ILogger
{
    // Minimal ILogger implementation that writes to the console.
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool IsEnabled(LogLevel logLevel) => true;

    public void Log<TState>(LogLevel logLevel, EventId eventId,
        TState state, Exception exception, Func<TState, Exception, string> formatter)
    {
        Console.WriteLine($"[{logLevel}] {formatter(state, exception)}");
    }
}
```

Теперь вы можете подключить этот логгер к Aspose AI:

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**Что вы увидите:** Когда модель проверки орфографии автоматически загружается, в консоль будет выведена строка вроде:

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

Это преимущество **add console logger** — вы никогда не будете гадать, успешно ли завершилась фоновая операция.

---

## Шаг 3 – Настройка и регистрация пост‑процессора Spell‑Check

Aspose AI поставляется с удобным пост‑процессором проверки орфографии, который исправляет типичные ошибки OCR (например, “rec0gn1ze” → “recognize”). Мы настроим его, при желании укажем библиотеке, где хранить модель, и затем зарегистрируем.

```csharp
// Create the built‑in spell‑check processor
SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

// Optional: tell AsposeAI where to keep downloaded models
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY/Models"
};

// Register the processor with the AI engine
ai.SetPostProcessor(spellProcessor, modelConfig);
```

**Почему может понадобиться пользовательский путь:** В CI/CD‑конвейерах часто требуется кэшировать модели в известной директории, чтобы избежать повторных загрузок. Флаг `AllowAutoDownload` гарантирует, что модель будет загружена при первом запуске кода.

---

## Шаг 4 – Запуск пост‑процессора над результатом OCR

Имея OCR‑текст и готовый процессор проверки орфографии, передаём сырую строку в `AsposeAI`. Движок запускает модель, а процессор сохраняет исправленный текст внутри себя.

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

После этого вызова объект `spellProcessor` содержит коллекцию объектов `RecognitionResult`, каждый из которых имеет свойство `RecognitionText` с очищенной версией.

---

## Шаг 5 – Получение и вывод исправленного текста

Наконец, извлекаем исправленную строку из процессора и выводим её. Это момент, когда вы действительно видите выгоду от OCR и рабочего процесса **add console logger**.

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**Ожидаемый вывод** (при условии, что изображение содержит фразу “Aspose OCR demo” с несколькими ошибками OCR):

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

Обратите внимание, как логгер сообщил, что модель готова, а исправленная строка выглядит чистой.

---

## Шаг 6 – Очистка ресурсов

И `AsposeAI`, и `OcrEngine` реализуют `IDisposable`. Их освобождение освобождает нативную память и файловые дескрипторы, что особенно важно в длительно работающих сервисах.

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

---

## Полный рабочий пример

Ниже представлен весь код программы, который можно скопировать‑вставить в новый консольный проект (`dotnet new console`). Замените `"YOUR_DIRECTORY"` на реальную папку на вашем компьютере.

```csharp
using Aspose.OCR;
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;
using Microsoft.Extensions.Logging; // optional logger
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // ---------- Step 1: OCR ----------
        string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");
        if (string.IsNullOrEmpty(ocrResult)) return;

        // ---------- Step 2: Initialise AI with console logger ----------
        ILogger consoleLogger = new ConsoleLogger(); // implements ILogger
        AsposeAI ai = new AsposeAI(consoleLogger);

        // ---------- Step 3: Spell‑check processor ----------
        SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

        // ---------- Step 4: Model configuration (optional) ----------
        AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
        {
            AllowAutoDownload = true,
            DirectoryModelPath = "YOUR_DIRECTORY/Models"
        };

        // ---------- Step 5: Register and run ----------
        ai.SetPostProcessor(spellProcessor, modelConfig);
        ai.RunPostprocessor(new[] { ocrResult });

        // ---------- Step 6: Show corrected text ----------
        string correctedText = spellProcessor.GetResult()[0].RecognitionText;
        Console.WriteLine("\nCorrected OCR output:\n" + correctedText);

        // ---------- Clean up ----------
        ai.Dispose();
    }

    static string PerformOcr(string imagePath)
    {
        using (OcrEngine ocr = new OcrEngine())
        {
            ocr.Image = ImageStream.FromFile(imagePath);
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }
            string raw = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + raw);
            return raw;
        }
    }
}

// Minimal console logger implementation
public class ConsoleLogger : ILogger
{
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}