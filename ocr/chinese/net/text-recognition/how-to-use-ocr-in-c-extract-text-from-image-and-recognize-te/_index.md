---
category: general
date: 2026-02-13
description: 如何在 C# 中使用 OCR 从图像中提取文本，识别照片或 JPG 中的文字，并在无网络情况下对图像进行 OCR。
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: zh
og_description: 如何在 C# 中使用 OCR 从图像中提取文本，识别照片中的文字，并提供完整可运行的示例来对图像进行 OCR。
og_title: 如何在 C# 中使用 OCR – 从图像中提取文本
tags:
- OCR
- C#
- Image Processing
title: 如何在 C# 中使用 OCR – 从图像提取文本并识别照片中的文字
url: /zh/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 从图像中提取文本并识别照片中的文字

是否曾经想过 **如何使用 OCR** 从截图、扫描的收据或手机随手拍的照片中提取文字？你并不是唯一有这种需求的人。在许多实际应用中，我们需要将图片转换为可搜索的文本，而在本地完成——无需依赖不稳定的网络连接——常常像解谜一样。

因此本指南将一步步演示如何使用 C# OCR 引擎 **从图像文件中提取文本**，并涵盖 **从照片中识别文字**、**从 JPG 中识别文字** 以及 **在本地磁盘上的图像文件上运行 OCR**。阅读完毕后，你将拥有一个完整的、可直接复制粘贴的程序，开箱即用。

## 你将学到

- 如何为简体中文（或任意你接入的语言）配置 OCR 引擎。  
- 从本地文件夹 **加载资源** 的完整代码——无需网络请求。  
- 如何 **从照片文件**（如 JPEG、PNG、BMP）中 **识别文字**。  
- 处理常见边缘情况的技巧，如模型文件缺失或不支持的图像格式。  
- 一个完整可运行的示例，直接放入 Visual Studio 即可看到结果。

### 前置条件

- .NET 6.0 或更高（本示例使用的 API 目标为 .NET Standard 2.0，旧版本同样可用）。  
- 对 C# 和 Visual Studio（或任意 IDE）有基本了解。  
- 你所使用的 OCR 库（示例代码假设有一个随语言模型一起提供的虚构 `OcrEngine` 类）。  
- 包含所需语言模型文件的文件夹——可以把它看作引擎读取中文字符的“大脑”。

> **Pro tip:** 如果还没有中文模型文件，请先从供应商网站下载一次，并放置在类似 `C:\OcrResources` 的文件夹中。之后引擎再也不需要联网。

---

![Diagram showing OCR process on a photo](path/to/ocr-diagram.png "Diagram showing OCR process on a photo")

## 如何使用 OCR：设置引擎

首先需要创建一个 OCR 引擎实例，并为其配置目标语言。本教程使用 **简体中文**，如果想换成 `OcrLanguage.English`（或其他枚举值）只需一行代码即可。

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**为什么这很重要：**  
设置 `Language` 属性告诉引擎应当识别哪套字符集。`ResourceFolder` 则是引擎查找神经网络权重和语言词典的路径——相当于大脑的记忆库。如果指向错误的文件夹，引擎会抛出 `FileNotFoundException`，导致程序卡死。

## 从图像中提取文本 – 加载资源

在引擎真正读取图像之前，需要先把模型文件加载到内存。此步骤 **至关重要**，因为它避免了每次处理图像时都进行网络请求。

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**可能出现的问题？**  
如果文件夹路径错误或模型文件损坏，`LoadResources()` 会抛出异常。上面的 `try/catch` 代码演示了优雅的错误处理方式——在生产环境中经常需要。

## 从照片中识别文字 – 运行 OCR

现在进入有趣的环节：将图像文件喂给引擎并获取识别结果。这正是 **在图像上运行 OCR** 场景的核心，无论图像是 JPEG、PNG 还是 BMP。

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

`RecognizeImage` 方法返回一个 `RecognitionResult`（或你 SDK 中对应的类型），通常包含：

- `Text` – 纯文本转录。  
- `Confidence` – 表示引擎对每行文字置信度的数值分数。  
- `BoundingBoxes` – 可选的每个词在图片上的坐标。

**为什么要关注置信度：**  
如果你在构建数据录入自动化工具，可以设定阈值（例如 0.85），对低置信度的行让用户确认。这样可以显著提升整体准确率。

## 从 JPG 中识别文字 – 处理不同格式

很多开发者误以为 OCR 只能处理 PNG，实际上现代引擎对 **JPG** 文件同样支持良好。唯一需要注意的是 JPEG 压缩可能产生的伪影，会干扰模型识别。

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

如果没有 `DenoiseAndDeskew` 辅助函数，许多库（例如 OpenCvSharp）都提供相应功能。关键点在于：**在对扫描件或手机拍摄的图片进行少量清理后再运行 OCR**。

## 在图像上运行 OCR – 小技巧、边缘情况与最佳实践

### 1. 内存管理
加载大型语言模型可能占用数百 MB。使用完毕后请释放引擎：

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. 批量处理
如果需要一次处理 dozens 张照片，先加载资源一次，然后在循环中调用：

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. 多语言场景
可以通过重新赋值 `ocrEngine.Language` 并再次调用 `LoadResources()` 来切换语言。但要注意额外的加载时间。

### 4. 处理空结果
有时引擎会返回空字符串，通常意味着图像过于模糊或文字颜色与背景融合。快速检查方式：

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. 安全考虑
绝不要直接将用户上传的文件喂给 OCR 引擎而不做验证。至少要检查文件扩展名和大小，并考虑进行恶意软件扫描。

---

## 完整可运行示例

下面是一段完整的、可直接复制到新 Console App 项目中的代码。它演示了 **如何使用 OCR**、**从图像中提取文本**、**从照片中识别文字**、**从 JPG 中识别文字** 以及 **在图像上运行 OCR** 的全部流程。

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**预期输出（示例）：**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

实际输出会根据图像内容不同而有所差异，但你应该会在控制台看到一段 Unicode 文本以及对应的置信度百分比。

---

## 结论

我们已经从头到尾演示了 **如何在 C# 中使用 OCR**——配置引擎、加载语言资源，最后 **从照片或 JPG 文件中识别文字**，且全程不依赖网络。按照上述步骤，你可以 **从图像文件中提取文本**、**在图像上运行 OCR**，并规避新手常犯的坑。

准备好迎接下一个挑战了吗？尝试将 PDF 页面转换为图像后喂给引擎，或换用其他语言包观察置信度的变化。你可能

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}