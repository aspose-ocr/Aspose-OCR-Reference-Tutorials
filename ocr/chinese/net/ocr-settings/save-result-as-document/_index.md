---
description: 了解如何使用 Aspose.OCR for .NET 保存 OCR 结果——将图像转换为 PDF，从 PNG 中提取文本，并将识别的文本保存为
  DOCX、TXT、PDF 或 XLSX。
linktitle: How to Save OCR Result as Document
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

在本教程中，您将学习使用 Aspose.OCR for .NET **保存 OCR** 输出。我们将演示如何识别图像中的文本，然后将该文本转换为常用文档格式，如 DOCX、 TXT、 PDF 和 XLSX。完成后，您即可自动从图片中提取数据并将其存储为可搜索、可编辑的文件——非常适合归档、报告或后续处理。

## 快速答案
- **“如何保存 OCR”是什么意思？** 它指的是将从图像中识别的文本持久化为 DOCX、PDF 等文件格式。  
- **我可以导出哪些格式？** DOCX、TXT、PDF 和 XLSX 开箱即用支持。  
- **我需要许可证吗？** 免费试用可用于评估；生产使用需要商业许可证。  
- **我可以直接将图像转换为 PDF 吗？** 可以——将 OCR 结果保存为 PDF，即可获得可搜索的 PDF 文档。  
- **支持 PNG 吗？** 当然；您可以使用相同的 API **从 PNG 图像中提取文本**。

## 什么是 OCR，为什么要将结果保存为文档？

光学字符识别（OCR）将图像中的印刷或手写文本转换为机器可读的字符串。将这些字符串保存为文档可让您：

* 创建用于合规的可搜索 PDF。  
* 填充电子表格（XLSX）以进行数据分析。  
* 生成可编辑的报告（DOCX）。  
* 归档纯文本日志（TXT），便于快速搜索。

## 前置条件

在开始之前，请确保您已拥有：

- 已安装 Aspose.OCR for .NET。您可以在 **[here](https://releases.aspose.com/ocr/net/)** 下载。  
- 机器上有一个文件夹用于存放源图像和输出文档。请在代码中将 `dataDir` 变量更新为指向该文件夹的路径。

## 导入命名空间

我们需要一些 .NET 命名空间来访问文件 I/O 和 Aspose OCR 类。

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### 步骤 1：初始化 Aspose.OCR

设置工作目录路径并创建 OCR 引擎实例。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### 步骤 2：识别图像

将图像文件（例如 PNG）传递给识别器。这一步我们 **识别文本图像** 并将其转换为 `RecognitionResult`。

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### 步骤 3：以不同格式保存结果

现在我们导出识别的文本。选择适合您工作流的格式——无论是 **将图像转换为 PDF**、**从 PNG 提取文本**，还是生成电子表格。

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### 步骤 4：显示成功信息

简单的控制台消息可确认该过程已成功完成且没有错误。

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## 常见陷阱与技巧

- **文件路径：** 始终使用绝对路径，或确保 `dataDir` 以路径分隔符（`\` 或 `/`）结尾。  
- **图像质量：** 更高分辨率的图像可提升准确率；考虑进行预处理（去倾斜、去噪）以获得更好效果。  
- **许可证模式：** 评估模式下输出可能包含水印；使用有效许可证可去除水印。

## 常见问题

**Q1. Aspose.OCR 是否兼容不同的图像格式？**  
A1：是的，Aspose.OCR 支持多种图像格式，确保在 OCR 任务中的灵活性。

**Q2：我可以自定义识别设置以获得更高的准确性吗？**  
A2：当然！Aspose.OCR 提供 `RecognitionSettings`，可根据您的具体需求微调 OCR 过程。

**Q3：是否提供免费试用？**  
A3：是的，您可以通过 **[here](https://releases.aspose.com/)** 开始免费试用。

**Q4：如何获取 Aspose.OCR 的临时许可证？**  
A4：可在 **[here](https://purchase.aspose.com/temporary-license/)** 获取临时许可证。

**Q5：我可以在哪里寻求帮助或加入社区？**  
A5：加入 **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** 的 Aspose.OCR 社区获取支持和讨论。

---

**最后更新：** 2026-02-12  
**测试环境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}