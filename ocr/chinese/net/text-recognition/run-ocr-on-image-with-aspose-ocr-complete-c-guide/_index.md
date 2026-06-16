---
category: general
date: 2026-02-17
description: 使用 Aspose OCR 在 C# 中对图像进行 OCR。学习如何从 JPG 提取文本、对图像进行 OCR 前的预处理，以及使用一步一步的代码加载图像进行
  OCR。
draft: false
keywords:
- run OCR on image
- extract text from jpg
- preprocess image for OCR
- load image for OCR
language: zh
og_description: 在 C# 中使用 Aspose OCR 对图像进行 OCR。本文指南展示了如何从 JPG 中提取文本、预处理图片以及加载图像进行 OCR。
og_title: 使用 Aspose OCR 对图像进行文字识别 – 完整 C# 指南
tags:
- Aspose OCR
- C#
- Image Processing
title: 使用 Aspose OCR 对图像进行 OCR – 完整 C# 指南
url: /zh/net/text-recognition/run-ocr-on-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在图像上运行 OCR – 完整 C# 指南

是否曾需要 **在图像上运行 OCR**，但不知从何入手？在许多实际应用中——比如发票扫描器或收据跟踪器——首要难题就是从 JPEG 中获取可靠的文本。好消息是，使用 Aspose OCR，你只需几行 C# 代码即可 **在图像上运行 OCR**，并且还能学习如何 **从 jpg 中提取文本**、**为 OCR 预处理图像**、以及 **为 OCR 加载图像**，无需在零散的文档中四处寻找。

在本教程中，我们将逐步演示一个完整的、可直接复制粘贴的示例，展示如何设置引擎、添加实用的预处理过滤器、将图片输入识别器，并将结果打印到控制台。完成后，你将拥有一个可直接嵌入任何 .NET 项目、立即从图像中提取文本的独立程序。

## 你需要准备的环境

- .NET 6.0 或更高版本（代码同样适用于 .NET Core）  
- Aspose.OCR NuGet 包（`Install-Package Aspose.OCR`）  
- 一个示例 JPEG（`input.jpg`），放置在可引用的文件夹中  
- 对 C# 语法的基本了解（无需高级技巧）

如果这些都已就绪，太好了——让我们开始吧。如果还没有，先获取 NuGet 包和测试图片；后续指南默认你已经完成这些步骤。

## 第一步：创建 OCR 引擎 – 运行 OCR 在图像上的核心

要 **在图像上运行 OCR**，首先需要实例化 `OcrEngine`。该对象包含识别所需的所有配置和状态。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // Step 1 – create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **为什么重要：** `OcrEngine` 是 Aspose 识别管道的入口。没有它，你无法访问过滤器、语言包或 `Recognize` 方法。

## 第二步：添加预处理过滤器 – 在 **从 jpg 中提取文本** 时提升准确率

相机直接拍摄的图像很少完美。倾斜角度或随机噪点会让即使是最好的 OCR 算法也束手无策。在 **从 jpg 中提取文本** 之前添加几种过滤器，能够显著提升结果质量。

```csharp
        // Step 2 – add preprocessing filters
        // Deskew corrects rotation; DenoiseGaussian reduces visual noise
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });
```

> **专业提示：** 如果源图像已经很干净，可以跳过 `DenoiseGaussianFilter`。过度平滑可能会抹掉微弱的字符。

## 第三步：为 OCR 加载图像 – 将 JPEG 输入引擎

接下来是 **为 OCR 加载图像**。Aspose 提供了便利的 `ImageStream.FromFile` 辅助方法，将文件路径包装成引擎可识别的流。

```csharp
        // Step 3 – specify the path to the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        // Load the image and run OCR in one call
        var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));
```

> **边缘情况：** 如果文件不存在，`FromFile` 会抛出 `FileNotFoundException`。如果运行时可能出现缺失文件，请将调用包装在 try/catch 中。

## 第四步：获取并显示识别结果

最后，当引擎完成识别后，你可以通过 `Text` 属性获取纯文本结果。将其打印到控制台足以演示，但你也可以将其写入数据库或文本文件。

```csharp
        // Step 4 – output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**预期输出**

```
=== OCR Result ===
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
```

具体内容取决于你提供的图像，但你应该会看到一段格式良好的文本，而不是乱码。

![显示 OCR 流程图 – 在图像上运行 OCR、预处理、加载、识别](/images/ocr-pipeline.png "在图像上运行 OCR 流程图")

### 为什么每一步都重要

| 步骤 | 目的 | 若省略会怎样 |
|------|------|--------------|
| **创建引擎** | 初始化内部结构 | 没有识别器可用 – 会出现 `NullReferenceException`。 |
| **添加过滤器** | 通过校正旋转和噪声提升准确率 | 倾斜或噪声图像会产生乱码输出。 |
| **加载图像** | 为引擎提供原始位图 | 引擎没有可处理的内容，`Text` 字段为空。 |
| **读取结果** | 提取纯文本供后续使用 | 虽然运行了 OCR，却看不到结果 – 用途不大！ |

## 常见变体及流程微调

### 更换语言包

Aspose OCR 开箱即支持多语言。如果需要 **在图像上运行 OCR** 并识别法语或德语等文本，请在调用 `Recognize` 前设置 `Language` 属性。

```csharp
ocrEngine.Language = OcrLanguage.French;
```

### 处理多页 PDF

如果源文件是多页 PDF 而非单个 JPEG，你可以先使用 Aspose.PDF 将每页转换为图像，然后将每张图像送入同一流水线。遍历页面的代码非常简洁：

```csharp
foreach (var pageImage in pdfPagesAsImages)
{
    var result = ocrEngine.Recognize(ImageStream.FromMemory(pageImage));
    Console.WriteLine(result.Text);
}
```

### 处理大文件

处理高分辨率图片时，内存占用可能会激增。考虑在 **为 OCR 加载图像** 之前对图像进行降采样：

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

var loadOptions = new JpegLoadOptions { Width = 1024, Height = 768 };
using (var img = (Image)Image.Load(imagePath, loadOptions))
{
    var stream = new MemoryStream();
    img.Save(stream, new JpegOptions());
    var ocrResult = ocrEngine.Recognize(ImageStream.FromMemory(stream.ToArray()));
}
```

## 完整、可直接运行的示例

下面是整合了上述所有内容的完整程序。复制粘贴到新的控制台项目中，将 `YOUR_DIRECTORY` 替换为存放 `input.jpg` 的文件夹路径，然后按 **F5** 运行。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Add useful preprocessing filters
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });

        // 3️⃣ Load the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        try
        {
            // Recognize text – this is where we actually run OCR on image
            var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));

            // 4️⃣ Print the extracted text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

### 验证结果

1. 运行程序。  
2. 查看控制台 – 你应该能看到 `input.jpg` 上的文本。  
3. 若输出出现乱码，尝试调整 `DenoiseGaussianFilter` 的 `Sigma` 值，或添加其他过滤器，如 `ContrastEnhancementFilter`。

## 小结与后续步骤

我们已经完整演示了如何使用 Aspose OCR **在图像上运行 OCR**，从引擎初始化到输出干净、可读的文本。关键要点如下：

- 创建 `OcrEngine` 实例。  
- 使用 `DeskewFilter`、`DenoiseGaussianFilter` 等 **为 OCR 预处理图像**。  
- 使用 `ImageStream.FromFile` **为 OCR 加载图像**。  
- 调用 `Recognize` 并读取 `ocrResult.Text` 以 **从 jpg 中提取文本**。

想进一步深入？可以尝试以下思路：

- **批量处理** – 读取一个文件夹中的所有 JPEG，并将每个结果输出为单独的 `.txt` 文件。  
- **集成 Azure Blob Storage** – 从云端拉取图片，运行 OCR，然后将文本存回。  
- **结合 NLP** – 将提取的文本喂入语言理解模型，实现发票自动分类。

欢迎尝试不同的过滤器组合、语言包，甚至切换到 PNG、TIFF 等格式——只要 **为 OCR 加载图像** 正确，整个流水线都能工作。

---

如果遇到任何问题，欢迎在下方留言或查阅 Aspose OCR 文档获取高级设置。祝编码愉快，玩转图片转可搜索文本！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}