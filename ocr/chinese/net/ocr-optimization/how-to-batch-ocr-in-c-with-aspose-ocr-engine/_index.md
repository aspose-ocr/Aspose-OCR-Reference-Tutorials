---
category: general
date: 2026-01-01
description: 如何在 C# 中使用 Aspose OCR 引擎进行批量 OCR。学习如何从图像识别文本以及使用 GPU 加速从 TIFF 文件提取文本。
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from TIFF
language: zh
og_description: 如何在 C# 中使用 Aspose OCR 引擎批量进行 OCR。本指南展示了如何高效地从图像识别文本并从 TIFF 文件中提取文本。
og_title: 如何在 C# 中批量 OCR – 完整的 Aspose 指南
tags:
- OCR
- C#
- Aspose
- GPU
title: 如何在 C# 中使用 Aspose OCR 引擎批量进行 OCR
url: /zh/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose OCR 引擎进行批量 OCR

有没有想过 **如何批量 OCR**，当你有几十个扫描文档放在一个文件夹中时？你并不孤单——许多开发者在从单张图像识别转向处理整个集合时都会遇到这个难题。好消息是，Aspose OCR 让这变得轻而易举，无论你是运行在 CPU 上还是利用 GPU 加速。

在本教程中，我们将逐步演示一个完整、可运行的示例，**从图像中识别文本**，甚至 **批量提取 TIFF 文件中的文本**。没有模糊的 “参考文档” 快捷方式——只有一个可以直接复制粘贴并立即运行的自包含解决方案。

## 前置条件

在开始之前，请确保你具备以下条件：

* 已安装 .NET 6.0 或更高版本（代码目标为 .NET 6，.NET 5 也可运行）。
* Aspose.OCR for .NET NuGet 包（提供 CPU 与 GPU 版本；请安装与你的硬件匹配的版本）。
* 一个包含若干 TIFF 或 PNG 示例文件的文件夹，供你处理。
* Visual Studio 2022 或任意你喜欢的 IDE。

> **专业提示：** 如果计划使用 GPU 版，请确认显卡驱动已是最新，并已安装 CUDA 11+。如果找不到兼容的 GPU，引擎会自动回退到 CPU。

## Step 1 – Set Up the Project and Install Aspose.OCR

### H2: 创建一个新的控制台应用并添加 Aspose.OCR

打开终端（或 Visual Studio 中的 Package Manager Console），运行：

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

如果你拥有 GPU 授权许可证，请改为添加 GPU 包：

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

就这样——你的项目现在已经引用了我们将用于 **批量 OCR** 的 OCR 库。

## Step 2 – Initialize the OCR Engine (CPU or GPU)

### H2: 批量 OCR – 引擎初始化

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**为什么重要：** 通过切换 `UseGpu`，让 Aspose 决定最快的路径。如果 GPU 不可用，引擎会静默切换回 CPU，确保批处理作业不会因硬件缺失而崩溃。

## Step 3 – Gather the Files You Want to Process

### H2: 从图像中识别文本 – 构建文件列表

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**边缘情况说明：** 如果文件格式混杂，请将搜索模式改为 `"*.*"`，并在循环内部按扩展名过滤。这样可以保持批处理的灵活性。

## Step 4 – Process Each Image and Show a Preview

### H2: 从 TIFF 中提取文本 – 循环遍历文件

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**你将看到的结果：** 对每个 TIFF，控制台会打印类似下面的内容：

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```

该预览确认批处理已成功完成，而无需手动打开每个文件。

## Step 5 – Save Results (Optional but Handy)

### H3: 将 OCR 输出持久化为文本文件

如果需要完整的文本进行后续处理，请在 `foreach` 循环内部加入以下代码：

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

现在每个 TIFF 都会生成一个对应的 `.txt` 文件，里面包含完整的 OCR 输出——非常适合索引、搜索或喂入语言模型。

## Step 6 – Run the Demo and Verify

1. 构建项目：`dotnet build`。
2. 执行：`dotnet run --project GpuBatchDemo.csproj`。

你应该会在控制台看到预览行的输出，并且（如果添加了可选步骤）在源图像旁边生成一系列 `.txt` 文件。

### H3: 常见问题及解决方案

| 症状 | 可能原因 | 解决办法 |
|------|----------|----------|
| **`ocrResult.Text` 为空** | 图像过暗或 DPI 过低 | 预处理图像（提升对比度、放大）或设置 `ocrEngine.Settings.PreprocessImage = true`。 |
| **GPU 错误 “CUDA driver version is insufficient”** | 驱动过旧 | 更新 GPU 驱动，或将 `UseGpu = false` 强制使用 CPU。 |
| **异常 “File not found”** | Linux/macOS 上路径分隔符错误 | 使用 `Path.Combine` 或正斜杠 (`/`)。 |

## Step 7 – Scaling Up (Beyond a Few Files)

当你从少量 TIFF 扩展到成千上万时，请考虑：

* **并行处理：** 将 `foreach` 包装在 `Parallel.ForEach` 中（确保引擎实例是线程安全的；否则为每个线程创建独立实例）。
* **分块 I/O：** 分批读取图像，防止内存耗尽。
* **日志记录：** 将进度写入日志文件，便于崩溃后恢复。

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **记住：** GPU 内存是共享的，启动过多并行 GPU 任务反而会拖慢速度。建议先用少量线程进行测试。

## Full Working Example (Copy‑Paste Ready)

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

运行此程序将 **从图像中识别文本**、**从 TIFF 中提取文本**，并演示 **如何高效批量 OCR**。

---

## 结论

现在你已经拥有一个完整、端到端的 **批量 OCR** 示例，使用 C# 与 Aspose 的 OCR 引擎实现。教程涵盖了从项目搭建、GPU 加速切换、文件列表构建、逐图像处理到结果持久化的全部步骤。无论是提取 TIFF 文件的文本还是其他图像格式，只需更换文件扩展名即可复用同一模式。

准备好下一步了吗？尝试将 OCR 输出集成到搜索索引中、喂入大语言模型，或通过并行处理进一步缩短大批量任务的耗时。天地无限，而你已经拥有了坚实的基础。

有任何问题或想分享自己的批量 OCR 技巧？在下方留言吧——祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}