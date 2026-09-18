---
category: general
date: 2026-02-09
description: Узнайте, как выполнять OCR в C# для извлечения текста из изображения,
  распознавания текста из PNG и быстрого создания JSON‑файла.
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: ru
og_description: Как выполнить OCR в C#? Следуйте этому пошаговому руководству, чтобы
  извлечь текст из изображения, распознать текст из PNG и эффективно записать JSON‑файл
  в C#.
og_title: Как выполнить OCR в C# — извлечь текст и записать JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: Как выполнить OCR в C# – извлечь текст и записать JSON
url: /ru/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить OCR в C# – Полное руководство

Как выполнить OCR в C# — это распространённая задача, когда нужно **извлечь текст из изображения**. В этом руководстве мы пройдём процесс распознавания текста из PNG, экспортируем подробный результат в строку JSON и, наконец, **запишем JSON‑файл C#**. Когда вы смотрите на отсканированную форму и задаётесь вопросом, как превратить эти каракули в поисковый текст, вы не одиноки; многие разработчики сталкиваются с этой проблемой в начале пути.

Мы будем использовать библиотеку Aspose.OCR, потому что она сразу предоставляет уверенность (confidence) для каждого символа и отлично работает с проектами .NET 6+. К концу этого урока у вас будет готовое консольное приложение, которое загружает PNG, извлекает каждый символ и сохраняет аккуратный JSON‑файл, который можно загрузить в базу данных или модель ИИ. Никаких «см. документацию» ухищрений — только автономное решение.

## Что вам понадобится

- **.NET 6 SDK** (или новее) — текущая LTS‑версия на момент написания.
- **Aspose.OCR for .NET** пакет NuGet — `Install-Package Aspose.OCR`.
- PNG‑изображение, которое вы хотите просканировать (например, `form.png`).  
- IDE или редактор — Visual Studio, VS Code, Rider — любой, с которым вам удобно работать.

Это всё. Если у вас есть эти компоненты, можно начинать.

![How to perform OCR example](ocr-example.png "How to perform OCR in C#")

*Текст альтернативного изображения: иллюстрация «как выполнить OCR», показывающая консольное приложение C# при обработке PNG.*

## Шаг 1: Создайте проект и добавьте зависимости

Сначала создайте новый консольный проект и подключите библиотеку Aspose OCR.

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **Pro tip:** Используйте флаг `--framework net6.0`, если хотите явно зафиксировать целевую платформу.

Почему этот шаг важен: пакет NuGet содержит классы `OcrEngine`, `ImageStream` и `JsonExporter`, на которые мы будем опираться. Без него компилятор не будет знать, что такое «OCR».

## Шаг 2: Напишите основную логику OCR

Откройте `Program.cs` (или создайте новый файл) и замените его содержимое следующим кодом. Каждый раздел прокомментирован, чтобы вы понимали его назначение.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### Почему каждый элемент важен

- **OcrEngine**: По сути, мозг операции. Загружает языковые модели и настраивает конвейер вывода.
- **ImageStream.FromFile**: Работает с PNG, JPEG, BMP и т.д. Абстрагирует особенности ввода‑вывода файлов.
- **RecognitionResult**: Содержит необработанный текст и оценки уверенности. Здесь вы получаете детальные данные, необходимые для последующей валидации.
- **JsonExporter**: Преобразует богатый `RecognitionResult` в чистый JSON‑payload, идеальный для API.
- **File.WriteAllText**: Прямой способ в .NET **записать JSON‑файл C#** без дополнительных зависимостей.

## Шаг 3: Запустите приложение и проверьте вывод

Скомпилируйте и выполните программу:

```bash
dotnet run
```

Вы должны увидеть сообщение в консоли, похожее на:

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

Откройте `form.json` — вы увидите что‑то вроде:

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

Шаг **извлечь текст из изображения** выполнен успешно, и теперь у вас есть машинно‑читаемое JSON‑представление каждого символа.

## Шаг 4: Обработка распространённых граничных случаев

### Отсутствующие или повреждённые файлы

Если путь к PNG неверен, `ImageStream.FromFile` бросит `FileNotFoundException`. Оберните код загрузки в блок try‑catch:

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### Низкие оценки уверенности

Иногда OCR выдаёт низкую уверенность для шумных сканов. Вы можете отфильтровать символы перед экспортом:

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

Это гарантирует, что JSON будет содержать только достаточно надёжные символы — полезно, когда данные передаются в последующие валидационные конвейеры.

### Большие файлы и память

Обработка многомегабайтного PNG может резко увеличить использование памяти. Рассмотрите возможность потоковой передачи изображения частями или используйте `OcrEngine.RecognizeAsync` (доступно в более новых версиях Aspose), чтобы UI оставался отзывчивым.

## Шаг 5: Расширьте решение (по желанию)

- **Пакетная обработка**: Пройдитесь по каталогу PNG‑файлов и создайте соответствующий JSON для каждого.
- **Хранение в базе данных**: Вставьте JSON в столбец SQL `NVARCHAR(MAX)` для последующего анализа.
- **Выбор языка**: Установите `ocrEngine.Language = OcrLanguage.Spanish;`, если нужен неанглийский язык.

Все эти расширения следуют той же схеме **как выполнить OCR**, которую мы описали — инициализировать, распознать, экспортировать и сохранять.

## Часто задаваемые вопросы

**В: Работает ли это с JPG или TIFF?**  
О: Абсолютно. `ImageStream.FromFile` автоматически определяет формат, так что вы можете заменить PNG на любой поддерживаемый растровый файл.

**В: Что делать, если нужно извлечь текст из PDF?**  
О: Сначала преобразуйте каждую страницу PDF в изображение (например, с помощью `Aspose.PDF`), а затем передайте полученный PNG в OCR‑процесс, описанный выше.

**В: Можно ли получить результат OCR в виде XML вместо JSON?**  
О: Да. Aspose.OCR также поставляется с `XmlExporter`. Замените `JsonExporter` на `XmlExporter` и измените расширение файла.

## Заключение

Мы прошли весь процесс **как выполнить OCR** в C# от начала до конца, показав, как **извлечь текст из изображения**, **распознать текст из PNG** и **записать JSON‑файл C#** без проблем. Полный, готовый к запуску пример находится в кодовых фрагментах выше, и теперь вы понимаете, почему каждый шаг важен — инициализация движка, обработка граничных случаев и сохранение результатов.

Дальше вы можете исследовать пакетные OCR‑конвейеры, интегрировать JSON‑вывод с Azure Cognitive Search или поэкспериментировать с пользовательскими языковыми моделями. Возможности безграничны, как только вы освоите основы OCR в C#.

Если у вас возникли трудности или есть идеи для дальнейших улучшений, оставляйте комментарий ниже. Приятного кодинга и удачной трансформации пиксельных сканов в чистые, поисковые данные!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}