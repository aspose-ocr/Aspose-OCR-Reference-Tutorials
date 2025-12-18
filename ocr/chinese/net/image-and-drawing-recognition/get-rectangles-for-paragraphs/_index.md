---
date: 2025-12-17
description: 学习如何使用 Aspose.OCR for .NET 从 OCR 图像中提取段落矩形——提取矩形和段落坐标的首选指南。
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: 如何在 OCR 图像识别中提取段落矩形
url: /zh/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 OCR 图像识别中提取段落的矩形

## 介绍

欢迎阅读本完整指南，了解如何使用 Aspose.OCR for .NET **提取段落的矩形**。如果您希望提升文档处理流水线、提取段落边界并实现数据自动化抽取，这里正是您的起点。我们将逐步演示从环境搭建到打印矩形坐标的全部过程，帮助您立即开始使用 OCR 结果。

## 快速答案
- **“提取矩形”是什么意思？** 返回检测到的文本区域的边界框（x、y、宽度、高度）。  
- **哪个 API 方法提供矩形？** `AsposeOcr.GetRectangles` 与 `AreasType.PARAGRAPHS`。  
- **开发阶段需要许可证吗？** 免费试用可用于测试，生产环境需商业许可证。  
- **可以一次处理多张图片吗？** 可以——遍历图片列表，对每个文件调用 `GetRectangles`。  
- **支持哪些格式？** PNG、JPEG、TIFF、BMP 等多种格式。

## OCR 中的 “提取矩形” 是什么？

在 OCR 领域，提取矩形指的是识别图像中每个段落或行文本的几何边界。这些坐标可用于高亮、裁剪或进一步分析扫描文档的特定区域。

## 为什么要提取段落坐标？
- **精确的后处理** – 可将每个矩形输入下游工作流（例如翻译、马赛克处理）。  
- **改进的 UI/UX** – 在原始图像上叠加边界框，向用户展示文本所在位置。  
- **批量自动化** – 快速定位并分离大批文档中的段落。

## 前置条件

- 具备 C# 和 .NET 开发的基础知识。  
- 已在开发环境中安装 Aspose.OCR for .NET，可从 [此处](https://releases.aspose.com/ocr/net/) 下载。  
- 熟悉图像处理概念以及 OCR 在从扫描文件中提取文本方面的重要性。

## 导入命名空间

在 C# 文件中导入所需的命名空间，以便使用 OCR 类：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 步骤 1：设置文档目录

定义包含待分析图片的文件夹路径：

```csharp
string dataDir = "Your Document Directory";
```

## 步骤 2：初始化 AsposeOcr 实例

创建 `AsposeOcr` 对象——这将提供所有 OCR 功能的访问权限：

```csharp
AsposeOcr api = new AsposeOcr();
```

## 步骤 3：指定图片路径

指向要处理的具体图片文件：

```csharp
string fullPath = dataDir + "sample.png";
```

## 步骤 4：识别图片并获取段落矩形

调用 `GetRectangles` 方法。将 `detect_areas` 设置为 `true` 可让引擎返回 **段落** 矩形：

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## 步骤 5：打印结果

输出坐标，以便查看检测到的 **提取段落坐标**：

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## 常见问题及解决方案

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 未返回矩形 | 图片质量太低或 `AreasType` 设置错误 | 确保图像清晰并使用 `AreasType.PARAGRAPHS`。 |
| 坐标偏移一像素 | DPI 缩放不匹配 | 加载图像时设置正确的 DPI，或使用 `api.Config.Dpi`。 |
| 许可证异常 | 生产环境未使用有效许可证 | 通过 `api.SetLicense` 应用临时或永久许可证。 |

## 常见问答

**Q: Aspose.OCR 是否兼容多种图片格式？**  
A: 是的，Aspose.OCR 支持 PNG、JPEG、TIFF、BMP 等常见格式。

**Q: 能否使用 Aspose.OCR 批量处理多张图片？**  
A: 完全可以！遍历文件路径集合，对每张图片调用 `GetRectangles`。

**Q: Aspose.OCR for .NET 有免费试用吗？**  
A: 有，您可以在 [此处](https://releases.aspose.com/) 试用免费版。

**Q: 如何获取 Aspose.OCR 的临时许可证？**  
A: 您可以在 [此处](https://purchase.aspose.com/temporary-license/) 获取临时许可证。

**Q: 哪里可以找到 Aspose.OCR 的更多支持和讨论？**  
A: 前往 [Aspose.OCR 论坛](https://forum.aspose.com/c/ocr/16) 获取社区支持和讨论。

## 结论

本教程展示了如何使用 Aspose.OCR for .NET **提取段落的矩形**，并逐步解释了每段代码及返回坐标的含义。将这些步骤集成到您的应用程序后，您即可可靠地提取段落边界，提升文档工作流，并构建更智能的 OCR 驱动解决方案。

---

**最后更新：** 2025-12-17  
**测试环境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}