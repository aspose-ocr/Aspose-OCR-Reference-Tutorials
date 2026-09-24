---
category: general
date: 2026-02-09
description: 使用 C# 通过设置批量 OCR 的最大并行度快速提取图像文字——学习转换扫描页、处理多图像 OCR 并高效读取 PNG 文本。
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: zh
og_description: 在 C# 中通过设置最大并行度提取图像文本。本教程展示如何转换扫描页面、运行多图像 OCR 并使用 Aspose OCR 读取 PNG
  文本。
og_title: 使用 C# 从 PNG 中提取文本图像 – 完整批量 OCR 指南
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: 使用 C# 从 PNG 中提取文本图像 – 使用 Aspose OCR 进行批量 OCR
url: /zh/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

placeholders unchanged.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 从 PNG 中提取文本图像 – 批量 OCR（Aspose OCR）

是否曾经需要 **从一文件夹的扫描 PNG 中提取文本图像**，却卡在 “怎么才能快？” 的问题上？你并不孤单。在许多真实项目中，开发者必须 **设置最大并行度**，才能让数十页在秒级而非分钟级完成处理。

在本指南中，我们将逐步演示一个完整、可运行的示例，**转换扫描页**、执行 **多图像 OCR**，并最终 **读取 png 文本**，全程轻松无压力。没有模糊的 “查看文档” 链接——只有可直接复制粘贴的代码、每行代码为何重要的解释，以及避免常见陷阱的技巧。

> **专业提示：** 如果你已经在其他地方使用 Aspose OCR，你会注意到这里同样出现了 `OcrEngine` 类，只是我们会对其配置进行调整，以实现真正的并行处理。

---

## 所需环境

- **.NET 6+**（或 .NET Framework 4.6+）。API 使用方式相同，但更新的运行时在线程处理上更优秀。  
- **Aspose.OCR for .NET** – 通过 NuGet 安装：`Install-Package Aspose.OCR`。  
- 一个包含若干 PNG 扫描文件的文件夹（如 `page1.png`、`page2.png` ……）。  
- 你熟悉的 IDE 或编辑器（Visual Studio、Rider、VS Code 等）。

就这些。无需额外服务、无需云密钥，全部本地处理。

---

## extract text images – 为批量 OCR 设置最大并行度

当你对多个文件启动 OCR 时，默认情况下引擎只会使用单线程。这样安全但极其缓慢。通过配置 `MaxDegreeOfParallelism`，可以告诉引擎同时可以启动多少线程。

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**为什么是 4？**  
在大多数现代笔记本上，4 是一个折中点——足够的核心数让 CPU 保持忙碌，但又不会抢占太多资源导致其他进程受阻。如果在拥有 16 核的服务器上运行，可将数值提升至 12 或 14，以获得明显的加速。

---

## Convert scanned pages – 构建 ImageStream 集合

Aspose 需要每张图片以 `ImageStream` 形式提供。`FromFile` 辅助方法读取文件、将其保存在内存中，并交给 OCR 引擎。如果图片来自数据库或 HTTP 响应，也可以传入 `MemoryStream`。

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**边缘情况：** 若文件缺失或损坏，`FromFile` 会抛出 `FileNotFoundException`。如果输入可能不可靠，请在构造时使用 `try/catch` 包裹。

---

## multiple image ocr – 执行批量 OCR

现在真正的工作开始了。`RecognizeBatch` 会根据前面设置的线程数并发处理每张图片，并返回 `OcrResult` 对象列表。

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

在内部，每个线程会加载自己的图片、运行神经网络并提取纯文本。结果列表的顺序与输入列表保持一致，因而可以安全地映射 page 1 → result 0，依此类推。

---

## read png text – 显示提取的内容

最后，我们遍历结果并将纯文本打印到控制台。此处你可以将输出重定向到文件、数据库，甚至下游的 NLP 服务。

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### 预期的控制台输出

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

如果看到空白段落，请确认 PNG 不是全白图像——OCR 需要一定的对比度。

---

## 实用技巧与常见陷阱

| Situation | What to Do |
|-----------|------------|
| **Memory pressure** on large batches | 将图片分批（10‑20 文件）处理，若出现内存峰值可调用 `GC.Collect()`。 |
| **Incorrect language detection** | 在调用 `RecognizeBatch` 前设置 `ocrEngine.Configuration.Language = OcrLanguage.English;`（或目标语言）。 |
| **Slow performance despite parallelism** | 确认 SSD 没有 I/O 限速；如本例所示，先将所有文件读取到内存（`ImageStream.FromFile`）。 |
| **Missing characters** | 将 `ocrEngine.Configuration.DPI = 300;` 提升，以获得更高分辨率的处理。 |

---

## Extending the Example – 从 PNG 到 PDF 或 DOCX

如果以后需要 **将扫描页转换为可搜索的 PDF**，只需将相同的 `ocrResults[i].PlainText` 交给 PDF 库（例如 Aspose.PDF），并将文本以不可见层叠加。相同的并行技巧同样适用。

---

## 完整源代码（可直接复制粘贴）

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

将其保存为 `BatchExample.cs`，运行 `dotnet run`，即可在控制台看到原本隐藏在 PNG 扫描中的文本。

---

## 可视化概览

![extract text images example](images/ocr-batch.png){alt="提取文本图像示例"}

该图展示了流程：**PNG 文件 → ImageStream 集合 → OcrEngine（最大并行度） → OCR 结果 → 控制台 / 下游存储**。

---

## 结论

现在，你已经掌握了一套完整的端到端方案，能够在 C# 中 **提取文本图像**、**设置最大并行度**、**转换扫描页**、处理 **多图像 OCR**，并高效 **读取 png 文本**。代码自包含，解释覆盖了 “怎么做” 与 “为什么”，技巧帮助你规避常见痛点。

接下来可以尝试将 PNG 列表换成动态的 `Directory.GetFiles` 循环，实验不同的线程数，或将输出写入可搜索的 PDF。相同模式可轻松扩展至数百页，几乎不需要额外代码。

有疑问或遇到棘手的边缘情况？在下方留言，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}