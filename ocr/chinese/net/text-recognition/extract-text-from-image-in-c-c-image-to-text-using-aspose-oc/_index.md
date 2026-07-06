---
category: general
date: 2026-04-17
description: 使用 Aspose OCR 在 C# 中从图像提取文本。了解如何读取 PNG 文本、将图像转换为文本，以及在几分钟内加载图像进行 OCR。
draft: false
keywords:
- extract text from image
- read text from png
- convert image to text
- c# image to text
- load image for ocr
language: zh
og_description: 使用 Aspose OCR 在 C# 中从图像提取文本。本教程展示了如何读取 PNG 文本、将图像转换为文本，以及高效加载图像进行
  OCR。
og_title: 在 C# 中从图像提取文本 – 完整的 Aspose OCR 指南
tags:
- Aspose OCR
- C#
- Image Processing
title: 在 C# 中从图像提取文本 – 使用 Aspose OCR 将图像转换为文本
url: /zh/net/text-recognition/extract-text-from-image-in-c-c-image-to-text-using-aspose-oc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本（C#）– 完整的 Aspose OCR 指南

是否曾经需要**从图像中提取文本**但不确定该选哪个库？你并不孤单。许多开发者在面对 PNG 截图、扫描的发票或多语言标识时，都希望将像素转换为可搜索的文本。  

在本教程中，我们将手把手演示一个解决方案，使用 Aspose OCR **从 PNG 读取文本**、**将图像转换为文本**以及**加载图像进行 OCR**——全部使用简洁、现代的 C#。完成后，你将拥有一个可直接运行的程序，能够放入任何 .NET 项目中。

## 你将学到

- 如何为 OCR 加载图像文件（即“load image for OCR”步骤）  
- 如何为特定语言组配置 Aspose OCR  
- 如何提取识别后的字符串并在控制台显示  
- 处理多语言、大文件以及内存管理的技巧  

无需外部文档；下面的代码片段已涵盖所有所需内容。

## 前提条件

- .NET 6+ SDK（或 .NET Core 3.1+ —— API 相同）  
- Visual Studio 2022、VS Code 或任意你喜欢的 IDE  
- NuGet 包 **Aspose.OCR**（使用 `dotnet add package Aspose.OCR` 安装）  

如果你已经准备好这些，让我们开始吧。

![Extract text from image using Aspose OCR in C#](https://example.com/aspsoe-ocr-demo.png "extract text from image using Aspose OCR")

## 第一步 – 为 OCR 加载图像

首先，你需要给 OCR 引擎提供可读取的内容。Aspose OCR 支持多种格式，但 PNG 是截图和扫描图形的常见选择。

```csharp
using Aspose.OCR;

// Replace with the actual path to your PNG file
string imagePath = @"C:\Images\sample.png";

// OcrImage.FromFile handles PNG, JPEG, BMP, TIFF, etc.
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

> **为什么这很重要：** 正确加载图像可确保引擎看到你期望的像素数据。如果传入损坏的流，识别将悄然失败。

## 第二步 – 创建并配置 OCR 引擎

接下来，实例化 `OcrEngine`。你可以选择性地设置语言组；对于多数西文脚本默认即可，但如果处理西里尔文、阿拉伯文或亚洲字符，最好提前告知引擎。

```csharp
// The using statement guarantees proper disposal of native resources.
using var ocrEngine = new OcrEngine();

// Example: set language to Cyrillic if your PNG contains Russian or Ukrainian text.
// OcrLanguage.Cyrillic covers several Slavic languages.
ocrEngine.Language = OcrLanguage.Cyrillic;

// If you need to support multiple languages, you can combine flags:
 // ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

> **专业提示：** 设置语言会缩小引擎搜索的字符集，从而加快识别速度并提升准确率。

## 第三步 – 执行 OCR 并提取文本

现在开始繁重的工作。使用之前加载的图像调用 `Recognize`，随后从结果中读取 `Text` 属性。

```csharp
// Run OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);

// The recognized string is available via the Text property
string extractedText = ocrResult.Text;

// Output the result to the console (or write to a file, DB, etc.)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(extractedText);
```

### 预期输出

如果 `sample.png` 包含短语 “Hello, World!” ，你将看到：

```
=== OCR Output ===
Hello, World!
```

如果图像更复杂（例如多行收据），引擎会保留换行符，提供一个可直接处理的文本块。

## 第四步 – 将所有内容封装为完整程序

下面是完整的、独立的控制台应用程序，你可以复制粘贴到新的 C# 项目中。它包含错误处理和解释每个部分的注释。

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Load the image you want to recognize
                // Change the path to point at your own PNG file.
                var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.png");

                // 2️⃣ Create an OCR engine instance (disposed automatically)
                using var ocrEngine = new OcrEngine();

                // 3️⃣ Choose the language group.
                // Cyrillic works for Russian, Ukrainian, Bulgarian, etc.
                // For English only, you could use OcrLanguage.English.
                ocrEngine.Language = OcrLanguage.Cyrillic;

                // 4️⃣ Perform OCR
                var ocrResult = ocrEngine.Recognize(ocrImage);

                // 5️⃣ Output the recognized text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Simple error handling – in production you’d log this.
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

在项目文件夹中运行程序（`dotnet run`），即可在控制台看到提取的字符串。这就是整个 **extract text from image** 工作流，代码不到 30 行。

## 第五步 – 常见变体与边缘情况

### 从 PNG 读取文本 vs. 其他格式

虽然示例使用 PNG，Aspose OCR 也支持 JPEG、BMP、TIFF 和 GIF。只需更改文件扩展名，`OcrImage.FromFile` 调用即可无需修改直接使用。

### 在 Web API 中将图像转换为文本

如果需要通过 HTTP 端点公开此功能，可以接受 `IFormFile` 上传，使用 `OcrImage.FromStream` 将流转换为 `OcrImage`，并将字符串以 JSON 返回。核心 OCR 逻辑保持不变。

```csharp
// Example snippet inside an ASP.NET Core controller action
[HttpPost("api/ocr")]
public async Task<IActionResult> OcrUpload(IFormFile file)
{
    using var stream = file.OpenReadStream();
    var ocrImage = OcrImage.FromStream(stream);
    using var engine = new OcrEngine { Language = OcrLanguage.English };
    var result = engine.Recognize(ocrImage);
    return Ok(new { text = result.Text });
}
```

### 处理大图像

大型高分辨率图像会占用大量内存。实用的做法是先将图像缩小后再送入引擎：

```csharp
// Reduce resolution to 150 DPI (good trade‑off between speed and accuracy)
ocrEngine.ImagePreprocessing = ImagePreprocessingOptions.AutoResize;
ocrEngine.Dpi = 150;
```

### 多语言文档

如果文档混合英文和西里尔文，可组合语言标志：

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

引擎将尝试识别两套字符。

### 释放资源

`using` 语句包裹 `OcrEngine` 可确保本机资源被释放。忘记此步骤可能导致内存泄漏，尤其在长时间运行的服务中。

## 稳定 OCR 的专业技巧

- **清晰图像更佳：** 在 OCR 前使用 **ImageSharp** 等库对图像进行预处理（去倾斜、降噪）。  
- **字体大小重要：** 小于 10 px 的文字常被漏检；考虑对图像进行放大。  
- **检查 `ocrResult.Confidence`：** `OcrResult` 对象还会为每个单词提供置信度分数——可用其标记低置信度段落以供人工复核。  
- **批量处理：** 对于数十个文件，复用同一个 `OcrEngine` 实例以避免重复初始化开销。

## 结论

你刚刚学习了如何在 C# 中使用 Aspose OCR **从图像中提取文本**，涵盖了从 **load image for OCR** 到 **convert image to text** 再到 **read text from PNG** 的全部过程。完整的可运行示例展示了所需的精确代码，解释了每一步的原因，并提供了面向真实场景的实用变体。

准备好迎接下一个挑战了吗？可以将提取的字符串写入搜索索引，使用 Azure Cognitive Services 进行翻译，或生成带有同层文本的可搜索 PDF。可能性无限，而你已经为任何 **c# image to text** 项目奠定了坚实基础。

欢迎随意实验，调整语言设置，或将此代码片段集成到更大的应用中。如果遇到任何问题，请在下方留言——祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}