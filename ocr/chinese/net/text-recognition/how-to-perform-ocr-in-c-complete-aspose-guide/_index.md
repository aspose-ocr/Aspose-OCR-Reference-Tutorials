---
category: general
date: 2026-02-16
description: 学习如何使用 Aspose.OCR 在 C# 中执行 OCR —— 从照片中识别文本、从扫描件中读取文本，并以高精度提取收据中的文本。
draft: false
keywords:
- how to perform OCR
- recognize text from photo
- read text from scan
- extract text from receipt
- improve OCR accuracy
language: zh
og_description: 了解如何使用 Aspose.OCR 在 C# 中执行 OCR。本指南向您展示如何从照片中识别文本、从扫描件中读取文本以及从收据中提取文本。
og_title: 如何在 C# 中进行 OCR – 完整的 Aspose 指南
tags:
- C#
- Aspose.OCR
- Image Processing
title: 如何在 C# 中进行 OCR – 完整的 Aspose 指南
url: /zh/net/text-recognition/how-to-perform-ocr-in-c-complete-aspose-guide/
---

: "## 结论"

Paragraph:

You now... translate.

Will translate whole paragraph.

Next final lines: "Got more questions..." translate.

Then closing shortcodes.

Now produce final content.

Be careful to keep markdown formatting exactly.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中执行 OCR – 完整 Aspose 指南

是否曾经想过在模糊的收据或手机拍摄的随机照片上 **如何执行 OCR**？你并不是唯一有此疑问的人。在许多真实场景的应用中，我们需要 **从照片中识别文本** 文件、**从扫描件中读取文本** 文档，或 **从收据图像中提取文本**，而且不将数据发送到云服务。

在本教程中，我们将通过一个自包含的示例演示如何使用 Aspose.OCR **执行 OCR**，并在过程中穿插 **提升 OCR 准确率** 的技巧。完成后，你将拥有一个可直接运行的 C# 控制台程序，能够从任意指向的图像中提取纯文本。

> **你需要准备的内容**  
> * .NET 6 SDK（或任意近期的 .NET 版本）  
> * Aspose.OCR NuGet 包（`Install-Package Aspose.OCR`）  
> * 示例图片——例如名为 `photo_receipt.jpg` 的收据照片  

![如何执行 OCR 示例](image.png){alt="如何执行 OCR"}

## 使用 Aspose.OCR 在 C# 中执行 OCR

第一步是设置 OCR 引擎并加载英文语言模型。这是 **执行 OCR** 的核心；如果没有语言模型，引擎将不知道要识别哪些字符。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the English language model – change this if you need another language
ocrEngine.LoadLanguage(LanguageModel.English);
```

*Why this matters*: 加载正确的语言模型直接影响识别速度和准确性。英文是最常见的情况，但 Aspose 还提供数十种其他模型，如果你需要 **从扫描件中读取文本** 的法语、德语等文档，也可以使用。

## 从照片中识别文本

手机拍摄的照片常常存在旋转、噪点或对比度低等问题。在让引擎 **从照片中识别文本** 之前，我们先配置一些预处理选项来清理图像。

```csharp
// Configure preprocessing to boost OCR results
PreprocessingOptions preprocessingOptions = new PreprocessingOptions
{
    Deskew = true,                     // Auto‑correct rotation (helps with tilted receipts)
    Denoise = DenoiseLevel.Medium,    // Reduce graininess
    Binarize = BinarizeMethod.Otsu,   // Convert to black‑and‑white for sharper edges
    ContrastEnhancement = true        // Boost contrast for faint characters
};

// Apply the preprocessing configuration
ocrEngine.Preprocessing = preprocessingOptions;
```

*Pro tip*: 如果发现字符缺失，尝试将 `DenoiseLevel` 调整为 `High`，或使用 `BinarizeMethod.Sauvola`。这些微调属于 **提升 OCR 准确率** 的策略。

## 从扫描件中读取文本

现在引擎已经准备就绪，我们加载图像。无论是保存为 JPEG 的扫描 PDF 页面，还是打印表单的照片，代码保持不变。

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/photo_receipt.jpg");
```

如果你拥有的是 `Stream` 而不是文件路径，只需将 `FromFile` 替换为 `FromStream`。这种灵活性在你 **从扫描件中读取文本** 的图像来自网页上传时非常有用。

## 从收据中提取文本

一切就绪后，实际的 OCR 调用只需一行代码。该方法返回提取的纯文本字符串，随后我们可以将其显示、存储或传递给其他系统。

```csharp
// Perform OCR and capture the result
string extractedText = ocrEngine.Recognize();

// Output the text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(extractedText);
```

**Expected output**（简单收据示例）：

```
=== OCR RESULT ===
Store: CoffeeShop
Date: 2024-02-15
Item      Qty   Price
Latte      2    4.50
Bagel      1    2.75
Total            7.25
```

如果输出出现乱码，请重新检查预处理部分——这是最常见的 **提升 OCR 准确率** 的位置。

## 提升 OCR 准确率 – 高级调优

虽然默认设置适用于多数情况，但生产级流水线往往需要额外的调优：

| 情况 | 调整 | 原因 |
|-----------|------------|--------|
| 背景非常暗 | `ContrastEnhancement = true` + `Binarize = BinarizeMethod.Sauvola` | 增加文本与背景的分离度 |
| 手写笔记 | `ocrEngine.LoadLanguage(LanguageModel.EnglishHandwritten)` | 针对连笔笔画的专用模型 |
| 多页扫描 | Loop over each page image and call `Recognize()` per iteration | 保持低内存占用 |
| 大图像（> 2000 px） | Resize before feeding to OCR (`Image.Resize(width, height)`) | 处理更快，内存消耗更少 |

请记住，**执行 OCR** 并非一刀切的配方——你通常需要反复调试这些参数，直到输出满足质量要求。

## 完整可运行示例

下面是完整的、可直接复制粘贴的程序。它包含了前文讨论的所有部分，并附带一个小助手，用于在读取文件前检查文件是否存在。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine and load language
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 2️⃣ Set up preprocessing to improve OCR accuracy
        ocrEngine.Preprocessing = new PreprocessingOptions
        {
            Deskew = true,
            Denoise = DenoiseLevel.Medium,
            Binarize = BinarizeMethod.Otsu,
            ContrastEnhancement = true
        };

        // 3️⃣ Path to the image – change this to your own file
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo_receipt.jpg");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"⚠️  Image not found: {imagePath}");
            return;
        }

        // 4️⃣ Load the image (recognize text from photo / read text from scan)
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 5️⃣ Perform OCR – this is the core of how to perform OCR
        string extractedText = ocrEngine.Recognize();

        // 6️⃣ Show the result – you can now extract text from receipt, invoice, etc.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

使用 `dotnet run` 运行程序。如果一切配置正确，你将在控制台看到提取的文本。

## 常见问题与边缘情况

**Q: 如果图像是 PDF 怎么办？**  
A: 首先将每页 PDF 转换为图像（例如使用 `Aspose.Pdf` 或 `PdfSharp`），然后将生成的位图传递给 `ocrEngine.Image`。

**Q: 能并行处理图像吗？**  
A: 可以，但每个线程必须实例化一个独立的 `OcrEngine`。该引擎不是线程安全的，共享同一个实例会导致竞争条件。

**Q: 这在 Linux 上能运行吗？**  
A: 完全可以。Aspose.OCR 是跨平台的，只需确保已安装本机依赖 (`libgdiplus` 用于 Linux 上的 .NET Core)。

**Q: 如何处理多语言收据？**  
A: 在识别之前加载多个语言模型：  
```csharp
ocrEngine.LoadLanguage(LanguageModel.English);
ocrEngine.LoadLanguage(LanguageModel.Spanish);
```  
引擎会按顺序尝试每个模型。

## 结论

现在，你已经掌握了使用 Aspose.OCR 在 C# 中 **执行 OCR** 的完整端到端方案。教程涵盖了从初始化引擎、**从照片中识别文本**、**从扫描件中读取文本** 到 **从收据中提取文本** 的全部步骤，并提供了实用的 **提升 OCR 准确率** 方法。

接下来可以尝试将英文模型换成手写模型，实验不同的 `BinarizeMethod` 值，或将 OCR 调用集成到 ASP.NET API 中，实现即时上传处理。可能性与您提供的图像数量一样广阔。

还有关于 OCR、图像预处理或 Aspose 库的其他问题吗？欢迎留言或查阅官方 Aspose.OCR 文档获取更深入的内容。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}