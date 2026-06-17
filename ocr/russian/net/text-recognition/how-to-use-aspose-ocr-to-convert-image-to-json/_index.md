---
category: general
date: 2026-03-15
description: Как использовать Aspose OCR для извлечения текста из изображений и преобразования
  изображения в JSON на C#. Узнайте, как распознавать текст из PNG и быстро получать
  структурированный вывод.
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: ru
og_description: Как использовать Aspose OCR для извлечения текста из изображений и
  преобразования изображения в JSON на C#. Это руководство проведёт вас через распознавание
  текста из PNG и получение структурированного вывода.
og_title: Как использовать Aspose OCR для преобразования изображения в JSON
tags:
- Aspose
- OCR
- C#
- JSON
title: Как использовать Aspose OCR для преобразования изображения в JSON
url: /ru/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать Aspose OCR для преобразования изображения в JSON

Вопрос о том, как использовать Aspose OCR, часто возникает у разработчиков, которым нужно извлечь текст из изображений. Если вы хотите **преобразовать изображение в JSON** или **распознать текст из PNG**, это руководство поможет вам — без лишних деталей, только практическое решение от начала до конца.

В течение нескольких минут мы пройдем всё, что вам нужно: установим библиотеку, настроим движок для вывода JSON, загрузим PNG‑чек, запустим OCR и, наконец, запишем результат в файл `.json`. К концу вы сможете **извлекать текст из изображения** одним вызовом метода и поймёте, почему каждый шаг важен.

> **Pro tip:** Aspose OCR работает с широким набором форматов изображений (PNG, JPEG, BMP, TIFF). Тот же код ниже справится со всеми ними, так что вам не придётся писать логику для конкретных форматов.

## Что понадобится

- .NET 6.0 или новее (код также работает на .NET Framework 4.6+)  
- Действительный пакет Aspose.OCR NuGet (бесплатная пробная версия или лицензия)  
- Файл изображения, который вы хотите обработать (например, `receipt.png`)  
- Visual Studio, VS Code или любой другой редактор C# по вашему выбору  

И всё — без дополнительных зависимостей, без внешних сервисов. Готовы? Поехали.

![как использовать движок Aspose OCR](image-placeholder.png "как использовать движок Aspose OCR")

## Как использовать Aspose OCR – настройка вывода JSON

Первое, что нужно сделать, когда вы **how to use aspose** для OCR, — создать экземпляр `OcrEngine` и указать ему выводить JSON. Этот крошечный переключатель конфигурации избавит вас от необходимости вручную сериализовать результат позже.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**Почему это важно:** Установка `OutputFormat` в `Json` означает, что OCR‑движок уже структурирует текст в иерархию страниц, строк и слов. Вам не придётся разбирать сырые строки позже, что делает последующую обработку — например, загрузку данных в базу данных — гораздо чище.

## Преобразование изображения в JSON с помощью Aspose OCR

Теперь, когда движок настроен, давайте подробнее рассмотрим часть **convert image to JSON**.

1. **Загрузите изображение** — `Image.FromFile` работает с любым поддерживаемым форматом. Если вы работаете со стримом (например, загруженным файлом), можно использовать `Image.FromStream`.  
2. **Выполните `Recognize`** — этот метод возвращает объект `OcrResult`. Поскольку мы задали вывод в JSON, `ocrResult.Text` уже содержит строку JSON.  
3. **Запишите файл** — `File.WriteAllText` — самый простой способ сохранить JSON. Если нужно сохранить его в облачном бакете, просто замените эту строку соответствующим вызовом SDK.

### Ожидаемый JSON‑вывод

Типичный JSON‑payload выглядит так (усечён для краткости):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Теперь вы можете передать эту структуру в любую downstream‑систему — будь то инструмент отчётности, модель машинного обучения или простой файл журнала.

## Извлечение текста из изображения с помощью Aspose OCR

Если вам нужен только сырой строковый результат (т.е. JSON не требуется), просто переключите формат вывода обратно на обычный текст:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**Когда выбирать обычный текст?**  
- Быстрая отладка или вывод в консоль.  
- Сценарии, где вы будете применять собственную пост‑обработку (например, извлечение с помощью regex).  

Но помните, **extract text from image** с использованием JSON даёт вам позиционные данные — полезно для подсветки текста в UI или выравнивания с полями формы.

## Распознавание текста из PNG‑файлов

PNG — это формат без потерь, который часто обеспечивает лучшую точность OCR по сравнению с сильно сжатым JPEG. Вот быстрый чек‑лист, чтобы гарантировать наилучший результат при **recognize text from PNG**:

| Пункт чек‑листа | Почему это помогает |
|-----------------|----------------------|
| Использовать DPI 300+ | Более высокое разрешение даёт движку больше пикселей для работы. |
| Оставить изображение в градациях серого | Снижает шум; Aspose OCR автоматически конвертирует, но предварительная обработка ускорит процесс. |
| Удалить фоновой шум | Чистый фон повышает коэффициенты уверенности. |

Если вы получаете низкие коэффициенты уверенности, попробуйте увеличить DPI или применить простой пороговый фильтр перед передачей изображения в Aspose.

## Как программно извлекать результаты OCR

Помимо простого сохранения JSON, вы можете программно читать конкретные поля — например, общую сумму на чеке. Поскольку JSON содержит иерархию, его можно десериализовать в объект C#:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

Теперь вы можете выполнять запросы к `ocrData` с помощью LINQ:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**Почему это работает:** JSON уже указывает, где каждое слово находится на странице, поэтому вы надёжно находите поля даже при небольших изменениях макета.

## Пограничные случаи и распространённые подводные камни

- **Null Result:** Если `ocrEngine.Recognize` возвращает `null`, изображение может быть неподдерживаемым или повреждённым. Всегда проверяйте это:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **Большие файлы:** Для изображений размером в несколько мегабайт рассмотрите возможность потоковой передачи изображения или его уменьшения перед OCR, чтобы избежать избыточного использования памяти.

- **Проблемы с лицензией:** Пробная версия добавляет водяной знак к результату. Убедитесь, что загрузили лицензию в начале программы:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Нелатинские скрипты:** Aspose OCR поддерживает множество языков, но вам нужно установить свойство `Language` соответствующим образом (например, `ocrEngine.Configuration.Language = Language.English;`).

## Полный рабочий пример (готовый к копированию)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}