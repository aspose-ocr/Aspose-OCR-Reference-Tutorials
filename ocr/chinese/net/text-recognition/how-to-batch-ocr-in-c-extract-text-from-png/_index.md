---
category: general
date: 2026-03-26
description: 在 C# 中批量 OCR 可轻松从 PNG 文件中提取文本。请按照本步骤式 C# OCR 教程，使用 Aspose OCR 进行批量文本提取。
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: zh
og_description: 如何在 C# 中批量 OCR，快速从 PNG 文件提取文本。本指南将带您完成完整的 C# OCR 教程，涵盖批量文本提取。
og_title: 如何在 C# 中批量 OCR – 从 PNG 提取文本
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中批量进行 OCR – 从 PNG 提取文本
url: /zh/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR – 从 PNG 提取文本

是否曾经想过 **如何批量 OCR** 一堆截图而不必为每个文件单独编写程序？你并不孤单。在许多项目中，我们会得到数十个需要提取文字的 PNG，逐个处理非常麻烦。  

好消息是？使用 Aspose OCR，你可以快速创建一个小型 C# 控制台应用程序并行处理所有这些图像，从而实现快速的 **批量文本提取** 并得到整洁的结果集。在本指南中，我们将完整演示一个 **c# ocr tutorial**，解释每个环节为何重要，并展示输出的实际样子。

通过本文，你将能够：

* 一次性加载 PNG 文件列表（或任何受支持的图像）。  
* 配置共享的 `OcrEngine`，使设置在整个批次中保持一致。  
* 使用最多四个并行工作者运行识别队列。  
* 获取每页的识别文本并打印到控制台。

没有魔法，只有可以直接放入你项目中的可靠代码。

## 你需要的准备

在开始之前，请确保你拥有：

* .NET 6 SDK（或任何近期的 .NET 版本）。  
* 有效的 Aspose OCR 许可证或临时评估密钥。  
* 包含待处理 PNG 文件的文件夹。  
* Visual Studio 2022 或你喜欢的编辑器。

就这些——除了 `Aspose.OCR` 和标准的 `System.Collections.Generic`，无需额外的 NuGet 包。

## 如何批量 OCR – 项目设置

首先，创建一个新的控制台项目并引入 Aspose OCR 库。

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

恢复完成后，打开 **Program.cs**（或新建文件），并添加常用的 `using` 指令：

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

这段简单的脚手架让我们能够访问 `OcrEngine`、`RecognitionQueue` 以及后续需要的辅助类。

## 从 PNG 提取文本 – 准备图像列表

现在我们需要告诉程序 **哪些 PNG** 需要进行 OCR。最直接的方式是构建一个保存绝对或相对路径的 `List<string>`。

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

将 `YOUR_DIRECTORY` 替换为实际的文件夹路径。如果你的文件集合是动态的，也可以使用 `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")` 并将结果填入列表。关键是 **extract text from PNG** 只需把正确的文件名喂给队列即可。

![如何批量 OCR 工作流](https://example.com/placeholder.png "展示如何对一组 PNG 文件进行批量 OCR 的示意图")

*图片替代文字：如何批量 OCR 工作流图示*

## C# OCR 教程 – 配置识别队列

批量操作的核心是 `RecognitionQueue`。可以把它想象成一条传送带，将每张图像交给共享的 `OcrEngine`。通过共享引擎，我们保持低内存占用并保证每页使用相同的设置。

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

为什么将 `MaxDegreeOfParallelism` 设置为 4？在典型的四核笔记本上，这能提供最佳吞吐量而不会让操作系统资源枯竭。如果在拥有更多核心的服务器上运行，可相应提升此数值。

### 小技巧

如果需要自定义语言包、DPI 设置或感兴趣区域裁剪，请在将任何图像入队之前 **一次性** 在共享的 `Engine` 上完成。例如：

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

所有后续的识别都会自动继承这些选项——这正是 **how to create OCR** 流水线保持一致性的核心所在。

## 批量文本提取 – 入队图像并运行队列

队列准备好后，下一步是将每张图像推入队列。`Enqueue` 方法接受一个 `OcrImage` 实例，我们从文件路径创建它。

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

所有文件入队后，启动处理：

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` 会阻塞直到每张图像处理完毕，然后返回一个列表，列表中每个元素对应输入的顺序。这保证了第 1 页的结果位于索引 0，第 2 页位于索引 1，依此类推——在需要将结果映射回源文件时非常方便。

## 如何创建 OCR – 显示结果

最后，让我们把识别的文本打印到控制台。这里你才能真正看到 **批量文本提取** 的效果。

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

运行程序（`dotnet run`）时，你应该会看到类似下面的输出：

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

如果某张图像处理失败（例如文件损坏），对应的 `OcrResult` 的 `Text` 属性将为空，你可以检查 `ocrResults[i].Exception` 以获取诊断信息。

## 如何创建 OCR – 提示、边缘情况和最佳实践

### 处理大批量

处理数百个 PNG 时，如果一直保留所有 `OcrResult` 对象，仍会占用大量内存。在这种情况下，可在每个结果返回后立即将输出流式写入文件或数据库：

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### 处理非 PNG 格式

Aspose OCR 同时原生支持 JPEG、BMP 和 TIFF。只需在列表中更改文件扩展名或使用通配符搜索即可。相同的 **c# ocr tutorial** 步骤依然适用——无需修改代码。

### 跳过空白页

如果你处理的扫描 PDF 有时会出现空白页，可以过滤掉这些结果：

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### 许可证注意事项

评估版会在每页添加水印。正式使用时，请确保在 `Main` 开头嵌入你的许可证文件：

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### 并行度调优

`MaxDegreeOfParallelism` 默认等于 `Environment.ProcessorCount`。如果发现 CPU 使用率过高或内存压力大，可降低该值。相反，在拥有大量核心的云 VM 上，可提升该值以充分利用硬件。

## 总结

现在你已经拥有一个完整的 **how to batch OCR** C# 解决方案，能够 **extract text from PNG** 文件、并行运行并得到整洁、有序的结果。通过共享单个 `OcrEngine`，你已经掌握了 **how to create OCR** 流水线的内存高效和易维护特性。此 **c# ocr tutorial** 还展示了如何仅通过几行额外代码，将 **batch text extraction** 扩展到数百张图像。

---

### 接下来做什么？

* 尝试添加语言检测（`Engine.Language = Language.AutoDetect`）。  
* 实验不同的输出格式——将结果写入 JSON 或 CSV，以供后续分析使用。  
* 将此批量 OCR 与 PDF‑to‑image 转换步骤结合，处理整套扫描文档。

随意调整并行度、替换为自己的图像来源，或将结果接入搜索索引。掌握了 **how to batch OCR** 在 C# 中后，想象空间无限。

祝编码愉快，愿你的 OCR 运行快速且无错误！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}