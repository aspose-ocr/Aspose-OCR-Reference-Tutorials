---
date: 2026-02-22
description: 学习如何使用 Aspose.OCR for .NET 通过识别图像中的文本行并提取行矩形来进行布局分析 OCR。
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: 布局分析 OCR – 从图像获取行矩形
url: /zh/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Layout Analysis OCR – 获取图像中的行矩形

## 介绍

在本教程中，你将学习 **如何使用 Aspose.OCR for .NET 获取 OCR 行矩形**。完成本指南后，你将能够 **识别图像中的文本行** 并 **提取每条检测到的行的坐标**——这对于后续处理如 **布局分析 OCR**、数据提取或自定义渲染非常有用。

## 快速回答
- **“获取 OCR 行矩形” 是什么意思？** 它返回图像中每条文本行的边界框。  
- **使用哪个 API 方法？** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`。  
- **需要许可证吗？** 免费试用可用于开发；生产环境需要商业许可证。  
- **支持的图像格式？** PNG、JPEG、BMP、TIFF 等。  
- **可以在 .NET Core 上运行吗？** 可以，Aspose.OCR 完全支持 .NET Core 和 .NET 5/6。

## 前置条件

在开始教程之前，请确保已具备以下前置条件：

- 基本的 C# 和 .NET 开发知识。  
- 如 Visual Studio 等集成开发环境（IDE）。  
- 已安装 Aspose.OCR for .NET 库。你可以在 [此处](https://releases.aspose.com/ocr/net/) 下载。  
- 一张包含文本的示例图像，用于 OCR 识别。

## 导入命名空间

确保已在项目中导入必要的命名空间。将以下代码行添加到 C# 文件的顶部：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

现在，让我们把获取 OCR 图像中行矩形的过程拆解为易于跟随的步骤。

## layout analysis ocr – 步骤指南

### 步骤 1：设置文档目录

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

将 `"Your Document Directory"` 替换为实际存放示例图像的文件夹路径。

### 步骤 2：初始化 Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

创建 `AsposeOcr` 类的实例以访问 OCR 功能。

### 步骤 3：指定图像路径

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

定义要进行 OCR 的图像的完整路径。

### 步骤 4：识别图像并获取矩形

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

`GetRectangles` 方法返回一个 `Rectangle` 对象列表，每个对象表示检测到的文本行的坐标。这就是 **获取 OCR 行矩形** 的核心，并支持 **布局分析 OCR**。

### 步骤 5：打印结果

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

将检测到的区域坐标打印到控制台。你将看到可以随后用于 **提取行坐标** 进行自定义处理的数值。

## 为什么使用 Aspose.OCR 获取行矩形？

- **高精度** – 先进的算法即使在噪声或倾斜的图像中也能检测行。  
- **跨平台** – 支持 .NET Framework、.NET Core 和 .NET 5/6。  
- **无外部依赖** – 纯 .NET 库，无需分发本机 DLL。  
- **丰富输出** – 除了行矩形，还可以获取单词、字符和置信度分数。

## 常见问题及解决方案

| 问题 | 解决方案 |
|-------|----------|
| **未返回矩形** | 确保图像包含清晰的水平文本，并且已指定 `AreasType.LINES`。 |
| **坐标不正确** | 检查图像 DPI；低分辨率图像可能导致边界不准确。 |
| **大图像性能瓶颈** | 在调用 `GetRectangles` 前将图像调整到合理分辨率。 |
| **许可证异常** | 测试时使用试用许可证；生产环境请使用正式许可证以避免评估限制。 |

## 常见问答

**问：我可以提取单个单词而不是整行吗？**  
答：可以，使用 `AreasType.WORDS` 与同一 `GetRectangles` 方法获取单词级别的边界框。

**问：API 是否支持多页 PDF？**  
答：先将每页 PDF 转换为图像，然后对每张图像调用 `GetRectangles`。

**问：如何处理旋转的文本？**  
答：在 OCR 设置中启用自动旋转选项，或在处理前预先旋转图像。

**问：有没有办法获取每行的置信度分数？**  
答：获取矩形后，调用 `api.RecognizeImage(...).Lines` 可访问包含置信度值的行对象。

**问：兼容哪些 .NET 版本？**  
答：库兼容 .NET Framework 4.5+、.NET Core 3.1+ 以及 .NET 5/6。

## 实际使用案例

- **文档布局分析 OCR** – 将行矩形输入布局引擎，以重建列结构。  
- **自动化数据提取** – 使用坐标裁剪单行图像，供后续 NLP 流程使用。  
- **自定义渲染** – 在原始图像上叠加边界框，以进行可视验证或 UI 覆盖。  

## 结论

恭喜！你已成功使用 Aspose.OCR for .NET **获取图像的 OCR 行矩形**。手握这些边界框后，你现在可以将行坐标输入到自定义渲染、数据提取或 **布局分析 OCR** 等下游工作流中。

---

**最后更新：** 2026-02-22  
**测试环境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}