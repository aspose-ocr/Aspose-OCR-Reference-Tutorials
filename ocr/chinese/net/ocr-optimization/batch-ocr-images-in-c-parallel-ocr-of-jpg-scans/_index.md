---
category: general
date: 2026-04-29
description: 使用 Aspose OCR 在 C# 中快速批量 OCR 图像。了解如何从 JPG 文件提取文本、读取扫描件中的文字，以及并行处理图像列表。
draft: false
keywords:
- batch OCR images
- extract text from jpg
- read text from scans
- parallel OCR processing
- process image list
language: zh
og_description: 使用 Aspose OCR 快速批量 OCR 图像。本指南展示了如何从 JPG 提取文本、读取扫描件中的文本，以及并行处理图像列表。
og_title: 在 C# 中批量 OCR 图像 – JPG 扫描的并行 OCR
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 在 C# 中批量 OCR 图像 – 并行 OCR JPG 扫描
url: /zh/net/ocr-optimization/batch-ocr-images-in-c-parallel-ocr-of-jpg-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中批量 OCR 图像 – JPG 扫描的并行 OCR

是否曾需要**批量 OCR 图像**，但不确定如何在多个文件之间扩展工作？你并不孤单——开发者在尝试逐个读取扫描件的文本时常常遇到瓶颈。好消息是，使用 Aspose OCR，你可以**从 jpg 文件中提取文本**、**从扫描件读取文本**，以及**并行处理图像列表**，只需几行 C# 代码。

在本教程中，我们将逐步演示一个完整、可直接运行的示例，展示如何实现上述功能。完成后，你将拥有一个独立的控制台应用程序，能够识别 JPEG 扫描文件夹中的图像，打印每页的文本，并显示每个操作所耗时间。无需查找外部文档，也没有不完整的代码片段——只需一个完整的解决方案，直接放入 Visual Studio 即可运行。

## 你需要的环境

- **.NET 6.0** 或更高（代码同样可以在 .NET Framework 4.6+ 上编译）
- **Aspose.OCR** NuGet 包 (`Install-Package Aspose.OCR`)
- 需要处理的若干 JPG 或扫描图像文件
- 任意你喜欢的 IDE；我使用 Visual Studio 2022，但 VS Code 也完全可用

就这些。如果你已经拥有该 NuGet 包，就可以开始了。

## 步骤 1 – 初始化 OCR 引擎（批量 OCR 图像设置）

我们首先创建一个 `OcrEngine` 实例，并指定要识别的语言。大多数情况下英语已经足够，但你可以将 `OcrLanguage.English` 替换为任何受支持的语言。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine and set the language to English
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };
```

*为什么重要：* 只初始化一次引擎并在所有图像间复用，要比对每个文件创建新实例高效得多。这也让 Aspose 能共享内部资源，这对于**并行 OCR 处理**至关重要。

## 步骤 2 – 构建图像列表（处理图像列表）

接下来我们定义要提供给批量识别器的文件路径集合。你可以使用 `Directory.GetFiles` 动态生成此列表，但为保持清晰，这里我们硬编码几条路径。

```csharp
        // Step 2: Define the image files that will be processed
        var imagePaths = new List<string>
        {
            @"YOUR_DIRECTORY/page1.jpg",
            @"YOUR_DIRECTORY/page2.jpg",
            @"YOUR_DIRECTORY/page3.jpg"
        };
```

*提示：* 如果有成千上万的扫描件，建议使用 `Directory.EnumerateFiles` 并加上 `*.jpg` 过滤，以避免一次性将整个列表加载到内存中。

## 步骤 3 – 运行批量识别（并行 OCR 处理）

现在进入关键步骤：调用 `BatchRecognize`。该方法接受 `maxDegreeOfParallelism` 参数，用于控制 Aspose 启动的线程数。默认使用四个线程，但如果你的 CPU 核心更多，可以将其调高。

```csharp
        // Step 3: Run batch recognition (4 parallel threads by default)
        var recognitionResults = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);
```

*内部原理是什么？* Aspose 将 `imagePaths` 集合拆分为若干块，分别交给不同线程处理，然后汇总结果。当你拥有可以并发处理的**处理图像列表**时，这是**从 jpg 文件中提取文本**的最高效方式。

## 步骤 4 – 显示结果（从扫描件读取文本）

最后我们遍历 `recognitionResults` 集合，打印每个文件的文本和处理时间。`OcrResult` 对象还提供源文件名，便于在记录或存储输出时使用。

```csharp
        // Step 4: Output the results for each image
        foreach (var result in recognitionResults)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

**预期输出（示例）：**

```
File: C:\Scans\page1.jpg
Time: 1.34s
The quick brown fox jumps over the lazy dog.
----------------------------------------
File: C:\Scans\page2.jpg
Time: 1.27s
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----------------------------------------
File: C:\Scans\page3.jpg
Time: 1.41s
Invoice #12345
Total: $1,250.00
----------------------------------------
```

请注意，每个块都会显示文件名、OCR 所耗时间以及提取的文本。这正是你在生产流水线中**从扫描件读取文本**时所需的信息。

## 处理常见边缘情况

| Situation | What to Watch For | Quick Fix |
|-----------|-------------------|-----------|
| **文件缺失** | `FileNotFoundException` 在 `BatchRecognize` 中抛出 | 在添加到 `imagePaths` 前使用 `File.Exists` 验证路径。 |
| **不支持的格式** | Aspose 仅支持光栅图像（JPG、PNG、BMP、TIFF）。 | 先将 PDF 转为图像（使用 Aspose.PDF），或跳过这些文件。 |
| **内存压力** | 在多线程运行时，超大图像会占用大量内存。 | 降低 `maxDegreeOfParallelism`，或在 OCR 前缩放图像。 |
| **非英文文本** | 语言设置为英文会遗漏其他文字。 | 将 `Language = OcrLanguage.French`（或多语言组合）进行更改。 |

这些技巧可以让你的批处理作业更稳健，尤其是在处理来自用户上传或扫描档案的**处理图像列表**时。

## 专业提示 – 调整并行度

如果在 8 核机器上运行，可将并行度调至 6 或 8，以观察速度提升。但请记住，每个线程也会消耗位图内存。一个经验法则是：

```csharp
int cores = Environment.ProcessorCount;
int maxThreads = Math.Max(1, cores - 1); // leave one core free for UI/OS
```

将 `maxThreads` 传入 `BatchRecognize`，即可实现动态、机器感知的配置。

## 完整可运行示例（复制粘贴即用）

下面是完整的程序，已准备好编译。只需将 `YOUR_DIRECTORY` 替换为存放 JPG 扫描文件的路径即可。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine – English language
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };

        // 2️⃣ Build the list of image files to process
        var imagePaths = new List<string>();
        string folder = @"C:\Scans"; // <-- change this
        foreach (var file in Directory.EnumerateFiles(folder, "*.jpg"))
        {
            imagePaths.Add(file);
        }

        if (imagePaths.Count == 0)
        {
            Console.WriteLine("No JPG files found in the specified folder.");
            return;
        }

        // 3️⃣ Run batch OCR – let the library use 4 threads (adjust as needed)
        var results = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);

        // 4️⃣ Output each result
        foreach (var result in results)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

> **注意：** `using System.IO;` 行是 `Directory` 辅助所必需的。如果未找到 JPG，代码会打印友好提示，防止静默失败。

## 结论

我们刚刚演示了一个简洁的 **批量 OCR 图像** 工作流，能够 **从 jpg 文件中提取文本**、**从扫描件读取文本**，并使用 **并行 OCR 处理** 高效 **处理图像列表**。完整的可运行示例展示了如何初始化引擎、提供文件集合以及处理结果——同时保持内存使用和线程数在可控范围内。

准备好下一步了吗？尝试将语言切换为法语，添加 PDF 转图像的转换，或将 OCR 文本存入数据库。模式保持不变：一次初始化，提供列表，让 Aspose 并行完成繁重工作。

有问题或想分享自己的改动吗？在下方留言吧，祝编码愉快！ 

![批量 OCR 图像处理流程](https://example.com/placeholder.png "展示批量 OCR 图像工作流的示意图")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}