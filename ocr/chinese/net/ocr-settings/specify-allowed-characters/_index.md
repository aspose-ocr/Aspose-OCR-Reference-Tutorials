---
description: 了解如何使用 Aspose.OCR for .NET 指定允许的字符进行 OCR，并高效识别数字图像。请按照分步指南将 OCR 限制为仅识别数字。
linktitle: Specify Allowed Characters OCR – Using Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: 指定允许字符的 OCR – 使用 Aspose.OCR for .NET
url: /zh/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 指定允许字符 OCR – 使用 Aspose.OCR for .NET

在本教程中，您将学习如何使用 Aspose.OCR for .NET **指定允许字符 OCR**，从而限制 OCR 输出仅包含您需要的字符。当您需要 **识别数字图像** 文件（例如序列号、发票编号或类似条形码的字符串）时，这尤其方便。我们将逐步演示设置、代码以及几个实际场景，帮助您立即应用此技术。

## 快速回答
- **“指定允许字符 OCR” 做什么？** 它将 OCR 限制在预定义的字符集合中，提高针对性数据的识别准确率。  
- **我可以允许哪些字符？** 您需要的任意组合——数字、字母或自定义符号（例如 “0123456789”）。  
- **为什么要限制字符？** 当已知预期字符集时，可减少误识别并加快处理速度。  
- **我需要许可证吗？** 免费试用可用于开发；生产环境需要商业许可证。  
- **支持哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。

## 什么是 “指定允许字符 OCR”？
当 OCR 扫描图像时，会尝试将每个视觉模式匹配到完整的可能字符字母表。通过 **指定允许字符 OCR**，您告诉引擎忽略白名单之外的所有字符，这在受限数据集上可显著提升识别准确率。

## 为什么使用 Aspose.OCR 来识别数字图像？
Aspose.OCR 为 .NET 开发者提供简洁、流畅的 API。其内置的 `AllowedCharacters` 选项让您无需编写自定义后处理逻辑即可专注于仅数字的场景。这非常适用于：
- 读取表计读数、发票号码或产品代码。  
- 验证从扫描表单中捕获的用户输入数据。  
- 在预先知道字符集的批量处理场景中加速处理。

## 前提条件

在深入代码之前，请确保您已具备以下条件：

- 熟悉 .NET 开发。  
- **Aspose.OCR for .NET** 库。您可以在[此处](https://releases.aspose.com/ocr/net/)下载。  
- Visual Studio（或任意您喜欢的 .NET IDE）。  

## 导入命名空间

在您的 .NET 项目中，导入必要的命名空间以使用 Aspose.OCR 功能：

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

现在，让我们将教程分解为一系列完整的步骤：

## 如何指定允许字符 OCR – 步骤指南

### 步骤 1：设置图像文件夹路径

首先，定义示例图像的存放位置。

```csharp
string dataDir = "Your Document Directory";
```

### 步骤 2：使用仅数字白名单初始化 Aspose.OCR

创建 `AsposeOcr` 实例并传入您想允许的字符——在本例中为所有数字。

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### 步骤 3：识别包含数字的单行

使用 `RecognizeLine` 方法从仅包含数字的图像中提取文本。

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### 步骤 4：输出识别的数字

将结果打印到控制台，以便验证输出。

```csharp
Console.WriteLine(result);
```

### 步骤 5：使用 RecognitionSettings 获得更细粒度控制

如果需要更细致的控制——例如强制单行识别——可以使用接受 `RecognitionSettings` 的重载。

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### 步骤 6：显示第二种情况的结果

```csharp
Console.WriteLine(result2.RecognitionText);
```

### 步骤 7：确认执行成功

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

通过上述步骤，您已经学习了如何使用 Aspose.OCR for .NET **指定允许字符 OCR** 并高效 **识别数字图像** 内容。

## 常见问题与故障排除

- **结果为空：** 确保图像质量足够（对比度清晰，噪点最小）。  
- **返回错误字符：** 仔细检查白名单字符串是否与您期望的字符完全一致。  
- **文件未找到：** 确认 `dataDir` 指向正确的文件夹，并且文件名大小写匹配。

## 常见问答

### Q1：Aspose.OCR for .NET 是否适合初学者和有经验的开发者？
**答：** 绝对适合！该 API 设计直观，适合新手，同时为高级用户提供丰富的选项。

### Q2：我可以使用 Aspose.OCR for .NET 识别多语言字符吗？
**答：** 可以，Aspose.OCR 支持多种语言。您可以将语言包与允许字符功能结合使用，以实现多语言场景。

### Q3：Aspose.OCR for .NET 更新频率如何？
**答：** 我们会定期发布更新，添加新功能、提升准确率并确保兼容性。请查看[文档](https://reference.aspose.com/ocr/net/)获取最新版本信息。

### Q4：Aspose.OCR for .NET 是否提供免费试用？
**答：** 是的，您可以通过下载[免费试用](https://releases.aspose.com/)来体验其功能。

### Q5：我可以在哪里寻求帮助或加入社区获取支持？
**答：** 请访问[Aspose.OCR 论坛](https://forum.aspose.com/c/ocr/16)，提问、分享经验，并获得 Aspose 工程师和其他开发者的帮助。

**最后更新：** 2026-02-15  
**测试环境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}