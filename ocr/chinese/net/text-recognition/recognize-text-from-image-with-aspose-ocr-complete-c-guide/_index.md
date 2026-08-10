---
category: general
date: 2026-05-25
description: 使用 Aspose OCR 在 C# 中识别图像中的文本。了解如何加载用于 OCR 的图像、设置 OCR 语言、创建 OCR 引擎以及从
  TIFF 中提取文本。
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- set OCR language
- create OCR engine
language: zh
og_description: 使用 Aspose OCR 在 C# 中识别图像文本。本教程展示了如何创建 OCR 引擎、加载 OCR 图像、设置 OCR 语言以及从
  TIFF 中提取文本。
og_title: 使用 Aspose OCR 从图像识别文本 – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: recognize text from image using Aspose OCR in C#. Learn how to load
    image for OCR, set OCR language, create OCR engine and extract text from TIFF.
  headline: recognize text from image with Aspose OCR – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Remove the `GpuDevice` line; the engine will automatically switch to CPU
      mode. Performance will be slower but the results remain accurate.
    question: What if my GPU isn’t detected?
  - answer: Absolutely—`Image.FromFile` works with any format supported by System.Drawing,
      so you can **load image for OCR** regardless of extension.
    question: Can I process PNG or JPEG files?
  - answer: Increase `ocrEngine.PreprocessOptions.Dpi` before calling `Recognize`.
      Higher DPI gives the engine more pixels to work with, improving accuracy.
    question: How do I handle low‑resolution scans?
  - answer: The `GpuMemoryLimit` property caps GPU usage. If you hit the limit, the
      engine will fallback to CPU for the remaining pages.
    question: Is there a limit to the size of the TIFF?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
- Text Extraction
title: 使用 Aspose OCR 从图像识别文本 – 完整 C# 指南
url: /zh/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 从图像识别文本 – 完整 C# 指南

是否曾经需要**从图像识别文本**，但不确定哪个库既能提供速度又能保证准确性？你并不孤单。在许多发票处理或归档项目中，最大的问题是如何在不编写自定义解析器的情况下，从 TIFF 文件中获取干净、可搜索的文本。

事实是：Aspose OCR for .NET 让整个流程变得轻而易举。在本指南中，我们将逐步演示你需要的所有内容——安装包、**创建 OCR 引擎**、加载 TIFF、设置 OCR 语言，最后**从 TIFF 中提取文本**。完成后，你将拥有一个可直接运行的控制台应用程序，能够快速**从图像识别文本**。

## Prerequisites

- .NET 6.0 或更高（代码同样适用于 .NET Core 和 .NET Framework）
- Visual Studio 2022（或任何你喜欢的 IDE）
- Aspose.OCR NuGet 包（GPU 支持需要 `Aspose.OCR.Gpu` 插件）
- 如果想要更快的速度，需要具备 CUDA 支持的 GPU（可选，但推荐）

> **技巧提示：** 如果没有 GPU，只需省略 `GpuDevice` 行，引擎会自动回退到 CPU。

## Step 1: Install Aspose OCR and Create OCR Engine

首先，通过 NuGet 添加必要的包：

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu   # optional GPU support
```

现在我们可以**创建 OCR 引擎**。该对象是整个过程的核心；它保存了运行设备和内存限制等配置。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU support
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine (GPU‑enabled)
        var ocrEngine = new OcrEngine
        {
            // 0 = first GPU in the system; change if you have multiple cards
            GpuDevice = new GpuDevice(0),
            // Optional: cap GPU memory usage to 1024 MB
            GpuMemoryLimit = 1024
        };
```

**为什么这很重要：** 将引擎绑定到 GPU 后，你可以显著缩短**从图像识别文本**所需的时间，尤其是处理大量高分辨率 TIFF 时。

## Step 2: Load Image for OCR

接下来，我们需要**加载图像进行 OCR**。Aspose.OCR 使用 `System.Drawing.Image`，因此任何 GDI+ 支持的格式（包括多页 TIFF）都可以。

```csharp
        // Step 2: Load the image you want to process
        // Replace the path with the location of your TIFF file
        var imagePath = @"C:\Invoices\invoice_batch.tif";
        Image image = Image.FromFile(imagePath);
```

如果处理多页 TIFF，可以使用 `image.SelectActiveFrame` 循环遍历页面，但在大多数情况下一次调用即可满足需求。

## Step 3: Set OCR Language

引擎不会自动识别你要扫描的语言。请在运行识别器之前**设置 OCR 语言**；否则会得到大量乱码。

```csharp
        // Step 3: Tell the engine which language to expect
        ocrEngine.Language = OcrLanguage.English; // change to .German, .French, etc. as needed
```

> **你知道吗？** 在运行时切换语言开销很小——甚至可以在页面之间更改此属性，以处理混合语言的文档。

## Step 4: Perform the Recognition – Recognize Text from Image

现在进入有趣的部分：实际**从图像识别文本**。`Recognize` 方法返回包含所有检测到字符的普通字符串。

```csharp
        // Step 4: Run OCR and capture the output
        string recognizedText = ocrEngine.Recognize(image);
```

如果需要置信度分数或边界框，可以使用返回 `OcrResult` 对象的重载，但对于大多数提取任务，普通字符串已足够。

## Step 5: Extract Text from TIFF (and handle multi‑page files)

当源文件是包含多页的 TIFF 时，需要对每一帧重复步骤 2‑4。下面是一个快速循环，**逐页从 TIFF 中提取文本**：

```csharp
        // Optional: process multi‑page TIFFs
        var totalFrames = image.GetFrameCount(FrameDimension.Page);
        for (int i = 0; i < totalFrames; i++)
        {
            image.SelectActiveFrame(FrameDimension.Page, i);
            string pageText = ocrEngine.Recognize(image);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
```

上述代码会打印每页提取的文本，使得将结果导入数据库或搜索索引变得非常简单。

## Step 6: Display or Persist the Extracted Text

最后，让我们**显示提取的文本**，并可选择将其写入文件以便后续处理。

```csharp
        // Step 6: Output the result to console
        Console.WriteLine("=== Full OCR Result ===");
        Console.WriteLine(recognizedText);

        // Optional: Save to a .txt file
        System.IO.File.WriteAllText(@"C:\Invoices\extracted_text.txt", recognizedText);
    }
}
```

运行程序后应输出识别的字符，并在源 TIFF 旁边创建 `extracted_text.txt` 文件。

---

## Common Questions & Edge Cases

- **如果我的 GPU 未被检测到怎么办？**  
  删除 `GpuDevice` 行；引擎会自动切换到 CPU 模式。性能会变慢，但结果仍然准确。

- **我可以处理 PNG 或 JPEG 文件吗？**  
  当然可以——`Image.FromFile` 支持 System.Drawing 支持的任何格式，因此无论扩展名如何，都可以**加载图像进行 OCR**。

- **如何处理低分辨率扫描？**  
  在调用 `Recognize` 之前提升 `ocrEngine.PreprocessOptions.Dpi`。更高的 DPI 为引擎提供更多像素，从而提升准确性。

- **TIFF 的大小有没有限制？**  
  `GpuMemoryLimit` 属性限制 GPU 使用量。如果达到上限，引擎会对剩余页面回退到 CPU。

## Conclusion

现在，你已经拥有一个完整的、可投入生产的代码片段，使用 Aspose OCR 在 C# 中**从图像识别文本**。本教程涵盖了如何**创建 OCR 引擎**、**加载图像进行 OCR**、**设置 OCR 语言**以及**从 TIFF 中提取文本**——并利用 GPU 加速提升速度。

从这里你可能：

- 尝试不同的语言（`OcrLanguage.Spanish`、`OcrLanguage.ChineseSimplified` 等）。
- 将输出集成到可搜索的 ElasticSearch 索引中。
- 添加后处理（拼写检查、正则清理）以提升数据质量。

在自己的发票批次上试一试，调整内存限制，观察 OCR 性能飞速提升。祝编码愉快！

## Related Tutorials

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}