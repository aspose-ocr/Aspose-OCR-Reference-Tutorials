---
category: general
date: 2026-05-31
description: 学习如何使用 Aspose OCR 在 C# 中识别图像中的文本，包括如何从 TIFF 文件提取文本以及高效加载图像进行 OCR。
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: zh
og_description: 使用 Aspose OCR 的逐步指南，识别图像中的文本，涵盖从 TIFF 提取以及正确的图像加载以进行 OCR。
og_title: 在 C# 中使用 Aspose OCR 识别图像中的文本
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: 在 C# 中使用 Aspose OCR 识别图像中的文本
url: /zh/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 在 C# 中识别图像中的文本

是否曾经需要**从图像中识别文本**却不知从何入手？你并不孤单——许多开发者在处理扫描文档或多页 TIFF 时都会遇到这个难题。在本指南中，我们将通过一个完整、可直接运行的示例，演示如何使用 Aspose OCR 库**识别图像中的文本**，并展示如何**从 tiff 中提取文本**以及在**加载图像进行 OCR**时的最佳实践，帮助你省去摸索的时间。

我们将覆盖从安装 NuGet 包到处理 GPU 加速以及在需要时回退到 CPU 的全部步骤。教程结束后，你将拥有一个控制台应用程序，能够打印识别出的文本和处理时间——没有遗漏的环节，也没有模糊的引用。

## 你将构建的内容

- 一个简单的 .NET 控制台应用，能够加载图像（包括多页 TIFF）  
- 一个配置了 GPU 使用的 OCR 引擎，并具备优雅的 CPU 回退机制  
- 从图像中提取纯文本并打印到控制台  
- 计时信息，帮助你直观看到 GPU 与 CPU 的性能差异  

**先决条件**

- .NET 6 SDK 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）  
- 对 C# 与命令行的基本了解  
- 能够访问互联网以获取 Aspose.OCR NuGet 包  

如果你满足以上条件，下面我们开始吧。

![使用 Aspose OCR 进行 C# 图像文本识别的代码](image.png "使用 Aspose OCR 进行 C# 图像文本识别的代码")

## 第一步 – 识别图像中的文本：设置 OCR 引擎

首先，需要创建一个 `OcrEngine` 实例。Aspose OCR 允许你选择处理设备——GPU 用于加速，CPU 作为安全备选。引擎还接受内存限制提示，在共享机器上非常实用。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**为什么重要：**  
选择 `OcrDevice.Gpu` 可以在处理大图像（尤其是多页 TIFF）时节省数秒的识别时间。`GpuMemoryLimit` 能防止你的应用在共享工作站上占用全部 GPU 内存。

## 第二步 – 为 OCR 加载图像（支持 TIFF）

接下来，将图像传给引擎。Aspose 的 `ImageStream.FromFile` 支持**任何**库能够处理的格式——TIFF、PNG、JPEG，随你挑选。这一步直接满足了**加载图像进行 OCR**的需求。

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**小技巧：** 如果你处理的是多页 TIFF，Aspose 会自动将每一页视为独立帧，引擎会顺序处理，无需额外代码。

## 第三步 – 运行识别并**从 tiff 中提取文本**

在引擎准备好、图像加载完毕后，启动 OCR 操作。`Recognize` 方法返回一个 `OcrResult`，其中包含纯文本、置信度分数以及计时细节。

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**边缘情况处理：**  
如果 GPU 不可用，`engine.Recognize()` 仍然可以工作，因为引擎会悄悄切换到 CPU。如果需要记录实际使用的设备，可在识别后检查 `engine.Device`。

## 第四步 – 获取识别后的纯文本

提取文本非常直接——读取 `Text` 属性即可。这正是我们最终**从 tiff 中提取文本**（或其他图像）并呈现给用户的地方。

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

你会看到原始字符，换行符会保持与源图像中的布局一致。若需要更结构化的输出（如 JSON 或 CSV），可以进一步探索 `result.Regions` 与 `result.Lines`，但对于快速脚本来说，纯文本已经足够。

## 第五步 – 测量处理时间并处理 GPU 回退

性能至关重要，尤其是在处理数十页时。`ProcessingTime` 属性会精准告知 OCR 所耗时长，无论是运行在 GPU 还是 CPU 上。

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**为什么要关注：**  
如果发现耗时急剧上升，可以尝试调小 `GpuMemoryLimit` 或显式切换到 CPU（`Device = OcrDevice.Cpu`）。相反，若在大尺寸 TIFF 上得到亚秒级结果，说明 GPU 加速发挥了作用。

## 完整、可直接运行的示例

将下面的代码复制到新建的控制台项目中（`dotnet new console -n OcrDemo`），然后执行 `dotnet add package Aspose.OCR`。随后将 `YOUR_DIRECTORY/sample_multi_page.tif` 替换为你的图像路径。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**预期输出（为简洁起见已截断）：**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

如果你的机器没有合适的 GPU，耗时可能会多几秒，但文本仍会被正确提取。

## 常见问题与注意事项

- **如果图像非常大（超过 10 MB）怎么办？**  
  在送入引擎前降低分辨率，或在显存充足的情况下提升 `GpuMemoryLimit`。  
- **可以在循环中处理多张图像吗？**  
  完全可以。只需复用同一个 `OcrEngine` 实例，并在每次迭代中为其分配新的 `ImageStream`。  
- **需要手动释放资源吗？**  
  `OcrEngine` 实现了 `IDisposable`。建议使用 `using` 块进行资源管理，尤其是在使用 GPU 资源时。  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **如何处理非英文语言？**  
  在调用 `Recognize()` 之前设置 `engine.Language = OcrLanguage.Spanish`（或任意受支持语言）。  

## 结论

现在，你已经拥有一个完整的端到端解决方案，能够在 C# 中使用 Aspose OCR **识别图像中的文本**。本教程涵盖了**加载图像进行 OCR**、**从 tiff 中提取文本**以及在优雅处理 GPU 回退的同时测量性能的全部要点。

接下来，你可以：

- 试验不同的图像格式（BMP、PDF），观察 Aspose 的处理效果。  
- 深入研究 `result.Regions`，获取包含位置信息的边界框数据，以实现版面感知的后续处理。

## 接下来该学习什么？

- [How to Use Aspose to Recognize Image from Stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}