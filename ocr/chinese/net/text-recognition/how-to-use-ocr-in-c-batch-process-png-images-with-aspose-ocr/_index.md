---
category: general
date: 2026-02-14
description: 如何在 C# 中使用 OCR 快速提取 PNG 文件中的文本。学习批量 OCR 图像、处理多张图像，并在一篇指南中使用 Aspose OCR
  C#。
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: zh
og_description: 如何在 C# 中使用 Aspose OCR C# 进行 OCR。本教程展示了如何提取 PNG 文件中的文本、批量 OCR 图像以及高效处理多张图像。
og_title: 如何在 C# 中使用 OCR – 批量 PNG 文本提取
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中使用 OCR – 使用 Aspose OCR 批量处理 PNG 图像
url: /zh/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 使用 Aspose OCR 批量处理 PNG 图像

是否曾想过 **如何使用 OCR** 从一堆 PNG 文件中提取文本，而不必为每个文件单独编写例程？你并不孤单。许多开发者在需要 **提取 PNG 文本** 时会遇到瓶颈，尤其是当图像位于同一个文件夹中，需要为每个文件启动 OCR 引擎时。

在本指南中，我们将演示一个完整、可直接运行的解决方案，能够 **批量 OCR 图像**、**并行处理多张图像**，并利用强大的 **Aspose OCR C#** 库。完成后，你将拥有一个可执行文件，能够读取任意数量的 PNG，提取其中的文本，并将结果打印到控制台——只需几行代码。

## 前置条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）  
- 有效的 Aspose.OCR for .NET 许可证（或免费试用版）——可从 Aspose 官网获取。  
- 包含待读取 PNG 文件的文件夹。  
- Visual Studio 2022（或任何支持 C# 的 IDE）。  

除 `Aspose.OCR` 之外，无需额外的 NuGet 包。

## 第一步：如何使用 OCR – 初始化 Aspose OCR 引擎

首先需要创建 `Engine` 类的实例。该对象抽象了底层 OCR 技术，可根据硬件和许可证在 CPU 或 GPU 上运行。

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*为什么重要：* 只初始化一次引擎并在多个线程间复用，可节省内存并避免重复加载 OCR 模型的开销。同时还能保证所有图像使用统一的设置。

## 第二步：提取 PNG 文本 – 收集图像路径

接下来，需要获取文件路径集合。实际项目中你可能会动态读取目录，但为保持示例简洁，这里手动列出几个文件。

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*提示：* 将 `YOUR_DIRECTORY` 替换为图像所在的绝对或相对路径。如果文件数量很多，可以用 `Directory.GetFiles("YOUR_DIRECTORY", "*.png")` 替代手动列表。

## 第三步：批量 OCR 图像 – 并行运行识别

逐个处理图像虽简单但速度慢。使用 `Parallel.ForEach` 可以 **并行处理多张图像**，充分利用多核 CPU。

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*为什么使用并行？* 每次 OCR 调用都是 CPU 密集型且相互独立， 并发执行可以显著缩短总运行时间，尤其在 4 核或更高的机器上。

## 第四步：处理多张图像 – 显示提取的文本

现在我们已经得到一组 `OcrResult` 对象，可以遍历它们并打印识别出的文本。通常你会将结果写入数据库或文件，但这里使用控制台输出以保持示例简洁。

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**预期的控制台输出（示例）：**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

如果某张图像加载失败，Aspose 会抛出异常；你可以在 `engine.Recognize` 调用外层加入 try/catch，以记录错误而不中止整个批处理。

## 第五步：完整工作示例 – 所有代码汇总

下面是可以直接复制到新的 C# 控制台项目中的完整程序。它包含了从 `using` 语句到最终输出循环的全部内容。

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### 运行示例

1. 在 Visual Studio 中创建一个新的 **Console App** 项目。  
2. 添加 **Aspose.OCR** NuGet 包（`Install-Package Aspose.OCR`）。  
3. 将 `YOUR_DIRECTORY` 替换为存放 PNG 文件的路径。  
4. 构建并运行——你应该能在控制台看到提取的文本。

## 专业技巧与边缘情况

- **GPU 加速：** 如果拥有兼容的 GPU 并且已获取 Aspose OCR 授权，可在创建引擎前通过 `EngineSettings` 启用 GPU 加速，这能为每张图像节省数秒。  
- **大文件处理：** 对于大于 10 MB 的图像，建议先进行下采样，以降低内存压力。  
- **语言支持：** 默认引擎假设文本为英文。可通过 `engine.Language = Language.French;`（或其他受支持语言）来提升非英文文本的识别准确率。  
- **错误处理：** 并行循环内部的 `try/catch` 确保单个损坏文件不会导致整个批处理终止。你也可以将失败记录写入文件，以便后续检查。  
- **结果存储：** 若不想打印，可使用 `File.WriteAllText(Path.ChangeExtension(path, ".txt"), result.Text)` 将 `result.Text` 写入对应的 `.txt` 文件。

## 结论

现在你已经掌握了 **如何在 C# 中使用 OCR** 来 **提取 PNG 文本**、**批量 OCR 图像**，以及 **高效并行处理多张图像** 的完整方案。该解决方案自包含、支持并行执行，并且可以轻松扩展以处理数百甚至数千个文件，只需做最小的改动。

准备好下一步了吗？尝试将控制台输出改为 CSV 报表，实验 GPU 加速，或将 OCR 文本导入搜索索引。可能性无限，而“初始化一次、并行运行、优雅处理错误”的核心模式将在任何图像处理流水线中为你提供坚实基础。

祝编码愉快，愿你的 OCR 任务快速且无错误！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}