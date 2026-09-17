---
category: general
date: 2026-01-13
description: C# OCR 教程，展示如何从图像中提取文本、加载图像进行 OCR，并使用 Aspose OCR 格式化 JSON 输出。学习将对象序列化为
  JSON。
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- format json output
- serialize object to json
- load image for ocr
language: zh
og_description: c# OCR 教程，手把手教你从图像中提取文本、加载图像进行 OCR，以及使用 Aspose OCR 格式化 JSON 输出。
og_title: c# OCR 教程 – 提取文本并格式化 JSON
tags:
- OCR
- C#
- JSON
title: C# OCR 教程 – 从图像提取文本并获取格式化的 JSON
url: /zh/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-get-formatted-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – 从图像提取文本并格式化 JSON 输出

是否曾经想过如何在 C# 项目中 **extract text from image** 文件，而无需处理低层像素？这正是这个 *c# ocr tutorial* 所解决的问题。只需几分钟，你就会看到如何 **load image for ocr**，运行 Aspose OCR，并 **format json output**，以便直接将数据馈入你的 API 或数据库。

我们将逐行讲解代码，解释每个部分为何重要，甚至展示你应得到的确切 JSON。完成后，你将拥有一个可直接运行的控制台应用程序，能够将发票 PNG 转换为整洁、带缩进的 JSON。没有冗余，只提供可直接放入任何 .NET 6+ 项目的实用方案。

## 本 c# ocr tutorial 涵盖的内容

- 安装 Aspose.OCR NuGet 包  
- 为 OCR 处理加载图像文件  
- 识别英文文本（或任何受支持的语言）  
- **Serializing the OCR result to JSON** 并进行美化打印  
- 在控制台显示 JSON，并在需要时保存  

你只需要对 C# 有基本了解并拥有最近的 .NET SDK。除此之外无需其他前置条件。如果你想了解如何 **extract text from image** 用于发票、收据或扫描表单，请继续阅读。

---

## Step 1: Set Up the c# ocr tutorial Environment

在编写任何代码之前，请确保你拥有合适的工具：

1. **.NET 6 SDK or later** – 可从 Microsoft 官网下载。  
2. **Visual Studio 2022**（Community 版完全足够）或任意你喜欢的编辑器。  
3. **Aspose.OCR NuGet package** – 在项目文件夹中运行 `dotnet add package Aspose.OCR`。

> **Pro tip:** 如果你使用 CI 流水线，请将包引用添加到 `.csproj`，这样构建时会自动恢复。

---

## Step 2: Load Image for OCR

在本教程的第一步，我们需要获取要处理的图像。Aspose OCR 支持常见格式，如 PNG、JPEG 和 TIFF。

```csharp
using Aspose.OCR;
using System.Text.Json;

// Replace this with the actual path to your invoice image
string imagePath = @"C:\Invoices\invoice.png";

// Create an OcrImage instance from the file system
OcrImage inputImage = OcrImage.FromFile(imagePath);
```

> **Why this matters:** 将图像加载为 `OcrImage` 能让引擎访问位图数据和 DPI 信息，从而提升识别准确度。跳过此步骤或提供损坏的文件会导致运行时异常。

---

## Step 3: Extract Text from Image

现在我们实际运行 OCR 引擎。`Recognize` 方法返回一个丰富的 `OcrResult` 对象，包含原始文本、置信度分数和布局细节。

```csharp
// Initialize the OCR engine – no license needed for a trial run
OcrEngine ocrEngine = new OcrEngine();

// Recognize English text (you can change the language enum if needed)
OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);
```

> **Edge case:** 如果需要处理多语言文档，可使用不同的 `OcrLanguage` 值分别调用 `Recognize` 两次并将结果拼接。该引擎是线程安全的，甚至可以并行处理大批量文件。

---

## Step 4: Serialize Object to JSON – Format JSON Output

`OcrResult` 对象是普通的 C# 类，这意味着我们可以将其交给 `System.Text.Json`。启用 `WriteIndented` 后，输出将变得易于阅读。

```csharp
// Serialize the OCR result with pretty printing
string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
{
    WriteIndented = true
});
```

> **What you get:** 一个带有良好缩进的 JSON 字符串，包含识别的文本、置信度以及页面布局。这非常适合日志记录、发送至 Web 服务或存储到 NoSQL 数据库。

---

## Step 5: Display and (Optionally) Save the Formatted JSON

最后，我们将 JSON 输出到控制台。如果需要，也可以使用 `File.WriteAllText` 将其写入文件。

```csharp
// Show the JSON in the console
Console.WriteLine(json);

// Optional: Save to a .json file next to the image
string jsonPath = Path.ChangeExtension(imagePath, ".json");
File.WriteAllText(jsonPath, json);
Console.WriteLine($"\nJSON saved to: {jsonPath}");
```

**Expected console output (truncated for brevity):**

```json
{
  "Text": "Invoice #12345\nDate: 2025‑12‑01\nTotal: $250.00",
  "Confidence": 0.97,
  "Pages": [
    {
      "PageNumber": 1,
      "Blocks": [
        {
          "Text": "Invoice #12345",
          "Confidence": 0.99,
          "Rectangle": { "X": 50, "Y": 30, "Width": 200, "Height": 30 }
        }
        // …more blocks…
      ]
    }
  ]
}
```

如果 OCR 引擎未能找到任何文本，`Text` 字段将为空字符串，`Confidence` 为 `0`。这时应检查图像质量。

---

## Step 6: Complete Working Example

将所有内容整合在一起，下面是可以直接复制粘贴到新控制台应用中的完整程序：

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonResultDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (replace with your own path)
        string imagePath = @"C:\Invoices\invoice.png";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize text – this is the core of our c# ocr tutorial
        OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);

        // 4️⃣ Serialize the result with pretty formatting
        string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
        {
            WriteIndented = true
        });

        // 5️⃣ Output to console and optionally write to a file
        Console.WriteLine(json);
        string jsonPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"\nJSON saved to: {jsonPath}");
    }
}
```

运行程序（在项目文件夹中执行 `dotnet run`），即可在控制台看到扫描发票的整齐 JSON 表示。

---

## Common Pitfalls & Tips (c# ocr tutorial Extras)

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Blank `Text` field** | 图像对比度低或已旋转。 | 预处理图像（提升对比度、去倾斜）或使用 `OcrEngine.ImagePreprocess`。 |
| **`System.DllNotFoundException`** | 缺少 Aspose OCR 本地二进制文件。 | 确认 NuGet 包已正确恢复，并且运行时架构（x64/x86）与操作系统匹配。 |
| **Performance lag on large PDFs** | OCR 按顺序处理每一页。 | 为每页创建独立的 `OcrEngine` 实例并行处理（引擎是线程安全的）。 |
| **JSON too large** | 正在序列化所有细节，包括边界框。 | 在序列化前使用仅包含 `Text` 和 `Confidence` 的 DTO。 |

> **Remember:** 本教程的目标是展示一个简洁的端到端流程。你随时可以裁剪 JSON 或后期添加更多元数据。

---

## Conclusion

你刚刚完成了一个 **c# ocr tutorial**：加载图像、**extracts text from image**，并通过 **serializing object to json** 生成 **format json output**。步骤简明，代码可直接运行，JSON 也已完美缩进，便于下游使用。

接下来可以尝试将 `OcrLanguage.English` 替换为 `OcrLanguage.French`，或将收据文件夹循环处理。还可以探索直接将 JSON 保存到 Azure Blob Storage，或喂入机器学习模型。

如果遇到任何问题，请再次确认图像路径正确，并在调用 `Recognize` 前加载 Aspose OCR 许可证（如果有）。祝编码愉快，愿你的 OCR 结果始终清晰！

*展示 OCR 流程的图片（alt text: "c# ocr tutorial diagram showing load image, recognize text, serialize to JSON")*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}