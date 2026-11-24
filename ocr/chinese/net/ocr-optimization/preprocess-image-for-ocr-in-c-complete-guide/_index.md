---
category: general
date: 2026-06-16
description: 使用 Aspose OCR 在 C# 中对图像进行 OCR 预处理。学习如何增强图像对比度并去除扫描图像中的噪声，以实现准确的文本提取。
draft: false
keywords:
- preprocess image for OCR
- enhance image contrast
- remove noise from scanned image
language: zh
og_description: 使用 Aspose OCR 对图像进行预处理。通过增强图像对比度和去除扫描图像噪声，提高识别准确率。
og_title: C# 中的 OCR 图像预处理 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Preprocess image for OCR using Aspose OCR in C#. Learn to enhance image
    contrast and remove noise from scanned image for accurate text extraction.
  headline: Preprocess Image for OCR in C# – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR using Aspose OCR in C#. Learn to enhance image
    contrast and remove noise from scanned image for accurate text extraction.
  name: Preprocess Image for OCR in C# – Complete Guide
  steps:
  - name: '**Heavy Salt‑and‑Pepper Noise** – Increase the aggressiveness of `DenoiseFilter`
      by passing a custom `DenoiseOptions` object (e.g., `new DenoiseFilter(new DenoiseOptions
      { Strength = 2 })`).'
    text: '**Heavy Salt‑and‑Pepper Noise** – Increase the aggressiveness of `DenoiseFilter`
      by passing a custom `DenoiseOptions` object (e.g., `new DenoiseFilter(new DenoiseOptions
      { Strength = 2 })`).'
  - name: '**Faded Ink on Yellow Paper** – Pair `ContrastEnhanceFilter` with a `BrightnessAdjustFilter`
      to lift the background tone before boosting contrast.'
    text: '**Faded Ink on Yellow Paper** – Pair `ContrastEnhanceFilter` with a `BrightnessAdjustFilter`
      to lift the background tone before boosting contrast.'
  - name: '**Colored Text** – Convert the image to grayscale first (`new GrayscaleFilter()`)
      because most OCR engines, including Aspose, work best on single‑channel data.'
    text: '**Colored Text** – Convert the image to grayscale first (`new GrayscaleFilter()`)
      because most OCR engines, including Aspose, work best on single‑channel data.'
  - name: '**Build** the console project (`dotnet build`).'
    text: '**Build** the console project (`dotnet build`).'
  - name: '**Run** (`dotnet run`). You should see something like:'
    text: '**Run** (`dotnet run`). You should see something like:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
title: 在 C# 中进行 OCR 图像预处理 – 完整指南
url: /zh/net/ocr-optimization/preprocess-image-for-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中对图像进行 OCR 预处理 – 完整指南

有没有想过，尽管原始照片相当清晰，为什么 OCR 结果却像一团乱麻？事实是，大多数 OCR 引擎——包括 Aspose OCR——都要求图像干净、对齐良好。**Preprocess image for OCR** 是将模糊、低对比度的扫描图像转化为清晰、机器可读文本的第一步。

在本教程中，我们将通过一个实用的端到端示例，既 **preprocess image for OCR**，又展示如何使用 Aspose 内置过滤器 **enhance image contrast** 和 **remove noise from scanned image**。完成后，您将拥有一个可直接运行的 C# 控制台应用程序，能够提供更可靠的识别结果。

---

## 您需要的环境

- **.NET 6.0 或更高**（代码同样适用于 .NET Framework 4.6+）  
- **Aspose.OCR for .NET** – 您可以获取 NuGet 包 `Aspose.OCR`  
- 一张受噪声、倾斜或对比度差影响的示例图片（演示中我们使用 `skewed-photo.jpg`）  
- 任意您喜欢的 IDE——Visual Studio、Rider 或 VS Code 都可以  

无需额外的本地库或复杂的安装；所有内容都包含在 Aspose 包中。

---

## ## OCR 图像预处理 – 步骤实现

下面是您需要编译的完整源文件。复制粘贴到新的控制台项目中，然后按 **F5** 运行。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2: Add preprocessing filters to improve recognition.
        // 2a – Remove noise from scanned image.
        ocrEngine.Settings.Filters.Add(new DenoiseFilter()); // Reduces random speckles.
        // 2b – Correct skew (deskew) that often appears in photographed documents.
        ocrEngine.Settings.Filters.Add(new DeskewFilter()); // Straightens the baseline.
        // 2c – Enhance image contrast for better character separation.
        ocrEngine.Settings.Filters.Add(new ContrastEnhanceFilter()); // Boosts contrast.

        // Step 3: (Optional) Rotate the image if it was captured at an angle.
        // Negative values rotate clockwise, positive counter‑clockwise.
        ocrEngine.Settings.Filters.Add(new RotateFilter(-3)); // Small correction.

        // Step 4: Perform OCR on the image file.
        // Replace the path with the actual location of your test image.
        string extractedText = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed-photo.jpg");

        // Step 5: Display the recognized text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

### 每个过滤器的重要性

| 过滤器 | 作用 | 为何有助于 OCR |
|--------|------|----------------|
| **DenoiseFilter** | 去除低光扫描中常见的随机像素噪声。 | 噪声可能被误认为字符碎片，破坏字符形状。 |
| **DeskewFilter** | 检测主要文本行的倾斜角度并将图像旋转至 0°。 | 倾斜的基线会让 OCR 引擎误以为字符倾斜，从而导致识别错误。 |
| **ContrastEnhanceFilter** | 扩大深色文字与浅色背景之间的差异。 | 更高的对比度提升大多数 OCR 流程中二值化阈值的效果。 |
| **RotateFilter**（可选） | 按您指定的角度手动旋转图像。 | 当自动去倾斜不足时非常有用，例如照片拍摄时有轻微倾斜。 |

> **专业提示：** 如果源文件是扫描的 PDF，先将页面导出为图像（例如使用 `PdfRenderer`），再将其送入相同的过滤链。预处理逻辑保持不变。

---

## ## OCR 前的图像对比度增强 – 可视化确认

添加过滤器是一回事，看到效果又是另一回事。下面是一张简单的前后对比示意图（测试时请替换为您自己的截图）。

![Diagram of preprocess image for OCR pipeline](image.png){alt="OCR 预处理图像管道示意图"}

左侧显示原始的噪声扫描，右侧则展示经过 **enhance image contrast**、**remove noise from scanned image** 以及去倾斜处理后的同一图像。注意字符变得清晰且独立——正是 OCR 引擎所需要的。

---

## ## 去除扫描图像噪声 – 边缘情况与技巧

并非所有文档都面临相同类型的噪声。以下是您可能遇到的几种场景以及对应的管道调整方法：

1. **Heavy Salt‑and‑Pepper Noise** – 通过传入自定义 `DenoiseOptions` 对象（例如 `new DenoiseFilter(new DenoiseOptions { Strength = 2 })`）来提升 `DenoiseFilter` 的强度。  
2. **Faded Ink on Yellow Paper** – 将 `ContrastEnhanceFilter` 与 `BrightnessAdjustFilter` 组合使用，在提升对比度前先提升背景亮度。  
3. **Colored Text** – 首先使用 `new GrayscaleFilter()` 将图像转换为灰度，因为包括 Aspose 在内的大多数 OCR 引擎在单通道数据上表现最佳。  

过滤器的顺序也会影响效果。实践中，我会把 `DenoiseFilter` **放在** `DeskewFilter` **之前**，因为更干净的图像能为去倾斜算法提供更可靠的边缘数据。

---

## ## 运行示例并验证输出

1. **构建** 控制台项目 (`dotnet build`).  
2. **运行** (`dotnet run`). 您应该会看到类似如下的输出：

```
=== OCR RESULT ===
The quick brown fox jumps over the lazy dog.
```

如果输出仍然出现乱码，请再次确认图像路径是否正确，以及源文件的分辨率是否过低（大多数 OCR 任务建议最低 300 dpi）。

---

## 结论

您现在拥有一套在 C# 中 **preprocess image for OCR** 的稳固、可投入生产的方案。通过串联 Aspose 的 `DenoiseFilter`、`DeskewFilter` 与 `ContrastEnhanceFilter`——以及可选的 `RotateFilter`——您可以 **enhance image contrast**、**remove noise from scanned image**，并显著提升后续文本提取的准确性。

接下来可以尝试将清理后的图像送入其他后处理步骤，如拼写检查、语言检测，或将原始文本输入自然语言处理流水线。您也可以探索 Aspose 的 `BinarizationFilter` 用于仅二值化的工作流，或在复用相同预处理链的情况下切换到其他 OCR 引擎（Tesseract、Microsoft OCR）。

遇到仍然难以处理的图像吗？留下评论，我们一起排查。祝编码愉快，愿您的 OCR 结果始终晶莹剔透！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，构建在本篇演示的技巧之上。每篇资源都提供完整可运行的代码示例和逐步解释，帮助您掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [如何使用 AspOCR：针对 .NET 的图像 OCR 预处理过滤器](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [从图像提取文本 – 使用 Aspose.OCR for .NET 进行 OCR 优化](/ocr/english/net/ocr-optimization/)
- [如何使用 Aspose.OCR for .NET 从图像提取文本](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}