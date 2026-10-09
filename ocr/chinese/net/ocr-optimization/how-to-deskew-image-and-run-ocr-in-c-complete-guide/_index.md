---
category: general
date: 2026-03-07
description: 学习如何使用 Aspose OCR 对图像进行去倾斜、增强对比度，并从扫描中提取文本。使用完整的 C# 示例对图像执行 OCR，并轻松加载图像进行
  OCR。
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: zh
og_description: 了解如何使用 Aspose OCR 在 C# 中对图像进行去倾斜、增强对比度并从扫描中提取文本。通过一步步的代码对图像执行 OCR。
og_title: 如何在 C# 中纠正图像倾斜并运行 OCR – 完整指南
tags:
- C#
- OCR
- Image Processing
title: 如何在 C# 中纠正图像倾斜并运行 OCR – 完整指南
url: /zh/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中去倾斜图像并运行 OCR – 完整指南

如果你曾经想过在运行 OCR 之前 **如何去倾斜图像**，那么你来对地方了。在本教程中，我们将逐步演示如何提升对比度、加载图像进行 OCR，最后使用 Aspose OCR **提取扫描文本**。

无论你是要数字化旧收据、清理扫描的合同，还是仅仅需要一种可靠的方法来读取倾斜照片中的文字，下面的步骤都涵盖了你所需的一切。没有废话——只提供一个可以直接复制粘贴到 Visual Studio 的可运行示例。

## 你将实现的目标

通过本指南，你将能够：

* 将倾斜校正至最高30°（这就是 **how to deskew image** 的部分）。  
* 提高图像对比度以获得更清晰的字符边缘（**how to boost contrast**）。  
* 将图片加载到 OCR 引擎中（**load image for OCR**）。  
* 运行识别过程并 **extract text from scan**。  

所有这些都基于最新的 Aspose.OCR .NET NuGet 包（撰写时为 v23.11）。

---

![如何去倾斜图像示例](/images/deskew-example.png "how to deskew image")

*上图展示了扫描文档在去倾斜前后的对比。*

## 前置条件

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）。  
* Visual Studio 2022（或任何你喜欢的 C# IDE）。  
* Aspose.OCR NuGet 包 – 通过 `dotnet add package Aspose.OCR` 安装。  

就这些。无需外部服务，也不需要 API 密钥。

---

## 如何使用 Aspose OCR 去倾斜图像

我们首先创建一个 **ImageProcessingPipeline** 并添加 `DeskewFilter`。该过滤器会自动检测主要文字行的角度并将图像旋转回水平。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**为什么这很重要：**  
倾斜的扫描会让 OCR 引擎困惑，因为字符不再与基线对齐。`DeskewFilter` 会分析图像直方图，找出倾斜角度并进行旋转，从而显著提升识别准确率。

> **专业提示：** 如果你的文档倾斜角度永远不超过 15°，可以将 `MaxAngle = 15` 以加快处理速度。

---

## 如何提升对比度以获得更佳识别效果

去倾斜后，下一步是让文字更突出。`ContrastBoostFilter` 会拉伸像素强度范围，对褪色的打印尤其有效。

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**为什么它有帮助：**  
低对比度的扫描会产生灰色字符，二值化器可能会把它们误判为背景。提升对比度会让暗像素更暗、亮像素更亮，为后续的 `BinarizationFilter` 提供更干净的画布。

---

## 对图像执行 OCR – 加载文件

现在图像已经预处理完毕，我们需要 **load image for OCR**。Aspose 提供了便利的 `ImageStream.FromFile` 辅助方法。

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

如果你的图像位于流中（例如通过 Web API 上传），可以改用 `ImageStream.FromStream(yourStream)`。引擎支持 BMP、JPEG、PNG、TIFF 等多种格式。

---

## 运行识别过程并提取扫描文本

所有步骤就绪后，调用 `Recognize()` 即可完成繁重的工作。调用结束后，识别得到的文本可通过 `ocrEngine.Text` 访问。

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**预期输出**（以下为简单发票的示例）：

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

如果输出出现乱码，请再次检查管道顺序——先去倾斜，再去噪声、提升对比度，最后二值化。顺序错误会导致结果下降。

---

## 常见陷阱与边缘情况

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| **结果为空** | 图像过暗或过亮，默认二值化方法无法处理。 | 增加 `ContrastBoostFilter.Strength` 或切换到 `BinarizationMethod.Otsu`。 |
| **部分文字缺失** | 去噪后仍残留噪声。 | 对较轻的图像使用 `DenoiseLevel.Medium`，或添加第二个 `DenoiseFilter`。 |
| **旋转方向错误** | 文档存在混合方向（例如拍摄了已旋转的页面）。 | 手动降低 `DeskewFilter.MaxAngle`，并使用 `ImageProcessor.Rotate` 预先旋转图像。 |
| **性能下降** | 大批量高分辨率图像。 | 在管道前使用 `ImageProcessor.Resize` 降低分辨率，或使用 `Parallel.ForEach` 并行处理。 |

---

## 完整可运行示例（复制粘贴即用）

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

将其保存为 `Program.cs`，运行 `dotnet run`，即可在控制台看到 **extract text from scan** 的结果。

---

## 后续步骤与相关主题

* **批量处理** – 将上述逻辑封装在循环中，以一次处理 dozens of files。  
* **自定义语言包** – 若需读取非拉丁文字，可通过 `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;` 加载语言模型。  
* **PDF 输出** – 将 Aspose.PDF 与 OCR 结合，直接在 PDF 中嵌入可搜索文本。  
* **性能调优** – 试验 `ImageProcessingPipeline` 的顺序；有时在去倾斜前先去噪会在噪声较大的照片上更快。  

所有这些都基于我们已经讨论的核心概念：**how to deskew image**、**how to boost contrast**、**load image for OCR**、**perform OCR on image**，以及最终的 **extract text from scan**。

---

## 总结

我们刚刚演示了一种完整、可投入生产的方式来 **how to deskew image** 并在 C# 中运行 OCR。通过串联去倾斜过滤器、去噪步骤、对比度提升以及二值化，你可以得到干净的输入，让 Aspose OCR 可靠地 **extract text from scan**。

试着运行代码，根据自己的文档微调过滤器参数，你会立刻看到识别准确率的提升。有任何问题请留言，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}