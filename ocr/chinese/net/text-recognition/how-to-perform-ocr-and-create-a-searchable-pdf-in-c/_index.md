---
category: general
date: 2026-02-14
description: 学习如何对 TIFF 或图像进行 OCR，并使用 OCR 将 PDF 转换为可搜索的 PDF——一步一步的 C# 指南。
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: zh
og_description: 了解如何在图像上执行 OCR、使用 OCR 转换 PDF，并使用 Aspose OCR 在简洁的 C# 教程中创建可搜索的 PDF。
og_title: 如何在 C# 中执行 OCR 并生成可搜索的 PDF
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: 如何在 C# 中进行 OCR 并创建可搜索的 PDF
url: /zh/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

translate headings and text.

Make sure code block placeholders remain unchanged.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中执行 OCR 并创建可搜索的 PDF

是否曾需要对扫描文档**执行 OCR**，但不确定如何将结果转换为可搜索的 PDF？你并不孤单——许多开发者在处理遗留的 TIFF 档案或仅包含图像的 PDF 时都会遇到这个难题。好消息是，只需几行 C# 代码并使用 Aspose.OCR 库，你就能在几秒钟内将 TIFF 或任何图像转换为完整的可搜索 PDF。

在本教程中，我们将逐步讲解所有必需的内容：从安装库、加载多页 TIFF，到调用 `RecognizeToPdf`，帮助你**使用 OCR 转换 PDF**并**生成可搜索的 PDF**文件，让用户真正可以搜索。完成后，你将拥有一个可直接运行的控制台应用程序，能够从图像源生成可搜索的 PDF。

## 前置条件

- **.NET 6.0** 或更高版本（代码同样适用于 .NET Framework 4.7+）。
- 有效的 **Aspose.OCR** 许可证或临时评估密钥（免费试用版足以进行测试）。
- Visual Studio 2022（或你喜欢的任何编辑器）并配有 **NuGet** 包管理器。
- 一个名为 `input.tif` 的输入文件，放置在你可控制的文件夹中——多页 TIFF 开箱即用。

> **专业提示：** 如果你使用 Windows，请将 TIFF 复制到编译后的 `.exe` 所在的同一文件夹，以避免路径相关的麻烦。

## 步骤 1：安装 Aspose.OCR NuGet 包

在终端中打开项目文件夹并运行：

```bash
dotnet add package Aspose.OCR
```

这将拉取最新的稳定版本（截至 2026 年 2 月为 23.10）并添加所有必需的依赖项。恢复完成后，你会在 **Solution Explorer** 的 **Dependencies** 下看到 `Aspose.OCR`。

## 步骤 2：创建最小化控制台应用程序

如果还没有控制台项目，请创建一个：

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

用 **步骤 3** 中的完整代码替换自动生成的 `Program.cs`。该程序将：

1. 实例化 OCR 引擎。
2. 加载源图像（或多页 TIFF）。
3. 执行 OCR 并直接将输出写入可搜索的 PDF。
4. 通知用户处理已成功完成。

## 步骤 3：完整可运行代码 – 从图像到可搜索 PDF

下面是**完整**的源文件。复制粘贴到 `Program.cs` 中。代码中已加入注释，解释不太直观的部分。

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**运行效果：** 程序执行后，会在目标文件夹生成名为 `searchable.pdf` 的文件。使用 Adobe Reader 或任意 PDF 查看器打开，尝试搜索原始 TIFF 中存在的单词。文本应立即被定位，证明你已经成功**从图像生成可搜索 PDF**。

### 运行应用

```bash
dotnet run
```

如果一切配置正确，你将看到：

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

打开 PDF，按 `Ctrl+F`，输入源文件中的任意单词，观察高亮立即跳转到正确位置。

## 步骤 4：常见变体与边缘情况

### 将普通 PDF（仅图像）转换为可搜索 PDF

如果源文件是包含扫描图像而非文本的 PDF，仍然可以使用相同的方法——只需更改 `ImageStream` 的来源：

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

这样即可满足**使用 OCR 转换 pdf**的场景，无需额外代码。

### 处理大型多页文档

对于页数超过几百页的文档，建议：

- **提升内存限制**（`Engine.MemoryLimit = 2_000; // MB`）。
- **分块处理**：加载部分页面，写入中间 PDF，然后使用 PDF 库（如 Aspose.PDF）合并。

### 处理非英文语言

Aspose.OCR 开箱即支持多种语言。识别前设置语言：

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

如果需要在非拉丁脚本下实现**tiff 转可搜索 pdf**，请确保已安装相应的语言包。

### 输出的 PDF 为空白怎么办？

- 确认输入文件未损坏。
- 确保 OCR 引擎拥有有效许可证——评估模式可能会限制页数。
- 检查图像分辨率是否至少为 300 dpi；分辨率过低会导致识别效果差。

## 步骤 5：以编程方式验证结果（可选）

有时你需要确认 PDF 确实包含文本层。可以使用 Aspose.PDF 提取文本：

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

如果 `extracted` 非空，则说明你已经成功**生成可搜索 pdf**。

## 结论

我们已经介绍了如何对 TIFF（或任意图像）**执行 OCR**，并无缝**使用 OCR 转换 PDF**，从而创建行为如同原生文档的**可搜索 PDF**。关键步骤如下：

1. 安装 Aspose.OCR。  
2. 初始化 `Engine`。  
3. 通过 `ImageStream` 加载图像。  
4. 调用 `RecognizeToPdf`。  

之后，你可以尝试语言设置、大批量处理，或将输出与其他 PDF 操作结合使用。同样的模式适用于 **tiff 转可搜索 pdf**、**从图像生成可搜索 pdf**，甚至扫描的 PDF。

准备好迎接下一个挑战了吗？尝试将 OCR 嵌入 Web API，让用户上传扫描件后即时返回可搜索 PDF，或探索使用 `OcrEngine` 的高级设置对手写笔记进行 OCR。可能性无限——祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}