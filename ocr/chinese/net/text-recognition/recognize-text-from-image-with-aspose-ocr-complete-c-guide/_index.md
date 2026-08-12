---
category: general
date: 2026-02-22
description: 使用 Aspose OCR 在 C# 中识别图像中的文本。了解如何加载 TIFF 图像、创建 OCR 引擎以及高效地从图像中提取文本。
draft: false
keywords:
- recognize text from image
- load tiff image
- extract text from image
- create OCR engine
language: zh
og_description: 一步一步识别图像中的文字。学习如何加载 TIFF 图像、创建 OCR 引擎，并使用 Aspose OCR 在 C# 中提取图像文字。
og_title: 从图像识别文本 – 完整的 C# Aspose OCR 教程
tags:
- C#
- Aspose OCR
- Image Processing
title: 使用 Aspose OCR 从图像识别文本 – 完整 C# 指南
url: /zh/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像识别文本 – 完整 C# Aspose OCR 教程

是否曾经需要**从图像识别文本**但在第一行代码就卡住了？你并不孤单。在许多项目中——发票扫描、档案数字化或构建可搜索的 PDF 库——从图片中获取干净的文本是第一道难关。  

好消息：使用 Aspose OCR，你可以加载 TIFF 图像，启动 OCR 引擎，并在几行代码内**从图像提取文本**。在本教程中，我们将完整演示整个流程，从加载高分辨率 TIFF 文件到打印识别的文本和处理时间。  

我们还会覆盖一些“如果如何”情景，例如禁用 GPU 加速或处理多页 TIFF，这样当你的真实数据略有不同的时候你就不会感到惊讶。结束时，你将拥有一个可直接运行的控制台应用程序，能够可靠地**从图像识别文本**。

## 前提条件

- .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）
- Aspose.OCR NuGet 包 (`dotnet add package Aspose.OCR`)
- 需要处理的 TIFF 文件（示例使用 `high_res_page.tif`）
- 任意你喜欢的 IDE——Visual Studio、Rider 或 VS Code 都可以

无需额外的本地库；Aspose 在内部处理所有内容，包括可选的 GPU 支持。

## 步骤 1：加载 TIFF 图像

首先需要将图像数据加载到内存中。Aspose 提供了一个静态的 `Image.Load` 方法，支持大多数常见格式，包括 TIFF。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Load the TIFF file – replace the path with your own image location
var inputImage = Image.Load(@"YOUR_DIRECTORY/high_res_page.tif");
```

**为什么重要：** TIFF 文件通常包含多页或高分辨率数据，其他库可能无法处理。Aspose 的加载器能够正确读取文件并保持像素深度，这对后续的高精度 OCR 至关重要。  

*小贴士：* 如果处理多页 TIFF，可以遍历 `inputImage.Frames` 并逐帧处理。这样就不会错过后续页面中隐藏的文本。

## 步骤 2：创建 OCR 引擎

图像已加载到内存后，你需要一个能够识别字符的引擎。`OcrEngine` 类用于配置语言、GPU 使用以及其他选项。

```csharp
// Initialize the OCR engine with desired settings
var ocrEngine = new OcrEngine
{
    // Enable GPU acceleration for faster processing (optional, requires compatible hardware)
    UseGpu = true,
    // Set the language to English – you can change this to Language.French, etc.
    Language = Language.English
};
```

**为什么重要：** 启用 GPU (`UseGpu = true`) 可以在支持的机器上显著缩短处理时间，但如果在 CI 服务器或低端笔记本上运行，关闭它也是完全安全的。另外，选择正确的语言能够提升字符识别，因为引擎会加载特定语言的词典。  

*注意：* 如果忘记设置 `Language`，引擎默认使用英语，这在非拉丁文字脚本上可能产生奇怪的结果。

## 步骤 3：从图像识别文本

引擎准备好后，实际的 OCR 调用只需一个方法：`Recognize`。它返回一个 `OcrResult` 对象，包含提取的文本和性能指标。

```csharp
// Perform OCR on the loaded image
var ocrResult = ocrEngine.Recognize(inputImage);
```

`OcrResult` 为你提供两个便利属性：

- `Text` – 引擎能够读取的所有内容的纯文本表示。
- `ProcessingTime` – OCR 所耗费的时间，以毫秒为单位。

## 步骤 4：审查结果

最后，让我们输出得到的内容。在实际应用中，你可能会将文本写入数据库，但演示目的下控制台输出已经足够。

```csharp
// Show how long the OCR took and the recognized text
Console.WriteLine($"Recognized in {ocrResult.ProcessingTime} ms");
Console.WriteLine("=== Extracted Text Start ===");
Console.WriteLine(ocrResult.Text);
Console.WriteLine("=== Extracted Text End ===");
```

**预期输出**（你的文本当然会不同）：

```
Recognized in 842 ms
=== Extracted Text Start ===
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
...
=== Extracted Text End ===
```

如果输出出现乱码，请再次确认图像是否清晰以及是否选择了正确的语言。你还可以调整 `ocrEngine` 的属性，例如 `PreprocessOptions`，以进行降噪处理。

## 处理边缘情况

### 1. 没有 GPU？没问题。

```csharp
ocrEngine.UseGpu = false; // fallback to CPU‑only processing
```

CPU 处理速度较慢（通常慢 2‑3 倍），但它在所有 Windows、Linux 或 macOS 机器上都能运行。

### 2. 多页 TIFF

```csharp
foreach (var frame in inputImage.Frames)
{
    var pageResult = ocrEngine.Recognize(frame);
    Console.WriteLine(pageResult.Text);
}
```

每一帧都会被视为单独的图像，因此每页都会得到一段文本。

### 3. 不同语言

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, Language.German, etc.
```

切换语言会加载相应的字符集和词典，显著提升非英文文档的识别准确率。

## 完整工作示例

下面是完整的程序代码，你可以复制粘贴到新的控制台项目中（`dotnet new console`）。它包含了我们讨论的所有部分，并加入了一些安全检查。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the TIFF image you want to process
        // -------------------------------------------------
        const string imagePath = @"YOUR_DIRECTORY/high_res_page.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"Error: File not found at {imagePath}");
            return;
        }

        var inputImage = Image.Load(imagePath);

        // -------------------------------------------------
        // Step 2: Create and configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,                 // optional – set to false if GPU not available
            Language = Language.English    // change if you need another language
        };

        // -------------------------------------------------
        // Step 3: Perform OCR on the loaded image
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 4: Display processing time and extracted text
        // -------------------------------------------------
        Console.WriteLine($"Recognized in {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text Start ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("=== Extracted Text End ===");

        // Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

保存文件，运行 `dotnet run`，即可在控制台看到识别出的文本。就这样——你的**从图像识别文本**流水线已经启动并运行。

## 常见问题

**Q: 这能用于 PNG 或 JPEG 吗？**  
A: 当然可以。`Image.Load` 会自动检测格式，所以你可以将 `.tif` 扩展名替换为 `.png`、`.jpg` 或甚至 `.bmp`。OCR 引擎对它们的处理方式相同。

**Q: 我的输出包含很多杂乱的符号。**  
A: 尝试启用预处理：`ocrEngine.PreprocessOptions = new PreprocessOptions { RemoveNoise = true, Deskew = true };`。这会在识别前清理图像。

**Q: 我能获取每个单词的边界框吗？**  
A: 可以。`ocrResult.Regions` 包含带坐标的 `OcrRegion` 对象。如果需要在 UI 中高亮显示单词，可遍历它们。

## 结论

我们刚刚演示了如何在 C# 中使用 Aspose OCR **从图像识别文本**。从加载 TIFF 文件开始，然后**创建 OCR 引擎**，运行识别，最后显示结果——每一步都简洁、解释完整，且可以直接复制到你的项目中。  

接下来，你可以探索文件夹的批量处理、将结果存储到可搜索的索引中，或将 OCR 与翻译 API 结合使用。无论选择何种方式，核心模式保持不变：加载图像、配置引擎、识别并处理输出。  

对加载 TIFF 图像、从图像提取文本或调优 OCR 引擎还有更多疑问吗？在下方留言吧，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}