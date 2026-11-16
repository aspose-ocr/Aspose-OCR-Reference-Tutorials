---
category: general
date: 2026-04-11
description: 在 C# 中使用 Aspose OCR 从图像中提取文本。了解如何加载图像进行 OCR，并使用 GPU 支持识别 TIFF 文件中的文本。
draft: false
keywords:
- extract text from image
- load image for OCR
- recognize text from TIFF
- Aspose OCR C#
- GPU OCR processing
- high‑resolution OCR
language: zh
og_description: 使用 Aspose OCR 在 C# 中从图像提取文本。本教程展示了如何加载图像进行 OCR，并使用 GPU 加速识别 TIFF 中的文本。
og_title: 使用 C# 从图像提取文本 – 完整 OCR 指南
tags:
- OCR
- C#
- Aspose
- GPU
title: 在 C# 中从图像提取文本 – 完整 OCR 指南
url: /zh/net/text-recognition/extract-text-from-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本（C#）– 完整 OCR 指南

是否曾需要 **从图像中提取文本**，却不确定哪个库能够在处理巨大的 TIFF 时不崩溃？你并不孤单。在许多实际项目中——比如发票数字化或扫描书籍的归档——能够加载图像进行 OCR 并快速识别 TIFF 文本往往是成败关键。

在本指南中，我们将手把手演示使用 Aspose OCR for .NET 完成上述任务。完成后，你将拥有一个可运行的 C# 控制台应用程序，能够加载高分辨率扫描件，启动 GPU 加速处理（并在必要时优雅回退），并输出纯文本结果。没有缺失的环节，也没有“请参阅文档”的死胡同。

## 你需要准备的环境

- **.NET 6 或更高版本**（代码可在任何近期 SDK 上编译）
- **Aspose.OCR for .NET** NuGet 包  
  `dotnet add package Aspose.OCR`
- 一个 **大型 TIFF** 或其他你想进行 OCR 的图像格式  
  （示例使用 `large_scan.tif`）
- （可选）支持 CUDA 11+ 的 GPU —— 如果没有，库会自动切换到 CPU 模式。

就这些。让我们开始吧。

![使用 Aspose OCR 在 C# 中从图像中提取文本](image-placeholder.png "使用 Aspose OCR 在 C# 中从图像中提取文本")

## 第一步：从图像中提取文本 – 初始化 OCR 引擎

在处理任何图像之前，需要先创建一个 `OcrEngine` 实例。该引擎保存所有控制识别过程的设置。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine and request GPU processing.
        // ProcessingMode.Auto tells Aspose to fall back to CPU if a GPU isn’t detected.
        var ocrEngine = new OcrEngine
        {
            Settings = { ProcessingMode = ProcessingMode.Gpu }
        };

        // Optional: cap GPU memory usage to avoid OOM on shared machines.
        ocrEngine.Settings.GpuMemoryLimit = 1024; // MB
```

**为什么这很重要：**  
`ProcessingMode.Gpu` 可以在现代显卡上将识别时间缩短数秒，但将 `ProcessingMode.Auto`（或保持默认）设为更安全，适用于可能没有 GPU 的环境。`GpuMemoryLimit` 限制是实用技巧——没有它，巨大的图像可能会占用全部显存并导致其他应用崩溃。

## 第二步：加载图像进行 OCR – 将 TIFF 读取到内存

引擎准备好后，需要把要分析的图片喂给它。Aspose 提供的 `ImageStream.FromFile` 能够抽象掉格式处理细节。

```csharp
        // Load the high‑resolution TIFF you want to OCR.
        // Replace the path with the location of your own file.
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/large_scan.tif");
```

**内部发生了什么？**  
`ImageStream.FromFile` 会将文件读取为流，并自动检测图像格式（TIFF、PNG、JPEG 等）。如果处理多页 TIFF，Aspose 会将每一页视为单独的帧；需要时可以随后遍历它们。

## 第三步：从 TIFF 识别文本 – 运行 OCR 引擎

图像加载完毕后，重活开始。`Recognize` 方法返回一个 `OcrResult` 对象，其中包含提取的文本以及一些实用的元数据字段。

```csharp
        // Perform the OCR operation.
        var ocrResult = ocrEngine.Recognize(image);
```

**为什么只调用一次 `Recognize`？**  
因为引擎在第一次运行后会缓存内部结构，单次调用即可满足大多数场景。如果需要处理多页，复用同一个 `OcrEngine` 实例——这可以避免重新初始化 GPU 上下文的开销。

## 第四步：显示结果 – 输出提取的文本

最后，我们将识别得到的字符串输出到控制台。在真实应用中，你可能会把它写入数据库或文件。

```csharp
        // Show the extracted plain text.
        Console.WriteLine(ocrResult.Text);
    }
}
```

**预期输出：**  
如果 `large_scan.tif` 包含一张打印的发票，你会看到类似如下内容：

```
Invoice #12345
Date: 2024‑03‑15
Total: $1,234.56
...
```

具体布局取决于源图像，但关键是你已经拥有 **extract text from image** 的结果，准备好进行后续处理。

## 第五步：故障排查与特殊情况

### GPU 未检测到？

如果在没有兼容 GPU 的机器上运行示例，使用 `ProcessingMode.Auto` 时引擎会静默回退到 CPU。若想显式强制 CPU 模式，可将前面的代码行替换为：

```csharp
ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
```

### 内存占用巨大的 TIFF

非常大的扫描（例如 10 000 × 10 000 像素）仍可能超出我们设定的 1 GB GPU 上限。此时，可以提升 `GpuMemoryLimit`（前提是有剩余显存），或在送入引擎前先对图像进行降采样：

```csharp
var resized = image.Resize(4000, 4000); // keep aspect ratio as needed
var ocrResult = ocrEngine.Recognize(resized);
```

### 多页文档

如果你的 TIFF 包含多页，可使用以下方式遍历：

```csharp
for (int i = 0; i < image.PageCount; i++)
{
    var pageStream = image.GetPage(i);
    var result = ocrEngine.Recognize(pageStream);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(result.Text);
}
```

### 语言与字体支持

Aspose OCR 能自动检测拉丁文字，但对于西里尔文、阿拉伯文或自定义字体，可能需要提供相应的语言包：

```csharp
ocrEngine.Settings.Language = Language.Russian; // example
```

## 专业技巧与最佳实践

- **复用引擎**：为每张图像创建新的 `OcrEngine` 会导致明显的延迟。
- **批量处理**：处理数十个 TIFF 时，可将它们排队并使用并行线程——但要注意 GPU 显存竞争。
- **验证输出**：OCR 并非完美；对 `ocrResult.Text` 进行简单的拼写检查或正则验证，以捕获明显的误识别。
- **记录性能**：在 `Recognize` 前后使用 `Stopwatch` 测量耗时，以决定在你的环境中是否值得使用 GPU 加速。

## 结论

现在，你已经拥有一个完整的、端到端的示例，能够使用 Aspose OCR 在 C# 中 **extract text from image**。通过加载图像进行 OCR、调用引擎识别 TIFF 文本，并处理 GPU 与 CPU 场景，本教程为你提供了可直接用于发票、护照或任何扫描文档的生产级基础。

接下来可以尝试将 TIFF 换成多页 PDF，实验自定义语言包，或将输出管道化到自然语言处理流程，实现自动化数据抽取。可能性无限——祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}