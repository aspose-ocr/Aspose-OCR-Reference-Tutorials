---
date: 2025-12-27
description: 使用 Aspose.OCR for .NET 探索先进的 OCR 语言支持和功能。高效、准确、对开发者友好。
linktitle: OCR Language Support – Ignored Characters in Image Recognition
second_title: Aspose.OCR .NET API
title: OCR语言支持——图像识别中的忽略字符
url: /zh/net/ocr-settings/specify-ignored-characters/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR语言支持：在图像识别中指定忽略字符

## 介绍

OCR 语言支持是现代文档自动化的基石，使应用程序能够读取跨多种字母表和符号的图像文本。在本教程中，您将学习如何让 **Aspose.OCR for .NET** 在识别过程中忽略特定字符——这是在需要更干净的输出或想过滤掉页码、装饰符号等噪声时的关键技巧。完成本指南后，您将拥有一个可直接运行的代码片段，演示该功能的完整流程。

## 快速答疑
- **“ignored characters” 是什么意思？** 构建结果字符串时，OCR 引擎会跳过的字符。  
- **为什么使用它？** 当某些符号与业务逻辑无关时，可提升准确性。  
- **哪个 API 方法处理它？** `RecognitionSettings.IgnoredCharacters`.  
- **我可以将其与语言包一起使用吗？** 是的——ignored characters 可与您加载的任何语言一起使用。  
- **是否需要许可证？** 生产环境需要临时或完整许可证。

## 前置条件

在深入了解 Aspose.OCR for .NET 提供的丰富功能之前，请确保已满足以下前置条件：

1. Aspose.OCR 安装  

   确保已成功安装 Aspose.OCR for .NET。您可以在[download page](https://releases.aspose.com/ocr/net/)找到所需文件。

2. 文档目录设置  

   为文档设置专用目录。这对于顺利运行示例至关重要。请在示例中将 `dataDir` 变量更新为您的文档目录路径。

3. 临时许可证（可选）  

   如果您使用临时许可证探索 Aspose.OCR for .NET，请从[here](https://purchase.aspose.com/temporary-license/)获取。

## 导入命名空间

要启动 Aspose.OCR for .NET 的使用，需要导入必要的命名空间。将以下代码行添加到您的项目中：

```csharp
using System.IO;

using Aspose.OCR;
using System;
```

## 为什么要指定忽略字符？

在许多实际场景中——例如处理发票、收据或多语言表单时，您可能会遇到重复出现但并非有意义数据的字符（如用作分隔符的连字符、页码或装饰符号）。通过告诉 OCR 引擎跳过这些字符，可减少后处理工作量并提升下游分析的可靠性。

## 步骤指南

### 第一步：设置文档目录

首先指定存放文档的目录。将 `"Your Document Directory"` 替换为实际的文档路径。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

### 第二步：初始化 Aspose.OCR

创建 OCR 引擎实例。该对象将处理后续的所有识别调用。

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### 第三步：使用忽略字符识别图像

将图像文件与包含要忽略字符的 `RecognitionSettings` 对象一起传递。在本例中我们忽略字符 `a`、`b` 和 `1`。

```csharp
// Recognize image with specified ignored characters
RecognitionResult result = api.RecognizeImage(dataDir + "SpanishOCR.bmp", new RecognitionSettings
{
    IgnoredCharacters = "ab1"
});
```

### 第四步：显示识别文本

最后，将清理后的文本输出到控制台或您喜欢的其他接收端。

```csharp
// Display the recognized text
Console.WriteLine(result.RecognitionText);
```

## 常见问题与技巧

- **路径不正确：** 确保 `dataDir` 以适合您操作系统的路径分隔符（`\` 或 `/`）结尾。  
- **不支持的语言：** OCR 引擎必须拥有源图像对应的语言包，否则忽略字符将无法正确应用。  
- **许可证错误：** 如果出现许可证异常，请确认临时许可证文件已在项目中正确引用。

## 结论

Aspose.OCR for .NET 为开发者提供了强大的 OCR 能力，简化了将图像转换为可编辑、可搜索文本的过程。通过本步骤指南，您已经学会了如何排除不需要的字符，使 OCR 流程更清洁、更可靠。请访问[documentation](https://reference.aspose.com/ocr/net/)获取更深入的洞见，探索 Aspose.OCR 如何提升您的 OCR 项目。

## 常见问题

### Q1：我可以在非商业项目中使用 Aspose.OCR for .NET 吗？

A1：是的，Aspose.OCR for .NET 可用于商业和非商业项目。请参阅[licensing details](https://purchase.aspose.com/buy)获取更多信息。

### Q2：是否提供免费试用？

A2：当然！您可以在[here](https://releases.aspose.com/)获取免费试用，以在做出决定前探索 Aspose.OCR for .NET 的功能和优势。

### Q3：如何获取 Aspose.OCR 的支持？

A3：如有任何疑问，请访问[Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)与社区交流并获取专家建议。

### Q4：Aspose.OCR 支持哪些语言？

A4：Aspose.OCR 支持广泛的语言，是 OCR 任务的多功能选择。请参阅文档获取完整列表。

### Q5：我可以为 Aspose.OCR 购买临时许可证吗？

A5：是的，如果需要临时许可证，可在[here](https://purchase.aspose.com/temporary-license/)获取，供短期使用。

---

**最后更新：** 2025-12-27  
**测试环境：** Aspose.OCR 23.12 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}