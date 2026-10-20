---
category: general
date: 2026-03-20
description: 快速创建可搜索的 PDF：将图像转换为 PDF，提取图像中的文字，并添加隐藏的文字层，实现完整的可搜索性。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- pdf with hidden text
- scan image to pdf
language: zh
og_description: 在 C# 中通过将图像转换为 PDF、提取文本并嵌入隐藏层，创建可搜索的 PDF，实现即时搜索。
og_title: 将图像转换为可搜索的 PDF – 完整 C# 教程
tags:
- Aspose
- C#
- OCR
- PDF generation
title: 在 C# 中从图像创建可搜索的 PDF – 步骤指南
url: /zh/net/text-recognition/create-searchable-pdf-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 将图像创建可搜索 PDF – 完整指南

是否曾需要从扫描的发票**创建可搜索 PDF**，但不想手动输入所有内容？你并不是唯一的。 在许多办公流程中，将位图扫描转换为可以实际搜索的 PDF 是一个每日的痛点。 好消息是？只需几行 C# 代码和 Aspose 的 OCR 与 PDF 库，就可以自动完成整个过程——无需手动复制粘贴。

在本教程中，我们将逐步演示如何**将图像转换为 PDF**，提取图像中的文本，然后将文本以不可见的方式叠加，使最终文件表现得像原生 PDF。完成后，你将拥有一种即用型方法来构建**带隐藏文本的 PDF**，适用于任何扫描文档，无论是发票、合同还是收据。

## 你需要的条件

- .NET 6.0 或更高（代码使用 `using var` 语句，较新的 SDK 更方便）
- Aspose.OCR 和 Aspose.Pdf NuGet 包（`Install-Package Aspose.OCR` 和 `Install-Package Aspose.Pdf`）
- 包含要索引文本的示例图像文件（PNG、JPG 或 TIFF）
- Visual Studio 2022 或任意你喜欢的 IDE

> **技巧提示：** 如果你正在处理多页扫描，只需遍历每个图像并重复这些步骤——相同的逻辑适用。

---

## 步骤 1 – 初始化 OCR 引擎（从图像提取文本）

在嵌入可搜索文本之前，我们需要实际读取图片中的字符。Aspose 的 `OcrEngine` 完成繁重的工作。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine and tell it which language to look for.
// English works for most invoices, but you can set Language.French, etc.
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**为什么这很重要：** 使用正确的语言初始化引擎可以显著提升准确率。如果跳过此步骤，OCR 可能会误识别数字——这在财务文件中是绝对要避免的。

## 步骤 2 – 加载扫描图像（将图像转换为 PDF）

现在我们将位图加载到内存中。Aspose 直接使用 `System.Drawing.Image`，因此任何 .NET 支持的格式都可以。

```csharp
using System.Drawing;

// Replace the path with the location of your scanned file.
var inputImage = Image.FromFile(@"C:\Docs\invoice.png");
```

如果你已有一个**扫描图像转 PDF**的工作流，已经生成多页 TIFF，只需更改文件扩展名并对每页重复加载步骤。

## 步骤 3 – 运行 OCR 并捕获识别的文本

图像准备好后，我们让 OCR 引擎发挥其魔力。

```csharp
// Perform OCR – the result contains the raw text and confidence scores.
var ocrResult = ocrEngine.Recognize(inputImage);

// For debugging, you might want to see what was read.
Console.WriteLine("OCR Output:");
Console.WriteLine(ocrResult.Text);
```

**特殊情况：** 如果图像分辨率低（< 300 dpi），置信度会下降。考虑在送入引擎前进行放大或重新以更高 DPI 扫描。

## 步骤 4 – 创建 PDF 并将原始图像设为背景

即使是**带隐藏文本的 PDF**，仍然需要扫描的视觉呈现。我们将把图像作为页面背景添加。

```csharp
using Aspose.Pdf;

// Start a fresh PDF document.
var pdfDocument = new Document();

// Add a new page.
var pdfPage = pdfDocument.Pages.Add();

// Insert the image; it will fill the page by default.
pdfPage.Paragraphs.Add(new Aspose.Pdf.Image
{
    ImageInfo = new ImageInfo(@"C:\Docs\invoice.png")
});
```

**为什么使用图像作为背景：** 用户仍然可以看到原始扫描的完整细节，保留签名和印章，同时隐藏文本层提供搜索功能。

## 步骤 5 – 将 OCR 文本覆盖为不可见层（PDF 带隐藏文本）

关键步骤如下：我们添加一个 `TextFragment`，它位于图像之上但被设为不可见。Aspose.Pdf 使这一步变得简单。

```csharp
using Aspose.Pdf.Text;

// Create a text fragment from the OCR result.
var searchableText = new TextFragment(ocrResult.Text)
{
    // Position (0,0) aligns with the bottom‑left of the page.
    Position = new Position(0, 0),

    // Make the text invisible – it still participates in search.
    TextState = { Font = FontRepository.FindFont("Arial"), FontSize = 0.1f, IsHidden = true }
};

// Add the invisible text to the same page.
pdfPage.Paragraphs.Add(searchableText);
```

**解释：** 将字体大小设为极小并将片段标记为隐藏，可保持视觉输出整洁，同时确保 PDF 的文本层包含 OCR 输出。搜索引擎和 PDF 阅读器会对其进行索引。

## 步骤 6 – 保存可搜索 PDF

最后，将文档写入磁盘。

```csharp
// Choose a destination path.
string outputPath = @"C:\Docs\invoice_searchable.pdf";

// Save the PDF. The file now contains both the image and searchable text.
pdfDocument.Save(outputPath);

Console.WriteLine($"Searchable PDF created at: {outputPath}");
```

在 Adobe Reader 中打开生成的文件，按 **Ctrl + F**，输入发票中出现的词语，你会看到匹配被高亮显示——即使该文本从未可见。

## 完整工作示例（所有步骤汇总）

下面是完整的程序代码，你可以复制粘贴到控制台应用中。只要已安装 NuGet 包且文件路径正确，它即可直接编译运行。

```csharp
// ------------------------------------------------------------
// Create Searchable PDF from Image – Complete C# Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load scanned image
        var inputImagePath = @"C:\Docs\invoice.png";
        var inputImage = Image.FromFile(inputImagePath);

        // 3️⃣ Perform OCR
        var ocrResult = ocrEngine.Recognize(inputImage);
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // 4️⃣ Create PDF and add image as background
        var pdfDocument = new Document();
        var pdfPage = pdfDocument.Pages.Add();
        pdfPage.Paragraphs.Add(new Aspose.Pdf.Image
        {
            ImageInfo = new ImageInfo(inputImagePath)
        });

        // 5️⃣ Add invisible searchable text layer
        var searchableText = new TextFragment(ocrResult.Text)
        {
            Position = new Position(0, 0),
            TextState = { Font = FontRepository.FindFont("Arial"), FontSize = 0.1f, IsHidden = true }
        };
        pdfPage.Paragraphs.Add(searchableText);

        // 6️⃣ Save the searchable PDF
        var outputPath = @"C:\Docs\invoice_searchable.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"✅ Searchable PDF saved to: {outputPath}");
    }
}
```

**预期结果：**  
- `invoice_searchable.pdf` 与 `invoice.png` 完全相同。  
- 文本搜索可针对原始扫描中出现的任何词语。  
- 文件大小仅略有增长（隐藏文本只增加几千字节）。

## 常见问题与特殊情况

### 我可以在一个 PDF 中处理多页吗？

当然可以。将 OCR 与 PDF 的逻辑包装在 `foreach (string imagePath in imageFiles)` 循环中，为每次迭代创建一个新的 `Page`。隐藏文本层会在每页添加，搜索功能覆盖整个文档。

### 如果文档包含多种语言怎么办？

将 `ocrEngine.Language` 设置为 `Language.Multilingual`，或为每个语言段实例化单独的引擎。Aspose 将返回混合语言的结果，你可以将其放入同一 PDF 页面。

### 如何控制 DPI 或图像缩放？

在将图像添加到 PDF 之前，你可以使用 `System.Drawing` 进行尺寸调整：

```csharp
var resized = new Bitmap(inputImage, new Size(1240, 1754)); // A4 at 150 dpi
```

然后将 `resized` 传递给 PDF 图像构造函数。

### 隐藏文本在所有查看器中真的不可见吗？

大多数现代查看器会遵守 `IsHidden` 标志。如果遇到仍显示微小文字的查看器，可进一步降低字体大小（例如 `0.01f`），或使用 `TextState.FillColor = Color.Transparent` 将文字颜色设为完全透明。

### 安全性如何——我可以给 PDF 设置密码吗？

可以。完成内容添加后，调用：

```csharp
pdfDocument.Encrypt("ownerPwd", "userPwd", EncryptionAlgorithms.AES256);
```

现在，可搜索的 PDF 也遵循了组织的保密政策。

## 生产级实现技巧

- **批量处理：** 对大量图像使用 `Parallel.ForEach`，但要注意 `OcrEngine` 实例不是线程安全的——每个线程创建一个实例。  
- **错误处理：** 将 OCR 调用包装在 try/catch 中；检查 `ocrResult.IsRecognized` 以跳过识别失败的页面。  
- **日志记录：** 保存 `ocrResult.Confidence` 值；低置信度可能表明需要进行图像预处理（去倾斜、去噪点）。  
- **性能优化：** 为所有页面复用同一个 `Document` 对象，避免反复打开/关闭文件。  
- **测试：** 将可搜索 PDF 的提取文本 (`pdfDocument.Pages[1].ExtractText()`) 与 OCR 输出进行比较，确保没有截断。

## 结论

我们刚刚演示了如何使用 C# **创建可搜索 PDF** 文件，从普通图像中提取文本。通过 Aspose.OCR 提取文本，将其以不可见方式叠加到 PDF 页面并保存结果，你将得到一份外观与原始扫描完全相同，却具备原生 PDF 功能的文档。此技术涵盖了经典的 **将图像转换为 PDF** 工作流，添加了 **带隐藏文本的 PDF**，并解决了日常需要 **将图像扫描为 PDF** 并能够搜索的问题。

准备好下一步了吗？尝试扩展代码以批量处理收据文件夹，或将其集成到实时返回可搜索 PDF 的 Web API 中。你还可以尝试不同的字体、添加元数据，甚至将 OCR 置信度分数嵌入为 PDF 注释，以便审计追踪。

如果你觉得本指南有帮助，请点星标、与团队分享，或留下评论分享你的改进。祝编码愉快，愿你的 PDF 永远可搜索！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}