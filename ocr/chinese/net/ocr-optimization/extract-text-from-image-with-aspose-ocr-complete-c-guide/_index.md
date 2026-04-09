---
category: general
date: 2026-04-08
description: 使用 Aspose OCR 在 C# 中提取图像文本。了解如何对图像进行 OCR 预处理以及如何通过预处理提升准确率。
draft: false
keywords:
- extract text from image
- preprocess image for ocr
- how to preprocess image
- Aspose OCR C#
- image preprocessing techniques
language: zh
og_description: 使用 Aspose OCR 在 C# 中提取图像文本。本指南展示了如何对图像进行预处理以进行 OCR，以及如何进行预处理以获得最佳效果。
og_title: 使用 Aspose OCR 从图像提取文本 – 完整 C# 指南
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 使用 Aspose OCR 从图像提取文本 – 完整 C# 指南
url: /zh/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 从图像中提取文本 – 完整 C# 指南

是否曾经需要**从图像中提取文本**，却发现结果错误连连？你并不孤单——大多数开发者在源图片倾斜、噪声大或对比度低时都会遇到这种情况。好消息是，只需一个简短的预处理步骤，就能把模糊的快照变成 OCR 的干净源文件，而 Aspose OCR 让整个过程轻而易举。

在本教程中，我们将通过一个真实案例演示**如何使用 Aspose OCR 内置过滤器对图像进行预处理**，随后仅用几行 C# **从图像中提取文本**。完成后，你将拥有一个可直接运行的程序，了解每个过滤器的作用，并知道如何为自己的特殊情况微调流水线。

## 你需要准备的环境

- .NET 6.0 或更高（代码同样适用于 .NET Framework 4.7+）
- Aspose.OCR NuGet 包（`Install-Package Aspose.OCR`）
- 一张倾斜、噪声大或对比度低的示例图片（例如 `skewed_noisy.jpg`）
- 任意 IDE——Visual Studio、Rider 或 VS Code 都可以

无需额外的本地库，也不需要调用 Web 服务，纯 C# 即可。

## 第一步：设置 OCR 引擎 – 提取文本的起点

首先，创建一个 `OcrEngine` 实例并指定要识别的语言。英语最常用，但你可以把 `"en"` 换成 `"fr"`、`"de"` 等。

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void PreprocessAndOcr()
    {
        // 1️⃣ Initialize the OCR engine – this is where we define the language.
        var ocrEngine = new OcrEngine { Language = "en" };
```

**为什么重要：** 引擎内部保存了字典和语言特定的启发式规则。如果不显式设置语言，Aspose 会默认使用英语，但明确指定可以避免在后期切换语言时出现意外。

## 第二步：构建预处理流水线 – 如何对图像进行预处理以获得最佳效果

接下来添加过滤器。把它们想象成在 OCR 步骤之前自动运行的微型照片编辑套件。下面的三个过滤器覆盖了最常见的问题：

| 过滤器 | 修复内容 | 何时使用 |
|--------|----------|----------|
| `DeskewFilter` | 将图像旋转回水平 | 角度拍摄的图片 |
| `DenoiseFilter` | 降低随机斑点和颗粒 | 低光照片或扫描文档 |
| `ContrastStretchFilter` | 提升对比度，使暗文字更突出 | 褪色的打印件或颜色被冲淡的截图 |

```csharp
        // 2️⃣ Add preprocessing steps – this is the core of “how to preprocess image”.
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast
```

**小技巧：** 顺序很重要。先去倾斜（Deskew），再去噪声（Denoise），最后拉伸对比度（ContrastStretch）。如果顺序颠倒，可能会放大噪声而不是去除它。

## 第三步：运行 OCR – 最终从图像中提取文本

流水线准备好后，将图片路径交给引擎。Aspose 会自动应用过滤器，然后执行识别算法。

```csharp
        // 3️⃣ Recognize text from the pre‑processed image.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");
```

如果文件未找到，会抛出明确的 `FileNotFoundException`。因此我们建议在开发阶段使用绝对路径，生产环境再切换为相对路径或配置项。

## 第四步：显示结果 – 看看得到什么

`OcrResult` 对象包含原始文本、置信度分数，甚至每个单词的边界框。为了快速演示，我们只把文本打印到控制台。

```csharp
        // 4️⃣ Output the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

运行程序后，你应该看到类似下面的输出：

```
=== OCR Output ===
Invoice Number: 2023-0456
Date: 03/15/2024
Total: $1,234.56
```

如果输出乱码，请再次检查图像质量或尝试添加额外过滤器（例如针对二值图的 `BinarizationFilter`）。

## 完整可运行示例 – 复制粘贴即可运行

下面是完整的、独立的程序。只需把 `YOUR_DIRECTORY/skewed_noisy.jpg` 替换为实际的测试图片路径。

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void Main()
    {
        PreprocessAndOcr();
    }

    public static void PreprocessAndOcr()
    {
        // Step 1: Create OCR engine and set language
        var ocrEngine = new OcrEngine { Language = "en" };

        // Step 2: Build preprocessing pipeline
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast

        // Step 3: Recognize text from the pre‑processed image
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // Step 4: Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**预期输出** – 控制台会打印图像中包含的纯文本。如果图像是一块写有 “OpenAI” 的标牌，控制台将仅显示该单词，不会出现多余符号。

## 边缘情况与流水线微调

### 1️⃣ 极暗图像

如果对比度过滤器仍不足，可在前面加入 `BrightnessCorrectionFilter`：

```csharp
ocrEngine.Preprocess.Add(new BrightnessCorrectionFilter(30)); // increase brightness by 30%
```

### 2️⃣ 多语言文档

设置 `Language = "en+fr"`（Aspose 支持逗号分隔的语言代码），并在需要时添加 `LanguageDetectionFilter` 让引擎自动检测语言。

### 3️⃣ 大型 PDF 转图片

一次处理千页 PDF 的每页图像会很慢。可以使用 `Parallel.ForEach` 并行处理多张图片，但要记住 `OcrEngine` 不是线程安全的——每个线程需要单独实例。

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine { Language = "en" };
    // add same filters...
    var result = engine.RecognizeImage(path);
    // store result...
});
```

### 4️⃣ 获取边界框

如果需要每个单词的位置（例如用于高亮），检查 `ocrResult.Regions`。每个 Region 包含 `Rectangle` 坐标，可用于 UI 覆盖层。

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

## 常见陷阱（以及如何避免）

- **跳过 Deskew 步骤** – 即使是 2 度的倾斜也会导致置信度下降约 20 %。源图像未完全对齐时务必添加 `DeskewFilter`。
- **使用高压缩的 JPEG** – 压缩伪影会被误认为噪声；改用 PNG 或 TIFF 可提升 OCR 效果。
- **硬编码路径** – 相对路径在本地开发时可行，但在 CI/CD 流水线中应从配置或环境变量读取图像位置。

## 测试你的配置

1. 使用干净、高对比度的图像运行程序，应该得到几乎完美的文本。
2. 换成噪声大、倾斜的照片。验证加入三个过滤器后输出是否有所提升。
3. 逐一移除过滤器观察其影响——这有助于理解*为什么*每一步都重要。

## 结论

我们已经演示了如何使用 Aspose OCR **从图像中提取文本**，并展示了一种在大多数真实场景下有效的 **图像预处理** 方法。通过串联 `DeskewFilter`、`DenoiseFilter` 与 `ContrastStretchFilter`，为引擎提供了干净的画布，从而显著提升识别准确率。

接下来，你可以探索更高级的过滤器、处理多页文档，或将 OCR 结果集成到搜索索引中。无论选择哪条道路，核心模式——初始化、预处理、识别、消费——始终如一。

准备好升级了吗？尝试为黑白扫描添加 `BinarizationFilter`，或将输出写入数据库以实现可搜索的 PDF。祝编码愉快，愿每一张交给 Aspose 的图像都能返回清晰、可读的文本！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}