---
category: general
date: 2026-11-26
description: 学习如何对 PNG 文件进行 OCR 识别，将 PNG 转换为文本，并使用 Aspose.OCR 提取西里尔文文本——面向开发者的逐步指南。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: zh
lastmod: 2026-11-26
og_description: 如何使用 Aspose.OCR 在 C# 中对 PNG 文件进行 OCR 并提取西里尔文字。请遵循本完整教程将 PNG 转换为文本。
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: 使用 Aspose.OCR 对 PNG 图像进行 OCR – C# 指南
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: 如何在 C# 中使用 Aspose.OCR 对 PNG 图像进行 OCR
url: /zh/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.OCR 在 C# 中对 PNG 图像执行 OCR

如果您需要 **如何执行 OCR** 对 PNG 文件进行处理，本指南将向您展示使用 Aspose.OCR 将 PNG 转换为文本的完整步骤。无论是从扫描文档中提取西里尔文文本，还是仅仅识别 PNG 截图中的文字，解决方案开箱即用，只需几行 C# 代码即可实现。

在本教程中，您将学习如何：

* **load image for OCR** 从本地文件夹加载图像，
* 配置引擎以 **extract Cyrillic text**，
* **recognize text from PNG** 并获取干净的字符串，
* 处理常见问题，如缺少语言模块和大图像。

无需任何 Aspose.OCR 经验——只需一个 .NET 开发环境和一张您想要处理的 PNG 图像。

## 前提条件

在开始之前，请确保您拥有：

* 已安装 .NET 6.0（或更高版本）。
* 已获取 **Aspose.OCR for .NET** 的授权或试用版。您可以从 Aspose 官网免费获取试用版。
* Visual Studio 2022（或任何支持 .NET 的 IDE）。
* 包含您想要提取文本的 PNG 文件（示例使用 `sample_image.png`）。

## 第一步：安装 Aspose.OCR NuGet 包

在项目文件夹中打开终端并运行：

```bash
dotnet add package Aspose.OCR
```

该包包含核心 OCR 引擎以及所有语言模块。当您请求本地不存在的语言时，Aspose.OCR 会自动下载所需模块。

## 第二步：创建 OCR 引擎实例（how to perform OCR）

在任何 OCR 工作流中，第一步都是实例化引擎。该对象管理后续的所有操作，例如加载图像和执行识别。

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**为什么这很重要：** `OcrEngine` 类封装了 OCR 流程。创建单个实例并在多张图像之间复用，可降低内存开销并提升性能。

## 第三步：加载 OCR 图像 – 指定源 PNG 文件

加载图像的过程即是 **load image for OCR**。Aspose.OCR 支持多种输入类型，最直接的是 `ImageStream.FromFile`。

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **专业提示：** 使用绝对路径或 `Path.Combine`，可避免在不同环境下运行时出现错误。

### 处理大图像

如果 PNG 大小超过 2 MB，建议在识别前先进行下采样，以加快处理速度：

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## 第四步：配置语言 – 提取西里尔文文本

默认情况下，Aspose.OCR 假设使用英文。要 **extract Cyrillic text**，请将 `Language` 属性设置为 `Language.Cyrillic`。首次运行代码时，所需模块会自动下载。

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

如果需要识别多种语言（例如英文和西里尔文），可以将它们组合使用：

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### 边缘情况：缺少语言模块

如果下载失败（例如离线环境），引擎会抛出 `OcrException`。捕获该异常以提供优雅的回退方案：

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## 第五步：执行识别操作（recognize text from PNG）

现在图像和语言均已设置，您可以 **recognize text from PNG**。`Recognize` 方法同步运行 OCR 流程。

```csharp
// Run OCR
ocrEngine.Recognize();
```

**为什么它有效：** 在内部，Aspose.OCR 会先进行预处理（二值化、去噪），然后将图像送入针对所选语言调优的神经网络识别器。

## 第六步：检索并显示识别文本（convert PNG to text）

识别完成后，可通过 `Text` 属性获取提取的字符串。这就是 **convert PNG to text** 的最终步骤。

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### 预期输出

如果 `sample_image.png` 包含西里尔文短语 “Привет мир”，控制台将显示：

```
=== OCR Result ===
Привет мир
```

输出可能包含换行符和标点，完全按照图像中的呈现方式。必要时，您可以使用 `String.Trim()`、`Regex` 或其他文本清理工具对字符串进行后处理。

## 第七步：可选 – 将结果保存到文件

将 OCR 结果保存下来可供后续处理（例如索引、翻译）。以下示例演示如何将文本写入 UTF‑8 编码的文件：

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## 常见陷阱及如何避免

| 问题 | 症状 | 解决方案 |
|------|------|----------|
| **Missing language module** | 在 `Language = Language.Cyrillic` 时出现 `OcrException` | 确保首次运行时联网，或通过 Aspose 的离线包预先下载模块。 |
| **Blurry or low‑contrast image** | 准确率低，出现大量 “?” 字符 | 预处理图像：提升对比度、进行锐化，或在送入引擎前转换为灰度图。 |
| **Very large PNG** | 处理时间长，可能出现 `OutOfMemoryException` | 如第 3 步所示进行下采样，或将多页图像拆分为独立瓦片。 |
| **Non‑UTF‑8 characters** | 输出乱码 | 确认控制台或文件写入器使用 UTF‑8 编码（`Encoding.UTF8`）。 |

## 完整、可运行的示例

下面是整合上述所有步骤的完整程序。复制到新的控制台项目中，调整文件路径后即可运行。

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### 工作原理

1. **Engine creation** – 准备 OCR 流程。  
2. **Image loading** – 支持原始 PNG 与下采样版本，以提升性能。  
3. **Language selection** – 演示 **extract Cyrillic text** 并处理缺失模块的情况。  
4. **Recognition** – 核心的 **recognize text from PNG** 调用。  
5. **Result handling** – 展示 **convert PNG to text** 并将结果写入文件。

使用 `dotnet run` 运行程序。如果一切配置正确，您将在控制台看到识别后的文本，并保存至 `ocr_output.txt`。

## 结论

在本教程中，您学习了使用 Aspose.OCR for .NET 对 PNG 文件 **如何执行 OCR**，涵盖了从 **load image for OCR** 到 **extract Cyrillic text** 再到 **convert PNG to text** 的完整流程。完整的可运行示例展示了标准工作流、常见边缘情况以及保持 OCR 管道可靠的实用技巧。

**后续步骤**

* 探索通过组合 `Language` 标志，使用 **recognize text from PNG** 识别其他语言（阿拉伯语、中文）  
* 将 OCR 结果集成到 Azure Cognitive Search，实现可搜索的文档存档  
* 试验 Aspose.OCR 的 `OcrEngine` 设置，例如 `Resolution`

## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步说明。

- [如何下载 Aspose.OCR 模型并在 C# 中从 PNG 提取文本](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [如何在 C# 中执行 OCR – 使用 Aspose 识别西里尔文](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [如何在 C# 中批量 OCR – 快速提取 PNG 文件文本](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}