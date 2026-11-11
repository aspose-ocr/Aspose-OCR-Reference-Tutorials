---
category: general
date: 2026-05-21
description: 使用 C# 对图像执行 OCR。了解如何加载图像进行 OCR，从 PNG 中提取文本，并使用简短的代码示例识别图像中的文本。
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: zh
og_description: 在 C# 中快速对图像进行 OCR。本指南展示如何加载用于 OCR 的图像、从 PNG 中提取文本，以及以布局感知的 HTML 输出识别图像中的文本。
og_title: 使用 C# 对图像进行 OCR – 完整编程教程
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: 使用 C# 对图像进行 OCR – 完整的逐步指南
url: /zh/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 对图像执行 OCR – 完整分步指南

是否曾想过在不使用笨重 GUI 的情况下 **对图像执行 OCR**？你并不是唯一有此想法的人。无论是数字化收据、从扫描表单中提取数据，还是仅仅需要将 PNG 转换为可搜索的文本，几行 C# 代码即可完成任务。

在本教程中，我们将逐步演示 **加载图像进行 OCR**、**从图像识别文本**，以及最终将 PNG 中的文本提取为干净的 HTML。完成后，你将拥有一个可直接运行的控制台应用程序，能够 **对图像执行 OCR** 并保留原始布局。

## 您将构建的内容

- 一个最小的控制台程序，读取 PNG（或任何受支持的图像）  
- 使用 OCR 引擎 **识别图像中的文本**  
- 将结果保存为支持布局的 HTML，并嵌入原始图片  
- 展示如何 **加载图像进行 OCR**、**从 PNG 提取文本**，以及处理常见的边缘情况  

> **先决条件**  
> - .NET 6.0 SDK 或更高版本（也可以针对 .NET Framework 4.7+）  
> - 与 NuGet 兼容的 OCR 库——示例使用 *Aspose.OCR*，但任何具有相似 API 的库都可工作  
> - 基础的 C# 知识（不需要高级技巧）  

准备好了吗？太好了——让我们开始吧。

## 对图像执行 OCR – 完整代码演练

下面是 **完整、可运行** 的程序。将其复制粘贴到新建的控制台项目（`dotnet new console`）中，然后按 **F5** 运行。

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **预期输出**  
> ```
> HTML with layout saved.
> ```  
> 运行结束后，你会在 PNG 同目录下看到 `form.html`。在浏览器中打开它，你会看到与原图完全相同的布局，只是文本现在可以选择和搜索了。

### 加载图像进行 OCR

代码行 `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` 正是我们 **加载图像进行 OCR** 的位置。`ImageStream` 帮手会抽象文件格式细节，因此你可以直接喂入 JPEG、BMP 或 TIFF 而无需更改代码。  

**为什么不直接传入 `Bitmap`？**  
因为许多 OCR SDK 期望接收同时携带 DPI 元数据的流。使用库自带的加载器可以确保引擎看到的图像与屏幕上显示的完全一致，从而提升识别准确率。

#### 小技巧
如果你要处理一批文件，请将加载步骤包装在 `try/catch` 中，并记录任何 `FileNotFoundException`。这样可以防止因为单个文件缺失而导致整个批处理崩溃。

### 从 PNG 提取文本

`engine.Recognize()` 完成后，OCR 引擎会在内部保存识别出的文本。如果只需要原始文本，可以将其提取为字符串：

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

这是在不关心布局时 **从 PNG 提取文本** 的最快方式。对于大多数数据录入工作，纯文本已经足够——如果要导入 CSV，请记得去除换行符。

### 从图像识别文本

`Recognize()` 调用负责真正的重活。底层引擎会：

1. 标准化图像（去倾斜、去噪）  
2. 将图像分割为行和词  
3. 使用在数百万字符上训练的神经网络分类器进行识别  

因为我们设置了 `Language = OcrLanguage.English`，引擎会应用针对英语的词典，大幅降低误报。如果需要多语言支持，只需传入语言数组：

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### 处理布局感知的 HTML 输出

大多数开发者只停留在纯文本，但我们使用的 `HtmlSaveOptions` 让你 **对图像执行 OCR** 的同时保持视觉结构完整。两个关键标志：

- `PreserveLayout = true` – 保留列、表格和间距。  
- `EmbedImages = true` – 将原始 PNG 以 Base64 编码的 `<img>` 元素嵌入 HTML，使文件自包含。

如果想要更轻量的文件，可将 `EmbedImages = false`，此时 HTML 会引用磁盘上的原始 PNG。

#### 边缘情况：大文件

对于大于 5 MB 的图像，嵌入会导致 HTML 大幅膨胀。此时请改用外部图片引用，并考虑使用 `ImageProcessor.Compress` 预先压缩 PNG。

## 常见问题与小技巧

| 症状 | 可能原因 | 解决办法 |
|--------|--------------|-----|
| 字符乱码 | 语言设置错误或缺少语言包 | 安装相应的语言数据文件，并正确设置 `engine.Language` |
| 输出中没有文本 | 图像过暗或分辨率太低 | 使用 `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` 进行预处理 |
| HTML 布局错乱 | `PreserveLayout` 默认 `false` | 在 `HtmlSaveOptions` 中设置 `PreserveLayout = true` |
| 大量页面处理缓慢 | 引擎每个文件都重新初始化 | 重用同一个 `OcrEngine` 实例，仅在循环中更改 `engine.Image` |

### 批量处理多个文件

如果需要在文件夹中 **对图像执行 OCR**，可以将核心逻辑包装在一个简单循环中：

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

注意我们在循环内部 **加载图像进行 OCR**，但保持同一个 `engine` 和 `htmlOptions` 对象不变。这可以减少内存抖动并加快批处理速度。

## 拓展：导出为 PDF 或 DOCX

同一个 `engine` 还能保存为其他格式：

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

如果下游系统需要可搜索的 PDF，只需一行代码即可实现——无需编写额外的转换管道。

## 结论

我们已经演示了如何使用 C# **对图像执行 OCR**，从加载图片到 **从 PNG 提取文本**，再到将 **从图像识别文本** 保存为布局感知的 HTML 文件。完整示例已可直接运行，你现在也了解了每一步的意义、如何针对不同语言进行调优，以及需要留意的常见坑点。

接下来，尝试将英语语言替换为其他语言，实验 `PreserveLayout = false` 以获得更精简的 HTML，或将纯文本输出导入数据库以实现可搜索的归档。当你把强大的 OCR 引擎与几行 C# 代码结合起来时，可能性几乎是无限的。

如果你对处理多页 TIFF 有疑问，或想了解如何将其集成到 ASP.NET Core API 中，请在下方留言，祝编码愉快！

## 相关教程

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}