---
category: general
date: 2026-09-22
description: 使用 Aspose.OCR 在 C# 中从图像提取文本。了解如何将图像转换为文本、加载图像进行 OCR，并高效识别西里尔文文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for OCR
- recognize text image
- recognize Cyrillic text
language: zh
lastmod: 2026-09-22
og_description: 使用 Aspose.OCR 在 C# 中提取图像文本。本教程展示了如何将图像转换为文本、加载图像进行 OCR，以及仅用几行代码识别西里尔文文本。
og_image_alt: Diagram showing extract text from image workflow using Aspose.OCR
og_title: 使用 Aspose.OCR 从图像提取文本 – 步骤详解 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Extract text from image with Aspose.OCR in C#. Learn how to convert
    image to text, load image for OCR, and recognize Cyrillic text efficiently.
  headline: How to extract text from image using Aspose.OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose.OCR in C#. Learn how to convert
    image to text, load image for OCR, and recognize Cyrillic text efficiently.
  name: How to extract text from image using Aspose.OCR in C#
  steps:
  - name: Install the Aspose.OCR package
    text: 'Open a terminal in your solution folder and run:'
  - name: Create the OCR engine instance
    text: '```csharp using Aspose.OCR; using System.Drawing; // Required for Image
      handling'
  - name: Choose the language to recognize
    text: '```csharp // Step 3: Select Cyrillic as the target language engine.Language
      = OcrLanguage.Cyrillic; ```'
  - name: Load image for OCR
    text: '```csharp // Step 4: Load the image that contains the text engine.Image
      = Image.FromFile(@"YOUR_DIRECTORY\sample_cyrillic.png"); ```'
  - name: Perform the recognition and get the result
    text: '```csharp // Step 5: Run the recognition process string recognizedText
      = engine.Recognize(); ```'
  - name: Output the extracted text
    text: '```csharp // Step 6: Display the extracted text Console.WriteLine("Recognized
      text:"); Console.WriteLine(recognizedText); ```'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image processing
title: 如何在 C# 中使用 Aspose.OCR 从图像提取文本
url: /zh/net/text-recognition/how-to-extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.OCR 在 C# 中从图像提取文本

如果您需要在 .NET 应用程序中**从图像提取文本**，本指南将带您完成一个完整、可直接运行的解决方案。您将看到如何**将图像转换为文本**、加载图像进行 OCR，以及在无需额外配置的情况下处理西里尔字符。

本教程涵盖您所需的全部内容：必需的 NuGet 包、完整的代码示例、每一步的说明以及常见陷阱的提示。完成后，您只需将几行代码粘贴到项目中，即可立即开始识别文本。

## 您需要的准备

- .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Framework 4.7+）
- Visual Studio 2022 或任何支持 C# 的 IDE
- 在项目中安装 Aspose.OCR NuGet 包（`Aspose.OCR`）
- 包含西里尔文本的示例图像（例如 `sample_cyrillic.png`）

> **小贴士：** 第一次请求未捆绑的语言时，Aspose.OCR 会自动下载所需模块。此行为实现了无缝的**识别西里尔文本**。

## 使用 Aspose.OCR 从图像提取文本

该解决方案的核心是创建 `OcrEngine`、配置语言、加载图像并调用 `Recognize()`。以下章节将逐步拆解每一步。

### 步骤 1：安装 Aspose.OCR 包

在解决方案文件夹中打开终端并运行：

```bash
dotnet add package Aspose.OCR
```

该命令会将最新的稳定版 Aspose.OCR 添加到项目文件中，确保运行时可用 OCR 引擎和语言模块。

### 步骤 2：创建 OCR 引擎实例

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image handling

// ...

// Step 2: Initialize the OCR engine
OcrEngine engine = new OcrEngine();
```

`OcrEngine` 是所有 OCR 操作的入口。实例化它会分配图像分析所需的内部资源。

### 步骤 3：选择要识别的语言

```csharp
// Step 3: Select Cyrillic as the target language
engine.Language = OcrLanguage.Cyrillic;
```

设置 `engine.Language` 告诉 Aspose.OCR 要查找的字符集。**识别西里尔文本** 会在机器上未存在相应语言包时自动下载西里尔语言包。

### 步骤 4：加载用于 OCR 的图像

```csharp
// Step 4: Load the image that contains the text
engine.Image = Image.FromFile(@"YOUR_DIRECTORY\sample_cyrillic.png");
```

此行使用 `System.Drawing.Image` **加载用于 OCR 的图像**。将 `YOUR_DIRECTORY` 替换为 PNG 或 JPEG 文件的实际路径。引擎现在持有待分析的位图。

### 步骤 5：执行识别并获取结果

```csharp
// Step 5: Run the recognition process
string recognizedText = engine.Recognize();
```

`Recognize()` 会扫描位图，应用特定语言模型，并返回提取的字符串。如果图像清晰且语言设置正确，方法将返回高精度的结果。

### 步骤 6：输出提取的文本

```csharp
// Step 6: Display the extracted text
Console.WriteLine("Recognized text:");
Console.WriteLine(recognizedText);
```

将结果打印到控制台可以验证**从图像提取文本**是否如预期工作。您也可以将文本写入文件、数据库，或传递给其他服务。

## 完整、可运行的示例

下面是一个包含上述所有步骤的独立程序。将代码复制到新建的控制台项目（`dotnet new console`）中并运行。

```csharp
using System;
using System.Drawing;          // Provides Image class
using Aspose.OCR;              // Aspose OCR namespace

namespace ImageToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            OcrEngine engine = new OcrEngine();

            // Select the language – Cyrillic triggers module download if needed
            engine.Language = OcrLanguage.Cyrillic;

            // Load the image file (adjust the path to your environment)
            string imagePath = @"YOUR_DIRECTORY\sample_cyrillic.png";
            engine.Image = Image.FromFile(imagePath);

            // Perform recognition
            string recognizedText = engine.Recognize();

            // Output the result
            Console.WriteLine("Recognized text:");
            Console.WriteLine(recognizedText);
        }
    }
}
```

**预期输出**

```
Recognized text:
Пример текста на кириллице
```

如果示例图像包含短语 “Пример текста на кириллице”，控制台将如示例所示准确显示。字体、大小或噪声的变化可能影响准确性，但 Aspose.OCR 的内置预处理能够处理大多数常见情况。

## 处理常见边缘情况

| 场景 | 处理方法 | 重要性说明 |
|------|----------|------------|
| 未找到图像 | 将 `Image.FromFile` 包裹在 `try / catch (FileNotFoundException)` 块中，并显示友好提示。 | 防止应用程序崩溃并帮助用户定位正确的文件。 |
| 低对比度图像 | 将 `engine.ImagePreprocessingOptions` 设置为 `ImagePreprocessingOptions.Auto`，或在识别前手动调整亮度/对比度。 | 在源图像较暗时提升 OCR 准确度。 |
| 需要识别多种语言 | 将 `engine.Language = OcrLanguage.Multilingual;`，并可选地添加 `engine.AdditionalLanguages.Add(OcrLanguage.English);`。 | 能够检测混合脚本文档（例如西里尔文与拉丁文混合）。 |
| 大量图像批处理 | 复用单个 `OcrEngine` 实例，在循环中调用 `engine.Recognize()`。处理完后释放引擎。 | 减少内存分配并加快处理速度。 |

## 可靠 OCR 的最佳实践

- **使用无损图像格式**（PNG 或 TIFF），尽可能避免使用 JPEG，因为 JPEG 压缩会产生干扰识别器的伪影。
- **保持图像分辨率** 在 300 dpi 或更高（针对印刷文本）；分辨率过低可能导致小字符缺失。
- **在加载图像前裁剪不必要的边框**；多余的空白会增加处理时间而无实际价值。
- **验证输出**，检查空字符串或异常字符，尤其是在处理带噪声的扫描文档时。

## 后续步骤

既然您已经能够**从图像提取文本**，可以考虑扩展此方案：

- **批量将图像转换为文本**：读取图像目录，对每个文件进行处理，并将结果写入 CSV 文件。
- **集成云存储**：从 Azure Blob Storage 或 Amazon S3 拉取图像，运行 OCR，并将提取的文本存回云端。
- **结合翻译 API**：在识别西里尔文本后，调用 Azure Translator 或 Google Cloud Translation 生成英文输出。
- **探索高级版面分析**：Aspose.OCR 提供 `OcrPage` 对象，可获取文本坐标，适用于重新生成 PDF 或可搜索文档。

通过本教程的步骤，您已经为任何需要**将图像转换为文本**或在多语言环境下**识别图像文本**的项目奠定了坚实基础。

---

## 接下来该学习什么？

以下教程涵盖与本指南技术密切相关的主题，帮助您进一步学习。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [如何使用 Aspose.OCR for .NET 提取图像文本](/ocr/english/net/text-recognition/get-recognition-result/)
- [使用 Aspose.OCR 提取图像文本并选择语言的 C# 示例](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [使用 Aspose OCR 提取图像文本 – C# 快速入门](/ocr/english/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-quickstart/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}