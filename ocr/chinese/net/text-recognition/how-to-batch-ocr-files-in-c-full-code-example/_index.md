---
category: general
date: 2026-02-17
description: 如何在 C# 中使用 Aspose OCR 批量对多个 PDF 和图像进行 OCR。学习从 PDF 提取文本、将 PDF 转换为文本以及从图像识别文本。
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: zh
og_description: 如何在 C# 中使用 Aspose OCR 批量对多个文档进行 OCR。获取逐步代码，以从 PDF 提取文本、将 PDF 转换为文本，以及从图像中识别文本。
og_title: 如何在 C# 中批量 OCR 文件 – 完整指南
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: 如何在 C# 中批量 OCR 文件 – 完整代码示例
url: /zh/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR 文件 – 完整指南

是否曾想过 **如何批量 OCR** 一堆 PDF 和图像扫描文件，而不必为每个文件单独编写循环？你并不孤单。大多数开发者在一次性处理数十页文本时都会遇到这个难题。好消息是？使用 Aspose OCR，你可以将文件集合一次性传递给同一个引擎，让它完成繁重的工作。

在本教程中，我们将一步步演示一个实用方案，帮助你 **从 pdf 中提取文本**、**将 pdf 转换为文本**，以及 **从图像中识别文本**，全部在一次批处理运行中完成。完成后，你将拥有一个可直接运行的控制台应用程序，能够打印每页的 OCR 结果，并且了解每一步背后的原理，以便在自己的项目中灵活应用。

## 前置条件 – 开始之前你需要准备的

- **.NET 6.0 或更高版本**（代码同样适用于 .NET Framework，但推荐使用 .NET 6+）
- **Aspose.OCR NuGet 包** – 使用 `dotnet add package Aspose.OCR` 安装
- 几个示例文件：一个多页 PDF（`doc1.pdf`）和一个扫描的 TIFF（`doc2.tif`）。将它们放在可引用的文件夹中，例如 `C:\OCRSamples`。
- 基础的 C# 知识 – 需要熟悉 `using` 语句和集合。

> 小技巧：如果没有许可证，Aspose 提供免费临时密钥，可在开发期间移除 100 页的限制。

## 第一步：创建项目并导入命名空间

首先，新建一个控制台项目（或在已有项目中添加），并引入所需的命名空间。

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **为什么重要：** 导入 `Aspose.OCR.Image` 可使用便捷的 `ImageStream.FromFile` 方法，它会自动将 PDF 页面拆分为独立的图像流。这正是让批处理轻松的关键。

## 第二步：初始化 OCR 引擎

引擎是与底层 OCR 核心交互的工作马。整个批处理只需要一个实例。

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **说明：** 重复使用同一个 `OcrEngine` 可以减少内存抖动并提升处理速度，因为原生库在页面之间保持加载状态。

## 第三步：构建图像流列表

在这里我们收集所有待处理的文档。`ImageStream.FromFile` 足够智能，能够将 PDF 拆分为单独的页面，因此一个三页的 PDF 会在幕后生成三个独立的流。

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **边缘情况：** 如果你混合使用 PDF、TIFF、JPEG 或 PNG，只需将它们全部加入同一个列表——Aspose 会自动检测格式。

## 第四步：执行批量 OCR 操作

现在把列表交给引擎。`RecognizeBatch` 返回一个 `OcrResult` 对象集合，每页对应一个。

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **为什么使用批处理？** 手动循环逐页 OCR 会导致引擎每次都重新初始化，处理时间可能翻倍。`RecognizeBatch` 能让引擎保持热状态，并在结果可用时即时返回。

## 第五步：输出识别的文本

最后，我们遍历结果并将每页的文本写入控制台。此处你可以将 `Console.WriteLine` 替换为文件写入、数据库插入或其他下游操作。

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### 预期的控制台输出

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

如果使用示例文件运行程序，你应该会看到每页对应的一段文本，证明你已经成功 **提取扫描 pdf 中的文本** 内容，且只需一次遍历。

## 常见问题处理

| 问题 | 产生原因 | 快速解决方案 |
|------|----------|--------------|
| **内存不足错误** | 大型 PDF 会生成大量高分辨率图像。 | 加载 PDF 时限制 DPI：`ocrEngine.Settings.ImageDpi = 200;` |
| **乱码字符** | 源扫描质量低或使用了不受支持的语言。 | 明确设置语言：`ocrEngine.Language = Language.English;` |
| **结果不完整** | 批处理列表中包含损坏的文件。 | 将 `RecognizeBatch` 包裹在 try/catch 中，并记录 `e.Message` 以定位问题文件。 |
| **性能瓶颈** | 在多核机器上仅使用单线程。 | 使用 `Parallel.ForEach`，为每个线程创建独立的 `OcrEngine` 实例（高级用法）。 |

## 进阶：将 OCR 结果保存为文本文件

如果希望为每页生成单独的 `.txt` 文件，只需在循环内部添加一个小的写入块：

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

现在你已经把 **将 pdf 转换为文本** 的过程转化为整齐的纯文本文件夹——非常适合后续的索引或搜索。

## 完整可运行示例

下面是完整的、可直接复制粘贴的程序代码。没有隐藏依赖，也不需要外部脚本。

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

在项目文件夹中运行 `dotnet run`，即可看到控制台输出提取的文本。这就是 **如何批量 OCR** 一组文档，只需几行 C# 代码。

## 本文回顾 – 快速要点

- 搭建 .NET 控制台应用并安装 Aspose.OCR。  
- 创建单个 `OcrEngine` 实例以保持高效。  
- 构建 `ImageStream` 列表，自动将 PDF 拆分为页面。  
- 使用 `RecognizeBatch` **一次性提取 pdf 中的文本** 以及其他图像格式。  
- 打印结果并可选地保存为单独的 `.txt` 文件，完成 **将 pdf 转换为文本** 的工作流。  

## 后续步骤与相关主题

- **规模化**：使用 `Parallel.ForEach` 与 `OcrEngine` 对象池并行处理数百个文件。  
- **语言包**：将 `Language.English` 替换为 `Language.French`，或在需要 **从图像中识别文本** 的其他语言时加载自定义词典。  
- **后处理**：将 OCR 输出通过拼写检查或自然语言解析器，以提升扫描合同的准确性。  
- **替代库**：如果你在寻找开源方案，可比较 Aspose OCR 与 Tesseract.NET——两者都能 **提取扫描 pdf 中的文本**，但在授权方式和开箱即用的准确度上有所不同。

---

![how to batch OCR example](alt="how to batch OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}