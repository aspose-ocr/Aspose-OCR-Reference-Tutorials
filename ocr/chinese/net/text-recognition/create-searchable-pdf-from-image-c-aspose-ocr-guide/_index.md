---
category: general
date: 2026-05-06
description: 使用 Aspose OCR 在 C# 中将图像创建为可搜索的 PDF。学习将 PNG 转换为 PDF、从图像提取文本并生成可搜索的 PDF。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- convert png to pdf
- ocr image to pdf
language: zh
og_description: 使用 Aspose OCR 在 C# 中将图像创建为可搜索的 PDF。本分步教程展示了如何将 PNG 转换为 PDF、从图像中提取文本，并生成可搜索的
  PDF。
og_title: 从图像创建可搜索的 PDF – C# Aspose OCR 指南
tags:
- Aspose
- C#
- OCR
- PDF
title: 从图像创建可搜索的 PDF – C# Aspose OCR 指南
url: /zh/net/text-recognition/create-searchable-pdf-from-image-c-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像创建可搜索的 PDF – C# Aspose OCR 指南

是否曾需要从扫描的图片**创建可搜索的 PDF**，但不知从何入手？也许你有一张 PNG 收据、一张 JPEG 合同，或任何想要转换为可实际搜索的 PDF 的位图。这是一个常见的痛点，尤其是当你处理那些闲置在文件夹中的旧扫描件时。

好消息是，使用 Aspose OCR，你可以**将图像转换为 PDF**，提取隐藏的文本，最终得到一个完整可搜索的文档——只需几行 C# 代码。在本指南中，我们还将展示如何**将 png 转换为 PDF**、**从图像中提取文本**，甚至涵盖处理多页 TIFF 的特殊情况。完成后，你将拥有一个可自行部署的解决方案，能够直接嵌入任何 .NET 项目。

## 你需要的环境

- **.NET 6+**（代码同样适用于 .NET Framework 4.6+）
- **Visual Studio 2022** 或你喜欢的任何 IDE
- **Aspose.OCR** NuGet 包（它会自动引入 Aspose.PDF）
- 一张想要转换为可搜索 PDF 的图像文件（PNG、JPEG、BMP、TIFF）

无需额外的授权技巧，也不需要外部服务——只需一个 NuGet 引用和几分钟的编码。

## 步骤 1：安装 Aspose.OCR NuGet 包

首先，将库添加到你的项目中。打开 Package Manager Console 并运行：

```powershell
Install-Package Aspose.OCR
```

该单行命令会同时拉取 **Aspose.OCR** 和它依赖的 **Aspose.Pdf** 程序集，这样你就可以读取图像并写入 PDF 了。

> **技巧提示：** 如果你使用 .NET CLI，等价命令是 `dotnet add package Aspose.OCR`。

## 步骤 2：初始化 OCR 引擎

创建 `OcrEngine` 实例是进行所有 OCR 工作的入口。可以把它看作会观察你的图片并开始“读取”字符的大脑。

```csharp
using Aspose.OCR;
using Aspose.Pdf;   // pulled in by the OCR package

// Create an OCR engine instance – this object holds configuration and state
var ocrEngine = new OcrEngine();
```

你可能会想，*为什么不直接调用静态方法？* 面向对象的方式让你以后可以调整设置（语言、分辨率等），而无需更改整体流程。

## 步骤 3：加载要转换的图像

这里我们在精神上**将图像转换为 PDF**——通过将位图输入 OCR 引擎。将 `"YOUR_DIRECTORY/input.png"` 替换为实际文件路径。

```csharp
// Load the source image (PNG, JPEG, BMP, or multi‑page TIFF)
ocrEngine.SetImage("YOUR_DIRECTORY/input.png");
```

如果你有**将 png 转换为 pdf**的场景，只需指向 PNG 文件。对于多页 TIFF，Aspose.OCR 会自动将每一帧视为单独的页面。

## 步骤 4：运行 OCR 并可选获取文本

调用 `Recognize()` 完成繁重的工作：它分析图片，检测字符，并返回结构化结果。你可以保留文本用于日志、搜索索引或显示。

```csharp
// Perform OCR – this extracts the textual content from the image
var ocrResult = ocrEngine.Recognize();

// Optional: show the extracted text in the console
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

> **为什么要提取文本？** 即使我们会将其嵌入最终的 PDF，保留原始字符串仍然对验证或分析有用。

## 步骤 5：为可搜索文档配置 PDF 选项

Aspose.PDF 为我们提供了一个名为 **CreateSearchablePdf** 的特殊 `PdfSaveOptions` 模式。它指示库将 OCR 文本作为不可见层嵌入图像后面，使 PDF 可搜索。

```csharp
// Prepare PDF save options – this tells Aspose to embed OCR text
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();
```

如果你只需要普通的仅图像 PDF（没有隐藏文本），可以改用 `PdfSaveOptions.CreatePdf()`。但对于我们的目标——**创建可搜索的 PDF**——可搜索模式才是关键。

## 步骤 6：将可搜索的 PDF 保存到磁盘

现在我们把所有步骤串联起来。`SavePdf` 方法将图像和隐藏文本写入同一个文件。

```csharp
// Save the searchable PDF file
ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created successfully.");
```

此时，你已经拥有一个**可搜索的 PDF**，可以在 Adobe Reader 中打开，输入关键词进行搜索，即可瞬间跳转到匹配位置——即使可见页面仍然是原始图像。

## 完整工作示例

将所有代码组合在一起，这里提供一个可直接运行的控制台应用程序。复制粘贴到新的 C# 项目中，调整文件路径，然后按 **F5** 运行。

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf; // included automatically with Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image that contains the scanned document
        // Replace with your actual image path
        ocrEngine.SetImage("YOUR_DIRECTORY/input.png");

        // Step 3: Run the OCR process to extract text (optional but useful)
        var ocrResult = ocrEngine.Recognize();

        // Show extracted text – helpful for debugging
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("======================");

        // Step 4: Prepare to export the recognized content as a searchable PDF
        var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

        // Step 5: Save the searchable PDF to disk
        // Replace with your desired output path
        ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created successfully.");
    }
}
```

### 预期输出

运行程序时，控制台会显示类似以下内容：

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑04‑30
Total: $1,250.00
...
======================
Searchable PDF created successfully.
```

在 `YOUR_DIRECTORY` 中会生成 `output.pdf`。打开它，按 **Ctrl F**，输入 “Invoice”，即可直接跳转到该词——即使页面看起来像平面扫描。

## 处理常见变体

### 一次转换多张图片

如果文件夹中有大量 PNG 并希望生成单个可搜索的 PDF，可遍历文件并将每张图片作为单独页面添加：

```csharp
var allImages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
var ocrEngine = new OcrEngine();
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

foreach (var imgPath in allImages)
{
    ocrEngine.SetImage(imgPath);
    ocrEngine.Recognize(); // extracts text for the current page
    ocrEngine.SavePdf("temp_page.pdf", pdfOptions);

    // Merge temp_page.pdf into the final document (omitted for brevity)
}
```

你也可以使用 Aspose.PDF 的 `PdfFileEditor` 将临时 PDF 合并为一个最终文件。

### 处理低分辨率扫描

当图像 DPI 低于 150 时，OCR 准确率会下降。可以在输入图像前对其进行放大：

```csharp
ocrEngine.ImageProcessingOptions.Dpi = 300; // forces 300 DPI for better recognition
```

### 选择特定语言

如果文档不是英文，请在 `Recognize()` 之前设置语言：

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, etc.
```

这些调整可确保 **从图像中提取文本** 在各种场景下都能可靠工作。

## 可视化结果

![Searchable PDF created with Aspose OCR – create searchable PDF](https://example.com/images/searchable-pdf.png)

*上图展示了一个 PDF，图像可见，但文本层可被搜索。*

## 结论

现在，你已经拥有一个完整、可投入生产的配方，使用 Aspose OCR 和 C# 将任意图像**创建可搜索的 PDF**文件。我们介绍了如何**将图像转换为 PDF**、**从图像中提取文本**，并涉及了**将 png 转换为 pdf**和**ocr 图像转 pdf**的边缘情况。代码完全自包含，可在任何 .NET 运行时上运行，并可扩展为批处理或自定义语言支持。

接下来可以尝试添加水印、加密 PDF，或将提取的文本导入 Elasticsearch 等搜索索引。可能性无限，而相同的模式——加载 → 识别 → 保存——将适用于任何基于 OCR 的工作流。

如果遇到任何问题或有酷炫的使用案例想分享，请在下方留言。祝编码愉快，尽情把顽固的扫描件变成可搜索的金子吧！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}