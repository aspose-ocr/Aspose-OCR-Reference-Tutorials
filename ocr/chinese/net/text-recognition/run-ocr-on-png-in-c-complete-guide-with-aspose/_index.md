---
category: general
date: 2026-02-16
description: 使用 Aspose OCR 在 C# 中快速对 PNG 进行 OCR。了解如何提取文本、读取 PNG 文本以及识别 PNG 文本，配有一步步教程。
draft: false
keywords:
- run OCR on PNG
- how to extract text
- read text png
- recognize text png
- ocr tutorial c#
language: zh
og_description: 使用 Aspose OCR 在 C# 中对 PNG 进行 OCR。本教程将逐步演示如何提取文本、读取 PNG 文本以及识别 PNG
  文本。
og_title: 在 C# 中对 PNG 进行 OCR – 完整指南
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 在 C# 中对 PNG 进行 OCR – Aspose 完整指南
url: /zh/net/text-recognition/run-ocr-on-png-in-c-complete-guide-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中对 PNG 进行 OCR – Aspose 完整指南

是否曾经需要 **在 PNG 上运行 OCR**，但不确定从何入手？你并不孤单——开发者经常询问 *如何提取文本*，无论是高分辨率的截图、收据还是扫描图表。在本教程中，我们将一步步演示一个实用的端到端解决方案，使用 Aspose.OCR 库在纯 C# 中 **在 PNG 上运行 OCR**。

我们将覆盖从安装 NuGet 包、启用 GPU 加速、加载英文语言模型，到最终将识别的字符串打印到控制台的全部内容。完成后，你将准确了解如何 **提取文本**（how to extract text）从任何 PNG，如何高效 **读取文本 PNG**（read text PNG），并拥有一个可复用的 **OCR 教程 C#** 代码片段，可直接嵌入任何项目。

## 你将学到的内容

- 安装并配置 Aspose.OCR for .NET。
- 启用硬件加速以提升处理速度。
- 加载语言模型并将 PNG 图像输入引擎。
- 捕获并显示输出，处理常见的陷阱。
- 将示例扩展到其他语言或图像格式。

**先决条件：** .NET 6 或更高版本，Visual Studio 2022（或你喜欢的 IDE），以及如果需要可选加速的兼容 GPU。无需任何 OCR 经验。

---

## 在 PNG 上运行 OCR – 环境设置

在深入代码之前，让我们确保开发环境已准备就绪。此步骤至关重要；缺少包或运行时不匹配会导致整个教程无法进行。

1. **创建一个新的控制台项目**  
   ```bash
   dotnet new console -n OcrPngDemo
   cd OcrPngDemo
   ```

2. **添加 Aspose.OCR NuGet 包**  
   ```bash
   dotnet add package Aspose.OCR
   ```

3. **（可选）验证 GPU 支持** – 如果你拥有支持 CUDA/OpenCL 的 NVIDIA 或 AMD GPU，请安装相应的驱动程序。当你设置 `HardwareAcceleration.Gpu` 时，库会自动检测硬件。

就这样。一个包含 OCR 库的全新项目现在已经准备好 **在 PNG 上运行 OCR**。

## 如何提取文本 – 初始化 OCR 引擎

第一行实际代码创建了一个 `OcrEngine` 实例。可以把引擎看作操作背后的“大脑”；它保存配置、语言模型和硬件设置。

```csharp
using Aspose.OCR;

// Step 1: Initialize the OCR engine (default CPU mode)
OcrEngine ocrEngine = new OcrEngine();
```

为什么我们手动实例化而不是使用静态帮助器？  
因为这让我们能够完全控制 **如何提取文本**——可以随时切换 GPU、修改语言或动态更换图像来源。在更大的应用中，你可能会保留一个单例引擎，以避免重复加载模型。

## 使用 GPU 加速读取文本 PNG

如果你处理高分辨率截图，仅使用 CPU 的 OCR 可能会显得迟缓。启用 GPU 加速可以为每次运行节省数秒。

```csharp
// Step 2: Enable GPU acceleration for faster processing (requires compatible GPU)
ocrEngine.HardwareAcceleration = HardwareAcceleration.Gpu;
```

*专业提示：* 如果你的机器没有兼容的 GPU，上述代码行会优雅地回退到 CPU 模式。不会抛出异常，因此你可以在不同环境中保持代码不变。

## 加载语言模型 – “English” 示例

Aspose 默认随附英文模型，但你可以通过一次调用加载其他模型（法语、德语等）。加载模型是 **识别文本 PNG**（recognize text PNG）的前提；如果不加载，引擎将不知道应期待哪种字符集。

```csharp
// Step 3: Load the language model you need (English is included by default)
ocrEngine.LoadLanguage(LanguageModel.English);
```

如果你需要在其他语言中 **读取文本 PNG**，请将 `LanguageModel.English` 替换为相应的枚举值。

## 提供图像 – 从文件到流

现在我们将 PNG 文件交给引擎。`ImageStream.FromFile` 辅助方法将文件读取到内存中，支持多种格式，但我们关注的是 PNG。

```csharp
// Step 4: Provide the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/high_res_image.png");
```

确保路径指向真实的 PNG；否则会抛出 `FileNotFoundException`。快速测试时，可将打印的发票截图放入文件夹并在此引用。

## 识别文本 PNG – 执行 OCR 操作

在所有准备就绪后，实际的 OCR 调用只需一个方法。该方法返回一个字符串，包含所有提取的字符，并在可能的情况下保留换行。

```csharp
// Step 5: Run the OCR operation and capture the recognized text
string recognizedText = ocrEngine.Recognize();
```

为什么这一次调用就能工作？  
在幕后，引擎会执行一系列阶段：预处理（去噪、二值化）、分割（将图像拆分为行和字符），最后使用深度学习模型进行分类。所有这些繁重的步骤对你都是透明的，这也是 API 如此轻量的原因。

## 显示结果 – 验证输出

最后，我们将结果打印到控制台。在实际应用中，你可能会将其写入数据库、写入搜索索引，或传递给其他服务。

```csharp
// Step 6: Display the OCR result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

运行程序后，你应该会看到类似以下内容：

```
=== OCR Result ===
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

如果输出出现乱码，请再次检查图像质量（对比度、方向），并考虑启用 `ocrEngine.PreprocessOptions` 进行额外的微调。

## 完整 OCR 教程 C# – 可运行完整示例

下面是 **完整、可运行** 的代码，将所有部分组合在一起。复制粘贴到 `Program.cs`，替换图像路径，然后按 **F5**。

```csharp
using System;
using Aspose.OCR;

namespace OcrPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize the OCR engine (CPU by default)
            OcrEngine ocrEngine = new OcrEngine();

            // Enable GPU acceleration if a compatible GPU is present
            ocrEngine.HardwareAcceleration = HardwareAcceleration.Gpu;

            // Load the English language model (default)
            ocrEngine.LoadLanguage(LanguageModel.English);

            // Specify the PNG image to process
            string imagePath = "YOUR_DIRECTORY/high_res_image.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR and retrieve the recognized text
            string recognizedText = ocrEngine.Recognize();

            // Output the result to the console
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

**预期输出：** 控制台会打印 PNG 中找到的精确字符，并保留换行。如果图像仅包含数字，你会看到一串数字；如果包含混合语言，则会得到相应的 Unicode 字符。

> **注意：** 上述程序可适用于任何 PNG、JPEG 或 BMP，只要文件路径正确。要从流（例如来自 Web API） **读取文本 PNG**，请将 `ImageStream.FromFile` 替换为 `ImageStream.FromBytes(byteArray)`。

---

## 常见问题与边缘情况

### 如果我的 PNG 被旋转了怎么办？

Aspose.OCR 可以自动旋转图像。添加以下代码：

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath);
ocrEngine.ImageOrientation = ImageOrientation.AutoDetect;
```

### 如何处理大批量文件？

将引擎放在 `using` 块中，并在多个文件之间复用：

```csharp
using (var engine = new OcrEngine())
{
    engine.LoadLanguage(LanguageModel.English);
    foreach (var file in Directory.GetFiles(folder, "*.png"))
    {
        engine.Image = ImageStream.FromFile(file);
        string text = engine.Recognize();
        // Process text...
    }
}
```

### 能否从低对比度图像中提取文本？

启用预处理：

```csharp
ocrEngine.PreprocessOptions = PreprocessOptions.EnhanceContrast | PreprocessOptions.Denoise;
```

### 有办法获取置信度分数吗？

可以——`ocrEngine.RecognizeWithDetails()` 返回一个 `OcrResult` 对象集合，每个对象都包含 `Confidence` 属性。

## 可视化示例

<img src="https://example.com/ocr-output.png" alt="在 PNG 上运行 OCR 示例输出，显示提取的发票文本">

*Alt 文本包含主要关键词，满足 SEO 要求。*

## 结论

现在，你已经拥有一个可靠的 **在 PNG 上运行 OCR** 工作流，使用 Aspose.OCR 开箱即用。通过遵循本 **OCR 教程 C#**，你可以在几行代码内实现 **如何提取文本**、**读取文本 PNG** 和 **识别文本 PNG**。引擎的 GPU 支持、语言加载以及简洁的 API，使其成为任何需要将图像转换为可搜索文本的 .NET 开发者的首选方案。

接下来怎么办？尝试将 `LanguageModel.English` 替换为其他语言，使用 `PreprocessOptions` 处理噪声扫描，或将结果集成到全文搜索索引中。可能性无限，而你刚写的代码是所有这些探索的可复用基础。

如果遇到任何问题，请在下方留言或查阅 Aspose 文档获取更深入的配置选项。祝编码愉快，尽情将顽固的 PNG 转换为可编辑文本！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}