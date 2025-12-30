---
date: 2025-12-30
description: 学习如何使用 Aspose.OCR 将图像转换为 PDF（C#），将多页 OCR 结果保存为文档，并使用 C# 从图像中提取文本。
linktitle: Convert Images to PDF C# – Save Multipage OCR Result
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

在本教程中，您将学习如何使用 Aspose.OCR for .NET **将图像转换为 PDF C#** 并将生成的多页 OCR 输出保存为文档。无论您是需要 **将扫描图像转换为 PDF** 以进行归档，还是 **从图像中提取文本 C#** 以进行数据处理，本指南都将一步步带您完成——并提供真实案例和最佳实践技巧。

## 快速答案
- **本教程涵盖什么内容？** 使用 Aspose.OCR 在 C# 中将多个图像转换为 PDF/Docx/Txt/Pdf/Xlsx。
- **支持哪些格式？** Docx、Text、Pdf 和 Xlsx（您也可以直接输出 PDF）。
- **我需要许可证吗？** 免费试用可用于评估；生产环境需要永久许可证。
- **兼容哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。
- **转换时可以提取文本吗？** 可以——在保存之前使用 OCR 结果提取文本。

## 什么是 “将图像转换为 PDF C#”？

在 C# 中将图像转换为 PDF 是指通过编程方式获取一个或多个位图文件（PNG、JPEG、TIFF 等），生成一个保留视觉布局的 PDF 文档，并可选择通过 OCR 嵌入可搜索的文本。Aspose.OCR 使此过程简洁且高度可定制。

## 为什么在此任务中使用 Aspose.OCR？

- **高精度** OCR 引擎，支持多种语言。
- **多页支持** – 在一次调用中处理批量图像。
- **直接保存** 为流行的办公格式，无需额外转换步骤。
- **完整的 .NET 集成** – 无本机依赖或外部工具。

## 前置条件

在开始之前，请确保您具备以下条件：

1. 安装 Aspose.OCR for .NET。您可以在[此处](https://releases.aspose.com/ocr/net/)下载。
2. 获取免费试用或购买许可证 – 在[此处](https://releases.aspose.com/)获取试用，或在[此处](https://purchase.aspose.com/buy)购买。
3. 查看官方[文档](https://reference.aspose.com/ocr/net/)，熟悉 API。
4. 加入[支持论坛](https://forum.aspose.com/c/ocr/16)社区，获取帮助。

现在一切准备就绪，让我们开始编码。

## 导入命名空间

在 C# 文件中添加所需的命名空间：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

这些导入让您可以使用集合、文件处理、LINQ 和 Aspose OCR 类。

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

创建 `AsposeOcr` 对象即可访问所有 OCR 操作，包括 **convert images to PDF C#** 工作流。

## 步骤 3：识别图像

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

`RecognizeMultipleImages` 方法处理列表中的每个文件，并返回 `RecognitionResult` 集合。您可以提供任意数量的图像，这对于 **convert scanned images to PDF** 场景非常适合。

## 步骤 4：以首选格式保存结果

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

选择最适合您后续工作流的格式：

- **Docx** – 可编辑的 Word 文档，带可搜索文本。
- **Text** – 纯文本提取，便于快速数据挖掘（**extract text from images C#**）。
- **Pdf** – 经典的 PDF 输出，适合归档。
- **Xlsx** – 电子表格形式，适用于表格数据。

## 常见使用场景

- **数字归档：** 将扫描的纸质合同转换为可搜索的 PDF。
- **数据录入自动化：** 从收据或发票中提取文本并写入数据库。
- **批量处理：** 使用最少代码在单个任务中处理数千张图像。

## 故障排除与技巧

- **大图像集：** 将图像分成较小批次处理，以避免内存激增。
- **图像质量：** 确保图像分辨率至少为 300 dpi，以获得最佳 OCR 精度。
- **许可证错误：** 在调用 OCR 方法前，确认许可证文件已正确加载。

## 常见问题解答（原文）

### Q1：是否提供用于测试的临时许可证？

A1：是的，您可以在[此处](https://purchase.aspose.com/temporary-license/)获取用于测试 Aspose.OCR 的临时许可证。

### Q2：我可以识别不同格式图像中的文本吗？

A2：当然！Aspose.OCR 支持多种图像格式，确保 OCR 任务的灵活性。

### Q3：对识别图像的数量有任何限制吗？

A3：可处理的图像数量取决于您的许可证。请查阅文档了解详情。

### Q4：如何处理 OCR 识别期间的错误？

A4：请参考文档中的错误处理最佳实践，或在支持论坛寻求帮助。

### Q5：Aspose.OCR 是否支持除英语之外的语言？

A5：是的，Aspose.OCR 支持多种语言。请查阅文档了解语言支持详情。

## 其他常见问题

**Q：我可以在不使用 OCR 的情况下将图像转换为 PDF C# 吗？**  
A：是的，您可以使用 Aspose.PDF 或其他库进行纯图像转 PDF 的转换，但 OCR 会添加可搜索的文本。

**Q：转换后，我如何从图像中提取文本 C#？**  
A：`RecognizeMultipleImages` 返回的 `result` 列表包含 `Text` 属性，您可以将其写入 `.txt` 文件或直接处理。

**Q：是否可以设置自定义页面边距或方向？**  
A：在保存为 PDF 或 Docx 时，您可以在调用 `SaveMultipageDocument` 之前，通过 Aspose.Words 或 Aspose.PDF API 修改文档布局。

**Q：如果图像无法读取会怎样？**  
A：OCR 引擎会为该页返回一个空的 `RecognitionResult`；您可以检查 `result[i].Text` 是否为 null 或空字符串，并相应处理。

**Q：API 是否支持云部署？**  
A：是的，只要运行时满足版本要求，该库即可在任何 .NET 运行时上运行，包括 Azure Functions 和 AWS Lambda。

---

**最后更新：** 2025-12-30  
**测试环境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}