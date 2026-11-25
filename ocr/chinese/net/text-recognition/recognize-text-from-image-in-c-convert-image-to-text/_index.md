---
category: general
date: 2026-06-19
description: 使用 Aspose OCR 在 C# 中识别图像文字：一步一步的指南，将图像转换为文本并从 JPG 文件中提取文字。
draft: false
keywords:
- recognize text from image
- extract text from jpg
- convert image to text
- perform ocr on image
- set ocr language
language: zh
og_description: 使用 Aspose OCR 在 C# 中识别图像文字。了解如何设置 OCR 语言、从 JPG 提取文本，并在几分钟内将图像转换为文字。
og_title: 在 C# 中识别图像文字 – 将图像转换为文本
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: 'recognize text from image using Aspose OCR in C#: step‑by‑step guide
    to convert image to text and extract text from jpg files.'
  headline: recognize text from image in C# – Convert Image to Text
  type: TechArticle
- description: 'recognize text from image using Aspose OCR in C#: step‑by‑step guide
    to convert image to text and extract text from jpg files.'
  name: recognize text from image in C# – Convert Image to Text
  steps:
  - name: 5.1 Low‑Resolution Images
    text: OCR accuracy drops sharply below 100 dpi. If you notice garbled output,
      try pre‑processing the image (increase contrast, resize, or apply a sharpening
      filter) before feeding it to Aspose OCR.
  - name: 5.2 Multi‑Page Documents
    text: "Even though Community mode caps at 100 pages, you can still process PDFs
      or multi‑page TIFFs. The engine will return concatenated text, preserving page
      breaks with `\f`."
  - name: 5.3 Non‑English Languages
    text: 'Switch the `Language` enum to another supported value:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: 在 C# 中识别图像文字 – 将图像转换为文本
url: /zh/net/text-recognition/recognize-text-from-image-in-c-convert-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中从图像识别文本 – 将图像转换为文本

是否曾经需要**从图像识别文本**，但不确定哪个库可以在不支付高额许可证费用的情况下实现？你并不孤单。在本教程中，我们将演示如何使用 Aspose OCR 的免费 Community 模式来**将图像转换为文本**，从 jpg 文件中提取文本，甚至**设置 OCR 语言**以应对多语言场景。

我们将涵盖从安装 NuGet 包到处理多页 PDF 或低分辨率图片等边缘情况的全部内容。完成后，你将拥有一个可运行的控制台应用程序，能够**对图像文件执行 OCR**，速度快如闪电。

## 你需要的条件

- .NET 6 SDK 或更高版本（代码同样适用于 .NET Core 3.1+）
- Visual Studio 2022 或任何你喜欢的编辑器
- 包含可读文本的图像文件（JPG、PNG、BMP…）
- 能够访问互联网以获取 `Aspose.OCR` NuGet 包

就这么简单——无需额外的 DLL，无需外部服务，纯 C#。

![从图像识别文本示例](https://example.com/ocr-screenshot.png "从图像识别文本示例")

*（该截图显示了识别示例 JPG 后的控制台输出。）*

## 步骤 1：通过 NuGet 安装 Aspose OCR

首先，将 Aspose OCR 库添加到你的项目中。打开项目文件夹中的终端并运行：

```bash
dotnet add package Aspose.OCR
```

该包附带**Community 模式**，每次运行限制处理 100 页，非常适合小规模实验。如果需要更高的限制，你可以稍后升级为付费许可证——无需更改代码。

## 步骤 2：配置 OCR 引擎（设置 OCR 语言）

在**对图像执行 OCR**之前，你必须告诉引擎期望的语言。默认是英语，但你可以通过一行代码切换到西班牙语、法语，甚至中文。

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;

// Choose the language you need – here we stick with English.
var ocrConfig = new OcrEngineConfig
{
    Language = Language.English,      // set ocr language
    MaxPagesPerRun = 100              // enforced limit in Community mode
};
```

语言为何重要？OCR 模型是基于字符集训练的；如果将法语文档喂给英语模型，会漏掉重音和连字。设置正确的语言可以显著提升准确率。

## 步骤 3：创建 OCR 引擎并识别图像

配置完成后，在 `using` 块中实例化引擎，以便自动释放资源。随后使用图像路径（JPG 或任何受支持的格式）调用 `RecognizeImage`。

```csharp
// Step 3: Create the OCR engine and recognize the image
using var ocrEngine = new OcrEngine(ocrConfig);

// Replace with the actual path to your image file.
string imagePath = @"YOUR_DIRECTORY/sample.jpg";

// Perform OCR – this will **recognize text from image**.
var ocrResult = ocrEngine.RecognizeImage(imagePath);
```

需要注意的几点：

- **线程安全性：**`OcrEngine` 实例不是线程安全的。如果计划并发处理大量图像，请为每个线程创建单独的引擎。
- **支持的格式：**除了 JPG，你还可以使用 PNG、BMP、TIFF，甚至 PDF。相同的方法适用，因此你可以**从 jpg 提取文本**或任何其他光栅图像。

## 步骤 4：输出识别的文本（将图像转换为文本）

现在 OCR 引擎已经完成工作，结果存储在 `OcrResult` 对象中。其 `Text` 属性包含引擎能够读取的所有内容的纯文本表示。

```csharp
// Step 4: Write the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

如果使用清晰的收据截图运行程序，你会看到类似如下的输出：

```
=== OCR Output ===
Item        Qty   Price
Apple       2     $1.20
Banana      5     $0.75
Total               $5.55
```

这就是**将图像转换为文本**的核心——图像现在变成了一个字符串，你可以存储、搜索或传递给其他系统。

## 步骤 5：处理常见的边缘情况

### 5.1 低分辨率图像

OCR 准确率在低于 100 dpi 时会急剧下降。如果发现输出乱码，请在将图像输入 Aspose OCR 之前进行预处理（提升对比度、调整大小或使用锐化滤镜）。

```csharp
// Example: Resize a low‑dpi image to improve accuracy
using var bitmap = new Bitmap(imagePath);
var highRes = new Bitmap(bitmap, new Size(bitmap.Width * 2, bitmap.Height * 2));
highRes.Save("highres_sample.jpg");
var highResResult = ocrEngine.RecognizeImage("highres_sample.jpg");
```

### 5.2 多页文档

即使 Community 模式限制为 100 页，你仍然可以处理 PDF 或多页 TIFF。引擎会返回合并的文本，并使用 `\f` 保留分页符。

```csharp
var multiPageResult = ocrEngine.RecognizeImage("multi_page.pdf");
Console.WriteLine(multiPageResult.Text); // contains form‑feed characters between pages
```

### 5.3 非英语语言

将 `Language` 枚举切换为其他受支持的值：

```csharp
ocrConfig.Language = Language.French; // now the engine expects French characters
```

如果超出默认语言集，请记得安装相应的语言包；Aspose 将其作为独立的 NuGet 包提供。

## 步骤 6：完整工作示例

将所有内容整合在一起，下面是一个完整的、可直接复制粘贴的控制台应用程序，能够**从图像识别文本**、**从 jpg 提取文本**，并根据需要**设置 OCR 语言**。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Configuration;

class OcrDemo
{
    static void Main()
    {
        // 1️⃣ Configure OCR – change Language to match your source.
        var ocrConfig = new OcrEngineConfig
        {
            Language = Language.English,   // set ocr language
            MaxPagesPerRun = 100
        };

        // 2️⃣ Create the engine inside a using block.
        using var ocrEngine = new OcrEngine(ocrConfig);

        // 3️⃣ Path to the image you want to process.
        string imagePath = @"YOUR_DIRECTORY/sample.jpg";

        // 4️⃣ Perform OCR – this **recognize text from image**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 5️⃣ Output – now you have **convert image to text** results.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**预期输出**（假设示例图像包含文本 “Hello World!”）：

```
=== OCR Output ===
Hello World!
```

使用 `dotnet run` 运行程序，你将在控制台看到提取的字符串。

## 专业技巧与常见陷阱

- **专业提示：**将 OCR 调用包装在 `try/catch` 块中，以优雅地处理损坏的文件。  
- **注意：**带有水印或大量背景噪声的图像；它们常常会干扰引擎。  
- **提示：**如果需要批量处理文件，可遍历目录条目并复用同一个 `OcrEngine` 实例——只需记得重置每张图像的设置。  
- **记住：**Community 模式的 100 页限制是针对每次运行，而非每个文件。如果达到上限，请拆分大型 PDF。

## 结论

现在你拥有了一个稳固、可投入生产的代码片段，使用 Aspose OCR 在 C# 中**从图像识别文本**。从安装 NuGet 包到**设置 OCR 语言**、处理低分辨率图片，直至**将图像转换为文本**，每一步都已涵盖。欢迎自行实验——更换语言、使用 PNG，或将输出链入下游搜索索引。

接下来，你可以通过将此代码集成到 Azure Function 中，规模化**从 jpg 提取文本**，或深入了解 Aspose OCR 的高级功能，如版面分析和手写识别。可能性无限，而你今天搭建的基础将使这些扩展变得轻而易举。

祝编码愉快，愿你的图像永远清晰可读！

## 接下来你应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于其中演示的技术。每个资源都提供完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 Aspose.OCR 进行语言选择的 C# 图像文本提取](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [使用 Aspose OCR 进行多语言文本识别](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [从图像提取文本 – 使用 Aspose.OCR 进行 .NET OCR 优化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}