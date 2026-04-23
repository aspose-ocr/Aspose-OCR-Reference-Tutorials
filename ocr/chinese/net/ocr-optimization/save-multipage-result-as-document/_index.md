---
date: 2026-04-23
description: 学习如何使用 Aspose.OCR 将图像转换为 PDF（C#），将多页 OCR 结果保存为文档，并从图像中提取文本。
keywords:
- extract text from images
- batch image to pdf
- convert scanned images pdf
linktitle: 将图像转换为 PDF C# – 保存多页 OCR 结果
second_title: Aspose.OCR .NET API
title: 从图像中提取文本 – 将图像转换为 PDF（C#）
url: /zh/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本 – 将图像转换为 PDF C#

## 介绍

在本教程中，您将学习如何使用 Aspose.OCR for .NET **从图像中提取文本** 并 **将图像转换为 PDF C#**，随后将多页 OCR 结果保存为文档。无论您是需要 **批量图像转 PDF** 进行归档，还是 **将扫描图像转换为 PDF** 以满足合规要求，亦或仅仅从图片中提取可搜索的文本，我们都会通过清晰的解释、实际案例提示和最佳实践建议，逐步演示每一步操作。

## 快速回答
- **本教程涵盖什么？** 将多个图像转换为 PDF/Docx/Txt/Xlsx，并使用 Aspose.OCR 在 C# 中从图像中提取文本。  
- **支持哪些输出格式？** Docx、Text、Pdf 和 Xlsx（也可以直接输出 PDF）。  
- **我需要许可证吗？** 免费试用可用于评估；生产环境需要永久许可证。  
- **兼容哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。  
- **我可以在转换时提取文本吗？** 可以——在保存之前使用 OCR 结果提取文本。

## 什么是“从图像中提取文本”，以及为何将其与 PDF 转换相结合？

从图像中提取文本是指使用 OCR（光学字符识别）将可视字符转换为可搜索、可编辑的字符串。当您 **将图像转换为 PDF C#** 时，会将这些字符串嵌入 PDF 中，使文档可搜索、可索引——这对于数字归档和数据挖掘非常理想。

## 为什么在此任务中使用 Aspose.OCR？

- **高精度**，支持数十种语言。  
- **多页支持** —— 在一次调用中处理批量图像（适用于 **批量图像转 PDF** 场景）。  
- **直接保存** 为流行的办公格式，无需额外转换步骤。  
- **完整的 .NET 集成** —— 无本机依赖，可在 Windows、Linux 以及云运行时上运行。

## 前置条件

在开始之前，请确保您已具备以下条件：

1. 已安装 Aspose.OCR for .NET。您可以在[此处](https://releases.aspose.com/ocr/net/)下载。  
2. 获取了免费试用或已购买许可证 —— 在[此处](https://releases.aspose.com/)获取试用，或在[此处](https://purchase.aspose.com/buy)购买。  
3. 阅读官方[文档](https://reference.aspose.com/ocr/net/)，熟悉 API。  
4. 加入[支持论坛](https://forum.aspose.com/c/ocr/16)社区，以获取帮助。  

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

这些导入让您可以使用集合、文件处理、LINQ 以及 Aspose OCR 类。

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

创建 `AsposeOcr` 对象后，您即可访问所有 OCR 操作，包括 **将图像转换为 PDF C#** 工作流。

## 步骤 3：识别图像

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

`RecognizeMultipleImages` 方法会处理列表中的每个文件，并返回 `RecognitionResult` 集合。您可以提供任意数量的图像，这对于 **将扫描图像转换为 PDF** 场景非常适合。

## 步骤 4：以首选格式保存结果

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

选择最适合您后续工作流的格式：

- **Docx** – 可搜索文本的可编辑 Word 文档。  
- **Text** – 用于快速数据挖掘的纯文本提取（**从图像中提取文本**）。  
- **Pdf** – 经典的 PDF 输出，适合归档。  
- **Xlsx** – 用于表格数据的电子表格表示。

## 常见使用场景

- **数字归档：** 将扫描的纸质合同转换为可搜索的 PDF。  
- **数据录入自动化：** 从收据或发票中提取文本并写入数据库。  
- **批量处理：** 使用最少的代码在单个作业中处理数千张图像——非常适合 **批量图像转 PDF** 的需求。

## 故障排除与提示

- **大批量图像：** 将图像分成较小批次处理，以避免内存激增。  
- **图像质量：** 确保图像分辨率至少为 300 dpi，以获得最佳 OCR 精度。  
- **许可证错误：** 在调用 OCR 方法前，确认许可证文件已正确加载。  
- **空结果：** 对于不可读的页面，OCR 引擎会返回空的 `RecognitionResult`；请检查 `result[i].Text` 是否为 null 或空字符串，并相应处理。

## 常见问题

**问：我可以在不使用 OCR 的情况下将图像转换为 PDF C# 吗？**  
答：可以，您可以使用 Aspose.PDF 或其他库进行纯图像转 PDF 的转换，但 OCR 会添加可搜索的文本。

**问：转换后，我如何在 C# 中从图像中提取文本？**  
答：`RecognizeMultipleImages` 返回的 `result` 列表包含 `Text` 属性，您可以将其写入 `.txt` 文件或直接处理。

**问：是否可以设置自定义页面边距或方向？**  
答：在保存为 PDF 或 Docx 时，您可以在调用 `SaveMultipageDocument` 之前，通过 Aspose.Words 或 Aspose.PDF API 修改文档布局。

**问：如果图像无法读取会怎样？**  
答：OCR 引擎会为该页返回空的 `RecognitionResult`；您可以检查 `result[i].Text` 是否为 null 或空字符串，并相应处理。

**问：API 是否支持云部署？**  
答：是的，该库可在任何 .NET 运行时上工作，包括 Azure Functions 和 AWS Lambda，只要运行时满足版本要求。

---

**最后更新：** 2026-04-23  
**测试版本：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}