---
category: general
date: 2026-02-22
description: 如何使用 Aspose.OCR 在 C# 中批量 OCR JPEG 图像。学习从 JPG 提取文本、将 JPG 转换为 TXT，并高效批量处理图像。
draft: false
keywords:
- how to batch ocr
- extract text from jpg
- convert jpg to txt
- batch process images
- c# ocr example
language: zh
og_description: 如何使用 Aspose.OCR 在 C# 中批量 OCR JPEG 图像。本教程向您展示如何从 JPG 中提取文本、将 JPG 转换为
  TXT，并在几分钟内批量处理图像。
og_title: 如何在 C# 中批量 OCR JPEG 图像 – 完整指南
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中批量 OCR JPEG 图像 – 完整指南
url: /zh/net/text-recognition/how-to-batch-ocr-jpeg-images-in-c-complete-guide/
---

.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR JPEG 图像 – 完整指南

是否曾经想过 **如何批量 OCR** 一个装满图片的文件夹，而不必为每个文件编写单独的程序？在本指南中，我们将向您展示如何使用 Aspose.OCR **批量 OCR** JPEG 文件，这样您只需几行代码就能 **从 jpg 中提取文本** 并 **将 jpg 转换为 txt**。  

如果您曾经盯着一堆扫描的发票目录并想，“一定有更快的方法”，那么您来对地方了。我们将逐步演示每一步，解释每个环节为何重要，并提供一些处理大批量文件的专业技巧。

## 您将构建的内容

通过本教程的学习，您将拥有一个小型控制台应用程序，它能够：

* 扫描指定目录下的 `*.jpg` 文件。  
* 将每张图片送入 Aspose OCR 引擎（如果有兼容的显卡，可使用 GPU 加速）。  
* 将识别出的文本写入与原图并列的 `.txt` 文件中。  

无需外部服务，无需手动复制粘贴——纯 C# 加上可靠的 OCR 库即可。

### 前置条件

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.8）。  
* Visual Studio 2022 或任何支持 C# 的编辑器。  
* Aspose.OCR NuGet 包（免费试用版可用于测试）。  

如果缺少上述任意项，请先暂停并完成安装；后续内容默认这些已就绪。

![批量 OCR 示例](/images/how-to-batch-ocr.png "批量 OCR 流程图")

## 第 1 步：安装 Aspose.OCR NuGet 包

首先，项目需要引入 OCR 库。在解决方案文件夹的终端中运行：

```bash
dotnet add package Aspose.OCR
```

或者在 Visual Studio 中使用 NuGet 包管理器 UI。这样会把所有必需的依赖拉进来，包括在机器支持的情况下的 GPU 版二进制文件。

> **专业提示：** 如果计划在没有 GPU 的服务器上运行，后续将 `UseGpu = false`；引擎会自动回退到 CPU。

## 第 2 步：配置 OCR 引擎

创建并配置 `OcrEngine` 是魔法开始的地方。您需要告诉引擎期望的语言、是否使用 GPU，以及输出的格式。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 2: Initialize and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most documents; change if you need another language.
    Language = Language.English,

    // Enable GPU for faster processing on supported hardware.
    UseGpu = true,

    // We only need plain text for our .txt files.
    OutputFormat = OutputFormat.Text
};
```

**为什么重要：** 设置 `Language` 能提升准确率，因为引擎可以缩小字符集范围。启用 `UseGpu` 在现代显卡上可以将处理时间减半，这在 **批量处理图像** 时是显著的优势。

## 第 3 步：识别文件夹中的所有 JPEG 文件

现在交给 Aspose 完成繁重的工作。静态方法 `BatchProcessor.RecognizeFolder` 会遍历目录，对每个匹配的文件执行 OCR，并返回结果集合。

```csharp
using System.Collections.Generic;

// ...

// Step 3: Run OCR on every *.jpg in the target directory
IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
    ocrEngine,
    @"C:\Images\Invoices",   // <-- replace with your folder path
    searchPattern: "*.jpg"); // Only JPEG files are processed
```

**边缘情况处理：** 如果文件夹中包含子目录，可以使用 `SearchOption.AllDirectories` 重载（或手动递归），确保不遗漏任何文件。

## 第 4 步：将每个结果写入对应的 `.txt` 文件

`OcrResult` 对象包含原始文件路径和识别文本。遍历它们，修改扩展名并写入输出即可。

```csharp
using System.IO;

// ...

// Step 4: Persist OCR results as .txt files next to the source images
foreach (var result in ocrResults)
{
    // Change "image.jpg" → "image.txt"
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");

    // Save the extracted text
    File.WriteAllText(txtFilePath, result.Text);
}
```

就这么简单——每个 JPEG 现在都有一个配套的文本文件，您可以将其送入后续流程、搜索索引，或直接归档。

## 第 5 步：运行应用并验证输出

编译并运行程序：

```bash
dotnet run
```

假设文件夹中有 `invoice1.jpg` 和 `receipt2.jpg`，您应当看到 `invoice1.txt` 与 `receipt2.txt` 出现在同一目录下。打开任意 `.txt` 文件，您会看到原始 OCR 输出，例如：

```
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

如果文本出现乱码，请检查源图像的对比度是否足够，以及 `Language` 属性是否与文档语言匹配。

## 第 6 步：高级微调（可选）

### a) 处理低质量扫描

有时 JPEG 噪点较多。您可以使用 Aspose.Imaging 或其他库对图像进行预处理：

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

// Example: increase contrast before OCR
using (var image = Image.Load(result.SourceFilePath))
{
    image.Contrast = 30; // boost contrast
    image.Save(result.SourceFilePath); // overwrite or save to temp file
}
```

### b) 并行化批处理

如果文件很多且 CPU 为多核，可将循环包装在 `Parallel.ForEach` 中：

```csharp
Parallel.ForEach(ocrResults, result =>
{
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
    File.WriteAllText(txtFilePath, result.Text);
});
```

需要注意的是，Aspose OCR 引擎本身并非线程安全；每个线程必须拥有独立的 `OcrEngine` 实例或使用并发队列。

### c) 日志记录与错误处理

一个健壮的方案会记录失败，以便后续重试：

```csharp
try
{
    // OCR and write logic here
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {result.SourceFilePath}: {ex.Message}");
    // Optionally write to a log file
}
```

## 完整工作示例

将所有代码整合在一起，下面是可以直接复制粘贴到新 Console App 中的完整程序：

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create and configure the OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = Language.English,
            UseGpu = true,
            OutputFormat = OutputFormat.Text
        };

        // 2️⃣ Recognize all JPEG images in the target folder
        IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
            ocrEngine,
            @"C:\Images\Invoices",   // <-- change to your directory
            searchPattern: "*.jpg");

        // 3️⃣ Write each OCR result to a matching .txt file
        foreach (var result in ocrResults)
        {
            string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
            File.WriteAllText(txtFilePath, result.Text);
        }

        Console.WriteLine("Batch OCR complete. Check the folder for .txt files.");
    }
}
```

运行它，观察控制台输出，然后打开几个 `.txt` 文件，以确认 **从 jpg 中提取文本** 步骤已成功。

---

## 结论

我们已经完整演示了 **如何在 C# 中批量 OCR** JPEG 图像，使用 Aspose.OCR 将每张图片转换为可搜索的 `.txt` 文件。该方案简洁、支持 GPU，并且易于扩展以加入错误处理、图像预处理或并行执行等功能。  

如果您想进一步深入，可以考虑以下方向：

* 通过修改 `searchPattern`，**批量处理其他格式**（`*.png`、`*.tif`）的图像。  
* 将输出与 Lucene.NET 等全文检索引擎结合，实现即时文档查找。  
* 探索 Aspose 的 PDF 转换功能，直接生成可搜索的 PDF 文档。  

欢迎随意实验——更换语言、关闭 GPU，或将文本导入数据库。核心模式保持不变，现在您已经拥有坚实的基础可以继续构建。

祝编码愉快，愿您的 OCR 流程始终快速且精准！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}