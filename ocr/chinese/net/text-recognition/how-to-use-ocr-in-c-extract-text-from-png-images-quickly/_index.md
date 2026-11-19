---
category: general
date: 2026-03-29
description: 如何使用 Aspose 的 OCR 从 PNG 文件中提取文本并将图像转换为文字。学习 C# 中的逐步异步 OCR。
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: zh
og_description: 如何在 C# 中使用 Aspose 的 OCR 从 PNG 文件中提取文本。本指南将带您了解异步 OCR、代码和技巧。
og_title: 如何在 C# 中使用 OCR – 从 PNG 图像提取文本
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 OCR – 快速从 PNG 图像提取文本
url: /zh/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 快速从 PNG 图像提取文本

是否曾好奇 **如何使用 OCR** 从少量 PNG 截图中提取文本？也许你有扫描的收据、发票或 UI 原型图，需要将这些文本转换为可搜索的格式。好消息是？使用 Aspose.OCR，你只需几行异步 C# 代码即可将图像转换为文本。  

在本教程中，我们将准确演示如何从 PNG 文件中提取文本，解释每一步的重要性，并提供一个可直接运行的程序，打印每页的识别文本。完成后，你将能够 **从图像中提取文本**，无需翻阅文档。

## 你将学到

- 安装并引用 Aspose.OCR NuGet 包。  
- 初始化 OCR 引擎并设置语言（本例中为英文）。  
- 将 PNG 文件数组传递给 `RecognizeImagesAsync` 以实现快速、非阻塞的处理。  
- 遍历 `OcrResult` 对象并输出提取的字符串。  

无需外部服务，也不需要复杂的回调——仅使用简洁的异步 C#，适用于 .NET 6+。

---

## 前提条件

| 需求 | 原因 |
|-------------|--------|
| .NET 6 SDK（或更高） | 现代语言特性，如 `async Main`。 |
| Visual Studio 2022 或 VS Code | 用于编译和运行代码的 IDE。 |
| Aspose.OCR NuGet 包（`Aspose.OCR`） | 提供示例中使用的 `OcrEngine` 类。 |
| 若干 PNG 图像（`page1.png`, `page2.png`, …） | OCR 处理的输入文件。 |

如果你已经有 .NET 项目，只需运行 `dotnet add package Aspose.OCR`。否则使用 `dotnet new console -n OcrDemo` 创建一个全新的控制台应用程序。

---

## 步骤 1：安装 Aspose.OCR 并设置项目

首先，将 OCR 库添加到你的项目中：

```bash
dotnet add package Aspose.OCR
```

重要性说明：Aspose.OCR 包含本机 OCR 引擎、语言包以及简洁的 API。通过 NuGet 引入可确保版本兼容并自动获取更新。

---

## 步骤 2：初始化 OCR 引擎并选择语言

引擎需要知道要识别的语言。英文是最常用的，但你可以替换为 `Language.Spanish`、`Language.French` 等。

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **小贴士：** 始终显式设置语言；使用默认值可能会降低准确率并增加处理时间。

---

## 步骤 3：准备 PNG 文件列表

你可以提供单个文件或数组。使用数组可让引擎异步批量处理，这对于少量页面非常理想。

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

如果图像位于子文件夹，只需在前面加上相对路径（`"images/page1.png"`）。如果路径错误，引擎会抛出明确的 `FileNotFoundException`——请务必核对文件名。

---

## 步骤 4：对所有图像运行异步 OCR

`RecognizeImagesAsync` 方法返回一个 `OcrResult` 数组。由于它是异步的，OCR 在后台运行时，UI（或控制台）保持响应。

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**为什么使用 async？**  
如果你将 OCR 集成到 Web API 或桌面应用中，不希望线程在引擎扫描每个像素时被阻塞。`await` 会将线程释放回线程池，从而提升可扩展性。

---

## 步骤 5：显示每页提取的文本

现在我们已经得到结果，遍历它们并打印识别的文本。`Text` 属性包含纯文本输出，可用于后续处理（例如保存到数据库）。

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### 预期输出

假设 `page1.png` 包含 “Invoice #12345”，`page2.png` 包含 “Total: $89.99”，你会看到类似如下的输出：

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

如果 OCR 未能定位任何文本，`Text` 属性将为空字符串——在生产代码中请通过检查 `string.IsNullOrWhiteSpace` 来处理此情况。

---

## 完整工作示例

下面是完整的程序代码，可直接复制粘贴到 `Program.cs`。它包含所有 using 指令、异步 `Main`，以及阐明每一步的注释。

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

保存文件，将 PNG 放在可执行文件旁边（或调整路径），然后运行：

```bash
dotnet run
```

你应该会在控制台看到提取的文本，确认已成功 **将图像转换为文本**。

---

## 处理常见边缘情况

| 情况 | 处理方法 |
|-----------|------------|
| **低分辨率 PNG** | 在识别前提升 `ocrEngine.ImageProcessingOptions.Dpi`。 |
| **多语言** | 设置 `ocrEngine.Language = Language.English | Language.Spanish;`（按位或）。 |
| **大批量（数百个文件）** | 分块处理（例如每次 `RecognizeImagesAsync` 传入 20 个文件），以避免内存激增。 |
| **需要置信度分数** | 使用 `ocrResults[i].Confidence`（0 到 1 之间的浮点数）过滤低质量结果。 |

这些调整可保持 OCR 流程的稳健，尤其是在从演示阶段转向生产环境时。

---

## 额外功能：将结果保存为文本文件

如果你更倾向于持久化保存而非控制台输出，可添加一个小助手：

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

现在你拥有一个单独的文件，可 **从图像中提取文本** 用于后续处理——非常适合索引、搜索或输入到语言模型中。

---

## 结论

我们已经演示了如何在 C# 中使用 Aspose **使用 OCR**，高效 **从 PNG 文件提取文本** 并 **将图像转换为文本**。异步方式确保应用保持响应，而简洁的 API 使代码易读且易维护。  

使用自己的文档试一试，尝试不同语言，甚至可以将输出链入搜索索引或摘要服务。当你能够可靠地将图片转化为可搜索的字符串时，可能性无限。

### 后续步骤与相关主题

- **从其他格式（JPEG、TIFF）提取文本**——只需更改文件扩展名。  
- **使用 Parallel.ForEach 批量处理**，适用于海量工作负载。  
- **OCR 后清理**，使用正则表达式规范化日期、金额或 ID。  
- **集成 Azure Cognitive Services**，如果需要基于云的 OCR 及额外功能。  

如果遇到任何问题，欢迎留言，或分享你对该基本流程的扩展。祝编码愉快！   (Image: ![OCR result screenshot showing extracted text](/images/ocr-result.png){.align-center alt="如何使用 OCR 示例输出"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}