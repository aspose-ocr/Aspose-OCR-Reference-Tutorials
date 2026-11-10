---
category: general
date: 2026-09-06
description: 使用 Aspose.OCR 在 C# 中将 OCR 图像转换为 JSON – 步骤指南，提取图像文本并获取 JSON 输出。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: zh
lastmod: 2026-09-06
og_description: 使用 Aspose.OCR 在 C# 中将 OCR 图像转换为 JSON。了解如何加载图像进行 OCR、从照片中识别文本，并将结果转换为
  JSON。
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: 在 C# 中将 OCR 图像转换为 JSON – 完整的 Aspose.OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: 如何在 C# 中使用 Aspose.OCR 将 OCR 图像转换为 JSON
url: /zh/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.OCR 将 OCR 图像转换为 JSON

如果您需要在 .NET 应用程序中 **ocr image to json**，本指南将向您展示如何使用 Aspose.OCR 实现。我们将逐步演示加载用于 OCR 的图像、从照片中识别文本以及将结果转换为 JSON，以便您在 API 或数据库中使用这些数据。

从图像文件中提取文本是发票处理、收据扫描和归档项目的常见需求。通过本教程，您将能够 **convert image to text**，获取纯文本结果，并生成保留布局信息的结构化 JSON 负载。

## 前提条件

在开始之前，请确保您拥有：

- .NET 6.0 SDK 或更高版本已安装  
- Visual Studio 2022（或任何支持 .NET 的编辑器）  
- 已在项目中添加 Aspose.OCR NuGet 包（`Aspose.OCR`）  
- 将示例图像（`input.jpg`）放置在代码可引用的文件夹中  

您无需额外的 OCR 引擎；Aspose.OCR 在内部已处理所有繁重工作。

## 第 1 步：安装 Aspose.OCR NuGet 包

在项目文件夹的终端中运行：

```bash
dotnet add package Aspose.OCR
```

该包包含 `Aspose.OCR.OcrEngine` 类，提供 **load image for ocr**、语言选择和结果导出等方法。

## 第 2 步：创建新的 C# 控制台项目

如果尚未有项目，请创建一个：

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

添加您需要的 `using` 指令：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## 第 3 步：加载图像并配置 OCR 引擎

以下代码演示如何 **load image for ocr**、设置语言并为处理做好准备。本例使用西里尔字母，但您可以根据源语言切换为 `OcrLanguage.English`、`OcrLanguage.French` 等。

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **为什么这很重要：** 正确设置语言可在您 **recognize text from photo** 时显著提升准确率。引擎会使用特定语言的词典和字符集。

## 第 4 步：运行 OCR 过程并获取结果

现在运行 OCR 引擎。如果过程成功，您可以将 **extract text from image** 为纯文本、HTML 或 JSON。Aspose.OCR 提供 `SaveJson` 方法，可将结构化结果写入文件。

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### 预期的 JSON 结构

典型的 `output.json` 文件如下（为便于阅读已格式化）：

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

JSON 负载包含每行的文本、置信度分数以及在原始照片中包围该行的矩形。这使得将 OCR 结果映射回 UI 元素或数据库字段变得轻而易举。

## 第 5 步：演示的完整源代码

下面是完整的、可直接运行的程序，实现 **ocr image to json** 工作流。将其复制到 `Program.cs` 并运行 `dotnet run`。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### 运行示例

1. 将名为 `input.jpg` 的图像放置在项目根目录。  
2. 执行 `dotnet run`。  
3. 观察控制台输出并打开 `output.json` 查看结构化数据。

## 专业提示与常见陷阱

| 情况 | 建议 |
|-----------|----------------|
| **低分辨率照片** | 在处理前提高 DPI，或使用 `ocrEngine.Image = ImageStream.FromFile(path, 300)` 强制 300 DPI。 |
| **混合语言** | 设置 `ocrEngine.Language = OcrLanguage.Multilingual`，并可通过 `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }` 提供语言列表。 |
| **大型文档** | 一次处理一页以保持低内存使用；引擎支持多页 TIFF。 |
| **字符错误** | 确认已选择正确的 `OcrLanguage`；使用错误的语言会在您 **convert image to text** 时降低准确率。 |
| **JSON 缺少字段** | 确保使用 Aspose.OCR 版本 23.6 或更高；旧版本未公开 `SaveJson` 方法。 |

## 常见问题

**Q: 我可以将 OCR 结果作为字节数组而不是文件获取吗？**  
A: 可以。使用 `ocrEngine.SaveJson(Stream)` 直接写入 `MemoryStream`，然后调用 `stream.ToArray()`。

**Q: 引擎支持 PDF 输入吗？**  
A: Aspose.OCR 可以接受通过 Aspose.PDF 转换为图像的 PDF 页面，但 OCR 引擎本身只能处理光栅图像。请先将 PDF 转为图像，然后 **load image for ocr**。

**Q: 如何处理阿拉伯语等从右到左的脚本？**  
A: 设置 `ocrEngine.Language = OcrLanguage.Arabic`。JSON 包含正确的文本方向，您可以在支持 RTL 的 UI 框架中渲染。

## 结论

您现在拥有一个完整的 **ocr image to json** C# 解决方案。通过加载图像、配置语言、运行 OCR 引擎并将结果导出为 JSON，您可以在单一、流畅的工作流中 **extract text from image**、**convert image to text** 和 **recognize text from photo**。

接下来您可以探索：

- 将 JSON 输出集成到 Web API（`ASP.NET Core`）  
- 将结果存储在 MongoDB 等 NoSQL 数据库中  
- 添加后处理以纠正常见的 OCR 错误  

随意尝试不同的语言、图像格式和输出选项，以满足项目需求。祝编码愉快！

## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式。每个资源都包含完整的可运行代码示例和逐步说明。

- [在 C# 中从图像识别文本 – OCR 与 JSON 完整指南](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [使用 Aspose OCR 将图像转换为文本 – 步骤指南](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [如何使用 Aspose.OCR for .NET 从图像提取文本](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}