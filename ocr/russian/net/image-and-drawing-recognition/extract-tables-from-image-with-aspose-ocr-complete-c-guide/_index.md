---
category: general
date: 2026-05-31
description: Извлекайте таблицы из изображения с помощью Aspose OCR на C#. Узнайте,
  как преобразовать изображение в таблицу, включить обнаружение таблиц и эффективно
  выводить результаты.
draft: false
keywords:
- extract tables from image
- convert image to table
- OCR table extraction
- Aspose OCR C#
- image to spreadsheet conversion
- table detection in OCR
language: ru
og_description: Извлекать таблицы из изображения с помощью Aspose OCR. Это руководство
  показывает, как преобразовать изображение в таблицу, включить обнаружение таблиц
  и обработать результаты в C#.
og_title: Извлечение таблиц из изображения – пошаговый учебник C#
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  headline: Extract Tables from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  name: Extract Tables from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: Expected Output
    text: 'Assuming the source image contains a 3 × 4 table of invoice line items,
      you might see something like:'
  - name: Low‑Resolution Images
    text: 'When your source picture is under 150 dpi, the table detection algorithm
      may miss cell boundaries. A quick fix is to upscale the image using `System.Drawing`
      before feeding it to Aspose:'
  - name: Skewed Tables
    text: 'If the table is rotated even a few degrees, enable auto‑deskew:'
  - name: Multiple Tables on One Page
    text: Aspose OCR returns each table as a separate object in `result.Tables`. You
      can treat them individually, or merge them into a single DataTable if you need
      a unified view.
  - name: Exporting to Excel
    text: 'Once you have a `DataTable`, exporting to an `.xlsx` file is a breeze with
      `ClosedXML`:'
  type: HowTo
- questions:
  - answer: Yes. Convert each PDF page to an image first (`PdfRenderer` or `Ghostscript`),
      then feed the bitmap to Aspose OCR.
    question: Does this work with PDFs?
  - answer: Absolutely. The `ImageStream.FromFile` method accepts JPEG, PNG, BMP,
      and TIFF out of the box.
    question: Can I extract tables from a JPG?
  - answer: Aspose OCR treats merged cells as separate logical cells; you may need
      to post‑process the output to combine them based on confidence or content patterns.
    question: What if my table has merged cells?
  - answer: Practically, the engine handles tables up to several hundred rows. Performance
      degrades linearly, so consider chunking very large scans.
    question: Is there a limit on table size?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- Data Extraction
title: Извлечение таблиц из изображения с помощью Aspose OCR – Полное руководство
  по C#
url: /ru/net/image-and-drawing-recognition/extract-tables-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение таблиц из изображения – Полное руководство на C#  

Когда‑нибудь вам нужно было **извлечь таблицы из изображения**, но вы не знали, с чего начать? Вы не одиноки; многие разработчики сталкиваются с этой проблемой, пытаясь превратить отсканированные счета или чеки в пригодные данные. Хорошая новость? С Aspose OCR вы можете **преобразовать изображение в таблицу** всего в несколько строк кода на C#.

В этом руководстве мы пройдем реальный пример: загрузим PNG, содержащий таблицу, превратим визуальное расположение в структурированную сетку и выведем содержимое каждой ячейки с оценкой уверенности. К концу у вас будет полностью рабочий фрагмент, который можно вставить в любой .NET‑проект, а также советы по обработке граничных случаев и масштабированию решения.

## Что вам понадобится

Прежде чем начать, убедитесь, что у вас есть:

- **.NET 6.0** или новее (код также работает с .NET Framework 4.6+)
- NuGet‑пакет **Aspose.OCR** (`Install-Package Aspose.OCR`)
- Файл изображения, действительно содержащий таблицу (например, `invoice_with_table.png`)
- Базовая IDE для C# (Visual Studio, Rider или VS Code с расширением C#)

И всё—никаких дополнительных OCR‑движков, никаких тяжёлых зависимостей. Готовы? Поехали.

## Шаг 1: Инициализация OCR‑движка для **извлечения таблиц из изображения**

Сначала создаём экземпляр `OcrEngine` и указываем ему наш исходный файл изображения. Думайте о движке как о мозге, который будет читать каждый пиксель и пытаться понять раскладку.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine with the input image
OcrEngine engine = new OcrEngine
{
    // ImageStream.FromFile loads the image from disk
    Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
};
```

> **Почему это важно:** Без правильной инициализации движка OCR не будет иметь чего анализировать, и вы никогда не получите таблицы из картинки. Вызов `ImageStream.FromFile` также решает типичные проблемы форматов (PNG, JPEG, BMP), так что дополнительные шаги конвертации не нужны.

## Шаг 2: Включение обнаружения таблиц – Ключ к **преобразованию изображения в таблицу**

Aspose OCR может читать обычный текст с изображения, но он не поймёт строки и столбцы, если явно не указать искать таблицы. Здесь вступает в действие флаг `DetectTables`.

```csharp
// Turn on table detection in the OCR options
engine.Options = new OcrOptions
{
    DetectTables = true   // This activates the table extraction algorithm
};
```

> **Pro tip:** Если вам нужен только сырой текст, оставьте `DetectTables` со значением `false`. Включение добавляет небольшие накладные расходы, но результат будет чистым и структурированным, готовым к импорту в таблицу или базу данных.

## Шаг 3: Выполнение OCR‑распознавания – Момент истины

Теперь просим движок действительно прочитать изображение. Метод `Recognize` возвращает объект `OcrResult`, содержащий как обычный текст, так и любые обнаруженные таблицы.

```csharp
// Execute the OCR process
OcrResult result = engine.Recognize();
```

> **Что происходит под капотом?** Aspose последовательно применяет предобработку изображения (выравнивание, бинаризация), а затем нейронно‑сетевой распознаватель текста. Когда `DetectTables` установлен в `true`, запускается дополнительный проход анализа раскладки, группирующий символы в строки и столбцы.

## Шаг 4: Итерация по обнаруженным таблицам – **извлечение таблиц из изображения** в действии

Если движок нашёл таблицы, они появятся в `result.Tables`. Мы пройдемся по каждой таблице, затем по каждой строке и столбцу, выводя текст ячейки и процент уверенности.

```csharp
// Loop over every detected table
foreach (var table in result.Tables)
{
    Console.WriteLine("Table found:");
    for (int r = 0; r < table.Rows; r++)
    {
        for (int c = 0; c < table.Columns; c++)
        {
            var cell = table[r, c];
            // Show cell text and its confidence level
            Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
        }
        Console.WriteLine(); // New line after each row
    }
}
```

> **Зачем проверять уверенность?** OCR не идеален, особенно при сканах низкого разрешения. Значение `Confidence` (0‑100) позволяет решить, принимать ячейку как есть или помечать её для ручной проверки. Типичный порог — 80 % для критически важных данных.

### Ожидаемый вывод

При условии, что исходное изображение содержит таблицу 3 × 4 со строками счёта, вы можете увидеть примерно следующее:

```
Table found:
Item (conf:96%)   Qty (conf:94%)   Price (conf:97%)   Total (conf:95%)
Pen (conf:99%)    10 (conf:98%)    1.20 (conf:97%)    12.00 (conf:96%)
Notebook (conf:95%) 5 (conf:93%)  3.50 (conf:94%)    17.50 (conf:92%)
...
```

Если таблиц не обнаружено, `result.Tables` будет пустым — ничего выводить не будет, но программа завершится корректно.

## Шаг 5: Обработка граничных случаев и распространённых подводных камней

### Изображения низкого разрешения

Когда исходная картинка имеет менее 150 dpi, алгоритм обнаружения таблиц может пропустить границы ячеек. Быстрое решение — масштабировать изображение с помощью `System.Drawing` перед передачей в Aspose:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load and upscale
Bitmap bmp = new Bitmap(@"YOUR_DIRECTORY/invoice_with_table.png");
Bitmap resized = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
engine.Image = ImageStream.FromBitmap(resized);
```

### Искажённые таблицы

Если таблица повернута даже на несколько градусов, включите авто‑выравнивание:

```csharp
engine.Options.Deskew = true; // Turns on automatic deskewing
```

### Несколько таблиц на одной странице

Aspose OCR возвращает каждую таблицу как отдельный объект в `result.Tables`. Их можно обрабатывать по отдельности или объединить в один `DataTable`, если нужен единый вид.

```csharp
// Example: Merge all tables into one DataTable
var merged = new System.Data.DataTable();
foreach (var tbl in result.Tables)
{
    // Simple merge logic – assumes same column count
    // Add rows from each table
    for (int r = 0; r < tbl.Rows; r++)
    {
        var row = merged.NewRow();
        for (int c = 0; c < tbl.Columns; c++)
        {
            row[c] = tbl[r, c].Text;
        }
        merged.Rows.Add(row);
    }
}
```

### Экспорт в Excel

Как только у вас есть `DataTable`, экспорт в файл `.xlsx` делается в один клик с помощью `ClosedXML`:

```csharp
using ClosedXML.Excel;

var workbook = new XLWorkbook();
var worksheet = workbook.Worksheets.Add(merged, "ExtractedTable");
workbook.SaveAs("ExtractedTable.xlsx");
```

Теперь вы действительно **преобразовали изображение в таблицу** и можете передать полученную таблицу дальнейшим процессам.

## Полный рабочий пример – От начала до конца

Ниже полностью готовая к запуску программа, объединяющая все шаги. Вставьте её в новый консольный проект, замените путь к файлу и нажмите **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;
using System.Data;
using ClosedXML.Excel;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine with the image
        OcrEngine engine = new OcrEngine
        {
            Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
        };

        // 2️⃣ Enable table detection (key to convert image to table)
        engine.Options = new OcrOptions
        {
            DetectTables = true,
            Deskew = true // Helps with slightly rotated scans
        };

        // 3️⃣ Perform recognition
        OcrResult result = engine.Recognize();

        // 4️⃣ Process each detected table
        DataTable merged = new DataTable();
        bool firstTable = true;

        foreach (var table in result.Tables)
        {
            Console.WriteLine("Table found:");
            for (int r = 0; r < table.Rows; r++)
            {
                // Ensure DataTable has enough columns
                if (firstTable && merged.Columns.Count < table.Columns)
                {
                    for (int i = merged.Columns.Count; i < table.Columns; i++)
                        merged.Columns.Add($"Col{i + 1}");
                }

                DataRow dr = merged.NewRow();
                for (int c = 0; c < table.Columns; c++)
                {
                    var cell = table[r, c];
                    Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
                    dr[c] = cell.Text; // Populate DataTable for Excel export
                }
                Console.WriteLine();
                merged.Rows.Add(dr);
            }
            firstTable = false;
            Console.WriteLine(); // Blank line between tables
        }

        // 5️⃣ Optional: Export merged result to Excel
        if (merged.Rows.Count > 0)
        {
            using var wb = new XLWorkbook();
            wb.Worksheets.Add(merged, "ExtractedTables");
            wb.SaveAs("ExtractedTables.xlsx");
            Console.WriteLine("\nExcel file 'ExtractedTables.xlsx' created successfully.");
        }
        else
        {
            Console.WriteLine("\nNo tables were detected in the image.");
        }
    }
}
```

**Объяснение процесса**

1. **Engine setup** – Загружает изображение и указывает Aspose искать таблицы.  
2. **Options tuning** – `DetectTables` делает основную работу; `Deskew` повышает точность при наклонных сканах.  
3. **Recognition** – Возвращает как обычный текст, так и коллекцию объектов `Table`.  
4. **Iteration** – Выводит каждую ячейку с уровнем уверенности, одновременно формируя `DataTable` для последующего экспорта.  
5. **Export** – Использует `ClosedXML` (лёгкая библиотека без внешних зависимостей) для записи файла `.xlsx` — идеально для аналитики или отчётности.

## Часто задаваемые вопросы

- **Работает ли это с PDF?**  
  Да. Сначала преобразуйте каждую страницу PDF в изображение (`PdfRenderer` или `Ghostscript`), затем передайте полученный битмап в Aspose OCR.

- **Можно ли извлекать таблицы из JPG?**  
  Абсолютно. Метод `ImageStream.FromFile` принимает JPEG, PNG, BMP и TIFF «из коробки».

- **Что делать, если в таблице объединённые ячейки?**  
  Aspose OCR рассматривает объединённые ячейки как отдельные логические ячейки; возможно, понадобится пост‑обработка вывода для их объединения на основе уверенности или шаблонов содержимого.

- **Есть ли ограничение на размер таблицы?**  
  Практически движок обрабатывает таблицы до нескольких сотен строк. Производительность линейно снижается, поэтому для очень больших сканов рекомендуется разбивать их на части.

## Подведение итогов

Мы только что показали вам, как

## Что стоит изучить дальше?

- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}