---
category: general
date: 2026-02-28
description: 在 C# 中通过垂直合并图像创建可搜索的 PDF。了解如何垂直堆叠图像并使用 Aspose OCR 将扫描页转换为 PDF。
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: zh
og_description: 在 C# 中通过垂直合并图像创建可搜索的 PDF。本指南展示了如何将图像垂直堆叠并使用 Aspose OCR 将扫描页面转换为 PDF。
og_title: 在 C# 中创建可搜索的 PDF – 垂直合并图像
tags:
- Aspose OCR
- C#
- PDF generation
title: 使用 C# 创建可搜索的 PDF – 垂直合并图像
url: /zh/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建可搜索 PDF – 垂直合并图像

是否曾经需要 **从少量扫描的 PNG 创建可搜索 PDF**，却不知从何入手？你并不孤单。在许多文档自动化项目中，最大痛点就是将一堆图像文件转换为一个整洁、可搜索的 PDF，以便索引和共享。

在本教程中，我们将演示一个完整、可直接运行的示例，展示如何 **垂直堆叠图像**、**垂直合并图像**，以及最终使用 Aspose.OCR 的 GPU 加速引擎将 **扫描页面 PDF** 转换为单个可搜索文档。完成后，你将拥有一个可直接嵌入任何 .NET 解决方案的自包含程序。

> **你将学到**
> - 使用 GPU 支持初始化 OCR 引擎。
> - 并行处理一批图像。
> - **垂直合并图像** 以模拟多页扫描。
> - 导出可搜索 PDF 并生成详细的 JSON 报告，以供后续分析使用。

## 前置条件

- .NET 6+（代码可在 .NET 6、.NET 7 或 .NET 8 上编译）
- Aspose.OCR NuGet 包（`Install-Package Aspose.OCR`）
- 若想使用 `ProcessingMode.Gpu` 设置，需要一台支持 GPU 的机器（CPU 回退同样可用）
- 一个包含若干扫描 PNG/JPEG 文件的文件夹（演示使用 `page1.png`、`page2.png`、`page3.png`）

无需外部服务、无需隐藏配置文件——纯 C#。

## 第一步 – 设置 OCR 引擎以 **创建可搜索 PDF**

首先创建 `OcrEngine`，开启 GPU 加速，选择英语作为语言，并添加几个预处理过滤器。这些过滤器通过校正倾斜页面（`DeskewFilter`）和去除噪声（`DenoiseFilter`）来提升识别准确度。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**为什么重要：** OCR 引擎负责繁重的文字识别工作。启用 `ProcessingMode.Gpu` 能在现代显卡上将识别时间减半，而这些过滤器则能消除常见的扫描伪影，避免输出乱码。

## 第二步 – 配置批处理器以高效 **转换扫描页面 PDF**

逐页处理对于少量图像尚可，但实际项目常常涉及数十甚至数百页。Aspose.OCR 的 `OcrBatchProcessor` 让我们能够并行执行识别，大幅加速 **转换扫描页面 pdf** 步骤。

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**小技巧：** 如果只有 CPU，设置 `ProcessingMode = ProcessingMode.Cpu`。批处理器仍会遵循 `MaxDegreeOfParallelism`，你可以调节它以防机器过载。

## 第三步 – 对批次运行 OCR 并收集结果

现在真正进行文字识别。`Recognize` 方法返回一个 `OcrResult` 对象列表，每个对象都包含原始图像和提取的文本。

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

此时你已经拥有创建 **可搜索 PDF** 所需的一切：内存中的图像以及对应的文字层。

## 第四步 – **垂直合并图像** 并生成可搜索 PDF

大多数扫描文档都是多页 PDF，因此我们需要将各页图像拼接成一张高图，模拟实际的纸张堆叠。Aspose.OCR 提供的 `Image.CombineVertical` 正是为此而生。

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

生成的文件（`combined_searchable.pdf`）在每页图像下方包含可选择、可搜索的文字——这正是从扫描源 **创建可搜索 PDF** 所需的效果。

![创建可搜索 PDF 示例](/images/create-searchable-pdf.png "创建可搜索 PDF 示例")

*图片替代文字：创建可搜索 PDF 示例，展示合并后的 PDF 及其可搜索文字层。*

**为什么采用垂直堆叠？** 许多 OCR 库会把每张图像当作单独的页。通过堆叠，我们保持 PDF 页序不变，同时只需一次 OCR 即可处理整份文档。

## 第五步 – 为首页导出详细 JSON（便于后续工作流）

有时仅有 PDF 不够；你可能需要将 OCR 数据写入数据库或喂给机器学习管道。Aspose.OCR 允许将每个 `OcrResult` 序列化为 JSON，保留边界框、置信度等信息。

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**预期的 JSON 片段（已截断）：**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

现在你可以将该 JSON 输入任意下游系统——无论是将文本索引到 Elasticsearch，还是送入自定义分析仪表板。

---

## 如何 **垂直堆叠图像** – 快速回顾

如果你想在不使用 Aspose 的情况下 **垂直堆叠图像**，可以使用 `System.Drawing` 创建新位图并依次绘制每页。然而，Aspose 内置的 `Image.CombineVertical` 已经帮你处理了 DPI、像素格式和内存管理，是生产代码中最可靠的选择。

### 备选方案：使用 `System.Drawing`（仅作好奇心探索）

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

手动方式可行，但会失去自动 DPI 处理的便利，也无法直接将结果喂给 `RecognizeToPdf`。除非有非常特殊的需求，否则请坚持使用 `CombineVertical`。

## 常见陷阱与规避方法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| **处理大量高分辨率扫描时出现内存不足** | 每张图像在写入 PDF 前都会驻留在内存中 | 在不再使用时立即释放 `Image` 对象（使用 `using` 块），或在合并前降低图像分辨率 |
| **OCR 后出现乱码** | 扫描倾斜或对比度低 | 保持使用 `DeskewFilter` 与 `DenoiseFilter`；必要时添加 `ContrastFilter` |
| **缺少可搜索层** | 调用了 `Recognize` 而非 `RecognizeToPdf` | 确保在合并图像后调用 `ocrEngine.RecognizeToPdf` |
| **在没有合适驱动的机器上 GPU 回退失败** | `ProcessingMode.Gpu` 抛出异常 | 将引擎创建包装在 try/catch 中，出现异常时回退到 `ProcessingMode.Cpu` |

## 后续步骤 – 扩展工作流

了解了如何 **创建可搜索 PDF** 后，你可能想要：

- 使用 `Directory.GetFiles` 和 `foreach` 循环 **批量处理整个文件夹**。
- 在合并前为每页 **添加水印**（使用 Aspose.Imaging 的 `ImageProcessor`）。
- 若需要单页 PDF，**将可搜索 PDF 再拆分为独立页面**（使用 Aspose.PDF 的 `PdfDocument.Split`）。
- **集成 Azure Blob Storage**，从云端拉取图像并将最终 PDF 推回云端。

所有这些扩展都围绕相同的核心概念：OCR 配置、图像处理以及 PDF 导出。

---

## 结论

我们已经覆盖了在 C# 中从一组扫描图像 **创建可搜索 PDF** 所需的全部步骤。通过初始化支持 GPU 的 `OcrEngine`、使用 `OcrBatchProcessor` 并行批处理、**垂直合并图像**，以及最终调用 `RecognizeToPdf`，即可得到整洁、可搜索的文档，适合归档或索引。额外的 JSON 导出为 OCR 结果提供了完整可视化，为分析或自定义工作流打开了大门。

动手试一试，尝试不同的过滤器，让你的文档自动化流水线更加顺畅。如遇到任何问题，欢迎留言——祝编码愉快！

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}