---
date: 2025-12-17
description: 学习如何使用 Aspose.OCR for .NET 获取 OCR 行矩形，以识别图像中的文本行并轻松提取行坐标。
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: 获取图像文本行的 OCR 行矩形
url: /zh/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 获取图像文本行的 OCR 行矩形

## 介绍

在本教程中，您将学习如何使用 Aspose.OCR for .NET **获取 OCR 行矩形**。完成本指南后，您将能够 **识别图像中的文本行** 并 **提取每个检测到的行的坐标**——这对于后续处理（如布局分析、数据提取或自定义渲染）非常适用。

## 快速答案
- **“获取 OCR 行矩形” 是什么意思？** 它返回图像中每个检测到的文本行的边界框。  
- **使用哪个 API 方法？** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`。  
- **我需要许可证吗？** 免费试用可用于开发；生产环境需要商业许可证。  
- **支持的图像格式？** PNG、JPEG、BMP、TIFF 等。  
- **我可以在 .NET Core 上运行吗？** 可以，Aspose.OCR 完全支持 .NET Core 和 .NET 5/6。

## 前提条件

在深入教程之前，请确保已具备以下前提条件：

- 对 C# 和 .NET 开发的基本了解。  
- 如 Visual Studio 等集成开发环境（IDE）。  
- 已安装 Aspose.OCR for .NET 库。您可以在[此处](https://releases.aspose.com/ocr/net/)下载。  
- 用于 OCR 识别的包含文本的示例图像。

## 导入命名空间

确保已将必要的命名空间导入到项目中。将以下代码行添加到 C# 文件的顶部：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

现在，让我们把 OCR 图像识别中获取行矩形的过程拆解为易于遵循的步骤。

## 步骤 1：设置文档目录

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

将 `"Your Document Directory"` 替换为实际保存示例图像的文件夹路径。

## 步骤 2：初始化 Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

创建 `AsposeOcr` 类的实例以访问 OCR 功能。

## 步骤 3：指定图像路径

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

定义要进行 OCR 的图像的完整路径。

## 步骤 4：识别图像并获取矩形

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

`GetRectangles` 方法返回一个 `Rectangle` 对象列表，每个对象表示检测到的文本行的坐标。这就是 **获取 OCR 行矩形** 的核心。

## 步骤 5：打印结果

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

将检测到的区域坐标打印到控制台。您将看到可用于 **提取行坐标** 的数值，以便后续自定义处理。

## 为什么使用 Aspose.OCR 获取行矩形？

- **高精度** – 高级算法即使在噪声或倾斜的图像中也能检测行。  
- **跨平台** – 在 .NET Framework、.NET Core 和 .NET 5/6 上均可运行。  
- **无外部依赖** – 纯 .NET 库，无需分发本机 DLL。  
- **丰富的输出** – 除了行矩形，还可以检索单词、字符和置信度分数。

## 常见问题及解决方案

| 问题 | 解决方案 |
|------|----------|
| **未返回矩形** | 确保图像包含清晰的水平文本，并指定 `AreasType.LINES`。 |
| **坐标不正确** | 检查图像 DPI；低分辨率图像可能导致边界不准确。 |
| **大图像性能瓶颈** | 在调用 `GetRectangles` 前将图像调整到合理分辨率。 |
| **许可证异常** | 测试时使用试用许可证；生产环境使用完整许可证以避免评估限制。 |

## 常见问题

**Q: 我可以提取单个单词而不是整行吗？**  
A: 可以，使用 `AreasType.WORDS` 与相同的 `GetRectangles` 方法获取单词级别的边界框。

**Q: API 是否支持多页 PDF？**  
A: 首先将每页 PDF 转换为图像，然后对每个图像调用 `GetRectangles`。

**Q: 如何处理旋转的文本？**  
A: 在 OCR 设置中启用自动旋转选项，或在处理前预先旋转图像。

**Q: 是否可以获取每行的置信度分数？**  
A: 获取矩形后，调用 `api.RecognizeImage(...).Lines` 可访问包含置信度值的行对象。

**Q: 哪些 .NET 版本兼容？**  
A: 该库兼容 .NET Framework 4.5+、.NET Core 3.1+ 和 .NET 5/6。

## 结论

恭喜！您已成功使用 Aspose.OCR for .NET **获取图像的 OCR 行矩形**。拥有这些边界框后，您可以将行坐标输入到后续工作流中，如自定义渲染、数据提取或布局分析。

---

**最后更新：** 2025-12-17  
**测试环境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}