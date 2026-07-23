---
date: 2026-07-23
description: 了解如何使用 Aspose.OCR for .NET 从图像中提取文本，准备矩形以提升 OCR 准确率，并高效地将图像转换为文本。
keywords:
- extract text from image
- convert image to text
- improve ocr accuracy
lastmod: 2026-07-23
linktitle: 在 OCR 图像识别中准备矩形
og_description: 使用 Aspose.OCR for .NET 从图像中提取文本。了解如何准备矩形、提升 OCR 准确率，并高效地将图像转换为文本。
og_image_alt: Guide to extract text from image using rectangles with Aspose.OCR for
  .NET
og_title: 使用矩形从图像中提取文本 – OCR指南
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from image using Aspose.OCR for .NET, preparing
    rectangles to improve OCR accuracy and convert image to text efficiently.
  headline: Extract Text from Image with Rectangles – OCR Guide
  type: TechArticle
- questions:
  - answer: It converts visual characters in a picture into machine‑readable strings.
    question: What does “extract text from image” mean?
  - answer: Aspose.OCR for .NET provides a full‑featured OCR engine.
    question: Which library handles this in .NET?
  - answer: A free trial works for development; a commercial license is required for
      deployment.
    question: Do I need a license for production?
  - answer: Yes—define rectangles to target only the areas that contain useful text.
    question: Can I limit OCR to specific zones?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: What .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr
- Aspire.OCR
- .NET image processing
- extract text from image
title: 使用矩形从图像中提取文本 – OCR指南
url: /zh/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用矩形从图像提取文本 – OCR 指南

## 介绍

Optical Character Recognition (OCR) 让您 **extract text from image** 文件可被搜索和编辑。在本教程中，我们将展示如何通过准备自定义矩形，将引擎聚焦在所需的精确区域，从而提升 OCR 准确度。使用 Aspose.OCR for .NET，您将看到完整的工作流——从项目设置到获取识别字符串——以便在任何 .NET 应用程序中嵌入可靠的图像转文本转换功能。

## 快速答案
- **“extract text from image” 是什么意思？** 它将图片中的可视字符转换为机器可读的字符串。  
- **哪个库在 .NET 中处理此功能？** Aspose.OCR for .NET 提供完整的 OCR 引擎。  
- **生产环境需要许可证吗？** 开发阶段可使用免费试用版；部署时需购买商业许可证。  
- **可以将 OCR 限制在特定区域吗？** 可以——定义矩形仅针对包含有用文本的区域。  
- **支持哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。

## 什么是使用矩形的“extract text from image”？
`extract text from image` 过程读取定义的矩形区域内的字符，忽略其他部分。通过将 OCR 限制在这些区域，您可以获得更高的准确率、更快的处理速度以及更少的后处理工作量。这种方法只提取您关心的文本，同时丢弃背景图形、装饰元素和其他可能干扰 OCR 引擎的视觉噪声。

## 为什么在 OCR 前准备矩形？
准备矩形可以让 OCR 引擎专注于图像中最相关的部分，从而提升速度和精度。通过缩小分析范围，减少引擎需要检查的数据量，能够更快得到结果，并降低因多余视觉杂乱导致的误识别。

- **专注于相关内容**：跳过标题、页脚或装饰性图形，避免干扰引擎。  
- **提升性能**：更小的区域需要更少的计算，最大可将大幅扫描的运行时间缩短约 40 %。  
- **提高准确率**：降低视觉噪声可将字符识别率从约 85 % 提升至 >95 %（在噪声文档上）。

## 为什么这对真实项目很重要
许多业务文档——收据、发票、身份证——将文本与徽标或条形码混合。通过在实际需要的字段周围绘制矩形，您只提取有价值的数据，显著减少下游清洗工作，并提升自动化工作流的可靠性。这种针对性的提取降低了后处理工作量，有助于遵守数据处理标准。

## 常见用例
- **数据录入自动化**：从扫描表单或费用收据中提取特定字段。  
- **合规检查**：隔离法律条款或监管声明进行验证。  
- **内容索引**：仅索引图像的标题或说明，以提升搜索引擎可见性。

## 先决条件

- 具备 C# 和 .NET 开发的基础知识。  
- 已安装 Aspose.OCR for .NET 库——在 **[此处](https://releases.aspose.com/ocr/net/)** 下载，或在 **[此处](https://releases.aspose.com/)** 浏览所有发行版。  
- 一张示例图像（例如 `sample.png`），其中包含您想要提取的文本。

## 导入命名空间

`using` 语句将 OCR 引擎和几何类引入作用域。

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 步骤 1：设置文档目录

指定存放图像的文件夹，并创建 OCR 引擎实例。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 如何使用多个矩形提取图像文本
一次加载图像，然后将矩形列表传递给 OCR 引擎。每个矩形定义一个感兴趣区域，引擎为每个区域返回单独的字符串，便于您单独处理字段并根据需要合并结果。

### 定义矩形

`Rectangle` 对象描述您想要扫描的每个区域的 X‑Y 坐标和大小。  

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### 执行 OCR 识别

`RecognizeImage` 方法使用提供的矩形列表处理图像，并返回每个区域的识别文本。  

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## 如何使用 RecognitionSettings 提取图像文本（替代方法）
如果您更倾向于基于设置的调用，可以使用 `RecognitionSettings` 实现相同效果。该对象允许您将矩形定义、语言、DPI 以及其他 OCR 选项打包在一起，提供简洁的单参数 API 调用。

### 定义识别设置

`RecognitionSettings` 让您将矩形列表和其他选项（例如语言、DPI）封装到一个对象中。  

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 显示识别文本

遍历返回的字符串并输出每个区域的文本。  

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## 常见问题与技巧

- **矩形坐标不正确**：确认 `X`、`Y`、`Width`、`Height` 对应到预期区域。  
- **图像质量**：低分辨率或高度压缩的图像会降低 OCR 结果；考虑进行二值化等预处理。  
- **结果为空**：确保矩形实际包含可读文本，否则引擎会返回空字符串。

## 故障排除与最佳实践

| 症状 | 可能原因 | 解决方案 |
|------|----------|----------|
| 无输出或返回空字符串 | 矩形超出图像边界 | 仔细检查图像尺寸和矩形坐标 |
| 字符乱码 | 对比度差或噪声 | 在 OCR 前进行灰度转换和阈值处理 |
| 大文件性能慢 | 矩形数量过多或图像过大 | 将图像拆分或尽可能减少矩形数量 |

## 结论

您现在已经了解如何通过使用 Aspose.OCR for .NET 准备自定义矩形来 **extract text from image**。此方法为 OCR 处理提供精确控制，为任何 .NET 解决方案提供更快、更准确的文本提取功能。

## 常见问题

**Q:** 我可以在其他 .NET 框架中使用 Aspose.OCR for .NET 吗？  
**A:** 可以，Aspose.OCR for .NET 支持 .NET Framework 4.5+、.NET Core 3.1+ 以及 .NET 5/6/7。

**Q:** 是否提供免费试用？  
**A:** 当然！在 **[此处](https://releases.aspose.com/)** 下载试用版。

**Q:** 哪里可以获取 Aspose.OCR for .NET 的支持？  
**A:** 访问 **[Aspose.OCR 论坛](https://forum.aspose.com/c/ocr/16)** 获取专门帮助。

**Q:** 我可以获取临时许可证用于测试吗？  
**A:** 可以，临时许可证可在 **[此处](https://purchase.aspose.com/temporary-license/)** 获取。

**Q:** 官方文档在哪里？  
**A:** 完整的 API 参考位于 **[此处](https://reference.aspose.com/ocr/net/)**。

---

**最后更新：** 2026-07-23  
**测试环境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< blocks/products/products-backtop-button >}}

## 相关教程

- [如何在 OCR 图像识别中为段落提取矩形](/ocr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/)
- [如何进行 OCR 图像识别 – 在 OCR 图像识别中对图像执行 OCR](/ocr/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [如何使用 Aspose.OCR for .NET 提取图像文本](/ocr/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}