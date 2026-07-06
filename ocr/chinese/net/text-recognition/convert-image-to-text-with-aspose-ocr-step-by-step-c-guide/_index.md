---
category: general
date: 2026-02-22
description: 使用 Aspose OCR 在 C# 中将图像转换为文本。了解如何注册语言模块、加载图像进行 OCR 并提取图像中的文本，包括对西里尔字母的支持。
draft: false
keywords:
- convert image to text
- extract text from image
- how to register module
- load image for ocr
- how to recognize cyrillic
language: zh
og_description: 即时将图像转换为文本。本指南展示如何注册模块、加载图像进行 OCR，并从图像中提取文本，包括西里尔字母识别。
og_title: 使用 Aspose OCR 将图像转换为文本 – 完整 C# 教程
tags:
- Aspose OCR
- C#
- Image Processing
title: 使用 Aspose OCR 将图像转换为文本 – C# 步骤指南
url: /zh/net/text-recognition/convert-image-to-text-with-aspose-ocr-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 将图像转换为文本 – 步骤详解 C# 指南

是否曾需要 **将图像转换为文本**，却不知从何入手？你并不孤单——许多开发者在图片包含非拉丁字符（如西里尔字母）时会卡住。在本教程中，我们将演示一个完整、可直接运行的解决方案，展示如何注册语言模块、加载用于 OCR 的图像，最终使用 Aspose OCR for .NET 从图像中提取文本。

我们将覆盖从安装 NuGet 包到处理缺少语言文件等边缘情况的全部内容。阅读完本指南后，你只需几行 C# 代码即可 **将图像转换为文本**，并且了解每一步的原因。

## 你将学到的内容

- 如何 **注册西里尔语言模块**，让 OCR 引擎能够识别该脚本。  
- 使用 Aspose 的 `Image.Load` 方法 **正确加载图像用于 OCR**。  
- 如何将引擎设置为 **识别西里尔文**，随后 **从图像中提取文本**。  
- 常见陷阱的排查技巧，如损坏的 zip 模块或不支持的图像格式。  

### 前置条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）。  
- Visual Studio 2022（或任何支持 C# 的 IDE）。  
- Aspose.OCR NuGet 包（`Install-Package Aspose.OCR`）。  
- 一个西里尔语言 zip 文件（`cyrillic.zip`）和一张示例图片（`cyrillic_sample.jpg`）。  

> **专业提示：** 将语言模块放在专用文件夹中（例如 `./ocr-modules/`），可避免路径相关的错误。

---

## 步骤 1：如何注册模块 – 添加西里尔支持

在 OCR 引擎能够读取西里尔字符之前，你必须告诉它语言数据所在的位置。这就是 **如何注册模块** 的环节。

```csharp
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to the Cyrillic language module (ZIP file)
string languageModulePath = Path.Combine("ocr-modules", "cyrillic.zip");

// Read the ZIP file into a byte array
byte[] moduleBytes = File.ReadAllBytes(languageModulePath);

// Register the module with the OCR engine
OcrEngine.RegisterLanguageModule(Language.Cyrillic, moduleBytes);
```

**为什么要注册？**  
Aspose OCR 默认只随库附带一套拉丁语言，以保持库体积轻量。通过注册西里尔模块，你可以扩展引擎的词典，使其能够正确地将字形映射到 Unicode 字符。跳过此步骤会导致引擎只能猜测，输出乱码。

> **常见错误：** 使用指向错误目录的相对路径。始终使用 `Path.Combine` 构建路径，或在调用 `RegisterLanguageModule` 前使用 `File.Exists` 进行验证。

---

## 步骤 2：加载图像用于 OCR – 准备输入

语言准备好后，我们需要将图片加载到内存中。这就是 **加载图像用于 OCR** 的步骤。

```csharp
using Aspose.OCR;

// Ensure the image exists
string imagePath = Path.Combine("ocr-images", "cyrillic_sample.jpg");
if (!File.Exists(imagePath))
{
    Console.WriteLine($"Image not found: {imagePath}");
    return;
}

// Load the image – Aspose automatically detects format (JPEG, PNG, BMP, etc.)
Image inputImage = Image.Load(imagePath);
```

**为什么要这样加载？**  
`Image.Load` 会自动完成格式检测和色彩空间转换，无论源文件类型如何，都能为你提供一致的 `Image` 对象。这降低了新手在 OCR 时常遇到的 *不支持的格式* 错误概率。

> **提示：** 如果需要对图像进行预处理（例如去倾斜或二值化），请在调用 `Recognize` 之前完成。Aspose 提供 `ImageProcessor` 实用工具来实现这些操作。

---

## 步骤 3：设置语言并将图像转换为文本

在模块已注册且图片已加载后，我们终于可以 **将图像转换为文本**。此步骤同样回答了 **如何识别西里尔文**。

```csharp
// Create an OCR engine instance and set its language to Cyrillic
var ocrEngine = new OcrEngine
{
    Language = Language.Cyrillic,
    // Optional: increase accuracy for noisy images
    // Settings = new OcrEngineSettings { EnableNoiseRemoval = true }
};

// Run the recognition process
OcrResult ocrResult = ocrEngine.Recognize(inputImage);
```

**为什么要显式设置语言？**  
即使已注册模块，引擎默认仍使用英语。指定 `Language.Cyrillic` 可让引擎使用新注册的词典，显著提升对斯拉夫文字的识别准确率。

> **边缘情况：** 如果在识别图像前未设置语言，Aspose 将回退到拉丁语，导致西里尔文本显示为不可读字符。

---

## 步骤 4：从图像中提取文本 – 获取结果

`OcrResult` 对象包含原始字符串、置信度分数以及位置信息。大多数场景下，你只需要纯文本。

```csharp
// Display the recognized text in the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);

// Optional: check confidence (0‑100)
// Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

**为什么要检查置信度？**  
置信度告诉你 OCR 结果的可靠程度。通常置信度高于 80% 的结果可直接用于后续处理，而较低的分数可能需要人工复核或进一步的图像预处理。

> **如果输出为空怎么办？**  
常见原因包括语言模块不正确、图像损坏，或图像对比度过低。尝试提升对比度或在识别前使用 `ImageProcessor.AdjustContrast`。

---

## 完整可运行示例

下面是完整的、可直接复制粘贴的程序，将所有步骤串联起来。将其保存为 `Program.cs` 并在项目根目录运行。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Register the Cyrillic language module
        // -------------------------------------------------
        string languageModulePath = Path.Combine("ocr-modules", "cyrillic.zip");
        if (!File.Exists(languageModulePath))
        {
            Console.WriteLine($"Language module not found: {languageModulePath}");
            return;
        }
        OcrEngine.RegisterLanguageModule(Language.Cyrillic, File.ReadAllBytes(languageModulePath));

        // -------------------------------------------------
        // Step 2: Load the image you want to convert
        // -------------------------------------------------
        string imagePath = Path.Combine("ocr-images", "cyrillic_sample.jpg");
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }
        Image inputImage = Image.Load(imagePath);

        // -------------------------------------------------
        // Step 3: Create OCR engine and set language
        // -------------------------------------------------
        var ocrEngine = new OcrEngine { Language = Language.Cyrillic };

        // -------------------------------------------------
        // Step 4: Recognize and extract text
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 5: Output the result
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**预期输出**

```
=== OCR Result ===
Привет мир! Это пример текста на кириллице.
```

如果看到的是乱码而非西里尔文字，请再次确认 `cyrillic.zip` 与所安装的 Aspose OCR 版本匹配，并确保图像足够清晰以供识别。

---

## 常见问题解答 (FAQ)

**问：我可以将此方法用于其他语言吗？**  
答：完全可以。将 `Language.Cyrillic` 替换为相应的枚举（例如 `Language.Arabic`），并注册对应的 ZIP 文件即可。

**问：支持哪些图像格式？**  
答：`Image.Load` 原生支持 JPEG、PNG、BMP、TIFF 和 GIF。若要处理 PDF，需要使用 Aspose.PDF 将页面转换为图像后再进行 OCR。

**问：如何提升对低质量扫描件的识别准确度？**  
答：对图像进行预处理——使用 `ImageProcessor` 进行二值化、去倾斜或噪声去除。同时，可提升 `OcrEngineSettings` 中的 `EnableNoiseRemoval`、`EnableTextSegmentation` 等选项。

**问：如何获取每个单词的边界框？**  
答：`OcrResult` 包含 `Regions` 集合，每个区域都有 `Location` 数据。遍历 `ocrResult.Regions` 即可提取坐标信息。

---

## 结论

我们展示了如何使用 Aspose OCR **将图像转换为文本**，涵盖了从 **如何注册模块** 到 **加载图像用于 OCR**，再到 **识别西里尔文并提取文本** 的完整流程。上面的完整代码片段已可直接运行，解释部分帮助你了解每行代码背后的原因，从而能够将该方案迁移到其他语言或更复杂的工作流中。

准备好下一步了吗？尝试对多页 PDF 进行转换，将 OCR 输出集成到搜索索引，或与 Azure Cognitive Services 结合实现语言检测。一旦掌握了图像转文本的基础，创意无限。

---

![将图像转换为文本示例](image-placeholder.png "将图像转换为文本")

*祝编码愉快！如果遇到任何问题，欢迎在下方留言，我们一起排查。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}