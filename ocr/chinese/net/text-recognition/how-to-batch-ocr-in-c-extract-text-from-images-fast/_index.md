---
category: general
date: 2026-03-21
description: 如何在 C# 中简化批量 OCR——学习从图像中提取文本、将图像转换为文本，并使用语言设置将 OCR 保存为文本。
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: zh
og_description: 如何在 C# 中批量 OCR，可让您从图像中提取文本、将图像转换为文本，并在轻松设置 OCR 语言的同时将 OCR 保存为文本。
og_title: 如何在 C# 中批量 OCR – 快速指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中批量 OCR – 快速提取图像文字
url: /zh/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR – 快速从图像提取文本

是否曾经想过 **如何批量 OCR**，当你有数百张图片放在一个文件夹中时？ 你并不孤单——开发者经常询问如何在不为每个文件编写循环的情况下从图像中提取文本。 好消息是 Aspose.OCR 为你提供了一种简洁、支持并行的方式，只需几行 C# 代码即可 **将图像转换为文本**。

在本教程中，我们将逐步演示一个完整、可直接运行的示例，展示如何 **将 OCR 保存为文本**、选择正确的语言，并通过并行处理提升速度。 完成后，你将拥有一个可直接嵌入任何 .NET 项目的独立解决方案。

## 您需要的条件

- .NET 6 或更高版本（API 同时支持 .NET Core 和 .NET Framework）
- Aspose.OCR for .NET（NuGet 包 `Aspose.OCR`）
- 需要处理的图像文件夹（PNG、JPEG、TIFF 等）
- 对并行编程有一点好奇心（可选，但有帮助）

无需额外服务，无需云密钥——只需本地运行的纯 C# 代码。

---

![how to batch OCR workflow](placeholder.png){alt="批量 OCR 工作流图"}

## 步骤 1：设置项目并安装 Aspose.OCR

首先，创建一个控制台应用（或复用已有项目），并添加 Aspose.OCR 包：

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **专业提示：** 如果你使用 Visual Studio，右键单击项目 → *管理 NuGet 包* → 搜索 *Aspose.OCR* 并安装最新的稳定版本。

这样你就可以使用 `OcrBatchProcessor`、`OcrEngineSettings` 以及枚举 `Language`。

## 步骤 2：定义输入和输出文件夹

批处理器需要知道源图像所在位置以及提取的文本文件应写入的目标位置。 将路径设为绝对或相对于项目根目录——只要在运行代码前确保这些文件夹已存在即可。

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

> **为什么重要：** 如果输出文件夹不存在，处理器会抛出异常，导致整个批次中断。提前创建文件夹可保证顺利执行。

## 步骤 3：配置 OCR 设置（包括语言）

这里是为整个批次 **设置 OCR 语言** 的地方。 Aspose.OCR 支持数十种语言；默认是英文，但你可以通过更改 `Language` 枚举值切换到法语、西班牙语等。

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

如果以后需要针对每张图像使用不同语言，可以在后续为单个文件覆盖此设置——稍后会详细说明。

## 步骤 4：构建 `OcrBatchProcessor` 对象

现在把所有内容串联起来。 `OcrBatchProcessor` 允许你指定输入文件夹、输出文件夹、输出格式、并行选项以及我们刚才创建的共享设置。

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

> **为什么使用并行？** 当处理数十或数百张图像时，逐个处理会非常慢。 将 `MaxDegreeOfParallelism` 设置为 4 可让运行时同时使用四个 CPU 核心，显著缩短在普通工作站上的总耗时。

## 步骤 5：运行批处理操作

配置好处理器后，只需一次方法调用即可执行。 库会自动处理文件枚举、OCR 以及结果写入。

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

当控制台打印 *“Batch OCR completed.”* 时，你会在 `BatchResults` 文件夹中找到每个原始图像旁边的 `.txt` 文件。 每个文本文件都包含从对应图像中提取的原始字符——这正是 **从图像中提取文本** 进行后续处理所需的内容。

### 预期输出

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

打开任意一个文件，你会看到图像内容的纯文本表示。

## 步骤 6：验证结果（可选）

养成检查少量文件以确保 OCR 正常工作的习惯是个好主意。 一个快速方法是读取每个生成文件的第一行并打印到控制台：

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

如果发现字符乱码，考虑切换 `Language` 设置或调整图像质量（例如，提高 DPI、转换为灰度）。

## 高级变体与边缘情况

### 1. 按文件语言覆盖
有时批次中会包含多语言文档。 你可以在运行时检查每张图像的文件名并动态分配语言：

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. 不同的输出格式
如果需要可搜索的 PDF 而不是纯文本，修改 `OutputFormat`：

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

这将 **将图像转换为文本** 并嵌入 PDF 容器中，保留原始布局。

### 3. 处理大尺寸图像
超高分辨率图像可能会占用大量内存。 为了保持轻量化，可启用图像下采样：

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. 错误日志记录
处理器会对无法读取的文件抛出异常。 将 `Execute` 包裹在 try/catch 中并记录有问题的文件名：

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## 完整可运行示例

将所有内容组合在一起，下面是完整的、可直接复制粘贴的程序：

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

将其保存为 `Program.cs`，构建项目，然后运行 `dotnet run`。 你将看到控制台输出确认完成，并随后预览提取的文本片段。

---

## 结论

我们刚刚介绍了使用 Aspose.OCR 在 C# 中 **批量 OCR** 的方法，展示了如何 **从图像中提取文本**、**将图像转换为文本**、以及 **将 OCR 保存为文本**，同时 **设置 OCR 语言** 以匹配你的内容。 示例功能完整，包含并行处理以提升速度，并提供了按文件语言覆盖或 PDF 输出等高级场景的扩展点。

准备好下一步了吗？尝试将 `OcrOutputFormat.PlainText` 替换为 `SearchablePdf`，感受生成可搜索 PDF 的简便。 或者实验不同的 `MaxDegreeOfParallelism` 值，在多核机器上挤出每一毫秒的性能。

如果遇到问题，请再次检查文件夹路径、确保图像可读，并确认语言枚举与图片中的文字相匹配。 祝编码愉快，愿你的 OCR 批处理快速且精准！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}