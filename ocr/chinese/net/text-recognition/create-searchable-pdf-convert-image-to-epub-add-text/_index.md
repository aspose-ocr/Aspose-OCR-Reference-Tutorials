---
category: general
date: 2026-03-13
description: 使用 Aspose OCR 将任意图像转换为可搜索的 PDF。了解如何将图像转换为 EPUB、添加可搜索文本，并在 C# 中生成可搜索的
  PDF。
draft: false
keywords:
- create searchable pdf
- convert image to epub
- ocr image to pdf
- add searchable text
- generate searchable pdf
language: zh
og_description: 使用 Aspose OCR 将任意图像转换为可搜索的 PDF。本指南展示了如何将图像转换为 EPUB、添加可搜索的文本，以及在 C#
  中生成可搜索的 PDF。
og_title: 创建可搜索的PDF – 将图像转换为EPUB并添加文本
tags:
- Aspose OCR
- C#
- PDF
- EPUB
title: 创建可搜索的 PDF – 将图像转换为 EPUB 并添加文本
url: /zh/net/text-recognition/create-searchable-pdf-convert-image-to-epub-add-text/
---

.

Continue.

Make sure to keep bold formatting.

Proceed through all sections.

Tables: translate column headers and content.

Code block placeholders remain.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建可搜索的 PDF – 将图像转换为 EPUB 并添加文本

想要 **从扫描的收据或任意图像创建可搜索的 PDF** 吗？在本教程中，我们将展示如何使用 Aspose OCR 创建可搜索的 PDF，同时 **将图像转换为 EPUB** 并 **添加可搜索的文本层**——全部在一个 C# 项目中完成。

如果你曾经为外观不错却无法搜索的 PDF 而苦恼，你并不孤单。好消息是，隐藏的文本层可以将平面图像变成完整可搜索的文档，而 Aspose 让这几乎毫不费力。

## 你将学到

* 如何初始化 Aspose OCR 引擎并设置语言。  
* 将 **图像转换为 EPUB** 以进行电子书分发的完整步骤。  
* 如何配置 PDF 写入器，使输出包含隐藏的、可搜索的文本层。  
* 处理多页收据或非英文语言等边缘情况的技巧。  

你只需要事先准备一个 .NET 开发环境（Visual Studio 2022 或更高）和 Aspose OCR NuGet 包。无需外部服务、也不需要晦涩的配置文件——只需可以直接复制粘贴并运行的纯 C# 代码。

## 前置条件

| 要求 | 为什么重要 |
|-------------|----------------|
| .NET 6.0+   | Aspose OCR 目标是 .NET Standard 2.0+，使用 .NET 6 可获得最新的运行时改进。 |
| Aspose.OCR NuGet 包 | 提供代码中使用的 `OcrEngine`、`EpubWriter` 和 `PdfWriter` 类。 |
| 一张图像文件（例如 `receipt.jpg`） | OCR 将对其进行识别。任何光栅图像（PNG、JPEG、BMP）均可。 |
| 基础 C# 知识 | 你只需阅读并微调代码片段，而不是从零学习语言。 |

你可以使用以下命令安装该包：

```bash
dotnet add package Aspose.OCR
```

> **专业提示：** 如果你使用 Visual Studio，NuGet 包管理器 UI 也能完成同样的操作——只需搜索 “Aspose.OCR”。

## 步骤 1 – 使用 Aspose OCR 创建可搜索的 PDF

首先需要一个 `OcrEngine` 实例来指明要识别的语言。默认是英文，但你可以通过设置 `ocrEngine.Language` 替换为法文、德文等。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialise the OCR engine and set the language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English          // Change this if your document isn’t English
};
```

为什么要先初始化引擎？引擎会在内存中保存识别模型，创建一次后在多张图像之间复用可以节省 CPU 和内存。在大批量作业中，你会让同一个实例在整个运行期间保持存活。

## 步骤 2 – 加载图像并执行 OCR

接下来将引擎指向我们要处理的文件。`ImageStream.FromFile` 会把图像读取为 OCR 引擎能够理解的格式。

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Run the recognition engine – this populates the internal text buffer
ocrEngine.Recognize();
```

> **如果图像是多页的怎么办？**  
> Aspose OCR 能直接处理多页 TIFF。只需传入 TIFF 文件的路径，引擎会自动遍历每一页。

## 步骤 3 – 将图像转换为 EPUB

如果你还需要扫描文档的电子书版本，Aspose 只需一行代码即可完成。`EpubWriter` 使用同一个 `OcrEngine` 实例，这意味着 OCR 结果会被复用，无需额外处理。

```csharp
// Export the recognised content to an ePub file
EpubWriter epubWriter = new EpubWriter();
epubWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt.epub");
```

为什么要导出为 EPUB？EPUB 是可重排的格式——非常适合移动阅读器。OCR 文本可以被选中，原始图像则作为背景保留，保持原始扫描的外观。

## 步骤 4 – 为 PDF 添加可搜索的文本层

下面这一步才是真正 **创建可搜索 PDF** 的关键。通过启用 `AddSearchableTextLayer`，PDF 写入器会嵌入一个与 OCR 输出相对应的不可见文本层。用户可以像在普通 PDF 中一样搜索、复制或高亮文本。

```csharp
// Configure PDF writer to include a hidden searchable text layer
PdfWriter pdfWriter = new PdfWriter
{
    AddSearchableTextLayer = true   // Enables the hidden text layer for searchability
};

// Save the OCR result as a searchable PDF
pdfWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt_searchable.pdf");
```

> **常见陷阱：** 忘记设置 `AddSearchableTextLayer` 会导致生成的 PDF 看起来一样，但实际上没有可搜索的文本。需要可搜索文档时务必检查此标志。

## 步骤 5 – 完整工作示例

将所有内容组合在一起，下面是一个可直接放入新 .NET 项目并立即运行的完整控制台应用示例。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace OcrToPdfAndEpub
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the source image
            string imagePath = "YOUR_DIRECTORY/receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            ocrEngine.Recognize();

            // 4️⃣ Convert to EPUB (optional but handy)
            EpubWriter epubWriter = new EpubWriter();
            string epubPath = "YOUR_DIRECTORY/receipt.epub";
            epubWriter.Save(ocrEngine, epubPath);
            Console.WriteLine($"EPUB saved to {epubPath}");

            // 5️⃣ Create searchable PDF
            PdfWriter pdfWriter = new PdfWriter
            {
                AddSearchableTextLayer = true
            };
            string pdfPath = "YOUR_DIRECTORY/receipt_searchable.pdf";
            pdfWriter.Save(ocrEngine, pdfPath);
            Console.WriteLine($"Searchable PDF saved to {pdfPath}");
        }
    }
}
```

### 预期输出

* `receipt.epub` – 可在 Calibre、Apple Books 或任意电子阅读器中打开的 EPUB 文件。  
* `receipt_searchable.pdf` – 一个可以使用 **Ctrl + F** 查找原始图像中出现的任意单词的 PDF。

如果在 Adobe Acrobat 中打开该 PDF 并查看 **文件 → 属性 → 描述**，你会在 **字体** 选项卡下看到一个隐藏的文本流，证明可搜索层已经存在。

## 常见问题与边缘情况

**问：这能处理非英文语言吗？**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}