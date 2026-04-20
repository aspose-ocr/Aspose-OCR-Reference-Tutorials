---
category: general
date: 2026-02-28
description: 如何在 C# 中使用 Aspose OCR 运行 OCR——学习如何从图像中提取文本，仅需几步即可将图像转换为 JSON 或 XML。
draft: false
keywords:
- how to run OCR
- extract text from image
- convert image to json
- convert image to xml
- how to extract text
language: zh
og_description: 如何在 C# 中使用 Aspose OCR 运行 OCR —— 探索如何从图像中提取文本并将图像转换为 JSON 或 XML，附带可直接运行的示例。
og_title: 如何在 C# 中使用 Aspose OCR 运行 OCR – 完整指南
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中使用 Aspose OCR 运行 OCR – 完整指南
url: /zh/net/text-recognition/how-to-run-ocr-with-aspose-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR 在 C# 中运行 OCR – 完整指南

如果你想了解 **如何在 C# 中运行 OCR** 来处理收据图片，你来对地方了。在本教程中，我们将演示 **从图像中提取文本**，以及使用 Aspose OCR 将 **图像转换为 JSON** 或 **图像转换为 XML**，全部在一个独立的程序中完成。

想象一下，你正在构建一个费用跟踪应用，需要从拍摄的收据中提取明细。手动逐条输入既费时又繁琐，对吧？阅读完本指南后，你将拥有一个可复用的代码片段，能够读取任意图像，返回结构化文本，并提供 JSON 与 XML 两种格式，方便后续处理。

## 前置条件

在开始之前，请确保你已经具备以下环境：

- .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Framework 4.8）
- Visual Studio 2022（或你喜欢的任何编辑器）
- 已激活的 **Aspose.OCR** NuGet 包（`Install-Package Aspose.OCR`）
- 一张示例图片（例如 `receipt.png`），放置在可引用的文件夹中

无需额外配置；库已自带所有必需的 OCR 模型。

![用于 OCR 处理的收据图像 – how to run OCR](receipt.png)

> *Alt text: 用于 OCR 处理的收据图像 – how to run OCR*

## 步骤实现

下面我们将解决方案拆分为若干逻辑块。每一步都会解释 **为什么** 要这么做，而不仅仅是展示 **代码**。

### 1️⃣ 初始化 OCR 引擎 – **how to run OCR** 的基础

`OcrEngine` 类是入口点。实例化它会加载内部语言模型并为识别做好准备。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        // This object holds the OCR model and settings.
        var ocrEngine = new OcrEngine();
```

> **专业提示：** 在多张图片之间复用同一个 `OcrEngine` 可以降低内存消耗并加快批处理速度。

### 2️⃣ 加载图片 – **extract text from image** 的核心

Aspose OCR 使用自己的 `Image` 包装类。使用 `using` 语句可以确保文件句柄及时释放。

```csharp
        // Step 2: Load the image you want to analyze
        // Replace YOUR_DIRECTORY with the actual path on your machine.
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");
```

如果图片是其他格式（BMP、TIFF、PDF），同样的 `Load` 方法也能处理——无需额外转换。

### 3️⃣ 执行 OCR 识别 – **how to run OCR** 的核心环节

调用 `Recognize` 完成繁重的工作：版面分析、字符分割以及语言特定的分类。

```csharp
        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);
```

返回的 `OcrResult` 包含原始文本、置信度分数以及可序列化的详细版面树。

### 4️⃣ 将图像转换为 JSON – **convert image to json** 的直接方式

JSON 非常适合 Web API 或 NoSQL 存储。`ToJson` 方法会返回格式化的字符串，调试时非常方便。

```csharp
        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);
```

典型的 JSON 输出如下（为简洁起见已截断）：

```json
{
  "Text": "Total 12.34",
  "Blocks": [
    {
      "Text": "Total",
      "Confidence": 0.98,
      "Bounds": { "X": 10, "Y": 150, "Width": 45, "Height": 15 }
    },
    {
      "Text": "12.34",
      "Confidence": 0.97,
      "Bounds": { "X": 60, "Y": 150, "Width": 30, "Height": 15 }
    }
  ]
}
```

现在你可以直接将该 JSON 发送到 REST 接口，或存入 Azure Cosmos DB。

### 5️⃣ 将图像转换为 XML – 当需要 **convert image to xml** 时

一些老旧系统仍然使用 XML。Aspose 提供的 `ToXml` 能生成干净、符合模式的 XML 表示。

```csharp
        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

示例 XML 片段：

```xml
<OcrResult>
  <Text>Total 12.34</Text>
  <Blocks>
    <Block>
      <Text>Total</Text>
      <Confidence>0.98</Confidence>
      <Bounds X="10" Y="150" Width="45" Height="15" />
    </Block>
    <Block>
      <Text>12.34</Text>
      <Confidence>0.97</Confidence>
      <Bounds X="60" Y="150" Width="30" Height="15" />
    </Block>
  </Blocks>
</OcrResult>
```

两种格式保存了相同的层级数据，你可以根据下游管道的需求自由选择。

## 常见坑点与可靠提取文本的技巧

即使使用了强大的库，真实场景的图片仍会带来各种挑战。下面列出三类常见问题及对应的解决方案。

### 📏 低分辨率图片

**影响原因：** 小字号会合并，导致置信度下降。  
**解决方案：** 预处理图片——使用 `Image.Resize` 放大，或在调用 `Recognize` 前应用锐化滤镜。

```csharp
using var highRes = image.Resize(2.0, InterpolationMode.HighQualityBicubic);
var result = ocrEngine.Recognize(highRes);
```

### 🌈 对比度差

**影响原因：** 亮文字在暗背景上会干扰分割算法。  
**解决方案：** 反转颜色或通过 `Image.AdjustBrightnessContrast` 调整亮度/对比度。

```csharp
image.AdjustBrightnessContrast(brightness: 30, contrast: 40);
```

### 📄 多语言文档

**影响原因：** 默认语言模型是英文，混合语言会导致输出乱码。  
**解决方案：** 在识别前设置 `ocrEngine.Language = OcrLanguage.Multilingual;`

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

处理好这些边缘情况后，**从任何图片中提取文本** 将变得可靠且可预测。

## 完整可运行示例（复制粘贴即用）

下面是完整的程序代码，直接编译运行即可。只需将 `YOUR_DIRECTORY` 替换为图片所在路径，然后按 F5 运行。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Optional: improve accuracy for low‑contrast images
        // ocrEngine.Language = OcrLanguage.Multilingual;

        // Step 2: Load the image you want to analyze
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");

        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);

        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

**预期的控制台输出**（为便于阅读已做格式化）会同时展示包含提取文本和边界框的 JSON 与 XML 结构。

## 小结 – 本文涵盖内容

- 使用 Aspose OCR 在 C# 中 **how to run OCR**
- **extract text from image** 的逐步流程
- 两种序列化方式：**convert image to json** 与 **convert image to xml**
- 处理低分辨率、低对比度和多语言场景的技巧
- 一个完整、可直接复制粘贴的代码示例，适用于任何 .NET 项目

## 接下来可以做什么？

现在你已经掌握了 **how to extract text** 并获得结构化数据，下面可以尝试以下进阶思路：

- 将 JSON 发送到 Azure Function，存入 Cosmos DB 中的收据记录。
- 使用 XML 输出填充已有的基于 SOAP 的会计系统。
- 将 Aspose OCR 与机器学习模型结合，实现费用类型的自动分类。

尽情实验吧——把 `receipt.png` 换成发票、名片或手写笔记。相同的模式同样适用于这些场景。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}