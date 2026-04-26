---
category: general
date: 2026-04-26
description: 如何快速批量 OCR PNG 图像。学习从 PNG 中提取文本、将图像转换为文本、写入识别的文本，并使用 Aspose OCR 读取 PNG
  目录。
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: zh
og_description: 如何使用 Aspose OCR 在 C# 中批量 OCR PNG 图像。本指南展示了如何从 PNG 中提取文本，将图像转换为文本，并高效地写入识别的文本。
og_title: 如何在 C# 中批量 OCR PNG 图像 – 步骤详解
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中批量 OCR PNG 图像 – 完整指南
url: /zh/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR PNG 图像 – 完整指南

是否曾经想过 **如何批量 OCR** 整个 PNG 文件夹，而无需为每张图片编写单独的程序？你并不是唯一需要处理数十张截图、扫描收据或图形并将其转换为可搜索文本的人。在本教程中，我们将演示一个动手实用的解决方案，**从 PNG 中提取文本**、**将图像转换为文本**，并 **将识别的文本写入单独的文件**——所有这些都自动读取 PNG 目录。

阅读完本指南后，你将拥有一个可直接运行的 C# 控制台应用程序，一次性处理任意数量的图像。无需额外脚本，无需手动复制粘贴——只有纯代码为你完成繁重的工作。

## 你需要的环境

- **.NET 6.0** 或更高（代码在 .NET Framework 上同样可运行）。
- **Aspose.OCR for .NET** NuGet 包（免费试用可用于测试）。
- 一个包含若干 *.png* 文件的文件夹，用于 OCR。
- Visual Studio 2022 或任何你喜欢的 C# IDE。

如果你已经准备好这些，就可以直接进入实现步骤。

## 步骤 1 – 准备输入和输出文件夹 *(读取 PNG 目录)*

首先，我们让程序指向包含图像的文件夹，并决定生成的 *.txt* 文件存放位置。使用 `Directory.GetFiles` 可以得到目录中所有 PNG 文件的干净可枚举集合。

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**这有什么意义：**
- 使用通配符 (`*.png`) 可确保仅处理图像文件，忽略其他杂散文档。
- 动态创建输出文件夹可防止后续出现 `DirectoryNotFoundException`。

> **技巧提示：** 如果需要支持其他格式（JPEG、BMP），只需扩展搜索模式或使用 `Directory.EnumerateFiles` 并传入多个扩展名。

## 步骤 2 – 初始化 OCR 引擎 *(将图像转换为文本)*

Aspose.OCR 提供两种引擎类型：基于 CPU 的 `OcrEngine` 和 GPU 加速的 `GpuOcrEngine`。对于大多数批处理任务，CPU 引擎已经足够，但如果你拥有合适的 GPU，可以更换为相应的类名。

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**这有什么意义：**
- 指定语言可显著提升准确率，因为引擎会预期相应的字符集。
- 在大批量处理出现性能瓶颈时，只需一行代码即可切换到 `GpuOcrEngine`。

## 步骤 3 – 创建批量识别器

Aspose 提供了便利的 `BatchRecognizer`，它接受文件路径的可枚举集合，并逐个流式返回结果。这避免了一次性将所有图像加载到内存中——对于大型文件夹来说至关重要。

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**这有什么意义：**
- 批量识别器封装了循环逻辑，让我们专注于如何处理每个结果，而不是如何安全地遍历。

## 步骤 4 – 对所有图像执行 OCR 并写入输出 *(写入识别文本)*

现在我们实际执行 OCR。`Recognize` 方法返回一个 `IEnumerable<RecognitionResult>`，其中每个结果包含提取的文本以及其他元数据。

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**这有什么意义：**
- 使用 `File.WriteAllText` 可确保默认以 UTF‑8 编码保存文本，保留特殊字符。
- 递增命名（`out_0.txt`、`out_1.txt`）与处理顺序保持一致，便于调试。

> **边缘情况：** 如果某张图像 OCR 失败（例如文件损坏），`RecognitionResult.Text` 将为空。你可以在循环内部添加简单检查来记录失败情况：

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## 步骤 5 – 整合全部代码 – 完整可运行示例

下面是完整的程序代码，你可以直接复制粘贴到新的控制台项目中。它包含 `using` 指令、文件夹验证以及一个简易的控制台 UI，帮助你了解批处理何时完成。

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**预期输出：**
运行程序时会打印类似以下内容：

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

你将在输出文件夹中看到 `out_0.txt` … `out_11.txt`，每个文件都包含对应图像的纯文本版本。

## 常见问题与技巧

| 问题 | 答案 |
|----------|--------|
| *Can I OCR sub‑folders as well?* | 是——将 `Directory.GetFiles` 替换为 `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`。 |
| *What if I need a different language?* | 设置 `ocrEngine.Language = Language.Spanish;`（或任意受支持的枚举）。 |
| *How do I handle huge batches (thousands of files)?* | 考虑分块处理或使用 `Parallel.ForEach` 并限制并行度，以避免耗尽内存。 |
| *Is the output always UTF‑8?* | `File.WriteAllText` 默认使用无 BOM 的 UTF‑8 编码，这对大多数拉丁语系语言有效。对于亚洲文字可能需要显式设置 `Encoding.UTF8`。 |
| *Can I get confidence scores?* | `RecognitionResult` 提供 `Confidence`——你可以将其与文本一起记录以进行质量控制。 |

## 可视化概览 *(批量 OCR 流程图)*

![批量 OCR 工作流图，展示输入文件夹 → OCR 引擎 → 批量识别器 → 输出 txt 文件](https://example.com/diagram-how-to-batch-ocr.png "批量 OCR")

*alt 文本包含主要关键词，满足 SEO 图片要求。*

## 总结

我们刚刚介绍了使用 Aspose.OCR 对 PNG 文件目录进行 **批量 OCR** 的完整流程，从读取 PNG 目录到写入每个识别文本文件。该方案完全独立，可在任何现代 .NET 运行时上运行，并且可以扩展为 GPU 加速、多语言支持或并行处理。

准备好下一步了吗？尝试将 `Language.Latin` 替换为其他语言，或将输出集成到搜索索引中，使文档即时可搜索。一旦掌握了批量 OCR，想象空间无限。

祝编码愉快，如有任何问题请在评论中告诉我！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}