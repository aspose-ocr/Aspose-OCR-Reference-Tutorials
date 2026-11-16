---
category: general
date: 2026-03-13
description: 使用 Aspose OCR 在 C# 中从图像提取文本。学习如何加载图像进行 OCR、在图像上运行 OCR，并使用清晰的逐步代码提取西里尔文文本。
draft: false
keywords:
- extract text from image
- load image for ocr
- run ocr on image
- extract cyrillic text
- recognize cyrillic text
language: zh
og_description: 使用 Aspose OCR 在 C# 中从图像提取文本。本教程展示了如何加载图像进行 OCR、对图像运行 OCR，以及高效提取西里尔文文本。
og_title: 使用 Aspose OCR 从图像提取文本 – C# 指南
tags:
- Aspose OCR
- C#
- Image Processing
title: 使用 Aspose OCR 从图像提取文本 – C# 编程指南
url: /zh/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 从图像提取文本 – C# 编程指南

是否曾经需要 **从图像中提取文本**，却不确定哪个库能够毫无障碍地处理西里尔字符？你并不孤单。在许多项目中——发票扫描、护照验证或快速记笔记——从图片中获取可靠的文本是必不可少的。

在本指南中，我们将逐步演示 **加载图像进行 OCR**、配置 Aspose OCR、**在图像上运行 OCR**，以及仅用几行 C# **提取西里尔文本**。完成后，你将拥有一个可直接运行的代码片段，能够将识别的文本打印到控制台。

## 你将学到

- 如何安装并引用 Aspose OCR NuGet 包。  
- 正确指向语言包资源的方式。  
- 为非拉丁脚本选择 `Language.Cyrillic` 的重要性。  
- 常见陷阱（缺少资源、不受支持的图像格式）以及如何规避。  
- 一个完整、可运行的示例，能够直接放入任何 .NET 项目。

无需任何 OCR 经验，但对 C# 和 Visual Studio 有基本了解会让学习过程更顺畅。

## 前置条件

在开始之前，请确保你已具备：

1. 已安装 **.NET 6.0** 或更高版本（代码兼容 .NET Core 和 .NET Framework）。  
2. **Visual Studio 2022**（或任何支持 C# 的编辑器）。  
3. **Aspose.OCR** NuGet 包。通过包管理控制台安装：

   ```powershell
   Install-Package Aspose.OCR
   ```

4. 包含 OCR 语言包的文件夹（可从 Aspose 官网下载）。  
5. 一张包含西里尔文本的图像文件（示例中为 `cyrillic.png`），用于读取。

> **小贴士：** 将语言包文件夹放在项目的 `bin` 目录旁边，可简化路径处理。

## 步骤 1 – 加载图像进行 OCR

首先，需要为引擎提供一个位图。Aspose OCR 接受 `ImageStream`，可以直接从文件路径创建。

```csharp
using Aspose.OCR;

// Step 1: Load the image you want to process
string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
ImageStream image = ImageStream.FromFile(imagePath);
```

*为什么重要：* 预先加载图像可以验证文件是否存在以及是否为受支持的格式（PNG、JPEG、BMP 等）。如果文件缺失，`FromFile` 调用会抛出明确的异常，避免后续出现模糊的 OCR 错误。

## 步骤 2 – 设置 OCR 引擎和资源

接下来，实例化 OCR 引擎并指向存放语言包的文件夹。没有正确的资源，引擎将无法识别西里尔字形。

```csharp
// Step 2: Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Tell Aspose where the language resources live
string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
ocrEngine.SetResourcesPath(resourcesPath);
```

*为什么重要：* `SetResourcesPath` 方法是代码与包含各语言字符形状的数据文件之间的桥梁。忘记此步骤通常会导致输出乱码或抛出 `ResourceNotFoundException`。

## 步骤 3 – 选择语言并 **在图像上运行 OCR**

现在选择我们期望的语言。示例中使用西里尔字符，因此设置 `Language.Cyrillic`。如果需要处理多种脚本，可使用按位或 (`|`) 运算符组合。

```csharp
// Step 3: Select the language you want to recognize
ocrEngine.Language = Language.Cyrillic;

// Assign the previously loaded image to the engine
ocrEngine.Image = image;

// Finally, perform the recognition
ocrEngine.Recognize();
```

*为什么重要：* 指定语言会缩小 OCR 算法的搜索空间，显著提升速度和准确率。当使用正确的语言标志 **在图像上运行 OCR** 时，误识别会大幅减少。

## 步骤 4 – 获取并使用提取的西里尔文本

识别完成后，引擎将结果存放在 `Text` 属性中。此时你可以将其显示、写入文件，或传递给其他系统。

```csharp
// Step 4: Output the recognized text
string recognizedText = ocrEngine.Text;
Console.WriteLine("=== Extracted Cyrillic Text ===");
Console.WriteLine(recognizedText);
```

典型的控制台输出如下：

```
=== Extracted Cyrillic Text ===
Привет, мир! Это тестовое изображение.
```

如果输出中出现意外符号，请再次确认语言包的版本与已安装的 Aspose OCR 匹配。

## 完整工作示例 – 合并所有步骤

下面是可以直接复制粘贴到新控制台项目中的完整程序。将 `YOUR_DIRECTORY` 替换为你机器上的实际路径。

```csharp
using System;
using Aspose.OCR;

namespace ExtractCyrillicDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the image you want to process
            string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // 2️⃣ Initialize OCR engine and point to language resources
            OcrEngine ocrEngine = new OcrEngine();
            string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
            ocrEngine.SetResourcesPath(resourcesPath);

            // 3️⃣ Choose Cyrillic language and run OCR on image
            ocrEngine.Language = Language.Cyrillic;
            ocrEngine.Image = image;
            ocrEngine.Recognize();

            // 4️⃣ Extract and display the text
            string result = ocrEngine.Text;
            Console.WriteLine("=== Extracted Cyrillic Text ===");
            Console.WriteLine(result);
        }
    }
}
```

### 预期结果

运行程序后，控制台应打印出 `cyrillic.png` 中的完整文本。如果图像包含短语 “Привет, мир!”，则该行会原样显示在控制台中，不会出现额外符号。

## 边缘情况与故障排除

| 情况 | 检查要点 | 建议解决方案 |
|-----------|---------------|---------------|
| **缺少语言包** | `resourcesPath` 是否指向包含 `.dat` 文件的文件夹？ | 重新从 Aspose 下载语言包并放置在指定文件夹中。 |
| **不受支持的图像格式** | 文件是否为 PNG、JPEG、BMP 或 TIFF？ | 在调用 `FromFile` 前将图像转换为受支持的格式。 |
| **输出出现乱码** | 是否正确设置了 `ocrEngine.Language`？ | 使用 `Language.Cyrillic`（或组合多个语言标志）。 |
| **大图像导致性能下降** | 图像分辨率是否超过 3000 px？ | 在 OCR 前将图像缩小到合理尺寸（例如宽度 1024 px）。 |

## 你可能感兴趣的相关主题

- 使用 Aspose PDF + OCR **从 PDF 中提取图像文本**。  
- 从 `Stream` **加载图像进行 OCR**（适用于图像来自 Web API 的场景）。  
- 并行 **在图像上运行 OCR** 以加速批量处理。  
- 使用 Aspose OCR 手写模式 **提取手写笔记的西里尔文本**。  
- 将结果与 **在数据库中识别西里尔文本** 集成，以实现搜索索引。

## 结论

本文展示了如何使用 Aspose OCR **从图像中提取文本**，涵盖了从加载图像到打印识别的西里尔字符的全部步骤。简短的自包含程序演示了所需的最小代码，而故障排除表格帮助你规避常见问题。

尝试在自己的截图上运行，换用阿拉伯语或中文语言包，感受同一套流程在全球范围的适用性。祝编码愉快，愿你的 OCR 结果始终清晰如晶！ 

![Extract text from image example](extract-text-from-image.png "Extract text from image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}