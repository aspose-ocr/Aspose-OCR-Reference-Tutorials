---
category: general
date: 2026-07-05
description: 使用 Aspose.OCR 在 C# 中对图像执行 OCR。了解如何加载图像进行 OCR、在 OCR 前对图像进行预处理，以及从收据中提取文本，同时提升
  OCR 准确率。
draft: false
keywords:
- perform OCR on image
- extract text from receipt
- improve OCR accuracy
- load image for OCR
- preprocess image before OCR
language: zh
og_description: 使用 Aspose.OCR 在 C# 中对图像进行 OCR。本教程展示了如何加载图像进行 OCR、在 OCR 前对图像进行预处理，以及从收据中提取文本以提升
  OCR 准确率。
og_title: 使用 Aspose 对图像进行 OCR – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Aspose.OCR in C#. Learn how to load image
    for OCR, preprocess image before OCR, and extract text from receipt while improving
    OCR accuracy.
  headline: Perform OCR on Image with Aspose – Complete C# Guide
  type: TechArticle
- description: Perform OCR on image using Aspose.OCR in C#. Learn how to load image
    for OCR, preprocess image before OCR, and extract text from receipt while improving
    OCR accuracy.
  name: Perform OCR on Image with Aspose – Complete C# Guide
  steps:
  - name: '**Load** the picture file into memory.'
    text: '**Load** the picture file into memory.'
  - name: '**Preprocess** it: deskew, denoise, and boost contrast.'
    text: '**Preprocess** it: deskew, denoise, and boost contrast.'
  - name: '**Run** the OCR engine.'
    text: '**Run** the OCR engine.'
  - name: '**Read** the resulting text.'
    text: '**Read** the resulting text.'
  type: HowTo
- questions:
  - answer: Aspose.OCR works best with printed text. For cursive or mixed fonts you
      may need a specialized handwriting model or a different library.
    question: What if the receipt is handwritten?
  - answer: Yes—convert each PDF page to an image (`Aspose.PDF` can help) and feed
      those images into the same pipeline.
    question: Can I process PDFs directly?
  - answer: Wrap the core logic inside a `foreach` loop that iterates over a folder
      of images. Remember to dispose of the `OcrEngine` after each file to free memory.
    question: Is there a way to batch‑process many receipts?
  - answer: Aspose offers a free evaluation with a watermark. For production use,
      purchase a license to remove the watermark and unlock full performance.
    question: Do I need a license?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- Image Processing
title: 使用 Aspose 对图像进行 OCR – 完整 C# 指南
url: /zh/net/ocr-optimization/perform-ocr-on-image-with-aspose-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose 执行图像 OCR – 完整 C# 指南

是否曾经需要 **对图像文件执行 OCR**，但结果模糊、缺字符或完全错误？你并不孤单——扫描收据、发票或手写笔记常常变成猜谜游戏。在本指南中，我们将实战演示如何 **加载图像进行 OCR**，对其进行清理，最终 **从收据中提取文本**，并显著 **提升 OCR 准确率**。

事实是：Aspose.OCR 库提供了整洁的 API，允许你按需堆叠预处理过滤器。完成本教程后，你将拥有一个可直接运行的 C# 控制台应用，能够读取倾斜的收据、去倾斜、去噪背景、增强对比度，并将干净的文本打印到控制台。没有神秘，只是一步步的代码，你可以复制粘贴使用。

## 你将学习的内容

- 如何使用 Aspose 的 `ImageStream` **加载图像进行 OCR**。
- 哪些 **在 OCR 前预处理图像** 的过滤器对收据最有效。
- 在不购买昂贵第三方服务的情况下 **提升 OCR 准确率** 的技巧。
- 精确的 **从收据中提取文本** 命令以及如何验证输出。
- 一个完整、可运行的示例，直接放入 Visual Studio 即可使用。

### 前置条件

- .NET 6.0 SDK 或更高（代码同样适用于 .NET Core）。
- 有效的 Aspose.OCR NuGet 包（`Aspose.OCR` 23.9 或更新）。
- 一张示例收据图像（例如 `skewed_receipt.jpg`），放在可引用的文件夹中。
- 对 C# 控制台应用有基本了解。

如果你已经具备以上条件，下面直接进入实战——不废话，只看核心。

---

## 执行图像 OCR – 步骤概览

在编写代码之前，先想象一下整个流水线：

1. **加载** 图片文件到内存。  
2. **预处理**：去倾斜、去噪、增强对比度。  
3. **运行** OCR 引擎。  
4. **读取** 产生的文本。

每个阶段都是拼图的一小块，组合起来即可 **对图像文件执行 OCR**，即使原始文件几乎不可读。下面的章节会逐一拆解。

---

## 加载图像用于 OCR

任何 OCR 工作流的第一步都是获取位图。Aspose 通过 `ImageStream` 抽象了文件处理，这意味着除非你想使用 `System.Drawing`，否则无需手动处理。

```csharp
using Aspose.OCR;
using System;

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Step 2: Load the image you want to recognize
// Replace the path with the actual location of your receipt image
ocrEngine.Image = ImageStream.FromFile(@"C:\OCRDemo\skewed_receipt.jpg");

// Quick sanity check – make sure the image was loaded
if (ocrEngine.Image == null)
{
    Console.WriteLine("Failed to load image. Verify the file path.");
    return;
}
```

> **为什么重要：** 正确加载图像是基础。如果路径错误，后续所有过滤器都会在空引用上悄悄运行，最终得到空结果。上面的检查可以帮助你避免这种尴尬。

---

## 在 OCR 前预处理图像

收据照片常见三大问题：旋转、随机噪点、对比度低。Aspose 自带的三个内置过滤器正好针对这些问题。顺序很重要——先去倾斜，再去噪，最后提升对比度。

```csharp
// Step 3: Add preprocessing filters in the desired order
ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Deskew);          // Corrects image rotation
ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Denoise);        // Reduces noise
ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.ContrastBoost); // Enhances contrast
```

> **小技巧：** 如果你处理的是全部以 300 dpi 扫描的收据批次，可以跳过 `ContrastBoost`，因为扫描仪已经提供了足够的对比度。针对你的数据集进行实验是 **提升 OCR 准确率** 的关键。

---

## 使用过滤器提升 OCR 准确率

图像预处理完成后，OCR 引擎即可大显身手。`Recognize()` 调用会在清理后的位图上运行基于神经网络的识别器。

```csharp
// Step 4: Perform OCR recognition
ocrEngine.Recognize();
```

在幕后，Aspose 会应用语言特定模型、字符分割以及后处理启发式算法。把去倾斜、去噪、高对比度的图像喂进去，相当于给它一本教材级别的页面——这正是你想要的 **提升 OCR 准确率**。

---

## 从收据中提取文本

最后，从引擎中取出识别后的字符串。`Text` 属性包含原始的 Unicode 结果，你可以将其写入控制台、文件或数据库。

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== Recognized Receipt Text ===");
Console.WriteLine(ocrEngine.Text);
```

典型的收据输出如下所示：

```
=== Recognized Receipt Text ===
Store: QuickMart
Date: 2024-06-15
Item 1  $2.99
Item 2  $5.49
Total   $8.48
Thank you!
```

如果发现缺失数字或字符乱码，请返回预处理步骤——可能需要更强的 `Denoise` 级别或自定义过滤器。好消息是，你可以根据需要堆叠同一过滤器的多个实例。

---

## 完整可运行示例

下面是完整的程序代码，直接复制粘贴即可。保存为 `Program.cs`，恢复 NuGet 包后运行。控制台会显示提取的收据文本。

```csharp
using Aspose.OCR;
using System;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create the OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣  Load the image you want to process
            // -------------------------------------------------
            // Change the path to point at your own receipt file
            string imagePath = @"C:\OCRDemo\skewed_receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image from '{imagePath}'. Check the path and try again.");
                return;
            }

            // -------------------------------------------------
            // 3️⃣  Preprocess the image – this is where we
            //     actually **improve OCR accuracy**
            // -------------------------------------------------
            ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Deskew);
            ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Denoise);
            ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.ContrastBoost);

            // -------------------------------------------------
            // 4️⃣  Run the OCR engine – **perform OCR on image**
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // 5️⃣  Extract and display the text – **extract text from receipt**
            // -------------------------------------------------
            Console.WriteLine("\n=== Recognized Receipt Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### 预期输出

对一张清晰、已去倾斜的收据运行程序，应该会打印出类似前面代码块中示例的文本。如果得到空字符串，请再次检查预处理顺序或尝试提升源图像的 DPI。

---

## 常见问题与注意事项

- **如果收据是手写的怎么办？**  
  Aspose.OCR 对印刷体文字效果最佳。对于草写或混合字体，可能需要专门的手写模型或其他库。

- **可以直接处理 PDF 吗？**  
  可以——先将每页 PDF 转为图像（`Aspose.PDF` 可协助），再将这些图像送入相同的流水线。

- **如何批量处理大量收据？**  
  将核心逻辑包装在 `foreach` 循环中，遍历文件夹中的图像。记得在每个文件处理完后释放 `OcrEngine`，以免占用过多内存。

- **需要许可证吗？**  
  Aspose 提供带水印的免费评估版。生产环境请购买许可证，以去除水印并解锁全部性能。

---

## 结论

我们已经完整演示了如何使用 Aspose.OCR **对图像文件执行 OCR**，从 **加载图像进行 OCR** 到 **在 OCR 前预处理图像**，再到 **从收据中提取文本**。通过按顺序应用去倾斜、去噪和对比度提升过滤器，通常可以显著 **提升 OCR 准确率**——尤其是对低质量的收据扫描。

接下来可以尝试添加语言提示（`ocrEngine.Language = Language.English;`）或实验自定义过滤器进行颜色反转。你甚至可以把提取的文本管道到一个简单的解析器，自动抽取项目明细和总额。

如果本教程帮助你突破了常见的 OCR 难题，请在 GitHub 上给项目点星或在下方留言。祝编码愉快，愿你的收据永远可读！

![展示帮助你对图像执行 OCR 的预处理流水线的示意图] 

---


## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并在项目中探索替代实现方式。每篇资源都提供完整可运行的代码示例和逐步解释。

- [从图像中提取文本 – 使用 Aspose.OCR 进行 .NET OCR 优化](/ocr/english/net/ocr-optimization/)
- [如何使用 AspOCR：.NET 图像 OCR 预处理过滤器](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [使用 Aspose.OCR 进行语言选择的 C# 图像文字提取](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}