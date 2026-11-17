---
category: general
date: 2026-03-28
description: Узнайте, как извлекать таблицы из изображений с помощью Aspose OCR на
  C#. В этом руководстве рассматривается, как обнаруживать таблицы на изображении,
  загружать изображение для OCR и извлекать таблицы из PNG‑файлов.
draft: false
keywords:
- how to extract tables
- extract table from image
- detect tables in image
- load image for ocr
- extract tables from png
language: ru
og_description: Пошаговое руководство по извлечению таблиц из изображений с помощью
  Aspose OCR на C#. Включает код, объяснения и советы по обнаружению таблиц в файлах‑изображениях.
og_title: Как извлечь таблицы из изображений с помощью Aspose OCR (C#)
tags:
- Aspose OCR
- C#
- Table Extraction
title: Как извлечь таблицы из изображений с помощью Aspose OCR (C#)
url: /ru/net/image-and-drawing-recognition/how-to-extract-tables-from-images-using-aspose-ocr-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как извлечь таблицы из изображений с помощью Aspose OCR (C#)

Когда‑нибудь задумывались **как извлечь таблицы** из отсканированного счета или скриншота таблицы? Вы не одиноки. Во многих реальных проектах нам нужно превратить изображение таблицы в данные, которые можно запросить — обычно CSV или DataTable. Хорошая новость? Aspose OCR делает это проще простого, и вы можете выполнить задачу всего в несколько строк C#.

В этом руководстве мы пройдем весь процесс: от **load image for OCR**, через **detect tables in image**, до **extract table from image** и сохранения её в CSV‑файл. К концу вы получите готовое к запуску консольное приложение, которое может **extract tables from PNG** (или любой поддерживаемый bitmap) без лишних хлопот.

## Prerequisites

Прежде чем начать, убедитесь, что у вас есть:

- .NET 6.0 SDK или новее (код также работает с .NET Framework)
- Visual Studio 2022 (или любая другая IDE по вашему выбору)
- Файл лицензии Aspose.OCR for .NET (можно начать с бесплатной пробной версии)
- Пример изображения с таблицей (например, `invoice_table.png`)

Если что‑то из этого вам незнакомо, не переживайте — просто установите .NET SDK, скачайте NuGet‑пакет, и вы будете готовы к работе.

## Overview of the Solution

На высоком уровне процесс выглядит так:

1. **Load the image**, которую нужно обработать.  
2. **Run OCR recognition**, чтобы движок понял, где находится текст.  
3. **Create a TableExtractor**, который сканирует результаты OCR в поисках сеточных структур.  
4. **Extract all detected tables** и выбрать нужную.  
5. **Save the table** в CSV (или любой другой предпочтительный формат).

Каждый шаг подробно описан ниже, с полными фрагментами кода, которые можно просто скопировать.

<img src="table_extraction_example.png" alt="пример извлечения таблиц из изображения" width="600">

*(На изображении выше показан пример таблицы счета, которую мы будем извлекать.)*

## Step 1 – Load the Image for OCR

Первое, что нужно сделать, — указать Aspose OCR, какой файл читать. Библиотека поддерживает PNG, JPEG, BMP, TIFF и несколько других форматов. Минимальный код выглядит так:

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image.FromFile

// ...

// Load the image that contains the table
var ocrEngine = new OcrEngine
{
    Image = Image.FromFile(@"C:\Images\invoice_table.png") // <-- adjust the path
};
```

**Почему это важно:**  
`Image.FromFile` выполняет тяжелую работу по декодированию PNG (или любого другого bitmap) в формат, понятный OCR‑движку. Если пропустить этот шаг или передать повреждённый файл, последующий вызов `Recognize()` бросит исключение.

> **Pro tip:** Если вы работаете с большими PDF‑файлами, сначала извлеките каждую страницу как изображение — иначе OCR‑движок может выйти из памяти.

## Step 2 – Recognize the Page (Required Before Table Detection)

Распознавание преобразует сырые пиксельные данные в поисковый текстовый макет. Без этого шага `TableExtractor` нечего будет обрабатывать.

```csharp
// Perform OCR recognition – this populates internal structures
ocrEngine.Recognize();
```

**Что происходит «под капотом»?**  
Aspose OCR запускает нейронную сеть‑детектор текста, затем создает иерархию объектов `Page`, `Paragraph` и `Word`. Детектор таблиц позже изучает пространственные отношения между этими словами.

Если вы обрабатываете множество изображений в цикле, рассмотрите возможность переиспользования одного экземпляра `OcrEngine` и просто меняйте свойство `Image` — это уменьшит накладные расходы на выделение памяти.

## Step 3 – Create a TableExtractor and Detect Tables in Image

Теперь, когда OCR‑данные есть, можно попросить Aspose найти таблицы. Класс `TableExtractor` делает именно это.

```csharp
using Aspose.OCR.Table;

// ...

// Initialize the TableExtractor with the recognized engine
var tableExtractor = new TableExtractor(ocrEngine);

// Extract all tables detected on the page
List<Table> extractedTables = tableExtractor.ExtractAll();
```

**Зачем использовать `ExtractAll()`?**  
Одно изображение может содержать несколько таблиц (например, в многоразделном отчёте). `ExtractAll()` возвращает `List<Table>`, чтобы вы могли перебрать их, выбрать нужную или даже объединить позже.

Если нужна только первая таблица, можно безопасно обратиться к `extractedTables[0]`, но всегда проверяйте, что список не пуст, чтобы избежать `IndexOutOfRangeException`.

```csharp
if (extractedTables.Count == 0)
{
    Console.WriteLine("No tables were detected. Check the image quality or try adjusting OCR settings.");
    return;
}
```

## Step 4 – Save the Extracted Table as CSV (or Any Other Format)

Aspose упрощает экспорт. Класс `Table` имеет встроенные методы `SaveCsv`, `SaveXls` и `SaveJson`. Вот как записать CSV‑файл:

```csharp
// Save the first detected table to CSV
string outputPath = @"C:\Output\invoice_table.csv";
extractedTables[0].SaveCsv(outputPath);

Console.WriteLine($"Table extraction completed. CSV saved to {outputPath}");
```

**Как выглядит CSV?**  
Если исходное изображение содержало сетку 4 × 3, CSV может выглядеть так:

```
Item,Quantity,Price
Widget A,2,19.99
Widget B,5,9.50
Service C,1,150.00
```

Вы можете открыть этот файл в Excel, Power BI или сразу передать в ваш конвейер данных.

## Full End‑to‑End Example

Ниже представлен полный, самодостаточный пример программы. Скопируйте его в новый консольный проект (`dotnet new console`) и запустите. Убедитесь, что установлен NuGet‑пакет `Aspose.OCR` (`dotnet add package Aspose.OCR`).

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;          // For Image
using Aspose.OCR;
using Aspose.OCR.Table;

namespace TableExtractTutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the image that contains the table
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                Image = Image.FromFile(@"C:\Images\invoice_table.png")
            };

            // -------------------------------------------------
            // Step 2: Recognize the page (required before table detection)
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 3: Create a TableExtractor and detect tables
            // -------------------------------------------------
            var tableExtractor = new TableExtractor(ocrEngine);
            List<Table> extractedTables = tableExtractor.ExtractAll();

            // Guard against no tables found
            if (extractedTables.Count == 0)
            {
                Console.WriteLine("No tables detected. Verify image quality or OCR settings.");
                return;
            }

            // -------------------------------------------------
            // Step 4: Save the first extracted table as CSV
            // -------------------------------------------------
            string csvPath = @"C:\Output\invoice_table.csv";
            extractedTables[0].SaveCsv(csvPath);

            Console.WriteLine($"Table extraction completed. CSV saved at: {csvPath}");
        }
    }
}
```

### Expected Output

При запуске программы вы должны увидеть примерно следующее:

```
Table extraction completed. CSV saved at: C:\Output\invoice_table.csv
```

Откройте `invoice_table.csv` — вы увидите строки и столбцы, соответствующие оригинальному изображению.

## Common Questions & Edge Cases

### What if the image is a JPEG instead of PNG?

Тот же код работает — просто измените расширение файла в `Image.FromFile`. Aspose OCR автоматически определяет формат, так что **extract tables from png** не является обязательным требованием; он работает с любым поддерживаемым bitmap.

### My table has merged cells. Will they be preserved?

Слитные ячейки обрабатываются как отдельные столбцы в CSV, потому что CSV не поддерживает объединение. Если нужна более богатая разметка (например, Excel со слитными ячейками), используйте `SaveXls`:

```csharp
extractedTables[0].SaveXls(@"C:\Output\invoice_table.xls");
```

### The detection missed a column. How can I improve accuracy?

- Увеличьте разрешение изображения (≥300 dpi — оптимально).  
- Предобработайте изображение: переведите в градации серого, увеличьте контраст или примените фильтр выравнивания (deskew).  
- Настройте параметры Aspose OCR, такие как `PageSegMode` или `Language`, если таблица содержит нелатинские символы.

### Can I extract tables from a PDF directly?

Да. Сначала преобразуйте каждую страницу PDF в изображение (с помощью `Aspose.PDF` или любой библиотеки PDF‑to‑image), а затем передайте полученные изображения в тот же рабочий процесс.

## Tips for Production‑Ready Implementations

1. **Wrap OCR in a try/catch** — в средах с сетевой лицензией могут возникать исключения лицензирования.  
2. **Dispose of `Image` objects** — оборачивайте их в `using`, чтобы освободить нативные ресурсы.  
3. **Log the confidence scores** — `TableExtractor` предоставляет `Table.Confidence`, который можно сохранять для мониторинга качества.  
4. **Batch processing** — при обработке сотен счетов параллелизуйте вызовы OCR, но учитывайте ограничения потокобезопасности лицензии.

## Next Steps

Теперь, когда вы знаете **how to extract tables** из изображений, вы можете исследовать:

- **Detect tables in image** видео (используя `TableExtractor` на каждом кадре).  
- **Load image for OCR** из веб‑API, создавая облачные сервисы извлечения таблиц.  
- **Extract tables from PNG** файлов, хранящихся в Azure Blob Storage, интегрируя с Azure Functions для безсерверной обработки.

Экспериментируйте с разными форматами файлов, настраивайте параметры OCR или направляйте CSV‑вывод напрямую в базу данных. Возможности безграничны.

---

*Счастливого кодинга! Если столкнётесь с проблемами или у вас есть идеи по улучшению, оставьте комментарий ниже. Разберёмся вместе.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}