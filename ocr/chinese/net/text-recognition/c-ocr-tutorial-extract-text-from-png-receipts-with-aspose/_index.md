---
category: general
date: 2026-05-25
description: C# OCR 教程，展示如何在 C# 中加载图像文件并使用 Aspose OCR 识别收据中的 PNG 文本——一步一步的指南。
draft: false
keywords:
- c# OCR tutorial
- load image file c#
- recognize png text
- read receipt OCR
- perform OCR image
language: zh
og_description: C# OCR 教程，手把手教你在 C# 中加载图像文件，并使用 Aspose OCR 识别收据中的 PNG 文本。
og_title: C# OCR 教程 – 从 PNG 收据中提取文本
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: c# OCR tutorial that shows how to load image file c# and recognize
    png text from a receipt using Aspose OCR – step‑by‑step guide.
  headline: 'c# OCR tutorial: Extract Text from PNG Receipts with Aspose'
  type: TechArticle
- description: c# OCR tutorial that shows how to load image file c# and recognize
    png text from a receipt using Aspose OCR – step‑by‑step guide.
  name: 'c# OCR tutorial: Extract Text from PNG Receipts with Aspose'
  steps:
  - name: Why Aspose?
    text: Aspose OCR supports over 30 languages, works offline, and returns a rich
      `OcrResult` object—perfect for **perform OCR image** tasks where you need more
      than just plain text.
  - name: Handling Common Edge Cases
    text: '| Situation | What to do | |-----------|------------| | **Image is blurry**
      | Pre‑process with `System.Drawing` to sharpen or increase DPI. | | **Receipt
      contains multiple languages** | Set `ocrEngine.Language = OcrLanguage.English
      | OcrLanguage.Spanish;` | | **Large batch processing** | Reuse a sin'
  - name: What’s Next?
    text: '- Experiment with **load image file c#** using `SkiaSharp` for true cross‑platform
      support. - Dive deeper into `OcrResult.Words` to extract line items, prices,
      and dates—perfect for expense‑tracking apps. - Combine this tutorial with Azure
      Functions or AWS Lambda to build a serverless receipt‑proces'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: C# OCR 教程：使用 Aspose 从 PNG 收据中提取文本
url: /zh/net/text-recognition/c-ocr-tutorial-extract-text-from-png-receipts-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教程 – 使用 Aspose 从 PNG 收据中提取文本

是否曾经需要一个 **c# OCR 教程**，能够真正完成任务而无需无休止的搜索？你来对地方了。在本指南中，我们将 **load image file c#**、**recognize png text**，以及 **read receipt OCR** 结果，同时向你展示如何使用 Aspose OCR 进行 **perform OCR image** 处理。

我们将从安装所需的 NuGet 包开始，逐行讲解代码，并以整洁的 JSON 输出结束，你可以直接将其导入下一个数据管道。没有废话，只有实用、可直接运行的解决方案。

## 你将学到

- 如何在 .NET 6（或更高）项目中设置 Aspose OCR。  
- **load an image file c#** 的确切步骤并将其交给引擎。  
- 如何从收据图像 **recognize png text** 并获取结果。  
- 将 **read receipt OCR** 输出以整齐的 JSON 格式呈现的方法。  
- 关于在不同文件类型上进行 **perform OCR image** 操作以及处理常见陷阱的技巧。

**先决条件**  
- Visual Studio 2022（或任何你喜欢的 IDE）。  
- .NET 6 SDK 或更高版本。  
- 一张 PNG 收据图像（我们称之为 `receipt.png`）。

如果你已经准备好，让我们开始吧。

![c# OCR 教程截图](ocr-demo.png "c# OCR 教程结果显示 JSON 输出")

## c# OCR 教程 – 设置 Aspose OCR 引擎

首先，我们需要 Aspose OCR 库。在解决方案文件夹的终端中运行：

```bash
dotnet add package Aspose.OCR
```

该单行命令会拉取所有必需的内容，包括用于图像解码的本机二进制文件。安装完成后，创建一个新的控制台项目或将代码添加到现有项目中。

### 为什么选择 Aspose？

Aspose OCR 支持超过 30 种语言，离线工作，并返回丰富的 `OcrResult` 对象——非常适合需要超出纯文本的 **perform OCR image** 任务。

## 加载图像文件 c# 并准备收据

库已准备就绪，现在让我们 **load image file c#**。`System.Drawing.Image` 类负责大部分工作，但如果你更喜欢跨平台替代方案，也可以使用 `SkiaSharp`。

```csharp
using System;
using System.Drawing;               // For Image loading
using Aspose.OCR;                  // OCR engine
using System.Text.Json;            // JSON serialization

// Step 1: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most receipts; change as needed
    Language = OcrLanguage.English
};

// Step 2: Load the image to be processed
// Replace the path with the actual location of your receipt PNG
string imagePath = @"C:\Receipts\receipt.png";
if (!File.Exists(imagePath))
{
    Console.WriteLine($"File not found: {imagePath}");
    return;
}
using Image receiptImage = Image.FromFile(imagePath);
```

> **专业提示：** 将 `Image` 包裹在 `using` 语句中（如示例所示），以及时释放本机资源——在循环中对大量文件 **perform OCR image** 时尤为重要。

## 使用 Aspose 识别 PNG 文本

图像已加载到内存后，引擎即可 **recognize png text**。Aspose 返回一个 `OcrResult`，其中包含原始字符串以及每个识别单词的详细数据。

```csharp
// Step 3: Perform OCR and obtain the result object
OcrResult ocrResult = ocrEngine.RecognizeWithResult(receiptImage);

// Quick sanity check – was anything recognized?
if (string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("No text detected. Verify image quality or language settings.");
    return;
}
```

为什么调用 `RecognizeWithResult` 而不是更简单的 `Recognize`？前者让你能够获取置信度分数、边界框和换行信息——如果以后需要 **read receipt OCR** 进行项目行提取，这非常方便。

## 将收据 OCR 结果读取为 JSON

大多数下游系统喜欢 JSON，所以我们将序列化 `OcrResult`。`System.Text.Json` 序列化器能够优雅地处理复杂对象，我们还会启用缩进以提升可读性。

```csharp
// Step 4: Convert the OCR result to a readable JSON string (indented)
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

生成的 JSON 大致如下（为简洁起见已截断）：

```json
{
  "Text": "Walmart\n123 Main St\nTotal $12.34",
  "Words": [
    {
      "Text": "Walmart",
      "Confidence": 0.98,
      "Rectangle": { "X": 10, "Y": 20, "Width": 150, "Height": 30 }
    },
    {
      "Text": "Total",
      "Confidence": 0.95,
      "Rectangle": { "X": 10, "Y": 150, "Width": 80, "Height": 25 }
    }
  ]
}
```

现在你可以将 `jsonResult` 导入数据库、消息队列，或仅仅记录日志进行调试。

## 执行 OCR 图像处理并显示输出

最后，将 JSON 输出到控制台。在实际应用中，你可能会将其写入文件或通过 HTTP 发送，但使用控制台可以轻松验证一切是否正常。

```csharp
// Step 5: Output the JSON to the console
Console.WriteLine("=== OCR Result (JSON) ===");
Console.WriteLine(jsonResult);
```

运行程序（`dotnet run`），你应该会看到整齐的 JSON 输出。如果收据图像清晰，文本将非常准确；如果不清晰，考虑提升图像分辨率或在送入引擎前应用预处理滤镜（例如灰度、对比度提升）。

### 处理常见边缘情况

| 情况 | 处理方法 |
|-----------|------------|
| **图像模糊** | 使用 `System.Drawing` 进行预处理以锐化或提升 DPI。 |
| **收据包含多种语言** | 设置 `ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;` |
| **大批量处理** | 重用单个 `OcrEngine` 实例；每次迭代仅更换 `Image`。 |
| **内存压力** | 及时释放 `Image` 对象，并考虑使用 `await Task.Run` 进行异步管道。 |

这些调整即使在输入不完美的情况下，也能保持你的 **perform OCR image** 工作流的稳健性。

## 总结

恭喜你——你刚刚完成了一个 **c# OCR 教程**，实现了加载图像、**recognizes png text**，以及 **reads receipt OCR** 输出为整洁的 JSON。核心步骤（引擎设置、图像加载、OCR 执行、序列化和显示）构成了一个坚实的基础，您可以将其扩展到发票、护照或任何其他扫描文档。

### 接下来做什么？

- 使用 `SkiaSharp` 试验 **load image file c#**，实现真正的跨平台支持。  
- 深入研究 `OcrResult.Words`，提取项目行、价格和日期——非常适合费用跟踪应用。  
- 将本教程与 Azure Functions 或 AWS Lambda 结合，构建无服务器收据处理 API。  

随意修改代码，添加更多图像，甚至切换到其他语言包。OCR 的世界充满惊喜，而你现在拥有探索它们的工具。

祝编码愉快，愿你的收据永远可读！

## 相关教程

- [使用 Aspose.OCR 进行语言选择的 C# 图像文本提取](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [从图像提取文本 – 使用 Aspose.OCR for .NET 的 OCR 优化](/ocr/english/net/ocr-optimization/)
- [如何使用 OCR - 在不进行文本区域检测的情况下识别图像](/ocr/english/net/image-and-drawing-recognition/recognize-image-without-text-area-detection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}