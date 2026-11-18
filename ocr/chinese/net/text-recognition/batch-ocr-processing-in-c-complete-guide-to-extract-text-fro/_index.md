---
category: general
date: 2026-06-16
description: 在 C# 中进行批量 OCR 处理，可快速将图像转换为文本。学习如何使用 Aspose.OCR 通过一步步的代码从图像中提取文本。
draft: false
keywords:
- batch OCR processing
- extract text from images
- convert images to text
language: zh
og_description: 在 C# 中进行批量 OCR 处理，将图像转换为文本。请按照本指南使用 Aspose.OCR 从图像中提取文本。
og_title: C# 批量 OCR 处理 – 从图像中提取文本
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  headline: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  type: TechArticle
- description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  name: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  steps:
  - name: Expected Output
    text: 'Assuming you have three images (`invoice1.png`, `receipt2.jpg`, `form3.tif`)
      in the input folder, the output folder will contain:'
  - name: What if some images fail to process?
    text: '`OcrBatchProcessor` logs errors to the console by default and continues
      with the next file. For production use, you can subscribe to the `OnError` event
      to collect failed filenames and retry later.'
  - name: Can I process PDFs directly?
    text: Yes. Aspose.OCR treats each page of a PDF as an image internally. Just point
      `InputFolder` to a directory containing PDFs, and the processor will extract
      text from every page—effectively **convert images to text** even when the source
      is a PDF.
  - name: How do I handle multi‑language documents?
    text: Set `Language` to `OcrLanguage.Multilingual` or specify a list of languages
      if the library version supports it. The engine will attempt to recognize characters
      from all provided languages, which is handy for international invoices.
  - name: What about memory consumption?
    text: The batch processor streams each image, so memory usage stays low even with
      thousands of files. However, enabling a high `MaxDegreeOfParallelism` on a memory‑constrained
      machine could cause spikes. Monitor your RAM and adjust the thread count accordingly.
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: C# 批量 OCR 处理——从图像中提取文本的完整指南
url: /zh/net/text-recognition/batch-ocr-processing-in-c-complete-guide-to-extract-text-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# 批量 OCR 处理 – 完整指南：从图像中提取文本

是否曾想过在 C# 中 **批量 OCR 处理** 而不必为每张图片单独写循环？你并不孤单。当你面对数十甚至数百张扫描的收据、发票或手写笔记时，手动将每个文件喂给 OCR 引擎很快就会变成噩梦。

好消息是？使用 Aspose.OCR，你可以一次性、整洁地 *将图像转换为文本*。在本教程中，我们将完整演示工作流，从安装库到运行生产级批处理任务，**从图像中提取文本** 并将结果保存为你需要的格式。

> **你将得到：** 一个可直接运行的控制台应用程序，能够处理整个文件夹，在原始文件旁边生成纯文本（或 JSON、XML、HTML、PDF）文件，并展示如何调节并行度以获得最大吞吐量。

## 前置条件

- .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）
- Visual Studio 2022、VS Code 或任意你喜欢的 C# 编辑器
- Aspose.OCR NuGet 许可证（免费试用版可用于评估）
- 一个包含图像文件（`.png`、`.jpg`、`.tif` 等）的文件夹，你希望 **将图像转换为文本**

如果这些条件都已满足，下面开始吧。

![Diagram illustrating batch OCR processing flow](batch-ocr-workflow.png "Batch OCR processing flow")

## 步骤 1：通过 NuGet 安装 Aspose.OCR

首先，将 Aspose.OCR 包添加到项目中。在项目目录打开终端并运行：

```bash
dotnet add package Aspose.OCR
```

或者，如果你在 Visual Studio 中，右键点击 *Dependencies → Manage NuGet Packages*，搜索 **Aspose.OCR**，然后点击 *Install*。这行命令会把进行 **批量 OCR 处理** 所需的一切拉进来。

> **小贴士：** 保持包版本最新；截至 2026 年 6 月的最新版本已支持更多图像格式并提升了多语言识别准确度。

## 步骤 2：创建控制台骨架

创建一个新的 C# 控制台应用（如果还没有），并用下面的骨架代码替换生成的 `Program.cs`。注意顶部的 `using Aspose.OCR;` 指令——它提供了 `OcrBatchProcessor` 类。

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // We'll fill this in later.
    }
}
```

此时文件仅是占位符，但为我们的 **批量 OCR 处理** 逻辑提供了干净的起点。

## 步骤 3：初始化 OcrBatchProcessor

`OcrBatchProcessor` 是负责扫描文件夹、对每个支持的图像执行 OCR 并写入输出的核心。实例化它非常简单：

```csharp
// Step 3: Create an OCR batch processor instance
var ocrBatchProcessor = new OcrBatchProcessor();
```

为什么使用批处理器而不是单图像 API？批处理类会自动处理文件枚举、错误日志，甚至并行执行，这意味着你可以少写循环，多专注于调优准确度。

## 步骤 4：指定输入和输出文件夹

告诉处理器从哪里读取图像以及把结果写到哪里。将占位路径替换为你机器上的真实目录。

```csharp
// Step 4: Configure the input folder containing images to process
ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

// Step 5: Set the folder where OCR results will be saved
ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";
```

两个文件夹在运行应用前必须已存在，否则会抛出 `DirectoryNotFoundException`。虽然可以在代码中创建它们，为了清晰起见这里保持示例简洁。

## 步骤 5：选择输出格式

Aspose.OCR 可以输出纯文本、JSON、XML、HTML，甚至 PDF。对大多数 **从图像中提取文本** 场景来说，纯文本已足够，但你也可以随意切换。

```csharp
// Step 6: Choose the desired output format (e.g., plain text)
ocrBatchProcessor.OutputFormat = ResultFormat.Text;   // alternatives: Json, Xml, Html, Pdf, etc.
```

如果需要结构化数据供后续处理，`ResultFormat.Json` 是稳妥的选择。库会自动将每页文本包装成 JSON 对象，并保留布局信息。

## 步骤 6：设置语言和并行度

OCR 的准确性依赖于正确的语言模型。英语适用于大多数西文文档，但你也可以选择任何受支持的语言（阿拉伯语、中文等）。此外，你还能指定处理器使用的线程数——默认最多四个。

```csharp
// Step 7: Specify the language for OCR recognition
ocrBatchProcessor.Language = OcrLanguage.English;

// Step 8: Define the level of parallelism (up to 4 concurrent threads)
ocrBatchProcessor.MaxDegreeOfParallelism = 4;
```

**并行度为何重要：** 如果你的机器是四核 CPU，将 `MaxDegreeOfParallelism` 设置为 `4` 可以将处理时间缩短约 75%。在双核笔记本上，`2` 更为安全。请根据硬件自行实验，找到最佳配置。

## 步骤 7：运行批处理任务

现在重活儿开始了。只需一行代码即可启动整个管道，处理输入文件夹中的所有图像并将结果写入输出文件夹。

```csharp
// Step 9: Execute the batch processing of all supported image files
ocrBatchProcessor.Execute();

Console.WriteLine("Batch OCR completed.");
```

当控制台打印出 *Batch OCR completed.* 时，你会在每个原始图像旁边看到一个 `.txt`（或你选择的其他格式）文件。文件名与源文件保持一致，便于快速对应 OCR 输出与原始图片。

## 完整工作示例

将所有代码整合在一起，下面是可以直接复制粘贴到 `Program.cs` 并立即运行的完整程序：

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create an OCR batch processor instance
        var ocrBatchProcessor = new OcrBatchProcessor();

        // Step 2: Configure the input folder containing images to process
        ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

        // Step 3: Set the folder where OCR results will be saved
        ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";

        // Step 4: Choose the desired output format (plain text is default)
        ocrBatchProcessor.OutputFormat = ResultFormat.Text; // alternatives: Json, Xml, Html, Pdf, etc.

        // Step 5: Specify the language for OCR recognition
        ocrBatchProcessor.Language = OcrLanguage.English;

        // Step 6: Define the level of parallelism (up to 4 concurrent threads)
        ocrBatchProcessor.MaxDegreeOfParallelism = 4;

        // Step 7: Execute the batch processing of all supported image files
        ocrBatchProcessor.Execute();

        Console.WriteLine("Batch OCR completed.");
    }
}
```

### 预期输出

假设输入文件夹中有三张图片（`invoice1.png`、`receipt2.jpg`、`form3.tif`），则输出文件夹会包含：

```
invoice1.txt
receipt2.txt
form3.txt
```

每个 `.txt` 文件保存了对应图像提取的原始字符。使用记事本打开任意文件，即可看到原始扫描的纯文本表现。

## 常见问题与边缘情况

### 某些图像处理失败怎么办？

`OcrBatchProcessor` 默认会将错误日志输出到控制台，并继续处理下一个文件。生产环境下，你可以订阅 `OnError` 事件，以收集失败的文件名并稍后重试。

```csharp
ocrBatchProcessor.OnError += (sender, args) =>
{
    Console.WriteLine($"Failed on {args.FileName}: {args.Exception.Message}");
};
```

### 能直接处理 PDF 吗？

可以。Aspose.OCR 会把 PDF 的每一页内部当作图像处理。只需将 `InputFolder` 指向包含 PDF 的目录，处理器就会从每页提取文本——即使源文件是 PDF，也能 **将图像转换为文本**。

### 如何处理多语言文档？

将 `Language` 设置为 `OcrLanguage.Multilingual`，或在库版本支持的情况下指定语言列表。引擎会尝试识别所有提供语言的字符，这对国际发票非常有用。

### 内存消耗如何？

批处理器会对每张图像进行流式处理，即使文件数千也能保持低内存占用。不过，在内存受限的机器上开启过高的 `MaxDegreeOfParallelism` 可能导致内存峰值。请监控 RAM 使用情况并相应调整线程数。

## 提升准确性的技巧

- **预处理图像**：在 OCR 前清除噪点、纠正倾斜并转为灰度。Aspose.OCR 提供 `ImagePreprocessOptions`，可附加到 `ocrBatchProcessor`。
- **选择合适的格式**：如果需要保留布局，`ResultFormat.Html` 或 `Pdf` 能保持换行和基本样式。
- **验证结果**：实现一个简单的后处理步骤，检查是否出现空输出文件——空文件通常意味着识别失败。

## 后续步骤

掌握了 **批量 OCR 处理** 与 **从图像中提取文本** 之后，你可能想要：

- **集成数据库** —— 将每条 OCR 结果连同元数据一起存储，以便搜索。
- **添加 UI** —— 构建一个小型 WPF 或 WinForms 前端，让用户拖拽文件夹。
- **横向扩展** —— 在 Azure Functions 或 AWS Lambda 上运行批处理任务，实现云原生处理。

上述主题都基于本指南的核心概念，你已经具备了进一步扩展解决方案的能力。

---

**祝编码愉快！** 如遇到问题或有改进想法，欢迎在下方留言。让我们一起让 OCR 自动化更加顺畅。

## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并探索在项目中的其他实现方式，每篇资源都提供完整可运行的代码示例和逐步解释。

- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}