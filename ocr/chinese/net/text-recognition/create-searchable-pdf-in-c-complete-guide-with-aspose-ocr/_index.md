---
category: general
date: 2026-06-28
description: 使用 C# 将图像创建为可搜索的 PDF。了解如何将图像转换为 PDF、从图像中提取文本，并在一次流程中识别多种语言。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- how to recognize multiple languages
- how to generate searchable pdf
language: zh
og_description: 使用 C# 创建可搜索的 PDF。本指南展示了如何将图像转换为 PDF、从图像中提取文本以及以编程方式识别多种语言。
og_title: 使用 C# 创建可搜索的 PDF – 步骤教程
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Create searchable PDF from images using C#. Learn how to convert image
    to PDF, extract text from image, and recognize multiple languages in one flow.
  headline: Create Searchable PDF in C# – Complete Guide with Aspose OCR
  type: TechArticle
- description: Create searchable PDF from images using C#. Learn how to convert image
    to PDF, extract text from image, and recognize multiple languages in one flow.
  name: Create Searchable PDF in C# – Complete Guide with Aspose OCR
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 SDK or later (the code compiles with .NET Core as well). - An
      Aspose.OCR license (you can start with a free trial; the API works without a
      license but adds a watermark). - A sample image that contains English, Arabic,
      and Korean text (or any languages you need). - Visual Studio 2022 or yo'
  - name: What If a Language Isn't Recognized?
    text: If you add a language that the engine doesn’t have a model for, it will
      simply ignore it and fall back to the others. To avoid surprises, double‑check
      the supported language list in the Aspose documentation.
  - name: Expected Output
    text: '``` Plain text: Hello World! مرحبا بالعالم! 안녕하세요 세계! Searchable PDF saved.
      ```'
  type: HowTo
tags:
- OCR
- PDF
- C#
- Aspose
title: 在 C# 中创建可搜索 PDF – 使用 Aspose OCR 的完整指南
url: /zh/net/text-recognition/create-searchable-pdf-in-c-complete-guide-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 创建可搜索 PDF – Aspose OCR 完整指南

是否曾想过如何在不离开 C# 项目的情况下直接从图像**创建可搜索的 PDF**？你并不是唯一有此需求的人。无论是数字化多语言文档，还是构建收据扫描应用，将图片转换为可搜索的 PDF 都是一项改变游戏规则的能力。

在本教程中，我们将逐步演示如何使用 Aspose.OCR **创建可搜索的 PDF**，涵盖从加载图片到导出完整可搜索文档的所有步骤。过程中我们还会展示如何 **将图像转换为 PDF**、**从图像提取文本**，以及 **识别多种语言**——全部在一个支持异步的方式中完成。

## 您将收获的内容

- 一个可运行的 C# 控制台应用程序，读取图像，在 GPU 加速模式下执行 OCR，并生成可搜索的 PDF。
- 了解为何启用 GPU 对性能至关重要。
- 用于下游处理的**从图像提取文本**技术。
- 一种在一次识别中**识别多种语言**的清晰模式。
- 关于扩展代码以处理其他格式或自定义 OCR 设置的提示。

### 前置条件

- .NET 6.0 SDK 或更高版本（代码同样可在 .NET Core 上编译）。
- Aspose.OCR 许可证（可先使用免费试用版；API 在没有许可证的情况下仍可工作，但会添加水印）。
- 一张包含英文、阿拉伯文和韩文的示例图像（或任何您需要的语言）。
- Visual Studio 2022 或您喜欢的 IDE。

准备好了吗？太好了——让我们开始吧。

---

## 步骤 1：设置项目并安装 Aspose.OCR

首先，创建一个新的控制台项目：

```bash
dotnet new console -n SearchablePdfDemo
cd SearchablePdfDemo
```

然后添加 Aspose.OCR NuGet 包：

```bash
dotnet add package Aspose.OCR
```

> **专业提示：** 如果您计划在支持 GPU 的机器上运行 OCR，还请安装 `Aspose.OCR.Gpu` 包。它会自动引入本机 CUDA 库。

## 步骤 2：创建 OCR 引擎并启用 GPU 加速

此操作的核心是 `OcrEngine`。启用 GPU 可以在处理高分辨率图像时节省数秒时间。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// ...

// Step 2: Create an OCR engine and turn on GPU support
var ocrEngine = new OcrEngine();
ocrEngine.Settings.EnableGpu = true;   // ← speeds up large images dramatically
```

为什么要启用 GPU？因为 OCR 本质上是一个巨大的矩阵乘法问题；GPU 能比 CPU 更高效地处理这些并行任务。如果您在没有 GPU 的无头服务器上，只需将 `EnableGpu` 保持为 `false`——引擎会回退到 CPU 处理。

## 步骤 3：异步加载图像

异步 I/O 能保持 UI 响应，并防止服务器场景下线程池耗尽。`OcrImage.FromFileAsync` 帮助方法抽象了流的处理。

```csharp
using Aspose.OCR;

// ...

// Step 3: Load the image to be processed (async)
var imagePath = @"C:\Docs\multilingual_sample.jpg";
var image = await OcrImage.FromFileAsync(imagePath);
```

如果您稍后需要 **将图像转换为 PDF**，请保留此 `OcrImage` 实例；您将直接把它传递给 PDF 导出器。

## 步骤 4：识别多语言文本

Aspose.OCR 允许您指定以逗号分隔的语言代码列表。这就是在一次识别中**识别多种语言**的答案。

```csharp
using Aspose.OCR;

// ...

// Step 4: Run OCR with English, Arabic, and Korean support
var ocrResult = await ocrEngine.RecognizeAsync(image, new OcrOptions
{
    Language = "en,ar,ko"   // ← multiple languages, order doesn’t matter
});
```

`ocrResult.Text` 属性现在保存了 Aspose 能够解读的所有内容的纯文本表示。这是**从图像提取文本**的核心。

```csharp
Console.WriteLine("Plain text extracted:");
Console.WriteLine(ocrResult.Text);
```

### 如果某种语言未被识别怎么办？

如果您添加的语言引擎没有相应的模型，它会直接忽略该语言并回退到其他语言。为避免意外，请在 Aspose 文档中再次确认受支持的语言列表。

## 步骤 5：直接导出可搜索的 PDF

与其手动创建 PDF 并覆盖文本，Aspose.OCR 提供了一行代码即可**生成可搜索的 PDF**。该方法将 OCR 文本嵌入为不可见层，使 PDF 在保持原始图像的同时可搜索。

```csharp
using Aspose.OCR.Output;

// ...

// Step 5: Export the recognized content as a searchable PDF
await ocrEngine.RecognizeToPdfAsync(image, new PdfExportOptions
{
    Language = "en,ar,ko",               // keep language consistency
    OutputPath = @"C:\Docs\sample_searchable.pdf"
});

Console.WriteLine("Searchable PDF saved at C:\\Docs\\sample_searchable.pdf");
```

在内部，Aspose 会创建一个 PDF 页面，以原始位图作为可见背景，并添加一个与图像坐标匹配的隐藏文本层。当您在 Adobe Reader 中打开文件并按 **Ctrl + F** 时，即可定位任意三种语言中的单词。

## 步骤 6：整合全部——完整的异步 `Main`

下面是完整的、可直接运行的程序。将其粘贴到 `Program.cs`，替换文件路径，然后按 **F5**。

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Output;

class AllInOne
{
    static async Task Main()
    {
        // Step 2: Create an OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.EnableGpu = true;

        // Step 3: Load the image to be processed (async)
        var image = await OcrImage.FromFileAsync(@"C:\Docs\multilingual_sample.jpg");

        // Step 4: Recognize text in the image using multiple languages
        var ocrResult = await ocrEngine.RecognizeAsync(image, new OcrOptions
        {
            Language = "en,ar,ko"
        });

        Console.WriteLine("Plain text:");
        Console.WriteLine(ocrResult.Text);

        // Step 5: Export the recognized content as a searchable PDF
        await ocrEngine.RecognizeToPdfAsync(image, new PdfExportOptions
        {
            Language = "en,ar,ko",
            OutputPath = @"C:\Docs\sample_searchable.pdf"
        });

        Console.WriteLine("Searchable PDF saved.");
    }
}
```

### 预期输出

```
Plain text:
Hello World!
مرحبا بالعالم!
안녕하세요 세계!
Searchable PDF saved.
```

当您打开 `sample_searchable.pdf` 并搜索 “Hello”、 “العالم” 或 “세계” 时，引擎能够定位相应的单词，即使它们是作为图像的一部分呈现的。

## 步骤 7：常见陷阱及解决方法

| 问题 | 产生原因 | 解决方案 |
|-------|----------------|-----|
| **GPU 未检测到** | 机器缺少 CUDA 驱动或未安装 `Aspose.OCR.Gpu` 包。 | 安装 NVIDIA 驱动，确认 CUDA 版本，或将 `EnableGpu = false`。 |
| **缺少语言支持** | 语言代码不在内置模型集合中。 | 从 Aspose 下载额外语言包，或限制使用受支持的代码。 |
| **PDF 显示为空白** | 输出路径无效或进程缺少写入权限。 | 使用具有适当权限的绝对路径，例如 `C:\Temp\output.pdf`。 |
| **性能下降** | 大图像（>5 MP）导致内存压力。 | 在 OCR 前缩小图像尺寸或提升进程的内存上限。 |

## 扩展示例

- **批量处理：** 将核心逻辑包装在 `foreach` 循环中，以遍历文件夹中的图像。
- **自定义 OCR 设置：** 调整 `ocrEngine.Settings.PageSegMode` 以适应单列或多列布局。
- **元数据注入：** 使用 `PdfExportOptions` 将作者、标题或创建日期嵌入可搜索的 PDF 中。

---

## 结论

您现在已经掌握了使用 C# 直接从图像 **创建可搜索 PDF** 的完整端到端方案。通过上述步骤，您已经学会了 **将图像转换为 PDF**、**从图像提取文本**，以及 **识别多种语言**——所有代码保持简洁且支持异步。

接下来，您可以尝试不同的语言包，添加 OCR 后处理（如拼写检查），或将此流程集成到按需提供可搜索 PDF 的 Web API 中。可能性无限，而您刚刚编写的代码是任何文档自动化项目的坚实基础。

对性能调优或授权有疑问？留下评论，让我们继续交流。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在自己的项目中探索替代实现方式。每个资源都包含完整可运行的代码示例和逐步解释。

- [提取图像文本 C#（使用语言选择）使用 Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [将图像转换为 PDF C# – 保存多页 OCR 结果](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [如何在 .NET 中使用 Aspose.OCR OCR PDF](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}