---
category: general
date: 2026-04-11
description: 使用 Aspose OCR 批处理在 C# 中提取 TIFF 文件的文本。了解如何高效处理批量 OCR 并获取实时进度反馈。
draft: false
keywords:
- extract text from tiff
- process batch ocr
- OCR batch processing
- Aspose OCR C#
- TIFF image OCR
language: zh
og_description: 使用 Aspose OCR 批处理在 C# 中从 TIFF 文件提取文本。本教程逐步演示如何进行批量 OCR 处理并读取进度。
og_title: 在 C# 中使用批量 OCR 从 TIFF 提取文本 – 完整指南
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 在 C# 中使用批量 OCR 从 TIFF 提取文本 – 完整指南
url: /zh/net/text-recognition/extract-text-from-tiff-with-batch-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 TIFF 中提取文本 – 批量 OCR 完整指南

是否曾需要**从 TIFF**文件中提取文本，但在批处理阶段卡住了？你并不是唯一遇到这种情况的人。在许多文档自动化项目中，处理数十个高分辨率的 TIF 图像很快会成为瓶颈——尤其是当你想要实时的进度反馈时。  

好消息是？使用 Aspose OCR，你可以在几行代码中**process batch OCR**，获取实时进度事件，并输出每个图像的识别文本。在本教程中，我们将逐步演示一个可直接运行的 C# 控制台应用程序，完成这些操作。  

我们将覆盖你需要了解的所有内容：必需的包、每行代码为何重要、缺失文件等边缘情况，以及如何验证结果。完成后，你就可以将示例直接放入自己的解决方案中，立即开始从 TIFF 图像中提取文本。  

## 你需要的条件

- **.NET 6 或更高**（代码同样可以在 .NET Core 上编译）  
- **Aspose.OCR for .NET** NuGet 包 – `Install-Package Aspose.OCR`  
- 一个包含若干你想读取的 **TIFF** 图像的文件夹（演示使用 `img1.tif`、`img2.tif`、`img3.tif`）  
- 任意你喜欢的 IDE——Visual Studio、Rider 或 VS Code 都可以  

无需额外配置；该库自带 OCR 引擎，无需安装外部本机二进制文件。

---

## 第一步 – 创建 OCR 引擎实例  

首先需要实例化一个 `OcrEngine`。可以把它看作分析每个像素并将其转化为字符的大脑。

```csharp
using Aspose.OCR;

// Step 1: Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **为什么这很重要：**  
> 引擎保存内部语言模型和设置（例如 DPI、语言）。只创建一次并在批处理中重复使用，比对每张图像实例化新引擎要高效得多。  

---

## 第二步 – 绑定实时进度事件  

如果你正在处理数十个 TIFF 文件，进度指示器可以帮助你避免怀疑应用是否卡住。

```csharp
using Aspose.OCR.Events;

// Step 2: Subscribe to progress updates
ocrEngine.ProgressChanged += Ocr_ProgressChanged;

// Event handler definition (placed later in the file)
```

`ProgressChanged` 事件在每张图像处理完毕后触发，提供 `Current`、`Total` 和 `Percentage`。这就是大多数开发者忘记实现的 **process batch OCR** 反馈循环。  

---

## 第三步 – 构建图像流列表  

Aspose.OCR 使用 `ImageStream` 对象。最简单的方式是从磁盘加载每个 TIFF。

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Step 3: Prepare the batch of TIFF images
List<ImageStream> imageFiles = new List<ImageStream>
{
    ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
};
```

> **提示：**  
> 如果文件夹是动态的，请将硬编码的列表替换为 `Directory.GetFiles(path, "*.tif")` 并使用 `Select(ImageStream.FromFile)` ——这样你就可以真正 **process batch OCR**，无需手动更新。  

---

## 第四步 – 运行批量 OCR 处理  

现在开始进行繁重的工作。`ProcessBatch` 返回一个只读的 `OcrResult` 对象列表，每个对象包含提取的文本和置信度分数。

```csharp
// Step 4: Execute batch OCR and collect results
IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);
```

> **为什么这很高效：**  
> 引擎在所有图像之间复用相同的语言模型，与单图像调用相比显著降低内存消耗。  

---

## 第五步 – 显示或存储识别文本  

最后，遍历结果。在实际项目中，你可能会将它们写入数据库或 JSON 文件，但在本演示中我们仅将其打印到控制台。

```csharp
// Step 5: Output the recognised text for each TIFF
foreach (var result in ocrResults)
{
    Console.WriteLine("=== OCR Result ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();
}
```

**预期的控制台输出**（为简洁起见已截断）：

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,250.00

=== OCR Result ===
Meeting Minutes
1. Project kickoff...
```

如果某张图像处理失败，`result.Text` 将为空字符串，且 `ProgressChanged` 事件仍会将该项标记为已处理——因此你可以单独记录失败情况。  

---

## 进度事件处理器（完整代码）

将此方法放在 `BatchDemo` 类中的任意位置——最好在 `Main` 方法之后。

```csharp
private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
{
    // Gives you a live view of how many files have been processed
    Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
}
```

> **专业提示：**  
> 如果你在构建桌面应用，可以将此输出重定向到 UI 进度条；相同的事件同样适用于 WinForms、WPF，甚至 ASP.NET Core SignalR 通知。  

---

## 完整、可直接运行的示例  

将所有内容整合后，下面是完整的程序，你可以复制粘贴到新的控制台项目中。

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Events;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Subscribe to progress events
        ocrEngine.ProgressChanged += Ocr_ProgressChanged;

        // 3️⃣ Load TIFF images into a list
        List<ImageStream> imageFiles = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
        };

        // 4️⃣ Run batch OCR
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);

        // 5️⃣ Print results
        foreach (var result in ocrResults)
        {
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();
        }
    }

    // Progress event handler
    private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
    {
        Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
    }
}
```

将文件保存为 `Program.cs`，运行 `dotnet add package Aspose.OCR`，将 `YOUR_DIRECTORY` 替换为实际路径，然后按 **Ctrl+F5**。你应该会看到进度数字，随后是每个 TIFF 的提取文本。  

---

## 处理常见边缘情况  

| Situation | What to Watch For | Quick Fix |
|-----------|-------------------|-----------|
| **缺失或损坏的 TIFF** | `ImageStream.FromFile` throws `FileNotFoundException` or `ArgumentException`. | 将列表创建包装在 `try/catch` 中，跳过无效文件并记录问题。 |
| **非常大的图像（>10 MP）** | OCR 可能会消耗大量内存并导致变慢。 | 在处理前降低 DPI：`ocrEngine.ImagePreprocessing.Dpi = 300;` |
| **非英文文本** | 默认语言模型是英文。 | 设置 `ocrEngine.Language = Language.Spanish;`（或任何受支持的语言）。 |
| **需要保存结果** | 控制台输出不是持久化的。 | 使用 `File.WriteAllText` 将 `result.Text` 写入 `.txt` 文件。 |

---

## 后续步骤与相关主题  

- **Extract text from PDF** – 类似的 API，只需将 `ImageStream` 替换为 `PdfDocument`。  
- **Parallel batch OCR** – 对于大规模工作负载，可在独立线程上启动多个 `OcrEngine` 实例；请记得遵守许可限制。  
- **Post‑processing** – 将 OCR 输出通过拼写检查器或正则表达式处理，以清除常见的 OCR 伪影。  

所有这些扩展仍然基于 **process batch OCR** 的核心思想，并且可以逐步添加。  

---

## 结论  

我们刚刚演示了如何使用 Aspose OCR 在 C# 中通过 **process batch OCR** 高效地**从 TIFF 文件中提取文本**。示例创建了一个引擎，订阅进度事件，加载图像流列表，运行批处理，并打印每个结果。  

从这里你可以将输出集成到数据库，生成可搜索的 PDF，或将文本输入下游的 NLP 流水线。可能性无限——可以尝试语言设置、 DPI 调整和并行执行，以适应你的特定工作负载。  

有问题或想分享你如何自定义批处理？在下方留言吧，祝编码愉快！  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}