---
category: general
date: 2026-03-17
description: 如何在 C# 中快速批量 OCR PNG 图像。学习提取 PNG 文件中的文本，将 PNG 转换为文本，并使用简易脚本从目录读取图像。
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: zh
og_description: 如何使用 C# 批量 OCR PNG 图像，提供逐步代码。提取 PNG 文件中的文本，将 PNG 转换为文本，并轻松读取目录中的图像。
og_title: 如何在 C# 中批量对 PNG 图像进行 OCR – 完整指南
tags:
- OCR
- C#
- Image Processing
title: 如何在 C# 中批量 OCR PNG 图像 – 完整指南
url: /zh/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

blocks/products/products-backtop-button >}}

We must ensure all shortcodes remain.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR PNG 图像 – 完整指南

有没有想过 **如何批量 OCR** 一个充满截图的文件夹，而无需手动打开每个文件？你并不是唯一的——开发者经常询问如何批量 OCR 大量 PNG，尤其是当目标是提取文本 PNG 文件用于后续分析时。

在本教程中，我们将逐步演示一个可直接运行的 C# 示例，它 **提取文本 PNG** 文件，**将 PNG 转换为文本**，并展示最佳的 **从目录读取图像** 方法。完成后，你将拥有一个脚本，能够在每个图像旁生成对应的 `.txt` 文件，为你节省数小时的手动复制粘贴工作。

## 你将实现的目标

- 初始化一次 OCR 引擎并在整个批处理中复用它。  
- 在指定文件夹中扫描每个 `*.png`，无需自行编写循环。  
- 将每个 OCR 结果写入各自的文本文件，保留原始文件名。  
- 优雅地处理常见边缘情况，如空文件夹或非图像文件。

### 前提条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）。  
- 一个提供 `OcrEngine`、`ImageStream` 和 `OcrResult` 类型的 OCR 库（例如本文片段中使用的虚构 **FastOCR** SDK）。  
- 基础的 C# 知识——无需高级模式。

---

## 批量 OCR PNG 图像 – 概览

下面是 **完整、可运行的程序**。请随意将其复制粘贴到新的控制台项目中，替换占位路径，然后按 **F5**。

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **预期输出：** 对于每个 `image01.png`，你会在同目录下找到一个包含识别字符的 `image01.txt`。控制台会在写入每个文件时列出文件名。

![批量 OCR 示意图](how-to-batch-ocr-diagram.png "使用 C# 批量 OCR PNG 图像的示意图")

---

## 步骤详解

### 1. 初始化 OCR 引擎 – 过程核心  

`var ocrEngine = new OcrEngine();` 创建了一个将在整个批处理中复用的引擎实例。复用引擎 **至关重要**，因为大多数 OCR 库在构造时会分配大量资源（如语言模型）。一次性初始化可显著提升性能——尤其是当你拥有数十或数百个 PNG 时。

> **专业提示：** 如果需要除英文之外的语言，请设置 `ocrEngine.Config.Language = Language.Spanish;`（或任何受支持的枚举）。

### 2. 从目录读取图像 – 定位每个 PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` 正好实现了二级关键词 *read images from directory* 所承诺的功能。它返回绝对路径数组，随后我们将这些路径传递给 OCR 引擎。

> **为什么不使用 `SearchOption.AllDirectories`？** 如果你的图像位于子目录中，可以改为 `GetFiles(path, "*.png", SearchOption.AllDirectories)`。只需记住，更深的扫描可能会带来不需要的文件，请相应地进行过滤。

### 3. 将文件路径转换为 ImageStream 对象  

大多数 OCR SDK 期望的是流而非原始路径。LINQ 表达式 `Select(path => ImageStream.FromFile(path)).ToList()` 构建了一个 **流列表**，批量识别器可以一次性消费。此步骤还确保文件句柄仅打开一次，降低 I/O 开销。

> **边缘情况：** 如果文件损坏，`ImageStream.FromFile` 可能抛出异常。若需要更高的鲁棒性，请将转换包装在 `try/catch` 中。

### 4. 批量识别文本  

`ocrEngine.RecognizeBatch(imageStreams)` 正是 *how to batch OCR* 的最佳实现。我们不再对每张图像单独循环调用单图像方法，而是一次性将整个集合交给引擎。库内部可能会并行处理，从而在多核机器上获得显著加速。

> **提示：** 如果你的 OCR 库没有提供批量方法，也可以通过在单图像 `Recognize` 调用外使用 `Parallel.ForEach` 来获得类似的性能。

### 5. 写入每个 OCR 结果 – 将 PNG 转换为文本  

最后的 `for` 循环将 `ocrResults[i].Text` 写入一个与原始 PNG 同名的 `.txt` 文件。这正是二级关键词 *convert PNG to text* 所描述的行为。`Path.Combine` 调用确保输出文件夹已存在，并防止路径遍历漏洞。

> **常见陷阱：** 若忘记先创建输出目录，会导致 `DirectoryNotFoundException`。使用 `Directory.CreateDirectory(outputFolder);` 可预先解决此问题。

---

## 处理真实场景的变体

| 场景 | 需要更改的内容 | 原因 |
|-----------|----------------|-----|
| **空输入文件夹** | 保留早期的 `if (imagePaths.Length == 0)` 检查 | 防止不必要的 OCR 调用并提供友好提示 |
| **混合文件类型** | 使用 `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | 确保只处理 PNG，满足 *extract text png* 而不会出错 |
| **超大图像（> 5 MB）** | 在送入 OCR 前进行下采样：`ImageStream.FromFile(path).Resize(1920, 1080)`（如果 API 支持） | 减少内存压力，通常还能提升识别准确度 |
| **不同的 OCR 语言** | 设置 `ocrEngine.Config.Language = Language.French;` | 使引擎与源图像的语言保持一致 |

## 常见问题 (FAQ)

**Q: 这能用于 JPEG 或 TIFF 文件吗？**  
A: 核心逻辑保持不变，只需将搜索模式改为 `"*.jpg"` 或 `"*.tif"`，并确保 OCR 库能够解码这些格式。

**Q: 如何在处理成千上万张图像时避免内存耗尽？**  
A: 将批量调用替换为流式处理——一次处理大约 50 张图像的块，处理完后释放流再加载下一块。

**Q: 我需要 OCR 的置信度分数。在哪里可以找到？**  
A: 大多数 `OcrResult` 对象都公开 `Confidence` 属性。你可以扩展写出步骤：

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## 总结

我们已经完整演示了 **如何在 C# 中批量 OCR** PNG 图像的全流程。通过初始化单一引擎、从目录读取图像、将路径转换为流、批量识别文本，最后将每个结果写入对应的文本文件，你现在拥有了一套稳健、可投入生产的模式，能够应对 **extract text PNG**、**convert PNG to text** 与 **read images from directory** 等任务。

接下来可以尝试更换 OCR 提供商、加入多线程后处理（例如拼写检查），或将生成的 `.txt` 文件导入搜索索引。掌握批量工作流后，可能性无限。

有新的思路想分享吗？留下评论吧，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}