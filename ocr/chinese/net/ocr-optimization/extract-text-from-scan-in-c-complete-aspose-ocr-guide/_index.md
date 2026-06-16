---
category: general
date: 2026-02-19
description: 学习如何使用 Aspose OCR 从扫描图像中提取文本，并对图像进行预处理以提升 OCR 准确率。一步一步的 C# 教程。
draft: false
keywords:
- extract text from scan
- preprocess image for ocr
language: zh
og_description: 快速从扫描件中提取文本。本指南展示如何对图像进行 OCR 预处理，并使用 Aspose OCR 在 C# 中获得可靠的结果。
og_title: 从扫描中提取文本 – 完整的 C# Aspose OCR 教程
tags:
- OCR
- C#
- Aspose
title: 在 C# 中从扫描中提取文本 – 完整的 Aspose OCR 指南
url: /zh/net/ocr-optimization/extract-text-from-scan-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从扫描中提取文本 – 完整的 Aspose OCR 指南

是否曾经需要**从扫描文件中提取文本**却总是得到乱码？你并不是唯一遇到这种情况的人。在许多真实项目中——比如发票数字化或旧文档归档——从扫描图像中获取干净的文本是第一道难关。好消息是，只需几行 C# 代码和 Aspose OCR，你就可以把噪声 JPEG 转换为可读字符，而一点预处理就能让结果从“马马虎虎”变成“惊艳”。

在本教程中，我们将完整演示整个流程：设置 OCR 引擎、**为 OCR 预处理图像**以提升质量、运行识别，最后打印提取的文本。完成后，你将拥有一个可直接运行的控制台应用，能够可靠地从任意扫描图像中提取文本。

## 需要的环境

在开始之前，请确保你拥有：

- **.NET 6+**（或 .NET Framework 4.7.2+）已安装——API 两者兼容。  
- **Aspose.OCR** NuGet 包（`Install-Package Aspose.OCR`）——唯一的外部依赖。  
- 一张示例扫描图像（例如 `skewed_scan.jpg`），放在可引用的文件夹中。  
- 任意代码编辑器或 IDE——Visual Studio、Rider 或 VS Code 都可以。

除此之外不需要其他库；我们将使用的预处理选项已内置于 Aspose OCR。

## 第一步：创建新控制台项目

首先，新建一个干净的控制台应用，以便拥有一个纯净的沙箱。

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

就这样——你的项目已经引用了 OCR 库。打开 `Program.cs`，删除默认的 `Hello World` 行，我们将用自己的代码替换它。

## 第二步：初始化 OCR 引擎 – 提取的核心

要**从扫描中提取文本**，需要创建一个 `OcrEngine` 实例。将语言设置为英文是最常见的情况，但如果需要，Aspose 支持数十种语言。

```csharp
using Aspose.OCR;
using Aspose.OCR.Preprocessing;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine and tell it we’re dealing with English text
        var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };
```

为什么要先实例化引擎？引擎保存了所有配置——语言、预处理以及内部缓存——提前创建可以确保后续的每一次调用都使用相同的设置。

## 第三步：为 OCR 预处理图像 – 提升准确率

扫描图像很少是完美的。它们可能被旋转、噪声较多或对比度低。Aspose OCR 提供了三种实用的预处理选项，能够显著提升识别效果：

- **Deskew** – 自动校正旋转的页面。  
- **Denoise** – 平滑斑点和颗粒噪声。  
- **Contrast** – 提升微弱字符的亮度。

```csharp
        // 2️⃣ Turn on preprocessing to clean up the image
        ocrEngine.Preprocessing = new PreprocessingOptions
        {
            Deskew = DeskewAdvanced.Enable(),      // corrects rotation
            Denoise = DenoiseWavelet.Enable(),    // reduces noise
            Contrast = ContrastBoost.Enable()     // enhances contrast
        };
```

把这一步想象成在把照片交给 OCR 引擎之前，先给扫描仪做一次快速抛光。跳过它就像尝试阅读一张被污渍覆盖的明信片——虽然可能，但会非常令人沮丧。

## 第四步：识别文本 – 真正的提取

现在把处理好的图像喂给引擎。将 `YOUR_DIRECTORY` 替换为实际存放 `skewed_scan.jpg` 的路径。

```csharp
        // 3️⃣ Run OCR on the preprocessed image
        var ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/skewed_scan.jpg");
```

`RecognizeImage` 方法返回一个 `OcrResult` 对象，其中包含原始文本、置信度分数，甚至还有后续可能需要的边界框信息。

## 第五步：显示（或保存）提取的文本

最后，让我们看看得到了什么。在真实项目中，你可能会把结果写入数据库或文件；这里我们仅将其打印到控制台。

```csharp
        // 4️⃣ Output the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

运行程序（`dotnet run`）后，你应该会看到类似下面的输出：

```
=== Extracted Text ===
Invoice #12345
Date: 01/02/2026
Total: $1,234.56
Thank you for your business!
```

如果输出仍然是乱码，请再次确认图像路径是否正确，以及预处理选项是否已启用。通常是细微的旋转或严重的噪声导致问题。

![从扫描中提取文本示例](/images/ocr-example.png)

*Alt text: 使用 Aspose OCR 在 C# 中从扫描中提取文本的截图*

## 常见陷阱及规避方法

- **文件路径错误** – 相对路径是相对于项目根目录，而不是二进制文件夹。若不确定，请使用绝对路径。  
- **不支持的图像格式** – Aspose OCR 支持 JPEG、PNG、BMP、TIFF。若是 PDF，请先转换为图像。  
- **缺少语言数据** – 对于非英文语言，可能需要从 Aspose 官方站点下载额外的语言包。  
- **过度预处理** – 对已经很干净的图像同时使用去噪和对比度提升，可能会把微弱字符冲淡。请分别测试每个选项的效果。

小技巧：如果只需要校正倾斜（大多数扫描仅此），可以省去去噪和对比度提升，以节省几毫秒的处理时间。

## 扩展方案 – 需要更多功能？

### 从多个扫描中提取文本

将识别代码包装在 `foreach` 循环中，遍历文件夹内的所有图像：

```csharp
string[] files = Directory.GetFiles(@"YOUR_DIRECTORY", "*.jpg");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"--- {Path.GetFileName(file)} ---");
    Console.WriteLine(result.Text);
}
```

### 获取置信度分数

如果需要过滤低置信度的结果：

```csharp
if (ocrResult.Confidence < 0.75)
{
    Console.WriteLine("Warning: Low confidence, consider manual review.");
}
```

### 在 Web API 中使用 OCR

通过 ASP.NET Core 端点公开提取逻辑。核心代码保持不变，只需将引擎注入为单例服务即可。

## 小结

我们已经完整演示了如何使用 Aspose OCR 在 C# 中**从扫描图像中提取文本**。从项目创建开始，我们：

1. 使用英文初始化了 OCR 引擎。  
2. **为 OCR 预处理图像**，包括校正倾斜、去噪和对比度提升。  
3. 对示例 JPEG 运行识别。  
4. 将干净的文本打印到控制台。

有了这些构件，你现在可以将 OCR 嵌入发票处理器、文档归档系统或任何需要将纸质内容转为可搜索数据的应用中。

## 接下来可以做什么？

- 尝试其他预处理组合（例如 `Binarize` 用于黑白文档）。  
- 试验不同语言或多语言检测。  
- 将 OCR 输出与自然语言处理结合，自动抽取关键字段。

如果在使用过程中遇到问题或发现了巧妙的技巧，欢迎留言交流。祝编码愉快，愿你的扫描始终清晰如新！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}