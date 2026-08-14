---
category: general
date: 2026-03-07
description: 学习如何在 C# 中使用 OCR 从图像文件中提取文本。本指南展示离线 OCR、将图像转换为文本以及加载图像进行 OCR。
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- convert image to text
- load image for ocr
language: zh
og_description: 如何在 C# 中使用 OCR 离线提取图像中的文本。逐步代码、技巧以及完整的图像转文本解释。
og_title: 如何在 C# 中使用 OCR – 完整离线指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 OCR – 离线从图像提取文本
url: /zh/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-offline/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 离线提取图像文字

是否曾想过 **如何在 .NET 项目中使用 OCR** 而不将数据发送到云端？你并不孤单。许多开发者需要在受保护的工作站上 *从图像文件中提取文字*，并担心网络流量会泄露敏感信息。  

好消息是？使用 Aspose.OCR，你可以完全离线地识别 PNG、JPEG 或 PDF 中的文字。在本教程中，我们将演示如何加载图像进行 OCR、配置离线模式的引擎，最后仅用几行 C# **将图像转换为文字**。

阅读完本指南后，你将能够：

* 安装 Aspose.OCR NuGet 包。  
* 为离线处理设置 OCR 引擎。  
* 加载图像进行 OCR 并提取其文本内容。  

无需外部服务，无需 API 密钥——只需纯 C# 代码，能够在任何 Windows 或 Linux 机器上运行。

---

## 前置条件

在开始之前，请确保你拥有：

* .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Framework 4.7+）。  
* Visual Studio 2022、VS Code，或任何支持 C# 的编辑器。  
* 一份 **Aspose.OCR** 库——可从 NuGet 获取 (`Aspose.OCR`)。  
* 一个 OCR 资源文件夹 (`Resources`)，随库一起提供（包含语言数据文件）。  
* 一张示例图片（例如 `offline_test.png`），放置在已知目录下。

> **专业提示：** 将资源文件夹放在可执行文件旁边，可简化 `ResourcesPath` 的配置。

---

## 第一步：安装 Aspose.OCR NuGet 包

首先，将库添加到项目中。在项目文件夹的终端运行：

```bash
dotnet add package Aspose.OCR
```

或者，如果你更喜欢 Visual Studio UI，右键 **Dependencies → Manage NuGet Packages**，搜索 *Aspose.OCR*，点击 **Install**。

> 安装该包会自动拉取所有必需的二进制文件，无需额外的 DLL。

---

## 第二步：创建并配置 OCR 引擎（如何使用 OCR – 离线模式）

接下来实例化 OCR 引擎并让它 **离线** 工作。这可确保识别过程中不产生任何网络流量。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Switch the engine to offline mode – crucial for privacy‑first apps
ocrEngine.Settings.EngineMode = EngineMode.Offline;
```

**为什么要离线？**  
当 `EngineMode` 设置为 `Online` 时，引擎会联系 Aspose 的云端实时下载语言包。在受监管的环境（金融、医疗）中，这类流量往往被禁止。强制离线模式即可保证所有操作都在本机完成。

---

## 第三步：指定 OCR 资源文件夹路径

OCR 引擎需要语言数据（训练模型）来识别字符。告诉它这些文件所在的位置：

```csharp
// Replace with the absolute or relative path to your Resources folder
ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";
```

如果不确定文件夹所在位置，可在 NuGet 包目录下找到（`%USERPROFILE%\.nuget\packages\aspose.ocr\*\resources`）。为便于部署，建议将整个文件夹复制到项目中。

---

## 第四步：加载待 OCR 的图像（Load Image for OCR）

引擎可以接受任意受支持的位图。这里我们从磁盘加载一张 PNG：

```csharp
// Load the image you want to recognize – this is the “load image for OCR” step
ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");
```

**提示：** 如果需要从流中处理图像（例如通过 API 上传），请使用 `ImageStream.FromStream(yourStream)`。

---

## 第五步：运行识别并将图像转换为文字

准备就绪后，调用 OCR。`Recognize()` 方法负责核心识别工作，提取的文字可通过 `Text` 属性获取。

```csharp
// Perform OCR – this is where the engine reads the pixels and produces text
ocrEngine.Recognize();

// Grab the result – now you have “convert image to text” completed
string extractedText = ocrEngine.Text;
```

---

## 第六步：输出提取的文字

最后，展示结果。在控制台应用中直接写入控制台；在 Web API 中则返回 JSON 字符串。

```csharp
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);
```

运行程序后应打印出 `offline_test.png` 的文本内容。例如，若图像中包含短语 *“Hello, World!”*，则会看到：

```
=== OCR Result ===
Hello, World!
```

---

## 完整可运行示例

下面是完整的、可直接运行的程序。将其复制粘贴到新建的控制台项目（`dotnet new console`）中，并根据实际环境调整路径。

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2: Set offline mode – no network traffic
        // -------------------------------------------------
        ocrEngine.Settings.EngineMode = EngineMode.Offline;

        // -------------------------------------------------
        // Step 3: Provide path to OCR resource files
        // -------------------------------------------------
        ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";

        // -------------------------------------------------
        // Step 4: Load the image you want to recognize
        // -------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");

        // -------------------------------------------------
        // Step 5: Run recognition and extract text
        // -------------------------------------------------
        ocrEngine.Recognize();
        string extractedText = ocrEngine.Text;

        // -------------------------------------------------
        // Step 6: Show the result
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

> **预期输出：** 控制台会打印 PNG 文件中包含的完整文字。若图像模糊，结果可能出现误识别字符——请参阅下方故障排除章节。

---

## 常见问题与技巧（高效从 PNG 识别文字）

| 问题 | 产生原因 | 解决办法 |
|------|----------|----------|
| **输出为空** | `ResourcesPath` 指向错误文件夹或缺少语言文件。 | 确认文件夹中包含 `eng.traineddata`（或其他语言文件），并再次检查路径字符串。 |
| **出现乱码** | 图像分辨率过低或未二值化。 | 预处理图像（提升 DPI，使用 `ImageProcessor` 锐化）。 |
| **性能卡顿** | 大图像以原始分辨率处理。 | 在送入 OCR 前将图像宽度限制在 2000 px 以内。 |
| **不支持的格式** | 使用了异常像素格式的 BMP。 | 先将图像转换为 PNG 或 JPEG（`System.Drawing.Image.Save`）。 |

**专业提示：** 若需识别多种语言，可在调用 `Recognize()` 前设置 `ocrEngine.Settings.Language = Language.English | Language.French;`。

---

## 常见问答

**问：这段代码可以在 Linux 上运行吗？**  
答：完全可以。Aspose.OCR 跨平台，只需确保本机包含 NuGet 包自带的原生库。

**问：如果没有 Resources 文件夹怎么办？**  
答：可以从 Aspose 官方网站下载免费语言包，或从 NuGet 包中提取（`.../aspose.ocr/<version>/resources`）。

**问：能获取置信度分数吗？**  
答：可以。`Recognize()` 之后，检查 `ocrEngine.RecognizedWords`——每个单词都有 `Confidence` 属性。

---

## 结论

我们已经完整演示了 **如何在 C# 中使用 OCR** 完全离线地 *从图像文件中提取文字*。通过安装 Aspose.OCR、将 `EngineMode` 设置为 `Offline`、指向资源文件夹、加载图像并调用 `Recognize()`，即可可靠地 **将图像转换为文字**，且全程不触及互联网。

拿起上面的代码，替换为自己的图像路径，开始构建可搜索的 PDF、数据录入自动化或辅助功能等特性吧。接下来，你可以尝试批量 **从 PNG 识别文字**，或将引擎集成到 ASP.NET Core API 中，为前端提供 OCR 结果。

祝编码愉快，尽情实验——一旦引擎配置妥当，OCR 的容错性出奇地好！

--- 

![离线 OCR 工作流示意图 – 在安全环境中如何使用 OCR](https://example.com/ocr-workflow.png "离线 OCR 工作流示意图")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}