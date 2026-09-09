---
category: general
date: 2026-01-09
description: 使用 Aspose OCR 快速提取 PNG 文本。了解如何读取图像文字、提升 OCR 准确率，并在 C# 中获得干净的结果。
draft: false
keywords:
- extract text from png
- read image text
- improve ocr accuracy
- extract text from image
- aspose ocr tutorial
language: zh
og_description: 使用 Aspose OCR 快速从 PNG 提取文本。了解如何读取图像文字、提升 OCR 准确率，并在 C# 中获得干净的结果。
og_title: 从 PNG 提取文本 – 完整的 Aspose OCR 教程
tags:
- Aspose OCR
- C#
- Image Processing
title: 从 PNG 中提取文本 – 完整的 Aspose OCR 教程
url: /zh/net/text-recognition/extract-text-from-png-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 PNG 提取文本 – 完整 Aspose OCR 教程

是否曾经需要**从 PNG 中提取文本**但结果却充斥着乱码？你并不孤单。在许多真实项目中——发票、收据或扫描表单——OCR 输出的质量可能决定自动化流水线的成败。

在本指南中，我们将向你展示一种**逐步**使用 Aspose OCR 读取图像文本的方法，加入自定义词典以**提升 OCR 准确率**，清理噪声，最终打印整洁的字符串。完成后，你将拥有一个可直接运行的 C# 控制台应用，可靠地从 PNG 图像中提取文本。

> **你将收获**  
> * 一个完整、可运行的代码示例。  
> * 对自定义词典重要性的理解。  
> * 处理低对比度扫描等边缘情况的技巧。  

## 前置条件

- .NET 6 SDK 或更高版本（代码面向 .NET 6，但 .NET 5 也可运行）。  
- Visual Studio 2022 或任意你喜欢的编辑器。  
- 你想要处理的**PNG**图像，例如 `invoice.png`。  
- **Aspose.OCR** NuGet 包（`dotnet add package Aspose.OCR`）。  

无需额外的配置文件；所有内容都在单个 `.cs` 文件中。

## 第一步 – 安装并引用 Aspose OCR

首先，将库拉入项目。在解决方案文件夹的终端中运行：

```bash
dotnet add package Aspose.OCR
```

这行命令会获取最新的稳定版本（截至 2026 年 1 月，版本 23.9）。该包包含我们在整个教程中使用的 `OcrEngine` 类。

## 第二步 – 初始化 OCR 引擎

创建 `OcrEngine` 实例是基础。可以把它想象成打开了一台准备解释像素的扫描仪。

```csharp
using Aspose.OCR;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **专业提示**：如果你计划在循环中处理大量图像，请复用同一个 `OcrEngine` 实例。它会缓存内部资源，从而加快后续调用。

## 第三步 – 使用自定义词典提升准确率

开箱即用的 OCR 已经相当不错，但在面对诸如 “Aspose”、 “OCR” 或 “SDK” 之类的领域专用词时仍可能出错。将这些词加入**自定义词典**，告诉引擎这些字符串是有效的，从而降低误识别。

```csharp
// Define domain‑specific terms that the engine should recognize
ocrEngine.CustomDictionary = new HashSet<string>
{
    "Aspose",
    "OCR",
    "SDK",
    "invoice"
};
```

### 为什么自定义词典有帮助

- OCR 背后的**统计模型**对常见语言模式权重很高。罕见词的概率低，可能被相似字符替代。  
- 明确列出这些词后，你就覆盖了模型的猜测。  
- 对于包含产品代码、缩写或品牌名称的**读取图像文本**场景尤为实用。

## 第四步 – 从 PNG 文件识别文本

现在将图像路径传给引擎。`RecognizeImage` 方法返回的原始字符串仍可能包含引擎无法映射的未知标记（例如 “#@!”）。

```csharp
// Path to the PNG you want to process
string imagePath = @"YOUR_DIRECTORY/invoice.png";

// Perform OCR
string rawText = ocrEngine.RecognizeImage(imagePath);
```

> **边缘情况**：如果文件未找到，`RecognizeImage` 会抛出 `FileNotFoundException`。在生产代码中请使用 try‑catch 包裹调用。

## 第五步 – 使用 `CleanText` 清理结果

Aspose OCR 附带的帮助方法会剔除它标记为“未知”的字符。这一步对**从图像中提取文本**的项目至关重要，因为下游解析器通常只接受字母数字和基本标点。

```csharp
// Remove unknown tokens and extra whitespace
string cleanedText = ocrEngine.CleanText(rawText);
```

`CleanText` 方法还会规范化换行符，使输出安全地存入数据库或传递给其他服务。

## 第六步 – 输出清理后的文本

最后，显示或保存结果。在控制台应用中，`Console.WriteLine` 就能完成任务。

```csharp
Console.WriteLine("=== Cleaned OCR Output ===");
Console.WriteLine(cleanedText);
```

运行程序后，你应该会看到一段整洁的文本，内容与 `invoice.png` 的实际文字相匹配。如果图像中出现 “Aspose”，自定义词典会确保它正确显示，而不是类似 “A5p0se” 的错误。

## 完整工作示例

将所有内容整合在一起，下面是可以直接复制到新控制台项目中的完整 `Program.cs`：

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add domain‑specific terms to improve OCR accuracy
        ocrEngine.CustomDictionary = new HashSet<string>
        {
            "Aspose",
            "OCR",
            "SDK",
            "invoice"
        };

        // 3️⃣ Path to your PNG file (adjust as needed)
        string imagePath = @"YOUR_DIRECTORY/invoice.png";

        try
        {
            // 4️⃣ Recognize raw text from the image
            string rawText = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Clean up unknown tokens
            string cleanedText = ocrEngine.CleanText(rawText);

            // 6️⃣ Show the result
            Console.WriteLine("=== Cleaned OCR Output ===");
            Console.WriteLine(cleanedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

**预期输出**（假设 PNG 包含一张简单的发票）：

```
=== Cleaned OCR Output ===
Invoice #12345
Date: 01/08/2026
Total: $1,250.00
Thank you for your business!
```

如果看到杂乱的符号，请检查图像质量或在自定义词典中添加更多词条。

## 额外技巧：处理低质量扫描

有时 PNG 以 72 dpi 扫描或存在严重压缩伪影。以下是几种**提升 OCR 准确率**的快速技巧，无需离开 C#：

1. 使用 `SixLabors.ImageSharp` 等库**预处理图像**——提升对比度、转换为灰度或轻度模糊以降低噪声。  
2. 在 `OcrEngine` 上**设置 `Resolution` 属性**（例如 `ocrEngine.Resolution = 300;`），告诉引擎将图像视为更高分辨率。  
3. **启用语言包**，如果处理非英文文本（`ocrEngine.Language = Language.English;`）。

上述三种方法都可以在调用 `RecognizeImage` 之前加入。

## 常见问题

- **这能用于其他图像格式吗？**  
  能。`RecognizeImage` 支持 JPEG、BMP、TIFF，甚至 PDF（作为图像容器）。使用步骤相同。

- **我能一次性从文件夹中的多个 PNG 提取文本吗？**  
  完全可以。将核心逻辑包装在 `foreach (var file in Directory.GetFiles(folder, "*.png"))` 循环中，并将每个结果存入列表或写入单独文件。

- **如果需要获取文本坐标怎么办？**  
  Aspose OCR 还提供包含边界框的 `OcrResult` 对象。使用 `ocrEngine.RecognizeImageToResult(imagePath)` 可实现该高级场景。

## 结论

我们已经完整演示了使用 Aspose OCR **从 PNG 文件中提取文本**的**端到端**解决方案。通过初始化引擎、加入**自定义词典**、清理原始输出并处理常见坑点，你可以在自己的 C# 应用中可靠地**读取图像文本**并**提升 OCR 准确率**。

准备好下一步了吗？尝试将 PNG 换成扫描收据，向词典中添加更多领域专用词，或将输出集成到数据库实现自动化发票处理。当 Aspose OCR 与 .NET 丰富生态结合时，可能性无限。

祝编码愉快，愿你的 OCR 永远精准无误！

![从 PNG 提取文本示例](/images/extract-text-from-png.png "从 PNG 提取文本 – Aspose OCR 演示")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}