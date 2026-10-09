---
category: general
date: 2026-10-08
description: 学习如何在 C# 中使用 Aspose.OCR 执行 OCR，以从图像文件中提取文本。本指南向您展示如何将图像转换为文本以及如何识别 JPEG
  中的文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- recognize text from jpeg
- c# ocr example
language: zh
lastmod: 2026-10-08
og_description: 如何在 C# 中使用 Aspose.OCR 执行 OCR。请按照本分步指南从图像文件中提取文本，将图像转换为文本，并识别 JPEG
  中的文本。
og_image_alt: Console output displaying Cyrillic text recognized from a JPEG image
  by a C# OCR program
og_title: 如何在 C# 中进行 OCR – 从图像中提取文本
schemas:
- author: Aspose
  dateModified: '2026-10-08'
  description: Learn how to perform OCR in C# using Aspose.OCR to extract text from
    image files. This guide shows you how to convert image to text and recognize text
    from JPEG.
  headline: How to perform OCR in C# – extract text from images
  type: TechArticle
- description: Learn how to perform OCR in C# using Aspose.OCR to extract text from
    image files. This guide shows you how to convert image to text and recognize text
    from JPEG.
  name: How to perform OCR in C# – extract text from images
  steps:
  - name: Why each line matters
    text: '* **`OcrEngine ocrEngine = new OcrEngine();`** – Instantiates the engine
      that orchestrates the whole OCR pipeline. * **`ocrEngine.Language = Language.Cyrillic;`**
      – Selects the language model. Choosing the correct language dramatically improves
      accuracy when you **extract text from image** files tha'
  - name: 4.1 Recognizing English or multilingual text
    text: 'Replace the language assignment with the appropriate enum:'
  - name: 4.2 Processing images from a stream instead of a file
    text: 'If your image arrives via an HTTP response or a database blob, use a `MemoryStream`:'
  - name: 4.3 Handling large or low‑resolution images
    text: 'Large images increase memory consumption. You can downscale before OCR:'
  - name: 4.4 Error handling
    text: 'Wrap the recognition call in a try‑catch block to catch network or file‑access
      errors:'
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
- Image Processing
title: 如何在 C# 中进行 OCR —— 从图像提取文本
url: /zh/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中执行 OCR – 从图像中提取文本

如果您需要在 .NET 应用程序中 **how to perform OCR**，本教程为您提供完整、可直接运行的解决方案。使用 Aspose.OCR，您可以 **extract text from image** 文件、**convert image to text**，以及 **recognize text from JPEG**，只需几行代码。

您将看到完整的工作流程——从安装库到打印识别的字符串——这样您可以将示例复制到自己的项目中，立即开始处理图像。

## 您将学习的内容

* 如何为 OCR 任务设置 C# 项目。  
* 如何加载 JPEG（或任何受支持的图像）并运行识别。  
* 如何获取生成的文本并在应用程序中使用它。  

唯一的前提条件是最近的 .NET SDK（≥ .NET 6）以及用于首次语言模型下载的互联网连接。

## 第一步：设置项目并安装 Aspose.OCR

1. 创建一个新的控制台项目：

   ```bash
   dotnet new console -n OcrDemo
   cd OcrDemo
   ```

2. 添加 Aspose.OCR NuGet 包：

   ```bash
   dotnet add package Aspose.OCR
   ```

   该包包含 OCR 引擎、语言模型以及进行 **convert image to text** 所需的图像处理工具。

> **Pro tip:** 如果您计划对多个图像运行 OCR，建议将该包添加到共享库中，以便重复使用同一个引擎实例。

## 第二步：编写 C# OCR 示例

创建或替换 `Program.cs` 为以下代码。它演示了一个 **c# ocr example**，可用于 Aspose.OCR 支持的任何图像格式（JPEG、PNG、BMP 等）。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // ---------------------------------------------------------
        // Step 2.1: Create an OCR engine instance
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // Step 2.2: Choose the language model.
        // The example uses Cyrillic; replace with Language.English,
        // Language.French, etc., to match your source image.
        // ---------------------------------------------------------
        ocrEngine.Language = Language.Cyrillic; // <-- change as needed

        // ---------------------------------------------------------
        // Step 2.3: Load the image you want to process.
        // ImageStream.FromFile automatically reads JPEG, PNG, BMP…
        // ---------------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile("sample_cyrillic.jpg");

        // ---------------------------------------------------------
        // Step 2.4: Run the recognition process.
        // This call downloads the required language model the first
        // time it is used, then performs the OCR.
        // ---------------------------------------------------------
        ocrEngine.Recognize();

        // ---------------------------------------------------------
        // Step 2.5: Retrieve the recognized text.
        // The Text property holds the result of the OCR engine.
        // ---------------------------------------------------------
        string recognizedText = ocrEngine.Text;

        // ---------------------------------------------------------
        // Step 2.6: Display the output.
        // This is where you can further process the string,
        // e.g., save to a database, feed to a search index, etc.
        // ---------------------------------------------------------
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

### 每行代码的重要性

* **`OcrEngine ocrEngine = new OcrEngine();`** – 实例化用于协调整个 OCR 流程的引擎。  
* **`ocrEngine.Language = Language.Cyrillic;`** – 选择语言模型。正确的语言选择在您 **extract text from image** 包含非拉丁字符的文件时能显著提升准确率。  
* **`ocrEngine.Image = ImageStream.FromFile(...);`** – 加载源 JPEG（或任何其他受支持的图像）。此步骤对 **recognize text from jpeg** 至关重要。  
* **`ocrEngine.Recognize();`** – 执行核心 OCR 算法。该方法会阻塞，直至引擎完成处理。  
* **`ocrEngine.Text;`** – 返回纯文本结果，您现在可以 **convert image to text** 用于后续逻辑。

## 第三步：运行程序并验证输出

编译并执行：

```bash
dotnet run
```

如果图像 `sample_cyrillic.jpg` 包含西里尔文短语 “Привет мир”，控制台将显示：

```
=== Recognized Text ===
Привет мир
```

该输出证明您已成功掌握 **how to perform OCR** 和使用 C# **extract text from image**。

## 第四步：常见变体和边缘情况

### 4.1 识别英文或多语言文本

将语言分配替换为相应的枚举：

```csharp
ocrEngine.Language = Language.English;           // English only
ocrEngine.Language = Language.Multilingual;      // Detects many languages automatically
```

### 4.2 从流而非文件处理图像

如果图像通过 HTTP 响应或数据库 BLOB 传入，请使用 `MemoryStream`：

```csharp
using (var ms = new MemoryStream(imageBytes))
{
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
}
```

### 4.3 处理大尺寸或低分辨率图像

大图像会增加内存消耗。您可以在 OCR 前进行降采样：

```csharp
ocrEngine.Config.ImagePreprocessOptions.ScaleFactor = 0.5; // Reduce size by 50%
```

### 4.4 错误处理

将识别调用包装在 try‑catch 块中，以捕获网络或文件访问错误：

```csharp
try
{
    ocrEngine.Recognize();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

## 第五步：后续步骤 – 扩展您的 OCR 工作流

* **批量处理：** 遍历目录中的文件，对每个 JPEG 执行 **convert image to text**。  
* **后处理：** 使用正则表达式清理识别的字符串，在需要 **extract text from image** 表单或发票时非常有用。  
* **与 Azure Cognitive Services 集成：** 将 Aspose.OCR 结果与基于云的 OCR 进行比较，以在复杂布局上获得更高的准确性。  
* **存储结果：** 将提取的文本插入 SQL 数据库或 ElasticSearch 索引，以实现可搜索的文档。

---

## 结论

您现在已经了解如何使用 Aspose.OCR 在 C# 中 **how to perform OCR**，从安装包到显示识别的字符串。此完整的 **c# ocr example** 让您能够 **extract text from image**、**convert image to text**，以及 **recognize text from JPEG**，仅需几行代码。尝试不同的语言模型、图像来源和后处理技术，以适应您的具体使用场景。

---

## 接下来您应该学习什么？

以下教程涵盖与本指南密切相关的主题，构建在本教程展示的技术之上。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [如何在 C# 中使用 OCR – 从图像文件中提取文本](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-files/)
- [使用 Aspose OCR 将图像转换为文本（C#） – 步骤指南](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [如何在 C# 中执行 OCR – 提取文本并写入 JSON](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}