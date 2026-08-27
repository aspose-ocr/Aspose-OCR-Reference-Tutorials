---
category: general
date: 2026-01-02
description: 使用 Aspose OCR 和 GPU 支持快速对 PNG 进行 OCR。了解如何从图像中识别文本、提取文本以及设置 GPU 内存限制。
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: zh
og_description: 通过利用 Aspose OCR 和 GPU 加速，高效地对 PNG 进行 OCR。本教程展示了如何从图像中识别文本、提取文本以及控制
  GPU 内存使用。
og_title: 在 PNG 上使用 GPU 运行 OCR – 完整 C# 指南
tags:
- OCR
- C#
- GPU
title: 在 PNG 上使用 GPU 运行 OCR – 完整 C# 指南
url: /zh/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 GPU 对 PNG 进行 OCR – 完整 C# 指南

是否曾经需要 **run OCR on PNG** 文件，却在性能上卡住了？你并不是唯一的遇到这种情况的人。在许多真实的流水线中，单个高分辨率 PNG 会拖慢仅使用 CPU 的 OCR 引擎，使本该快速的查询变成需要数分钟的等待。  

好消息是，Aspose OCR 附带了 GPU 扩展，使您能够在极短的时间内 **recognize text from image** 文件。在本教程中，我们将通过一个实战示例，向您展示如何使用 C# **run OCR on PNG**，如何 **extract text from image**，以及如何 **set GPU memory limit**，以便在硬件预算范围内运行。  

我们还会讲解每一步背后的“如何”和“为什么”，让您获得扎实的概念模型，而不仅仅是复制粘贴的代码片段。

## 您将学习

- 使用 Aspose OCR GPU 支持的前置条件。  
- 如何将 PNG 加载到 `Bitmap` 并传递给 OCR 引擎。  
- 如何配置 `GpuDevice` 和 `GpuMemoryLimitMb` 以获得最佳性能。  
- 如何 **recognize text from image** 并获取纯文本结果。  
- 处理常见边缘情况的技巧，例如低内存 GPU 或多页 PNG。  

通过本指南，您将能够以 GPU 速度 **run OCR on PNG** 文件，并自信地控制 OCR 作业的内存占用。  

![展示使用 GPU 加速运行 OCR 的 PNG 示例图](run-ocr-on-png-diagram.png "run OCR on PNG 示例")

## 前置条件

在深入之前，请确保您已经具备以下条件：

1. .NET 6.0 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）。  
2. 支持 CUDA 的 NVIDIA GPU（示例使用设备索引 0）。  
3. Aspose.OCR NuGet 包及其 GPU 扩展 (`Aspose.OCR.Extensions`)。  
4. 一个示例 PNG (`input.png`)，放置在项目可引用的文件夹中。  

如果上述内容有任何不熟悉的，请不要担心——我们将在适当的地方提供替代方案。

---

## 第一步 – 安装 Aspose OCR 和 GPU 扩展

首先，先把基础工作做好。没有正确的库，其余代码将无法编译。

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

`Aspose.OCR.Extensions` 包会引入 GPU 加速所需的本机 CUDA 二进制文件。  
*技巧提示:* 如果您使用的机器没有 GPU，仍然可以编译项目；只需在后面将 `PreferGpu = false` 即可。

---

## 第二步 – 加载要处理的 PNG

现在我们通过将 PNG 加载到 `Bitmap` 来实际 **run OCR on PNG**。此步骤很直接，但值得提醒一下：`Bitmap` 需要文件路径，请确保相对于可执行文件的路径正确。

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

如果 PNG 异常大（例如，任一边 > 5000 像素），您可能需要先将其缩小，以免耗尽 GPU 内存。这时 **set GPU memory limit** 选项就非常有用了。

---

## 第三步 – 创建并配置用于 GPU 的 OCR 引擎

这就是本教程的核心：使用 GPU 配置 OCR 引擎以 **recognize text from image**。两个属性是关键：

- `GpuDevice` – 选择使用哪个 CUDA 设备。  
- `GpuMemoryLimitMb` – 限制引擎可分配的 GPU 内存量。

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**为什么要设置内存限制？** 某些 GPU 与显示器共享内存或同时运行多个工作负载。通过限制分配，可以防止内存不足导致的崩溃，尤其是在并行处理大量 PNG 时。

---

## 第四步 – 定义识别选项（语言 & GPU 偏好）

`RecognitionOptions` 对象告诉引擎要识别的语言以及是否即使在小图像上也 **prefer GPU**。对于大多数英文文档，这已经足够，但您可以将 `Language.English` 替换为其他受支持的语言。

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

如果您需要在非英文语言中 **extract text from image**，只需更改 `Language` 枚举。该库开箱即支持数十种语言。

---

## 第五步 – 运行 OCR 并获取结果

所有配置完成后，最后只需一行代码即可实际 **run OCR on PNG** 并返回丰富的结果对象。

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

`OcrResult` 不仅包含纯文本 (`ocrResult.Text`)，还包括置信度分数、边界框，甚至带有高亮单词的原始图像——如果需要调试或可视化提取过程，这非常有用。  

**预期输出**（针对显示 “Hello World” 的示例 PNG）：

```
=== OCR Output ===
Hello World
```

如果文本出现乱码，请再次确认 PNG 未损坏且 GPU 内存限制对图像大小而言不太低。

---

## 第六步 – 处理边缘情况和最佳实践提示

### 低内存 GPU

如果出现类似 `CudaException: out of memory` 的异常，请降低 `GpuMemoryLimitMb` 或在处理前将 PNG 切分为多个瓦片。瓦片化可以使用 `Graphics.DrawImage` 在 `Bitmap` 克隆上完成。

### 批量处理多个 PNG

在处理 PNG 文件夹时，复用同一个 `OcrEngine` 实例——只初始化一次可节省 GPU 上下文切换。

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### 回退到 CPU

如果没有可用的 GPU，只需将 `PreferGpu = false`。引擎会自动回退到 CPU，无需更改代码。

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## 完整可运行示例

下面是完整的程序代码，您可以复制粘贴到新的控制台项目中。它包含上述所有步骤，并加入了一些安全检查。

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

将文件保存为 `Program.cs`，运行 `dotnet run`，您应该会在控制台看到提取的文本。

---

## 结论

我们已经演示了如何使用 Aspose OCR 的 GPU 扩展 **run OCR on PNG** 文件，如何 **recognize text from image**，以及如何在控制 **set GPU memory limit** 的同时 **extract text from image**。通过配置 `GpuDevice` 和 `GpuMemoryLimitMb`，即使在普通 GPU 上也能保持应用的快速与稳定。  

接下来您可以：

- 尝试其他语言（`Language.French`、`Language.Spanish`）。  
- 将 OCR 步骤集成到更大的文档处理流水线中。  
- 添加后处理，例如拼写检查或实体抽取，以完善原始文本。  

请记住，关键不仅在于代码本身，更在于理解每个设置背后的原因。当您了解如何 **set GPU memory limit** 以及何时回退到 CPU 时，便能构建出可优雅扩展的 OCR 解决方案。  

如果您对特定 PNG 大小、多页 TIFF 或 GPU 错误排查有疑问，请在下方留言，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}