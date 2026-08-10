---
category: general
date: 2026-05-31
description: 如何在 C# 中使用 Aspose OCR 批量进行 OCR。学习将图像转换为文本、从图像中提取文本，并高效处理多个文件。
draft: false
keywords:
- how to batch OCR
- convert images to text
- extract text from images
- OCR multiple files
- batch OCR processing
language: zh
og_description: 如何在 C# 中使用 Aspose OCR 批量 OCR。将图像转换为文本，从图像中提取文本，并轻松处理多个文件的 OCR。
og_title: 如何在 C# 中批量 OCR – 完整编程指南
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  headline: How to Batch OCR in C# – Complete Programming Guide
  type: TechArticle
- description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  name: How to Batch OCR in C# – Complete Programming Guide
  steps:
  - name: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
    text: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
  - name: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
    text: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
  - name: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
    text: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- batch-processing
title: 如何在 C# 中批量 OCR – 完整编程指南
url: /zh/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR – 完整编程指南

是否曾想过 **如何批量 OCR** 整个文件夹的扫描图片，而不必手动打开每个文件？你并不是唯一有此需求的人。在许多实际项目中——比如发票自动化或历史照片归档——你需要 **批量将图像转换为文本**，而逐个处理会耗费大量时间。

在本教程中，我们将演示一个可直接运行的 C# 控制台应用程序，它会读取源目录下的所有 PNG、JPG 或 TIFF 文件，使用 Aspose OCR 对每个文件进行识别，并将相应的 *.txt* 文件写入输出文件夹。完成后，你将能够 **从图像中提取文本**、处理 **多个文件的 OCR**，并拥有一个坚实的基础，以便后续进行任何 **批量 OCR 处理**。

## 你将学到

- 使用 Aspose OCR NuGet 包搭建 .NET 项目。  
- 为 **批量 OCR** 运行定义源文件夹和目标文件夹。  
- 枚举支持的图像类型并将其传递给 OCR 引擎。  
- 将识别出的文本写入单独的 *.txt* 文件，实质上 **将图像转换为文本**。  
- 解决常见问题，如缺少文件夹、不受支持的格式以及性能调优。

不需要事先了解 Aspose；只要具备基本的 C# 和 Visual Studio 知识即可上手。

---

![Diagram showing the flow of batch OCR processing from image folder to text output – how to batch OCR](/images/batch-ocr-flow.png){alt="how to batch OCR flow diagram"}

## 如何批量 OCR – 项目设置

在编写代码之前，请确保你已经具备以下环境：

1. 已安装 **.NET 6 SDK**（或更高版本）——最新运行时提供更好的性能和对异步 I/O 的原生支持。  
2. **Visual Studio 2022**（Community 版完全足够）或其他你喜欢的编辑器。  
3. **Aspose.OCR** NuGet 包。通过包管理器控制台安装：

   ```powershell
   Install-Package Aspose.OCR
   ```

就这些。后续教程默认该包已正确引用。

## 第 2 步：准备源文件夹和目标文件夹（将图像转换为文本）

首先，需要两个文件夹：一个存放原始图片，另一个用于保存生成的 *.txt* 文件。下面的代码会在目标文件夹不存在时自动创建——无需手动操作。

```csharp
// Define where the images live and where the text files will go
string sourceFolder = @"C:\OCR\Batch";
string outputFolder = @"C:\OCR\BatchTxt";

// Ensure the output directory exists; CreateDirectory is idempotent
Directory.CreateDirectory(outputFolder);
```

> **为什么重要：** 如果省略 `CreateDirectory` 调用，程序在尝试写入第一 个文本文件时会抛出 `DirectoryNotFoundException`。提前处理可以让批量 OCR 过程更加稳健。

## 第 3 步：枚举用于 OCR 多文件的图像文件

接下来，我们收集所有符合支持格式的文件。使用 LINQ 可以让代码简洁且易读。

```csharp
// Grab all PNG, JPG, and TIFF files from the source folder (non‑recursive)
var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
    .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));
```

> **提示：** 如果以后需要处理 PDF 或 BMP，只需在 `Where` 子句中扩展即可。将过滤条件集中管理，可让后续修改轻松无痛。

## 第 4 步：对每张图像运行 OCR 引擎（如何批量 OCR）

现在进入核心：将每张图像送入 Aspose OCR 并获取识别文本。下面的循环为每个文件创建一个全新的 `OcrEngine` 实例——这保证了前一张图像的内存会在处理下一张之前被释放。

```csharp
foreach (var imagePath in imageFiles)
{
    // Initialize the OCR engine with the current image
    OcrEngine ocrEngine = new OcrEngine
    {
        Image = ImageStream.FromFile(imagePath)
    };

    // Perform recognition; Recognize() returns an OcrResult object
    OcrResult ocrResult = ocrEngine.Recognize();

    // Build the output .txt file path (same base name, .txt extension)
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    // Persist the extracted text
    File.WriteAllText(textFilePath, ocrResult.Text);

    Console.WriteLine($"Processed {Path.GetFileName(imagePath)} → {Path.GetFileName(textFilePath)}");
}
```

**发生了什么？**  

- `ImageStream.FromFile` 将图像加载为 Aspose 可读取的流。  
- `ocrEngine.Recognize()` 执行实际的 OCR 算法，返回的字符串位于 `ocrResult.Text` 中。  
- `File.WriteAllText` 将该字符串写入磁盘，实质上 **从图像中提取文本**。

### 处理边缘情况

- **损坏的图像** – 将识别调用包装在 `try/catch` 中并记录失败，然后继续处理下一个文件。  
- **大批量** – 如果机器拥有多核，考虑使用 `Parallel.ForEach` 进行异步处理。  
- **不同语言** – 在调用 `Recognize()` 前设置 `ocrEngine.Language = Language.English;` 或其他受支持语言。

## 第 5 步：保存提取的文本（从图像中提取文本）

上面的代码片段已经实现了 OCR 输出的保存，但我们可以把这段逻辑抽取到一个帮助方法中。这样可以让主循环更简洁，并便于复用。

```csharp
static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
{
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    File.WriteAllText(textFilePath, recognizedText);
}
```

随后将内联的 `File.WriteAllText` 调用替换为：

```csharp
SaveOcrResult(outputFolder, imagePath, ocrResult.Text);
```

> **为什么要抽取为方法？** 这将识别逻辑与持久化逻辑分离，并为后续的后处理（如去除空白或追加时间戳）提供统一入口。

## 完整可运行示例 – C# 中的批量 OCR 处理

将所有代码片段组合起来，下面是一个可以直接复制到新 Console App 项目并立即运行的完整程序。

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Define source & destination folders
            string sourceFolder = @"C:\OCR\Batch";
            string outputFolder = @"C:\OCR\BatchTxt";

            // 2️⃣ Make sure the output folder exists
            Directory.CreateDirectory(outputFolder);

            // 3️⃣ Get all supported image files (convert images to text)
            var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
                .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));

            // 4️⃣ Process each image (how to batch OCR)
            foreach (var imagePath in imageFiles)
            {
                try
                {
                    // Initialise OCR engine for the current file
                    OcrEngine ocrEngine = new OcrEngine
                    {
                        Image = ImageStream.FromFile(imagePath)
                    };

                    // Run OCR – this extracts text from images
                    OcrResult result = ocrEngine.Recognize();

                    // 5️⃣ Save the result (extract text from images)
                    SaveOcrResult(outputFolder, imagePath, result.Text);

                    Console.WriteLine($"✅ {Path.GetFileName(imagePath)} processed.");
                }
                catch (Exception ex)
                {
                    // Gracefully handle problematic files
                    Console.WriteLine($"⚠️ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }

            Console.WriteLine("🎉 Batch OCR processing complete!");
        }

        // Helper to write the OCR output to a .txt file
        static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
        {
            string textFilePath = Path.Combine(outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, recognizedText);
        }
    }
}
```

### 预期输出

运行程序后，控制台会输出类似以下的行：

```
✅ invoice001.png processed.
✅ receipt123.jpg processed.
✅ map.tif processed.
🎉 Batch OCR processing complete!
```

与此同时，`C:\OCR\BatchTxt` 文件夹将包含：

- `invoice001.txt`
- `receipt123.txt`
- `map.txt`

每个文件都保存了对应源图像的纯文本表示，便于索引、搜索或后续分析。

## 专业技巧与常见陷阱（批量 OCR 处理）

- **内存管理：** Aspose OCR 在每次 `Recognize()` 调用后会释放图像缓冲区，但如果处理成千上万的文件，建议适度调用 `GC.Collect()` 以保持内存占用低。  
- **加速方法：** 在 .NET 6 及以上版本中使用 `OcrEngine.RecognizeAsync()`，并结合 `Task` 并行执行多个任务，以充分利用多核 CPU。  

## 接下来该学习什么？

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Perform OCR on Archive Images with Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}