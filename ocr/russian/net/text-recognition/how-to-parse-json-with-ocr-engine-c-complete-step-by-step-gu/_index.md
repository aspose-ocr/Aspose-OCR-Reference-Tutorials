---
category: general
date: 2026-03-17
description: Узнайте, как разбирать JSON из результатов OCR в C#. В этом руководстве
  рассматривается, как извлекать текст, загружать изображение для OCR, запускать распознавание
  OCR и эффективно использовать OCR‑движок в C#.
draft: false
keywords:
- how to parse json
- how to extract text
- load image for OCR
- run OCR recognition
- use OCR engine C#
language: ru
og_description: Как разобрать JSON из вывода OCR в C#. Следуйте нашему руководству,
  чтобы извлечь текст, загрузить изображение для OCR, выполнить распознавание OCR
  и использовать OCR‑движок в C#.
og_title: Как парсить JSON с помощью OCR Engine C# – Полный учебник
tags:
- C#
- OCR
- JSON
- Image Processing
title: Как разобрать JSON с помощью OCR Engine C# – Полное пошаговое руководство
url: /ru/net/text-recognition/how-to-parse-json-with-ocr-engine-c-complete-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как разобрать JSON с помощью OCR Engine C# – Полное пошаговое руководство

Когда‑нибудь задумывались **how to parse json**, получаемый напрямую из OCR‑движка? Вы не одиноки. Большинство разработчиков сталкиваются с одной и той же проблемой — получают «сырой» JSON и пытаются понять, как лучше извлечь полезные данные, такие как оценки уверенности или сам текст. В этом руководстве мы пройдем процесс загрузки изображения для OCR, запуска распознавания и, наконец, **how to parse json** в чистом, поддерживаемом виде.

К концу урока вы сможете:

* Загрузить изображение для OCR всего в несколько строк кода.  
* Запустить распознавание OCR, используя C# OCR‑движок.  
* **How to extract text** и другие метаданные из JSON‑получения.  
* Обрабатывать распространённые граничные случаи (отсутствующие поля, неожиданные форматы) без сбоев.

Никакой внешней документации не требуется — всё, что нужно, находится здесь.

## Требования

Прежде чем погрузиться в детали, убедитесь, что у вас есть:

* .NET 6.0 или новее (код также компилируется на .NET Framework 4.7+).  
* Ссылка на используемую OCR‑библиотеку (в примере используется гипотетический класс `OcrEngine`).  
* Пакет NuGet `Newtonsoft.Json` для работы с JSON (`Install-Package Newtonsoft.Json`).  
* Файл изображения (например, `passport.png`), расположенный там, где приложение может его прочитать.

> **Pro tip:** Если вы используете коммерческий OCR‑SDK, проверьте, что формат вывода JSON включён — большинство поставщиков позволяют это через конфигурационное свойство, например `ocrEngine.Config.OutputFormat`.

## Шаг 1 – Создание и настройка OCR‑движка (Primary Keyword in Action)

Первое, что нужно сделать, — создать экземпляр OCR‑движка и указать, что он должен возвращать JSON. Именно здесь в коде впервые появляется фраза **how to parse json**, потому что движок отдаст нам строку JSON, которую мы позже разберём.

```csharp
using System;
using Newtonsoft.Json.Linq;   // For JSON parsing
// Assume OcrEngine, OutputFormat, and ImageStream live in the OCR SDK namespace
using OcrSdk;                  // <-- replace with the real namespace

// Step 1: Create an OCR engine instance and set JSON output
var ocrEngine = new OcrEngine();
ocrEngine.Config.OutputFormat = OutputFormat.Json;
```

**Почему это важно:** Установка `OutputFormat` в `Json` гарантирует, что ответ будет содержать как распознанный текст, **так и** полезные метаданные, такие как оценки уверенности. Если пропустить этот шаг, вы получите обычный текст, и **how to parse json** станет бессмысленным.

## Шаг 2 – Загрузка изображения для OCR

Теперь загружаем картинку, которую хотим проанализировать. Здесь как раз проявляется вторичное ключевое слово **load image for OCR**.

```csharp
// Step 2: Load the image you want to recognize
// Make sure the path points to a real file; otherwise an exception is thrown.
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\passport.png");
```

> **Что если файл отсутствует?** Оберните вызов в `try/catch` и выведите дружелюбное сообщение — приложение не упадёт, а пользователь узнает, в чём проблема.

## Шаг 3 – Запуск распознавания OCR

С готовым движком и загруженным изображением следующий логичный шаг — запустить процесс распознавания. Это реализует вторичное ключевое слово **run OCR recognition**.

```csharp
// Step 3: Execute OCR and get the raw result object
var ocrResult = ocrEngine.Recognize();
```

Свойство `ocrResult.Text` теперь содержит строку JSON. Если вывести её в консоль, вы увидите примерно следующее:

```json
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}
```

## Шаг 4 – Как извлечь текст (и другие поля) из JSON

Это сердце руководства: **how to parse json** и **how to extract text** из OCR‑payload. Мы будем использовать `Newtonsoft.Json.Linq.JObject` за его гибкость.

```csharp
// Step 4: Output the raw JSON (optional, helps debugging)
Console.WriteLine("Raw OCR JSON:");
Console.WriteLine(ocrResult.Text);
Console.WriteLine();

// Step 5: Parse the JSON into a JObject
JObject jsonObject = JObject.Parse(ocrResult.Text);

// Extract the overall confidence score
var overallConfidence = jsonObject["OverallConfidence"]?.Value<double>() ?? 0.0;
Console.WriteLine($"Overall confidence: {overallConfidence:P0}");

// Extract the text from the first page (how to extract text)
string pageText = jsonObject["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
Console.WriteLine("Extracted text:");
Console.WriteLine(pageText);
```

**Почему `JObject`?** Он позволяет безопасно перемещаться по дереву JSON без необходимости создавать полную модель C#. Операторы условного доступа (`?.`) защищают от `NullReferenceException`, если OCR‑движок вдруг опустит какое‑то поле.

### Обработка граничных случаев

* **Отсутствующие поля:** Шаблон `?.Value<T>() ?? default` возвращает разумный запасной вариант.  
* **Несколько страниц:** Пройдитесь по `jsonObject["Pages"]`, если ожидаете более одной страницы.  
* **Не числовая уверенность:** Используйте `double.TryParse`, если SDK иногда возвращает строку.

## Шаг 5 – Объединение всего в переиспользуемый метод

Чтобы не копировать один и тот же шаблон, инкапсулируйте весь процесс в вспомогательный метод. Это также демонстрирует **use OCR engine C#** в чистом, переиспользуемом виде.

```csharp
public static void RunOcrAndParseJson(string imagePath)
{
    // 1️⃣ Create engine & set JSON output
    var engine = new OcrEngine();
    engine.Config.OutputFormat = OutputFormat.Json;

    // 2️⃣ Load image (load image for OCR)
    engine.Image = ImageStream.FromFile(imagePath);

    // 3️⃣ Run OCR (run OCR recognition)
    var result = engine.Recognize();

    // 4️⃣ Show raw JSON (optional)
    Console.WriteLine("=== Raw JSON ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();

    // 5️⃣ Parse JSON (how to parse json)
    JObject obj = JObject.Parse(result.Text);

    // 6️⃣ Extract useful data (how to extract text)
    double confidence = obj["OverallConfidence"]?.Value<double>() ?? 0.0;
    string text = obj["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;

    Console.WriteLine($"Overall confidence: {confidence:P0}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(text);
}
```

Теперь вы можете вызвать `RunOcrAndParseJson(@"C:\Images\passport.png");` из `Main` или любой другой части вашего приложения.

## Полный рабочий пример

Ниже представлена полностью автономная консольная программа, которую можно скопировать в новый `.csproj`. В ней собраны все обсуждённые части, плюс небольшая обработка ошибок.

```csharp
// File: Program.cs
using System;
using Newtonsoft.Json.Linq;
using OcrSdk;               // Replace with the actual namespace of your OCR library

class Program
{
    static void Main()
    {
        try
        {
            // Adjust the path to point at a real image on your machine
            string imagePath = @"YOUR_DIRECTORY\passport.png";

            RunOcrAndParseJson(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Unexpected error: {ex.Message}");
        }
    }

    /// <summary>
    /// Demonstrates how to parse JSON returned by an OCR engine,
    /// and how to extract text, confidence, and other metadata.
    /// </summary>
    /// <param name="imagePath">Full path to the image file.</param>
    public static void RunOcrAndParseJson(string imagePath)
    {
        // 1️⃣ Initialize OCR engine (use OCR engine C#)
        var engine = new OcrEngine();
        engine.Config.OutputFormat = OutputFormat.Json;

        // 2️⃣ Load image for OCR
        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Run OCR recognition
        var result = engine.Recognize();

        // 4️⃣ Print raw JSON (helps debugging)
        Console.WriteLine("=== Raw OCR JSON ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // 5️⃣ Parse JSON (how to parse json)
        JObject json = JObject.Parse(result.Text);

        // 6️⃣ Extract overall confidence
        double overallConf = json["OverallConfidence"]?.Value<double>() ?? 0.0;
        Console.WriteLine($"Overall confidence: {overallConf:P0}");

        // 7️⃣ Extract text from first page (how to extract text)
        string firstPageText = json["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(firstPageText);
    }
}
```

**Ожидаемый вывод** (при успешном распознавании OCR):

```
=== Raw OCR JSON ===
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}

Overall confidence: 92%
=== Extracted Text ===
John Doe
Passport No: 123456789
```

Если изображение не удаётся прочитать, SDK бросит исключение, которое мы перехватываем в `Main`, выводя дружелюбную ошибку вместо падения программы.

## Часто задаваемые вопросы (FAQ)

**В: Что делать, если OCR‑движок возвращает массив страниц?**  
О: Пройдитесь по `json["Pages"]` и конкатенируйте каждое значение `["Text"]`, либо обрабатывайте их по отдельности в зависимости от задачи.

**В: Можно ли десериализовать JSON в типизированный класс C#?**  
О: Конечно. Определите структуру классов, соответствующую схеме JSON, и используйте `JsonConvert.DeserializeObject<YourRootClass>(result.Text)`. Это даёт проверку на этапе компиляции, но требует поддерживать модель в актуальном состоянии с выводом SDK.

**В: Работает ли это с асинхронными OCR‑API?**  
О: Да. Замените `engine.Recognize()` на `await engine.RecognizeAsync()` и сделайте `RunOcrAndParseJson` `async Task`. Часть парсинга JSON остаётся без изменений.

**В: Как сохранить JSON в файл для последующего анализа?**  
О: После получения `result.Text` вызовите `File.WriteAllText(@"output.json", result.Text);`. Затем можно загрузить его обратно через `JObject.Parse(File.ReadAllText(...))`.

## Далее

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}