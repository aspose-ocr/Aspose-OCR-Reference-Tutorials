---
category: general
date: 2026-02-19
description: 学习如何在 C# 中使用 Aspose.OCR 批量 OCR。本指南向您展示如何高效地从图像中提取文本并将图像转换为 txt。
draft: false
keywords:
- how to batch ocr
- extract text from images
- convert images to txt
- Aspose OCR batch processing
- C# image to text conversion
language: zh
og_description: 如何在 C# 中使用 Aspose.OCR 批量 OCR。只需几个简单步骤，即可从图像中提取文本并将图像转换为 txt。
og_title: 如何在 C# 中批量 OCR – 快速图像转文本转换
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中批量 OCR – 快速从图像中提取文本
url: /zh/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR – 完整分步指南

有没有想过 **如何批量 OCR** 整个文件夹的图片，而不必为每个文件编写单独的程序？你并不是唯一的。许多开发者在需要从数十甚至数千页扫描的文档、收据或截图中提取文本时会遇到瓶颈。好消息是？使用 Aspose.OCR，你可以自动化整个流程，**从图像中提取文本**，并 **将图像转换为 txt**，只需几行代码。

在本教程中，我们将逐步演示一个完整、可直接运行的示例，展示如何设置 OCR 批处理器、调整预处理、处理并行以及将每个结果写入 `.txt` 文件。完成后，你将拥有一个可自行包含的控制台应用程序，能够直接嵌入任何 .NET 项目。

## 您需要的条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）
- Aspose.OCR for .NET NuGet 包（`Aspose.OCR`）  
- 一个包含待处理图像文件（`.png`、`.jpg` 等）的文件夹
- 适量的内存；演示使用 4 条并行线程，你可以自行调整

无需外部服务，无需隐藏的配置文件——只需纯 C# 代码，今天即可编译运行。

![展示批量 OCR 处理流程的图示](/images/how-to-batch-ocr-flow.png "批量 OCR 流程图")

## 第 1 步：安装 Aspose.OCR 并创建项目

首先，将 Aspose.OCR 包添加到你的项目中：

```bash
dotnet add package Aspose.OCR
```

**为什么这很重要**：Aspose.OCR 已经打包了 OCR 引擎、语言数据和预处理工具，你不需要任何第三方二进制文件。安装完包后，创建一个新的控制台应用（或在已有项目中添加代码），并引入所需的命名空间：

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
```

这些 `using` 语句让你能够使用批处理器类和实用的 I/O 辅助功能。

## 第 2 步：配置 OCR 批处理器

现在我们将实例化 `OcrBatchProcessor`，并指定要识别的语言、图像清理方式以及并行线程数。这是高效 **批量 OCR** 的核心。

```csharp
// Step 2: Create and configure the OCR batch processor
var ocrBatch = new OcrBatchProcessor
{
    // Language selection – English is the most common, but you can change it
    Language = Language.English,

    // Preprocessing improves accuracy; Deskew removes rotation
    Preprocessing = new PreprocessingOptions
    {
        Deskew = DeskewAdvanced.Enable()
    },

    // Parallelism – adjust based on your CPU/GPU capabilities
    MaxDegreeOfParallelism = 4
};
```

**为什么要启用 Deskew？** 许多扫描文档并未完全对齐；Deskew 算法会将它们旋转回水平基线，通常能提升 10‑15 % 的识别率。

## 第 3 步：挂载结果回调以保存文本文件

批处理器会为每张处理完的图像触发一次事件。我们订阅 `ResultProcessed`，将每个 OCR 结果写入 `.txt` 文件——实际上实现了 **将图像转换为 txt** 的即时转换。

```csharp
// Step 3: Register a callback to save each OCR result as a text file
ocrBatch.ResultProcessed += (sender, args) =>
{
    // Change the original file extension to .txt
    string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");

    // Write the recognized text to the new file
    File.WriteAllText(txtPath, args.Result.Text);

    // Inform the console for debugging / progress monitoring
    Console.WriteLine($"Processed: {args.ImagePath}");
};
```

小技巧：如果需要保留原始文件夹结构，可以修改 `txtPath`，让其包含子文件夹或指向单独的输出目录。

## 第 4 步：对图像文件夹执行批处理

剩下的工作就是把处理器指向存放待 **从图像中提取文本** 的图片的文件夹。`ProcessFolder` 方法会递归扫描子文件夹，你只需放入整个扫描树，库会自行完成其余工作。

```csharp
// Step 4: Run the batch on all image files in the target folder
ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
```

运行程序后，你会看到类似下面的控制台输出：

```
Processed: C:\Path\To\Your\Images\invoice1.png
Processed: C:\Path\To\Your\Images\receipt_2024.jpg
...
```

每张图片现在都有一个对应的 `.txt` 文件，里面保存了提取的文本。

## 完整可运行示例

将所有代码组合在一起，下面是可以直接复制粘贴到 `Program.cs` 的完整程序：

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR batch processor
        var ocrBatch = new OcrBatchProcessor
        {
            Language = Language.English,
            Preprocessing = new PreprocessingOptions
            {
                Deskew = DeskewAdvanced.Enable()
            },
            // Step 2: Define the level of parallelism (adjust for your CPU/GPU)
            MaxDegreeOfParallelism = 4
        };

        // Step 3: Register a callback to save each OCR result as a text file
        ocrBatch.ResultProcessed += (sender, args) =>
        {
            string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");
            File.WriteAllText(txtPath, args.Result.Text);
            Console.WriteLine($"Processed: {args.ImagePath}");
        };

        // Step 4: Run the batch on all image files in the target folder
        ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
    }
}
```

### 预期输出

- 对源目录下的每个 `*.png` 或 `*.jpg`，都会在同目录生成对应的 `*.txt` 文件。
- 控制台会为每个文件输出一行，提供实时反馈。
- 如果某张图片无法读取（文件损坏、不支持的格式），Aspose.OCR 会记录错误并继续处理其余文件——这得益于批处理引擎内置的鲁棒性。

## 常见问题与边缘情况

### 如果需要处理 PDF 而不是图像怎么办？

Aspose.OCR 可以内部将 PDF 页面当作图像处理，但你需要先将 PDF 转换为光栅图像（例如使用 Aspose.PDF）。得到 PNG 后，批处理代码无需修改即可使用。

### 能否动态切换语言？

可以。`Language` 属性接受任意 `Language` 枚举值（西班牙语、法语、中文等）。如果文档包含多语言，考虑分别运行两遍——每种语言一次，或使用 `Language.AutoDetect`。

### 如何限制批处理只处理特定文件类型？

`ProcessFolder` 支持可选的 `SearchOption` 和 `string[] extensions` 参数。例如：

```csharp
ocrBatch.ProcessFolder(@"C:\Images", new[] { ".png", ".tif" });
```

### GPU 加速支持吗？

Aspose.OCR 通过 `OcrEngine` 配置支持 GPU，但批处理器的 `MaxDegreeOfParallelism` 仍是并发的主要控制参数。如果有兼容的 GPU，请在创建 `OcrBatchProcessor` 前于引擎设置中启用它。

### 如何处理非常大的文件夹（成千上万的文件）？

- 谨慎提升 `MaxDegreeOfParallelism`，线程过多会耗尽内存。
- 使用专用的输出文件夹，避免目录混乱。
- 定期将日志刷新到磁盘，防止内存膨胀。

## 高质量 OCR 的专业技巧

- **DPI 重要**：300 DPI 及以上的图像可获得最佳准确率。如果扫描分辨率较低，考虑使用双三次滤波进行放大后再处理。
- **噪声消除**：如果源图像颗粒感强，开启 `Preprocessing.NoiseRemoval`。
- **文件命名**：保持文件名简短且仅使用字母数字；特殊字符可能导致回调路径逻辑出错。
- **日志记录**：在生产环境中，用专业日志框架（如 `Serilog`）替代 `Console.WriteLine`。

## 后续步骤

既然你已经掌握了 **批量 OCR**，接下来可以：

- **从图像中提取文本** 并将输出导入搜索索引（如 Elasticsearch）实现全文检索。
- **将图像转换为 txt**，随后进行自然语言处理（NLP）以自动分类文档。
- 试验 **不同语言包** 或自定义词典，以适配行业专用术语。

如果你对后处理感兴趣，可查看 “使用正则表达式解析 OCR 输出” 或 “将 OCR 结果存入 SQL 数据库” 等教程。

---

**祝编码愉快！** 随意调整并行度、添加更多预处理步骤，或将整个程序封装为 Windows 服务实现持续监控。结合 Aspose.OCR 的批处理能力和一点 .NET 创意，天地皆可为你所用。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}