---
category: general
date: 2026-01-07
description: 使用 Aspose OCR 在 C# 中从图像提取文本。了解如何从照片识别文本、提升 OCR 准确率、加载用于 OCR 的图像以及设置 OCR
  语言。
draft: false
keywords:
- extract text from image
- recognize text from photo
- improve ocr accuracy
- load image for ocr
- set ocr language
language: zh
og_description: 使用 Aspose OCR 从图像中提取文本。本指南展示了如何从照片中识别文本、提高 OCR 准确率、加载图像进行 OCR 以及设置
  OCR 语言。
og_title: 使用 Aspose OCR 从图像提取文本 – C# 教程
tags:
- Aspose OCR
- C#
- Image Processing
title: 使用 Aspose OCR 从图像提取文本 – 完整 C# 指南
url: /zh/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本 – 完整的 C# 实现（使用 Aspose OCR）

是否曾需要 **从图像中提取文本**，却不确定哪个库能够提供可靠的结果？你并不孤单。在许多实际应用中——收据扫描、身份证验证，或只是一个快速记事工具——**从照片中识别文本** 是必备功能。

在本教程中，我们将逐步演示一个完整、可直接运行的示例，展示如何 **加载图像进行 OCR**、配置引擎以 **设置 OCR 语言**，以及使用一些预处理技巧来 **提升 OCR 准确率**。完成后，你将拥有一个单独的 C# 文件，能够将提取的文本打印到控制台，并且了解每个设置背后的原因。

> **提示：** 代码适用于 Aspose.OCR ≥ 23.5、.NET 6+，以及任何能够运行 .NET Core 的 Windows、Linux 或 macOS 环境。

## 前置条件

- 已安装 .NET 6 SDK（或更高）  
- Visual Studio 2022、VS Code，或任意你喜欢的编辑器  
- NuGet 包 `Aspose.OCR`（通过 `dotnet add package Aspose.OCR` 安装）  
- 一张包含清晰印刷或打字文本的图像文件（JPEG/PNG）  

如果你已经准备好这些，就让我们开始吧。

![extract text from image example](/images/ocr-example.png "extract text from image – Aspose OCR output")

## 步骤 1：创建并释放 OCR 引擎 – “从图像中提取文本”核心

首先需要一个 `OcrEngine` 实例。将其放在 `using` 块中可以确保本机资源得到正确释放。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

/// <summary>
/// Demonstrates how to extract text from image using Aspose OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // Step 1 – Initialize the OCR engine (the heart of the process)
        using (var ocrEngine = new OcrEngine())
        {
            // The rest of the workflow lives inside this block.
```

**为什么重要：** `OcrEngine` 为本机 OCR DLL 持有非托管内存。及时释放可以防止内存泄漏，尤其是在批量处理大量图像时。

## 步骤 2：定义识别设置 – 提升 OCR 准确率

接下来创建一个 `RecognitionSettings` 对象。在这里我们 **设置 OCR 语言** 并添加常用的预处理过滤器，这些过滤器往往决定了输出是乱码还是干净的文本。

```csharp
            // Step 2 – Configure recognition settings
            var recognitionSettings = new RecognitionSettings
            {
                // Set the language to English; other languages are available via Language enum.
                Language = Language.English,

                // PreprocessFilters help the engine deal with real‑world photo issues.
                PreprocessFilters = new[]
                {
                    PreprocessFilter.Deskew,          // Corrects slight rotation
                    PreprocessFilter.Denoise,         // Reduces grainy noise
                    PreprocessFilter.ContrastEnhance // Boosts text visibility
                }
            };
```

**这些过滤器的作用是什么？**  
- **Deskew** 修正手机拍摄的照片常出现的轻微倾斜。  
- **Denoise** 去除可能被误识别为字符的噪点。  
- **ContrastEnhance** 让淡淡的墨迹更加突出，这对于 **提升 OCR 准确率** 至关重要。

## 步骤 3：加载图像 – 高效地为 OCR 加载图像

Aspose 提供 `ImageStream.FromFile` 以便快速加载。如果图像来自网络请求或数据库，也可以使用 `MemoryStream`。

```csharp
            // Step 3 – Load the image you want to analyze
            var imagePath = @"YOUR_DIRECTORY/phone_photo.jpg";
            var imageStream = ImageStream.FromFile(imagePath);
```

**常见坑点：** 在 Windows 上使用正斜杠路径可以工作，但使用 `Path.Combine` 对跨平台项目更安全。

## 步骤 4：执行识别 – 从照片中识别文本

现在调用 `Recognize`，同时传入图像流和我们的设置。该方法返回包含提取文本的普通字符串。

```csharp
            // Step 4 – Run OCR and capture the result
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

如果图像中包含多个文本块，Aspose 会使用换行符将它们连接起来，尽可能保留原始布局。

## 步骤 5：输出结果 – 验证提取效果

最后，将结果写入控制台。在真实应用中，你可能会将其存入数据库、发送给其他服务，或在 UI 中显示。

```csharp
            // Step 5 – Show the extracted text
            Console.WriteLine("=== Extracted Text Start ===");
            Console.WriteLine(recognizedText);
            Console.WriteLine("=== Extracted Text End ===");
        } // End of using block – OcrEngine disposed
    }
}
```

### 预期的控制台输出

```
=== Extracted Text Start ===
This is a sample receipt.
Total: $23.45
Thank you for shopping!
=== Extracted Text End ===
```

如果出现乱码，请再次确认图像是否清晰、语言是否匹配，以及预处理过滤器是否合适。

## 步骤 6：可选微调 – 针对特殊情况进行细调

### a. 切换语言

```csharp
recognitionSettings.Language = Language.Spanish; // For Spanish receipts
```

### b. 添加自定义过滤器

Aspose 还提供 `PreprocessFilter.Sharpen` 或 `PreprocessFilter.Binarize`。当默认的三种过滤器不足以满足需求时，可尝试这些选项。

### c. 处理大图像

对于超高分辨率的照片，建议先进行下采样，以降低内存占用：

```csharp
var resizedStream = ImageProcessor.Resize(imageStream, 1024, 768);
string text = ocrEngine.Recognize(resizedStream, recognitionSettings);
```

## 常见问题

**Q: 这能处理手写笔记吗？**  
A: Aspose OCR 主要针对印刷文本进行优化。手写识别需要使用其他引擎（例如 Aspose.OCR for Handwriting）或机器学习模型。

**Q: 能否在循环中处理多张图像？**  
A: 完全可以。只需将 `using (var ocrEngine = new OcrEngine())` 块移到循环外部，复用同一个引擎以获得更好性能。

**Q: 如果图像是 PDF 页面怎么办？**  
A: 先将 PDF 页面转换为图像（Aspose.PDF 可将页面渲染为 PNG/JPEG），然后再交给 OCR 引擎处理。

## 回顾 – 我们实现了什么

- 使用单个、独立的 C# 程序 **从图像中提取文本**。  
- 演示了如何通过预处理 **从照片中识别文本**，从而 **提升 OCR 准确率**。  
- 展示了正确的 **为 OCR 加载图像** 与 **设置 OCR 语言** 的方式，适用于多语言场景。  

## 后续步骤与相关主题

- **批量处理：** 将本代码片段与 `Directory.GetFiles` 结合，可一次性 OCR 整个文件夹。  
- **后处理：** 使用正则表达式在提取后清理日期、金额或 ID 等信息。  
- **集成：** 将提取的文本导入 Azure Cognitive Search 或 Elastic，实现可搜索的文档。  

欢迎尝试不同的过滤器组合、语言以及图像来源。核心模式保持不变：创建引擎、配置设置、加载图像、识别并输出。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}