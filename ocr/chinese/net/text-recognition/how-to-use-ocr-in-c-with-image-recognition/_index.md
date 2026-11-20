---
category: general
date: 2026-11-20
description: 如何在 C# 中使用 OCR 识别图像中的文字。学习加载图像 OCR、设置 OCR 语言以及从 JPEG 文件中提取文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text image
- load image OCR
- recognize text JPEG
- set OCR language
language: zh
lastmod: 2026-11-20
og_description: 如何在 C# 中使用 OCR 从图像中提取文本。本指南展示了加载图像、设置 OCR 语言以及从 JPEG 文件中识别文本。
og_image_alt: Screenshot of C# code demonstrating how to use OCR to recognize text
  from an image
og_title: 如何在 C# 中使用 OCR – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to use OCR in C# to recognize text from an image. Learn to load
    image OCR, set OCR language, and extract text from JPEG files.
  headline: How to use OCR in C# with image recognition
  type: TechArticle
tags:
- OCR
- C#
- Image processing
- Text extraction
title: 如何在 C# 中使用 OCR 进行图像识别
url: /zh/net/text-recognition/how-to-use-ocr-in-c-with-image-recognition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中使用 OCR 进行图像识别的方式

如果您需要在 C# 应用程序中 **how to use OCR**，本指南将带您完整了解整个过程。无论是数字化扫描的合同还是从照片中提取信息，您都将学习如何快速且可靠地 **recognize text image** 文件。

本教程涵盖加载图像、配置 OCR 引擎以及从 JPEG 文件检索识别文本的过程。完成后，您将拥有一个自包含、可运行的示例，能够直接放入任何 .NET 项目中。

## 前提条件

在开始之前，请确保您具备：

* 已安装 .NET 6.0（或更高版本）。
* 可访问提供 `OcrEngine`、`ImageStream` 和语言模块的 OCR 库（例如 **Leadtools**、**Aspose.OCR** 或任何兼容的包）。
* 在已知目录中有一个名为 `sample.jpg` 的示例图像。

无需额外的外部服务——OCR 引擎会自动下载缺失的语言包。

## 步骤 1：加载用于 OCR 的图像

加载图像是任何 OCR 工作流的第一步。下面的代码从磁盘上的 JPEG 文件创建一个 `ImageStream`。

```csharp
// Step 1: Load the image to be recognized
var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
var image = ImageStream.FromFile(imagePath);
```

*为什么重要：* `ImageStream` 对象抽象了文件处理并提供 OCR 引擎使用的像素数据。如果文件未找到，`FromFile` 会抛出明确的异常，使调试变得直接。

## 步骤 2：创建 OCR 引擎实例（自动释放）

使用 `using` 块可确保在 OCR 工作完成后立即释放非托管资源。

```csharp
// Step 2: Create an OCR engine instance (automatically disposes when done)
using var ocrEngine = new OcrEngine();
```

*专业提示：* 与手动调用 `Dispose()` 相比，`using` 语句更受推荐，因为它消除了忘记释放本机内存的风险，后者可能导致长期运行服务的内存泄漏。

## 步骤 3：设置 OCR 语言（可选但推荐）

如果您知道源文档的语言，设置语言可以提升准确率并加快处理速度。示例将语言设置为 Cyrillic；您可以将其替换为任何受支持的语言枚举。

```csharp
// Step 3 (optional): Specify the language module, e.g., Cyrillic
// The required language pack will be downloaded automatically if missing
ocrEngine.Language = OcrLanguage.Cyrillic;
```

*为什么要设置语言？* OCR 引擎包含特定语言的字符模型。选择正确的模型可减少误报并避免不必要的字符替换。

## 步骤 4：对已加载的图像执行 OCR

现在引擎处理位图并将识别的文本作为字符串返回。

```csharp
// Step 4: Perform OCR on the loaded image
string recognizedText = ocrEngine.Recognize(image);
```

*边缘情况：* 如果图像分辨率低或压缩严重，引擎可能只返回部分结果。考虑进行预处理（例如二值化）以获得更好效果。

## 步骤 5：输出识别的文本

最后，在控制台显示提取的文本或将其转发给其他组件。

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

**预期输出**

```
=== Recognized Text ===
Пример текста, полученного из изображения.
```

具体内容取决于源图像，但控制台会显示 OCR 引擎检测到的完整字符串。

## 完整、可运行的示例

将所有步骤组合在一起即可得到一个紧凑的程序，您可以立即编译并运行。

```csharp
using System;
using System.IO;

// Ensure you reference the OCR library that provides these types
// e.g., using Leadtools.OCR;

class Program
{
    static void Main()
    {
        // Load the image to be recognized
        var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
        var image = ImageStream.FromFile(imagePath);

        // Create an OCR engine instance (auto‑dispose)
        using var ocrEngine = new OcrEngine();

        // Optional: set the language (Cyrillic in this case)
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // Perform OCR
        string recognizedText = ocrEngine.Recognize(image);

        // Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

将代码复制到新的控制台项目中，将 `YOUR_DIRECTORY` 替换为图像所在路径，然后运行 `dotnet run`。程序将在控制台打印识别的文本。

## 常见问题与故障排除

| Question | Answer |
|----------|--------|
| **如果语言包未下载怎么办？** | OCR 库会自动尝试下载。请确保机器有互联网访问，或根据库的文档预先安装语言包。 |
| **我可以识别 PNG 或 BMP 文件中的文本吗？** | 可以。`ImageStream.FromFile` 支持底层图像库支持的任何格式。只需更改文件扩展名即可。 |
| **如何提升噪声扫描的准确性？** | 在传递给 `Recognize` 之前对图像进行预处理（对比度调整、噪声去除）。许多库提供 `ImageProcessor` 类用于此目的。 |
| **在用户上传的文件上运行 OCR 安全么？** | 验证文件大小和类型，并在沙箱环境中运行 OCR，以避免恶意负载。 |

## 结论

您现在已经了解如何在 C# 中 **how to use OCR** 来可靠地 **recognize text image** 文件、**load image OCR**、**set OCR language**，以及 **recognize text JPEG** 内容。完整示例展示了一个简洁、可释放的工作流，您可以在此基础上添加额外的预处理、多语言支持或集成到更大的文档处理流水线中。

### 下一步

* 通过遍历 JPEG 目录实现批处理。  
* 将 OCR 与自然语言处理（NLP）结合，以提取结构化数据。  
* 尝试其他语言模块，例如 `OcrLanguage.English` 或 `OcrLanguage.Arabic`。  

欢迎根据您的具体使用场景调整代码，祝编码愉快！

## 接下来应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方法。

- [在 C# 中使用 Windows.Media.Ocr 识别文本图像 – 完整 OCR 指南](/ocr/english/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/)
- [如何在 C# 中使用 OCR – 异步提取图像文本](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-asynchronously/)
- [如何在 C# 中使用 OCR – 使用 Aspose OCR 提取图像文本](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}