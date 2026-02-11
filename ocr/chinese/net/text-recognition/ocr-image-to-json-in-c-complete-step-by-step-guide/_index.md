---
category: general
date: 2026-02-11
description: 在 C# 中将 OCR 图像转换为 JSON。学习如何从图像中提取文本、读取图像文件（C#），格式化 JSON 输出，并使用 Aspose.OCR
  对 JSON 进行美化打印。
draft: false
keywords:
- ocr image to json
- extract text from image
- read image file c#
- format json output
- pretty print json c#
language: zh
og_description: 在 C# 中将 OCR 图像转换为 JSON。本指南展示了如何从图像中提取文本、读取图像文件、格式化 JSON 输出以及使用 Aspose.OCR
  在 C# 中美化打印 JSON。
og_title: C# 中将 OCR 图像转换为 JSON – 完整分步指南
tags:
- OCR
- C#
- JSON
title: C# 中将 OCR 图像转换为 JSON – 完整的逐步指南
url: /zh/net/text-recognition/ocr-image-to-json-in-c-complete-step-by-step-guide/
---

Paragraph.

Translate.

Then closing shortcodes.

Make sure to keep all markdown syntax.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr image to json in C# – 完整分步指南

是否曾经需要 **ocr image to json**，却不确定该选哪个库或如何获得格式良好的结果？你并不孤单。在许多真实场景的应用中——收据扫描、身份证验证或简单的文档归档——你都会希望从图像中提取文本，并得到一个干净的 JSON 负载供下游服务使用。

在本教程中，我们将完整演示整个流程：从 C# 读取图像文件、使用 Aspose.OCR 提取文本、请求引擎返回结构化的 JSON 输出，最后对 JSON 进行美化打印，使其易于阅读。完成后，你将拥有一个自包含、可直接投入生产的代码片段，能够在任何 .NET 项目中使用。

我们还会涉及常见的坑（例如缺少语言包），并展示几种快速变体——比如切换为 XML 输出或处理多页 PDF。无需查阅外部文档，所有内容都在这里。

## What You’ll Need

- **.NET 6+**（代码同样适用于 .NET Framework 4.7+）
- **Aspose.OCR for .NET** – 通过 NuGet 安装 (`Install-Package Aspose.OCR`)
- 一张示例图片（例如 `receipt.png`），放在可引用的位置
- 基本的 C# 语法了解（只要写过 “Hello World” 就足够）

> *Pro tip:* 如果你在 CI 服务器上运行，设置 `AutomaticResourceDownload = true`，让 Aspose 在运行时自动下载语言数据——无需手动处理 DLL。

## Step 1: Read image file C# and create the OCR engine  

首先，我们从磁盘加载图像。使用 `System.Drawing.Image` 可以让代码保持简洁，并且支持 PNG、JPEG、BMP，甚至多页 TIFF（引擎默认只处理第一页）。

```csharp
using System.Drawing;          // For Image
using Aspose.OCR;              // Core OCR classes
using Aspose.OCR.Models;       // Language and output enums
using System.Text.Json;        // JSON parsing & pretty‑print

// 1️⃣ Configure the OCR engine – this is where we tell Aspose what language we expect
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // extract text from image in English
    AutomaticResourceDownload = true,        // auto‑download language packs if missing
    OutputFormat = OcrOutputFormat.Json      // ask for JSON rather than plain text
};
```

**为什么重要：**  
- `AutomaticResourceDownload` 可以防止在本地缺少英文语言文件时导致运行时崩溃。  
- 将 `OutputFormat` 设置为 `Json` 意味着引擎已经完成了将原始 OCR 结果转换为结构化对象的工作——不需要手动解析字符串。

## Step 2: Run OCR and obtain JSON output  

接下来，将加载好的位图传入引擎。`Recognize` 方法返回一个 `OcrResult`，其中的 `Text` 属性即为 JSON 字符串。

```csharp
// 2️⃣ Load the image you want to process
using (var receiptImage = Image.FromFile(@"C:\Images\receipt.png"))
{
    // 3️⃣ Perform OCR – this call blocks until the engine finishes
    var ocrResult = ocrEngine.Recognize(receiptImage);

    // 4️⃣ The OCR engine gave us JSON straight away
    string rawJson = ocrResult.Text;
    
    // Optional: write the raw JSON to a file for debugging
    System.IO.File.WriteAllText(@"C:\Temp\ocr_raw.json", rawJson);
}
```

**边缘情况：** 如果图像损坏或路径错误，`Image.FromFile` 会抛出 `FileNotFoundException`。在输入可能不可靠时，请使用 `try/catch` 包裹代码块。

## Step 3: Parse and format the JSON – pretty print JSON C#  

OCR 引擎返回的原始 JSON 紧凑且难以阅读。借助 `System.Text.Json`，我们可以将其反序列化为 `JsonDocument`，随后再以带缩进的方式重新序列化。

```csharp
// 5️⃣ Parse the JSON string into a DOM-like structure
using var jsonDoc = JsonDocument.Parse(rawJson);

// 6️⃣ Pretty‑print with indentation (2 spaces by default)
string prettyJson = JsonSerializer.Serialize(
    jsonDoc.RootElement,
    new JsonSerializerOptions { WriteIndented = true });

// 7️⃣ Output to console – you could also send this to an API or a file
Console.WriteLine(prettyJson);

// 8️⃣ Save the pretty JSON for later use
System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
```

**你将看到：**  

```json
{
  "Lines": [
    {
      "Text": "Store Name",
      "BoundingBox": { "X": 12, "Y": 5, "Width": 150, "Height": 20 }
    },
    {
      "Text": "Total: $23.45",
      "BoundingBox": { "X": 12, "Y": 200, "Width": 100, "Height": 20 }
    }
  ],
  "Language": "English",
  "Confidence": 0.96
}
```

现在的 JSON 包含逐行文本、边界框、检测到的语言以及置信度分数——非常适合喂给下游分析系统或 UI 组件。

## Step 4: Bonus – Switching output format or language  

如果你需要 **format json output** 为 XML，或想要 OCR 西班牙语收据，只需调整引擎配置：

```csharp
ocrEngine.Language = OcrLanguage.Spanish;          // extract text from image in Spanish
ocrEngine.OutputFormat = OcrOutputFormat.Xml;     // ask for XML instead of JSON
```

其余代码保持不变；只需要更改反序列化步骤（XML 可使用 `XmlDocument`）。

## Full Working Example  

下面把所有步骤整合到一个文件中，你可以直接复制粘贴到控制台应用程序里：

```csharp
// ---------------------------------------------------------------
// ocr_image_to_json_demo.cs
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Text.Json;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Configure OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            AutomaticResourceDownload = true,
            OutputFormat = OcrOutputFormat.Json
        };

        // Path to your image – adjust as needed
        string imagePath = @"C:\Images\receipt.png";

        try
        {
            using (var receiptImage = Image.FromFile(imagePath))
            {
                var ocrResult = ocrEngine.Recognize(receiptImage);
                string rawJson = ocrResult.Text;

                // Parse & pretty‑print
                using var jsonDoc = JsonDocument.Parse(rawJson);
                string prettyJson = JsonSerializer.Serialize(
                    jsonDoc.RootElement,
                    new JsonSerializerOptions { WriteIndented = true });

                Console.WriteLine("=== Pretty‑Printed OCR JSON ===");
                Console.WriteLine(prettyJson);

                // Optional: write to file
                System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Error processing image: {ex.Message}");
        }
    }
}
```

运行该程序后，控制台会打印出美化后的 JSON，并将其保存到 `C:\Temp\ocr_pretty.json`。`try/catch` 块确保即使图像读取失败，也会返回清晰的错误信息，而不是静默崩溃。

## Common Questions & Gotchas  

- **如果 OCR 返回空文本怎么办？**  
  通常意味着图像噪声过大或语言不匹配。尝试提升图像对比度或将 `Language` 设置为 `AutoDetect`。  

- **可以在循环中处理多张图片吗？**  
  当然可以。将 `using (var img = Image.FromFile(...))` 包裹在 `foreach (var file in Directory.GetFiles(...))` 循环中，并将每个 `prettyJson` 收集到列表或写入独立文件。  

- **JSON 模式是否稳定？**  
  Aspose 对 `Json` 输出格式保证向后兼容，但如果你针对特定 API 版本，仍需检查响应中的 `Version` 属性。  

- **使用 Aspose.OCR 是否需要许可证？**  
  免费评估密钥可用于最多 100 页。生产环境请购买许可证，并使用 `License license = new License(); license.SetLicense("Aspose.OCR.lic");` 进行设置。

## Conclusion  

现在，你已经拥有一个 **complete, self‑contained solution to ocr image to json** 的 C# 实现。通过读取图像文件、配置 OCR 引擎、请求 JSON 输出并进行美化打印，你可以在任何 .NET 服务中轻松集成文本提取，而无需手动编写字符串处理代码。

接下来，你可以探索 **extract text from image** 的其他文件类型（PDF、多页 TIFF），尝试不同语言，或将 JSON 导入 NoSQL 存储进行分析。只要妥善处理错误并关注许可证使用，OCR 管道的潜力无限。

祝编码愉快，愿你的 OCR 流程始终精准！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}