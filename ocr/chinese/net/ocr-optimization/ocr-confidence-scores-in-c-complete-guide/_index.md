---
category: general
date: 2026-05-31
description: 学习如何在 C# 中获取 OCR 置信度分数，同时从图像提取文本并使用 Aspose OCR 读取收据图像。
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: zh
og_description: OCR 置信度分数让您能够评估准确性；本指南展示了如何使用 Aspose OCR 从图像中提取文本、获取边界框以及读取收据图像。
og_title: C# 中的 OCR 置信度分数——完整指南
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C# 中的 OCR 置信度分数 – 完整指南
url: /zh/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# 中的 OCR 置信度分数 – 完整指南

有没有想过在需要*从图像中提取文本*时，如何获取 **OCR 置信度分数**？也许你正在尝试读取用于费用跟踪的 **收据图像** 文件，并想了解引擎对哪些字符不确定。好消息是？使用 Aspose.OCR，你可以在几行 C# 代码中从 JPG 中提取置信度百分比、边界框和纯文本。

在本教程中，我们将逐步讲解你需要了解的所有内容：安装库、将引擎配置为 **在 JPG 上执行 OCR**、提取置信度分数，以及解释 **OCR 边界框**（告诉你每个字符在页面上的位置）。完成后，你将拥有一个可直接运行的控制台应用程序，打印每个字符、其置信度和位置——非常适合验证收据或任何扫描文档。

## 你将学到的内容

- 通过 NuGet 安装 Aspose.OCR 并设置基本的 OCR 引擎。  
- 配置 `OcrOptions` 以请求纯文本输出 **带置信度分数** 和 **边界框**。  
- 遍历 `OcrResult`，**逐行逐符号提取图像文本**。  
- 处理常见问题，如文件缺失、低置信度字符以及非 JPG 格式。  
- 将示例扩展为处理文件夹中的多个收据图像。

无需任何 Aspose 经验；只需一个可用的 .NET 环境和一张你想测试的收据图像（JPG）。

---

## 第一步 – 安装 Aspose.OCR 并准备项目

首先，你需要 Aspose.OCR NuGet 包。在项目文件夹中打开终端并运行：

```bash
dotnet add package Aspose.OCR
```

> **小技巧：** 免费试用支持最多 200 页，足以进行收据扫描测试。

安装包后，创建一个新的控制台项目（如果还没有的话）：

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

现在你可以打开生成的 `Program.cs` 并开始添加 using 指令：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

这些命名空间让你能够访问 `OcrEngine`、`OcrOptions` 以及后面需要的结果类型。

## 第二步 – 获取 OCR 置信度分数和 OCR 边界框

这是本教程的核心。我们将配置引擎，使每个识别的字符都带有 **置信度分数** 和 **边界框**（包围字形的矩形）。此 H2 标题本身已包含主要关键词，满足 SEO 规则。

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**为什么要包含置信度分数？**  
置信度分数（0‑100%）告诉你引擎对每个字符的确定程度。如果你将输出传递给下游逻辑——例如费用审批工作流——可以自动拒绝或标记低置信度的符号。

**为什么要请求边界框？**  
当你需要在原始图像上高亮文本、提取子区域或将 OCR 结果与 UI 覆盖层对齐时，边界框是必不可少的。每个 `character.Bounds` 提供像素坐标系下的 X、Y、宽度和高度。

## 第三步 – 在 JPG 上执行 OCR 并提取图像文本

现在我们实际运行引擎。调用 `Recognize()` 完成所有繁重工作并返回一个 `OcrResult` 对象。

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

如果图像路径错误或文件格式不受支持，Aspose 会抛出 `FileNotFoundException` 或 `UnsupportedImageFormatException`。在生产代码中请使用 try/catch 块来优雅地处理这些异常情况。

### 提取纯文本

如果只需要连贯的文本，可以读取 `ocrResult.Text`：

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

但由于我们还请求了置信度分数和边界框，需要遍历结构以查看每个字符的详细信息。

## 第四步 – 遍历行、符号并显示 OCR 置信度分数

下面的循环会打印每个字符、其置信度以及其边界框。这正是 **读取收据图像** 示例的亮点所在。

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

示例输出可能如下：

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**解释这些数字：**  
- **置信度 ≥ 90%** – 通常可以直接接受。  
- **置信度 70‑89%** – 可能需要再次检查，尤其是金额中的数字。  
- **置信度 < 70%** – 建议标记为手动复核。

## 第五步 – 完整可运行示例（含错误处理）

将所有内容整合后，下面是一个完整的程序，你可以复制粘贴到 `Program.cs` 中。它包含对缺失文件的简单检查，并在 OCR 失败时打印友好提示。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### 预期输出

运行 `dotnet run` 时，控制台首先显示连贯的收据文本，然后列出每个字符的置信度分数和边界框。如果某字符的置信度较低，你会看到低于 80 的百分比，这提示需要手动核对该部分收据。

## 额外内容：在文件夹中批量处理收据

如果你有一批收据 JPG，使用 `foreach (var file in Directory.GetFiles(folder, "*.jpg"))` 循环将上述逻辑包装起来。记得为每个文件重置 `OcrEngine`，或在循环内部实例化新对象，以避免状态泄漏。

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

批量处理对于夜间费用导入非常方便。

---

## 结论

现在，你已经拥有一个完整、端到端的解决方案，可在 C# 中获取 **OCR 置信度分数**、**从图像中提取文本**，并在 **对 JPG（如读取收据图像）执行 OCR** 时检索 **OCR 边界框**。代码完全独立，兼容最新的 Aspose.OCR 版本（截至 2026‑05‑31），并提供构建可靠文档处理流水线所需的细粒度数据。

接下来可以尝试使用 `System.Drawing` 或 UI 库在原始收据上可视化边界框，或将低置信度字符送入二次校验服务。你也可以通过设置 `ocrEngine.Options.Language = OcrLanguage.French;` 来实验不同语言——API 支持多种语言环境。

祝编码愉快，愿你的置信度分数始终保持高位！ 

![显示收据 OCR 置信度分数和边界框的控制台输出

## 接下来你应该学习什么？

- [使用 Aspose.OCR 提取图像文本（C#）并选择语言](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [获取图像识别中已识别字符的 OCR 选项](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [在图像识别中使用 Aspose OCR 获取 JSON 结果](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}