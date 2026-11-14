---
category: general
date: 2026-11-14
description: 学习如何使用 Aspose OCR 在 C# 中实现图像转文本。本分步指南还涵盖了如何从 JPG 中提取文本并高效地将图像转换为文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize image to text
- extract text from jpg
- perform OCR on image
- convert image to text
- recognize text from image
language: zh
lastmod: 2026-11-14
og_description: 使用 Aspose OCR 在 C# 中将图像识别为文本。请按照本完整教程从 JPG 中提取文本，对图像执行 OCR，并将图像转换为文本。
og_image_alt: Screenshot of C# code that recognize image to text using Aspose OCR
og_title: 使用 Aspose OCR 将图像识别为文本 – C# 指南
schemas:
- author: Aspose
  dateModified: '2026-11-14'
  description: Learn how to recognize image to text using Aspose OCR in C#. This step‑by‑step
    guide also covers how to extract text from jpg and convert image to text efficiently.
  headline: How to recognize image to text with Aspose OCR in C#
  type: TechArticle
- description: Learn how to recognize image to text using Aspose OCR in C#. This step‑by‑step
    guide also covers how to extract text from jpg and convert image to text efficiently.
  name: How to recognize image to text with Aspose OCR in C#
  steps:
  - name: Large images
    text: Large files increase memory usage and processing time. Resize the image
      to a maximum of 2000 px on the longest side before calling `RecognizeImage`.
  - name: Missing language model
    text: If the required language pack cannot be downloaded (e.g., offline environment),
      the engine throws `IOException`. Wrap the call in a try‑catch block and provide
      a fallback language.
  - name: Asynchronous processing
    text: For UI applications, avoid blocking the UI thread. Wrap the recognition
      call in `Task.Run`.
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中使用 Aspose OCR 将图像识别为文本
url: /zh/net/text-recognition/how-to-recognize-image-to-text-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR 在 C# 中实现图像转文本

如果您需要在 .NET 应用程序中实现图像转文本，本指南将展示所需的完整步骤。您将看到如何从 jpg 文件中提取文本、对图像数据执行 OCR，以及使用最少代码将图像转换为文本。

本教程涵盖了从安装 Aspose.OCR NuGet 包到安全处理 OCR 结果的全部内容。无需外部服务，代码可在 .NET 6 或更高版本上运行。

## 安装 Aspose OCR 包

在编写任何代码之前，先将 Aspose.OCR 库添加到项目中。该包包含所有语言模型，并在运行时自动下载所需文件。

```bash
dotnet add package Aspose.OCR
```

该命令会将最新的稳定版 **Aspose.OCR** 添加到您的 `csproj` 中。此步骤确保您可以直接调用 `OcrEngine`，无需手动管理 DLL。

## 创建并配置 OCR 引擎

创建 OCR 引擎是您必须执行的第一步操作。引擎负责图像加载、语言选择和识别。

```csharp
using Aspose.OCR;

// Step 1: Instantiate the OCR engine (required modules are downloaded automatically)
OcrEngine ocrEngine = new OcrEngine();
```

`OcrEngine` 是执行核心工作负载的类。实例化它会触发轻量级初始化；库仅在您选择语言时才下载相应的语言包。

## 选择语言模型（从 jpg 中提取文本）

选择正确的语言模型会影响识别准确度。对于西里尔文文本，使用 `OcrLanguage.Cyrillic`。第一次设置本地未缓存的语言时，Aspose 会在后台下载模型。

```csharp
// Step 2: Choose the language model – triggers download if needed
ocrEngine.Language = OcrLanguage.Cyrillic;
```

如果处理拉丁文字，可将 `Cyrillic` 替换为 `English` 或其他枚举值。无论使用何种语言，代码路径都是 **perform OCR on image**。

## 从 JPG 文件识别文本（将图像转换为文本）

现在可以将图像文件传递给引擎。`RecognizeImage` 方法接受文件路径、流或 `Bitmap`。这里使用 JPEG，因为它是扫描文档的常见格式。

```csharp
// Step 3: Recognize text from the image file
OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/cyrillic-sample.jpg");
```

该方法返回一个 `OcrResult` 对象，其中包含原始字符串、置信度分数以及可选的布局信息。此调用在一行代码中实现 **recognize text from image**。

## 显示 OCR 结果（从 jpg 中提取文本）

识别完成后，将检测到的文本输出到控制台或传递给其他组件。

```csharp
// Step 4: Display the recognized text
Console.WriteLine(ocrResult.Text);
```

典型的控制台输出如下：

```
Пример текста на кириллице
```

如果图像中没有可识别的字符，`ocrResult.Text` 将为空字符串。务必在后续处理前检查此情况。

## 处理常见边缘情况

### 大图像

大文件会增加内存使用和处理时间。调用 `RecognizeImage` 前，请将图像最长边缩放至不超过 2000 px。

```csharp
using System.Drawing;

// Load, resize, then recognize
using (Bitmap original = new Bitmap("YOUR_DIRECTORY/large-sample.jpg"))
{
    int maxDim = 2000;
    int width = original.Width;
    int height = original.Height;

    if (width > maxDim || height > maxDim)
    {
        float scale = Math.Min((float)maxDim / width, (float)maxDim / height);
        int newWidth = (int)(width * scale);
        int newHeight = (int)(height * scale);
        using (Bitmap resized = new Bitmap(original, newWidth, newHeight))
        {
            OcrResult result = ocrEngine.RecognizeImage(resized);
            Console.WriteLine(result.Text);
        }
    }
    else
    {
        OcrResult result = ocrEngine.RecognizeImage(original);
        Console.WriteLine(result.Text);
    }
}
```

### 缺少语言模型

如果无法下载所需语言包（例如离线环境），引擎会抛出 `IOException`。请使用 try‑catch 包裹调用，并提供备用语言。

```csharp
try
{
    ocrEngine.Language = OcrLanguage.Cyrillic;
    OcrResult result = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(result.Text);
}
catch (IOException ex)
{
    Console.WriteLine($"Language model download failed: {ex.Message}");
    // Fallback to English
    ocrEngine.Language = OcrLanguage.English;
    OcrResult fallback = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(fallback.Text);
}
```

### 异步处理

对于 UI 应用程序，避免阻塞 UI 线程。将识别调用包装在 `Task.Run` 中。

```csharp
await Task.Run(() =>
{
    OcrResult asyncResult = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(asyncResult.Text);
});
```

## 实用技巧，提升 OCR 可靠性

- **预处理图像**：对光照不佳的图像执行灰度转换和对比度增强，可在 **perform OCR on image** 时提高准确率。
- **选择正确语言**：在识别前务必设置 `ocrEngine.Language`。默认是 English，对西里尔文或亚洲文字的准确度会很低。
- **验证输出**：使用正则表达式检查识别文本是否符合预期模式（如日期、ID），再进行存储。
- **缓存语言包**：首次下载可能需要数秒。如需即时启动，可将所需语言包随应用一起部署。

## 完整示例

下面是一个独立程序，演示了从包安装到显示 OCR 结果的完整工作流。

```csharp
// -----------------------------------------------------------
// Recognize image to text with Aspose OCR – complete example
// -----------------------------------------------------------
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1. Create the OCR engine (modules are downloaded automatically)
        OcrEngine ocrEngine = new OcrEngine();

        // 2. Select the language model – triggers download if missing
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 3. Recognize text from a JPG file (convert image to text)
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/cyrillic-sample.jpg");

        // 4. Output the recognized string (extract text from jpg)
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**预期的控制台输出**

```
Recognized text:
Пример текста на кириллице
```

在不同图像上运行该程序（例如英文发票）只需更改 `Language` 枚举和文件路径。相同代码即可 **recognize text from image**，无需修改。

## 结论

现在您已经掌握了如何在 C# 中使用 Aspose OCR 实现图像转文本。教程涵盖了库的安装、OCR 引擎的创建与配置、图像转文本以及常见边缘情况的处理。基于此，您可以 **extract text from jpg**、**perform OCR on image** 任意大小的数据，并将结果集成到更大的 .NET 工作流中。

接下来，可进一步探索以下高级功能：

- **多页 PDF OCR**（使用 `PdfInput` 替代 JPG）
- **自定义字符白名单**，提升数值代码的识别准确度
- 使用 `OcrEngine.Save` 将 OCR 结果保存为可搜索的 PDF

尝试不同的语言模型和图像预处理技术，以在您的特定领域获得最佳识别率。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您在项目中进一步使用 API 功能并探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [recognize text from image in C# – step‑by‑step Aspose OCR guide](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-step-by-step-aspose-ocr-guide/)
- [recognize text from image with Aspose OCR – Complete C# Async Guide](/ocr/english/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-async-g/)
- [recognize text from image in C# – Complete Aspose OCR Tutorial](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}