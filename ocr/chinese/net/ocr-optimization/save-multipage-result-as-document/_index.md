---
date: 2026-04-29
description: 学习如何使用 Aspose.OCR 将图像转换为 PDF（C#），将多页 OCR 结果保存为文档，并使用 C# 从图像中提取文本。
keywords:
- convert images to pdf
- extract text from images
- c# ocr library
- convert images to xlsx
- generate pdf from tiff
linktitle: 将图像转换为 PDF（C#）— 保存多页 OCR 结果
second_title: Aspose.OCR .NET API
title: 将图像转换为 PDF C# – 保存多页 OCR 结果
url: /zh/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将图像转换为 PDF C# – 保存多页 OCR 结果

## 介绍

在本教程中，您将学习如何使用强大的 **Aspose.OCR** .NET 库 **convert images to PDF C#**。无论您是需要 **convert scanned TIFF files to searchable PDFs**、从图像中提取文本进行数据挖掘，还是从一批图片生成 Excel 工作簿，本指南都将通过清晰的解释、实际技巧和最佳实践建议，逐步带您完成每个环节。

## 快速答案
- **What does this tutorial cover?** 使用 Aspose.OCR 在 C# 中将多个图像转换为 PDF、Docx、Text 和 Xlsx，并将 OCR 结果保存为多页文档。  
- **Which output formats are supported?** 支持的输出格式有 Docx、Text、Pdf 和 Xlsx（也可以直接输出 PDF）。  
- **Do I need a license?** 免费试用可用于评估；生产环境需要永久许可证。  
- **What .NET versions are compatible?** 兼容的 .NET 版本包括 .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。  
- **Can I extract text while converting?** 可以——在保存之前使用 OCR 结果提取可搜索的文本。

## 什么是 “convert images to PDF C#”？

在 C# 中将图像转换为 PDF 是指以编程方式获取一个或多个位图文件（PNG、JPEG、TIFF 等），生成一个保留视觉布局的 PDF 文档，并可选择通过 OCR 嵌入可搜索的文本。Aspose.OCR 提供了一个 **c# ocr library**，能够端到端处理此过程，包括多页支持以及直接保存为流行的办公格式。

## 为什么在此任务中使用 Aspose.OCR？

- **High‑accuracy OCR** 支持数十种语言。  
- **Multipage processing** – 将整个文件夹的图像输入，即可生成单个可搜索的 PDF。  
- **Direct export** 直接导出为 Docx、Text、Pdf 和 Xlsx，无需二次转换。  
- **Pure .NET** – 无本地依赖，可在 Windows、Linux 以及云运行时上运行。  

## 先决条件

1. 安装 Aspose.OCR for .NET。您可以在 [here](https://releases.aspose.com/ocr/net/) 下载。  
2. 获取免费试用或购买许可证 – 在 [here](https://releases.aspose.com/) 获取试用，或在 [here](https://purchase.aspose.com/buy) 购买。  
3. 阅读官方 [documentation](https://reference.aspose.com/ocr/net/) 以熟悉 API。  
4. 加入社区的 [support forums](https://forum.aspose.com/c/ocr/16) 获取帮助。  

现在一切准备就绪，让我们开始编码。

## 导入命名空间

首先在 C# 文件中添加所需的命名空间：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

这些导入使您能够使用集合、文件处理、LINQ 以及 Aspose OCR 类。

## 步骤 1：设置文档目录

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

将 `"Your Document Directory"` 替换为源图像所在的绝对或相对路径，以及您希望保存输出文件的路径。

## 步骤 2：初始化 Aspose.OCR

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

创建 `AsposeOcr` 对象后，您即可访问所有 OCR 操作，包括 **convert images to PDF C#** 工作流。

## 步骤 3：识别图像

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

`RecognizeMultipleImages` 方法处理列表中的每个文件，并返回 `RecognitionResult` 集合。您可以提供任意数量的图像，这对于 **convert scanned images to PDF** 场景非常合适。

## 步骤 4：以首选格式保存结果

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

选择最适合您后续工作流的格式：

- **Docx** – 可编辑的 Word 文档，包含可搜索的文本。  
- **Text** – 纯文本提取，便于快速数据挖掘（**extract text from images**）。  
- **Pdf** – 经典的 PDF 输出，适合归档。  
- **Xlsx** – 表格数据的电子表格表示（**convert images to xlsx**）。

## 如何将图像转换为 PDF C# – 步骤回顾

1. **Prepare the folder** 包含您想要转换的图像的文件夹。  
2. **Create an `AsposeOcr` instance** 以访问 OCR 功能。  
3. **Call `RecognizeMultipleImages`** 获取每个文件的 OCR 结果。  
4. **Save the multipage result** 使用 `SaveMultipageDocument` 以所需格式保存多页结果。

## 常见用例

- **Digital archiving:** 将扫描的纸质合同转换为可搜索的 PDF。  
- **Data entry automation:** 从收据或发票中提取文本并导入数据库。  
- **Batch processing:** 使用最少的代码在单个作业中处理数千张图像。  
- **Generate PDF from TIFF:** 适用于需要保持原始高分辨率扫描文档的情况。  

## 故障排除与技巧

- **Large image sets:** 将图像分成更小的批次处理，以避免内存激增。  
- **Image quality:** 确保图像分辨率至少为 300 dpi，以获得最佳 OCR 准确度。  
- **License errors:** 在调用 OCR 方法前，确认许可证文件已正确加载。  
- **Empty results:** 如果图像无法读取，相应的 `RecognitionResult` 的 `Text` 属性将为空——在保存前检查是否为 null 或空字符串。  

## 常见问题

**Q: 我可以在不使用 OCR 的情况下将图像转换为 PDF C# 吗？**  
A: 是的，您可以使用 Aspose.PDF 或其他库进行纯图像转 PDF 的转换，但 OCR 会添加可搜索的文本，使 PDF 更加有用。

**Q: 转换后，我如何在 C# 中从图像提取文本？**  
A: `RecognizeMultipleImages` 返回的 `result` 列表为每页包含 `Text` 属性。您可以将这些字符串写入 `.txt` 文件，或直接在应用程序中处理。

**Q: 是否可以设置自定义页面边距或方向？**  
A: 可以——在保存为 PDF 或 Docx 之前，您可以通过 Aspose.Words 或 Aspose.PDF API 修改文档布局，然后再调用 `SaveMultipageDocument`。

**Q: 如果图像无法读取会怎样？**  
A: OCR 引擎会为该页返回空的 `RecognitionResult`；您可以检测到后跳过或记录有问题的文件。

**Q: API 是否支持云部署？**  
A: 是的，只要运行时满足版本要求，该库即可在任何 .NET 运行时上工作，包括 Azure Functions 和 AWS Lambda。

## 结论

您现在拥有完整的、可投入生产的工作流，可 **convert images to PDF C#**，提取可搜索的文本，甚至从一批图片生成 Word、纯文本或 Excel 文件。欢迎尝试不同的输出格式，为特定语言调整 OCR 设置，或将代码集成到更大的文档处理流水线中。

---

**最后更新:** 2026-04-29  
**测试环境:** Aspose.OCR 24.11 for .NET  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}