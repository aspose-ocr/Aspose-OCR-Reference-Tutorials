---
category: general
date: 2025-12-30
description: 使用 Aspose OCR 在 C# 中将图像转换为 PDF。学习如何对图像进行 OCR 预处理，识别韩文文本图像，并快速创建可搜索的 PDF
  图像。
draft: false
keywords:
- convert image to pdf
- preprocess image for ocr
- recognize korean text image
- create searchable pdf image
language: zh
og_description: 使用 Aspose OCR 将图像转换为 PDF。本教程展示了如何对图像进行 OCR 预处理，识别韩文文本图像，并创建可搜索的 PDF
  图像。
og_title: 在 C# 中将图像转换为 PDF – 完整 OCR 指南
tags:
- C#
- OCR
- Aspose
- PDF
title: 在 C# 中将图像转换为 PDF – 完整 OCR 指南
url: /zh/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中将图像转换为 PDF – 完整 OCR 指南

是否曾经需要 **convert image to PDF**，但又希望其中的文本可搜索？你并不是唯一的。许多开发者在处理扫描页，尤其是韩文时，都会遇到同样的难题。好消息是，使用 Aspose OCR，你可以 **preprocess image for OCR**、**recognize Korean text image**，并最终 **create searchable PDF image**，只需几行代码。

在本教程中，我们将完整演示整个流程——从加载韩文书籍页面的原始 JPEG、清理图像、提取文本，到将所有内容封装为可搜索的 PDF。完成后，你将拥有一个可直接运行的 C# 控制台应用程序，能够放入任何 .NET 项目中使用。

## 您需要的环境

- **.NET 6.0 或更高**（代码在 .NET Core 和 .NET Framework 上均可运行）  
- **Aspose.OCR for .NET** NuGet 包（`Aspose.OCR`）——免费试用密钥可在 Aspose 官网获取。  
- 包含韩文文本的示例图像（例如 `korean_book_page.jpg`）。  
- 你喜欢的开发环境（Visual Studio、VS Code、Rider——我使用 VS 2022）。

> **Pro tip:** 将图像文件放在专用文件夹如 `Resources/` 中，以确保路径在不同机器上保持一致。

## 过程概览

1. **使用 GPU 加速初始化 OCR 引擎**，提升速度。  
2. **添加预处理过滤器**（去倾斜、去噪），提高识别准确率。  
3. **下载并加载韩文语言模型**——如有需要，Aspose 会自动完成。  
4. **对输入图像执行识别**。  
5. **使用内置导出器将结果导出为可搜索的 PDF**。  
6. **可选：将结果序列化为 JSON**，便于后续分析或日志记录。

下面我们将逐步拆解每一步，解释 *为什么* 重要，并提供可以直接复制粘贴的完整代码。

---

## ## 将图像转换为 PDF – 完整工作流

以下代码片段是 *完整* 程序。你可以新建一个控制台项目（`dotnet new console -n OcrPdfDemo`），然后用下面的代码替换自动生成的 `Program.cs`。

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

- **GPU 加速** 将识别时间大幅缩短，约为仅使用 CPU 时的一半。  
- **Deskew** 与 **Denoise** 是经典的 *preprocess image for OCR* 技术；它们修正常见的扫描缺陷，防止引擎漏掉字符。  
- **语言模型加载** 对 **recognize Korean text image** 至关重要——没有韩文模型，引擎会回退到通用的拉丁字母模型，输出乱码。  
- **SearchablePdfExporter** 将原始位图与不可见的文本层捆绑，生成 **create searchable pdf image** 的结果，能够在任何 PDF 查看器中被索引。

---

## ## 预处理图像以进行 OCR – 小技巧与技巧

虽然我们添加的两个过滤器通常已足够，但有时会遇到顽固的图像。以下是一些可尝试的额外步骤：

| 问题 | 附加过滤器 | 如何添加 |
|-------|-------------------|------------|
| 对比度低 | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| 背景噪声严重 | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| 方向混杂（竖版与横版） | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **注意：** 添加过多过滤器会降低处理速度。请在单页上测试每项更改后再批量应用。

---

## ## 识别韩文文本图像 – 常见陷阱

韩文字符密集且形态复杂。如果出现乱码输出，请尝试以下措施：

1. **确保语言模型已完整下载**——在控制台中查找类似 “Downloading Korean model…” 的提示。  
2. **在 DeskewFilter 中增大 `MaxAngle`**，如果扫描图像的旋转角度超过 12°。  
3. **通过设置 `ocrEngine.GpuMemoryLimit = 2048;`（单位 MB）提升 GPU 内存**。

这些调整直接影响 **recognize Korean text image** 的成功率。

---

## ## 创建可搜索的 PDF 图像 – 验证结果

程序执行完毕后，用任意 PDF 阅读器（Adobe Acrobat Reader、Foxit，甚至 Chrome）打开 `korean_page.pdf`。你应该能够：

- **使用鼠标选取文本**，就像原生 PDF 一样。  
- **在搜索框中搜索韩文字词**。

如果文本层为空，请再次确认 `Export` 方法接收了正确的图像路径，并且 OCR 结果的 `RecognitionResult.Text` 非空。

---

## ## 完整 JSON 输出 – 预期内容

控制台会打印格式化的 JSON 负载。以下是一个裁剪后的示例：

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

你可以将此 JSON 直接喂给下游服务（例如索引管道、翻译 API），而无需重新运行 OCR。

---

## ## 故障排查 & FAQ

**Q: 我的 PDF 与原始图像相比体积太大。**  
A: 导出器会以原始分辨率嵌入位图。如果文件大小是个问题，请在识别前**先缩小图像**：

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: OCR 返回空字符串。**  
A: 请确认图像路径正确且文件未损坏。同时，确保 GPU 驱动是最新的；旧版驱动可能导致静默失败。

**Q: 能否在循环中处理多页？**  
A: 完全可以。将第 4‑6 步包装在 `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` 循环中，并相应更改输出 PDF 的路径。

---

## ## 结论

我们已经使用 Aspose OCR 的强大管道，实现了 **convert image to PDF** 并保留可搜索文本。通过 **preprocess image for OCR** 提升准确率；通过 **recognize Korean text image** 处理复杂脚本；通过 **create searchable pdf image** 获得可携带、可索引的文档。

获取代码，指向你的扫描文件，尝试添加更多过滤器或语言模型。同样的模式也适用于中文、日文或任何基于拉丁字母的语言——只需将 `LanguageModel.Korean` 替换为相应的枚举即可。

还有其他问题吗？留下评论吧，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}