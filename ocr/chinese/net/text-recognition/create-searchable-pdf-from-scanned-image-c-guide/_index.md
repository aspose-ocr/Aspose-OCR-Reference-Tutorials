---
category: general
date: 2026-04-26
description: 使用 Aspose OCR 在 C# 中将扫描图像创建为可搜索的 PDF。了解如何快速转换扫描图像、提取文本并生成可搜索的 PDF。
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: zh
og_description: 使用 Aspose OCR 将扫描图像创建为可搜索的 PDF。逐步的 C# 代码实现转换、提取文本并生成可搜索的 PDF。
og_title: 从扫描图像创建可搜索的 PDF – C# 指南
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: 将扫描图像转换为可搜索的 PDF – C# 指南
url: /zh/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 将扫描图像转换为可搜索 PDF

是否曾需要 **创建可搜索的 PDF** 文件来处理纸质合同、收据或旧档案？你并不孤单——大多数开发者在客户交付一堆 TIFF 扫描件并要求交付可搜索 PDF 时都会遇到这个难题。

在本教程中，我们将展示 **如何对文档进行 OCR**，并使用 Aspose OCR for .NET 将扫描图像转换为 **可搜索的 PDF**。完成后，你将能够 **转换扫描图像** 文件、**从图像中提取文本**，甚至轻松处理多页 TIFF。

## 所需环境

在开始之前，请确保你具备以下条件：

* .NET 6.0 或更高版本（API 兼容 .NET Core、.NET Framework 和 .NET 5+）。  
* 有效的 Aspose OCR 许可证，或接受评估水印。  
* 已安装 `Aspose.OCR` NuGet 包（`dotnet add package Aspose.OCR`）。  
* 一个示例 TIFF 文件（例如 `contract_scan.tif`），用于转换为可搜索 PDF。

就这些——无需额外库，也不需要复杂配置。准备好了吗？让我们开始吧。

![创建可搜索 PDF 示例](create-searchable-pdf.png "创建可搜索 PDF 示例")

## 第一步 – 初始化 OCR 引擎（创建可搜索 PDF）

首先，需要一个 `OcrEngine` 实例。该对象负责读取位图、识别字符并返回文本。  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**为什么要设置语言？**  
如果保持默认，Aspose 会尝试所有语言包，这会降低速度。指定 `Language.Latin` 可让引擎专注于拉丁字母，提升速度并在英文合同中获得更准确的结果。

## 第二步 – 加载扫描图像（转换扫描图像）

现在把要处理的图像传给引擎。Aspose 可以读取文件路径、流，甚至 `byte[]`。这里为简便使用 `ImageStream.FromFile`。  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

如果以后需要 **将 TIFF 转换为 PDF**，请记住多页 TIFF 会自动处理——每一帧都会成为 PDF 的单独页面。

## 第三步 – 执行 OCR 并获取文本（从图像中提取文本）

执行 OCR 只需调用 `Recognize`。引擎会返回一个 `RecognitionResult`，其中包含纯文本、置信度分数和布局信息。  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**小技巧：**如果只需要文本（不需要 PDF），可以在此停止，并将 `extractedText` 写入 `.txt` 文件。但大多数情况下我们的目标是可搜索 PDF，所以继续后面的步骤。

## 第四步 – 保存为可搜索 PDF（创建可搜索 PDF）

Aspose 让最后一步变得非常简单：只需使用 `SaveFormat.PdfSearchable` 调用 `Save`。库会在保留原始图像外观的同时，将提取的文本嵌入为不可见层。  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

在任意 PDF 查看器中打开 `contract_searchable.pdf`，即可选中、复制并搜索文本——这正是客户对 “可搜索 PDF” 的期望。

## 处理多页 TIFF（将 Tiff 转换为 PDF）

如果源文件包含多页，Aspose 会自动将每帧视为单独页面，无需额外循环。不过，你可能想为每页控制 DPI 或图像质量：

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

设置完这些选项后，重复 **步骤 2** 处理每一帧，或直接将 `ImageStream.FromFile` 指向多页 TIFF，让 Aspose 完成所有工作。

## 常见问题及解决方案

| 症状 | 可能原因 | 解决办法 |
|------|----------|----------|
| 文本乱码或缺失 | 语言设置错误 | 将 `ocrEngine.Language` 设置为正确的语言包（例如 `Language.German`）。 |
| PDF 文件过大（单页扫描 10 MB） | 默认图像压缩率低 | 将 `ocrEngine.ImageProcessingOptions.Compression` 调整为 `Jpeg`，并设置合适的 `Quality` 值（0‑100）。 |
| OCR 运行非常慢 | 使用默认的 `Auto` 语言检测 | 明确设置预期的语言。 |
| 没有可搜索层 | 使用 `SaveFormat.Pdf` 而非 `PdfSearchable` 保存 | 使用 `PdfSearchable`。 |

## 完整端到端示例

下面是一个可直接复制到 Visual Studio 的完整控制台应用示例：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**运行后你会看到：**  
* 控制台窗口打印出 OCR 识别的文本片段。  
* 在原始 TIFF 同目录下生成 `contract_searchable.pdf`。打开后，按 **Ctrl + F** 搜索原始扫描中出现的任意单词——效果即现。

## 后续步骤与相关主题

* **如何批量 OCR 文档** – 将上述代码包装在 `foreach` 循环中，处理整个文件夹。  
* **转换除 TIFF 之外的扫描图像格式**（PNG、JPEG） – 同样的 API 可用，只需更改文件扩展名。  
* **从图像中提取文本** 进行进一步分析 – 将 `result.Text` 输入自然语言处理流水线。  
* **优化 PDF 大小** – 探索 `PdfSaveOptions` 进一步压缩图像或仅在需要时嵌入字体。  

尝试这些思路，你很快就会成为处理 “将扫描件转换为可搜索 PDF” 请求的首选专家。

---

### TL;DR

现在你已经掌握了使用 Aspose OCR 在 C# 中 **创建可搜索 PDF** 文件的完整流程。步骤为：初始化引擎、加载图像、执行 OCR、使用 `PdfSearchable` 保存。通过调整语言设置、DPI 和压缩选项，可应对各种边缘情况，进而实现 **转换扫描图像**、**从图像中提取文本**，甚至大规模 **将 TIFF 转换为 PDF**。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}