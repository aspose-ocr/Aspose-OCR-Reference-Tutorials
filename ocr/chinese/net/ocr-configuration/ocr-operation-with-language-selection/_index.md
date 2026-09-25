---
date: 2026-02-25
description: 学习如何使用 Aspose.OCR for .NET 在 C# 中提取图像文字。本分步指南展示了多语言 OCR、语言选择以及实用技巧。
linktitle: Extract image text C# with language selection using Aspose.OCR
second_title: Aspose.OCR .NET API
title: 使用 Aspose.OCR 在 C# 中提取图像文本并选择语言
url: /zh/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.OCR 进行语言选择的图像文本提取 C#

## 介绍

如果您需要在 .NET 应用程序中 **extract image text C#**（从图片和 PDF 中提取图像文本），Aspose.OCR for .NET 提供了一种快速、准确且支持语言的解决方案。在本教程中，我们将通过一个真实案例演示带语言选择的 OCR 图像识别，让您只需几行代码即可从图像中提取多语言文本。结束时，您将看到将 OCR 集成到 C# 项目有多么简便，以及为何此方法是生产工作负载的可靠选择。

## 快速回答
- **Aspose.OCR 的作用是什么？** 它识别图像中的印刷体和手写文本并返回提取的文本。  
- **我可以选择语言吗？** 可以——您可以指定任何受支持的语言，例如 English、German、Spanish、Chinese 等。  
- **开发是否需要许可证？** 免费试用可用于评估；生产使用需要许可证。  
- **支持哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6+。  
- **倾斜校正是自动的吗？** 您可以启用 `AutoSkew` 并微调 `SkewAngle` 设置。  

## 什么是 “extract image text C#”？

在 C# 中提取图像文本是指使用库读取图像（PNG、JPEG、TIFF 等）的视觉内容，并将其转换为可搜索、可编辑的文本。Aspose.OCR 在本地提供此功能，无需将数据发送到外部服务，从而保持工作流的安全性和合规性。

## 为什么选择 Aspose.OCR 进行 OCR 任务？

- **高精度**，适用于多种字体和图像质量。  
- **内置语言选择**，无需外部语言包。  
- **简洁的 API**，可干净地集成到现有 C# 项目中，使 **extract image text C#** 变得直观。  
- **无外部依赖**——所有操作本地运行，确保数据安全。  

## 前提条件

在深入代码之前，请确保已具备以下前提条件：

- Aspose.OCR for .NET：确保已安装 Aspose.OCR 库。您可以从 [Aspose.OCR for .NET download page](https://releases.aspose.com/ocr/net/) 下载。  
- 开发环境：搭建带有 .NET 应用程序的工作环境。如果尚未完成，请参阅 [documentation](https://reference.aspose.com/ocr/net/) 获取详细说明。  

## 导入命名空间

在 .NET 应用程序中，首先导入必要的命名空间：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 步骤 1：初始化 Aspose.OCR

首先初始化 Aspose.OCR 类的实例。这为在应用程序中使用 OCR 功能做好准备。

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 步骤 2：指定图像路径

接下来，定义要进行 OCR 的图像路径。确保应用程序能够访问该图像。

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## 步骤 3：使用语言选择识别图像

现在进行核心 OCR 操作。使用 Aspose.OCR 库识别指定图像中的文本。调整识别设置，包括语言选择，以微调 **extract image text C#** 过程。

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## 步骤 4：打印并显示结果

OCR 操作完成后，打印并显示结果，包括识别的文本、区域、警告以及 JSON 表示。

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## 常见问题与技巧

- **语言选择错误**——如果输出乱码，请再次确认 `Language` 属性与源图像的语言匹配。  
- **图像倾斜**——启用 `AutoSkew` 或手动调整 `SkewAngle` 以提升倾斜扫描的准确性。  
- **大文件**——将大图像分块处理或在传入 `RecognizeImage` 前降低分辨率，以节省内存。  

## 常见问答

**Q: Aspose.OCR 适用于多语言文本识别吗？**  
A: 是的，Aspose.OCR 支持多种语言，为多语言 OCR 任务提供灵活性。

**Q: 我可以针对特定图像特征微调 OCR 设置吗？**  
A: 当然！可以调整倾斜角度、行识别、区域检测等参数，以优化不同场景下的 OCR。

**Q: 我在哪里可以找到更多支持或社区讨论？**  
A: 访问 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 获取支持并与社区交流。

**Q: 是否提供免费试用？**  
A: 是的，您可以探索 [free trial](https://releases.aspose.com/) 体验 Aspose.OCR 的功能。

**Q: 如何购买 Aspose.OCR for .NET？**  
A: 购买请访问 [purchase page](https://purchase.aspose.com/buy)。

## 结论

恭喜！您已经学习了使用 Aspose.OCR for .NET 通过语言选择 **how to extract image text C#**。本教程展示了如何配置 OCR 引擎、选择合适的语言以及处理结果，为在您的应用程序中构建多语言文本提取功能奠定了坚实基础。

---

**最后更新：** 2026-02-25  
**测试版本：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}