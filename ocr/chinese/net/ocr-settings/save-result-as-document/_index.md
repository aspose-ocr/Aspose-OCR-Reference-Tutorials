---
date: 2026-06-29
description: 了解如何使用 Aspose.OCR for .NET 保存 OCR 结果——一步步指南，教您保存 OCR 输出、将图像转换为可搜索的 PDF、从
  PNG 提取文本，并导出为 DOCX、TXT、PDF 或 XLSX。
keywords:
- how to save ocr
- image to searchable pdf
- extract text from png
- create searchable pdf
- ocr result to txt
linktitle: 如何将 OCR 结果保存为文档
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Learn how to save OCR results with Aspose.OCR for .NET – a step‑by‑step
    guide on how to save ocr output, convert image to searchable pdf, extract text
    from png, and export to DOCX, TXT, PDF, or XLSX.
  headline: How to Save OCR Result as Document
  type: TechArticle
- description: Learn how to save OCR results with Aspose.OCR for .NET – a step‑by‑step
    guide on how to save ocr output, convert image to searchable pdf, extract text
    from png, and export to DOCX, TXT, PDF, or XLSX.
  name: How to Save OCR Result as Document
  steps:
  - name: Initialize Aspose.OCR
    text: AsposeOcr is the primary class that performs OCR operations. Set the path
      to your working directory and create an instance of the OCR engine.
  - name: Recognize Image
    text: RecognitionResult holds the text and layout information extracted from the
      image. Pass the image file (e.g., a PNG) to the recognizer. This is where we
      **recognize text images** and turn them into a `RecognitionResult`.
  - name: Save Result in Different Formats
    text: Now we export the recognized text. Choose the format that fits your workflow—whether
      you need to **convert image to searchable pdf**, **extract text from png**,
      or generate a spreadsheet.
  - name: Display Success Message
    text: A simple console message confirms that the process completed without errors.
  type: HowTo
- questions:
  - answer: It refers to persisting the text recognized from an image into a file
      format like DOCX, PDF, etc.
    question: What does “how to save ocr” mean?
  - answer: DOCX, TXT, PDF, and XLSX are supported out‑of‑the‑box.
    question: Which formats can I export to?
  - answer: A free trial works for evaluation; a commercial license is required for
      production use.
    question: Do I need a license?
  - answer: Yes—save the OCR result as PDF to get a searchable PDF document.
    question: Can I convert image to PDF directly?
  - answer: Absolutely; you can **extract text from PNG** images with the same API.
    question: Is PNG supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
title: 如何将 OCR 结果保存为文档
url: /zh/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何将 OCR 结果保存为文档

## 介绍

在本教程中，您将了解如何使用 Aspose.OCR for .NET 保存 OCR 输出。我们将演示如何识别图像中的文本，然后将该文本转换为常见的文档格式，如 DOCX、TXT、PDF 和 XLSX。完成后，您将能够自动从图片中提取数据并将其存储为可搜索、可编辑的文件——非常适合归档、报告或后续处理。

## 快速答复
- **“how to save ocr” 是什么意思？** 它指的是将从图像中识别的文本持久化为 DOCX、PDF 等文件格式。  
- **我可以导出哪些格式？** 支持 DOCX、TXT、PDF 和 XLSX。  
- **我需要许可证吗？** 免费试用可用于评估；生产环境需要商业许可证。  
- **我可以直接将图像转换为 PDF 吗？** 可以——将 OCR 结果保存为 PDF，即可获得可搜索的 PDF 文档。  
- **支持 PNG 吗？** 完全支持；您可以使用相同的 API **从 PNG 图像中提取文本**。

## OCR 是什么以及为何将结果保存为文档？

OCR（光学字符识别）将图像中的印刷或手写文本转换为机器可读的字符串。将这些字符串保存为文档可让您创建 **可搜索的 PDF**、填充电子表格、生成可编辑的报告或归档纯文本日志。Aspose.OCR 能够在一步操作中将扫描图片转换为 **可搜索的 PDF**，无需使用其他 PDF 创建工具。

## 先决条件

在开始之前，请确保您已：

- 已安装 Aspose.OCR for .NET。您可以在 **[here](https://releases.aspose.com/ocr/net/)** 下载。  
- 您机器上的一个文件夹，用于存放源图像和输出文档。请在代码中将 `dataDir` 变量更新为指向该文件夹的路径。

## 导入命名空间

我们需要一些 .NET 命名空间来访问文件 I/O 和 Aspose OCR 类。

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### 步骤 1：初始化 Aspose.OCR

AsposeOcr 是执行 OCR 操作的主要类。设置工作目录的路径并创建 OCR 引擎的实例。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### 步骤 2：识别图像

RecognitionResult 保存从图像中提取的文本和布局信息。将图像文件（例如 PNG）传递给识别器。这就是我们 **识别文本图像** 并将其转换为 `RecognitionResult` 的地方。

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### 步骤 3：以不同格式保存结果

现在我们导出识别的文本。选择适合您工作流的格式——无论是需要 **将图像转换为可搜索的 pdf**、**从 png 中提取文本**，还是生成电子表格。

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### 步骤 4：显示成功信息

简单的控制台消息确认过程已成功完成且没有错误。

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## 常见陷阱与技巧

- **文件路径：** 始终使用绝对路径，或确保 `dataDir` 以路径分隔符（`\` 或 `/`）结尾。  
- **图像质量：** 更高分辨率的图像可提升准确性；考虑进行预处理（去倾斜、去噪）以获得更好结果。  
- **许可证模式：** 评估模式下输出可能包含水印；使用有效许可证可去除水印。

## 常见问题

**Q1. Aspose.OCR 是否兼容不同的图像格式？**  
A1：是的，Aspose.OCR 支持超过 30 种图像格式，包括 PNG、JPEG、TIFF、BMP 和 GIF，确保在 OCR 任务中的灵活性。

**Q2. 我可以自定义识别设置以获得更高的准确性吗？**  
A2：当然！Aspose.OCR 提供 `RecognitionSettings`，可根据您的具体需求微调 OCR 过程。

**Q3. 是否提供免费试用？**  
A3：是的，您可以通过免费试用 **[here](https://releases.aspose.com/)** 开始使用。

**Q4. 我如何获取 Aspose.OCR 的临时许可证？**  
A4：临时许可证可在 **[here](https://purchase.aspose.com/temporary-license/)** 获取。

**Q5. 我可以在哪里寻求帮助或加入社区？**  
A5：加入 Aspose.OCR 社区 **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** 获取支持和讨论。

---

**最后更新：** 2026-06-29  
**测试环境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< blocks/products/products-backtop-button >}}

## 相关教程

- [使用 Aspose.OCR .NET 从图像提取文本](/ocr/net/image-and-drawing-recognition/)
- [将图像转换为 PDF C# – 保存多页 OCR 结果](/ocr/net/ocr-optimization/save-multipage-result-as-document/)
- [提取文本图像 – OCR 设置](/ocr/net/ocr-settings/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}