---
category: general
date: 2026-05-28
description: 使用 Aspose 在 C# 中进行韩语 OCR 教程。学习如何从流加载图像、提取纯文本、将图像转换为 PDF 并导出可搜索的 PDF。
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: zh
og_description: 使用 Aspose 在 C# 中进行韩语 OCR。一步步指南：从流加载图像、提取纯文本、将图像转换为 PDF 并导出可搜索的 PDF。
og_title: 韩语 OCR – 将图像转换为 PDF 并提取文本（C# 指南）
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 使用 Aspose 进行韩语 OCR：将图像转换为 PDF 并在 C# 中提取文本
url: /zh/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose 进行韩语 OCR：将图像转换为 PDF 并在 C# 中提取文本

有没有想过在不将图片上传到云端的情况下运行 **Korean Language OCR**？你并不是唯一有此需求的人。无论是数字化街道标识、处理收据，还是构建多语言搜索索引，能够在本地识别韩文字字符都能为你节省时间、金钱并避免隐私困扰。

在本教程中，我们将逐步演示一个完整且可运行的示例，展示如何 **load image from stream**、**extract plain text**、**convert image to PDF**，以及最终 **export searchable PDF**——全部使用 Aspose.OCR 和几行 C# 代码。无需外部服务，也没有隐藏的魔法——仅仅是可以直接放入任意控制台应用的纯 .NET 代码。

## 你将收获的内容

- 一个能够通过文件流读取 JPEG 文件的可运行控制台程序。  
- 以纯 Unicode 字符串形式提取的韩文文本。  
- 用于调试或分析的 OCR 运行详细 JSON 报告。  
- 一个可搜索的 PDF，你可以在任何 PDF 阅读器中打开并实际选中韩文字词。  

**Prerequisites**  
- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）。  
- 已安装 Aspose.OCR for .NET NuGet 包（`Install-Package Aspose.OCR`）。  
- 包含 `korean_sign.jpg` 的文件夹以及用于输出文件的可写位置。  

如果你已经准备好上述所有内容，太好了——让我们动手实践吧。

## 步骤 1：初始化用于韩语 OCR 的 OCR 引擎

首先需要一个 `OcrEngine` 实例。启用 GPU（如果有的话）可以显著加快识别速度，而关闭自动资源下载则强制库使用你提供的离线语言包。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **为什么这很重要：**  
> *GPU 加速* 可以将大批量处理时间从秒级降低到毫秒级。将 `AutomaticResourceDownload` 设置为 `false` 可确保演示在离线环境下运行——这对许多企业环境来说是关键需求。

## 步骤 2：从流加载图像

通过流读取图像可以提供灵活性：你可以从磁盘、网络共享，甚至内存缓存的 Blob 中获取文件。这里我们打开本地 JPEG 文件，但相同的模式适用于任何 `Stream`。

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **专业提示：** 如果需要处理通过 Web API 上传的图像，只需将 `File.OpenRead` 替换为传入的 `IFormFile.OpenReadStream()`——其余代码保持不变。

## 步骤 3：选择韩语并应用预处理过滤器

Aspose.OCR 支持少量预处理步骤，可在识别前清理图像。对于韩语标识，去倾斜和去噪通常已足够。

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **内部原理是什么？**  
> `Deskew` 过滤器会校正倾斜的文字，而 `Denoise` 去除可能干扰字符分类器的颗粒噪声。跳过这些步骤往往会导致输出乱码，尤其是在低分辨率照片上。

## 步骤 4：异步提取纯文本

现在是关键时刻——让引擎识别字符并返回干净的字符串。使用 `RecognizeAsync` 可以在将其嵌入桌面或 Web 应用时保持 UI 响应。

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

运行程序后，你应该会看到类似如下的输出：

```
OCR complete. Extracted text:
서울시청
```

> **为什么使用 async？**  
> OCR 可能会占用大量 CPU。异步执行可以防止线程阻塞，这在 ASP.NET Core 中尤为有用，因为线程饥饿是一个真实的顾虑。

## 步骤 5：获取详细识别结果并保存为 JSON

有时你需要的不止原始字符串——可能还想要置信度分数、边界框或原始图像数据。`RecognizeDetailed` 方法返回一个 `RecognitionResult` 对象，可序列化为 JSON 以供后续分析。

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

打开 `korean_ocr.json` 将显示类似以下结构的内容：

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **何时使用此功能？**  
> 如果你在构建搜索索引，置信度值可以帮助过滤低质量结果。如果需要在 UI 中高亮显示文本，边界框就是你的映射。

## 步骤 6：将图像转换为 PDF 并导出可搜索 PDF

Aspose 让从光栅到矢量的转换变得轻而易举。将 `OutputFormat` 设置为 `SearchablePdf`，库会嵌入原始图像并覆盖一层包含 OCR 输出的不可见文本层。生成的 PDF 可像普通 PDF 一样进行搜索、复制和索引。

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

在 Adobe Reader 或任意 PDF 查看器中打开 `korean_searchable.pdf`，按 **Ctrl+F**，输入韩语单词，即可看到它跳转到页面的确切位置。这就是可搜索 PDF 的强大之处。

> **额外提示：** 如果只需要不带隐藏文本层的普通视觉 PDF，只需将 `OutputFormat` 改为 `Pdf`。

## 完整可运行示例

下面是完整的程序——复制粘贴后，将 `YOUR_DIRECTORY` 替换为实际路径，然后按 **F5** 运行。

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### 预期的控制台输出

```
OCR complete. Extracted text:
서울시청
```

你会在源图像旁边看到三个新文件：

- `korean_ocr.json` – 完整的识别数据。  
- `korean_searchable.pdf` – 可搜索的 PDF。  
- （可选）任何你选择添加的中间日志。

## 常见问题与边缘情况

**如果没有 GPU 怎么办？**  
将 `EnableGpu = false`；CPU 回退对小批量完全足够。

**我可以一次处理多张图像吗？**  
当然可以。将核心逻辑包装在 `foreach (var file in Directory.GetFiles(...))` 循环中，并在每次迭代中重新赋值 `ocrEngine.Image`。

**如何同时处理韩语和其他语言？**  
Aspose.OCR 允许你将 `Language = Language.AutoDetect`，或使用按位或运算符组合语言（例如 `Language.Korean | Language.English`）。

**如果 OCR 置信度低怎么办？**  
检查 `detailedResult.Pages[0].Words` 并过滤掉 `Confidence < 0.7` 的条目。你也可以调整预处理过滤器——尝试添加 `PreprocessFilter.ContrastEnhancement`。

## 总结

你已经看到如何端到端执行 **Korean Language OCR**，从 **loading image from stream** 到 **extract plain text**，再到 **convert image to PDF**，最后 **export searchable PDF**。该方法模块化，可随意更换图像来源、修改输出格式，或将 JSON 接入任何下游流水线。

接下来

## 相关教程

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}