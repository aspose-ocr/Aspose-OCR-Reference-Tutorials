---
category: general
date: 2026-04-04
description: 如何快速安全地使用 OCR。学习从图像提取文本、将 DJVU 转换为文本，以及使用 Aspose.OCR 加载图像进行 OCR。
draft: false
keywords:
- how to use OCR
- extract text from image
- convert djvu to text
- load image for OCR
- extract text from djvu
language: zh
og_description: 如何在 C# 中使用 OCR 从图像文件和 DJVU 文档中提取文本。一步一步的教程，附完整代码。
og_title: 如何在 C# 中使用 OCR – 完整指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 OCR——从图像和 DJVU 文件中提取文本
url: /zh/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 从图像和 DJVU 文件提取文本

是否曾经想过 **如何使用 OCR** 从扫描页中提取文字，而不必手动输入？你并不是唯一有此需求的人。在许多项目中——无论是数字化旧书还是从收据中提取数据——从图像获取文本都是日常痛点。好消息是？使用 Aspose.OCR，你只需几行代码，即使源文件是 DJVU 也能轻松实现。

在本指南中，我们将逐步讲解 **从图像文件提取文本**、**加载图像进行 OCR**，以及使用 C# **将 DJVU 转换为文本** 的全部内容。阅读完毕后，你将拥有一个可直接运行的控制台应用程序，能够将识别的文本直接打印到控制台。没有神秘的步骤，也不需要额外的依赖，仅使用纯 C# 和 Aspose。

## 你将学到

- 如何安装并引用 Aspose.OCR 库。
- 加载图像进行 OCR 的完整代码，无论是 PNG、JPEG 还是 DJVU 页面。
- 如何调用引擎并获取结果。
- 处理大文档的技巧以及常见陷阱。
- 一个完整、可运行的示例，直接复制粘贴到 Visual Studio 中使用。

> **先决条件：** .NET 6.0 或更高版本，以及有效的 Aspose.OCR 许可证（或免费试用版）。如果尚未获取库，可使用 `dotnet add package Aspose.OCR` 从 NuGet 获取。

---

## 如何在 C# 中使用 Aspose 的 OCR

这一步是核心，真正回答 **如何在 C# 项目中使用 OCR** 的问题。下面的代码是完整程序；你可以将其粘贴到新的控制台应用并按 F5 运行。

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance.
            var ocrEngine = new OcrEngine();

            // Step 2: Load the image (or DJVU page) you want to analyze.
            // Replace the path with your own file location.
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book-page.djvu");

            // Step 3: Run the recognition process.
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 4: Output the extracted text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**为什么这样可行：**  
- `OcrEngine` 是入口点；它封装了图像预处理、语言检测和字符分类等繁重工作。  
- `ImageStream.FromFile` 能处理多种格式，包括 DJVU，这意味着你可以 **将 DJVU 转换为文本**，而无需额外的转换步骤。  
- `Recognize()` 返回一个 `OcrResult` 对象，其中包含纯文本输出、置信度分数，甚至在需要时的边界框信息。

运行程序后会输出类似如下内容：

```
=== OCR Result ===
In the beginning God created the heavens and the earth.
```

这就是你的第一次成功 **从 DJVU 提取文本** 操作。

![如何使用 OCR 示例](/images/ocr-demo.png "显示在 C# 控制台应用中使用 OCR 的截图")

*替代文字：“如何使用 OCR” 控制台输出截图。*

---

## 加载图像进行 OCR

在引擎能够读取任何内容之前，你必须 **正确加载图像进行 OCR**。Aspose 开箱即支持大多数光栅格式，但以下几点技巧可以让识别更顺畅：

- **将大图像缩放**至最长边不超过 2000 px。过大的文件会增加内存占用并可能减慢引擎速度。  
- **将彩色图像转换为灰度**，如果你注意到背景噪声较多。使用 `ocrEngine.Image = ImageStream.FromFile(path).ConvertToGrayscale();`。  
- **手动设置 DPI** 以应对低分辨率扫描（`ocrEngine.Image.DpiX = 300; ocrEngine.Image.DpiY = 300;`）。

这些调整是可选的，但在 **从图像文件提取文本**（如扫描收据）时，常能提升准确率。

---

## 从图像提取文本 – 最佳实践

当处理常见图像格式（PNG、JPEG、BMP）时，步骤保持不变，但你可以对引擎进行微调：

```csharp
ocrEngine.Image = ImageStream.FromFile("sample.png");

// Optional: enable language packs for better accuracy.
ocrEngine.Language = Language.English;

// Optional: set recognition mode to auto.
ocrEngine.RecognitionMode = RecognitionMode.Auto;
```

- **语言选择** 很重要。如果处理多语言文档，请设置 `ocrEngine.Language = Language.Multilingual;`。  
- **RecognitionMode** 可以是 `Auto`、`Fast` 或 `Accurate`。`Accurate` 能提供更高质量的识别，但速度较慢——适用于归档任务。

---

## 将 DJVU 转换为文本 – 处理多页文件

DJVU 文件通常包含多页。Aspose 将每页视为独立的图像流，你可以遍历它们：

```csharp
using Aspose.OCR;
using System.Collections.Generic;

var ocrEngine = new OcrEngine();
List<string> allPagesText = new List<string>();

int pageCount = ImageStream.GetPageCount("book.djvu");
for (int i = 1; i <= pageCount; i++)
{
    ocrEngine.Image = ImageStream.FromFile("book.djvu", i); // Load page i
    OcrResult result = ocrEngine.Recognize();
    allPagesText.Add(result.Text);
}

// Combine all pages into a single string.
string fullText = string.Join("\n--- Page Break ---\n", allPagesText);
Console.WriteLine(fullText);
```

**为什么要循环？**  
DJVU 文件本质上是一堆图像。通过遍历每一页，你可以 **按顺序从 DJVU 提取文本**，保持原始文档的顺序。

---

## 常见陷阱与专业提示

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| **乱码字符** | DPI 过低或压缩过重 | 放大图像，设置 `ocrEngine.Image.DpiX/Y = 300` |
| **处理速度慢** | 在大文件上使用 `Accurate` 模式 | 对批量任务切换为 `Fast` 模式 |
| **缺少语言支持** | 默认语言仅为英文 | 加载额外语言包（`ocrEngine.Language = Language.Spanish;`） |
| **内存溢出** | 一次加载过多高分辨率页面 | 逐页处理并释放资源（`ocrEngine.Dispose();`） |

一个快速 **专业提示**：在完成页面处理后务必调用 `ocrEngine.Dispose()`。它会释放本机资源，防止长期运行的服务出现细微的内存泄漏。

---

## 测试你的 OCR 流程

为了验证一切正常，尝试以下简单检查：

1. **打印识别字符串的长度**：`Console.WriteLine($"Characters recognized: {ocrResult.Text.Length}");`  
2. **与已知文本进行比对**，如果有基准文本，可使用简单的 diff 库。  
3. **记录置信度分数**（`ocrResult.Confidence`），自动发现低质量页面。

如果置信度持续低于 0.7，请回顾前面提到的图像预处理步骤。

---

## 后续步骤

既然已经掌握 **如何使用 OCR**，可以考虑扩展工作流：

- **批量处理**：将循环包装在 `Parallel.ForEach` 中，以加速大批量文件。  
- **导出为 PDF**：使用 Aspose.PDF 将识别文本嵌入为隐藏层，生成可搜索的 PDF。  
- **与 AI 集成**：将提取的字符串输入语言模型，进行摘要或实体抽取。

所有这些都基于你刚刚搭建的基础，每一步都受益于我们讨论的 **从图像提取文本** 原则。

---

## 结论

我们深入探讨了在 C# 中使用 Aspose **如何使用 OCR**，涵盖了从加载图像、**从图像提取文本**、处理 **DJVU** 文件到常见问题排查的全部内容。上面的完整可运行示例为你提供了坚实的起点，文中散布的技巧也能帮助你将解决方案适配到真实项目中。

动手尝试，针对你的特定文档微调设置，你很快就能将扫描页转换为可搜索的文本。有什么问题或遇到顽固文件无法处理？欢迎留言——祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}