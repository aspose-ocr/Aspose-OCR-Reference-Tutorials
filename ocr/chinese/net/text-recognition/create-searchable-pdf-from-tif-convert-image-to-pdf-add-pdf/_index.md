---
category: general
date: 2026-04-04
description: 在 C# 中从 TIF 图像创建可搜索的 PDF —— 学习如何将图像转换为 PDF，添加 PDF 元数据，并使用 Aspose.OCR
  生成可搜索的文档。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: zh
og_description: 使用 C# 从 TIF 文件创建可搜索的 PDF。将图像转换为 PDF，添加 PDF 元数据，并使用 Aspose.OCR 生成可搜索的文档。
og_title: 将 TIF 转换为可搜索 PDF – 步骤指南
tags:
- Aspose.OCR
- C#
- PDF generation
title: 从 TIF 创建可搜索 PDF – 将图像转换为 PDF，添加 PDF 元数据
url: /zh/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 TIF 创建可搜索 PDF – 完整 C# 演练

是否曾需要从扫描的发票 **创建可搜索 PDF**，但不确定如何保持文本可搜索且文件元数据整洁？您并不孤单。在许多自动化项目中，PDF 必须既可机器读取，又要正确标记诸如标题、作者和置信阈值等信息。  

在本指南中，我们将演示一个完整的解决方案，**将图像转换为 PDF**，注入 **PDF 元数据**，并过滤低置信度的 OCR 结果——全部使用 Aspose.OCR 库。完成后，您将拥有一个可直接放入任何 .NET 项目的代码片段，以及处理边缘情况的一些技巧。

## 前提条件

- .NET 6.0 或更高（代码同样适用于 .NET Framework 4.6+）  
- Aspose.OCR NuGet 包 (`Install-Package Aspose.OCR`)  
- 您想要转换为可搜索 PDF 的 TIF 图像（例如 `input.tif`）  
- 对 C# 和 Visual Studio（或您喜欢的 IDE）有基本了解  

不需要其他外部服务——整个过程在本地运行。

## 第一步 – 设置 OCR 引擎（创建可搜索 PDF 核心）

我们首先需要一个能够识别语言的 `OcrEngine` 实例。在大多数业务场景中，英语已足够，但您可以将 `Language.English` 替换为任何受支持的语言。

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**为什么这很重要：** OCR 引擎负责将光栅像素转换为 Unicode 文本。正确设置语言可提升准确率，并减少后续被过滤的低置信度词汇。

> **专业提示：** 如果处理多语言文档，请实例化多个引擎或使用 `Language.Multilingual` 让 Aspose 自动进行语言检测。

## 第二步 – 加载 TIF 图像（从 TIF 创建 PDF）

现在我们将引擎指向源文件。`ImageStream.FromFile` 辅助方法将图像读取为 OCR 引擎可消费的流。

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

您可能会想，*“我可以使用 JPEG 或 PNG 吗？”* 当然可以——Aspose.OCR 支持大多数光栅格式。只需更改文件扩展名即可。

## 第三步 – 配置 PDF 选项（向 PDF 添加元数据）

在转换之前，我们定义一个 `PdfOptions` 对象。在这里我们 **添加 PDF 元数据**（如标题和作者），并指示引擎删除置信度低于阈值的词。

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**这里发生了什么？**  
- `Title` 和 `Author` 成为 PDF 文档信息字典的一部分，使文件在文档管理系统中更易于索引。  
- `MinConfidence` 是一道防护栏：OCR 常误读模糊字符；过滤它们可保持可搜索层干净，并提升后续文本提取的效果。

如果需要自定义元数据（例如 `Subject`、`Keywords`），可以通过 `PdfOptions.CustomProperties` 设置。

## 第四步 – 将图像转换为可搜索 PDF（将图像转换为 PDF）

在引擎准备就绪并设置好选项后，最后的调用执行转换。它将可搜索的 PDF 写入磁盘，在原始图像下嵌入 OCR 文本层。

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

此行执行后，`output.pdf` 包含：  
- 原始 TIF 图像作为可视背景  
- 搜索引擎和复制粘贴操作可读取的不可见文本层  
- 我们之前定义的元数据（标题、作者等）

### 预期结果

在 Adobe Reader 或任意 PDF 查看器中打开生成的 PDF 并尝试选择文本。您应该能够复制与原始扫描相匹配的句子。文档的 **Properties** 对话框会显示标题 “Invoice #12345” 和作者 “MyCompany”。

## 第五步 – 验证置信度过滤（为何 MinConfidence 有帮助）

确认低置信度词已被移除是有用的。您可以使用 `pdftotext` 等工具检查 PDF 的隐藏文本：

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

如果该词根本未出现，则 `MinConfidence` 过滤器按预期工作。如需更严格或更宽松的过滤，可调整阈值（例如 `0.7f`）。

## 第六步 – 处理多页（从多页 TIF 创建可搜索 PDF）

许多发票是多页 TIFF。Aspose.OCR 会自动将每帧视为单独的页面。只需将引擎指向多页文件；相同的 `ConvertToSearchablePdf` 调用将生成多页可搜索 PDF。

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**边缘情况：** 如果页面为空白，OCR 仍可能生成空的文本层，但这无害。不过，您可以在转换前通过检查 `ocrEngine.HasText` 来跳过空白页。

## 第七步 – 打包完整示例（所有步骤合并）

下面是一个可直接运行的完整程序，将所有内容整合在一起。将 `YOUR_DIRECTORY` 替换为您机器上的实际文件夹路径。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

运行程序（`dotnet run` 或在 Visual Studio 中按 **F5**）即可看到确认信息。生成的 PDF 与源图像位于同一目录，随时可用于索引或归档。

## 常见问题与注意事项

| Question | Answer |
|----------|--------|
| **我可以向可搜索层添加自定义字体吗？** | OCR 层使用 Unicode；视觉外观由底层图像决定，因此无需额外嵌入字体。 |
| **如果我的 TIF 是彩色的怎么办？** | Aspose.OCR 会自动将彩色图像转换为灰度进行 OCR，但通过设置 `PdfOptions.PreserveColor = true` 可以在 PDF 中保留原始颜色。 |
| **该库是线程安全的吗？** | 每个 `OcrEngine` 实例应由单个线程使用。若进行并行处理，请为每个线程创建单独的引擎。 |
| **如何加密 PDF？** | 在 OCR 转换后，使用 `PdfOptions.Security` 设置密码和权限即可。 |

## 后续步骤（扩展您的 PDF 工具箱）

- **批量处理：**遍历 TIFF 文件夹，为每个文件生成可搜索 PDF。  
- **后处理：**使用 Aspose.PDF 将生成的 PDF 合并为单个主文档。  
- **高级元数据：**填充自定义 XMP 字段，以更好地集成到 SharePoint 或 ECM 系统中。  

所有这些扩展都基于我们刚刚介绍的核心模式：**创建可搜索 PDF**、**将图像转换为 PDF**，以及 **添加 PDF 元数据**。

---

*祝编码愉快！如果遇到任何问题，请在下方留言或查阅 Aspose.OCR 文档获取最新 API 更新。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}