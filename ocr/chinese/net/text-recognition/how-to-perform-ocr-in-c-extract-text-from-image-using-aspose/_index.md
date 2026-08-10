---
category: general
date: 2026-02-16
description: 如何快速在 C# 中执行 OCR —— 学会使用 Aspose OCR 库在几个简单步骤中从图像提取文本。
draft: false
keywords:
- how to perform OCR
- extract text from image
- Aspose OCR C#
- OCR JSON output
- image text extraction
language: zh
og_description: 如何在 C# 中执行 OCR？请按照本分步教程使用 Aspose OCR 从图像中提取文本并获取 JSON 结果。
og_title: 如何在 C# 中进行 OCR – 快速指南
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中执行 OCR – 使用 Aspose OCR 从图像提取文本
url: /zh/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/
---

.

Also need to translate the block of shortcodes at top and bottom, but they are shortcodes, not to be translated. Keep them unchanged.

Now produce final content.

Let's translate:

Original headings:

# How to Perform OCR in C# – Extract Text from Image Using Aspose OCR

Translate: "# 如何在 C# 中执行 OCR – 使用 Aspose OCR 从图像提取文本"

Similarly other headings.

Now bullet points, paragraphs.

Make sure to keep markdown links unchanged. There are none except maybe none. There's a link in image alt text.

Now produce final output.

Let's write translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中执行 OCR – 使用 Aspose OCR 从图像提取文本

是否曾经想过 **如何在 C# 中执行 OCR** 而不抓狂？你并不孤单。许多开发者在需要从扫描的表单、收据或手写笔记中提取文本时都会遇到瓶颈。好消息是？使用 Aspose OCR，你只需几行代码就能 **从图像文件中提取文本**。

在本教程中，我们将演示一个完整、可直接运行的示例，展示如何加载语言模型、提供图像、运行识别引擎并将结果序列化为 JSON。完成后，你将拥有一个可在任何 .NET 项目中复用的代码片段，以及一些针对实际场景的实用技巧。

## 你需要准备的内容

在开始之前，请确保具备以下条件：

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework，但推荐使用 .NET 6+）
- 有效的 Aspose.OCR NuGet 包（`Install-Package Aspose.OCR`）
- 包含待读取文本的图像文件（JPEG、PNG、BMP 等）
- 基本的 C# 开发环境（Visual Studio、Rider 或 VS Code）

基本上就这些——无需额外的 OCR 引擎、无需本地 DLL，只需一个干净的托管库。

## 第一步：创建 OCR 引擎实例 – 如何执行 OCR

首先需要一个 `OcrEngine` 对象。可以把它看作负责繁重计算的大脑。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **为什么这一步很重要：** `OcrEngine` 封装了所有配置选项。没有它，你无法告诉库使用哪种语言或从哪里读取图像。

## 第二步：加载语言模型 – 从图像提取文本

Aspose OCR 附带了多个语言包。对于大多数英文文档，你可以加载内置的英文模型。

```csharp
// Load the English language model
ocrEngine.LoadLanguage(LanguageModel.English);
```

> **专业提示：** 如果需要识别法语、德语或自定义语言，请将 `LanguageModel.English` 替换为相应的枚举值，或加载自定义模型文件。

## 第三步：提供待处理的图像 – 如何执行 OCR

现在将引擎指向你想读取的文件。`ImageStream.FromFile` 辅助方法会把图像读取为 OCR 引擎能够理解的格式。

```csharp
// Supply the image (replace the path with your own file location)
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.jpg");
```

> **边缘情况：** 大图像（>5 MB）可能会导致处理变慢。建议在喂给引擎之前先对其进行缩放或压缩。

## 第四步：运行识别 – 从图像提取文本

所有准备就绪后，就可以执行 OCR 操作了。`Recognize` 方法返回一个 `OcrResult` 对象，里面包含文本、边界框以及置信度分数。

```csharp
// Perform OCR and capture the result
OcrResult ocrResult = ocrEngine.Recognize();
```

> **底层原理是什么？** 引擎运行一个在数百万字符上训练的神经网络，然后将每个检测到的字形映射为 Unicode 文本。

## 第五步：将结果转换为 JSON – 如何执行 OCR

大多数现代 API 都使用 JSON，因此我们将结果序列化。`ToJson` 扩展方法会返回格式良好的字符串。

```csharp
// Serialize the OCR result to JSON
string jsonResult = ocrResult.ToJson();
```

典型的 JSON 负载如下（为简洁起见已截断）：

```json
{
  "Text": "Invoice #12345\nDate: 01/02/2026\nTotal: $250.00",
  "Words": [
    {
      "Value": "Invoice",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 80, "Height": 20 },
      "Confidence": 0.98
    },
    // ... more words ...
  ]
}
```

> **为什么使用 JSON？** 它与语言无关，易于记录，并且非常适合发送到下游服务，如 Elasticsearch 或 REST API。

## 第六步：输出 JSON – 从图像提取文本

最后，将 JSON 写入控制台（或文件、数据库——随你决定）。

```csharp
// Print the JSON result to the console
Console.WriteLine(jsonResult);
```

运行程序后应显示完整的 JSON 结构，确认你已经成功 **从图像中提取文本**。

## 完整可运行示例

下面是可以直接复制粘贴到新控制台项目中的完整代码。没有缺失的部分——所需的一切都在这里。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Step 2: Load the English language model for recognition
            ocrEngine.LoadLanguage(LanguageModel.English);

            // Step 3: Provide the image to be processed
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.jpg");

            // Step 4: Perform OCR on the image
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 5: Convert the recognition result to JSON (includes text, bounding boxes, confidence scores)
            string jsonResult = ocrResult.ToJson();

            // Step 6: Output the JSON result
            Console.WriteLine(jsonResult);
        }
    }
}
```

> **预期输出：** 包含识别文本、每个单词的边界框以及置信度值的 JSON 字符串。如果图像清晰且语言模型匹配，置信度通常会高于 0.90。

## 常见问题与注意事项

- **如果图像被旋转怎么办？**  
  Aspose OCR 能自动检测方向，但为了获得最佳效果，你可以在将图像传递给引擎之前使用 `System.Drawing` 或 `ImageSharp` 进行预旋转。

- **能直接处理 PDF 吗？**  
  不能直接。需要先将每页 PDF 转为图像（例如使用 Aspose.PDF），再将这些图像喂给 OCR 引擎。

- **如何处理多页表单？**  
  对每页图像循环执行相同步骤，并将 JSON 结果聚合到一个集合中。

- **有没有办法只输出纯文本？**  
  有——如果只需要连贯的字符串，请使用 `ocrResult.Text` 属性而不是 `ToJson()`。

## 生产环境 OCR 的专业技巧

1. **缓存语言模型** – 加载模型的开销不大，但如果每秒处理数百张图像，建议保持单个 `OcrEngine` 实例而不是每次都重新创建。
2. **调节置信度阈值** – 过滤掉 `Confidence < 0.80` 的单词，以降低噪声。
3. **批量处理** – 对于大规模工作负载，可将图像路径加入队列，并使用 `Task.Run` 异步处理。
4. **日志记录** – 将原始 JSON 与原始图像一起存储，以便审计；在调试识别错误时极其有价值。

## 结论

现在，你已经掌握了在 C# 中使用 Aspose OCR 库 **执行 OCR** 并 **从图像中提取文本** 的完整端到端解决方案。示例涵盖了引擎创建、语言加载、图像输入、识别、JSON 序列化以及输出——全部在一个可运行的程序中实现。

接下来可以尝试将英文模型换成其他语言，实验不同的图像格式，或将 JSON 负载集成到搜索索引中。只要有这些构件，你就能应对任何文本提取挑战。

祝编码愉快，愿你的 OCR 结果始终精准！

![演示如何使用 Aspose OCR 库在 C# 中执行 OCR 的示意图](https://example.com/ocr-diagram.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}