---
category: general
date: 2026-10-15
description: 使用 Aspose OCR 在 C# 中将 JPG 转换为文本。遵循此 C# OCR 示例，几行代码即可加载图像、读取文本并提取文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert jpg to text
- extract text image
- read text image
- c# ocr example
- load image ocr
language: zh
lastmod: 2026-10-15
og_description: 使用 Aspose OCR 在 C# 中将 JPG 转换为文本。此 C# OCR 示例展示了如何加载图像、读取文本图像并快速提取文本。
og_image_alt: Screenshot of a C# console app converting a JPG image to text using
  Aspose OCR
og_title: 在 C# 中将 JPG 转换为文本 – 完整的 Aspose OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-10-15'
  description: Convert JPG to text in C# using Aspose OCR. Follow this c# ocr example
    to load image, read text image, and extract text image in a few lines.
  headline: How to convert JPG to text in C# with Aspose OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何使用 Aspose OCR 在 C# 中将 JPG 转换为文本
url: /zh/net/text-recognition/how-to-convert-jpg-to-text-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose OCR 将 JPG 转换为文本

如果您需要**快速将 JPG 转换为文本**，本指南将一步步演示。教程结束后，您将拥有一个可运行的 C# OCR 示例，能够加载图像、读取图像文本并提取得到的字符串——只需几行代码。

将文档图片转换为可搜索文本是发票自动化、数据录入和无障碍项目中的常见需求。本教程涵盖了从安装 Aspose.OCR 包到处理语言模块以及排查常见问题的全部内容。

## 您需要的环境

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.6+）
- Visual Studio 2022 或任意支持 C# 的 IDE
- 首次运行时需要网络连接（Aspose OCR 会自动下载语言模块）
- 一张包含可识别字符的 JPG 示例文件（示例使用西里尔字母图像，任意语言均可）

## 第一步：安装 Aspose OCR 并创建控制台项目

1. 在终端或 Visual Studio 的 Package Manager Console 中打开。  
2. 运行以下命令以添加 Aspose.OCR NuGet 包：

```bash
dotnet add package Aspose.OCR
```

该包包含 `OcrEngine` 类以及进行**加载图像 OCR**操作所需的所有辅助类型。

## 第二步：转换 JPG 为文本 – 初始化 OCR 引擎

创建引擎是将 JPG 转换为文本的第一步。引擎负责图像分析和语言检测的繁重工作。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image loading
using System;

namespace JpgToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            OcrEngine engine = new OcrEngine();
```

**为什么重要：** `OcrEngine` 对象保存了语言、DPI 和图像来源等配置信息。一次实例化后在多张图像间复用，可降低内存开销。

## 第三步：加载要读取的图像（load image ocr）

引擎需要一个 `System.Drawing.Image` 实例。您可以从磁盘、流或字节数组加载任意 JPG 文件。

```csharp
            // Step 3: Load the JPG image
            string imagePath = @"YOUR_DIRECTORY/sample_image.jpg";
            engine.Image = Image.Load(imagePath);
```

**提示：** 若处理大批量文件，建议在 `using` 块中使用 `Image.FromFile` 加载图像，以便及时释放本机资源。

## 第四步：选择语言并执行 OCR（read text image）

Aspose OCR 支持 100 多种语言。如果所选语言在机器上不存在，库会自动下载所需模块。

```csharp
            // Step 4: Select language (optional but improves accuracy)
            engine.Language = OcrLanguage.English;   // Change to Cyrillic, Arabic, etc.
            
            // Perform the OCR operation
            engine.Recognize();
```

**为何要设置语言：** 指定正确的语言可降低误识别率并加快识别速度，尤其是字符集独特的脚本。

## 第五步：获取并显示提取的文本（extract text image）

识别完成后，识别得到的字符串可通过 `engine.Text` 访问。这就是**将 JPG 转换为文本**的核心结果。

```csharp
            // Step 5: Get the recognized text
            string recognizedText = engine.Text;

            // Step 6: Output the result
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

**预期输出**

```
=== OCR Result ===
The quick brown fox jumps over the lazy dog.
```

如果使用的是非英文样本，您将看到相应的字符。控制台输出确认图像已成功转换为纯文本。

## 完整 C# OCR 示例（c# ocr example）

下面是完整的、可直接复制到 `Program.cs` 的程序。除 NuGet 引用外，无需其他外部配置即可编译运行。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;
using System;

namespace JpgToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create the OCR engine
            OcrEngine engine = new OcrEngine();

            // Choose the language (optional)
            engine.Language = OcrLanguage.English; // Change as needed

            // Load the JPG image you want to convert
            string imagePath = @"YOUR_DIRECTORY/sample_image.jpg";
            engine.Image = Image.Load(imagePath);

            // Run the OCR process
            engine.Recognize();

            // Retrieve the recognized text
            string recognizedText = engine.Text;

            // Show the result
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

保存文件后，运行 `dotnet run`，即可在控制台看到提取的文本。此 **c# ocr example** 支持 `System.Drawing` 所支持的 JPG、PNG、BMP 或 TIFF 图像。

## 处理常见边缘情况

| 情况 | 建议 |
|-----------|----------------|
| **缺少语言模块** | 第一次调用 `engine.Recognize()` 时会自动下载所需文件。确保机器能上网，或手动从 Aspose 门户下载模块并放置在应用程序的执行文件夹中。 |
| **低分辨率图像** | 在识别前提升 DPI：`engine.Image = Image.Load(imagePath, new ImageLoadOptions { DpiX = 300, DpiY = 300 });`。更高的 DPI 为 OCR 引擎提供更多细节。 |
| **噪声背景** | 使用 `engine.PreprocessOptions` 进行二值化或去噪。例如：`engine.PreprocessOptions = new PreprocessOptions { BinarizationMethod = BinarizationMethod.Otsu };`。 |
| **大批量处理** | 在循环中复用单个 `OcrEngine` 实例并调用 `engine.Image = Image.Load(nextPath); engine.Recognize();`。使用后及时释放每个 `Image`，保持内存占用低。 |
| **非拉丁脚本** | 将 `engine.Language` 设置为相应脚本（如 `OcrLanguage.Cyrillic`、`OcrLanguage.Arabic`）。某些脚本需要的语言包会在首次使用时下载。 |

## 专业技巧：将 OCR 输出保存到文件

如果需要后续处理文本，可将其写入 `.txt` 文件：

```csharp
System.IO.File.WriteAllText(@"output.txt", recognizedText);
Console.WriteLine("Text saved to output.txt");
```

这一小改动即可将控制台演示转变为轻量级的提取工具。

## 结论

现在您已经掌握了如何在 C# 中使用 Aspose OCR **将 JPG 转换为文本**。本教程涵盖了安装包、加载图像、读取图像文本以及提取最终字符串的全过程，并提供了完整的 **c# ocr example**。有了这些知识，您可以将 OCR 集成到文档索引、数据录入自动化或无障碍工具等更大工作流中。

**后续步骤**

- 尝试其他语言（`engine.Language = OcrLanguage.Cyrillic;`），观察库对多语言文档的处理效果。  
- 使用简单的 `foreach` 循环处理文件夹中的多个文件。

## 接下来您应该学习什么？

以下教程与本指南紧密相关，帮助您进一步掌握 API 功能并探索项目中的其他实现方式，每篇都包含完整可运行的代码示例和逐步说明。

- [How to Perform OCR in C# – Extract Text from Image Using Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-with-aspose/)
- [Convert Image to Text in C# with Aspose OCR – Step‑by‑Step Guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}