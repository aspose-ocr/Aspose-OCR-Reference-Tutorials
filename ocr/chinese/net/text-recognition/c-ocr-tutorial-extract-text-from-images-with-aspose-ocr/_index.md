---
category: general
date: 2026-03-21
description: c# OCR 教程：学习如何使用 Aspose OCR（GPU 加速）在 c# 中提取图像文本、扫描发票并加载图像。
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- ocr invoice scanning
- how to ocr image
- load image in c#
language: zh
og_description: c# OCR 教程：逐步指南，教你从图像中提取文本，进行 OCR 发票扫描，并学习如何在 C# 中使用 GPU 加速进行图像 OCR。
og_title: c# OCR 教程 – 使用 Aspose OCR 从图像中提取文本
tags:
- OCR
- C#
- Image Processing
title: C# OCR 教程 – 使用 Aspose OCR 从图像中提取文本
url: /zh/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教程 – 使用 Aspose OCR 从图像中提取文本

有没有想过如何以 **c# OCR tutorial** 的方式解决现实问题，比如将扫描的发票转换为可编辑的文本？你并不孤单。许多开发者在需要 *extract text from image* 文件时会遇到瓶颈，最终写出脆弱的解析器，一遇到噪声扫描就崩溃。

事实是——Aspose.OCR 让整个过程轻而易举，尤其是在启用 GPU 加速时。在本指南中，你将看到如何 **how to ocr image** 文件在 C# 中使用，正确地在 c# 中加载图像，甚至能够处理常见的发票扫描怪癖，而无需抓狂。

通过本教程，你将拥有一个可运行的控制台应用程序，它读取 TIFF 发票，在 GPU 上执行 OCR，并打印干净的纯文本输出。没有魔法，只有可以复制粘贴并适配的可靠代码。

---

## 你需要的环境

- **.NET 6.0** (or later) – 当前的 LTS 版本，让你的项目面向未来。
- **Aspose.OCR for .NET** NuGet package – 版本 23.10（撰写时的最新版本）。
- 一台 **GPU‑enabled machine**（可选但推荐）– 如果未检测到兼容的 GPU，代码会自动回退到 CPU。
- 示例图像，例如 `large_invoice.tif`。任何受支持的格式（PNG、JPEG、TIFF、PDF）均可使用。

如果你尚未安装 NuGet 包，请运行：

```bash
dotnet add package Aspose.OCR
```

既然我们已经介绍了前置条件，接下来深入实际步骤。

---

## 步骤 1：创建新控制台项目并添加 Aspose.OCR

首先，创建一个全新的控制台应用，以便保持教程的自包含性。

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
dotnet add package Aspose.OCR
```

> **专业提示：** 使用 `-n` 参数为项目指定有意义的名称；当你以后开始添加更多模块时，它能保持解决方案整洁。

Visual Studio 创建的 `Program.cs` 文件将成为我们的实验场。打开它并清除默认的 `Console.WriteLine` 行——我们将用 OCR 逻辑替换它。

---

## 步骤 2：在 C# 中加载图像 – 正确方式

加载图像看似简单，但处理不当会导致内存泄漏或文件被锁定。`System.Drawing.Image` 类在大多数场景下工作良好，但必须将其包装在 `using` 块中以确保释放。

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 2: Load the image you want to OCR.
            // Replace the path with the actual location of your invoice file.
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // The using statement ensures the image gets disposed automatically.
            using var inputImage = Image.FromFile(imagePath);
            
            // Continue to the OCR engine setup…
        }
    }
}
```

请注意注释 `// 👉 Step 2:`——它对应了本教程的步骤编号，帮助后续阅读代码的人快速定位。

---

## 步骤 3：使用 GPU 加速初始化 OCR 引擎

Aspose.OCR 允许你在构造时选择处理模式。`OcrEngineMode.Gpu` 告诉库在检测到显卡时使用它；否则会静默回退到 CPU，无需额外的回退逻辑。

```csharp
// 👉 Step 3: Create the OCR engine.
// The constructor argument selects GPU mode; it's the fastest option for large invoices.
var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);
```

> **为什么使用 GPU？**  
> 对高分辨率发票进行 OCR 会非常耗费 CPU。将计算卸载到 GPU 可以将运行时间从数秒缩短到瞬间，尤其是在批量处理时效果更明显。

---

## 步骤 4：运行 OCR 并从图像中提取文本

现在魔法出现了。调用 `Recognize` 并获取纯文本。Aspose 返回一个 `OcrResult` 对象，里面包含原始文本、置信度分数，甚至每个字符的边界框（如果你后续需要的话）。

```csharp
// 👉 Step 4: Perform the OCR operation.
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Display the extracted text.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

运行程序后，你应该会看到类似的输出：

```
=== OCR Output ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

如果输出乱码，请再次确认图像对比度足够高且 OCR 语言设置正确（默认是 English）。你也可以微调 `ocrEngine.Settings` 以提升准确率，但默认设置已能很好地处理大多数打印发票。

---

## 步骤 5：处理 OCR 发票扫描的边缘情况

发票形态多样——有的多页，有的包含表格或手写备注。下面提供几种无需重写整个流水线的快速调整方式。

### 5.1 多页 PDF 或 TIFF

如果源文件包含多页，需要遍历每一页并将结果拼接起来。

```csharp
using var multiPageImage = Image.FromFile(@"C:\Invoices\multi_page_invoice.tif");

// Aspose can split multi‑page TIFFs into separate images.
for (int i = 0; i < multiPageImage.GetFrameCount(FrameDimension.Page); i++)
{
    multiPageImage.SelectActiveFrame(FrameDimension.Page, i);
    using var page = (Image)multiPageImage.Clone();
    var pageResult = ocrEngine.Recognize(page);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

### 5.2 低分辨率扫描

如果 DPI 低于 150，在送入引擎前先对图像进行放大。这样可以显著提升字符识别率。

```csharp
// Simple nearest‑neighbor scaling – replace with a better algorithm if needed.
var highRes = new Bitmap(inputImage, new Size(inputImage.Width * 2, inputImage.Height * 2));
var highResResult = ocrEngine.Recognize(highRes);
Console.WriteLine(highResResult.Text);
```

### 5.3 自定义语言包

默认情况下 Aspose 使用英语。若需其他语言，请从 Aspose 官方站点下载相应的语言包并进行注册：

```csharp
ocrEngine.Settings.Language = OcrLanguage.Spanish; // example for Spanish invoices
```

这些微调让你的 **ocr invoice scanning** 方案足够稳健，能够应对生产环境的工作负载。

---

## 完整工作示例

下面是完整的、可直接运行的程序示例，已整合上述所有步骤。复制到 `Program.cs`，修改文件路径后按 **F5** 运行。

```csharp
// ---------------------------------------------------------------
// Complete c# OCR tutorial – Aspose OCR with GPU acceleration
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialize the OCR engine (GPU mode)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);

            // -----------------------------------------------------------------
            // Step 2: Load the image you want to process
            // -----------------------------------------------------------------
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // Using ensures the image is disposed properly.
            using var inputImage = Image.FromFile(imagePath);

            // -----------------------------------------------------------------
            // Step 3: Run OCR and extract plain text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);

            // -----------------------------------------------------------------
            // Step 4: Output the result
            // -----------------------------------------------------------------
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);

            // -----------------------------------------------------------------
            // Optional: Demonstrate handling a multi‑page TIFF (comment out if not needed)
            // -----------------------------------------------------------------
            // HandleMultiPageTiff(@"C:\Invoices\multi_page_invoice.tif", ocrEngine);
        }

        // ---------------------------------------------------------------
        // Helper for multi‑page TIFFs – shows how to iterate pages
        // ---------------------------------------------------------------
        static void HandleMultiPageTiff(string path, OcrEngine engine)
        {
            using var multiPage = Image.FromFile(path);
            int pageCount = multiPage.GetFrameCount(FrameDimension.Page);

            for (int i = 0; i < pageCount; i++)
            {
                multiPage.SelectActiveFrame(FrameDimension.Page, i);
                using var page = (Image)multiPage.Clone();
                var result = engine.Recognize(page);
                Console.WriteLine($"\n--- Page {i + 1} ---");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

**预期输出**（为简洁起见已截断）：

```
=== OCR Output ===
Invoice #98765
Date: 02/28/2026
Bill To: Acme Corp.
Subtotal: $2,500.00
Tax (8%): $200.00
Total: $2,700.00
...
```

运行程序并确认控制台打印出发票上的文本。如果得到空字符串，请再次检查图像路径是否正确以及文件是否损坏。

---

## 常见问题 (FAQ)

**Q: 这在 Linux 上能工作吗？**  
A: 能。Aspose.OCR 是跨平台的。只需在 Linux 上安装 .NET 运行时，使用同一 NuGet 包即可。GPU 加速需要兼容 CUDA 的显卡以及相应的驱动。

**Q: 如果没有 GPU 怎么办？**  
A: `OcrEngineMode.Gpu` 构造函数会在未检测到兼容 GPU 时自动回退到 CPU。仍然可以得到准确的结果，只是耗时会稍长。

**Q: 能识别手写笔记吗？**  
A: Aspose 默认模型侧重于印刷文本。手写体需要专门的模型或其他服务（例如 Azure Form Recognizer）。当然，你仍可以尝试相同的代码，只是要预期置信度会更低。

---

## 结论

你刚刚完成了一个 **c# OCR tutorial**，展示了如何 *extract text from image* 文件，进行 **ocr invoice scanning**，并了解 **how to o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}