---
category: general
date: 2026-01-10
description: 如何快速运行 OCR 并从图像中提取阿拉伯语文本。学习将图像转换为文本，读取 PNG 中的文本，并了解如何使用 Aspose OCR 提取文本。
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: zh
og_description: 如何在 C# 中运行 OCR 并从 PNG 图像中提取阿拉伯文文本。本指南将一步步演示如何将图像转换为文本并读取 PNG 中的文字。
og_title: 如何在 C# 中运行 OCR – 从 PNG 提取阿拉伯文文本
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中运行 OCR – 从 PNG 中提取阿拉伯文文本
url: /zh/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中运行 OCR – 从 PNG 中提取阿拉伯语文本

有没有想过 **如何运行 OCR** 来处理包含阿拉伯字符的图片？你并不孤单。许多开发者在需要 **从 PNG 中提取阿拉伯语文本** 时会卡住，因为不知道哪个库能够轻松处理从右到左的脚本。  

在本教程中，我们将逐步讲解使用 Aspose.OCR 在简洁的 C# 控制台应用中 **将图像转换为文本**、**从 PNG 读取文本**，以及最终 **如何提取文本** 所需的全部内容。完成后，你将拥有一个可直接运行的程序，能够在终端中打印出阿拉伯语字符串。

## 你将学到

- 安装并引用 Aspose.OCR NuGet 包。  
- 为阿拉伯语支持配置 OCR 引擎。  
- 加载 PNG 图像并运行识别过程。  
- 获取并显示提取的文本。  
- 调整设置以获得更高的准确性并处理常见问题。

不需要任何 OCR 经验，只需对 C# 有基本了解，并具备 .NET 开发环境（Visual Studio、Rider 或 `dotnet` CLI 均可）。

---

## 如何运行 OCR – 设置 Aspose OCR

### 步骤 1：添加 Aspose.OCR NuGet 包

我们首先需要的是 OCR 库本身。Aspose.OCR 是商业产品，但它提供了免费试用版，完全适合学习使用。

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

或者，在 Visual Studio 中打开 **NuGet 包管理器**，搜索 **Aspose.OCR**，然后点击 **Install**。

> **技巧提示：** 如果计划在 CI 流水线中使用该库，请添加 `-v` 标志以锁定版本，例如 `dotnet add package Aspose.OCR -v 23.10`。

### 步骤 2：创建一个新的控制台项目（如果还没有的话）

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

现在你已经拥有一个全新的 `Program.cs` 文件，可用于编写我们的代码。

---

## 提取阿拉伯语文本 – 编写 OCR 代码

下面是完整的、可直接运行的程序。将其保存为 `Program.cs`（或替换自动生成的文件）。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### 每行代码的重要性

- **`OcrEngine`**：协调图像加载、语言选择和识别的核心类。  
- **`Language = OcrLanguage.Arabic`**：阿拉伯语使用从右到左的脚本和独特的字形；设置语言可让引擎使用正确的字符模型。  
- **`ImageStream.FromFile`**：支持 PNG、JPEG、BMP 等多种格式。如果需要从 `MemoryStream`（例如上传的文件）读取，请相应替换此调用。  
- **`Recognize()`**：执行繁重的工作——像素分析、分割和字符分类。  
- **`ocrEngine.Text`**：最终的 Unicode 字符串，可用于后续处理、存储或显示。

### 预期输出

如果 `arabic_sample.png` 包含短语 “مرحبا بالعالم”（Hello World），控制台将打印：

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

如果输出出现乱码，请再次确认图像清晰、语言已设置为 Arabic，并且 OCR 引擎版本与文档匹配。

---

## 将图像转换为文本 – 调整准确性

虽然默认设置适用于大多数干净的扫描件，但实际图像常常需要额外的调优。

| 设置 | 作用 | 使用场景 |
|------|------|----------|
| `ocrEngine.Config.Preprocess = true` | 启用自动二值化和噪声去除。 | 有阴影的扫描文档。 |
| `ocrEngine.Config.Deskew = true` | 旋转图像以纠正轻微倾斜。 | 倾斜拍摄的照片。 |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | 将整幅图像视为一个文本块。 | 简单的标题或单行标签。 |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | 仅限识别阿拉伯字符。 | 在混合语言页面上减少误报。 |

可以在创建引擎后立即添加这些行：

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## 从 PNG 读取文本 – 处理不同的图像来源

有时 PNG 存在于数据库中或来自网络请求。下面是一个读取 `byte[]` 的快速示例：

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

其余流程保持一致，这意味着 **如何提取文本** 在任何来源下都保持一致。

---

## 如何提取文本 – 高级选项与边缘情况

### 1. 多页 PDF 或 TIFF

如果需要对多页文档进行 OCR，可遍历每一页：

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **注意：** 该代码片段需要 `Aspose.PDF` 包。

### 2. 自动检测语言

Aspose.OCR 也提供自动检测功能，但速度较慢。如果不确定图像是阿拉伯语还是其他脚本，请启用此功能：

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

### 3. 性能技巧

- **复用 `OcrEngine`** 对象以处理多张图像；每次创建新实例会增加开销。  
- **并行运行** 仅在每个线程拥有独立的引擎实例时可行——共享同一实例会导致竞争条件。

---

## 结论

我们已经从头到尾介绍了在 C# 中 **如何运行 OCR**，演示了如何 **提取阿拉伯语文本**、**将图像转换为文本**、**从 PNG 读取文本**，以及在各种场景下解答 **如何提取文本**。示例代码完整、独立，可直接粘贴到任何 .NET 控制台项目中使用。

下一步？尝试将 `OcrLanguage.Arabic` 替换为韩语或塞尔维亚西里尔文，以体验库的多语言能力。尝试使用预处理标志提升噪声扫描的准确性，或将 OCR 过程集成到 Web API 中，让用户上传图像并即时获取文本结果。

祝编码愉快，愿你的 OCR 结果始终清晰如晶！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}