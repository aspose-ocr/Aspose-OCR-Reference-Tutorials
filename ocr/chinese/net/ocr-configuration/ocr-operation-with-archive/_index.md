---
date: 2026-04-12
description: 学习如何使用 Aspose.OCR for .NET 对压缩文件中的图像执行 OCR，以提取文本，包括设置、代码和故障排除。
keywords:
- extract text from zip
- read images from zip
- Aspose OCR .NET
linktitle: 使用 Aspose.OCR for .NET 从 ZIP 档案中提取文本的方法
second_title: Aspose.OCR .NET API
title: 如何使用 Aspose.OCR for .NET 从 ZIP 档案中提取文本
url: /zh/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.OCR for .NET 从 ZIP 存档中提取文本

## 介绍

在本综合教程中，您将学习 **如何通过对存档中的每张图片应用 OCR 来从 zip 存档中提取文本**。无论您是需要 **将图像转换为文本**、**从 zip 中读取图像**，还是构建可搜索的文档库，下面的分步指南都将带您完成全部过程——从安装 Aspose.OCR for .NET 到打印 ZIP 文件中每张图片的识别文本。

## 快速答案
- **本教程覆盖哪些内容？** 使用 Aspose.OCR for .NET 从 ZIP 存档中提取文本。  
- **目标关键词是什么？** *extract text from zip*（提取 zip 文本）。  
- **是否需要许可证？** 免费试用可用于评估；生产环境需要商业许可证。  
- **支持哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6+。  
- **可以自定义识别设置吗？** 可以——使用 `RecognitionSettings` 调整不同语言或图像质量的准确性。

## 什么是 OCR，为什么要在 ZIP 存档上使用它？

光学字符识别（OCR）将扫描的图像或 PDF 转换为可搜索、可编辑的文本。当这些图像被打包在 ZIP 文件中时，一次性提取并识别每张图片可以节省时间并降低代码复杂度。Aspose.OCR 的 `RecognizeMultipleImages` 方法使此过程变得直观，让您 **从 zip 中读取图像** 并立即获取文本内容。

## 前置条件

- Visual Studio 2019 或更高版本（或任何兼容 .NET 的 IDE）。  
- 已安装 .NET Framework 4.5 + 或 .NET Core 3.1 +。  
- 可获取 Aspose.OCR for .NET 库（下载链接见下文）。  
- 生产使用需拥有有效的 Aspose.OCR 许可证（提供试用版）。

## 导入命名空间

在 .NET 项目中，导入必要的命名空间以访问 Aspose.OCR 提供的功能：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 下载并安装 Aspose.OCR for .NET

从发布页面 **[here](https://releases.aspose.com/ocr/net/)** 获取最新包，并按照标准的 NuGet 或手动安装步骤进行操作。

## 获取许可证

从 **[purchase page](https://purchase.aspose.com/buy)** 购买许可证或尝试 **[free trial](https://releases.aspose.com/)**。将许可证文件放置在项目根目录，并按照 Aspose 文档在运行时加载。

## 步骤 1：设置文档目录

首先初始化文档目录的路径。该文件夹将包含您要处理的 ZIP 存档：

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";
// ExEnd:1
```

> **小贴士：** 使用 `Path.Combine` 进行跨平台路径处理。

## 步骤 2：初始化 Aspose.OCR

创建 Aspose.OCR 实例以启动 OCR 操作：

```csharp
// ExStart:3
AsposeOcr api = new AsposeOcr();
// ExEnd:3
```

## 步骤 3：指定 ZIP 存档路径

定义指向存档图像（包含要读取的图片的 ZIP 文件）的完整路径：

```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## 步骤 4：识别 ZIP 内的图像

使用默认或自定义设置对指定存档执行 OCR 识别。此调用会自动从 ZIP 中提取每张图像并进行 OCR：

```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> 您可以调整 `RecognitionSettings` 以提升特定语言、DPI 或手写识别的准确性。

## 步骤 5：打印提取的文本

遍历结果并打印存档中每张图像的识别文本。这正是 **从 zip 中提取文本** 的过程：

```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

输出显示每个图像索引及其对应的提取字符串，实质上实现了 **将图像转换为文本** 并 **从存档文件中提取文本** 的一体化操作。

## 为什么这种方法重要

- **批量处理：** 可处理 ZIP 中任意数量的图像，无需手动解压。  
- **性能：** 通过直接读取存档降低 I/O 开销。  
- **可扩展性：** 适用于大型 ZIP 文件，并可结合异步模式实现高吞吐量场景。

## 常见问题与故障排除

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 未返回文本 | 图像质量太低 | 预处理图像（例如二值化）或调整 `RecognitionSettings.Dpi` |
| 读取 ZIP 时出现异常 | 存档路径无效 | 确认 `fullPath` 指向有效的 `.zip` 文件且应用具有读取权限 |
| 许可证未生效 | 未找到或未加载许可证文件 | 在创建 `AsposeOcr` 实例前调用 `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

## 常见问答

**问：可以在没有许可证的情况下使用 Aspose.OCR for .NET 吗？**  
答：可以，免费试用可用于评估，但生产部署必须使用授权版本。

**问：库是否支持受密码保护的 ZIP 存档？**  
答：目前，`RecognizeMultipleImages` 仅支持标准 ZIP 文件。对于加密存档，需要先使用第三方库解压图像，然后将图像数组传递给 OCR 引擎。

**问：如何提升手写文本的识别准确度？**  
答：启用 `RecognitionSettings.EnableHandwritingRecognition` 标志并提供更高的 DPI 设置（如 300）。

**问：是否可以获取每行识别的置信度分数？**  
答：每个 `RecognitionResult` 都包含 `Confidence` 属性，您可以记录或用于过滤低置信度结果。

## 其他资源

- **Aspose.OCR 论坛：** 如需社区支持和高级场景，请访问 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)。  
- **临时许可证：** 如需短期评估，可申请 [temporary license](https://purchase.aspose.com/temporary-license/)。  
- **官方文档：** 通过查看 [documentation](https://reference.aspose.com/ocr/net/) 及时了解最新 API 变更。

---

**最后更新：** 2026-04-12  
**测试环境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}