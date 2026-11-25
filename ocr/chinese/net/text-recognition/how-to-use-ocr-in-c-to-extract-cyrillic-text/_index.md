---
category: general
date: 2026-09-10
description: 如何在 C# 中使用 OCR 提取西里尔文字，对图像进行预处理，并将其转换为 PDF 或 HTML 文件的单个可运行示例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- preprocess image for OCR
- convert image to PDF
- convert image to HTML
- extract Cyrillic text
language: zh
lastmod: 2026-09-10
og_description: 如何在 C# 中使用 OCR 提取西里尔文文本、预处理图像，并将结果导出为 PDF 或 HTML。请按照本分步指南操作。
og_image_alt: Diagram illustrating how to use OCR to extract Cyrillic text and convert
  images
og_title: 如何在 C# 中使用 OCR —— 提取西里尔文字并转换图像
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: How to use OCR in C# to extract Cyrillic text, preprocess images, and
    convert them to PDF or HTML files in a single, runnable example.
  headline: How to use OCR in C# to extract Cyrillic text
  type: TechArticle
tags:
- OCR
- C#
- Cyrillic
- Image processing
- PDF conversion
title: 如何在 C# 中使用 OCR 提取西里尔文字
url: /zh/net/text-recognition/how-to-use-ocr-in-c-to-extract-cyrillic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中使用 OCR 提取西里尔文文本

如果您需要在 C# 中 **使用 OCR** 来从扫描文档中提取西里尔文文本，本指南将为您展示一个完整、可直接运行的解决方案。您还将学习如何 **预处理图像以进行 OCR**，以及在文本识别后如何 **将图像转换为 PDF** 或 **将图像转换为 HTML**。

文档数字化项目常常遇到两个问题：低质量扫描和需要以多种格式存储结果。本教程通过使用 Aspose.OCR 库来解决这两个问题，该库会自动下载缺失的语言包，提供内置的图像处理助手，并且可以通过一次调用将 OCR 结果导出为 PDF 或 HTML。

## 前提条件

* .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Framework 4.7+）。
* Visual Studio 2022 或任何支持 C# 项目的编辑器。
* **Aspose.OCR** NuGet 包。使用以下方式安装：

```bash
dotnet add package Aspose.OCR
```

* 包含西里尔字符的图像文件（例如 `sample_cyrillic.jpg`）。  
  将文件放置在您可以引用为 `YOUR_DIRECTORY` 的文件夹中。

库将在您首次设置 `ocrEngine.Language = Language.Cyrillic;` 时自动下载西里尔语言包，因此无需手动下载。

## 第一步 – 初始化 OCR 引擎（使用 OCR）

创建 `OcrEngine` 实例会为后续所有操作准备引擎。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine – the first step in how to use OCR with Aspose
        var ocrEngine = new OcrEngine();
```

**为什么重要：** 引擎保存语言、图像处理设置和输出选项等配置。一次性初始化可以保持其余代码简洁且线程安全。

## 第二步 – 选择西里尔语言（提取西里尔文文本）

```csharp
        // Select Cyrillic language; the pack is fetched automatically if missing
        ocrEngine.Language = Language.Cyrillic;
```

**为什么重要：** OCR 的准确性在很大程度上取决于正确的语言模型。通过显式选择 `Language.Cyrillic`，引擎会使用适用于俄语、乌克兰语、保加利亚语等的字符频率表。

## 第三步 – 为 OCR 预处理图像

低质量扫描可能存在倾斜、斑点或光照不均。内置的 `ImageProcessor` 只需两次调用即可提升识别率。

```csharp
        // Optional but strongly recommended: deskew and despeckle the image
        ocrEngine.ImageProcessor.Deskew();      // Aligns rotated text
        ocrEngine.ImageProcessor.Despeckle();  // Removes isolated noise pixels
```

**为什么重要：** 预处理可以减少错误字符并提升置信度。倾斜的文本常会产生乱码；去倾斜可以将其校正。去斑点可以消除微小的伪影，防止 OCR 引擎误将其识别为字符。

> **专业提示：** 如果源图像已经很干净，可以跳过这些调用。对于严重退化的扫描，可考虑额外的步骤，例如 `Binarize()` 或 `ContrastStretch()`。

## 第四步 – 对输入图像执行 OCR

```csharp
        // The image path can be absolute or relative to the executable
        string inputPath = Path.Combine("YOUR_DIRECTORY", "sample_cyrillic.jpg");
        ocrEngine.Process(inputPath);
```

**为什么重要：** `Process` 在提供的位图上运行识别流水线。它返回 `void`；识别后的文本可通过 `Text` 属性获取。

## 第五步 – 获取识别文本并保存到文件

```csharp
        // Access the recognized string
        string recognizedText = ocrEngine.Text;

        // Save the plain‑text result
        string txtOutput = Path.Combine("YOUR_DIRECTORY", "result.txt");
        File.WriteAllText(txtOutput, recognizedText);
        Console.WriteLine("Text saved to: " + txtOutput);
```

**为什么重要：** 保存原始文本可用于后续处理，如搜索、索引或输入到翻译服务中。

## 第六步 – 将 OCR 结果导出为其他格式（将图像转换为 PDF 与将图像转换为 HTML）

```csharp
        // Export as PDF – useful for archival or sharing with non‑technical users
        string pdfOutput = Path.Combine("YOUR_DIRECTORY", "result.pdf");
        ocrEngine.SaveResultAsPdf(pdfOutput);
        Console.WriteLine("PDF saved to: " + pdfOutput);

        // Export as HTML – retains basic layout and can be displayed in browsers
        string htmlOutput = Path.Combine("YOUR_DIRECTORY", "result.html");
        ocrEngine.SaveResultAsHtml(htmlOutput);
        Console.WriteLine("HTML saved to: " + htmlOutput);
    }
}
```

**为什么重要：** 将 OCR 结果转换为 PDF 或 HTML 可以在提供可搜索文本的同时保留原始图像的视觉上下文。这对于法律或档案工作流尤为重要。

### 预期输出

使用清晰的西里尔文扫描运行程序会生成三个文件：

* `result.txt` – 纯 Unicode 文本，例如 `Пример текста на кириллице`。
* `result.pdf` – 包含图像且带有不可见文本层以供搜索的 PDF。
* `result.html` – 显示图像并可选择文本的 HTML 页面。

打开任意文件即可验证西里尔字符已被正确提取。

## 常见问题与边缘情况

| 问题 | 回答 |
|----------|--------|
| **如果语言包下载失败怎么办？** | 确保机器能够访问互联网。您也可以从 Aspose 网站预先下载语言包并放置在 `bin` 文件夹中。 |
| **我可以在同一次运行中识别其他字母表吗？** | 可以。在调用 `Process` 之前设置 `ocrEngine.Language = Language.English;`（或任何受支持的枚举）。如果图像混合了多种脚本，可能需要针对每种语言分别运行 `Process`。 |
| **我的图像是多页 TIFF —— 能够处理吗？** | `OcrEngine` 每次只能处理一个位图。将每页加载为 `Bitmap`，在循环中调用 `Process`，并将结果拼接起来。 |
| **如何提升大批量处理的性能？** | 复用同一个 `OcrEngine` 实例并设置 `ocrEngine.OptimizeMemory = true;`。此外，可考虑为每个线程使用独立的引擎实例进行并行处理。 |

## 结论

现在，您已经了解了在 C# 中 **使用 OCR** 来 **提取西里尔文文本**、**预处理图像以进行 OCR**，以及 **将图像转换为 PDF** 或 **将图像转换为 HTML** 的简洁步骤。完整示例展示了生产环境的——

## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [如何使用 AspOCR：针对 .NET 的图像 OCR 过滤器预处理](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [如何在 C# 中提取 OCR 文本 – 完整分步指南](/ocr/english/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/)
- [如何在图像识别中使用 Aspose OCR 获取 JSON 结果](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}