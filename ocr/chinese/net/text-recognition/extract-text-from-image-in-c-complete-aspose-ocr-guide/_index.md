---
category: general
date: 2026-01-10
description: 使用 Aspose OCR 在 C# 中提取图像文本。了解如何通过批处理将扫描文档的文本转换并保存结果。
draft: false
keywords:
- extract text from image
- convert scanned document text
- batch OCR processing
- Aspose OCR
- C# OCR tutorial
language: zh
og_description: 使用 Aspose OCR 在 C# 中从图像提取文本。本教程展示了如何使用批处理将扫描文档的文本转换。
og_title: 在 C# 中从图像提取文本 – 完整的 Aspose OCR 指南
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 在 C# 中从图像提取文本 – 完整的 Aspose OCR 指南
url: /zh/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像提取文本 – 完整的 Aspose OCR 指南

是否曾需要 **从图像提取文本**，却不知从何入手？你并不孤单；许多开发者在处理扫描的 PDF、多页 TIFF 或基于照片的收据时都会遇到这个难题。好消息是，使用 Aspose OCR，你只需几行 C# 代码就能 **将扫描文档的文本转换**。

在本教程中，我们将通过一个真实场景：读取多页 TIFF，对每一页执行批量 OCR，并将所有页面的内容写入单个文本文件。完成后，你将拥有一个可直接运行的控制台应用，了解每一步的意义，并掌握如何针对密码保护的图像或自定义语言包等边缘情况进行调整。

## 前置条件

- .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）  
- Visual Studio 2022（或任意你喜欢的编辑器）  
- Aspose OCR 许可证文件（或使用免费评估模式）  
- 一个多页图像文件（例如 `multipage.tif`），放置在可引用的文件夹中  

除 `Aspose.OCR` 之外无需其他 NuGet 包，我们将在第一步中进行安装。

## 第一步 – 安装 Aspose OCR 并创建项目

首先，创建一个新的控制台项目并引入 Aspose OCR 库。

```bash
dotnet new console -n ImageTextExtractor
cd ImageTextExtractor
dotnet add package Aspose.OCR
```

> **专业提示：** 如果你有许可证文件（`Aspose.OCR.lic`），请将其复制到项目根目录。库会在运行时自动加载该文件。

为什么要这一步？安装包后，你即可使用 `BatchProcessor`、`OcrEngine` 等便利类，免去低层图像处理的繁琐。同时也确保使用 Aspose 提供的最新 OCR 算法。

## 第二步 – 使用 BatchProcessor 加载多页图像

`BatchProcessor` 正是为此场景设计的：在不手动拆分文件的情况下遍历多页图像的每一页。

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System.Text;

// Step 2: Initialize the batch processor with the path to your TIFF
var batchProcessor = new BatchProcessor(@"YOUR_DIRECTORY\multipage.tif");

// Verify that pages were loaded
if (batchProcessor.Pages.Count == 0)
{
    Console.WriteLine("No pages found – double‑check the file path.");
    return;
}
```

`BatchProcessor` 会将所有页面读取到内存中，通过 `batchProcessor.Pages` 暴露。每个页面对象都有其页码（`ocrPage.Number`），我们稍后会用它来生成清晰的标题。

## 第三步 – 准备 StringBuilder 累积结果

我们希望得到一个包含所有页面 OCR 输出的单一文本文件，并以标题分隔。`StringBuilder` 是在循环中拼接字符串的最高效方式。

```csharp
// Step 3: Create a StringBuilder to collect OCR results
var extractedText = new StringBuilder();
```

为什么使用 `StringBuilder`？在循环中使用 `+` 进行字符串拼接会在每次迭代时分配新字符串，导致性能下降——尤其是处理大型文档时。

## 第四步 – 遍历每页，执行 OCR 并追加结果

现在进入教程的核心：遍历每页，识别文本，并使用页面标记保存。

```csharp
// Step 4: Process each page individually
foreach (var ocrPage in batchProcessor.Pages)
{
    // Create a fresh OcrEngine for every page – this isolates settings
    var ocrEngine = new OcrEngine
    {
        Image = ocrPage
    };

    // Perform recognition
    ocrEngine.Recognize();

    // Append a clear header and the recognized text
    extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
    extractedText.AppendLine(ocrEngine.Text);
}
```

**为什么每页都创建新的 `OcrEngine`？** 有些开发者会复用同一个引擎并更改其 `Image` 属性，但这可能会保留语言设置或前一次的结果，导致细微错误。实例化全新的引擎可确保每次都是干净的状态。

### 处理常见边缘情况

- **空白页：** 如果页面没有可识别的文本，`ocrEngine.Text` 将为空字符串。你可以插入占位符，例如 “(未检测到文本)”。
- **语言选择：** 默认情况下 Aspose OCR 使用英语。若要处理德语或法语，可在调用 `Recognize()` 前设置 `ocrEngine.Language = Language.German;`。
- **性能技巧：** 对于巨大的 TIFF，可以启用 `ocrEngine.UseParallelProcessing = true;` 以利用多核 CPU。

## 第五步 – 将合并后的输出写入文本文件

最后，将累积的字符串持久化到磁盘。

```csharp
// Step 5: Save the result to a .txt file
string outputPath = @"YOUR_DIRECTORY\multipage_result.txt";
File.WriteAllText(outputPath, extractedText.ToString());

Console.WriteLine($"OCR complete! Results saved to {outputPath}");
```

生成的 `multipage_result.txt` 大致如下所示：

```
--- Page 1 ---
This is the first page of the scanned document.
It contains a title and some introductory text.

--- Page 2 ---
Continuation of the report.
Data tables and figures follow.
```

至此，你已经 **从图像提取文本**，并成功 **将扫描文档的文本转换** 为可搜索、可编辑的格式。

## 额外内容 – 可视化概览（图片替代文字）

下面是一张简易流程图，展示了整个过程。  
*替代文字：* “使用 Aspose OCR 批处理在 C# 中从图像提取文本的流程图”。

![OCR Flow Diagram](placeholder-image-url.png)

*（如果你在静态站点上发布本教程，请将占位图替换为实际的 SVG 或 PNG。）*

## 常见问题

**这能用于 PDF 文件吗？**  
可以，Aspose OCR 能将 PDF 页面读取为图像。你只需先将 PDF 转为图像，或使用 `Aspose.PDF` 中的 `PdfDocument`，将每页栅格化后传给 `OcrEngine`。

**如果我的 TIFF 受密码保护怎么办？**  
`BatchProcessor` 本身不处理加密。请先使用诸如 `Aspose.Imaging` 等库解密文件，再将其传入 OCR 流程。

**可以输出 JSON 而不是纯文本吗？**  
完全可以。将 `StringBuilder` 逻辑替换为 JSON 序列化（例如 `System.Text.Json`），并将每页的文本存入 `pageNumber` 键下。

## 完整示例代码

以下是可直接复制到 `Program.cs` 的完整程序，包含所有 using 指令、错误处理和注释。

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Text;

namespace ImageTextExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            string inputImagePath = @"YOUR_DIRECTORY\multipage.tif";
            string outputTextPath = @"YOUR_DIRECTORY\multipage_result.txt";

            // 1️⃣ Load the multi‑page image
            var batchProcessor = new BatchProcessor(inputImagePath);
            if (batchProcessor.Pages.Count == 0)
            {
                Console.WriteLine("No pages detected – verify the file path.");
                return;
            }

            // 2️⃣ Prepare a StringBuilder for the final output
            var extractedText = new StringBuilder();

            // 3️⃣ Process each page
            foreach (var ocrPage in batchProcessor.Pages)
            {
                var ocrEngine = new OcrEngine
                {
                    Image = ocrPage,
                    // Uncomment to change language:
                    // Language = Language.German,
                    // UseParallelProcessing = true
                };

                // Run OCR
                ocrEngine.Recognize();

                // Append header and text
                extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
                // Guard against empty results
                string pageText = string.IsNullOrWhiteSpace(ocrEngine.Text)
                    ? "(No text detected on this page)"
                    : ocrEngine.Text;
                extractedText.AppendLine(pageText);
            }

            // 4️⃣ Write to file
            File.WriteAllText(outputTextPath, extractedText.ToString());

            Console.WriteLine($"✅ Extraction complete. File saved at: {outputTextPath}");
        }
    }
}
```

运行程序：

```bash
dotnet run
```

你应该会在控制台看到成功提示，输出文件中则包含合并后的 OCR 结果。

## 结论

我们已经演示了使用 Aspose OCR **从图像提取文本** 的实用方法，将任意多页扫描文件转换为纯文本、可搜索的内容。通过 `BatchProcessor` 与每页独立的 `OcrEngine` 设置，你可以可靠地 **将扫描文档的文本转换**，同时保持代码简洁易维护。

欢迎尝试：更换语言、改为 JSON 输出，或将此逻辑集成到实时处理上传的 Web API 中。核心模式保持不变——加载、识别、累积、持久化。

对 OCR、Aspose 授权或大批量文档处理还有疑问？欢迎在下方留言，或查阅 Aspose 官方文档获取更深入的内容。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}