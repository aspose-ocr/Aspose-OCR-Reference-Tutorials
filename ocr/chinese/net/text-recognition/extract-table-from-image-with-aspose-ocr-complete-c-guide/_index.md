---
category: general
date: 2026-03-18
description: 使用 Aspose OCR 在 C# 中从图像提取表格。了解如何将表格转换为 JSON，获取表格 JSON，并在几分钟内从图像中提取文本。
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: zh
og_description: 使用 Aspose OCR 在 C# 中从图像提取表格。学习将表格转换为 JSON，获取表格 JSON 并快速从图像中提取文本。
og_title: 使用 Aspose OCR 从图像提取表格 – 完整 C# 指南
tags:
- Aspose OCR
- C#
- Table Extraction
title: 使用 Aspose OCR 从图像提取表格 – 完整 C# 指南
url: /zh/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取表格 – 完整 C# 指南

是否曾经需要**从图像中提取表格**，但不确定哪个库能够在不进行大量手动解析的情况下完成？你并不孤单。在许多发票处理或收据扫描项目中，真正的痛点是将嘈杂的位图转换为下游系统可以使用的结构化表格。

好消息是？使用 Aspose OCR，你只需几行代码就能**convert table to JSON**，并且还能获取整张图片的纯文本，所以**extract text from image** 也是顺带的收益。在本教程中，我们将完整演示整个流程——从加载图片到获得检测到的表格的整洁 JSON 表示。

> **快速收获：** 完成后，你将拥有一个可运行的 C# 控制台应用，它会打印原始 OCR 文本以及一个可以直接写入数据库或 API 的 JSON 字符串。

## 前置条件

在开始之前，请确保你已经具备：

- 已安装 .NET 6.0 SDK（或任意较新的 .NET 版本）。  
- 有效的 Aspose OCR 许可证或免费试用版（库在没有许可证的情况下仍可使用，但会添加水印）。  
- 一张实际包含表格的图片，例如 `invoice_table.png`。  
- Visual Studio 2022、VS Code，或任意你喜欢的编辑器。

除 `Aspose.OCR` 之外，无需其他 NuGet 包。

## 第一步：创建项目并安装 Aspose OCR

首先，创建一个新的控制台项目并引入 OCR 库。

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **小技巧：** 如果你使用公司代理，请添加 `--no-restore` 标志，随后使用适当的环境变量运行 `dotnet restore`。

## 第二步：初始化 OCR 引擎并启用表格识别

解决方案的核心是 `OcrEngine`。通过切换 `EnableTableRecognition`，我们告诉 Aspose OCR 去寻找网格状结构，而不是把所有内容都当作纯文本处理。

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

为什么这一步至关重要？如果不启用表格识别，引擎会把图像展平成单个字符串，后续就无法重建行列。启用后会增加一个轻量级的布局分析阶段，几乎不影响性能，却能带来巨大的下游收益。

## 第三步：加载图片并执行识别

现在把引擎指向包含表格的文件。`ImageStream.FromFile` 支持大多数常见格式（PNG、JPEG、TIFF）。

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

如果图片尺寸较大，建议先缩放以加快处理速度。Aspose OCR 会自动检测 DPI，但 300 DPI 的扫描通常是大多数表格的最佳选择。

## 第四步：提取纯文本 – “extract text from image”

即使我们的主要目标是表格，通常仍需要原始文本用于日志或回退处理。

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

`Text` 属性会把引擎看到的所有内容连接在一起，并保留换行。这在你需要验证 OCR 是否正确读取表格外的标题或页脚时非常有用。

## 第五步：获取检测到的表格 JSON – “convert table to json” & “get table json”

下面就是魔法所在。`GetTableAsJson()` 会把检测到的行、列以及单元格内容序列化为整洁的 JSON 字符串。

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

生成的 JSON 大致如下（为可读性做了格式化）：

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

为什么首选 JSON？它语言无关，易于反序列化为对象，并且与现代 Web API 配合得天衣无缝。如果你需要 CSV，只需遍历行并用逗号连接单元格文本即可。

## 第六步：（可选）将 JSON 转换为 .NET 对象 – “convert image to json”

如果你更喜欢强类型，使用 `System.Text.Json` 反序列化 JSON。

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

你需要定义 `TableModel`、`RowModel` 和 `CellModel` 来匹配 JSON 架构。此步骤展示了如何从**convert image to json**一路走到强类型对象，使后续验证轻而易举。

## 完整示例

将所有代码组合在一起，下面是可直接运行的完整程序。将其保存为项目文件夹下的 `Program.cs`。

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

### 预期输出

运行 `dotnet run` 时，你应该会看到类似以下的输出：

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

如果输出为空，请再次确认 `EnableTableRecognition` 已设置为 `true`，且图片确实包含清晰的网格线。

## 常见问题及规避方法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| **未返回 JSON** | 表格检测未开启或图像对比度过低。 | 确保 `ocrEngine.Settings.EnableTableRecognition = true`，并提升图像质量（增加对比度、二值化）。 |
| **行不完整** | 合并单元格或文字旋转导致 OCR 误判。 | 预处理图像：使用 `ImageProcessor.Rotate` 去除倾斜，或手动拆分合并单元格。 |
| **出现 Unicode 垃圾字符** | 字体未被识别（如手写体）。 | 通过 `ocrEngine.Language = Language.English;` 切换语言包，或使用专门的手写体 OCR 引擎。 |
| **性能下降** | 图像过大（>5 MP）。 | 将宽度缩放至约 1500 px，同时保持 DPI。 |

## 后续步骤：深入拓展

既然已经能够**extract table from image**并**convert table to JSON**，可以考虑以下扩展：

- 使用 Entity Framework 将 JSON **Persist the JSON** 到数据库。  
- **Post‑process** JSON，统一货币格式（例如去除 `$` 符号）。  
- 使用 `Directory.GetFiles` 并配合 `Parallel.ForEach` 批量处理文件夹中的发票。  
- 将 OCR 流程 **Integrate** 到 Azure Functions 或 AWS Lambda，实现无服务器 OCR 管道。

这些主题自然会涉及其他二级关键词，如 **convert image to json**（将完整 OCR 结果发送到云端）以及 **get table json**（供下游分析使用）。

---

### 结论

我们已经演示了如何使用 Aspose OCR **extract table from image**，将表格转换为整洁的 JSON，甚至反序列化为 C# 对象。相同的模式

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}