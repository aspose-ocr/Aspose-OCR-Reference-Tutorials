---
category: general
date: 2026-01-15
description: c# OCR 教程，展示如何使用 Aspose OCR 在 GPU 上识别图像中的文本、提取发票文本并将图像转换为文本。
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- extract text from invoice
- convert image to text
- load image for ocr
language: zh
og_description: c# OCR 教程，教你从图像识别文本、从发票提取文本，并使用 Aspose OCR 在 GPU 上将图像转换为文本。
og_title: c# OCR 教程 – 快速 GPU 加速文本识别
tags:
- OCR
- C#
- Aspose
- GPU
title: C# OCR 教程 – 使用 GPU 加速识别图像中的文字
url: /zh/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr 教程 – 使用 GPU 加速识别图像中的文本

是否曾经需要一个真正能完成任务、无需无尽反复试验的 **c# ocr tutorial**？也许你正盯着一张高分辨率的发票，想要在几秒钟内 **extract text from invoice** 文件。好消息是，你不必重新发明轮子——Aspose.OCR 为你提供了干净的、GPU 加速的 API，帮你完成繁重的工作。

在本指南中，我们将逐步演示一个完整的、可运行的示例，展示如何 **recognize text from image** 文件、**convert image to text**，以及如何处理最常见的陷阱。完成后，你将拥有一个独立的程序，能够读取任何文档图片，从收据到扫描的合同，并输出干净、可搜索的文本。

## 你将学到

- 如何安装并引用 Aspose.OCR NuGet 包。
- 如何配置 OCR 引擎在 GPU 上运行，以实现飞快的性能。
- 使用 `OcrImage.FromFile` 正确 **load image for ocr** 的方法。
- 如何使用所需语言调用 `Recognize` 并获取结果。
- 处理多页 PDF、低对比度扫描以及错误处理的技巧。

不需要任何 Aspose 经验；只需一个可用的 .NET 开发环境（Visual Studio 2022 或 VS Code）和一块普通的 GPU（即使是集成的 Intel GPU 也能胜任）。

## 第一步 – 安装 Aspose.OCR 并准备项目

首先，你需要 Aspose.OCR 库。最简单的方式是通过 NuGet。

```bash
dotnet add package Aspose.OCR
```

> **技巧提示：** 如果你针对 .NET 6 或更高版本，包会自动拉取 Windows、Linux 和 macOS 的本机 GPU 二进制文件。无需额外复制 DLL。

添加包后，打开你的项目文件（`*.csproj`）并确认引用：

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.12.0" />
</ItemGroup>
```

现在你已经拥有开始编码所需的一切。

## 第二步 – 创建 GPU 加速的 OCR 引擎（c# ocr tutorial）

**c# ocr tutorial** 的核心是 `OcrEngine`。通过将 `Engine = Engine.Gpu` 设置为 GPU，我们告诉 Aspose 使用显卡而非 CPU。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine with GPU acceleration.
            var ocrEngine = new OcrEngine
            {
                Engine = Engine.Gpu // GPU acceleration is selected; the library auto‑detects the device.
            };

            // The rest of the steps are broken out into separate methods for clarity.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            PerformOcr(ocrEngine, imagePath);
        }
    }
}
```

> **为什么使用 GPU？** GPU 能并行处理成千上万的像素，将大尺寸、高 DPI 图像的 OCR 时间从秒级缩短到毫秒级。

## 第三步 – 加载图像进行 OCR（load image for ocr）

正确加载图像比你想象的更重要。`OcrImage.FromFile` 支持 PNG、JPEG、BMP、TIFF，甚至 PDF 页面。它还会读取图像的 DPI，这会影响识别准确度。

```csharp
static void PerformOcr(OcrEngine engine, string filePath)
{
    // Step 3: Load the image you want to recognize.
    // The FromFile method automatically detects the format.
    var image = OcrImage.FromFile(filePath);

    // Optional: Pre‑process the image for better results.
    // For example, you can increase contrast or convert to grayscale.
    image = ImagePreprocessor.AdjustContrast(image, 1.2);
    image = ImagePreprocessor.ConvertToGrayscale(image);
    
    // Continue to recognition...
    RecognizeAndDisplay(engine, image);
}
```

**注意：** 如果处理的是 PDF，你可以将每页提取为 `OcrImage` 并逐个喂入。

## 第四步 – 从图像识别文本（recognize text from image）

现在魔法开始了。我们让引擎识别英文文本，但你可以传入 Aspose 支持的任何语言（西班牙语、德语、中文等）。

```csharp
static void RecognizeAndDisplay(OcrEngine engine, OcrImage image)
{
    // Step 4: Perform OCR on the image using the desired language.
    var result = engine.Recognize(image, Language.English);

    // Step 5: Output the recognized text.
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(result.Text);
}
```

`result.Text` 属性包含纯文本字符串。如果需要每个单词的置信度分数，可以检查 `result.Regions`。

### 预期输出

```
=== OCR RESULT ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,234.56
Thank you for your business!
```

如果图像模糊，你可能会看到乱码——这时第 3 步的预处理就派上用场了。

## 第五步 – 从发票中提取文本 – 实际案例

假设你有一个装满扫描发票的文件夹，想要提取总金额。下面是对前面代码的快速扩展，使用了一个简单的正则表达式。

```csharp
using System.Text.RegularExpressions;

static void ExtractTotalAmount(string ocrText)
{
    // Look for a pattern like "$1,234.56"
    var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
    if (match.Success)
        Console.WriteLine($"Detected total: {match.Value}");
    else
        Console.WriteLine("Total amount not found.");
}
```

在打印 OCR 结果后，你可以调用 `ExtractTotalAmount(result.Text);`。这展示了一旦拥有原始字符串，**extract text from invoice** 文件是多么容易。

## 第六步 – 批量将图像转换为文本（convert image to text）

处理单个文件适用于演示，但生产代码通常需要处理数十甚至数百张图像。下面是一个简洁的循环，用于处理整个目录：

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    foreach (var file in Directory.EnumerateFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly)
                                 .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
    {
        Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
        var img = OcrImage.FromFile(file);
        var res = engine.Recognize(img, Language.English);
        Console.WriteLine(res.Text);
        ExtractTotalAmount(res.Text); // optional invoice extraction
    }
}
```

运行 `ProcessFolder(ocrEngine, @"C:\Invoices")` 将对文件夹中每个受支持的文件 **convert image to text**，并利用 GPU 加速。

## 边缘情况和常见陷阱

| 情况 | 产生原因 | 快速修复 |
|-----------|----------------|-----------|
| **低对比度扫描** | OCR 难以区分前景和背景。 | 提高对比度（`ImagePreprocessor.AdjustContrast`）或使用自适应阈值。 |
| **多页 PDF** | `OcrImage.FromFile` 只读取第一页。 | 使用 `PdfDocument` 将每页提取为 `OcrImage` 并循环。 |
| **不支持的语言** | 默认语言设置为英文。 | 传入 `Language.Spanish` 或任何受支持的枚举值。 |
| **未检测到 GPU** | 缺少本机二进制文件或驱动程序过旧。 | 确认 GPU 驱动是最新的；使用 `-runtime` 标志重新安装 NuGet 包。 |
| **大图像内存不足** | GPU 内存有限。 | 缩小图像尺寸（`image = ImagePreprocessor.Resize(image, 2000, 0)`）。 |

提前解决这些问题可以为你节省大量调试时间。

## 完整可运行示例

下面是完整的程序，你可以复制粘贴到新的控制台应用中。它包含了上面讨论的所有辅助方法。

```csharp
using System;
using System.IO;
using System.Linq;
using System.Text.RegularExpressions;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize GPU‑accelerated OCR engine.
            var ocrEngine = new OcrEngine { Engine = Engine.Gpu };

            // 2️⃣ Define the path to a single image or a folder.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            // string folderPath = @"C:\Invoices";

            // Uncomment one of the following lines:
            PerformOcr(ocrEngine, imagePath);
            // ProcessFolder(ocrEngine, folderPath);
        }

        // -------------------------------------------------
        // Load image, preprocess, recognize, and display.
        // -------------------------------------------------
        static void PerformOcr(OcrEngine engine, string filePath)
        {
            var image = OcrImage.FromFile(filePath);
            image = ImagePreprocessor.AdjustContrast(image, 1.2);
            image = ImagePreprocessor.ConvertToGrayscale(image);

            var result = engine.Recognize(image, Language.English);
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);

            ExtractTotalAmount(result.Text);
        }

        // -------------------------------------------------
        // Bulk processing of a folder.
        // -------------------------------------------------
        static void ProcessFolder(OcrEngine engine, string folderPath)
        {
            foreach (var file in Directory.EnumerateFiles(folderPath, "*.*")
                                          .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
            {
                Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
                var img = OcrImage.FromFile(file);
                var res = engine.Recognize(img, Language.English);
                Console.WriteLine(res.Text);
                ExtractTotalAmount(res.Text);
            }
        }

        // -------------------------------------------------
        // Simple regex to pull the total amount from an invoice.
        // -------------------------------------------------
        static void ExtractTotalAmount(string ocrText)
        {
            var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
            if (match.Success)
                Console.WriteLine($"Detected total: {match.Value}");
            else
                Console.WriteLine("Total amount not found.");
        }
    }
}
```

**Run it** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}