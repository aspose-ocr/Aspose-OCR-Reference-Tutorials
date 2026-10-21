---
category: general
date: 2026-10-21
description: 学习如何在 JPG 上执行 OCR，提取图像中的文本，并使用 Aspose.OCR 在 C# 中加载图像进行 OCR。完整的分步指南。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from jpg
- load image for OCR
- perform OCR on image
language: zh
lastmod: 2026-10-21
og_description: 如何在 C# 中使用 Aspose.OCR 对图像执行 OCR。请按照本指南加载图像进行 OCR，识别 JPG 中的文本并提取图像中的文字。
og_image_alt: Screenshot showing how to perform OCR on a Cyrillic image in C#
og_title: 如何在 C# 中对图像进行 OCR – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to perform OCR on a JPG, extract text from image and load
    image for OCR using Aspose.OCR in C#. Complete step‑by‑step guide.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
- Image processing
- Text extraction
title: 如何在 C# 中使用 Aspose.OCR 对图像进行 OCR
url: /zh/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.OCR 对图像进行 OCR

如果您需要**执行 OCR**，本教程为您提供一个完整、可直接运行的解决方案。您将学习如何加载用于 OCR 的图像、从 JPG 文件识别文本，以及使用 Aspose.OCR 库从图像中提取文本。

本指南涵盖了从安装 NuGet 包到处理语言模型并打印识别结果的全部步骤。完成后，您即可在任何 .NET 项目中集成 OCR，并在 IDE 中处理西里尔字母或其他语言的文本。

## 您需要的环境

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）
- Visual Studio 2022（或任何 C# 编辑器）
- 首次运行需要网络连接（Aspose.OCR 会自动下载语言模型）
- 示例图像，例如 `cyrillic_sample.jpg`，放置在代码可引用的文件夹中

## 步骤 1：安装 Aspose.OCR

打开 NuGet 包管理器并将 **Aspose.OCR** 添加到项目中：

```bash
dotnet add package Aspose.OCR
```

该包包含 OCR 引擎、语言模型以及图像处理所需的辅助类。无需额外的 DLL。

## 步骤 2：创建 OCR 引擎 – 如何执行 OCR

在 **执行 OCR** 的第一步是实例化引擎。该对象管理整个识别流水线。

```csharp
using Aspose.OCR;

// Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

`OcrEngine` 体积轻巧；您可以在多个图像之间复用同一实例，从而在批量处理时提升性能。

## 步骤 3：加载用于 OCR 的图像

在识别之前必须提供图像数据。**加载用于 OCR 的图像** 步骤支持多种格式，本示例聚焦于 JPEG 文件。

```csharp
// Load the image you want to process
engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

`OcrImage.FromFile` 将文件读取到内存并为引擎做好准备。如果文件路径无效，会抛出 `ArgumentException`，请确保路径正确。

## 步骤 4：选择合适的语言（可选但推荐）

如果图像中包含西里尔字符，请将语言设置为 `Cyrillic`。所需模型将在首次运行时自动下载。

```csharp
// Choose the language model
engine.Language = OcrLanguage.Cyrillic;
```

您可以通过更改此属性切换到其他语言（例如 `OcrLanguage.English`）。该库支持超过 60 种语言。

## 步骤 5：从 JPG 识别文本 – 如何在 JPEG 上执行 OCR

现在调用 `Recognize` 方法。这是 **执行 OCR** 的核心，它将位图转换为 Unicode 文本。

```csharp
// Perform the recognition
engine.Recognize();
```

该方法会阻塞直至 OCR 过程完成。对于大图像，建议在后台线程中运行，以保持 UI 响应。

## 步骤 6：从图像中提取文本

识别完成后，引擎会将结果存储在 `Text` 属性中。这标志着 **从图像中提取文本** 步骤已完成。

```csharp
// Retrieve the extracted text
string extractedText = engine.Text;

// Output the recognized text to the console
Console.WriteLine(extractedText);
```

输出将包含图中找到的精确字符，保留换行和标点。

## 完整、可运行的示例

将所有步骤组合在一起，即可得到一个可以复制、粘贴并直接运行的程序：

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image for OCR
        engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");

        // Step 3: Choose the language model (Cyrillic in this case)
        engine.Language = OcrLanguage.Cyrillic;

        // Step 4: Perform OCR on the image
        engine.Recognize();

        // Step 5: Extract text from image
        string extractedText = engine.Text;

        // Step 6: Output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

### 预期输出

如果 `cyrillic_sample.jpg` 包含短语 “Привет мир”（Hello world），控制台将显示：

```
=== OCR Result ===
Привет мир
```

不同的字体或图像质量可能影响准确率，但 Aspose.OCR 在清晰印刷品上通常能实现 >95 % 的识别率。

## 常见陷阱与实用技巧

- **图像质量很重要** – 低分辨率或噪声较大的 JPEG 会降低准确率。必要时使用 `engine.Image.AdjustContrast()` 对图像进行预处理（例如提升对比度）。
- **语言模型下载** – 第一次执行时模型会下载到 `%USERPROFILE%\.Aspose\OCR`。请确保进程拥有写入权限。
- **批量处理** – 复用同一 `OcrEngine` 实例，仅在文件之间更换 `engine.Image`，可避免重复加载模型。
- **内存使用** – 大图像会占用更多 RAM。若在循环中处理大量文件，识别后调用 `engine.Image.Dispose()` 释放资源。
- **线程安全** – `OcrEngine` 不是线程安全的。并行时请为每个线程创建独立实例。

## 结论

您现在已经掌握了使用 Aspose.OCR 在 C# 中对 JPEG **执行 OCR**、**加载用于 OCR 的图像**以及**从图像中提取文本**的完整流程。完整示例演示了语言设置、从 JPG 识别文本并打印结果，为任何文本提取项目奠定了坚实基础。

接下来，您可以探索诸如 **批量对图像执行 OCR**、将 OCR 与 ASP.NET Core API 集成，或将提取的文本转换为可搜索的 PDF 等相关主题。尝试不同语言和图像预处理方法，以最大化识别质量。

## 您接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您在已有技巧的基础上进一步提升。每篇资源都提供完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [如何在 C# 中执行 OCR – 使用 Aspose OCR 将图像转换为文本](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-text-with-aspose-oc/)
- [如何在 C# 中执行 OCR – 从图像识别文本](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/)
- [如何使用 Aspose.OCR for .NET 从图像中提取文本](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}