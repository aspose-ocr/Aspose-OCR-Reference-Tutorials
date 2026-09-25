---
category: general
date: 2026-02-17
description: 如何在 C# 中快速执行 OCR 并将图像转换为 JSON。请遵循此 C# OCR 教程，从图像中提取文本并将布局保存为 JSON。
draft: false
keywords:
- how to perform OCR
- convert image to json
- c# ocr tutorial
- extract text image c#
- load image file c#
language: zh
og_description: 如何在 C# 中执行 OCR？本指南向您展示如何将图像转换为 JSON、在 C# 中从图像中提取文本以及加载图像文件进行 OCR。
og_title: 如何在 C# 中进行 OCR – 将图像转换为 JSON
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中进行 OCR – 将图像转换为 JSON 的指南
url: /zh/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-json-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中执行 OCR – 将图像转换为 JSON 指南

是否曾想过 **如何在 C# 中执行 OCR** 来处理收据、发票或任何扫描文档？你并不是唯一有此困惑的人。许多开发者在需要提取文本 *并* 保持布局时会遇到瓶颈，而不想花费数小时编写自定义解析器。

在本教程中，我们将完整演示一个 **c# ocr tutorial**，向你展示如何执行 OCR、**将图像转换为 JSON**，并将结果保存以供后续分析。完成后，你将拥有一个可直接运行的控制台应用程序，能够在 C# 中加载图像文件、提取文本，并生成包含坐标、置信度分数和原始文本的详细 JSON 文件。

## 前置条件 — 你需要准备的东西

- .NET 6 SDK 或更高版本（代码同样适用于 .NET Core）  
- Visual Studio 2022 或任意你喜欢的编辑器  
- Aspose OCR 许可证（可先使用免费试用版）  
- 一张示例图片，例如 `receipt.png`，放置在可引用的文件夹中  

就这些——除 `Aspose.OCR` 之外无需额外的 NuGet 包。如果你已经准备好上述内容，即可开始。

## 如何执行 OCR 并获取 JSON 输出

使用 Aspose 执行 **如何执行 OCR** 的核心步骤非常直接：创建 `OcrEngine`，提供图像流，调用 `Recognize`，然后将 `OcrResult` 序列化为 JSON。下面我们一步一步拆解。

### 步骤 1：安装 Aspose OCR NuGet 包

在项目文件夹的终端中运行：

```bash
dotnet add package Aspose.OCR
```

> **小技巧：** 使用 `--version` 参数锁定到最新的稳定版本（例如 `23.9.0`），可以保证构建可复现。

### 步骤 2：创建控制台项目骨架

如果还没有项目，创建一个：

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
```

现在你已经拥有一个 `Program.cs` 文件，可以在其中编写 **加载图像文件 c#** 并启动 OCR 过程的代码。

### 步骤 3：编写完整的 OCR‑to‑JSON 代码

下面是完整的、可直接运行的程序。将其复制粘贴到 `Program.cs` 中。每行代码都有注释，帮助你了解 *为什么* 需要这些代码。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutput
{
    static void Main()
    {
        // ---------------------------------------------------------
        // 1️⃣  Initialize the OCR engine – this object holds
        //     language settings, recognition options, etc.
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // 2️⃣  Load the image you want to analyze.
        //     This demonstrates **load image file c#** in a clean way.
        // ---------------------------------------------------------
        // Replace the path with the actual location of your receipt.png
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");
        ImageStream image = ImageStream.FromFile(imagePath);

        // ---------------------------------------------------------
        // 3️⃣  Perform the recognition.
        //     The engine returns an OcrResult containing text,
        //     confidence scores, and layout information.
        // ---------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ---------------------------------------------------------
        // 4️⃣  Convert the result to a detailed JSON string.
        //     This is the heart of **convert image to json**.
        // ---------------------------------------------------------
        string jsonResult = ocrResult.ToJson();

        // ---------------------------------------------------------
        // 5️⃣  Save the JSON to disk – you can later import this into
        //     databases, analytics pipelines, or UI components.
        // ---------------------------------------------------------
        string jsonPath = Path.Combine(
            Environment.CurrentDirectory, "receipt.json");
        File.WriteAllText(jsonPath, jsonResult);

        // ---------------------------------------------------------
        // 6️⃣  Let the user know we’re done.
        // ---------------------------------------------------------
        Console.WriteLine("JSON with layout saved to " + jsonPath);
    }
}
```

#### 代码功能说明

| 步骤 | 为什么重要 |
|------|------------|
| **Initialize OcrEngine** | 设置默认语言（英语）并准备内部模型。 |
| **Load image file** | 使用 `ImageStream.FromFile` 可确保图像以 Aspose 期望的格式读取。 |
| **Recognize** | 核心工作——像素分析、字符分割以及词典查找。 |
| **ToJson** | 生成结构化输出，包含边界框、置信度和原始文本。 |
| **WriteAllText** | 将 JSON 持久化，便于与其他服务共享。 |
| **Console.WriteLine** | 提供即时反馈——在终端运行时非常实用。 |

> **注意：** 如果图像较大，建议先对其进行缩放，以提升速度并降低内存占用。Aspose 提供 `Resize` 方法，可在 `ImageStream` 上调用。

### 步骤 4：运行应用并验证输出

在终端中执行：

```bash
dotnet run
```

你应该会看到：

```
JSON with layout saved to C:\Path\To\OcrJsonDemo\receipt.json
```

打开 `receipt.json`，任意编辑器中会看到类似如下内容：

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $12.34",
          "Confidence": 0.98,
          "BoundingBox": { "X": 120, "Y": 340, "Width": 150, "Height": 30 }
        }
      ]
    }
  ]
}
```

该 JSON 捕获了 **extract text image c#** 以及布局元数据，十分适合后续处理。

## 将图像转换为 JSON – 超越基础

既然已经掌握了 **如何执行 OCR**，接下来我们看看实际项目中可能需要的几种变体。

### 处理多页文档

如果源文件是多页 PDF 或 TIFF，只需遍历每一页：

```csharp
foreach (var pageStream in multiPageImageStreams)
{
    OcrResult result = ocrEngine.Recognize(pageStream);
    // Append each page's JSON to a master list
}
```

### 自定义语言和精度

Aspose 支持 40 多种语言。切换到西班牙语：

```csharp
ocrEngine.Language = Language.Spanish;
```

你还可以调整 `ocrEngine.Settings`，启用 **auto‑rotate**、**noise removal** 或 **dictionary‑based correction**——这些都能提升生成的 JSON 质量。

### 以美化格式保存 JSON

如果希望 JSON 具备缩进以便阅读：

```csharp
string prettyJson = ocrResult.ToJson(true); // true = formatted
File.WriteAllText(jsonPath, prettyJson);
```

## Load Image File C# – 常见坑点与技巧

在 **load image file c#** 时，可能会遇到：

- **文件未找到** – 确保使用绝对路径，或通过 `Path.Combine` 与 `Environment.CurrentDirectory` 组合路径。  
- **不支持的格式** – Aspose 支持 PNG、JPEG、BMP、TIFF 和 PDF。对于 RAW 格式，请先转换。  
- **大文件导致内存压力** – 使用 `ImageStream.FromFile(path, maxSizeInKB)` 在加载时进行下采样。

提前解决这些问题，可避免在 OCR 流程后期出现难以定位的异常。

## Extract Text Image C# – 验证结果

获取 JSON 后，若只需要纯文本，可使用：

```csharp
var ocrResult = ocrEngine.Recognize(image);
string plainText = ocrResult.Text; // Simple string with line breaks
Console.WriteLine(plainText);
```

该代码演示了 **extract text image c#**，不包含布局细节，适用于快速搜索或日志记录。

---

![Diagram showing OCR workflow – how to perform OCR, convert image to JSON, and extract text image c#](/images/ocr-workflow.png "how to perform OCR workflow")

*图片 alt 文本: "how to perform OCR workflow diagram illustrating convert image to JSON and extract text image c#"*  

*(该图片为占位符，发布时请替换为实际流程图。)*

---

## 结论

我们从头到尾完整演示了 **如何在 C# 中执行 OCR**，并展示了 **将图像转换为 JSON** 的全过程，同时解释了 **load image file c#** 与 **extract text image c#** 的细节。完整代码可直接嵌入任意 .NET 项目，生成的 JSON 同时提供原始文本和精准的布局数据，便于后续分析。

接下来可以尝试将 JSON 写入数据库、在 UI 上可视化边界框，或批量处理多个 OCR 任务。你也可以探索 Aspose 的其他功能，如手写识别或条形码检测——这些都能自然地融入同一流水线。

如果遇到问题，请回顾 “Load Image File C#” 部分的故障排查技巧，或查阅 Aspose 的详细文档以获取高级设置。祝编码愉快，玩转图像到结构化数据的转换！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}