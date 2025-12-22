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

## Introduction

光学字符识别（OCR）对于将视觉内容转换为可搜索、可编辑的文本至关重要。在本教程中，您将通过准备自定义矩形来**从图像中提取文本**，使 OCR 引擎聚焦于特定区域。使用 Aspose.OCR for .NET，我们将逐步演示从项目设置到获取识别文本的全部过程，帮助您在 .NET 应用程序中集成强大的图像转文本功能。

## Quick Answers
- **“从图像中提取文本”是什么意思？** 指将图片中的可视字符转换为机器可读的字符串。  
- **哪个库在 .NET 中提供此功能？** Aspose.OCR for .NET。  
- **开发阶段需要许可证吗？** 免费试用可用于测试；生产环境需要许可证。  
- **可以只针对特定区域吗？** 可以，通过定义矩形来限制 OCR 的范围。  
- **支持哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。

## What is “extract text from image” with rectangles?
当您在图像上定义矩形区域时，OCR 引擎仅处理这些区域。这可以提升准确性、缩短处理时间，并且可以忽略噪声背景或无关部分。

## Why prepare rectangles before OCR?
- **聚焦相关内容：** 跳过页眉、页脚或装饰性图形。  
- **提升性能：** 较小的区域意味着更快的识别。  
- **提高准确性：** 减少视觉噪声可获得更清晰的结果。

## Prerequisites

- 熟悉 C# 和 .NET 开发。  
- 已安装 Aspose.OCR for .NET 库 – 您可以在 **[here](https://releases.aspose.com/ocr/net/)** 下载。  
- 一张示例图片（例如 `sample.png`），其中包含您想要提取的文本。

## Import Namespaces

First, bring the required namespaces into scope:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Step 1: Set Up Your Document Directory

Specify where your image files live and create an instance of the OCR engine.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## How to extract text from image using multiple rectangles

### Step 2: Recognize Image with Multiple Rectangles

#### 2.1 Define the rectangles

Create a list of `Rectangle` objects that outline the areas you want the OCR engine to scan.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 Perform OCR recognition

Pass the image path and the rectangle list to `RecognizeImage`. The method returns a collection of strings—each entry corresponds to one rectangle.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Step 3: Recognize Image with Recognition Settings (Alternative Approach)

If you prefer using `RecognitionSettings`, you can achieve the same result with a slightly different API call.

#### 3.1 Define recognition settings

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Display recognized text

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Common Issues & Tips

- **矩形坐标不正确：** 确保 `X`、`Y`、`Width` 和 `Height` 的值正确映射到目标区域。  
- **图像质量：** 低分辨率图像可能导致 OCR 结果不佳；考虑进行预处理（例如二值化）。  
- **结果为空：** 验证矩形内部确实包含文本，否则引擎会返回空字符串。

## Conclusion

You’ve now learned how to **extract text from image** by preparing custom rectangles with Aspose.OCR for .NET. This technique gives you fine‑grained control over OCR processing, helping you build faster, more accurate text‑extraction features in your applications.

## Frequently Asked Questions

**Q:** Can I use Aspose.OCR for .NET with other .NET frameworks?  
**A:** Yes, Aspose.OCR for .NET is compatible with various .NET frameworks.

**Q:** Is there a free trial available for Aspose.OCR for .NET?  
**A:** Absolutely! You can access the free trial **[here](https://releases.aspose.com/)**.

**Q:** How do I get support for Aspose.OCR for .NET?  
**A:** Visit the **[Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)** for dedicated support.

**Q:** Can I obtain a temporary license for testing purposes?  
**A:** Yes, you can acquire a temporary license **[here](https://purchase.aspose.com/temporary-license/)**.

**Q:** Where can I find the documentation for Aspose.OCR for .NET?  
**A:** The documentation is available **[here](https://reference.aspose.com/ocr/net/)**.

---

**Last Updated:** 2025-12-22  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}