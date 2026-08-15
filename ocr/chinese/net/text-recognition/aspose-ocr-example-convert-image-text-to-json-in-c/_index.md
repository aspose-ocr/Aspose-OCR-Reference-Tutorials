---
category: general
date: 2026-04-17
description: 学习 Aspose OCR 示例，使用 C# 读取图像文件、提取图像文本并写入 JSON 文件。完整的逐步 C# OCR 教程。
draft: false
keywords:
- aspose ocr example
- write json file c#
- read image file c#
- extract text image c#
- c# ocr tutorial
language: zh
og_description: 掌握 Aspose OCR 示例，使用 C# 读取图像、提取文本并写入 JSON 文件。请跟随本简洁的 C# OCR 教程。
og_title: Aspose OCR 示例 – 将图像文本转换为 JSON（C#）
tags:
- Aspose
- OCR
- C#
- JSON
title: aspose OCR 示例 – 在 C# 中将图像文本转换为 JSON
url: /zh/net/text-recognition/aspose-ocr-example-convert-image-text-to-json-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# aspose ocr 示例 – 将图像文本转换为 JSON（C#）

是否曾需要一个 **aspose ocr 示例**，不仅能读取图像，还能输出整洁的 JSON 供后续处理？你并不孤单。在许多项目中——发票自动化、收据扫描，甚至简单的文档归档——开发者都会遇到同样的难题：“如何把 OCR 结果转换成我的 API 喜欢的格式？”  

好消息是？使用 Aspose.OCR 只需几行代码，我会一步步展示给你。阅读完本指南后，你将掌握 **read image file C#**、**extract text image C#** 和 **write JSON file C#**——全部封装在一个简洁、可复用的 C# OCR 教程中。

## 需要的环境

- .NET 6.0 或更高（代码同样可以在 .NET Core 上编译）  
- Aspose.OCR for .NET NuGet 包（`Install-Package Aspose.OCR`）  
- 一张包含清晰、机器可读文本的图片（`input.jpg`）  
- 文本编辑器或 Visual Studio（任何 IDE 都可以）  

无需额外的配置文件，也没有隐藏的魔法——只需要 SDK 和一张图片。

## Step 1 – Read image file C# with Aspose.OCR

首先要做的就是把有效的图像喂给 OCR 引擎。Aspose.OCR 需要一个 `OcrImage` 对象，你可以直接从文件路径创建它。

```csharp
using Aspose.OCR;
using System.IO;

// Path to the source picture
string imagePath = @"C:\MyProject\Images\input.jpg";

// Load the image – this is the “read image file C#” part
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

*为什么重要：* 预先加载图像可以验证文件是否存在并在引擎开始处理像素前捕获格式问题。如果文件缺失，`FromFile` 会抛出明确的异常，便于后续处理。

## Step 2 – Initialize the Aspose OCR engine

创建引擎的开销很小，但建议使用 `using` 语句包装，以便及时释放资源。

```csharp
// Create the OCR engine – it holds all the recognition settings
using var ocrEngine = new OcrEngine();
```

*小技巧：* 默认引擎对大多数拉丁文字表现良好。如果需要其他语言，可在调用 `Recognize` 前设置 `ocrEngine.Language = Language.YourLanguage;`。

## Step 3 – Extract text image C# – Perform the recognition

现在开始真正的工作。`Recognize` 方法返回一个 `OcrResult` 对象，里面包含原始文本、置信度分数以及每个单词的边界框。

```csharp
// Run OCR – this is the “extract text image C#” step
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);
```

你会看到 `ocrResult.Text` 保存了纯字符串，而 `ocrResult.Regions` 提供了位置信息，方便在 UI 中高亮显示单词。

## Step 4 – Write JSON file C# – Serialize the result

使用 `System.Text.Json` 序列化为 JSON 非常直接。我们会对输出进行美化，使其易于阅读。

```csharp
using System.Text.Json;

// Convert the OCR result to nicely formatted JSON
string json = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true });
```

*为什么使用 `System.Text.Json`：* 它内置于 .NET，速度快且无需额外依赖。如果你更喜欢 Newtonsoft，只需改动几行代码。

## Step 5 – Persist the JSON to disk

最后，将字符串写入文件。这一步完成了 **write json file c#** 的全部内容。

```csharp
// Destination path for the JSON output
string jsonOutputPath = @"C:\MyProject\Output\ocrResult.json";

// Save the JSON – now you have a portable data file
File.WriteAllText(jsonOutputPath, json);

Console.WriteLine("OCR data saved as JSON.");
```

### 预期的 JSON 输出（示例）

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑01\nTotal: $1,234.56",
  "Regions": [
    {
      "BoundingBox": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Confidence": 0.98,
      "Text": "Invoice #12345"
    },
    {
      "BoundingBox": { "X": 10, "Y": 60, "Width": 150, "Height": 30 },
      "Confidence": 0.96,
      "Text": "Date: 2024‑03‑01"
    },
    {
      "BoundingBox": { "X": 10, "Y": 100, "Width": 180, "Height": 30 },
      "Confidence": 0.99,
      "Text": "Total: $1,234.56"
    }
  ]
}
```

*注意：* 具体数值会因你的图像而异，但结构保持不变——非常适合喂给 API、数据库或前端可视化组件。

## Full C# OCR tutorial – All steps combined

下面是完整的、可直接复制粘贴的程序，涵盖所有步骤。没有缺失的部分，也没有“请参考文档”的快捷方式。

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\MyProject\Images\input.jpg";
        var ocrImage = OcrImage.FromFile(imagePath);

        // -------------------------------------------------
        // Step 2: Create and configure the OCR engine
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine();
        // Example: ocrEngine.Language = Language.English; // optional

        // -------------------------------------------------
        // Step 3: Perform OCR recognition
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // -------------------------------------------------
        // Step 4: Serialize the result to indented JSON
        // -------------------------------------------------
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // -------------------------------------------------
        // Step 5: Write the JSON to a file
        // -------------------------------------------------
        string jsonOutputPath = @"C:\MyProject\Output\output.json";
        File.WriteAllText(jsonOutputPath, json);

        // -------------------------------------------------
        // Step 6: Let the user know we’re done
        // -------------------------------------------------
        Console.WriteLine("OCR data saved as JSON.");
    }
}
```

### 运行代码

1. 将两个 `@"C:\MyProject\…"` 路径替换为你实际的目录。  
2. 构建项目（`dotnet build`）并运行（`dotnet run`）。  
3. 打开 `output.json`——你应该能看到图像文本的结构化表示。

## Common Questions & Edge Cases

**如果我的图像模糊怎么办？**  
Aspose.OCR 提供了预处理选项，例如 `ocrEngine.ImagePreprocessOptions.Deskew = true;`。在调用 `Recognize` 前启用它们，可提升准确率。

**能只输出纯文本吗？**  
可以——只需序列化 `ocrResult.Text` 而不是整个对象：

```csharp
string plainJson = JsonSerializer.Serialize(
    new { Text = ocrResult.Text },
    new JsonSerializerOptions { WriteIndented = true });
```

**需要处理多页 PDF 吗？**  
本示例聚焦单张图像，但你可以遍历每页的图像，执行相同步骤，并将结果聚合成 JSON 数组。

## Pro Tips & Gotchas

- **文件路径：** 使用 `Path.Combine` 避免硬编码反斜杠，尤其是将来迁移到 Linux 时。  
- **内存：** 对于大批量处理，复用同一个 `OcrEngine` 实例，而不是为每张图像创建新实例。  
- **JSON 大小：** 若只需要文本，去掉 `Regions` 属性可显著减小负载。  
- **版本检查：** 本教程在 Aspose.OCR 23.9.0 上测试通过；新版本保持相同的 API，但请始终查看发行说明以防止破坏性更改。

![示例 OCR JSON 输出 – aspose ocr 示例](https://example.com/sample-ocr-json.png "aspose ocr 示例 JSON 预览")

## Conclusion

我们完整演示了一个 **aspose ocr 示例**：读取图像、提取文本并使用纯 C# 将结果写入 JSON 文件。该方案自包含、可用于生产环境，并且易于扩展——无论是添加语言支持、调整置信度阈值，还是将 JSON 送入下游服务。

想进一步？可以把本教程与 **C# OCR tutorial** 结合，上传 JSON 到 Azure Cognitive Search，或尝试从发票中提取表格。只要手中有 JSON，可能性无限。

有趣的改进想法？欢迎留言、fork 代码库，或在 GitHub 上私信我。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}