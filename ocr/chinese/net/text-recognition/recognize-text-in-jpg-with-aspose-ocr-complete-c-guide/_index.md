---
category: general
date: 2026-01-09
description: 使用 Aspose OCR 在 C# 中快速识别 jpg 文本。学习如何从图像提取文字，将图像转换为 JSON 和 EPUB，一站式教程。
draft: false
keywords:
- recognize text in jpg
- extract text from image
- convert image to json
- convert image to epub
- create epub from image
language: zh
og_description: 使用 Aspose OCR 识别 JPG 中的文本。本指南展示了如何从图像提取文本、将图像转换为 JSON 和 EPUB，以及如何从图像创建
  ePub。
og_title: 在 JPG 中识别文字 – 完整 C# 教程
tags:
- Aspose OCR
- C#
- Image Processing
title: 使用 Aspose OCR 识别 JPG 中的文本 – 完整 C# 指南
url: /zh/net/text-recognition/recognize-text-in-jpg-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 JPG 中识别文本 – 完整 C# 指南

是否曾经需要 **在 jpg 中识别文本**，却不确定该选用哪个库？你并不孤单。许多开发者在首次尝试从照片或扫描文档中提取文字时都会遇到同样的难题。  

好消息是？使用 Aspose OCR，你只需几行 C# 代码即可 **从图像中提取文本**，随后还能立即 **将图像转换为 JSON**，甚至 **将图像转换为 EPUB**——全部在 IDE 中完成，无需离开编辑环境。

在本教程中，我们将完整演示整个工作流：从安装合适的 NuGet 包、在 JPG 中识别文本，到将结果保存为结构化的 JSON 和 ePub 文档。结束时，你将能够 **从图像创建 epub**，这对电子学习平台、数字图书馆或任何需要可搜索电子书的应用都非常实用。

---

## 你需要准备的环境

- **.NET 6+**（或 .NET Framework 4.6+）。代码可在任意近期运行时上运行。
- **Aspose.OCR** NuGet 包 —— 核心 OCR 引擎。
- **Aspose.Publishing** NuGet 包 —— 用于生成 ePub 输出格式。
- 一张名为 `input.jpg` 的图像文件，放置在磁盘的任意位置（请自行替换路径）。
- 文本编辑器或 IDE（Visual Studio、VS Code、Rider——随你喜欢）。

就这些。无需额外服务、外部 API，只需几个库和一张 JPG 文件。

---

## 第一步：设置项目以 **在 jpg 中识别文本**

首先，新建一个控制台应用程序（或在已有项目中添加）。然后通过 NuGet 包管理器添加这两个 Aspose 包：

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.Publishing
```

> **小技巧：** 如果使用 Visual Studio，右键点击项目 → *Manage NuGet Packages* → 搜索 *Aspose.OCR* 与 *Aspose.Publishing*，随后点击 **Install**。

这些包包含了 **从图像中提取文本** 所需的一切，并在后续生成 ePub 文件。

---

## 第二步：使用 Aspose OCR **从图像中提取文本**

接下来我们编写代码，实际读取 JPG 并提取其中的字符。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ImageToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // 2️⃣ Recognize text from the JPG file
            // Replace the path with the location of your own image
            string inputPath = @"YOUR_DIRECTORY\input.jpg";
            var ocrResult = ocrEngine.RecognizeImage(inputPath);

            // 3️⃣ Show the recognized text in the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**工作原理说明：** `OcrEngine` 把所有低层的图像预处理、语言检测和字符分割都抽象掉。你只需指向文件，它就会返回一个 `OcrResult` 对象，里面包含纯文本字符串（`ocrResult.Text`）以及丰富的元数据。

---

## 第三步：**将图像转换为 JSON** – 导出 OCR 结果

如果需要以结构化格式存储 OCR 输出（用于 API、数据库或后续处理），Aspose 能轻松将结果序列化为 JSON。

```csharp
// 4️⃣ Convert the OCR result to JSON
string jsonContent = ocrResult.ToJson();

// 5️⃣ Save the JSON to disk
string jsonPath = @"YOUR_DIRECTORY\output.json";
File.WriteAllText(jsonPath, jsonContent);

Console.WriteLine($"JSON saved to: {jsonPath}");
```

生成的 JSON 大致如下（为简洁起见已截断）：

```json
{
  "Text": "Hello world!",
  "Confidence": 0.98,
  "PageCount": 1,
  "Words": [
    { "Value": "Hello", "Confidence": 0.99 },
    { "Value": "world!", "Confidence": 0.97 }
  ]
}
```

**适用场景：** 当你将 OCR 数据送入 Web 服务、存入 NoSQL 数据库，或需要一种任何语言都能解析的可移植表示时，JSON 是理想选择。

---

## 第四步：**将图像转换为 EPUB** – 保存为电子书

Aspose Publishing 为多种电子书格式提供支持，包括 EPUB。只需在 `OcrResult` 上调用 `Save`，即可生成符合规范的 ePub 文件，文件中包含识别的文本以及（可选的）原始图像。

```csharp
// 6️⃣ Save the OCR result as an ePub document
string epubPath = @"YOUR_DIRECTORY\output.epub";
ocrResult.Save(epubPath, OcrOutputFormat.Epub);

Console.WriteLine($"EPUB created at: {epubPath}");
```

**你将得到：** 一个可以在任意阅读器（Calibre、Apple Books、Adobe Digital Editions）中打开的 ePub。文件将提取的文本作为可搜索内容，同时保留源图像作为背景层——非常适合构建 **从图像创建 epub** 的流水线。

---

## 第五步：完整示例 – 从 JPG 到 JSON 与 EPUB

将上述所有步骤整合在一起，下面是完整的、可直接运行的程序。将其复制粘贴到 `Program.cs`，根据实际情况调整文件路径，然后按 **F5** 运行。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ImageToEpubDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // Path to the input JPG
            string inputPath = @"YOUR_DIRECTORY\input.jpg";

            // Recognize text
            var ocrResult = ocrEngine.RecognizeImage(inputPath);

            // Output recognized text to console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine();

            // Export to JSON
            string jsonPath = @"YOUR_DIRECTORY\output.json";
            File.WriteAllText(jsonPath, ocrResult.ToJson());
            Console.WriteLine($"JSON saved to: {jsonPath}");

            // Export to EPUB
            string epubPath = @"YOUR_DIRECTORY\output.epub";
            ocrResult.Save(epubPath, OcrOutputFormat.Epub);
            Console.WriteLine($"EPUB created at: {epubPath}");
        }
    }
}
```

运行程序后，你应该会看到三件事：

1. 控制台中打印出识别的文本。
2. 一个名为 `output.json` 的文件，包含结构化的 OCR 数据。
3. 一个名为 `output.epub` 的文件，可在任意电子书阅读器中打开。

---

## 常见问题与边缘情况

- **如果图像是 PNG 或 BMP 呢？**  
  Aspose OCR 支持大多数光栅格式（PNG、BMP、TIFF、GIF）。只需在 `inputPath` 中更改文件扩展名，代码即可复用。

- **能指定除英语之外的语言吗？**  
  可以。在调用 `RecognizeImage` 之前设置 `ocrEngine.Language = OcrLanguage.French;`（或任意受支持语言）。

- **多页 PDF 怎么处理？**  
  对于 PDF，首先将每页转换为图像（可使用 Aspose.PDF），然后将每张图像喂给 `RecognizeImage`。得到的多个 `OcrResult` 对象可以在导出为 JSON 或 EPUB 前合并。

- **我得到的置信度分数很低，如何提升准确率？**  
  对图像进行预处理：提升对比度、去倾斜或转换为灰度。Aspose OCR 还提供 `PreprocessOptions` 可供调节。

---

## 结论

现在，你已经掌握了一套完整的 **在 jpg 中识别文本** 的方案，使用 Aspose OCR **从图像中提取文本**，随后 **将图像转换为 JSON** 用于数据管道，或 **将图像转换为 EPUB** 构建可搜索的电子书。该方法轻量，仅需两个 NuGet 包，且兼容所有现代 .NET 运行时。

接下来你可以：

- 将 JSON 输出集成到搜索索引（Azure Cognitive Search、Elastic）中。
- 批量处理文件夹中的图像，生成电子书库。
- 与翻译 API 结合，自动创建多语言电子书。

动手尝试吧，实验不同的图像质量，让 OCR 引擎为你完成繁重的工作。祝编码愉快！

---

![在 jpg 中识别文本的输出截图](placeholder-image.png "在 jpg 中识别文本示例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}