---
date: 2025-12-22
description: 学习如何使用 Aspose.OCR for .NET 从图像中提取文本。本指南将带您了解为 OCR 图像识别准备矩形并提升准确度的技巧。
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: 如何在 OCR 中通过划定矩形提取图像文字
url: /zh/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 OCR 图像识别中准备矩形

## 简介

光学字符识别（OCR）对于将视觉内容转换为可搜索、可编辑的文本至关重要。在本教程中，您将通过准备自定义矩形来**从图像中提取文本**，使 OCR 引擎聚焦于特定区域。使用 Aspose.OCR for .NET，我们将逐步演示从项目设置到获取识别文本的全部过程，帮助您在 .NET 应用程序中集成强大的图像转文本功能。

## 快速解答
- **“从图像中提取文本”是什么意思？** 指将图片中的可视字符转换为机器可读的字符串。  
- **哪个库在 .NET 中提供此功能？** Aspose.OCR for .NET。  
- **开发阶段需要许可证吗？** 免费试用可用于测试；生产环境需要许可证。  
- **可以只针对特定区域吗？** 可以，通过定义矩形来限制 OCR 的范围。  
- **支持哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。

## 什么是使用矩形框从图像中提取文本？
当您在图像上定义矩形区域时，OCR 引擎仅处理这些区域。这可以提升准确性、缩短处理时间，并且可以忽略噪声背景或无关部分。

## 为什么要在进行 OCR 之前准备矩形框？
- **聚焦相关内容：** 跳过页眉、页脚或装饰性图形。  
- **提升性能：** 较小的区域意味着更快的识别。  
- **提高准确性：** 减少视觉噪声可获得更清晰的结果。

## 前提条件

- 熟悉 C# 和 .NET 开发。  
- 已安装 Aspose.OCR for .NET 库 – 您可以在 **[here](https://releases.aspose.com/ocr/net/)** 下载。  
- 一张示例图片（例如 `sample.png`），其中包含您想要提取的文本。

## 导入命名空间

首先，将所需的命名空间引入作用域：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 步骤 1：设置文档目录

指定图像文件所在的位置，并创建 OCR 引擎的实例。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 如何使用多个矩形框从图像中提取文本

### 步骤 2：使用多个矩形框识别图像

#### 2.1 定义矩形框

创建“矩形”对象列表，以标出您希望 OCR 引擎扫描的区域。

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 执行 OCR 识别

将图像路径和矩形列表传递给 `RecognizeImage` 方法。该方法返回一个字符串集合，每个字符串对应一个矩形。

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### 步骤 3：使用识别设置识别图像（替代方法）

如果您更喜欢使用 `RecognitionSettings`，则可以通过略有不同的 API 调用实现相同的结果。

#### 3.1 定义识别设置

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 显示识别的文本

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## 常见问题及提示

- **矩形坐标不正确：** 确保 `X`、`Y`、`Width` 和 `Height` 的值正确映射到目标区域。  
- **图像质量：** 低分辨率图像可能导致 OCR 结果不佳；考虑进行预处理（例如二值化）。  
- **结果为空：** 验证矩形内部确实包含文本，否则引擎会返回空字符串。

## 总结

您现在已经学会了如何使用 Aspose.OCR for .NET 通过创建自定义矩形来**从图像中提取文本**。这项技术让您可以精细地控制 OCR 处理，从而帮助您在应用程序中构建更快、更准确的文本提取功能。

## 常见问题解答

**问：**我可以将 Aspose.OCR for .NET 与其他 .NET 框架一起使用吗？

**答：**可以，Aspose.OCR for .NET 与各种 .NET 框架兼容。

**问：**Aspose.OCR for .NET 是否提供免费试用版？

**答：**当然！您可以访问**[此处](https://releases.aspose.com/)**获取免费试用版。

**问：**如何获得 Aspose.OCR for .NET 的支持？ **答：** 请访问 **[Aspose.OCR 论坛](https://forum.aspose.com/c/ocr/16)** 获取专门支持。

**问：** 我可以申请临时许可证进行测试吗？

**答：** 可以，您可以[在此处](https://purchase.aspose.com/temporary-license/)** 获取临时许可证。

**问：** 在哪里可以找到 Aspose.OCR for .NET 的文档？

**答：** 文档位于 **[此处](https://reference.aspose.com/ocr/net/)**。

---

**上次更新：** 2025-12-22
**测试版本：** Aspose.OCR 24.11 for .NET
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}