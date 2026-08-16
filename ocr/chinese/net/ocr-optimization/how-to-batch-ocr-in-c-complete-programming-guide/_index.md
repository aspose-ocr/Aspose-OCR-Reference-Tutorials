---
category: general
date: 2026-03-13
description: 如何快速可靠地批量 OCR，并学习使用 Aspose.OCR 从 TIFF 文件中提取文本。请按照本分步教程操作。
draft: false
keywords:
- how to batch OCR
- extract text from tiff
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: zh
og_description: 学习如何在 C# 中批量 OCR，并使用 Aspose.OCR 从 TIFF 文件中提取文本。本指南涵盖设置、代码和最佳实践技巧。
og_title: 如何在 C# 中批量 OCR – 完整编程指南
tags:
- OCR
- C#
- Aspose
- Batch processing
title: 如何在 C# 中批量进行 OCR – 完整编程指南
url: /zh/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR – 完整编程指南

是否曾想过 **如何批量 OCR** 大量扫描的发票，而不必为每个文件编写单独的脚本？你并非唯一遇到此问题的人。在许多真实项目中，痛点并非 OCR 的准确性本身，而是需要转换为可搜索文本的图像（通常是 TIFF）的庞大数量。

本教程将展示 **如何批量 OCR**，使用 Aspose.OCR 的 `BatchProcessor`，并教你如何在一次干净的运行中 **从 tiff 中提取文本**。完成后，你将拥有一个可直接运行的控制台应用程序，能够处理整个文件夹，利用可选的 GPU 加速，并将纯文本结果输出到你指定的位置。

## 所需条件

- **.NET 6+**（或如果你更喜欢传统运行时，可使用 .NET Framework 4.7.2）  
- **Aspose.OCR for .NET** – 可通过 `dotnet add package Aspose.OCR` 获取 NuGet 包。  
- 一个包含 **TIFF** 图像的文件夹（教程中使用 `Invoices` 作为示例）。  
- 可选：支持 DirectX 11 或 CUDA 的 GPU，以加速处理。  

无需额外服务，无需云密钥——只需一个本地 C# 项目和 Aspose 库。

## 第一步：创建项目并安装 Aspose.OCR

首先，创建一个控制台应用。

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **小贴士：** 如果你在 Windows 上并计划使用 GPU 加速，请确保已安装最新的显卡驱动程序。否则 `UseGpu = true` 标志会自动回退到 CPU。

## 第二步：创建 BatchProcessor 配置

现在我们来配置 `BatchProcessor`。这就是 **如何批量 OCR** 的核心——你告诉 Aspose 期望的语言、要应用的预处理过滤器，以及是否使用 GPU。

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 2: Configure the batch processor
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                // Primary language – English works for most invoices
                Language = Language.English,

                // Set to true if you have a compatible GPU; otherwise false
                UseGpu = true,

                // Optional pre‑processing to improve OCR accuracy
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),   // straightens tilted scans
                    new DespeckleFilter() // removes speckles and noise
                }
            };
```

**为什么要这样设置？**  
- `Language = Language.English` 告诉引擎使用英文语言模型，其准确性远高于通用模型。  
- `UseGpu` 在性能良好的 GPU 上可以将处理时间减半，但如果你的笔记本没有 GPU，保持 `false` 也是安全的。  
- 过滤器管道模拟人工操作：先校正页面倾斜，再去除斑点，然后再交给 OCR 引擎。

## 第三步：指向你的 TIFF 文件夹

接下来 **如何批量 OCR** 的关键是告诉库源文件所在位置。支持通配符，你可以一次性获取所有 `.tif` 文件。

```csharp
            // -------------------------------------------------
            // Step 3: Add the folder containing TIFF images
            // -------------------------------------------------
            // Replace YOUR_DIRECTORY with the actual path on your machine
            batchProcessor.AddFolder(@"C:\Data\Invoices", "*.tif");
```

> **边缘情况：** 如果你的图像扩展名混杂（`.tiff`、`.tif`、`.png`），请多次调用 `AddFolder`，或使用 `*.*` 并在代码中后期过滤。

## 第四步：选择 OCR 结果的输出位置

你可能会想，“提取的文本到底保存在哪里？”这正是 **如何批量 OCR** 的第三个支柱——定义输出位置和格式。我们将在原文件旁边存放纯文本文件。

```csharp
            // -------------------------------------------------
            // Step 4: Define output folder and format
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;
```

如果需要 JSON 或 XML 而不是纯文本，只需将 `OutputFormat.PlainText` 替换为 `OutputFormat.Json` 或 `OutputFormat.Xml`。库会自动完成转换。

## 第五步：运行批处理任务并报告结果

最后，启动任务。`Execute` 方法会阻塞，直至所有文件处理完毕，然后你可以检查 `ProcessedCount` 以确认成功。

```csharp
            // -------------------------------------------------
            // Step 5: Execute the batch job
            // -------------------------------------------------
            batchProcessor.Execute();

            // Simple verification output
            Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
            Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
        }
    }
}
```

### 预期输出

运行程序后，控制台会打印类似以下内容：

```
Batch completed. Processed files: 42
Check C:\Data\Output for .txt files containing extracted text.
```

在 `Output` 文件夹中，你会看到每个源 TIFF 对应的 `.txt` 文件，文件名与原图像相同（例如 `Invoice_001.txt`）。打开任意文件，即可看到原始 OCR 文本——这非常适合喂入搜索索引或后续的数据提取管道。

## 常见问题处理

### 1. GPU 不可用

如果 `UseGpu = true` 但未检测到兼容设备，Aspose 会静默回退到 CPU。若想显式捕获，可捕获 `DeviceNotFoundException`：

```csharp
try
{
    batchProcessor.Execute();
}
catch (DeviceNotFoundException)
{
    Console.WriteLine("GPU not detected – switching to CPU mode.");
    batchProcessor.UseGpu = false;
    batchProcessor.Execute();
}
```

### 2. 同一文件夹中有非 TIFF 文件

当文件夹中混有其他类型文件时，可在代码中进行过滤：

```csharp
var tiffFiles = Directory.GetFiles(@"C:\Data\Invoices", "*.*")
                         .Where(f => f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase) ||
                                     f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));

foreach (var file in tiffFiles)
    batchProcessor.AddFile(file);
```

### 3. 超大文件导致内存不足

对于巨大的多页 TIFF，启用流式处理：

```csharp
batchProcessor.EnableMemoryManagement = true; // reduces RAM footprint
```

## 提升 **从 tiff 中提取文本** 准确性的专业技巧

- **分辨率很重要** – 目标为 300 dpi 或更高。低于此值 OCR 引擎可能会漏字符。  
- **彩色 vs. 灰度** – 在 OCR 前将彩色扫描转换为灰度；`DeskewFilter` 已在内部完成此操作，但你可以额外添加 `ColorDepthReductionFilter` 以提升速度。  
- **后处理** – 获得纯文本后，可运行拼写检查或正则清理，以修复常见的 OCR 错误（例如 “0” 与 “O” 的混淆）。

## 完整可运行示例（复制粘贴即用）

下面是完整的程序代码，只需将占位路径替换为你自己的目录即可。

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Configure the batch processor (how to batch OCR)
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                Language = Language.English,
                UseGpu = true, // set false if no GPU
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),
                    new DespeckleFilter()
                },
                EnableMemoryManagement = true // helps with huge TIFFs
            };

            // -------------------------------------------------
            // Add source TIFF files
            // -------------------------------------------------
            string sourceFolder = @"C:\Data\Invoices";
            batchProcessor.AddFolder(sourceFolder, "*.tif");

            // -------------------------------------------------
            // Optional: add only TIFFs if folder contains other images
            // -------------------------------------------------
            var extraTiffs = Directory.GetFiles(sourceFolder, "*.*")
                                      .Where(f => f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));
            foreach (var file in extraTiffs)
                batchProcessor.AddFile(file);

            // -------------------------------------------------
            // Define where results go
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;

            // -------------------------------------------------
            // Execute the batch job
            // -------------------------------------------------
            try
            {
                batchProcessor.Execute();
                Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
                Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
            }
            catch (DeviceNotFoundException)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
                batchProcessor.UseGpu = false;
                batchProcessor.Execute();
                Console.WriteLine($"Batch completed (CPU). Processed files: {batchProcessor.ProcessedCount}");
            }
        }
    }
}
```

编译并运行：

```bash
dotnet run
```

现在，你应该拥有一套整齐的 `.txt` 文件——每个文件都是通过全自动批处理 **从 tiff 中提取文本** 的结果。

## 结论

我们已经从头到尾演示了 **如何在 C# 中批量 OCR**，并高效 **从 tiff 中提取文本**。关键要点如下：

1. 使用 Aspose.OCR 的 `BatchProcessor`，避免编写重复的循环。  
2. 利用预处理过滤器（去倾斜、去斑点）提升准确性。  
3. 在可能的情况下启用 GPU 加速，但始终保留 CPU 备选。  
4. 将结果存放在可预测的文件夹结构中，以便下游任务自动读取。

接下来，你可以探索：

- 将纯文本导入 **搜索索引**（如 Elasticsearch），实现发票可搜索。  
- 将输出转换为 **JSON**，并喂入机器学习模型以提取明细行。  
- 为损坏的 TIFF 或权限问题添加 **错误处理**。

祝你玩得开心，

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}