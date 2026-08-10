---
category: general
date: 2026-05-06
description: 学习如何在 C# 中批量 OCR，并使用 Aspose OCR Batch 快速从扫描件中提取文本。遵循完整的逐步指南，包含代码、技巧和边缘案例处理。
draft: false
keywords:
- how to batch OCR
- extract text from scans
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: zh
og_description: 如何在 C# 中批量进行 OCR？本指南展示了如何使用 Aspose OCR、GPU 支持和并行处理，高效地从扫描件中提取文本。
og_title: 如何在 C# 中批量 OCR – 从扫描件提取文本
tags:
- C#
- OCR
- Aspose
title: 如何在 C# 中批量 OCR – 从扫描件提取文本
url: /zh/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR – 从扫描件提取文本

是否曾经想过 **如何批量 OCR**，当你手头有一个装满扫描 PDF 或 JPEG 的文件夹时？你并不是唯一一个面对大量图像并想：“一定有更快的方式把文本提取出来”。在本教程中，我们将一步步演示一个实用方案，它不仅可以 **从扫描件提取文本**，还能通过 GPU 加速和并行处理提升速度。

事实是：一次只处理一个文件的 OCR 是巨大的时间消耗，尤其是当你要处理数十甚至数百页时。阅读完本指南后，你将拥有一个可直接运行的 C# 控制台应用，它可以一次性处理整个目录，生成干净的文本文件，供索引、搜索或后续处理使用。

## 前置条件

在开始之前，请确保你具备：

- **.NET 6.0 或更高版本**（代码使用了现代 C# 特性）。
- **Aspose.OCR 的许可证**（免费试用版可用于测试）。
- 若想启用 `UseGpu`，需要一台 **支持 GPU 的机器**；否则库会自动回退到 CPU。
- 对 **C# 控制台应用** 有基本了解。

无需外部服务、无需隐藏的配置文件——只需要 SDK 和一文件夹的图像。

## 第一步：安装 Aspose.OCR NuGet 包

首先，将 Aspose OCR 库添加到项目中。打开解决方案文件夹的终端，运行：

```bash
dotnet add package Aspose.OCR
```

这会把 `Aspose.OCR` 及其批处理命名空间拉进来，后面我们将使用它来 **批量 OCR**。

> **小技巧：** 如果你使用 Visual Studio，也可以通过 NuGet 包管理器 UI 添加该包。

## 第二步：创建控制台应用骨架

我们先搭建一个最小的控制台应用来承载批处理器。新建一个名为 `Program.cs` 的文件，并粘贴以下骨架代码：

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll configure and run the OCR batch processor here.
        }
    }
}
```

为什么把逻辑放在 `Main` 里？因为控制台应用可以通过 `Console.WriteLine` 即时反馈，便于快速验证 **批量 OCR** 作业是否真正完成。

## 第三步：配置 OcrBatchProcessor

下面进入核心实现。我们将实例化 `OcrBatchProcessor`，指向输入文件夹，设置结果输出位置，并调节几个性能参数。

```csharp
// Step 3: Configure the OCR batch processor
var batch = new OcrBatchProcessor
{
    // Folder that contains the source images to be processed
    InputFolder = @"YOUR_DIRECTORY/Scans",

    // Folder where the OCR results will be saved
    OutputFolder = @"YOUR_DIRECTORY/OcrResults",

    // Specify the language of the documents (Spanish in this example)
    Language = OcrLanguage.Spanish,

    // Enable GPU acceleration for faster processing (if available)
    UseGpu = true,

    // Limit the number of concurrent OCR operations
    MaxDegreeOfParallelism = 4
};
```

### 为什么这些设置很重要

| 设置 | 功能说明 | 何时需要更改 |
|------|----------|--------------|
| `InputFolder` | 要处理的扫描文件所在路径。 | 为了可移植性，可使用相对路径。 |
| `OutputFolder` | 每张图片提取的文本将保存为 `.txt` 文件的目标文件夹。 | 若需集中存储，可指向网络共享。 |
| `Language` | OCR 语言模型；此处使用西班牙语演示多语言支持。 | 切换为 `OcrLanguage.English` 或其他受支持语言。 |
| `UseGpu` | 将大量矩阵计算交给 GPU 处理。 | 在没有 GPU 的无头服务器上设为 `false`。 |
| `MaxDegreeOfParallelism` | 控制一次并行处理的图像数量。 | 在低 CPU 机器上降低此值以避免过度占用。 |

## 第四步：执行批处理并加入错误处理

运行批处理只需调用 `Execute()`，但我们会把它包在 try‑catch 中，这样如果出现问题（例如缺少文件夹、图像格式不受支持）时，你会得到友好的提示信息。

```csharp
try
{
    // Step 4: Run the batch OCR operation
    batch.Execute();

    // Step 5: Inform the user that processing has finished
    Console.WriteLine("Batch completed.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
}
```

当处理器完成后，控制台会显示 **Batch completed.**，并且每个源图像在 `OcrResults` 中会生成对应的 `.txt` 文件。文件名与原图保持一致，便于映射回原始扫描件。

## 第五步：验证输出 – 预期结果

程序运行完毕后，打开 `YOUR_DIRECTORY/OcrResults` 下的任意文件。你应该能看到从对应图像提取出的纯文本，例如：

```
Este es un documento de prueba.
Contiene varias líneas de texto.
```

如果输出出现乱码，请再次确认 `Language` 与扫描件的语言相匹配。Aspose OCR 支持 100 多种语言，你可以将 `OcrLanguage.Spanish` 替换为任何需要的语言。

## 处理边缘情况和常见陷阱

### 1. GPU 不可用

如果机器没有兼容的 GPU，`UseGpu = true` 会静默回退到 CPU 模式，但会失去加速效果。若想明确检测 GPU 能力，可使用：

```csharp
if (!OcrBatchProcessor.IsGpuSupported)
{
    batch.UseGpu = false;
    Console.WriteLine("GPU not detected – falling back to CPU processing.");
}
```

### 2. 大文件导致内存不足

处理巨大的 TIFF 或 PDF 时，建议先将其拆分为更小的图像。Aspose OCR 能处理多页 PDF，但内存消耗随页数增长。可以使用 `Aspose.Imaging` 预处理，将文档切割成可管理的块。

### 3. 输入文件夹中出现非图像文件

批处理器会忽略无法解析的文件，但保持文件夹整洁是个好习惯。你可以通过扩展名进行过滤：

```csharp
batch.InputFolder = @"YOUR_DIRECTORY/Scans";
batch.FileFilter = file => file.EndsWith(".png", StringComparison.OrdinalIgnoreCase)
                         || file.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase);
```

*（注：`FileFilter` 为假设属性；如有实际 API，请替换为对应实现。）*

## 完整可运行示例

下面给出完整的、可直接复制粘贴的程序。将 `YOUR_DIRECTORY` 替换为你机器上的绝对路径。

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Configure the batch processor
            var batch = new OcrBatchProcessor
            {
                InputFolder = @"C:\MyScans",          // <-- change this
                OutputFolder = @"C:\OcrResults",     // <-- change this
                Language = OcrLanguage.Spanish,
                UseGpu = true,
                MaxDegreeOfParallelism = 4
            };

            // Optional: fall back to CPU if no GPU is found
            if (!OcrBatchProcessor.IsGpuSupported)
            {
                batch.UseGpu = false;
                Console.WriteLine("GPU not detected – using CPU.");
            }

            try
            {
                // Run the batch job
                batch.Execute();

                Console.WriteLine("Batch completed.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### 预期的控制台输出

```
Batch completed.
```

在 `C:\OcrResults` 中，你会看到每个 `C:\MyScans` 中图像对应的 `.txt` 文件。

## 结论

现在，你已经掌握了一种可靠、可投入生产的 **在 C# 中批量 OCR** 方法，能够 **从扫描件提取文本**，无需手动打开每个文件。借助 Aspose 的批处理 API、GPU 加速以及可配置的并行度，该方案可以从少量页面扩展到成千上万页。

接下来可以尝试以下思路：

- **与搜索索引集成**（例如 Elasticsearch），让提取的文本可搜索。
- **添加后处理**，如拼写检查或语言检测。
- **将控制台应用封装为 Windows Service**，实现对投递文件夹的持续监控。

欢迎自行实验、调节并行度或更换语言模型。如遇到任何问题，欢迎在下方留言——祝你 OCR 顺利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}