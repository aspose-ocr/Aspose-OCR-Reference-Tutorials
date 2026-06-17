---
date: 2026-02-22
description: 学习如何使用 Aspose.OCR for .NET 对图像进行 OCR 并提取图像文字。本分步指南将向您展示如何快速将图像转换为文本。
linktitle: Perform OCR on Image in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: 如何对图像进行 OCR – 在 OCR 图像识别中执行图像 OCR
url: /zh/net/image-and-drawing-recognition/perform-ocr-on-image/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何对图像进行 OCR – 在 OCR 图像识别中执行图像 OCR

## 介绍

在现代应用中，**如何对图像进行 OCR** 是开发者常见的问题，尤其是需要将扫描文档、截图或照片转换为可搜索、可编辑的文本时。Aspose.OCR for .NET 为您提供了强大且易于使用的 API，只需几行代码即可 **提取图像文本**、**将图像转换为文本**，以及 **识别图像文本**。在本教程中，我们将完整演示从库的设置到显示识别文本的全过程，让您在几分钟内将 OCR 功能集成到 C# 项目中。

## 快速回答
- **应该使用哪个库？** Aspose.OCR for .NET
- **可以处理 PNG、JPEG 和 TIFF 吗？** 可以，支持所有常见图像格式
- **生产环境需要许可证吗？** 需要，生产使用必须购买商业许可证
- **兼容哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6
- **一次基础 OCR 调用需要多长时间？** 对于标准尺寸的图像，通常在一秒以内

## 什么是 OCR 图像文本提取？

OCR（光学字符识别）图像文本提取是分析位图图像、识别字符并将其输出为可编辑文本的过程。这项技术为可搜索的 PDF、收据的自动数据录入等场景提供动力。

## 为什么选择 Aspose.OCR 作为您的 C# OCR 库？

- **高准确率** – 内置语言模型即使在低质量扫描件上也能提供可靠结果。  
- **广泛的格式支持** – 支持 PNG、JPEG、BMP、TIFF 等多种格式，轻松 **将图像转换为文本**，不论来源如何。  
- **无外部依赖** – 纯 .NET 库，无需安装本地 OCR 引擎。  
- **可扩展** – 您可以微调识别设置，或与其他 Aspose 产品集成，实现端到端的文档工作流。

## 前置条件

在编写代码之前，请确保您已具备：

1. **Aspose.OCR for .NET 库** – 从 [download link](https://releases.aspose.com/ocr/net/) 下载并安装。  
2. **开发环境** – 任意兼容 .NET 的 IDE（Visual Studio、Rider、VS Code 等）。  
3. **示例图像** – 本指南使用 `sample.png`，请将其放置在您选择的文件夹中。

## 导入命名空间

首先，添加所需的命名空间，以便编译器能够找到 OCR 类：

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## 使用 Aspose.OCR for .NET 对图像进行 OCR 的步骤

下面是完整的工作流，分为清晰的编号步骤。每一步都包含简短说明以及您需要复制的完整代码。

### 步骤 1：指定文档目录

```csharp
string dataDir = "Your Document Directory";
```

将 `"Your Document Directory"` 替换为包含 `sample.png` 的绝对或相对路径。此路径告诉 API 在哪里查找要处理的图像。

### 步骤 2：初始化 Aspose.OCR

```csharp
AsposeOcr api = new AsposeOcr();
```

创建 `AsposeOcr` 实例后，您即可使用所有 OCR 方法，例如 `RecognizeImage`。

### 步骤 3：识别图像

```csharp
string result = api.RecognizeImage(dataDir + "sample.png");
```

`RecognizeImage` 方法读取图像文件并返回提取的文本字符串。这一步完成了 **识别图像文本** 的核心工作。

### 步骤 4：显示识别文本

```csharp
Console.WriteLine(result);
```

您可以将结果打印到控制台、写入文件，或传递给其他组件进行进一步处理。

### 步骤 5：结束流程

```csharp
Console.WriteLine("PerformOCROnImage executed successfully");
```

一个简单的确认信息帮助您验证 OCR 调用已成功完成且未抛出异常。

## 将图像转换为文本 .NET – 其他提示

- **使用 `Path.Combine`** 在跨平台时安全构建文件路径。  
- **设置语言** 以处理非英文文本：`api.Language = "eng";`（或相应的 ISO 代码）。  
- **通过预处理**（如缩放、二值化）调整图像质量，以提升低分辨率扫描的识别准确率。

## 常见问题与故障排除

| 症状 | 可能原因 | 解决方案 |
|------|----------|----------|
| 返回空字符串 | 图像路径错误或文件未找到 | 检查 `dataDir` 和文件名；使用 `Path.Combine` 确保路径安全 |
| 字符乱码 | 图像分辨率过低或语言不受支持 | 使用更高分辨率的图像；通过 `api.Language = "eng"` 设置语言选项 |
| 异常 `System.IO.FileNotFoundException` | 缺少 `sample.png` | 确认文件已放置在指定文件夹中 |

## 常见问答

**问：Aspose.OCR 能处理多种图像格式吗？**  
答：可以，支持广泛的格式，您可以 **提取图像文本**，包括 PNG、JPEG、BMP、TIFF 等。

**问：是否提供用于测试的临时许可证？**  
答：当然。您可以在 Aspose 门户申请 30 天的评估许可证。

**问：在哪里可以找到 Aspose.OCR for .NET 的完整文档？**  
答：官方指南位于 [Aspose.OCR documentation](https://reference.aspose.com/ocr/net/)。

**问：如何获取支持或加入社区获取帮助？**  
答：访问 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 提问并分享经验。

**问：购买前可以免费试用 Aspose.OCR for .NET 吗？**  
答：可以，完整功能的 **免费试用** 可在 [free trial](https://releases.aspose.com/) 页面获取。

## 结论

通过上述步骤，您已经掌握了使用 Aspose.OCR for .NET **对图像进行 OCR** 的方法。无论是构建文档管理系统、收据处理应用，还是任何需要 **将图像转换为文本** 的解决方案，这个库都提供了一条简洁、高性能的路径，将视觉数据转化为可搜索的内容。

---

**最后更新：** 2026-02-22  
**测试环境：** Aspose.OCR for .NET 24.12（撰写时的最新版本）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}