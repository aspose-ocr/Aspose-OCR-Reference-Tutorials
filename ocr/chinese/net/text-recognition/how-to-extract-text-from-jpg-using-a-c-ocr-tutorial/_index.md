---
category: general
date: 2026-09-13
description: 学习在 C# 中通过加载图像进行 OCR、设置 OCR 语言并运行 Aspose OCR，从 JPG 文件中提取文本——一步一步的指南。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from jpg
- load image for ocr
- set ocr language
- c# ocr tutorial
language: zh
lastmod: 2026-09-13
og_description: 使用本简明 OCR 教程在 C# 中从 JPG 文件提取文本。学习如何加载图像进行 OCR、设置 OCR 语言，并获得准确的结果。
og_image_alt: Screenshot of C# console output showing extracted Ukrainian text from
  a JPG image
og_title: 在 C# 中从 JPG 提取文本 – 完整 OCR 教程
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn to extract text from JPG files in C# by loading an image for
    OCR, setting OCR language, and running Aspose OCR – a step‑by‑step guide.
  headline: How to extract text from JPG using a C# OCR tutorial
  type: TechArticle
- description: Learn to extract text from JPG files in C# by loading an image for
    OCR, setting OCR language, and running Aspose OCR – a step‑by‑step guide.
  name: How to extract text from JPG using a C# OCR tutorial
  steps:
  - name: Install the Aspose.OCR package
    text: 'Open a terminal in your project folder and run:'
  - name: Create a console application skeleton
    text: 'Create a new console project if you don’t already have one:'
  - name: Load an image for OCR
    text: The first operation after instantiating the engine is to provide the image
      you want to process. Aspose.OCR supports JPEG, PNG, BMP, GIF, and TIFF. In this
      tutorial we work with a JPEG file named **sample_ukrainian.jpg**.
  - name: Set OCR language
    text: OCR accuracy heavily depends on the language model. Aspose.OCR ships with
      data files for more than 30 languages. To recognize Ukrainian text, set the
      language code to `"ukr"`.
  - name: Perform OCR and extract text from JPG
    text: Calling `Recognize()` runs the recognition pipeline and returns the detected
      text as a plain string.
  - name: Run the program and verify the output
    text: 'Compile and execute the application:'
  - name: Loading images from memory or a web request
    text: 'Instead of `ImageStream.FromFile`, you can create a stream from a byte
      array:'
  - name: Processing multiple images in a batch
    text: 'Wrap the OCR logic in a method and iterate over a collection of file paths:'
  - name: Handling errors and edge cases
    text: 'OCR can fail if the image is corrupted or the language data cannot be downloaded.
      Catch exceptions to provide a graceful fallback:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: 如何使用 C# OCR 教程从 JPG 中提取文本
url: /zh/net/text-recognition/how-to-extract-text-from-jpg-using-a-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# OCR 教程从 JPG 中提取文本

如果您需要在 .NET 应用程序中从 JPG 图像中提取文本，本指南将逐步演示完整操作。您将加载用于 OCR 的图像，设置 OCR 语言，并使用 Aspose.OCR 获取识别后的文本——全部在一个独立的 C# 程序中完成。

本教程涵盖在乌克兰语、英语或任何受支持语言上运行 OCR 所需的全部内容。除了 Aspose.OCR NuGet 包外，无需任何外部工具，代码遵循资源管理和错误处理的最佳实践。

## 您将实现的目标

完成本教程后，您将能够：

* 直接从文件系统加载用于 OCR 的图像。  
* 将 OCR 语言设置为与源文档匹配。  
* 从 JPG 文件中提取文本并将结果输出到控制台。  
* 理解如何将示例适配到其他图像格式或语言。

**先决条件**  

* 已安装 .NET 6.0 SDK 或更高版本。  
* Visual Studio 2022（或任意 C# IDE）。  
* Aspose.OCR NuGet 包（`dotnet add package Aspose.OCR`）。  

无需任何 OCR 先验经验。

## 如何使用 Aspose OCR 在 C# 中从 JPG 提取文本

以下章节将过程拆解为清晰的步骤。每一步都包含代码片段、步骤意义说明以及可在实际项目中应用的实用技巧。

### 步骤 1：安装 Aspose.OCR 包

在项目文件夹的终端中运行：

```bash
dotnet add package Aspose.OCR
```

该包包含 `OcrEngine` 类、语言数据文件以及用于加载图像的实用工具。只需安装一次，即可在引用 `.csproj` 文件的所有项目中使用该库。

### 步骤 2：创建控制台应用程序骨架

如果尚未创建控制台项目，请执行：

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

用后续步骤中的代码替换自动生成的 `Program.cs`。保持项目简洁有助于您专注于 OCR 工作流。

### 步骤 3：加载用于 OCR 的图像

实例化引擎后，第一步是提供要处理的图像。Aspose.OCR 支持 JPEG、PNG、BMP、GIF 和 TIFF。本教程使用名为 **sample_ukrainian.jpg** 的 JPEG 文件。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 3: Load the image to be processed
        // ImageStream.FromFile reads the file and creates a stream compatible with OcrEngine.
        var imagePath = "YOUR_DIRECTORY/sample_ukrainian.jpg";
        using (var engine = new OcrEngine())
        {
            engine.Image = ImageStream.FromFile(imagePath);
```

**为什么重要** – 将图像加载到 `ImageStream` 中可确保引擎能够访问像素数据而不会锁定原始文件。此方式同样适用于内存中的图像或来自 Web API 的图像。

### 步骤 4：设置 OCR 语言

OCR 的准确性高度依赖语言模型。Aspose.OCR 附带超过 30 种语言的数据文件。要识别乌克兰语文本，请将语言代码设为 `"ukr"`。

```csharp
            // Step 4: Set the language for recognition (Ukrainian = "ukr")
            engine.Language = "ukr";
```

如果需要处理英语，请使用 `"eng"`；西班牙语使用 `"spa"`。语言代码遵循 ISO 639‑2 标准。当您指定的语言尚未下载时，引擎会在首次运行代码时自动获取所需数据。

### 步骤 5：执行 OCR 并从 JPG 中提取文本

调用 `Recognize()` 会运行识别管道，并将检测到的文本作为普通字符串返回。

```csharp
            // Step 5: Perform OCR – required language data will be downloaded automatically if missing
            string recognizedText = engine.Recognize();

            // Step 6: Output the recognized text
            Console.WriteLine("=== Extracted text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

**说明** – `using` 块保证 `OcrEngine` 实例能够正确释放，包括本机内存缓冲区等非托管资源。在需要长时间运行并处理大量图像的服务中，及时释放引擎尤为关键。

### 步骤 6：运行程序并验证输出

编译并执行应用程序：

```bash
dotnet run
```

您应看到类似如下的输出：

```
=== Extracted text ===
Привіт, це тестовий текст українською мовою.
```

如果控制台出现乱码，请确保终端使用 UTF‑8 编码（Windows 上使用 `chcp 65001`），并且源图像具有清晰的高对比度文字。

## 将 C# OCR 教程适配到其他场景

### 从内存或 Web 请求加载图像

可以使用 `ImageStream.FromFile` 的替代方案，从字节数组创建流：

```csharp
byte[] imageBytes = await httpClient.GetByteArrayAsync(imageUrl);
engine.Image = ImageStream.FromBytes(imageBytes);
```

该技术在通过 API 接口上传图像时非常有用。

### 批量处理多个图像

将 OCR 逻辑封装为方法，并遍历文件路径集合：

```csharp
static string ExtractText(string path, string language = "eng")
{
    using var engine = new OcrEngine();
    engine.Image = ImageStream.FromFile(path);
    engine.Language = language;
    return engine.Recognize();
}
```

如果将 `using` 语句移到循环外部，复用同一 `OcrEngine` 实例即可降低开销。

### 处理错误和边缘情况

当图像损坏或语言数据无法下载时，OCR 可能会失败。捕获异常以提供优雅的回退：

```csharp
try
{
    string text = ExtractText(imagePath, "ukr");
    Console.WriteLine(text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

记录异常有助于在语言文件需要下载时排查网络问题。

## 完整可运行示例

下面是完整的程序代码，可直接复制到 `Program.cs` 中。它包含所有必需的 `using` 指令、注释以及错误处理。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Path to the JPEG image you want to process.
        var imagePath = "YOUR_DIRECTORY/sample_ukrainian.jpg";

        // Ensure the file exists before attempting OCR.
        if (!System.IO.File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        try
        {
            // Create the OCR engine inside a using block to guarantee disposal.
            using var engine = new OcrEngine();

            // Load the image for OCR.
            engine.Image = ImageStream.FromFile(imagePath);

            // Set OCR language (Ukrainian = "ukr").
            engine.Language = "ukr";

            // Perform OCR and retrieve the recognized text.
            string recognizedText = engine.Recognize();

            // Output the extracted text.
            Console.WriteLine("=== Extracted text from JPG ===");
            Console.WriteLine(recognizedText);
        }
        catch (Exception ex)
        {
            // Handle any exceptions that occur during OCR.
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

运行此代码即可从 JPG 文件中提取文本并打印到控制台。修改 `imagePath` 和 `engine.Language` 即可用于其他文件和语言。

## 结论

现在，您已经掌握了在 C# 中通过加载图像、设置 OCR 语言并执行简洁的 `c# ocr tutorial` 来提取 JPG 文本的完整流程。示例展示了最佳实践，包括正确释放 `OcrEngine`、处理缺失语言数据以及提供清晰的错误信息。

接下来您可以：

* 尝试不同的语言代码（`"eng"`、`"spa"`、`"fra"`）。  
* 将 OCR 逻辑集成到 ASP.NET Core API 中，实现按需图像处理。  
* 将 OCR 输出与自然语言处理库结合，分析提取的内容。

欢迎将代码应用到自己的项目中，并在评论或社交媒体上分享您的成果。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并探索项目中的替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image in C# – Offline OCR with Aspose (Step‑by‑Step Guide)](/ocr/english/net/text-recognition/extract-text-from-image-in-c-offline-ocr-with-aspose-step-by/)
- [Extract Text from Image in C# – Complete Aspose OCR Guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}