---
category: general
date: 2026-08-09
description: 使用 Aspose OCR 在 C# 中从图像提取文本。了解如何加载图像进行 OCR、设置 OCR 语言、处理图像 OCR，以及高效地将图像转换为文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for ocr
- process image ocr
- set ocr language
language: zh
lastmod: 2026-08-09
og_description: 使用 Aspose OCR 在 C# 中提取图像中的文本。本教程展示了如何加载图像进行 OCR、设置 OCR 语言、处理图像 OCR，以及用几行代码将图像转换为文本。
og_image_alt: Screenshot of C# console output showing extracted text from an image
  using Aspose OCR
og_title: 使用 Aspose OCR 从图像提取文本 – C# 指南
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  headline: Extract text from image using Aspose OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  name: Extract text from image using Aspose OCR in C#
  steps:
  - name: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
    text: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
  - name: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
    text: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
  - name: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
    text: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
  - name: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
    text: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
  - name: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
    text: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
  - name: Instantiates `OcrEngine`.
    text: Instantiates `OcrEngine`.
  - name: '**Sets OCR language** to Cyrillic (or any language you choose).'
    text: '**Sets OCR language** to Cyrillic (or any language you choose).'
  - name: '**Loads image for OCR** from disk.'
    text: '**Loads image for OCR** from disk.'
  - name: '**Processes image OCR** to obtain the textual result.'
    text: '**Processes image OCR** to obtain the textual result.'
  - name: '**Converts image to text** and prints it.'
    text: '**Converts image to text** and prints it.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 使用 Aspose OCR 在 C# 中从图像提取文本
url: /zh/net/text-recognition/extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 在 C# 中提取图像文本

如果您需要在 .NET 应用程序中 **从图像中提取文本**，本指南将手把手带您完成一个完整、可直接运行的解决方案。您将看到如何 **加载图像进行 OCR**、选择合适的语言模块、运行 OCR 引擎，最后仅用几行 C# **将图像转换为文本**。

本教程涵盖了使用 Aspose.OCR 获得可靠结果所需的全部内容，包括常见的陷阱（如不受支持的图像格式和语言特定的细微差别）。完成后，您将拥有一个自包含的程序，能够将识别的文本打印到控制台。

## 您将实现的目标

* 将图像文件加载到 Aspose OCR 引擎。  
* **设置 OCR 语言**（示例使用西里尔字母，实际可使用任何受支持的语言）。  
* **处理图像 OCR** 并获取文本表示。  
* **将图像转换为文本** 并显示，后续可用于进一步处理或存储。  

**先决条件**

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.6+）。  
* Visual Studio 2022（或任何支持 C# 的 IDE）。  
* Aspose.OCR NuGet 包（`Install-Package Aspose.OCR`）。  

---

## 提取图像文本 – 完整代码演练

下面是完整的可运行程序。将其复制到新的控制台项目中，并将 `YOUR_DIRECTORY/sample_cyrillic.jpg` 替换为您自己的图像路径。

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create an OCR engine instance.
            // The using block ensures the engine is disposed correctly.
            using (var engine = new OcrEngine())
            {
                // Step 2: Set OCR language.
                // Change OcrLanguage.Cyrillic to any other supported language,
                // e.g., OcrLanguage.English, OcrLanguage.Chinese, OcrLanguage.Hindi.
                engine.Language = OcrLanguage.Cyrillic;

                // Step 3: Load image for OCR.
                // ImageStream.FromFile reads the image from disk.
                // Supported formats: JPEG, PNG, BMP, TIFF, GIF.
                engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.jpg");

                // Step 4: Process image OCR.
                // The Process method runs the recognition engine and returns an OcrResult.
                var result = engine.Process();

                // Step 5: Convert image to text.
                // The recognized text is available via result.Text.
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

### 每一步的重要性

1. **创建 OCR 引擎实例** – `OcrEngine` 封装了所有 OCR 功能。及时释放它可以释放本机资源，这对长期运行的服务至关重要。  
2. **设置 OCR 语言** – 选择正确的语言模块可以显著提升准确率。Aspose 提供 30 多种语言包，默认是英语。示例使用西里尔字母以演示非拉丁脚本。  
3. **加载图像进行 OCR** – 引擎使用 `ImageStream`。提供高分辨率图像（≥300 dpi）可降低误识别，尤其是复杂脚本。  
4. **处理图像 OCR** – 这里完成核心工作。该方法返回包含提取文本、置信度分数以及可选布局数据的 `OcrResult`。  
5. **将图像转换为文本** – `result.Text` 是普通的 `string`。您可以将其写入文件、写入搜索索引，或传递给下游的 NLP 流程。

---

## 加载图像进行 OCR

`ImageStream.FromFile` 方法支持常见的光栅格式。如果您从 Web API 等获取的是字节数组，请改用 `ImageStream.FromBytes(byte[])`：

```csharp
byte[] imageBytes = File.ReadAllBytes("path/to/image.png");
engine.Image = ImageStream.FromBytes(imageBytes);
```

**小技巧：** 在将图像传递给引擎之前，务必先确认图像未损坏。使用 `try { Image.FromFile(...); } catch { ... }` 可以防止运行时异常。

---

## 设置 OCR 语言

Aspose.OCR 随附的语言包可以在运行时启用。要列出所有可用语言：

```csharp
foreach (var lang in Enum.GetValues(typeof(OcrLanguage)))
{
    Console.WriteLine(lang);
}
```

如果需要在同一文档中识别多种语言，可使用按位或运算符组合：

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Russian;
```

**特殊情况：** 将从右到左（RTL）语言（如阿拉伯语）与从左到右脚本混合使用时，可能需要额外的布局处理。Aspose 会自动检测方向，但您可以通过 `engine.PageSegmentationMode` 进行微调。

---

## 处理图像 OCR

`Process` 调用是同步的，会阻塞直到引擎完成。对于大批量或 UI 应用，建议使用异步重载：

```csharp
var task = engine.ProcessAsync();
OcrResult result = await task;
```

**常见陷阱：** 在调用 `Process` 之前忘记设置 `engine.Image` 会抛出 `InvalidOperationException`。请务必先分配图像。

---

## 将图像转换为文本

提取的字符串可以像普通 .NET `string` 一样操作。例如，将输出写入文件：

```csharp
File.WriteAllText("output.txt", result.Text);
```

如果需要保留图像中出现的换行符，请直接使用 `result.Text`。若要进行后处理（如去除多余空白），可使用标准的字符串方法：

```csharp
string cleaned = result.Text
    .Replace("\r\n", "\n")
    .Trim();
```

---

## 完整示例回顾

将所有步骤组合起来，程序的流程如下：

1. 实例化 `OcrEngine`。  
2. **设置 OCR 语言** 为西里尔字母（或您选择的任何语言）。  
3. **加载图像进行 OCR**（从磁盘读取）。  
4. **处理图像 OCR** 以获得文本结果。  
5. **将图像转换为文本** 并打印出来。  

使用清晰的西里尔字母图像运行示例后，输出大致如下：

```
=== Recognized Text ===
Пример текста на кириллице
```

如果图像包含英文文本，只需将 `engine.Language = OcrLanguage.English;`，相同代码即可 **从图像中提取文本**。

---

## 结论

现在您已经掌握了如何在 C# 中使用 Aspose OCR **从图像中提取文本**。本教程涵盖了加载图像、选择合适语言、运行 OCR 过程以及 **将图像转换为文本** 以供后续使用的全部步骤。

接下来您可以：

* 试验其他语言（`load image for OCR` → `set OCR language` → `process image OCR`）。  
* 将 OCR 步骤集成到更大的流水线中（例如文档摄取、可搜索 PDF）。  
* 通过批量处理图像或使用异步 API 来优化性能。

欢迎深入阅读 Aspose.OCR 文档，了解自定义词典、页面分割模式以及 OCR 精度调优等高级功能。祝编码愉快！

## 接下来您应该学习什么？

以下教程与本指南紧密相关，帮助您进一步掌握 API 功能并探索在项目中的其他实现方式。每篇资源都提供完整的可运行代码示例和逐步解释。

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}