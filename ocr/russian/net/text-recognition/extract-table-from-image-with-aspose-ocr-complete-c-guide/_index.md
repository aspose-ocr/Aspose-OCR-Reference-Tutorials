---
category: general
date: 2026-03-18
description: Извлеките таблицу из изображения с помощью Aspose OCR на C#. Узнайте,
  как преобразовать таблицу в JSON, получить JSON‑таблицы и извлечь текст из изображения
  за несколько минут.
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: ru
og_description: Извлеките таблицу из изображения с помощью Aspose OCR в C#. Узнайте,
  как преобразовать таблицу в JSON, получить JSON‑таблицы и быстро извлечь текст из
  изображения.
og_title: Извлечение таблицы из изображения с помощью Aspose OCR – полное руководство
  по C#
tags:
- Aspose OCR
- C#
- Table Extraction
title: Извлечение таблицы из изображения с помощью Aspose OCR – Полное руководство
  по C#
url: /ru/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение таблицы из изображения – Полное руководство по C#  

Когда‑нибудь вам нужно было **extract table from image**, но вы не знали, какая библиотека справится с этим без горы ручного парсинга? Вы не одиноки. Во многих проектах по обработке счетов‑фактур или сканированию чеков основной проблемой является преобразование шумного битмапа в структурированную таблицу, которую может использовать ваша downstream система.  

Хорошая новость? С Aspose OCR вы можете **convert table to JSON** в несколько строк, а также получить обычный текст всего изображения, так что **extract text from image** будет бонусом. В этом руководстве мы пройдем весь процесс – от загрузки изображения до получения аккуратного JSON‑представления обнаруженной таблицы.  

> **Quick win:** К концу вы получите исполняемое консольное приложение C#, которое выводит как необработанный OCR‑текст, так и строку JSON, которую можно сразу передать в базу данных или API.  

## Требования  

Перед тем как начать, убедитесь, что у вас есть:  

- .NET 6.0 SDK (или любая современная версия .NET) установлен.  
- Действительная лицензия Aspose OCR или бесплатная пробная версия (библиотека работает без лицензии, но добавляет водяной знак).  
- Изображение, действительно содержащее таблицу – например `invoice_table.png`.  
- Visual Studio 2022, VS Code или любой другой редактор по вашему выбору.  

Дополнительные пакеты NuGet, кроме `Aspose.OCR`, не требуются.  

## Шаг 1: Настройка проекта и установка Aspose OCR  

Сначала создайте новый консольный проект и подключите библиотеку OCR.  

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Если вы используете корпоративный прокси, добавьте флаг `--no-restore` и позже выполните `dotnet restore` с правильными переменными окружения.  

## Шаг 2: Инициализация OCR‑движка и включение распознавания таблиц  

Сердце решения – это `OcrEngine`. Переключив `EnableTableRecognition`, мы говорим Aspose OCR искать структуры, похожие на сетку, вместо того чтобы рассматривать всё как обычный текст.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;

class TableJsonDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable table detection – this is what lets us get a JSON table later
        ocrEngine.Settings.EnableTableRecognition = true;
```

Почему этот шаг критичен? Без распознавания таблиц движок «сплющит» изображение в одну строку, что делает невозможным последующее восстановление строк и столбцов. Включение этой опции добавляет лёгкую фазу анализа макета, которая почти не влияет на производительность, но даёт огромные преимущества downstream.  

## Шаг 3: Загрузка изображения и запуск распознавания  

Теперь указываем движку файл, содержащий таблицу. `ImageStream.FromFile` поддерживает большинство популярных форматов (PNG, JPEG, TIFF).  

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

Если изображение большое, рассмотрите возможность его предварительного изменения размера для ускорения обработки. Aspose OCR автоматически определяет DPI, но сканирование с 300 DPI обычно является оптимальным для большинства таблиц.  

## Шаг 4: Извлечение обычного текста – “extract text from image”  

Хотя нашей основной целью является таблица, часто всё равно нужен сырой текст для логирования или резервной обработки.  

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

Свойство `Text` конкатенирует всё, что видит движок, сохраняя разрывы строк. Это удобно, когда нужно проверить, правильно ли OCR прочитал заголовки или нижние колонтитулы за пределами области таблицы.  

## Шаг 5: Получение обнаруженной таблицы в виде JSON – “convert table to json” & “get table json”  

Здесь происходит магия. `GetTableAsJson()` сериализует обнаруженные строки, столбцы и содержимое ячеек в чистую строку JSON.  

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

Полученный JSON выглядит примерно так (отформатировано для удобства чтения):  

```json
{
  "Rows": [
    {
      "Cells": [
        { "Text": "Item", "ColumnIndex": 0 },
        { "Text": "Quantity", "ColumnIndex": 1 },
        { "Text": "Price", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget A", "ColumnIndex": 0 },
        { "Text": "10", "ColumnIndex": 1 },
        { "Text": "$5.00", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget B", "ColumnIndex": 0 },
        { "Text": "7", "ColumnIndex": 1 },
        { "Text": "$8.50", "ColumnIndex": 2 }
      ]
    }
  ]
}
```

Почему JSON предпочтителен? Он независим от языка, легко десериализуется в объекты и отлично работает с современными веб‑API. Если нужен CSV, просто пройдитесь по строкам и соедините тексты ячеек запятыми.  

## Шаг 6: (Опционально) Преобразование JSON в объект .NET – “convert image to json”  

Если вы предпочитаете работать с сильными типами, десериализуйте JSON с помощью `System.Text.Json`.  

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

Вы определите `TableModel`, `RowModel` и `CellModel` в соответствии со схемой JSON. Этот шаг показывает, как перейти от **convert image to json** к типизированному объекту, делая downstream‑валидацию простой.  

## Полный рабочий пример  

Объединив всё вместе, получаем полностью готовую к запуску программу. Сохраните её как `Program.cs` в папке проекта, созданной ранее.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;
using System.Text.Json;

class TableJsonDemo
{
    static void Main()
    {
        // Step 1: Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable table recognition
        ocrEngine.Settings.EnableTableRecognition = true;

        // Step 3: Load image containing a table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Step 4: Run OCR
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Print full text (extract text from image)
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);

        // Step 6: Get table as JSON (convert table to json, get table json)
        string tableJson = ocrResult.GetTableAsJson();
        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);

        // Optional: Deserialize JSON to C# objects (convert image to json)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
    }
}

// Helper classes matching Aspose's JSON structure
public class TableModel
{
    public RowModel[] Rows { get; set; }
}
public class RowModel
{
    public CellModel[] Cells { get; set; }
}
public class CellModel
{
    public string Text { get; set; }
    public int ColumnIndex { get; set; }
}
```

### Ожидаемый вывод  

При запуске `dotnet run` вы должны увидеть нечто подобное:  

```
Full text:
Item Quantity Price
Widget A 10 $5.00
Widget B 7 $8.50

Detected table (JSON):
{
  "Rows":[
    {"Cells":[{"Text":"Item","ColumnIndex":0},{"Text":"Quantity","ColumnIndex":1},{"Text":"Price","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget A","ColumnIndex":0},{"Text":"10","ColumnIndex":1},{"Text":"$5.00","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget B","ColumnIndex":0},{"Text":"7","ColumnIndex":1},{"Text":"$8.50","ColumnIndex":2}]}
  ]
}

First cell value: Item
```

Если вывод пустой, проверьте, что `EnableTableRecognition` установлен в `true`, и что изображение действительно содержит чёткие линии сетки.  

## Частые ошибки и как их избежать  

| Проблема | Почему происходит | Как исправить |
|----------|-------------------|---------------|
| **No JSON returned** | Обнаружение таблицы отключено или изображение имеет слишком низкий контраст. | Убедитесь, что `ocrEngine.Settings.EnableTableRecognition = true`, и улучшите качество изображения (увеличьте контраст, бинаризуйте). |
| **Partial rows** | OCR запутался из‑за объединённых ячеек или повернутого текста. | Предобработайте изображение: исправьте наклон (`ImageProcessor.Rotate`) или вручную разделите объединённые ячейки. |
| **Unicode gibberish** | Шрифт не распознан (например, рукописный). | Переключите языковые пакеты через `ocrEngine.Language = Language.English;` или используйте другой OCR‑движок для рукописного текста. |
| **Performance slowdown** | Очень большое изображение (>5 МП). | Уменьшите размер до ширины ~1500 px, сохраняя DPI. |

## Следующие шаги: выход за рамки базового  

Теперь, когда вы умеете **extract table from image** и **convert table to JSON**, рассмотрите следующие расширения:  

- **Persist the JSON** в базу данных с помощью Entity Framework.  
- **Post‑process** JSON для нормализации форматов валют (например, удалить `$`).  
- **Batch process** папку со счетами, используя `Directory.GetFiles` и параллелизацию через `Parallel.ForEach`.  
- **Integrate** с Azure Functions или AWS Lambda для безсерверных OCR‑конвейеров.  

Каждая из этих тем естественно включает вторичные ключевые слова, такие как **convert image to json** (когда вы отправляете весь результат OCR в облачный endpoint) и **get table json** для downstream‑аналитики.  

### Заключение  

Мы только что продемонстрировали, как **extract table from image** с помощью Aspose OCR, преобразовать эту таблицу в чистый JSON и даже десериализовать его в объекты C#. Та же схема  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}