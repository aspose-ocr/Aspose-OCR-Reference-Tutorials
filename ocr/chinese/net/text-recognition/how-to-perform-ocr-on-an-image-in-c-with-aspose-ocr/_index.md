---
category: general
date: 2026-10-18
description: 在 C# 中快速执行图像 OCR。学习如何从 JPG 提取文本，将图像转换为文字，并使用 Aspose.OCR 读取图像中的文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- convert image to text
- read text from image
- load image for OCR
language: zh
lastmod: 2026-10-18
og_description: 使用 Aspose.OCR 在 C# 中对图像执行 OCR。本教程展示了如何从 JPG 中提取文本、将图像转换为文字，并在几分钟内读取图像中的文字。
og_image_alt: Console output displaying recognized Cyrillic text after performing
  OCR on an image
og_title: 在 C# 中对图像进行 OCR – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Perform OCR on an image in C# quickly. Learn to extract text from JPG,
    convert image to text and read text from image using Aspose.OCR.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
title: 如何在 C# 中使用 Aspose.OCR 对图像进行 OCR
url: /zh/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.OCR 对图像执行 OCR

如果您需要在 .NET 应用程序中**对图像执行 OCR**，本指南提供了一个完整、可直接运行的解决方案。您将看到如何**加载用于 OCR 的图像**、识别西里尔字符，以及**从 JPG 文件中提取文本**，而无需编写任何底层图像处理代码。

在本教程中，您将：

* 安装 Aspose.OCR NuGet 包。  
* 加载图像文件（JPG、PNG、BMP 等）。  
* 运行 OCR 引擎以**将图像转换为文本**。  
* 在控制台中**读取图像中的文本**输出。  

这些步骤适用于任何 .NET 兼容的图像，因此您可以将其应用于 PDF、扫描收据或屏幕截图等。

## 前提条件

* .NET 6.0 SDK 或更高版本（代码也适用于 .NET Framework 4.7+）。  
* Visual Studio 2022 或您喜欢的任何 C# 编辑器。  
* 首次运行需要互联网访问——Aspose.OCR 会自动下载西里尔语言模块。  

> **小贴士：** 保持 NuGet 包为最新版本；更新的版本会提升识别准确性并添加语言包。

## 步骤 1：安装 Aspose.OCR

打开项目文件夹中的终端并运行：

```bash
dotnet add package Aspose.OCR
```

该包包含用于**对图像执行 OCR**的 `OcrEngine` 类。命令完成后，包引用会出现在您的 *.csproj* 文件中。

## 步骤 2：创建控制台程序框架

如果还没有控制台项目，请创建一个新项目：

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

用下一节中展示的代码替换生成的 *Program.cs*。该框架包含所需的 `using` 指令和驱动 OCR 过程的 `Main` 方法。

## 步骤 3：加载用于 OCR 的图像

第一行功能代码**加载要分析的图像**。Aspose.OCR 接受任何流，因此您可以从磁盘、网页 URL 或嵌入资源加载文件。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Step 3: Load the image containing Cyrillic text
        // Replace the path with the location of your JPG file.
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);
```

*为什么重要*：使用 `ImageStream.FromFile` 抽象了格式处理，确保 OCR 引擎无论原始文件类型如何都能收到一致的位图。得益于 `using` 语句，流也会自动释放。

## 步骤 4：初始化 OCR 引擎并设置语言（可选）

默认情况下，Aspose.OCR 会自动检测语言。对于西里尔文文本，您可以显式请求 `Language.Cyrillic` 模块，从而加快首次下载速度。

```csharp
        // Step 4: Initialize the OCR engine
        var engine = new OcrEngine();

        // Optional: force Cyrillic language to avoid auto‑detection overhead
        engine.Language = Language.Cyrillic;
```

如果省略语言设置，引擎将在您首次调用 `Recognize` 时下载所需模块。下载通过 HTTPS 进行，并在本地缓存，以供后续运行使用。

## 步骤 5：执行 OCR 并将图像转换为文本

现在您实际**对图像执行 OCR**并获得纯文本字符串。`Recognize` 方法完成所有繁重工作：预处理、布局分析和字符分类。

```csharp
        // Step 5: Perform OCR – convert image to text
        engine.Image = image;
        string recognizedText = engine.Recognize();
```

返回的 `recognizedText` 包含与原始布局匹配的换行符，便于后处理或存入数据库。

## 步骤 6：显示结果 – 从图像读取文本

最后，通过将结果写入控制台**从图像读取文本**。此步骤验证 OCR 是否成功，并准确显示提取的内容。

```csharp
        // Step 6: Display the recognized text – read text from image
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

运行程序（`dotnet run`）时，您应该会看到类似以下的输出：

```
=== OCR Result ===
Пример текста на кириллице
```

> **注意：** 精确输出取决于源 JPG 的质量。清晰的高分辨率图像可获得最佳效果。

## 完整、可运行的源代码

下面是完整的程序，您可以复制粘贴到 *Program.cs* 中并直接执行（除图像路径外无需其他修改）。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Load the image containing Cyrillic text
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);

        // Initialize the OCR engine
        var engine = new OcrEngine
        {
            // Force Cyrillic language; optional but speeds up first run
            Language = Language.Cyrillic,
            Image = image
        };

        // Recognize the text – this converts the image to text
        string recognizedText = engine.Recognize();

        // Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

运行程序会将提取的字符打印到控制台，证明您已成功**从 JPG 中提取文本**并**将图像转换为文本**。

## 处理常见变体

| Scenario | Adjustment |
|----------|------------|
| **不同语言** | 设置 `engine.Language = Language.English;` 或其他受支持的枚举。 |
| **多页 PDF** | 将每页转换为图像（例如使用 `Aspose.PDF`），并对每个图像调用 OCR 循环。 |
| **大批量** | 将 OCR 调用包装在 `Parallel.ForEach` 循环中；复用单个 `OcrEngine` 实例以降低内存开销。 |
| **低分辨率图像** | 在识别前使用 `engine.Image = ImageProcessing.Filters.GaussianBlur(image, 1.5);` 进行预处理，以降低噪声。 |

## 性能提示

* **缓存语言模块** – 首次下载可能需要几秒钟；后续运行几乎是瞬时的。 |
* **复用 `OcrEngine`** 实例以处理多张图像，避免重复初始化开销。 |
* **限制图像尺寸** – 极大的照片会增加内存使用。将宽度最大限制为 2000 像素后再送入引擎。 |

## 结论

现在您已经了解如何使用 Aspose.OCR 在 C# 中**对图像文件执行 OCR**。通过加载图像、配置引擎并调用 `Recognize`，您可以仅用几行代码就**从 JPG 中提取文本**、**将图像转换为文本**以及**从图像读取文本**。

从这里您可以进一步探索：

* 将 OCR 结果存储在数据库中，以实现可搜索的档案。  
* 将工作流集成到接受上传图像的 Web API 中。  
* 使用其他语言模块（阿拉伯语、印地语等），扩大应用的覆盖范围。  

欢迎尝试不同的图像格式、语言和批处理策略。核心模式——**加载用于 OCR 的图像 → 识别 → 处理纯文本输出**——保持不变，为任何文本提取项目提供坚实基础。

## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您在自己的项目中掌握更多 API 功能并探索替代实现方式。每个资源都包含完整的可运行代码示例和逐步解释。

- [使用 Aspose.OCR 进行语言选择的 C# 图像文本提取](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [将图像转换为文本 – 从 URL 对图像执行 OCR](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [如何使用 Aspose.OCR for .NET 从图像提取文本](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}