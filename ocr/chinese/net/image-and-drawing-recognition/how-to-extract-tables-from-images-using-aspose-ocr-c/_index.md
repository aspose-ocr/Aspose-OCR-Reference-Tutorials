---
category: general
date: 2026-03-28
description: 学习如何使用 Aspose OCR 在 C# 中从图像中提取表格。本指南涵盖如何检测图像中的表格、加载图像进行 OCR，以及从 PNG 文件中提取表格。
draft: false
keywords:
- how to extract tables
- extract table from image
- detect tables in image
- load image for ocr
- extract tables from png
language: zh
og_description: 使用 Aspose OCR 在 C# 中从图像提取表格的逐步教程。包括代码、说明以及检测图像文件中表格的技巧。
og_title: 如何使用 Aspose OCR（C#）从图像中提取表格
tags:
- Aspose OCR
- C#
- Table Extraction
title: 如何使用 Aspose OCR（C#）从图像中提取表格
url: /zh/net/image-and-drawing-recognition/how-to-extract-tables-from-images-using-aspose-ocr-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR (C#) 从图像中提取表格

是否曾想过 **如何从扫描的发票或电子表格的截图中提取表格**？你并不是唯一有此需求的人。在许多实际项目中，我们需要把表格的图片转换成可以查询的数据——通常是 CSV 或 DataTable。好消息是，Aspose OCR 让这件事变得轻而易举，只需几行 C# 代码即可实现。

在本教程中，我们将完整演示整个过程：从 **加载图像进行 OCR**，到 **检测图像中的表格**，最后 **从图像中提取表格** 并保存为 CSV 文件。完成后，你将拥有一个可直接运行的控制台应用程序，能够 **从 PNG** 文件（或任何受支持的位图）中 **零难度提取表格**。

## 前置条件

在开始之前，请确保你具备以下环境：

- .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Framework）
- Visual Studio 2022（或你喜欢的任何 IDE）
- Aspose.OCR for .NET 授权文件（可先使用免费试用版）
- 包含表格的示例图片（例如 `invoice_table.png`）

如果对上述任意项目不熟悉，也无需担心——只需安装 .NET SDK 并获取 NuGet 包，即可开始。

## 解决方案概览

从宏观上看，工作流如下：

1. **加载待处理的图像**。  
2. **执行 OCR 识别**，让引擎知道文字所在位置。  
3. **创建 TableExtractor**，在 OCR 结果中扫描网格结构。  
4. **提取所有检测到的表格**，并挑选需要的那一个。  
5. **将表格保存为 CSV**（或其他你喜欢的格式）。

下面将逐步详细说明每一步，并提供可直接复制粘贴的完整代码片段。

<img src="table_extraction_example.png" alt="如何从图像中提取表格示例" width="600">

*(上图展示了我们将在教程中提取的示例发票表格。)*

## 步骤 1 – 加载 OCR 所需的图像

首先，需要告诉 Aspose OCR 要读取哪个文件。库支持 PNG、JPEG、BMP、TIFF 等多种格式。最简代码如下：

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

**为什么这一步很重要：**  
`Image.FromFile` 完成了解码 PNG（或其他位图）的重活，将其转换为 OCR 引擎能够理解的格式。如果跳过此步骤或传入损坏的文件，后续的 `Recognize()` 调用将抛出异常。

> **小贴士：** 若处理的是大型 PDF，建议先将每页导出为图像——否则 OCR 引擎可能会因内存不足而崩溃。

## 步骤 2 – 进行页面识别（表格检测前的必备步骤）

识别将原始像素数据转换为可搜索的文本布局。没有这一步，`TableExtractor` 将无所适从。

```csharp
// Perform OCR recognition – this populates internal structures
ocrEngine.Recognize();
```

**内部到底发生了什么？**  
Aspose OCR 采用基于神经网络的文字检测器，然后生成 `Page`、`Paragraph`、`Word` 等层级对象。表格检测器随后会检查这些单词之间的空间关系。

如果在循环中处理大量图像，建议复用同一个 `OcrEngine` 实例，仅替换其 `Image` 属性——这样可以降低分配开销。

## 步骤 3 – 创建 TableExtractor 并检测图像中的表格

OCR 数据准备好后，就可以让 Aspose 去寻找表格了。`TableExtractor` 类正是为此而生。

```csharp
using Aspose.OCR.Table;

// ...

// Initialize the TableExtractor with the recognized engine
var tableExtractor = new TableExtractor(ocrEngine);

// Extract all tables detected on the page
List<Table> extractedTables = tableExtractor.ExtractAll();
```

**为什么使用 `ExtractAll()`？**  
一张图像可能包含多个表格（例如多章节报告）。`ExtractAll()` 返回 `List<Table>`，便于遍历、挑选或后续合并。

如果只需要第一张表格，可以安全地使用 `extractedTables[0]`，但务必先判断列表是否为空，以避免 `IndexOutOfRangeException`。

```csharp
if (extractedTables.Count == 0)
{
    Console.WriteLine("No tables were detected. Check the image quality or try adjusting OCR settings.");
    return;
}
```

## 步骤 4 – 将提取的表格保存为 CSV（或其他格式）

Aspose 的导出功能非常简洁。`Table` 类内置了 `SaveCsv`、`SaveXls`、`SaveJson` 等方法。下面演示如何写入 CSV 文件：

```csharp
// Save the first detected table to CSV
string outputPath = @"C:\Output\invoice_table.csv";
extractedTables[0].SaveCsv(outputPath);

Console.WriteLine($"Table extraction completed. CSV saved to {outputPath}");
```

**CSV 文件长什么样？**  
假设源图像是一个 4 × 3 的网格，生成的 CSV 可能如下所示：

```
Item,Quantity,Price
Widget A,2,19.99
Widget B,5,9.50
Service C,1,150.00
```

你可以在 Excel、Power BI 中打开此文件，或直接将其导入数据管道。

## 完整端到端示例

下面是完整的、可独立运行的程序。将其复制到新建的控制台项目（`dotnet new console`）中并执行。确保已安装 NuGet 包 `Aspose.OCR`（`dotnet add package Aspose.OCR`）。

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

### 预期输出

运行程序后，你应该会看到类似以下的输出：

```
Table extraction completed. CSV saved at: C:\Output\invoice_table.csv
```

打开 `invoice_table.csv`，即可看到与原始图片对应的行列数据。

## 常见问题与边缘情况

### 如果图像是 JPEG 而不是 PNG，怎么办？

代码保持不变，只需在 `Image.FromFile` 中更换文件扩展名即可。Aspose OCR 会自动检测格式，因此 **从 png 提取表格** 并非硬性要求，任何受支持的位图均可使用。

### 我的表格有合并单元格，是否会被保留？

合并单元格在 CSV 输出中会被视为独立的列，因为 CSV 本身不支持跨列合并。如果需要更丰富的格式（例如保留合并单元格的 Excel），请使用 `SaveXls`：

```csharp
extractedTables[0].SaveXls(@"C:\Output\invoice_table.xls");
```

### 检测漏掉了一列，如何提升准确率？

- 提高图像分辨率（≥300 dpi 为佳）。  
- 预处理图像：转为灰度、增强对比度或使用去倾斜滤镜。  
- 调整 Aspose OCR 设置，如 `PageSegMode` 或 `Language`（当表格包含非拉丁字符时）。

### 能直接从 PDF 提取表格吗？

可以。先使用 `Aspose.PDF` 或其他 PDF‑转‑图像库将每页转换为图像，然后将这些图像交给相同的工作流即可。

## 生产环境实现建议

1. **在 OCR 调用外层使用 try/catch** —— 网络授权环境可能抛出授权异常。  
2. **释放 `Image` 对象** —— 使用 `using` 块包装，以释放本地资源。  
3. **记录置信度分数** —— `TableExtractor` 暴露的 `Table.Confidence` 可用于质量监控。  
4. **批量处理** —— 处理数百张发票时，可并行化 OCR 调用，但需遵守授权的线程安全指南。

## 后续步骤

了解了 **如何从图像中提取表格** 后，你可以进一步探索：

- 使用 Aspose 的 `TableExtractor` 对每帧视频进行 **检测表格**。  
- 从 Web API **加载图像进行 OCR**，实现云端表格提取服务。  
- 从 Azure Blob Storage 中 **提取 PNG 文件中的表格**，并结合 Azure Functions 实现无服务器处理。

欢迎尝试不同的文件格式、微调 OCR 参数，或直接将 CSV 输出写入数据库。可能性无限。

---

*祝编码愉快！如果遇到任何问题或有改进建议，欢迎在下方留言。我们一起解决。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}