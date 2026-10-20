---
category: general
date: 2026-05-31
description: 使用 Aspose OCR 在 C# 中从图像中提取表格。了解如何将图像转换为表格、启用表格检测以及高效输出结果。
draft: false
keywords:
- extract tables from image
- convert image to table
- OCR table extraction
- Aspose OCR C#
- image to spreadsheet conversion
- table detection in OCR
language: zh
og_description: 使用 Aspose OCR 从图像中提取表格。本指南展示了如何将图像转换为表格、启用表格检测以及在 C# 中处理结果。
og_title: 从图像提取表格 – 步骤详解 C# 教程
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
title: 使用 Aspose OCR 从图像中提取表格 – 完整 C# 指南
url: /zh/net/image-and-drawing-recognition/extract-tables-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取表格 – 完整 C# 指南

是否曾经需要**从图像中提取表格**却不知从何入手？你并不孤单；许多开发者在尝试将扫描的发票或收据转换为可用数据时都会遇到这个难题。好消息是？使用 Aspose OCR，你只需几行 C# 代码就能**将图像转换为表格**。

在本教程中，我们将通过一个真实案例进行演示：加载包含表格的 PNG， 将视觉布局转换为结构化网格，并打印每个单元格的内容及置信度分数。完成后，你将拥有一个可直接放入任何 .NET 项目的完整代码片段，并附带处理边缘情况和扩展方案的技巧。

## 你需要准备什么

在开始之前，请确保拥有：

- **.NET 6.0** 或更高版本（代码同样适用于 .NET Framework 4.6+）
- **Aspose.OCR** NuGet 包（`Install-Package Aspose.OCR`）
- 一张实际包含表格的图片文件（例如 `invoice_with_table.png`）
- 基本的 C# IDE（Visual Studio、Rider 或带 C# 扩展的 VS Code）

就这些——无需额外的 OCR 引擎，也不需要笨重的依赖。准备好了吗？让我们开始吧。

## 第一步：初始化 OCR 引擎以 **Extract Tables from Image**

首先，创建一个 `OcrEngine` 实例并指向源图片。可以把引擎想象成读取每个像素并尝试理解布局的大脑。

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

> **为何重要：** 如果没有正确初始化引擎，OCR 引擎将无从分析，图片中也永远提取不到表格。`ImageStream.FromFile` 调用同时处理常见的格式问题（PNG、JPEG、BMP），无需额外的转换步骤。

## 第二步：启用表格检测 – **Convert Image to Table** 的关键

Aspose OCR 能读取图片中的纯文本，但除非显式告诉它寻找表格，否则它不会自动识别行列。这时 `DetectTables` 标志就派上用场了。

```csharp
// Turn on table detection in the OCR options
engine.Options = new OcrOptions
{
    DetectTables = true   // This activates the table extraction algorithm
};
```

> **专业提示：** 如果只需要原始文本，可将 `DetectTables` 保持为 `false`。开启该选项会带来一点额外开销，但换来的是干净、结构化的结果，直接可用于电子表格或数据库。

## 第三步：执行 OCR 识别 – 真正的考验时刻

现在让引擎真正读取图片。`Recognize` 方法返回一个 `OcrResult` 对象，里面包含纯文本以及检测到的表格。

```csharp
// Execute the OCR process
OcrResult result = engine.Recognize();
```

> **内部发生了什么？** Aspose 会先执行一系列图像预处理步骤（去倾斜、二值化），随后使用基于神经网络的文本识别器。若 `DetectTables` 为 true，还会进行布局分析，将字符分组为行和列。

## 第四步：遍历检测到的表格 – **Extract Tables from Image** 实战

如果引擎发现了表格，它们会出现在 `result.Tables` 中。我们将遍历每个表格、每行、每列，打印单元格文本和置信度百分比。

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

> **为何要检查置信度？** OCR 并非完美，尤其是低分辨率扫描时。`Confidence` 值（0‑100）帮助你决定是直接接受该单元格还是标记为人工复核。对关键数据的常用阈值是 80 %。

### 预期输出

假设源图片包含一个 3 × 4 的发票明细表格，输出可能类似于：

```
Table found:
Item (conf:96%)   Qty (conf:94%)   Price (conf:97%)   Total (conf:95%)
Pen (conf:99%)    10 (conf:98%)    1.20 (conf:97%)    12.00 (conf:96%)
Notebook (conf:95%) 5 (conf:93%)  3.50 (conf:94%)    17.50 (conf:92%)
...
```

如果未检测到表格，`result.Tables` 将为空——不会打印任何内容，但程序仍会优雅退出。

## 第五步：处理边缘情况和常见陷阱

### 低分辨率图像

当源图片低于 150 dpi 时，表格检测算法可能漏掉单元格边界。一个快速的解决办法是使用 `System.Drawing` 将图像放大后再交给 Aspose：

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load and upscale
Bitmap bmp = new Bitmap(@"YOUR_DIRECTORY/invoice_with_table.png");
Bitmap resized = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
engine.Image = ImageStream.FromBitmap(resized);
```

### 倾斜的表格

如果表格旋转了几度，启用自动去倾斜：

```csharp
engine.Options.Deskew = true; // Turns on automatic deskewing
```

### 单页多表格

Aspose OCR 会把每个表格作为 `result.Tables` 中的独立对象返回。你可以单独处理它们，或在需要统一视图时合并为一个 `DataTable`。

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

### 导出到 Excel

一旦拥有 `DataTable`，使用 `ClosedXML` 导出为 `.xlsx` 文件轻而易举：

```csharp
using ClosedXML.Excel;

var workbook = new XLWorkbook();
var worksheet = workbook.Worksheets.Add(merged, "ExtractedTable");
workbook.SaveAs("ExtractedTable.xlsx");
```

至此，你已经真正实现了**converted image to table**，并可以将生成的电子表格交给后续流程使用。

## 完整可运行示例 – 从头到尾

下面是完整的、可直接运行的程序示例。将其粘贴到新的控制台项目中，替换文件路径后按 **F5** 运行。

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

**流程说明**

1. **引擎设置** – 加载图片并告知 Aspose 寻找表格。  
2. **选项调优** – `DetectTables` 完成核心工作；`Deskew` 提升倾斜扫描的准确度。  
3. **识别** – 同时返回纯文本和 `Table` 对象集合。  
4. **遍历** – 打印每个单元格及置信度，并构建 `DataTable` 供后续导出使用。  
5. **导出** – 使用 `ClosedXML`（轻量、无 COM 依赖）写入 `.xlsx` 文件——非常适合下游分析或报表。

## 常见问题

- **这能处理 PDF 吗？**  
  可以。先使用 `PdfRenderer` 或 `Ghostscript` 将每页 PDF 转为图像，然后交给 Aspose OCR。

- **可以从 JPG 中提取表格吗？**  
  完全可以。`ImageStream.FromFile` 方法原生支持 JPEG、PNG、BMP 和 TIFF。

- **如果表格中有合并单元格怎么办？**  
  Aspose OCR 会把合并单元格视为独立的逻辑单元格；你可能需要根据置信度或内容模式在后处理阶段自行合并。

- **表格大小有没有限制？**  
  实际上引擎可以处理上百行的表格。性能呈线性下降，若扫描文件非常大，建议分块处理。

## 结束语

我们刚刚向你展示了如何

## 接下来该学习什么？

- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}