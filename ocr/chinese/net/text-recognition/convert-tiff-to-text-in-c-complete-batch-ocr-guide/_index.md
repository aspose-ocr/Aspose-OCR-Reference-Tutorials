---
category: general
date: 2026-05-25
description: 使用 Aspose.OCR 在 C# 中将 TIFF 转换为文本。了解批量图像转文本的转换方法，并高效提取 TIFF 文件中的文本。
draft: false
keywords:
- convert tiff to text
- extract text from tiff
- batch image to text conversion
- convert scanned images txt
language: zh
og_description: 使用 Aspose.OCR 将 TIFF 转换为文本。本指南展示批量图像转文本的转换方法，以及如何在几行 C# 代码中从 TIFF
  文件中提取文本。
og_title: 在 C# 中将 TIFF 转换为文本 – 完整批量 OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  headline: Convert TIFF to Text in C# – Complete Batch OCR Guide
  type: TechArticle
- description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  name: Convert TIFF to Text in C# – Complete Batch OCR Guide
  steps:
  - name: '**Create** an OCR engine set for English.'
    text: '**Create** an OCR engine set for English.'
  - name: '**Collect** every TIFF file from the target folder.'
    text: '**Collect** every TIFF file from the target folder.'
  - name: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
    text: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
  - name: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
    text: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
  type: HowTo
tags:
- C#
- OCR
- Aspose
- TIFF
title: 在 C# 中将 TIFF 转换为文本 – 完整批量 OCR 指南
url: /zh/net/text-recognition/convert-tiff-to-text-in-c-complete-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 TIFF 转换为文本（C#）– 完整批量 OCR 指南

是否曾需要 **将 TIFF 转换为文本**，却不知从何入手？你并不孤单——许多开发者在处理扫描文档时都会卡在批量 OCR 上。本文将手把手演示一个 **从 TIFF 文件提取文本** 的解决方案，使用 Aspose.OCR，并通过并行处理让大型文件夹在几秒钟内完成。

我们还会涉及 **批量图像转文本** 的最佳实践，最终你将拥有一个可复用的代码片段，能够将整个目录的扫描图像转换为整洁的 *.txt* 文件——非常适合索引、搜索或后续分析。

## 所需环境

- **.NET 6.0** 或更高（代码同样可以在 .NET Framework 上编译）  
- **Aspose.OCR for .NET** NuGet 包（`Install-Package Aspose.OCR`）  
- 包含一个或多个 *.tif* 文件的文件夹（经典的 TIFF 扫描格式）  
- 你喜欢的 IDE（Visual Studio、VS Code、Rider——随你挑）

就这些。无需外部服务、无需 API 密钥，纯 C# 加 Aspose 即可。

![Screenshot of a TIFF file being processed and the resulting text file](/images/ocr-result.png "OCR result showing converted TIFF to text output")

*(Alt text: Screenshot showing converted TIFF to text output on screen)*

## 第一步：设置 OCR 引擎 – 将 TIFF 转换为文本

首先，需要创建一个 `OcrEngine` 实例，并指定读取英文字符。引擎是转换的核心；正确配置可确保结果可靠。

```csharp
using Aspose.OCR;
using System.IO;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Create an OCR engine configured for English – this is the core of convert TIFF to text
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };
```

*为什么重要：*  
Aspose.OCR 支持数十种语言。如果你的扫描件是多语言的，只需将 `OcrLanguage.English` 改为相应的枚举值。若不指定语言，引擎会进入自动检测模式，速度更慢且准确度可能下降。

## 第二步：收集所有 TIFF 文件 – 高效提取 TIFF 文本

接下来，从你指定的文件夹中获取每个 *.tif* 文件。使用 `Directory.GetFiles` 可以得到一个干净的数组，供批处理使用。

```csharp
        // Locate every TIFF in the input folder – adjust the path to your own directory
        string inputFolder = @"C:\Scans\Batch";
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif", SearchOption.TopDirectoryOnly);

        if (tiffFiles.Length == 0)
        {
            System.Console.WriteLine("No TIFF files found. Check the folder path.");
            return;
        }
```

*小技巧：* 若扫描文件分布在子文件夹中，可使用 `SearchOption.AllDirectories` 标志。只需注意更深的递归可能会在批处理阶段增加内存占用。

## 第三步：并行执行 OCR – 批量图像转文本

现在进入有趣的部分。Aspose.OCR 提供了静态助手 `BatchOcr.RecognizeAll`，接受文件路径数组、引擎以及 `parallelism` 提示。我们将启动四个线程，在现代四核笔记本上几乎实现线性加速。

```csharp
        // Run OCR on all files in parallel (4 threads by default)
        // The result is a dictionary where Key = file path, Value = extracted text
        Dictionary<string, string> ocrResults = BatchOcr.RecognizeAll(tiffFiles, ocrEngine, parallelism: 4);
```

*为何使用并行？*  
批量处理高分辨率 TIFF 会消耗大量 CPU。将工作分配到多个线程可以让所有核心忙碌，从而显著缩短总运行时间。如果在拥有更多核心的服务器上运行，只需相应提升 `parallelism` 值。

## 第四步：写入输出 – 将扫描图像保存为 TXT 文件

最后遍历字典，将每段文本写入与原文件同名的 *.txt* 文件。这就是 **将扫描图像转换为 txt** 的实现时刻。

```csharp
        // Save each recognized text to a .txt file with the same base name as the source TIFF
        foreach (var kvp in ocrResults)
        {
            string sourcePath = kvp.Key;
            string extractedText = kvp.Value;

            // Change extension from .tif to .txt
            string txtPath = Path.ChangeExtension(sourcePath, ".txt");

            // Write the text – UTF‑8 ensures all characters are preserved
            File.WriteAllText(txtPath, extractedText);
            System.Console.WriteLine($"Saved: {txtPath}");
        }

        System.Console.WriteLine("Batch conversion complete!");
    }
}
```

### 代码做了什么（简明中文说明）

1. **创建** 一个设置为英文的 OCR 引擎。  
2. **收集** 目标文件夹下的所有 TIFF 文件。  
3. **调用** `BatchOcr.RecognizeAll`，使用四个线程将每张图像转换为字符串。  
4. **遍历** 结果，将 `.tif` 扩展名替换为 `.txt` 并写入磁盘。

这就是不到 50 行代码的完整 **将 TIFF 转换为文本** 工作流。

## 处理边缘情况 – 当出现问题时

- **缺失或损坏的 TIFF** – `BatchOcr` 会抛出 `OcrException`。如需优雅降级，请将调用包装在 `try / catch` 中。  
- **非英文文档** – 将 `OcrLanguage.English` 改为 `OcrLanguage.Spanish`、`OcrLanguage.French` 等，或使用 `OcrLanguage.AutoDetect`。  
- **超大图像** – 考虑在 OCR 前降低 DPI（`ocrEngine.ImagePreprocessing.Dpi = 200`），以节省内存，虽可能牺牲部分准确度。  
- **输出编码** – 如需特定代码页（例如 Windows‑1252），可使用 `File.WriteAllText(txtPath, extractedText, Encoding.GetEncoding(1252))`。

## 稳健批量转换的专业技巧

- **记录失败**：创建 `List<string> failedFiles`，将抛异常的文件加入列表，循环结束后写入日志。  
- **复用引擎**：同一个 `OcrEngine` 实例可在多文件间复用，切勿在循环内部实例化。  
- **验证结果**：使用 `if (string.IsNullOrWhiteSpace(extractedText))` 快速标记空白或不可读的扫描件。  
- **与 PDF 结合**：若源文件是多页 PDF，可先使用 Aspose.PDF 将每页转换为 TIFF，再执行本批处理。

## 后续步骤 – 超越简单转换

现在你已经能够 **批量提取 TIFF 文本**，接下来可以：

- 将 *.txt* 文件导入搜索索引（Elasticsearch、Azure Cognitive Search）。  
- 对每个结果进行语言检测，以将文档路由到对应的本地化流水线。  
- 通过在原始图像上叠加 OCR 文本生成可搜索的 PDF（再次使用 Aspose.PDF）。

所有这些场景都基于同一个核心概念：**批量图像转文本** 是更大文档处理系统的基石。

---

### 结论

你已经学会了如何使用 Aspose.OCR **将 TIFF 转换为文本**，并行处理整个文件夹，将每个结果保存为整洁的 *.txt* 文件。该方案轻量、可完全配置，且已准备好投入生产——无论是数字化遗留发票、归档扫描合同，还是为文本搜索引擎提供数据。

动手试一试，调节并行度，让这些新生成的文本文件流入你的任意工作流。祝你 OCR 愉快！

---


## 相关教程

- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}