---
date: 2025-12-27
description: 了解如何使用 Aspose.OCR for .NET 将 OCR 图像转换为文本，指定允许的字符并微调 OCR 识别设置。包括识别数字图像的代码。
linktitle: 'ocr image to text: Specify Allowed Characters in OCR'
second_title: Aspose.OCR .NET API
title: OCR图像转文本：指定允许的字符
url: /zh/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr image to text：在 OCR 中指定允许的字符

## 介绍

在不断演进的技术领域，光学字符识别（OCR）——或 **ocr image to text** 转换——已成为一种变革性工具，使机器能够理解图像中的文本。Aspose.OCR for .NET 作为强大的解决方案脱颖而出，为寻求在 .NET 应用程序中实现强大 OCR 功能的开发者提供无缝集成。

## 快速答案
- **“Specify Allowed Characters” 的作用是什么？** 它将 OCR 输出限制在定义好的符号集合中，例如仅数字。  
- **哪个方法提取单行文本？** `RecognizeLine` 返回检测到的第一行。  
- **我可以实时更改 OCR 识别设置吗？** 可以——使用 `RecognitionSettings` 调整诸如 `AllowedCharacters` 等选项。  
- **是否提供试用版？** 当然，可从 Aspose 网站下载免费试用版。  
- **支持哪些 .NET 版本？** 所有现代 .NET Framework 和 .NET Core/5/6 版本。

## 先决条件

在深入教程之前，请确保具备以下先决条件：

- 具备 .NET 开发的工作经验。  
- Aspose.OCR for .NET 库。您可以在[此处](https://releases.aspose.com/ocr/net/)下载。  
- 熟悉 Visual Studio 或其他首选的 .NET 开发环境。

## 导入命名空间

在 .NET 项目中，导入必要的命名空间，以有效利用 Aspose.OCR for .NET 的功能：

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

现在，让我们将教程分解为一系列完整的步骤：

## 步骤 1：在 ocr image to text 中指定允许的字符

首先，设置文档目录的路径：

```csharp
string dataDir = "Your Document Directory";
```

## 步骤 2：使用允许的符号初始化 Aspose.OCR（识别数字图像）

创建 `AsposeOcr` 实例，并指定允许的符号。本例中，仅允许数字（0‑9）：

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## 步骤 3：识别图像

使用 `AsposeOcr` 实例对图像进行文本识别：

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## 步骤 4：显示识别的文本

将识别的文本打印到控制台：

```csharp
Console.WriteLine(result);
```

## 步骤 5：第二种情况 – 使用特定 OCR 识别设置识别图像

初始化另一个 `AsposeOcr` 实例，这次使用更具体的设置，以演示 **ocr recognition settings** 的用法：

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## 步骤 6：显示第二种情况的识别文本

将第二种情况的识别文本打印到控制台：

```csharp
Console.WriteLine(result2.RecognitionText);
```

## 步骤 7：成功执行

最后，确认 **SpecifyAllowedCharacters** 教程成功执行：

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

通过这些步骤，您已经掌握了在使用 Aspose.OCR for .NET 进行 OCR 图像识别时 **指定允许的字符** 的能力，从而实现仅数字场景下精确的 **ocr image to text** 转换。

## 为什么使用允许字符过滤？

- **更高的准确性：** 限制字符集可减少误识别，尤其在噪声图像中。  
- **性能提升：** OCR 引擎跳过不相关的字形，加快处理速度。  
- **合规性：** 在 OCR 阶段直接强制数据格式（例如发票号、序列码）。

## 常见陷阱与技巧

- **陷阱：** 为允许的字符提供空字符串会禁用过滤。  
  **技巧：** 始终传入非空字符串或使用 `CharactersAllowedType` 枚举。  
- **陷阱：** 在多行文档上使用 `RecognizeLine` 可能会遗漏数据。  
  **技巧：** 切换到 `RecognizeImage` 并将 `RecognizeSingleLine = false` 用于整页提取。  
- **陷阱：** 未正确组合目录路径可能导致 `FileNotFoundException`。  
  **技巧：** 使用 `Path.Combine(dataDir, "file.jpg")` 以获得跨平台的路径。

## 常见问题

**问：Aspose.OCR for .NET 是否适合初学者和有经验的开发者？**  
答：当然！该 API 对新手直观易用，同时为高级用户提供高级设置。

**问：我可以使用 Aspose.OCR for .NET 识别多种语言的字符吗？**  
答：可以，Aspose.OCR 支持多种语言；您还可以组合语言包以实现多语言项目。

**问：Aspose.OCR for .NET 更新频率如何？**  
答：我们定期发布更新，以跟上新的 .NET 版本和 OCR 改进。请查看[文档](https://reference.aspose.com/ocr/net/)获取最新版本。

**问：是否提供 Aspose.OCR for .NET 的免费试用？**  
答：是的，您可以通过下载[免费试用](https://releases.aspose.com/)来体验其功能。

**问：我可以在哪里寻求帮助或加入社区获取支持？**  
答：访问[Aspose.OCR 论坛](https://forum.aspose.com/c/ocr/16)，与专家和其他开发者交流。

---

**最后更新：** 2025-12-27  
**测试环境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}