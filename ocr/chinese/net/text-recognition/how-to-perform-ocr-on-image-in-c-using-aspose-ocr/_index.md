---
category: general
date: 2026-10-11
description: 学习如何在 C# 中使用 Aspose.OCR 对图像进行 OCR，包括安装 System.Drawing.Common 并从 JPG 文件中提取文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: zh
lastmod: 2026-10-11
og_description: 在 C# 中使用 Aspose.OCR 对图像执行 OCR。本指南展示了如何安装 System.Drawing.Common、加载用于
  OCR 的图像以及从 JPG 中提取文本。
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: 在 C# 中对图像进行 OCR – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 Aspose.OCR 对图像进行 OCR
url: /zh/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.OCR 对图像执行 OCR

如果您需要在 .NET 应用程序中 **对图像文件执行 OCR**，本指南提供了完整的解决方案。使用 Aspose.OCR，您可以快速 **从图片中识别文本**（如 JPG），并在控制台窗口中显示结果。

您将学习如何：

* **安装 System.Drawing.Common 包** —— 提供 `Image` 类的库，
* **加载用于 OCR 的图像** —— 将 JPEG 或 PNG 读取到内存，
* 配置语言模型，
* **对图像执行 OCR**，以及最后，
* **从 JPG 中提取文本** 并输出。

这些步骤针对 .NET 6+ 编写，但同样适用于 .NET Framework 4.6.1 及以上版本。

---

## 前置条件

| 要求 | 为什么重要 |
|------|------------|
| .NET 6 SDK（或 .NET Framework 4.6.1+） | 为 C# 控制台应用提供运行时。 |
| Visual Studio 2022（或任意 IDE） | 便于添加 NuGet 包并运行程序。 |
| 网络连接（仅首次运行） | Aspose.OCR 会自动下载语言模块。 |
| 包含西里尔文或拉丁文的示例图像（例如 `sample_cyrillic.jpg`） | 用于演示 **从 JPG 中提取文本**。 |

---

## 第 1 步：安装 System.Drawing.Common 包

`System.Drawing.Common` NuGet 包提供了您将在 **加载用于 OCR 的图像** 时使用的 `Image` 类。打开包管理器控制台并运行：

```powershell
Install-Package System.Drawing.Common
```

> **小贴士：** 如果在 Linux/macOS 上遇到平台特定警告，请将目标设置为 `net6.0-windows`，或在项目文件中添加 `<UseWindowsForms>true</UseWindowsForms>`。

---

## 第 2 步：添加 Aspose.OCR NuGet 包

Aspose.OCR 包含 OCR 引擎和语言模型。使用以下命令安装：

```powershell
Install-Package Aspose.OCR
```

该包体积轻巧；所需的语言数据（例如西里尔文）会在您首次设置 `OcrEngine.Language` 时自动下载。

---

## 第 3 步：如何加载用于 OCR 的图像

在 **对图像执行 OCR** 之前，首先需要加载图片。`Image.FromFile` 方法可以读取 GDI+ 支持的任何格式，包括 JPG、PNG、BMP 和 TIFF。

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*如果文件不存在，会抛出 `FileNotFoundException` —— 在生产代码中请使用 try/catch 包裹此调用。*

---

## 第 4 步：配置引擎并 **对图像执行 OCR**

创建 `OcrEngine` 实例，选择语言模型，分配已加载的图像，然后调用 `Recognize()`。

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

`Recognize()` 方法返回一个 `OcrResult` 对象，其中包含提取的文本、置信度分数和边界框。语言模块会在首次使用时自动下载，无需额外文件。

---

## 第 5 步：**从 JPG 中提取文本** 并显示

现在您可以 **从图片中识别文本** 并输出结果。`OcrResult` 的 `Text` 属性包含纯字符串。

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### 预期的控制台输出

```
Recognized text:
Пример текста на кириллице
```

如果源图像包含英文文本，输出将是您在图片中放置的英文句子。

---

## 边缘情况和最佳实践提示

| 情况 | 建议 |
|------|------|
| **大图像（> 5 MB）** | 在 OCR 前将图像最长边缩放至 ≤ 2000 px，以降低内存占用并提升速度。 |
| **一张图片中包含多种语言** | 除西里尔文外，再调用 `ocrEngine.AddLanguage(OcrLanguage.English)`，然后将 `ocrEngine.Language = OcrLanguage.Multilingual`。 |
| **低对比度扫描件** | 在将位图传递给引擎前，使用 `System.Drawing.Graphics` 提高对比度。 |
| **在 Linux/macOS 上运行** | 确保已安装 `libgdiplus` 本地依赖（`sudo apt-get install -y libgdiplus`）。 |
| **重复调用 OCR** | 重用同一个 `OcrEngine` 实例，仅替换 `ocrEngine.Image`，以避免重复加载模块。 |

---

## 完整可运行程序

下面是整合了所有前述步骤的完整控制台应用程序代码。将代码复制到新的 C# 控制台项目中，替换图像路径后运行。

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**运行程序** 后，识别出的字符串会打印到控制台，证明您已经成功 **对图像执行 OCR** 并 **从 JPG 中提取文本**。

---

## 结论

现在，您已经掌握了如何在 C# 中使用 Aspose.OCR 对 **图像文件执行 OCR**，从安装必需的 **System.Drawing.Common 包**、**加载用于 OCR 的图像**、选择合适的语言模型，到最终 **从 JPG 中提取文本**。这个端到端示例为您构建更高级的文档处理流水线奠定了坚实基础，例如批量处理文件夹中的图片或将 OCR 集成到 Web API 中。

### 接下来可以做什么？

* 探索 **从 PDF 中识别图片文本**，先将每页转换为图像再进行 OCR。
* 试验 `OcrEngine` 的 `Resolution`、`Threshold` 和 `MaxProcessingTime` 属性，以在噪声扫描件上微调准确度。
* 将 OCR 输出与自然语言处理库结合，实现自动分类提取的内容。

欢迎根据其他图像格式调整代码，添加错误处理，或将其集成到更大的应用程序中。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并探索替代实现方式。

- [Extract Text from Image in C# – Complete Aspose OCR Guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}