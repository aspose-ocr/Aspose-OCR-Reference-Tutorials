---
date: 2025-12-19
description: 了解如何使用 Aspose.OCR for .NET 对归档图像执行 OCR、将图像转换为文本以及从归档文件中提取文本。
linktitle: How to Perform OCR on Archive Images with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: 如何使用 Aspose.OCR for .NET 对归档图像进行 OCR
url: /zh/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.OCR for .NET 对归档图像执行 OCR 的方法

## 介绍

在本综合教程中，您将学习 **如何对归档图像文件执行 OCR**，使用 Aspose.OCR 库 for .NET。无论是 **将图像转换为文本** 还是 **从归档文件中提取文本**，下面的分步指南将从搭建开发环境到从 ZIP 归档中的每张图像获取识别文本，全部为您演示。

## 快速回答
- **本教程涵盖哪些内容？** 使用 Aspose.OCR for .NET 对归档（ZIP）图像执行 OCR。  
- **目标关键字是什么？** *how to perform ocr*。  
- **是否需要许可证？** 免费试用可用于评估；生产环境需购买商业许可证。  
- **支持哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6+。  
- **可以自定义识别设置吗？** 可以——使用 `RecognitionSettings` 调整准确度。

## 什么是 OCR 以及为何在归档上使用它？

光学字符识别（OCR）将扫描的图像或 PDF 转换为可搜索、可编辑的文本。当图像被打包在归档文件（例如 ZIP）中时，一次性提取并识别每张图片可以节省时间并降低代码复杂度。Aspose.OCR 的 `RecognizeMultipleImages` 方法使此过程变得简洁。

## 前置条件

- Visual Studio 2019 或更高版本（或任何兼容 .NET 的 IDE）。  
- 已安装 .NET Framework 4.5 + 或 .NET Core 3.1 +。  
- 访问 Aspose.OCR for .NET 库（下载链接见下文）。  
- 生产使用需有效的 Aspose.OCR 许可证（提供试用版）。

## 导入命名空间

在 .NET 项目中，确保导入访问 Aspose.OCR 功能所需的命名空间：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 下载并安装 Aspose.OCR for .NET

从发布页面 **[here](https://releases.aspose.com/ocr/net/)** 获取最新包，并按照标准 NuGet 或手动安装步骤进行操作。

## 获取许可证

从 **[purchase page](https://purchase.aspose.com/buy)** 购买许可证，或尝试 **[free trial](https://releases.aspose.com/)**。将许可证文件放置在项目根目录，并按 Aspose 文档在运行时加载。

## 步骤 1：设置文档目录

初始化文档目录的路径：

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";
// ExEnd:1
```

> **专业提示:** 使用 `Path.Combine` 进行跨平台路径处理。

## 步骤 2：初始化 Aspose.OCR

创建 Aspose.OCR 实例以启动 OCR 操作：

```csharp
// ExStart:3
AsposeOcr api = new AsposeOcr();
// ExEnd:3
```

## 步骤 3：指定图像路径

定义指向归档图像（包含待读取图片的 ZIP 文件）的完整路径：

```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## 步骤 4：识别图像

使用默认或自定义设置对指定归档执行 OCR 识别。此调用会自动从 ZIP 中提取每张图像并进行 OCR：

```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> 您可以调整 `RecognitionSettings` 以提升特定语言或图像质量的准确度。

## 步骤 5：打印结果

遍历结果并打印归档中每张图像的识别文本：

```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

输出显示每个图像索引及其提取的字符串，实质上 **将图像转换为文本** 并 **从归档文件中提取文本**。

## 常见问题与故障排除

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 未返回文本 | 图像质量过低 | 预处理图像（如二值化）或调整 `RecognitionSettings.Dpi` |
| ZIP 读取异常 | 归档路径无效 | 确认 `fullPath` 指向有效的 `.zip` 文件且应用具有读取权限 |
| 许可证未生效 | 缺少许可证文件或未加载 | 在创建 `AsposeOcr` 实例前调用 `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

## 常见问答

**问：可以在没有许可证的情况下使用 Aspose.OCR for .NET 吗？**  
答：可以，免费试用可用于评估，但生产部署必须使用已授权的版本。

**问：库是否支持受密码保护的 ZIP 归档？**  
答：目前，`RecognizeMultipleImages` 仅支持标准 ZIP 文件。对于加密归档，请先使用第三方库解压图像，然后将图像数组传递给 OCR 引擎。

**问：如何提升手写文字的识别准确度？**  
答：启用 `RecognitionSettings.EnableHandwritingRecognition` 标志，并提供更高的 DPI 设置（例如 300）。

**问：是否可以获取每行识别的置信度分数？**  
答：每个 `RecognitionResult` 都包含 `Confidence` 属性，您可以记录或用于过滤低置信度结果。

## 结论

现在，您已经掌握了一套完整的、可用于生产的工作流，能够 **对归档图像执行 OCR**、**将图像转换为文本**，以及 **从归档文件中提取文本**，全部基于 Aspose.OCR for .NET。将其集成到您的应用程序中，可实现可搜索的文档库、自动化数据录入或任何需要批量图像文本提取的场景。

## 附加资源

- **Aspose.OCR 论坛：** 如需社区支持和高级场景，请访问 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)。  
- **临时许可证：** 如需短期评估，可申请 [temporary license](https://purchase.aspose.com/temporary-license/)。  
- **官方文档：** 通过查看 [documentation](https://reference.aspose.com/ocr/net/) 及时了解最新 API 变更。

---

**最后更新：** 2025-12-19  
**测试环境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
