---
category: general
date: 2026-06-19
description: 如何在 C# 中使用 Aspose OCR 从图像中提取文本、对图像进行 OCR 以及识别扫描件中的文字——一步步指南。
draft: false
keywords:
- how to use aspose
- extract text from images
- run ocr on images
- recognize text from scans
language: zh
og_description: 如何在 C# 中使用 Aspose OCR 从图像中提取文本、对图像进行 OCR 并识别扫描件中的文字——完整指南。
og_title: 如何在 C# 中使用 Aspose OCR —— 从图像中提取文本
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to use Aspose OCR in C# to extract text from images, run OCR on
    images, and recognize text from scans – step‑by‑step guide.
  headline: How to Use Aspose OCR in C# – Extract Text from Images
  type: TechArticle
tags:
- Aspose
- OCR
- C#
- Image Processing
title: 如何在 C# 中使用 Aspose OCR – 从图像中提取文本
url: /zh/net/text-recognition/how-to-use-aspose-ocr-in-c-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose OCR – 从图像中提取文本

是否曾想过 **如何使用 Aspose** 从文档的照片中提取文字？你并不是第一个为此抓耳挠腮的人。在本教程中，我们将通过一个实用的端到端示例，向你展示如何从图像中提取文本、批量运行 OCR，以及仅用几行 C# 代码识别扫描件中的文字。

我们将先设置 Aspose OCR 引擎，然后提供一组 JPEG 文件，最后将每个结果打印到控制台。完成后，你将拥有一个可在任何 .NET 项目中直接使用的可复用代码片段——没有神秘步骤，也没有缺失的引用。

## 你需要准备的东西

在开始之前，请确保你拥有：

* .NET 6.0 SDK 或更高版本（代码在 .NET Core 和 .NET Framework 上均可运行）  
* 有效的 **Aspose.OCR** NuGet 包（可从 Aspose 官网获取免费试用密钥）  
* 包含若干扫描图像或文字照片的文件夹（JPEG 或 PNG 均可）  
* 你喜欢的 IDE——Visual Studio、Rider，甚至 VS Code 都可以。

就这些。无需庞大的 OCR 库，也不需要外部命令行工具。只要 Aspose 加上几行代码即可。

## 第一步：安装 Aspose.OCR NuGet 包

在项目文件夹的终端中运行：

```bash
dotnet add package Aspose.OCR
```

该命令会拉取最新版本（截至 2026 年 6 月为 22.9）并将引用添加到你的 `.csproj` 中。如果你更喜欢 Visual Studio 的 UI，右键 **Dependencies → Manage NuGet Packages** 并搜索 “Aspose.OCR”。

> **小贴士：** 注意许可证到期日期；免费试用可用 30 天，之后需要商业密钥。

## 第二步：配置 OCR 引擎 – “如何使用 Aspose” 从这里开始

包已就位后，创建 OCR 引擎并指定要识别的语言。大多数情况下英语已足够，但 Aspose 支持超过 70 种语言。

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;
using System.Collections.Generic;

// Configure the OCR engine to use English language
var ocrConfig = new OcrEngineConfig { Language = Language.English };
using var ocrEngine = new OcrEngine(ocrConfig);
```

为什么要在 `using` 语句中包装 `OcrEngine`？因为它实现了 `IDisposable`。释放会释放 OCR 引擎内部分配的本机资源（如非托管内存）——在每分钟处理数十个文件的生产服务中，这一点尤为重要。

## 第三步：构建图像路径列表 – 为 **在图像上运行 OCR** 做准备

接下来只需一个简单的 `List<string>`，指向所有待处理的图片。你可以手动构建（如下所示），也可以使用 `Directory.GetFiles` 动态生成。

```csharp
// Prepare a list of image file paths to be processed
var imagePaths = new List<string>
{
    @"C:\Scans\page1.jpg",
    @"C:\Scans\page2.jpg",
    @"C:\Scans\page3.jpg"
};
```

如果图像位于相对于可执行文件的子文件夹，只需在其中加入 `Path.Combine`。关键是列表顺序会被保留——Aspose 会按相同顺序返回结果，这使得输出与输入的对应变得非常简单。

## 第四步：在一次批处理中 **在图像上运行 OCR**

当需要一次处理大量文件时，Aspose OCR 的优势尽显。`ProcessBatch` 方法接受我们刚才构建的列表，并返回 `IList<OcrResult>`，其中每个元素包含识别的文本、置信度分数，甚至还有后续可能需要的边界框信息。

```csharp
// Run OCR on the entire batch and obtain results in the same order
IList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imagePaths);
```

在内部，Aspose 会生成本机线程加速处理，因此可以实现近乎线性的 CPU 核心扩展。对于超大工作负载，你可能需要调优 `OcrEngineConfig.ThreadCount` 属性，但默认的自动检测在大多数桌面场景下已经足够。

## 第五步：显示 **从扫描件中识别的文本** – 验证输出

最后，遍历结果并打印每段文本。我们还会回显原始文件名，以便你看到每个输出对应的是哪张扫描件。

```csharp
// Iterate through the results and display the recognized text for each image
for (int i = 0; i < ocrResults.Count; i++)
{
    System.Console.WriteLine($"--- Result for {imagePaths[i]} ---");
    System.Console.WriteLine(ocrResults[i].Text);
}
```

运行程序后，控制台会显示类似如下内容：

```
--- Result for C:\Scans\page1.jpg ---
Invoice #12345
Date: 06/15/2026
Total: $1,250.00

--- Result for C:\Scans\page2.jpg ---
Terms and Conditions
...
```

这正是 **如何使用 Aspose** 将一堆扫描的 PDF 或 JPEG 转换为可搜索、可编辑文本的最佳示例。

![如何使用 Aspose OCR 示例输出](image-placeholder.png "如何使用 Aspose OCR 示例输出")

*图片替代文字：“如何使用 Aspose OCR 示例输出，展示从扫描件中识别的文本。”*

## 可选：微调准确度 – 当 **从图像中提取文本** 需要提升时

如果发现缺字符或文字乱码，可尝试以下调整：

| 设置 | 功能说明 | 适用场景 |
|---------|--------------|----------------|
| `ocrConfig.DetectOrientation = true` | 自动旋转横向图像 | 扫描的书籍常为纵向模式 |
| `ocrConfig.Preprocess = true` | 应用对比度增强和降噪 | 用手机拍摄的低质量照片 |
| `ocrConfig.CharacterWhitelist = "0123456789"` | 仅识别数字 | 提取发票总额或序列号 |
| `ocrEngine.SetPageSegmentationMode(PageSegMode.SingleBlock)` | 将整页视为一个文本块 | 布局简单且追求速度时 |

不断尝试这些标志，直到置信度分数（通过 `ocrResults[i].Confidence` 获取）超过 0.9。记住，源图像越清晰，OCR 结果越好——在 Photoshop 或 ImageMagick 中进行一点预处理可以为你省下数小时的调试时间。

## 完整可运行示例 – 复制粘贴即用

下面是完整的程序代码，可直接编译运行。只需将文件路径替换为你自己的文件夹路径。

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure the OCR engine (how to use Aspose OCR)
        var ocrConfig = new OcrEngineConfig
        {
            Language = Language.English,
            DetectOrientation = true,          // optional: auto‑rotate
            Preprocess = true                  // optional: improve low‑quality scans
        };
        using var ocrEngine = new OcrEngine(ocrConfig);

        // 2️⃣ List of image files (run OCR on images)
        var imagePaths = new List<string>
        {
            @"C:\Scans\page1.jpg",
            @"C:\Scans\page2.jpg",
            @"C:\Scans\page3.jpg"
        };

        // 3️⃣ Process the batch (extract text from images)
        IList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imagePaths);

        // 4️⃣ Show the results (recognize text from scans)
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Result for {imagePaths[i]} ---");
            Console.WriteLine(ocrResults[i].Text);
            Console.WriteLine($"Confidence: {ocrResults[i].Confidence:P2}");
            Console.WriteLine(); // blank line for readability
        }
    }
}
```

使用 `dotnet run` 编译并运行，观察控制台输出干净、可搜索的文本。这就是 **如何使用 aspose** 的完整工作流，代码行数不足 50 行。

## 常见坑点及解决方案

* **`ocrResults[i]` 抛出 NullReferenceException** – 通常表示引擎无法打开文件（路径错误、格式不受支持）。请检查文件扩展名和权限。  
* **出现乱码字符** – 若看到 “�” 符号，图像可能采用了非 UTF‑8 编码。先将图像转换为无损 PNG，或启用 `ocrConfig.Preprocess`。  
* **性能瓶颈** – 当批次超过 100 张图像时，考虑使用 `Parallel.ForEach` 并为每个线程创建独立的 `OcrEngine` 实例进行并行处理。只要每个线程拥有自己的引擎，Aspose 即是线程安全的。

## 后续步骤 – 深入探索

掌握了 **如何使用 Aspose** 进行 OCR 基础后，你可以进一步探索：

* **导出为可搜索 PDF** – 使用 `Aspose.Pdf` 将识别的文本嵌入 PDF 文件，使扫描文档真正可搜索。  
* **与 Azure Functions 集成** – 当新图像上传至 Azure Blob 容器时自动触发 OCR。  
* **结合 AI 语言模型** – 将提取的文本喂给 ChatGPT 或 Claude，实现摘要、实体抽取或翻译。

上述主题自然会再次出现我们的二级关键词——**从图像中提取文本**、**在图像上运行 OCR**、以及**从扫描件中识别文本**——帮助你在扩展技能的同时保持关键词一致性。

## 结论

我们已经完整演示了一个可投入生产的示例，回答了 **如何使用 Aspose** 来从图像中提取文本、批量运行 OCR，以及以最少代码识别扫描件中的文字。通过配置引擎、准备文件路径列表、批量处理并打印结果，你现在拥有了任何文档自动化项目的坚实基础。

动手试一试，调节配置标志，很快你就能将成山的纸质文档转化为可搜索的数字内容。


## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你在自己的项目中进一步掌握 API 功能并探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步说明。

- [使用 Aspose.OCR 在 C# 中提取图像文本并选择语言](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [在文件夹上执行 OCR 操作以提取图像文本](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [使用 Aspose.OCR 对 .NET 进行 OCR 优化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}