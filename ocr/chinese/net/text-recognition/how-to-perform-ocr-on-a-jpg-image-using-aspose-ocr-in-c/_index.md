---
category: general
date: 2026-11-17
description: 如何在 C# 中对 JPG 图像进行 OCR——学习从图像中提取文本、提升 OCR 准确率，并使用 Aspose OCR 加载图像进行 OCR。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- convert JPG to text
- improve OCR accuracy
- load image for OCR
language: zh
lastmod: 2026-11-17
og_description: 如何在 C# 中对 JPG 图像执行 OCR，并使用 Aspose OCR 高精度提取图像中的文本。请跟随完整的逐步教程。
og_image_alt: Screenshot showing how to perform OCR with Aspose OCR in C#
og_title: 使用 Aspose OCR 对 JPG 图像进行 OCR 的 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: How to perform OCR on a JPG image in C# – learn to extract text from
    image, improve OCR accuracy, and load image for OCR with Aspose OCR.
  headline: How to perform OCR on a JPG image using Aspose OCR in C#
  type: TechArticle
- description: How to perform OCR on a JPG image in C# – learn to extract text from
    image, improve OCR accuracy, and load image for OCR with Aspose OCR.
  name: How to perform OCR on a JPG image using Aspose OCR in C#
  steps:
  - name: Load image for OCR
    text: The first operation is to give the OCR engine a bitmap to analyze. Aspose
      OCR accepts an `ImageStream` created from a file path, a byte array, or a stream.
      Using a file path is the simplest approach for a quick demo.
  - name: Improve OCR accuracy (optional language hint)
    text: If your image contains non‑Latin characters, specifying the language dramatically
      raises recognition quality. Aspose OCR ships with built‑in language packs such
      as `Cyrillic`, `Arabic`, `ChineseSimplified`, etc.
  - name: Run the OCR process
    text: Calling `Process()` performs the heavy lifting. It returns `true` when the
      engine successfully extracts text; otherwise, you can inspect `ocrEngine.LastError`.
  - name: Extract text from image
    text: When `Process()` succeeds, the recognized plain‑text result is available
      through the `Text` property.
  - name: Display the extracted text
    text: For a console demo, simply write the string to `stdout`. In a real application
      you might store it in a database, feed it to a search index, or pass it to a
      translation service.
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 Aspose OCR 对 JPG 图像进行 OCR
url: /zh/net/text-recognition/how-to-perform-ocr-on-a-jpg-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 在 C# 中对 JPG 图像执行 OCR 的方法

如果您需要了解 **如何执行 OCR** 对图片文件的操作，本指南提供了一个可直接运行的解决方案。您将看到如何 **加载图像进行 OCR**、运行引擎以及 **从图像中提取文本**，且无需离开 IDE。

本教程涵盖了使用 Aspose OCR 将 **JPG 转换为文本** 所需的每一步，解释了如何为西里尔文或其他语言 **提高 OCR 准确率**，并展示了如何在控制台应用程序中显示结果。无需外部服务；所有操作均在本地的 .NET 6 或更高版本上运行。

## 您将学习的内容

* 如何创建 OCR 引擎实例并 **加载图像进行 OCR**。  
* 哪个属性用于控制语言选择以 **提高 OCR 准确率**。  
* 如何安全地运行引擎并 **从图像中提取文本**。  
* 如何 **将 JPG 转换为文本** 并将输出打印到控制台。  
* 常见陷阱以及可靠 OCR 结果的最佳实践提示。

**先决条件**

* .NET 6 SDK（或任何支持 C# 10 的 .NET 版本）。  
* Aspose.OCR NuGet 包（`dotnet add package Aspose.OCR`）。  
* 您想要读取的 JPG 文件，例如放在已知文件夹中的 `sample.jpg`。

---

## 如何执行 OCR – 步骤指南

以下章节将过程拆分为离散且可复用的步骤。每一步都包含完整的代码片段、简短说明，以及在需要时帮助您 **提高 OCR 准确率** 的提示。

### 步骤 1：加载图像进行 OCR

第一步是为 OCR 引擎提供一个位图进行分析。Aspose OCR 接受由文件路径、字节数组或流创建的 `ImageStream`。使用文件路径是快速演示的最简方法。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Load the JPG file – this is the “load image for OCR” step
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\sample.jpg");
```

**为什么这很重要：**  
正确加载图像可确保引擎使用您想要处理的精确像素数据。提供损坏或不受支持的格式会导致 `Process()` 返回 `false`。

### 步骤 2：提高 OCR 准确率（可选语言提示）

如果图像包含非拉丁字符，指定语言可以显著提升识别质量。Aspose OCR 附带了内置语言包，如 `Cyrillic`、`Arabic`、`ChineseSimplified` 等。

```csharp
        // Optional: set the language to Cyrillic to boost recognition for Russian text
        ocrEngine.Language = Language.Cyrillic;
```

**提示：**  
仅在明确知道文字所属脚本时才设置语言；保持默认 (`English`) 可能导致外观相似但属于其他字母表的字符被误识别。

### 步骤 3：运行 OCR 过程

调用 `Process()` 执行核心工作。当引擎成功提取文本时返回 `true`；否则，您可以检查 `ocrEngine.LastError`。

```csharp
        // Execute the OCR operation
        if (!ocrEngine.Process())
        {
            Console.WriteLine($"OCR failed: {ocrEngine.LastError}");
            return;
        }
```

**为什么这很重要：**  
检查返回值可防止您处理空字符串，并为调试提供明确的错误路径。

### 步骤 4：从图像中提取文本

当 `Process()` 成功时，识别得到的纯文本结果可通过 `Text` 属性获取。

```csharp
        // Retrieve the recognized plain‑text result
        string recognizedText = ocrEngine.Text;
```

至此，您已成功 **将 JPG 转换为文本**。该字符串可能包含换行符、标点和空白字符，完全按照引擎检测到的方式呈现。

### 步骤 5：显示提取的文本

对于控制台演示，只需将字符串写入 `stdout`。在实际应用中，您可能会将其存入数据库、写入搜索索引，或传递给翻译服务。

```csharp
        // Show the OCR result
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**完整程序**

将所有部分组合在一起即可得到一个可复制、粘贴并运行的独立应用程序：

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        var ocrEngine = new OcrEngine();

        // Load the JPG file – this is the “load image for OCR” step
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\sample.jpg");

        // Optional: improve OCR accuracy by specifying the language
        ocrEngine.Language = Language.Cyrillic; // remove or change for other scripts

        // Run the OCR engine
        if (!ocrEngine.Process())
        {
            Console.WriteLine($"OCR failed: {ocrEngine.LastError}");
            return;
        }

        // Extract and display the recognized text
        string recognizedText = ocrEngine.Text;
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**预期输出**

如果 `sample.jpg` 包含短语 “Привет мир”（俄语的 Hello world），控制台将输出：

```
=== OCR Result ===
Привет мир
```

如果图像中是英文文本，输出将匹配该语言。将 `ocrEngine.Language` 改为 `Language.English`（或省略此行）也会得到相似的结果。

---

## 常见陷阱与最佳实践提示

| 问题 | 产生原因 | 解决方法 |
|------|----------|----------|
| 模糊或低分辨率的 JPG | OCR 引擎需要清晰的边缘来区分字符。 | 使用至少 300 dpi 的源图像；可选地进行图像预处理（对比度、二值化）。 |
| 语言设置错误 | 引擎尝试将字符匹配到默认的英文字符集。 | 将 `ocrEngine.Language` 设置为正确的脚本，或保持未设置以进行多语言检测。 |
| 文件路径过长 | 如果路径超过操作系统限制，`ImageStream.FromFile` 会抛出异常。 | 将图像文件夹放在项目根目录附近或使用相对路径。 |
| 缺少 NuGet 包 | 编译时出现 “type or namespace name ‘Aspose’ could not be found” 错误。 | 在构建前运行 `dotnet add package Aspose.OCR`。 |

**专业提示：**  
如果需要批量处理大量图像，请复用同一个 `OcrEngine` 实例，仅在调用之间更换 `ocrEngine.Image`。这可以减少内存分配并加快处理速度。

---

## 扩展解决方案

既然您已经了解了对单个 JPG **如何执行 OCR**，可以进一步探索以下相关主题：

* 通过先将 PDF 的每页加载为图像来 **从图像中提取文本**。  
* 在后台服务中使用 `Task.Run` 并行化来 **将 JPG 转换为文本**。  
* 通过自定义词典或训练新语言模型进一步 **提高 OCR 准确率**。  
* 当图片来自 Web API 而非文件系统时，从 `MemoryStream` **加载图像进行 OCR**。

这些扩展都基于上述核心步骤，只需进行最小的修改即可复用代码。

---

## 结论

您现在拥有一个完整、可投入生产的示例，展示了使用 Aspose OCR 在 C# 中对 JPG 图像 **执行 OCR**、**从图像中提取文本**以及 **将 JPG 转换为文本** 的方法。通过可选的语言设置，您可以 **提高 OCR 准确率**，而步骤的清晰划分使代码易于维护和扩展。

尝试更换语言、使用不同的图像，或将结果集成到更大的工作流中。同样的模式同样适用于 PNG、BMP 或 TIFF 文件，几乎可以处理任何包含可读文本的光栅图像。

祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术密切相关的主题，构建在上述技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [如何使用 Aspose.OCR for .NET 进行图像文本提取 – OCR 优化](/ocr/english/net/ocr-optimization/)
- [如何使用 Aspose.OCR for .NET 提取图像文本](/ocr/english/net/text-recognition/get-recognition-result/)
- [如何使用 Aspose OCR 从流进行图像转文本转换](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}