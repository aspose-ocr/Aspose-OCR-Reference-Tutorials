---
category: general
date: 2026-06-06
description: 使用 C# OCR 识别文本图像——一步一步的 C# OCR 示例，可从扫描件中提取文本，并在几分钟内将扫描转换为文本。
draft: false
keywords:
- recognize text image
- c# ocr example
- extract text scan
- convert scan to text
- image to text c#
language: zh
og_description: 使用 C# OCR 识别文本图像。学习一个实用的 C# OCR 示例，提取扫描件中的文本，将扫描转换为文本，并处理真实世界的图像。
og_title: 在 C# 中识别文本图像 – 完整 OCR 教程
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text image using C# OCR – a step‑by‑step c# ocr example that
    extracts text from scans and convert scan to text in minutes.
  headline: recognize text image in C# – Full OCR Guide
  type: TechArticle
- questions:
  - answer: The `Windows.Media.Ocr` namespace is Windows‑only. On Linux or macOS you’d
      swap it for TesseractSharp or IronOcr—both expose a similar `Engine.Recognize`
      method, so the surrounding code stays virtually unchanged.
    question: Does this work on .NET Core on Linux?
  - answer: Handwriting recognition is still experimental. For best results, stick
      to printed fonts or consider a cloud service like Azure Cognitive Services if
      you need high accuracy.
    question: How accurate is the built‑in OCR for handwritten notes?
  - answer: 'Not out of the box. Convert each PDF page to an image first (using `PdfSharp`
      or `Ghostscript`) and then feed the bitmap to the OCR engine. --- ## Conclusion
      You now have a complete, production‑ready **c# ocr example** that can **recognize
      text image** files, **extract text scan** contents, and **co'
    question: Can I process PDFs directly?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: 在 C# 中识别文本图像 – 完整 OCR 指南
url: /zh/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中识别文本图像 – 完整 OCR 教程

有没有想过如何直接从扫描的照片中 **识别文本图像**？你并不是唯一的疑问者。无论是数字化旧收据、从名片中提取数据，还是将低分辨率扫描件转换为可编辑文本，能够从图像中提取文字都是每位开发者工具箱中必备的技巧。

在本指南中，我们将演示一个 **c# ocr example**，它加载图片、运行光学字符识别，并将结果打印到控制台。完成后，你将能够 **提取文本扫描** 文件、**将扫描转换为文本**，甚至对噪声图像进行微调。无需任何花哨的第三方服务——只需内置的 Windows.Media.Ocr API（或任何兼容的 OcrEngine）以及几行代码。

## 你将学到的内容

* 如何为 OCR 设置 C# 项目。
* 完整的代码示例，用于 **识别文本图像** 文件。
* 处理低分辨率扫描和多页文档的技巧。
* 将示例扩展为可在自己的应用中复用的库的方法。

### 前置条件

* .NET 6.0 或更高版本（该 API 在 .NET 5+ 上同样可用）。
* Visual Studio 2022（社区版即可）或任意你喜欢的 IDE。
* 一个示例图像，例如 `lowres_scan.jpg`，放置在可引用的文件夹中。
* 对 async/await 有基本了解——Windows API 中的 OCR 调用是异步的。

> **专业提示：** 如果你在非 Windows 平台上开发，使用 `Windows.Media.Ocr` 命名空间的地方换成跨平台库如 TesseractSharp；其余逻辑保持不变。

---

## 步骤 1：使用 OCR 引擎 **识别文本图像**

首先，需要创建一个 OCR 引擎实例。`OcrEngine` 类是任何 **图像转文本 c#** 操作的入口点。

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Create the OCR engine – default language is English.
        OcrEngine engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));
        if (engine == null)
        {
            Console.WriteLine("Failed to create OcrEngine. Make sure you are on Windows 10 version 1809 or later.");
            return;
        }

        // Continue with the rest of the pipeline...
```

**原因说明：** 引擎抽象了模式识别的繁重工作。显式创建它可以让我们控制语言设置，这在后续想要 **提取文本扫描** 文档的多语言场景中至关重要。

## 步骤 2：加载图像文件 – **将扫描转换为文本** 的核心

接下来，从磁盘读取图像并将其转换为 `SoftwareBitmap`，这是 OCR 引擎所期望的格式。

```csharp
        // Load the image file into a SoftwareBitmap.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "lowres_scan.jpg");
        using (FileStream fs = new FileStream(imagePath, FileMode.Open, FileAccess.Read))
        {
            // Decode the image (supports JPEG, PNG, BMP, etc.).
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Optional: upscale low‑resolution images for better accuracy.
            SoftwareBitmap upscaled = SoftwareBitmap.Convert(bitmap, bitmap.BitmapPixelFormat, bitmap.BitmapAlphaMode);
            // Pass the bitmap to OCR.
            await RecognizeAsync(engine, upscaled);
        }
    }
```

**这样做的原因：** 直接将原始文件流喂给 OCR 往往会得到糟糕的结果，尤其是低分辨率扫描时。转换为 `SoftwareBitmap` 之后，我们可以在识别前调整 DPI、色深，甚至应用滤镜。

## 步骤 3：执行 **识别文本图像** 操作

现在终于调用引擎的 `RecognizeAsync` 方法。魔法就在这里发生。

```csharp
    private static async Task RecognizeAsync(OcrEngine engine, SoftwareBitmap bitmap)
    {
        // Run OCR – this returns an OcrResult object.
        OcrResult result = await engine.RecognizeAsync(bitmap);

        // The Result contains a collection of lines and words.
        Console.WriteLine("=== OCR Output ===");
        foreach (var line in result.Lines)
        {
            Console.WriteLine(line.Text);
        }

        // For a quick **image to text c#** check, also output the raw string.
        Console.WriteLine("\nFull Text:\n" + result.Text);
    }
}
```

**你将看到的结果：** 如果 `lowres_scan.jpg` 包含 “Hello World” 这句话，控制台会输出：

```
=== OCR Output ===
Hello World

Full Text:
Hello World
```

这就是完整的 **c# ocr example**——仅四个逻辑步骤，却涵盖了从文件加载到最终输出的全部过程。

## 步骤 4：处理边缘情况 – 当扫描不完美时

实际图像并不总是清晰。以下是几种无需重写整个程序的调优方式：

| 问题 | 快速解决方案 |
|------|--------------|
| **极低 DPI（≤ 72）** | 在识别前使用 `BitmapTransform` 对位图进行放大。 |
| **文字倾斜** | 使用 `SoftwareBitmap.Rotate` 进行旋转校正，使页面恢复水平。 |
| **多语言** | 创建 `OcrEngine.TryCreateFromLanguage(new OcrLanguage("en-fr"))` 并相应设置 `engine.Language`。 |
| **文件过大** | 将图像分块处理（`engine.RecognizeAsync(tileBitmap)`），随后拼接结果。 |

这些微调可确保你的 **提取文本扫描** 过程在处理噪声收据或倾斜照片时仍然可靠。

## 步骤 5：将示例封装为可复用的帮助类（可选）

如果你计划在应用的多个位置 **将扫描转换为文本**，可以将逻辑封装到一个小型工具类中：

```csharp
public static class OcrHelper
{
    private static readonly OcrEngine _engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));

    public static async Task<string> ImageToTextAsync(string filePath)
    {
        using var fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        var decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
        var bitmap = await decoder.GetSoftwareBitmapAsync();

        var result = await _engine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

随后只需调用：

```csharp
string text = await OcrHelper.ImageToTextAsync("YOUR_DIRECTORY/lowres_scan.jpg");
Console.WriteLine(text);
```

**为何值得使用：** 该帮助类将 OCR 的底层实现隔离，使你专注于业务逻辑——这正是一个将在多个项目中复用的 **c# ocr example** 所需要的。

---

![recognize text image example](https://example.com/ocr-demo.png "Screenshot of OCR console output showing recognize text image result")

*Alt text:* **recognize text image** 输出，来自 C# OCR 控制台应用程序。

---

## 常见问题

**问：这在 Linux 上的 .NET Core 能运行吗？**  
答：`Windows.Media.Ocr` 命名空间仅限 Windows。若在 Linux 或 macOS 上，可改用 TesseractSharp 或 IronOcr——它们同样提供类似的 `Engine.Recognize` 方法，外围代码几乎不需要改动。

**问：内置 OCR 对手写笔记的识别准确率如何？**  
答：手写识别仍属实验阶段。若追求高准确率，建议使用印刷体或考虑 Azure Cognitive Services 等云服务。

**问：能直接处理 PDF 吗？**  
答：不支持直接处理。需要先使用 `PdfSharp` 或 `Ghostscript` 将每页 PDF 转为图像，再将位图送入 OCR 引擎。

---

## 结论

现在，你已经拥有一个完整、可投入生产的 **c# ocr example**，能够 **识别文本图像** 文件、**提取文本扫描** 内容，并 **将扫描转换为文本**，仅需几行代码。通过理解整个流程——引擎创建、图像加载、异步识别以及结果处理——你可以将该模式迁移到任何需要将图片转为可搜索字符串的 C# 项目中。

准备好下一步了吗？尝试为其添加 WinForms 或 WPF 简单 UI，实验不同语言，或将输出写入数据库以实现可搜索归档。掌握 **图像转文本 c#** 技巧后，天地皆可为你所用。

祝编码愉快，愿你的扫描始终清晰！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在自己的项目中进一步掌握 API 功能并探索替代实现方式。每篇资源均提供完整可运行的代码示例和逐步解释。

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}