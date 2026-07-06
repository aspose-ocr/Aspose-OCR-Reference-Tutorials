---
category: general
date: 2026-02-20
description: C# OCR 教程，展示如何从图像中提取文本，识别 PNG 中的文字，并仅用几行代码将图像转换为文本。
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from png
- convert image to text
- how to extract text
language: zh
og_description: c# OCR 教程，带您逐步提取图像文件中的文本，识别 PNG 中的文本，并使用 Aspose.OCR 将图像转换为文本。
og_title: c# OCR 教程 – 快速指南：从图像中提取文本
tags:
- OCR
- C#
- Aspose
title: C# OCR 教程 – 使用 Aspose.OCR 从图像中提取文本
url: /zh/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教程 – 使用 Aspose.OCR 从图像中提取文本

曾经需要一个实际上能够在真实 PNG 文件上运行的 **c# ocr tutorial** 吗？你并不是唯一遇到这种情况的人。在许多项目中——比如发票扫描、收据归档或简单的截图解析——开发者在尝试 **extract text from image** 文件时常常碰壁，因为缺少可靠的库。  

好的消息是 Aspose.OCR 让整个过程变得轻而易举。在本指南中，我们将逐步演示一个完整且可运行的示例，展示 **how to extract text** 从 PNG 中提取文本，解释每行代码的 *why*，并涉及诸如授权和图像预处理等边缘情况。完成后，你将能够使用少量 C# 语句 **recognize text from png** 文件并 **convert image to text**。

## 本教程涵盖内容

- 在 .NET 控制台应用中设置 Aspose.OCR 引擎。  
- 从磁盘加载 PNG（或任何受支持的位图）。  
- 运行 OCR 并将结果打印到控制台。  
- 可选的授权、错误处理和性能技巧。  

没有外部服务，也没有隐藏的魔法——只有可以复制粘贴并运行的纯 C# 代码。如果你曾经想了解 **how to extract text** 从扫描文档中提取文本，继续阅读；我们会在过程中回答这个以及一些 “what if” 问题。

## 前提条件

- .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Framework 4.7+）。  
- Visual Studio 2022（或你喜欢的任何编辑器）。  
- 免费或付费的 Aspose.OCR for .NET NuGet 包。  
- 一个名为 `sample.png` 的图像文件，放置在可引用的文件夹中。  

就是这样——无需其他第三方工具。

## c# OCR 教程：设置 Aspose.OCR

首先，您需要 Aspose.OCR 库。在项目文件夹的终端中运行：

```bash
dotnet add package Aspose.OCR
```

这将获取最新的稳定版本并添加必要的 DLL 引用。如果您有许可证文件 (`Aspose.OCR.lic`)，请妥善保管；否则免费试用版也能使用，但 OCR 结果会带有水印。

### 为什么许可证很重要

没有许可证时，引擎会以评估模式运行，会在某些语言的输出中插入 “Powered by Aspose” 行。对于生产代码，您应尽早调用 `SetLicense`，如下面的代码所示。这只是一行调用，却能去除水印并解锁全速处理。

## 使用 Aspose.OCR 从图像中提取文本

现在让我们深入实际的 OCR 代码。下面是一个 **complete, self‑contained** 程序，您可以立即编译并运行。

```csharp
using System;
using System.Drawing;          // Needed for Image class
using Aspose.OCR;               // Core OCR namespace
using Aspose.OCR.Models;       // For OCR settings (optional)

class LicenseCheck
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2 (Optional): Apply your Aspose.OCR license
        // -------------------------------------------------
        // Uncomment and set the correct path if you have a license file.
        // ocrEngine.SetLicense(@"C:\MyLicenses\Aspose.OCR.lic");

        // -------------------------------------------------
        // Step 3: Load the image you want to process
        // -------------------------------------------------
        // You can use any supported format (png, jpg, bmp, tiff, etc.)
        string imagePath = @"C:\Images\sample.png";
        Image inputImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // Step 4: Recognize text from the loaded image
        // -------------------------------------------------
        // The Recognize method returns a plain string.
        string recognizedText = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 5: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**What’s happening here?**  

1. **Engine creation** – `OcrEngine` 是主要入口点；它在内部加载语言数据。  
2. **License loading** – 可选但推荐；只需指向您的 `.lic` 文件。  
3. **Image loading** – `Image.FromFile` 适用于任何位图格式；我们使用 PNG 因为它保持无损质量，这对 OCR 准确性至关重要。  
4. **Recognition** – `ocrEngine.Recognize` 完成所有繁重工作，返回包含检测到字符的字符串。  
5. **Output** – 我们将结果写入控制台，但您也可以轻松将其写入文件、数据库或 UI 控件。

### 预期输出

如果 `sample.png` 包含文本 “Hello World”，控制台将显示：

```
=== OCR Result ===
Hello World
```

如果图像模糊或包含非拉丁字符，输出可能会出现乱码。这时就需要预处理（对比度调整、二值化），将在下一节中介绍。

## 从 PNG 文件识别文本 – 提示与技巧

PNG 是一种流行的格式，因为它存储像素时没有压缩伪影。但并非所有 PNG 都一样。以下是一些实用技巧，或许对您有帮助：

- **Resolution matters** – 目标分辨率至少为 300 dpi。更低会导致字符缺失。  
- **Color vs. Grayscale** – 在 OCR 前将彩色 PNG 转为灰度可以提升速度且不影响准确性。  
- **Noise removal** – 小噪点常会干扰引擎，使用简单的中值滤波可以改善。

下面是一个快速代码片段，展示如何在将图像输入 Aspose.OCR 前进行预处理：

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
Bitmap grayBitmap = new Bitmap(inputImage.Width, inputImage.Height);
using (Graphics g = Graphics.FromImage(grayBitmap))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}});
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(inputImage, new Rectangle(0,0,grayBitmap.Width,grayBitmap.Height),
                0,0,inputImage.Width,inputImage.Height, GraphicsUnit.Pixel, attributes);
}

// Optional: Apply a simple binary threshold
Bitmap binBitmap = new Bitmap(grayBitmap.Width, grayBitmap.Height);
for (int y = 0; y < grayBitmap.Height; y++)
{
    for (int x = 0; x < grayBitmap.Width; x++)
    {
        Color pixel = grayBitmap.GetPixel(x, y);
        int bw = pixel.R < 128 ? 0 : 255; // threshold at 128
        binBitmap.SetPixel(x, y, Color.FromArgb(bw, bw, bw));
    }
}

// Now run OCR on the cleaned bitmap
string cleanedText = ocrEngine.Recognize(binBitmap);
Console.WriteLine(cleanedText);
```

**Pro tip:** 如果您要处理数十张图像，请实例化一个 `OcrEngine` 并重复使用。每张图像创建新引擎会增加不必要的开销。

## 将图像转换为文本 – 高级选项

Aspose.OCR 不仅限于纯文本提取。您可以让它返回 **structured data**（如单词边界框），或设置 **language hints** 以提升多语言文档的准确性。

```csharp
// Set language to English + Spanish (ISO codes)
ocrEngine.Language = Language.English | Language.Spanish;

// Request detailed OCR result
OcrResult result = ocrEngine.RecognizeImage(inputImage, OcrOptions.DetectTextBlocks);

// Iterate over detected words
foreach (var word in result.Words)
{
    Console.WriteLine($"{word.Text} (x:{word.Bounds.X}, y:{word.Bounds.Y})");
}
```

`OcrResult` 对象提供每个单词的坐标，这对于在 UI 中高亮显示文本或后处理（例如，遮盖敏感信息）非常有用。

## 在真实场景中提取文本

下面我们来解答在生产环境中常见的几个 “what if” 问题。

### 如果图像是 PDF 页面怎么办？

Aspose.OCR 可以直接读取 PDF，但您需要先使用 Aspose.PDF 库将每页光栅化为图像。工作流程如下：

1. 使用 `Aspose.Pdf.Document` 加载 PDF。  
2. 将页面转换为位图（`PdfConverter`）。  
3. 将位图提供给 `OcrEngine.Recognize`。

### 如果 OCR 结果包含乱码怎么办？

常见原因包括分辨率低、噪声过多或不受支持的字体。可以尝试：

- 放大图像（`Bitmap` 重设大小）。  
- 应用锐化滤波器。  
- 指定正确的语言（如上所示）。

### 如果需要并行处理图像怎么办？

由于 `OcrEngine` 不是线程安全的，请为每个线程 **separate instance per thread** 或使用线程本地池。以下是使用 `Parallel.ForEach` 的示例：

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine(); // each thread gets its own engine
    var img = Image.FromFile(path);
    string text = engine.Recognize(img);
    // Store or log 'text' as needed
});
```

## 完整可运行示例

将所有内容整合在一起，下面是一个紧凑的版本，您可以直接放入全新的控制台项目中：

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialize OCR engine (single instance for this demo)
        OcrEngine engine = new OcrEngine();

        // Uncomment if you have a license file
        // engine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Path to the PNG you want to read
        string file = @"C:\Images\sample.png";

        // Load, optionally preprocess, then recognize
        using (Image img = Image.FromFile(file))
        {
            string text = engine.Recognize(img);
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(text);
        }
    }
}
```

使用 `dotnet run` 编译并运行，观察控制台打印提取的文本。很简单，对吧？这就是一个完善的示例的魅力所在。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}