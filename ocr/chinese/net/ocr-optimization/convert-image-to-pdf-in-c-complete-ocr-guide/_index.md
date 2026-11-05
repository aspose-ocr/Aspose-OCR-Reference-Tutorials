---
category: general
date: 2026-09-13
description: 了解如何使用 Aspose OCR 在 C# 中将扫描页转换为 PDF。本指南展示了图像预处理、韩文文本识别以及创建可搜索 PDF 的方法。
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: 了解如何使用 Aspose OCR 在 C# 中将扫描页转换为 PDF。教程涵盖图像预处理、GPU‑accelerated OCR
  用于韩文文本，以及在几分钟内生成可搜索的 PDF。
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: 如何在 C# 中使用 OCR 将扫描页转换为 PDF
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: 如何在 C# 中使用 OCR 将扫描页转换为 PDF
url: /zh/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR 将扫描页转换为 PDF

如果您需要**将扫描页转换为 PDF**并保持文本可搜索，那么您来对地方了。本教程将指导您使用 Aspose OCR 来**预处理图像以进行 OCR**、**识别韩文图像**，以及最终**创建可搜索 PDF 图像**——全部通过一个简单的 C# 控制台应用程序完成。

## 快速答案
- **哪个库负责 OCR？** Aspose.OCR for .NET  
- **我可以使用 GPU 吗？** 是的 – 启用 GPU 加速可提升至 2 倍的处理速度  
- **我需要韩语语言包吗？** 它会在首次使用时自动下载  
- **输出会是可搜索的吗？** 生成的 PDF 包含不可见的文本层  
- **支持哪些 .NET 版本？** .NET 6.0 或更高（包括 .NET Core 和 .NET Framework）

## 要求

- **.NET 6.0 或更高** – 在 .NET Core、.NET Framework 和 .NET 5/6+ 上均可工作  
- **Aspose.OCR for .NET** NuGet 包 (`Aspose.OCR`) – 试用密钥可在 Aspose 网站免费获取  
- 一个包含韩文字符的示例图像，例如 `korean_book_page.jpg`  
- 您喜欢的 IDE（Visual Studio 2022、VS Code、Rider 等）

> **专业提示：** 将图像存放在 `Resources/` 文件夹中，以便路径在不同机器间保持一致。

## 流程概述

1. 使用 GPU 支持初始化 OCR 引擎。  
2. 添加 **预处理图像以进行 OCR** 过滤器，例如去倾斜和去噪。  
3. 下载并加载韩语语言模型（自动处理）。  
4. 对图像运行 OCR。  
5. 使用 **SearchablePdfExporter** 导出结果，以 **创建可搜索 PDF 图像**。  
6. （可选）将 OCR 输出序列化为 JSON，以供下游流水线使用。  

下面我们展开每一步，解释*原因*以及提供您可以直接复制粘贴的完整代码。

## 扫描页转 PDF 转换是如何工作的？

`OcrEngine` 是 Aspose.OCR 中执行图像光学字符识别的主要类。  
`SearchablePdfExporter` 创建一个包含原始图像和用于搜索的不可见文本层的 PDF。  
`RecognitionResult` 保存 OCR 引擎返回的文本和置信度数据。  

使用 `new OcrEngine()` 加载图像并调用 `engine.Recognize("korean_book_page.jpg")`，然后将 `RecognitionResult` 传递给 `SearchablePdfExporter.Export`。此两步流程读取位图，提取 Unicode 文本，并将两者嵌入单个 PDF，其中文本层不可见但可搜索。GPU 加速将识别时间大约缩短一半，而去倾斜和去噪过滤器在噪声扫描上可将准确率提升至 15 %。

## 将图像转换为 PDF – 完整工作流

以下代码片段是*完整*程序。创建一个新的控制台项目（`dotnet new console -n OcrPdfDemo`），并用占位符中显示的代码替换自动生成的 `Program.cs`。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### 为什么这样有效

- **GPU 加速** 将识别时间大约缩短一半，相比仅使用 CPU 的模式。  
- **Deskew** 和 **Denoise** 是经典的 *预处理图像以进行 OCR* 技术；它们纠正常见的扫描缺陷，否则会导致引擎漏掉字符。  
- **语言模型加载** 对于 **recognize Korean text image** 至关重要——没有韩语模型，引擎将回退到通用的拉丁字母并产生乱码。  
- **SearchablePdfExporter** 将原始位图和不可见的文本覆盖层捆绑在一起，为您提供 **create searchable pdf image** 结果，您可以在任何 PDF 查看器中进行索引。

## 为什么这样有效

- **GPU 加速** 将识别时间大约缩短一半，相比仅使用 CPU 的模式。  
- **Deskew** 和 **Denoise** 是经典的 *预处理图像以进行 OCR* 技术；它们纠正常见的扫描缺陷，否则会导致引擎漏掉字符。  
- **语言模型加载** 对于 **recognize Korean text image** 至关重要——没有韩语模型，引擎将回退到通用的拉丁字母并产生乱码。  
- **SearchablePdfExporter** 将原始位图和不可见的文本覆盖层捆绑在一起，为您提供 **create searchable pdf image** 结果，您可以在任何 PDF 查看器中进行索引。

## 预处理图像以进行 OCR – 提示与技巧

`DeskewFilter` 校正扫描页的旋转。  
`ContrastFilter` 调整图像对比度以提升 OCR 准确率。  
`BinarizationFilter` 根据阈值将图像转换为黑白，从而降低背景噪声。  
`OrientationFilter` 检测并校正混合的纵向/横向页面。  

| 问题 | 附加过滤器 | 如何添加 |
|-------|-------------------|------------|
| 低对比度 | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| 严重背景噪声 | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| 混合方向（纵向 & 横向） | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **注意：** 添加过多过滤器会减慢处理速度。在扩大规模之前，请在单页上测试每项更改。

## 识别韩文图像 – 常见陷阱

韩文脚本包含视觉上密集的韩文字母。如果您发现输出乱码：

1. **确保语言模型已完整下载** – 在控制台检查类似 “Downloading Korean model…” 的信息。  
2. **在 `DeskewFilter` 中增加 `MaxAngle`**，如果您的扫描图像旋转超过 12°。  
3. **通过设置 `ocrEngine.GpuMemoryLimit = 2048;`（单位为 MB）来提升 GPU 内存。**  

`LanguageModel.Korean` 为 OCR 加载韩语语言数据，使得韩文字母识别准确。  
这些调整直接影响 **recognize Korean text image** 的成功率。

## 创建可搜索 PDF 图像 – 验证结果

程序完成后，在任何 PDF 阅读器（Adobe Acrobat Reader、Foxit，甚至 Chrome）中打开 `korean_page.pdf`。您应该能够：

- **使用鼠标选择文本**，就像它是原生 PDF 一样。  
- **使用内置搜索框**搜索韩语单词。  

如果文本层显示为空，请再次确认 `Export` 方法接收了正确的图像路径，并且 OCR 结果的 `RecognitionResult.Text` 非空。

## 完整 JSON 输出 – 预期内容

控制台会打印格式良好的 JSON 负载。以下是一个精简示例：

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## 故障排除 & 常见问题

**Q: 我的 PDF 与原始图像相比太大。**  
**A:** 导出器以原始分辨率嵌入位图。如果大小是问题，请在识别之前*缩小*图像：

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: OCR 返回空字符串。**  
**A:** 确认图像路径正确且文件未损坏。同时，确保 GPU 驱动程序是最新的；旧版驱动可能导致静默失败。

**Q: 我可以在循环中处理多页吗？**  
**A:** 当然可以。将步骤 4‑6 包装在 `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` 循环中，并相应更改输出 PDF 的路径。

## 结论

我们刚刚**将图像转换为 PDF**并保留可搜索的文本，这全靠 Aspose OCR 强大的流水线。通过 **preprocess image for OCR**，您提升了准确率；通过 **recognize Korean text image**，您处理了复杂的脚本；通过 **create searchable pdf image**，您获得了可携带、可索引的文档。

获取代码，将其指向您自己的扫描件，并尝试额外的过滤器或语言模型。同样的模式适用于中文、日文或任何基于拉丁字母的语言——只需将 `LanguageModel.Korean` 替换为相应的枚举即可。

还有其他问题吗？留下评论，祝编码愉快！

**最后更新：** 2026-09-13  
**测试使用：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose

## 相关教程

- [使用 Aspose Ocr 从扫描文件创建可搜索 PDF](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [OCR 预处理流水线：如何从图像识别文本](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [使用 Aspose Ocr 从图像识别文本的完整 C 指南](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}