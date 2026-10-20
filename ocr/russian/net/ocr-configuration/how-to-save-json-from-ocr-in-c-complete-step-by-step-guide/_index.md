---
category: general
date: 2026-03-02
description: Узнайте, как сохранять JSON при извлечении текста из изображения с помощью
  Aspose OCR. Включает код записи JSON‑файла, советы по загрузке bitmap‑изображения
  и полный пример на C#.
draft: false
keywords:
- how to save json
- extract text from image
- write json file
- how to extract text
- load bitmap image
language: ru
og_description: Узнайте, как сохранять JSON при извлечении текста из изображения с
  помощью Aspose OCR. Полный код на C#, шаги записи JSON‑файла и практические советы.
og_title: Как сохранить JSON из OCR в C# — полный учебник по программированию
tags:
- C#
- OCR
- Aspose
- JSON
title: Как сохранить JSON из OCR в C# — Полное пошаговое руководство
url: /ru/net/ocr-configuration/how-to-save-json-from-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как сохранить JSON из OCR в C# – Полное пошаговое руководство

Когда‑нибудь задумывались **как сохранить JSON**, содержащий текст, который вы только что извлекли из изображения? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужно *извлечь текст из изображения* и затем сохранить эту информацию в аккуратно отформатированном файле JSON. Хорошая новость? Решение довольно простое, как только у вас есть все необходимые компоненты.

В этом руководстве мы пройдем реальный сценарий: используя Aspose.OCR для **извлечения текста из изображения**, затем **записи JSON‑файла**, и, наконец, **как сохранить JSON** на диск. По пути мы также покажем, как правильно **загружать bitmap‑изображения**, и рассмотрим несколько возможных проблем. К концу у вас будет автономное консольное приложение C#, которое делает всё — от загрузки изображения до создания готового JSON‑документа.

## Что понадобится

- .NET 6.0 или новее (код работает и с .NET Core, и с .NET Framework)
- Aspose.OCR for .NET (можно взять бесплатный пробный пакет NuGet)
- Пример изображения PNG или JPG, содержащего английский текст
- Visual Studio, VS Code или любой IDE, совместимый с C#

Дополнительные библиотеки не требуются — только стандартное пространство имён `System.Drawing` для работы с bitmap и `System.Text.Json` для сериализации.

---

## Шаг 1 – Загрузка Bitmap‑изображения (часть «load bitmap image»)

Прежде чем можно будет выполнить OCR, необходимо загрузить изображение в память как `Bitmap`. Представьте это как открытие книги перед тем, как начать читать её страницы.

```csharp
using System.Drawing;

// Replace the placeholder with the actual path to your image file
string imagePath = @"C:\Images\sample-page.png";

// Load the image – this is the “load bitmap image” step
Bitmap bitmapImage = new Bitmap(imagePath);
```

> **Совет:** Если изображение большое, рассмотрите возможность предварительного изменения его размера для повышения производительности. OCR‑движок работает быстрее с изображениями размером менее 2 МБ.

---

## Шаг 2 – Настройка Aspose OCR Engine

Теперь, когда bitmap готов, нам нужен `OcrEngine`. Этот объект умеет **извлекать текст из изображения** и при необходимости предоставлять геометрические данные, такие как ограничивающие рамки.

```csharp
using Aspose.OCR;

// Create the OCR engine with English language and enable bounding boxes
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    ExportBoundingBoxes = true // adds geometry info to the result
};
```

Зачем включать `ExportBoundingBoxes`? Если вам когда‑нибудь понадобится подсвечивать слова в пользовательском интерфейсе, эти координаты бесценны. Если они не нужны, можно установить флаг в `false`, и JSON будет немного компактнее.

---

## Шаг 3 – Выполнение OCR и получение структурированного результата

После настройки движка следующий шаг — реальная операция **как извлечь текст**. Метод `RecognizeToOcrResult` возвращает богатый объект, содержащий распознанный текст, оценки уверенности и необязательные данные о макете.

```csharp
// Run OCR – this is the core “how to extract text” call
var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);
```

Переменная `ocrResult` теперь содержит всё необходимое. Если посмотреть её в отладчике, вы увидите иерархию объектов `Page`, `Paragraph`, `Line` и `Word`, каждый из которых имеет собственное свойство `Text`.

---

## Шаг 4 – Сериализация результата в отформатированную строку JSON

Здесь начинается настоящая магия **how to save json**. Мы будем использовать `System.Text.Json`, потому что он встроен, быстрый и поддерживает красивый вывод «из коробки».

```csharp
using System.Text.Json;

// Serialize with indentation for readability
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

Если нужен другой стиль именования (например, camelCase), просто добавьте `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` в параметры.

---

## Шаг 5 – Запись JSON на диск (шаг «write json file»)

Наконец, мы действительно **записываем JSON‑файл** в файловую систему. Это конкретный ответ на вопрос **how to save json** в среде C#.

```csharp
using System.IO;

// Choose where you want the JSON output
string jsonPath = @"C:\Images\sample-page.json";

// Save the JSON string – this completes the “how to save json” workflow
File.WriteAllText(jsonPath, jsonResult);
```

После выполнения этой строки вы найдете аккуратно отформатированный `sample-page.json` рядом с оригинальным изображением. Откройте его в любом текстовом редакторе или передайте в другой сервис — ваши OCR‑данные теперь портативны.

---

## Шаг 6 – Проверка вывода (Что вы должны увидеть?)

Запуск программы должен вывести короткое подтверждение в консоль:

```csharp
Console.WriteLine("OCR result saved as JSON.");
```

Откройте сгенерированный JSON‑файл, и вы увидите примерно следующее:

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello, world!",
          "Words": [
            { "Text": "Hello,", "Confidence": 0.99 },
            { "Text": "world!", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Если флаг `ExportBoundingBoxes` был установлен в true, каждое слово также будет содержать координаты `Rectangle`. Это удобно для дальнейшей работы с UI.

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если путь к изображению недействителен?

Оберните загрузку bitmap в блок `try/catch` и выдайте понятную ошибку:

```csharp
try
{
    Bitmap bitmapImage = new Bitmap(imagePath);
}
catch (FileNotFoundException)
{
    Console.Error.WriteLine($"Image not found: {imagePath}");
    return;
}
```

### Как обрабатывать неанглийские языки?

Просто измените свойство `Language`:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Aspose поддерживает более 50 языков, так что выберите тот, который соответствует вашему исходному материалу.

### Нужно ли освобождать объекты `Bitmap`?

Да. `Bitmap` реализует `IDisposable`, поэтому оберните его в оператор `using`, чтобы своевременно освободить нативные ресурсы.

```csharp
using (Bitmap bitmapImage = new Bitmap(imagePath))
{
    // OCR code here
}
```

### Как получить компактный JSON без отступов?

Замените `JsonSerializerOptions`:

```csharp
new JsonSerializerOptions { WriteIndented = false }
```

Это уменьшит размер файла — полезно в сценариях с ограниченной пропускной способностью.

---

## Полный рабочий пример (готовый к копированию и вставке)

Ниже представлен полный код программы, включающий все шаги, обработку ошибок и рекомендации по лучшим практикам, обсуждённые выше. Сохраните его как `Program.cs` и запустите из командной строки или вашей IDE.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1 – Load the bitmap image (load bitmap image)
        // -------------------------------------------------
        string imagePath = @"C:\Images\page.png";
        string jsonPath  = @"C:\Images\page.json";

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Error: Image file not found at {imagePath}");
            return;
        }

        using Bitmap bitmapImage = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2 – Configure the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ExportBoundingBoxes = true // optional, adds geometry info
        };

        // -------------------------------------------------
        // Step 3 – Perform OCR (how to extract text)
        // -------------------------------------------------
        var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);

        // -------------------------------------------------
        // Step 4 – Serialize to JSON (how to save json)
        // -------------------------------------------------
        string jsonResult = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true }
        );

        // -------------------------------------------------
        // Step 5 – Write JSON file (write json file)
        // -------------------------------------------------
        try
        {
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"OCR result saved as JSON at {jsonPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to write JSON file: {ex.Message}");
        }
    }
}
```

**Что делает этот код:**  
1. Проверяет, существует ли изображение.  
2. Загружает его безопасно с помощью блока `using`.  
3. Выполняет OCR для **извлечения текста из изображения**.  
4. Сериализует результат в красиво отформатированную строку JSON.  
5. Сохраняет эту строку на диск, отвечая на основной вопрос **how to save json**.

Запустите `dotnet run` (или нажмите F5 в Visual Studio), и вы увидите сообщение подтверждения после записи файла.

---

## Заключение

Теперь у вас есть полный, готовый к использованию в продакшене рецепт **how to save JSON**, полученного из OCR‑извлечённого текста. От загрузки bitmap‑изображения до записи чистого JSON‑файла каждый шаг объяснён с указанием «почему», чтобы вы могли адаптировать решение под свои проекты.  

Если вам интересны дальнейшие возможности, рассмотрите:

- **Как извлекать текст** из PDF, предварительно преобразовав каждую страницу в изображение.  
- Использование данных о ограничивающих коробках для подсветки слов в UI WPF или WinForms.  
- Потоковая передача JSON напрямую в веб‑API вместо записи в файл (используйте `HttpClient`).

Попробуйте, настройте параметры и позвольте OCR‑данным подпитывать любое приложение, которое вы создаёте. Есть вопросы? Оставьте комментарий, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}