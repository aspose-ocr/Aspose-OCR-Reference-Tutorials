---
category: general
date: 2026-06-25
description: 批量 OCR 处理教程展示了如何使用 Aspose.OCR 在 C# 中将图像转换为文本并从图像中提取文本。学习一步一步的实现方法。
draft: false
keywords:
- batch ocr processing
- convert images to text
- how to extract text from images
language: zh
og_description: C# 中的批量 OCR 处理可让您快速将图像转换为文本。请按照本指南学习如何使用 Aspose.OCR 从图像中提取文本。
og_title: C# 批量 OCR 处理 – 将图像转换为文本
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  headline: Batch OCR Processing in C# – Convert Images to Text Quickly
  type: TechArticle
- description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  name: Batch OCR Processing in C# – Convert Images to Text Quickly
  steps:
  - name: Expected Output
    text: 'When you run `dotnet run`, you’ll see something like:'
  - name: What image formats are supported?
    text: Aspose.OCR handles JPEG, PNG, TIFF, BMP, and GIF out of the box. If you
      encounter a format like WebP, convert it first or use a third‑party decoder.
  - name: Can I limit the OCR language to English only?
    text: 'Yes. Set the `Language` property on the `BatchRecognizer` before calling
      `Recognize`:'
  - name: How do I process thousands of files without blowing up memory?
    text: Break the list into smaller batches (e.g., 500 files each) and run the above
      routine in a loop. This keeps the in‑memory dictionary manageable and lets you
      log progress per batch.
  - name: What if I need the OCR results in a database instead of files?
    text: 'Replace the `File.WriteAllText` call with your preferred data‑access code.
      For example, using Dapper:'
  type: HowTo
tags:
- OCR
- Aspose
- C#
title: C# 批量 OCR 处理 — 快速将图像转换为文本
url: /zh/net/text-recognition/batch-ocr-processing-in-c-convert-images-to-text-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 批量 OCR 处理（C#）——快速将图像转换为文本

有没有想过如何 **批量 OCR 处理** 整个扫描文件夹，而无需为每个文件编写单独的循环？你并不是唯一有此需求的人。在许多项目中——比如发票自动化、旧文档归档，甚至是一个简单的个人照片转文本工具——你都需要 **将图像转换为文本** 大规模地进行。

好消息是？使用 Aspose.OCR，你可以用几行代码实现这一点。本指南将带你逐步完成一个完整、可直接运行的示例，展示如何使用批量 OCR 处理 **从图像中提取文本**，解释每个环节为何重要，并提供避免常见陷阱的技巧。

## 你将学到

- 为批量操作设置 Aspose.OCR。
- 配置并行度以加速大批量任务。
- 自动将 OCR 结果写入各自的 `.txt` 文件。
- 处理进度事件，让你随时了解运行情况。
- 扩展代码以实现自定义错误处理或不同的输出格式。

无需任何 Aspose 经验；只需具备基本的 C# 背景并已安装 .NET 6（或更高版本）。

---

## 步骤 1：为批量 OCR 处理准备项目

在深入代码之前，请确保已安装 Aspose.OCR NuGet 包。在项目文件夹中打开终端并运行：

```bash
dotnet add package Aspose.OCR
```

> **专业提示：** 使用最新的稳定版本（截至 2026 年 6 月为 23.9），以获得性能提升和最新的语言支持。

如果尚未创建控制台应用程序，请新建一个：

```bash
dotnet new console -n BatchOcrApp
cd BatchOcrApp
```

现在，你可以编写实际的批量 OCR 处理逻辑了。

## 步骤 2：定义要转换的图像文件

**批量 OCR 处理** 的第一步就是告诉识别器要处理哪些文件。你可以硬编码列表、从目录读取，甚至从数据库获取路径。为清晰起见，这里使用静态列表：

```csharp
// Step 2: List of image files to be processed
var imageFiles = new List<string>
{
    @"C:\Images\invoice1.jpg",
    @"C:\Images\receipt2.png",
    @"C:\Images\scan3.tif"
};
```

> **重要性说明：** 通过传递集合，`BatchRecognizer` 可以在内部跨多个线程调度工作，这正是快速 **将图像转换为文本** 操作的核心。

## 步骤 3：创建并配置 BatchRecognizer

现在进入本教程的核心。`BatchRecognizer` 类为你抽象了线程细节。你可以调节 `Parallelism` 属性以匹配 CPU 核心数，或设置自定义值以保留部分核心用于其他工作。

```csharp
// Step 3: Initialise the BatchRecognizer with optional settings
var ocrBatch = new BatchRecognizer
{
    // Number of concurrent threads (default = Environment.ProcessorCount)
    Parallelism = 4,

    // Optional: Hook into progress events for real‑time feedback
    ProgressChanged = (s, e) =>
        Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
};
```

> **解释：** 将 `Parallelism = 4` 设置为让库一次运行四个 OCR 任务。在典型的四核笔记本上，这能带来显著的加速而不会使系统饱和。如果在多核服务器上运行，可将此数值调高。

> **边缘情况：** 如果处理极大的图像，可能会触及内存限制。在这种情况下，降低并行度或将文件分成更小的批次处理。

## 步骤 4：运行 OCR 并捕获结果

在 `BatchRecognizer` 上调用 `Recognize` 会返回一个字典，键为原始文件路径，值为包含提取文本、置信度分数等信息的 `OcrResult`。

```csharp
// Step 4: Execute batch OCR – returns a map of file → OcrResult
IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);
```

> **返回内容：** 对于每张图像，`OcrResult.Text` 保存纯文本表示。这正是以编程方式 **从图像中提取文本** 时所需的。

## 步骤 5：将每个结果持久化为 .txt 文件

大多数实际场景需要将 OCR 输出保存下来以供后续处理——例如将其导入搜索索引或关联到数据库记录。下面的循环会在每个源图像旁边写入一个 `.txt` 文件，保留原始文件名。

```csharp
// Step 5: Write each OCR result to a corresponding .txt file
foreach (var entry in ocrResults)
{
    string txtPath = Path.ChangeExtension(entry.Key, ".txt");
    File.WriteAllText(txtPath, entry.Value.Text);
    Console.WriteLine($"Saved OCR text to {txtPath}");
}
```

> **提示：** 如果需要其他格式（JSON、CSV 等），只需按需序列化 `entry.Value`。`OcrResult` 对象还提供 `Confidence` 和 `PageCount`，如果这些指标对你有用的话。

## 步骤 6：发出完成信号并优雅地处理错误

干净的结束让你的工具更显专业。示例代码已经会打印最后一行，但我们可以添加 try‑catch 块，以捕获任何意外异常，例如文件缺失或不支持的图像格式。

```csharp
try
{
    // (All steps 2‑5 go here)
    Console.WriteLine("Batch OCR processing finished successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
}
```

> **包装原因：** 当在大型文件夹上运行程序时，单个损坏的图像可能导致整个任务中止。通过适当的错误处理，你可以记录问题并继续处理剩余文件。

## 完整、可直接运行的示例

下面是完整的程序代码，你可以复制粘贴到 `Program.cs` 中。请确保图像路径指向机器上的真实文件。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchExample
{
    static void Main()
    {
        try
        {
            // Step 2: Define the image files to be processed
            var imageFiles = new List<string>
            {
                @"C:\Images\invoice1.jpg",
                @"C:\Images\receipt2.png",
                @"C:\Images\scan3.tif"
            };

            // Step 3: Create a BatchRecognizer and configure optional settings
            var ocrBatch = new BatchRecognizer
            {
                // Set the degree of parallelism (default = Environment.ProcessorCount)
                Parallelism = 4,

                // Hook into progress events to monitor processing
                ProgressChanged = (s, e) =>
                    Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
            };

            // Step 4: Run OCR on the batch of images (returns file → OcrResult)
            IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);

            // Step 5: Write each OCR result to a corresponding .txt file
            foreach (var entry in ocrResults)
            {
                string txtPath = Path.ChangeExtension(entry.Key, ".txt");
                File.WriteAllText(txtPath, entry.Value.Text);
                Console.WriteLine($"Saved OCR text to {txtPath}");
            }

            // Step 6: Indicate that batch processing has completed
            Console.WriteLine("Batch OCR processing finished successfully.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
        }
    }
}
```

### 预期输出

运行 `dotnet run` 时，你会看到类似以下的输出：

```
Processed 1/3 – C:\Images\invoice1.jpg
Saved OCR text to C:\Images\invoice1.txt
Processed 2/3 – C:\Images\receipt2.png
Saved OCR text to C:\Images\receipt2.txt
Processed 3/3 – C:\Images\scan3.tif
Saved OCR text to C:\Images\scan3.txt
Batch OCR processing finished successfully.
```

每个 `.txt` 文件现在都包含对应图像的纯文本版本——这正是大规模 **将图像转换为文本** 所需的。

---

## 常见问题与边缘情况

### 支持哪些图像格式？

Aspose.OCR 开箱即支持 JPEG、PNG、TIFF、BMP 和 GIF。如果遇到 WebP 等格式，请先进行转换或使用第三方解码器。

### 能否仅将 OCR 语言限制为英文？

可以。在调用 `Recognize` 之前，设置 `BatchRecognizer` 的 `Language` 属性：

```csharp
ocrBatch.Language = "en";
```

限制语言可以提升准确度和速度，尤其是当你只关注单一语言的 **从图像中提取文本** 时。

### 如何在不耗尽内存的情况下处理成千上万的文件？

将列表拆分为更小的批次（例如每批 500 个文件），在循环中运行上述例程。这样可以保持内存中的字典规模可控，并且可以按批记录进度。

### 如果需要将 OCR 结果存入数据库而不是文件怎么办？

将 `File.WriteAllText` 调用替换为你偏好的数据访问代码。例如，使用 Dapper：

```csharp
connection.Execute(
    "INSERT INTO OcrResults (FilePath, Text) VALUES (@Path, @Text)",
    new { Path = entry.Key, Text = entry.Value.Text });
```

## 结论

你已经掌握了使用 Aspose.OCR 在 C# 中进行 **批量 OCR 处理**，学会了干净利落的 **将图像转换为文本** 方法，并发现了多条高效 **从图像中提取文本** 的实用技巧。完整的工作流——收集文件路径、配置 `BatchRecognizer`、运行 OCR、持久化结果——全部浓缩在一个易读的程序中。

接下来可以做什么？在多核服务器上提升 `Parallelism`，尝试不同的语言包，或加入拼写检查等后处理。你甚至可以将提取的文本导入 Azure Cognitive Search，让扫描文档在几秒钟内可搜索。

有想分享的技巧吗——比如 OCR PDF 或处理多页 TIFF？在下方留言，让我们继续交流。祝编码愉快！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，构建在已演示的技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 OCR 操作在文件夹中提取图像文本](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [如何在 Aspose.OCR for .NET 中使用列表批量 OCR 图像](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [如何使用 Aspose.OCR for .NET 从 ZIP 存档中提取文本](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}