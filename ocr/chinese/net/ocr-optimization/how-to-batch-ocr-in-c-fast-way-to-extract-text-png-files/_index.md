---
category: general
date: 2026-04-03
description: 学习如何在 C# 中使用 Aspose.OCR 批量进行 OCR。本指南向您展示如何提取 PNG 图像中的文本并高效地将图像转换为文本。
draft: false
keywords:
- how to batch ocr
- extract text png
- convert images to text
- Aspose OCR
- C# parallel processing
language: zh
og_description: 了解如何在 C# 中批量 OCR，从 PNG 图像中提取文本，并使用 Aspose.OCR 将图像转换为文本。附带完整代码。
og_title: 如何在 C# 中批量 OCR – 快速指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中批量 OCR – 快速提取 PNG 文件的文本
url: /zh/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR – 快速提取 PNG 文件文本

是否曾想过 **如何批量 OCR** 整个文件夹的截图，而不必为每个文件写循环？你并不是唯一有此需求的人。在许多项目中——比如发票数字化或扫描收据归档——你会面对成十甚至上百个需要提取文本的 PNG 文件。好消息是？使用 Aspose.OCR，你可以 **提取文本 PNG** 图像并行处理，整个过程只需几行 C# 代码即可完成。

在本教程中，我们将演示一个完整、可直接运行的示例，展示如何使用批处理器 **将图像转换为文本**。我们会介绍前置条件，解释每行代码的意义，并提供一些专业技巧，帮助你避免后期常见的坑。

## 前置条件

在开始之前，请确保你已经：

- **.NET 6.0**（或更高）已安装在机器上。旧版运行时也能工作，但最新版本提供更好的性能和 async 支持。
- **Aspose.OCR for .NET** 包。可通过 NuGet 获取：`dotnet add package Aspose.OCR`。
- 一个包含待处理 **PNG** 图像的文件夹。本文中将其统一称为 `YOUR_DIRECTORY`。
- 适量的内存——如果并行度调高，批量 OCR 会比较吃内存，但使用 `Environment.ProcessorCount` 可以保持安全。

> **专业提示：** 如果你在 CI/CD 流水线中运行，建议将 Aspose 许可证文件作为密钥添加，以避免免费评估版的 20 页限制。

现在，让我们动手实践。

## 步骤 1：设置批量 OCR 处理器（标题中的主要关键词）

首先需要创建一个 `BatchOcrProcessor` 实例。该类封装了线程逻辑，让你专注于每张图像的处理方式。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Create a batch OCR processor and tell it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };
```

**为什么这很重要：**  
- `Engine = new OcrEngine()` 为每个线程提供全新的 OCR 引擎，避免竞争。  
- `MaxDegreeOfParallelism = Environment.ProcessorCount` 会自动根据 CPU 核心数扩展，实现最佳吞吐量，无需手动调参。

## 步骤 2：挂接进度事件（帮助跟踪提取进度）

在处理上百个文件时，看到进度非常关键。`ProgressChanged` 事件在每个文件处理完毕后触发，方便你记录状态。

```csharp
        // Subscribe to progress updates so we know which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");
```

**你会喜欢的原因：**  
- 实时反馈可以防止你怀疑程序卡死。  
- 若需要暂停或取消，已经有钩子可以检查 `e.Current` 与 `e.Total`。

## 步骤 3：定义文件夹扫描及文件模式（Extract Text PNG）

接下来告诉处理器去哪里找文件以及匹配哪些文件。模式 `"*.png"` 确保只处理 PNG 图像。

```csharp
        // Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"YOUR_DIRECTORY",          // folder containing the images
            "*.png",                    // file pattern
            (imagePath, ocrText) =>     // callback for each processed file
            {
                // Step 4 is inside this callback – see next section
            });
```

**关键所在：**  
- 使用全局匹配模式使代码更灵活；以后若需处理 JPEG，只需将 `*.png` 改为 `*.jpg`。  
- 回调同时收到图像路径和识别文本，便于你自行决定后续操作。

## 步骤 4：将识别文本保存到源文件旁边（Convert Images to Text）

在回调中，我们会把 OCR 输出写入与原 PNG 同目录的 `.txt` 文件。这是将 **将图像转换为文本** 用于后续处理的最简方式。

```csharp
                // Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
```

**为何选择并列的 `.txt` 文件：**  
- 关系一目了然——打开 PNG，打开对应的 TXT，即可对比。  
- 小规模项目无需数据库或额外存储层。

## 步骤 5：以友好的完成信息收尾

一条简洁的控制台信息告诉你全部工作已结束。

```csharp
        // Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

运行程序后，你会看到类似以下的输出：

```
Processed 1/27: C:\Images\invoice1.png
Processed 2/27: C:\Images\invoice2.png
...
Batch processing completed.
```

每个 PNG 现在都有一个对应的 `.txt` 文件，里面保存了提取的文本。

## 完整可运行示例（所有步骤合并）

下面是可以直接复制到新控制台项目中的完整代码。只需将 `YOUR_DIRECTORY` 替换为你的图片绝对路径。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create a batch OCR processor and configure it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 2: Subscribe to progress updates to see which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");

        // Step 3: Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"C:\MyImages",          // folder containing the images
            "*.png",                // file pattern
            (imagePath, ocrText) => // callback for each processed file
            {
                // Step 4: Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
            });

        // Step 5: Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

### 预期结果

- 对于 `C:\MyImages` 下的每个 `image.png`，会在旁边生成 `image.txt`。  
- 控制台会打印进度行，便于监控大批量任务。  
- 无需手动循环或线程管理——`BatchOcrProcessor` 已帮你处理一切。

## 常见问题与边缘情况

### 我的图像不是 PNG，怎么办？

只需将 `ProcessFolder` 的第二个参数改为 `"*.jpg"` 或 `"*.*"`，即可处理 JPEG 或所有文件。OCR 引擎支持大多数光栅格式。

### 这会占用多少内存？

`BatchOcrProcessor` 每个线程加载一张图像。比如 `Environment.ProcessorCount` 为 8 核心时，最多会有 8 张图像同时驻留内存。若出现 OutOfMemory 异常，可降低并行度：

```csharp
MaxDegreeOfParallelism = 4; // or any number that fits your machine
```

### 能自定义 OCR 语言吗？

当然可以。创建引擎后，设置其 `Language` 属性：

```csharp
Engine = new OcrEngine { Language = Language.English };
```

Aspose 支持多种语言；如有需要，只需添加相应的 NuGet 包。

### 错误处理该怎么做？

在回调中使用 try/catch 并记录失败。处理器会继续下一个文件，防止单个损坏的图像导致整个任务中止。

```csharp
(imagePath, ocrText) =>
{
    try
    {
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, ocrText);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {imagePath}: {ex.Message}");
    }
}
```

## 扩展规模的专业技巧

- **分块文件夹**：如果文件数量达数万，可将其拆分为子文件夹，依次运行多个批处理任务。  
- **使用云 VM**：拥有更多核心的机器（例如 32 核）能够显著加速完成时间。记得相应调整许可证限制。  
- **后处理文本**：提取后可使用正则表达式抽取发票号或日期等信息。`.txt` 文件正好是此类管道的理想输入。

## 结论

现在，你已经掌握了一套完整、可投入生产的 **如何批量 OCR** 目录下 PNG 文件、**提取文本 PNG** 文件以及 **将图像转换为文本** 的方案，全部基于 Aspose.OCR 与 C#。示例代码自成一体，解释了每行代码背后的“为什么”，并提供了处理更大工作负载或不同文件类型的技巧。

准备好下一步了吗？尝试将回调改为将结果写入数据库，或在 OCR 前加入图像预处理（如去倾斜）。该模式易于扩展，能够适配任何批处理场景。

祝编码愉快，愿你的 OCR 流水线快速且无错误！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}