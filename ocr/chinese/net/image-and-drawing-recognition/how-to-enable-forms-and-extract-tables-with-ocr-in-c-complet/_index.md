---
category: general
date: 2026-01-04
description: 学习如何在 C# 中使用 OCR 启用表单并从图像中提取表格。本分步教程还展示了如何运行 OCR 图像并检测表格。
draft: false
keywords:
- how to enable forms
- how to extract tables
- run OCR image
- use OCR C#
- detect tables OCR
language: zh
og_description: 逐步指南，介绍如何在 C# 中启用表单、提取表格、运行 OCR 图像以及检测表格 OCR。
og_title: 如何在 C# 中启用表单并使用 OCR 提取表格
tags:
- OCR
- C#
- Computer Vision
title: 如何在 C# 中启用表单并使用 OCR 提取表格 – 完整指南
url: /zh/net/image-and-drawing-recognition/how-to-enable-forms-and-extract-tables-with-ocr-in-c-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中启用表单并提取表格（使用 OCR）——完整指南

是否曾经想过 **如何在扫描发票、收据或任何结构化文档时启用表单**？你并不孤单。在许多真实项目中，最大的摩擦点是让 OCR 同时理解表单字段 **和** 表格，而不需要成千上万行的自定义解析。

在本教程中，我们将一步步演示一个实用的端到端解决方案，展示 **如何启用表单**、**如何提取表格**，甚至 **如何在单个 C# 程序中运行 OCR 图像** 处理。完成后，你将拥有一个可直接运行的代码片段，能够以 OCR 方式检测表格、提取键值对并将其打印到控制台。

> **先决条件** – .NET 6+（或 .NET Framework 4.7+），引用你使用的 OCR SDK（示例假设有一个通用的 `OcrEngine` 类），以及一张包含表格或表单的图像文件（`invoice_table.png`）。不需要其他外部库。

![how to enable forms with OCR C#](image.png)

## 本教程涵盖内容

- **启用表单识别**，自动识别诸如 “Invoice Number” 或 “Date” 等字段。  
- **从扫描文档中提取表格**，获取行/列计数以及单元格内容。  
- **在一次调用中运行 OCR 图像** 处理，并以编程方式处理结果。  
- 针对 **detect tables OCR** 的边缘情况提示，如合并单元格或缺失边框。  

让我们开始吧。

## 第一步：设置 OCR 引擎 – 如何启用表单

在进行任何识别之前，你需要一个 OCR 引擎实例。大多数 SDK 都提供一个简单的构造函数；我们还会指出后续可以调整的配置选项位置。

```csharp
using System;
using System.Linq;

// Assume the OCR SDK namespace is OcrSdk
using OcrSdk;

public class OcrDemo
{
    public static void Main()
    {
        // Create the OCR engine – this is where “how to enable forms” starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that contains a table or form.
        // Replace the path with the actual location of your PNG/JPEG/TIFF file.
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");
```

**为什么这很重要：** 实例化引擎会分配内部资源（如语言模型）。如果跳过此步骤，后续的 `Recognize` 调用将抛出 `NullReferenceException`。

## 第二步：打开结构化提取 – 如何提取表格 & detect tables OCR

现在我们启用两个核心功能：表格识别和表单字段提取。大多数现代 OCR 引擎都提供布尔标志或更细粒度的 `Config` 对象。

```csharp
        // Enable structured extraction features.
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms
```

**专业提示：** 如果只需要其中一个功能，禁用另一个可以提升约 20 % 的性能。

## 第三步：运行 OCR 图像并获取结果 – run OCR image

引擎配置好后，单个方法调用即可完成繁重工作。返回的 `OcrResult` 包含表格和表单字段的集合。

```csharp
        // Run OCR – this is the “run OCR image” step.
        OcrResult ocrResult = ocrEngine.Recognize();

        // -----------------------------------------------------------------
        // Step 4: Process Detected Tables – how to extract tables
        // -----------------------------------------------------------------
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");

            // Show the first row for a quick sanity check.
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // -----------------------------------------------------------------
        // Step 5: Process Detected Form Fields – how to enable forms
        // -----------------------------------------------------------------
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

### 预期的控制台输出

```
Table 1: 5 rows, 4 columns
Item | Qty | Price | Total
InvoiceNumber: INV-2025-001
Date: 2025-12-31
Customer: Acme Corp.
```

具体数字会因源图像而异，但你应该会看到每个表格的汇总行，随后是第一行的单元格值，接着是一组表单字段的键‑值对列表。

## 第四步：处理 Detect Tables OCR 的边缘情况

即使 `EnableTableRecognition = true`，OCR 仍可能在以下情况下出错：

| 问题 | 产生原因 | 快速修复 |
|------|----------|----------|
| **合并单元格** | 引擎将合并区域视为单个单元格。 | 后处理行：查找异常宽的单元格，并根据空白拆分。 |
| **缺失边框** | 表格线条淡或断裂。 | 在送入引擎前提升图像对比度（`ocrEngine.PreprocessImage`）。 |
| **表格旋转** | 文档以角度扫描。 | 使用 `ocrEngine.Config.AutoRotate = true`（若支持）。 |

**技巧：** 在访问索引前，务必先验证 `table.Rows.Count` 和 `table.Columns.Count`，以避免 `IndexOutOfRangeException`。

## 第五步：完整示例 – 可直接运行的代码

下面是完整程序，可复制粘贴到新的控制台项目中。它包含 `using` 指令、引擎设置以及前面展示的处理逻辑。

```csharp
using System;
using System.Linq;
using OcrSdk;   // Replace with your actual OCR SDK namespace

public class OcrDemo
{
    public static void Main()
    {
        // 1️⃣ Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the target image
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");

        // 3️⃣ Enable structured extraction (forms + tables)
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms

        // 4️⃣ Run OCR – “run OCR image”
        OcrResult ocrResult = ocrEngine.Recognize();

        // 5️⃣ Process tables – “how to extract tables”
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // 6️⃣ Process form fields – “how to enable forms”
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

运行程序（`dotnet run` 或在 Visual Studio 中 `Ctrl+F5`），即可看到前述的控制台输出。

## 常见问题解答 (FAQ)

**Q: 这能处理 PDF 输入吗？**  
A: 大多数 OCR SDK 会通过内部光栅化每页来接受 PDF。只需调用 `ocrEngine.LoadPdf("file.pdf")` 替代 `LoadImage` 即可。

**Q: 如果我的图像同时包含表格 *和* 签名怎么办？**  
A: 签名会作为单独的图像区域出现。通过检查 `ocrResult.Images` 中的低置信度文本即可忽略它。

**Q: 能把表格导出为 CSV 吗？**  
A: 完全可以。在遍历 `table.Rows` 时，将每个 `cell.Text` 写入 `StringBuilder`，用逗号分隔，然后保存为 `.csv` 文件。

## 结论

现在你已经掌握了 **如何启用表单**、**如何提取表格**，以及使用 C# **run OCR image** 处理的完整步骤。示例演示了从引擎创建、配置到结果处理的完整工作流，方便你直接复制到自己的项目中。

接下来，尝试将示例图像换成多页发票 PDF，实验 `ocrEngine.Config.AutoRotate`，或将提取的数据写入数据库。这些扩展将帮助你深入掌握 **detect tables OCR** 与 **use OCR C#** 在生产环境中的应用。

如果遇到任何问题，欢迎在下方留言。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}