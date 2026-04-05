---
category: general
date: 2026-04-04
description: 学习如何使用 C# 中的 OCR 引擎示例从 TIFF 文件中提取文本。一步步指南，输出 JSON 和 XML。
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: zh
og_description: 使用 OCR 引擎在 C# 中提取 TIFF 文件的文本示例。详细步骤、完整代码以及 JSON/XML 输出技巧。
og_title: 使用 Aspose OCR 引擎从 TIFF 提取文本 – 完整指南
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 使用 Aspose OCR 引擎从 TIFF 提取文本 – 完整示例
url: /zh/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 TIFF 中提取文本 – 完整的 OCR 引擎示例（C#）

是否曾经需要**从 TIFF 图像中提取文本**，但不确定哪个库能够在没有繁琐变通方案的情况下处理多页文件？你并非唯一有此需求的人。在许多遗留系统中，文档以多页 TIFF 扫描件的形式出现，而提取原始文本是搜索、合规或数据录入自动化的必备功能。

好消息是？使用 Aspose OCR，你只需几行代码即可完成——无需操作低层像素缓冲区。本教程将带你完成一个**完整的 OCR 引擎示例**，该示例加载多页 TIFF，识别每一页，并输出美化的 JSON 与可选的 XML。完成后，你将拥有一个可直接运行的 C# 控制台应用，能够在几秒钟内从 TIFF 文件中提取文本。

## 你将学到

- 如何在 .NET 项目中设置 Aspose OCR 引擎。  
- 提取 **TIFF 文本** 所需的完整代码，包括多页处理。  
- 为什么可能需要 JSON 而不是 XML 输出，以及如何同时生成两者。  
- 常见问题的排查技巧（例如图像 DPI、内存使用）。  

### 前置条件

- .NET 6.0 SDK 或更高版本（代码兼容 .NET Core 和 .NET Framework）。  
- 有效的 Aspose OCR 许可证（或免费试用密钥）。  
- Visual Studio 2022 或任意你喜欢的 C# 编辑器。  
- 一个示例多页 TIFF 文件（示例中命名为 `multi-page.tiff`）。  

> **专业提示：** 如果预算紧张，免费试用仍然允许每月提取最多 100 页文本——非常适合测试。

---

## 第一步 – 初始化 OCR 引擎（ocr engine example）

在我们能够**从 TIFF 中提取文本**之前，需要先创建 OCR 引擎的实例。该对象保存了后续可能会调整的所有配置（语言、分辨率等）。

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*为什么重要：* `OcrEngine` 类封装了繁重的底层工作。只实例化一次并在多张图像之间复用，比为每页创建新引擎更省内存。

---

## 第二步 – 加载多页 TIFF（extract text from TIFF）

现在将引擎指向我们的源文件。`ImageStream.FromFile` 支持 TIFF、JPEG、PNG 等多种格式，但本教程聚焦于 TIFF。

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **注意：** 将 `YOUR_DIRECTORY` 替换为你机器上的实际文件夹路径。  
> **提示：** 如果你的 TIFF DPI 较低（低于 150），考虑先进行预处理以提升 OCR 准确度。

---

## 第三步 – 识别所有页面

调用 `Recognize()` 会在 TIFF 的**每一页**上运行 OCR 算法。返回的结果对象包含原始文本、置信度分数以及逐页分割信息。

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*返回内容：* `ocrResult` 包含一系列 `PageResult` 对象。每页的文本可通过 `ocrResult.Pages[i].Text` 访问。引擎还提供置信度水平，可用于质量检查。

---

## 第四步 – 将结果保存为 JSON（以及可选的 XML）

大多数现代流水线更倾向于 JSON，而传统系统仍然使用 XML。下面演示如何同时生成两者，并进行美化。

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### 示例 JSON 输出（已截断）

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

JSON 可读性强，调试时非常方便。如果需要，XML 结构与其保持一致。

---

## 第五步 – 验证提取结果（extract text from TIFF）

文件写入后，快速进行一次完整性检查，以确保一切正常。

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

如果看到打印的片段，说明你已经成功**从 TIFF 中提取文本**并将其持久化。从这里你可以将 JSON 导入搜索索引、数据库或任何下游服务。

---

## 为什么使用 Aspose OCR 来提取 TIFF 文本？

- **开箱即用的多页支持** – 无需手动拆分 TIFF。  
- **高准确率**，得益于专有的神经网络模型。  
- **跨平台** – 可在 Windows、Linux 和 macOS 的 .NET 运行时上运行。  
- **丰富的输出格式**（JSON、XML、纯文本），兼容现代和传统技术栈。  

如果仍有顾虑，试用免费版在示例文档上运行一下。你会发现其速度与简易性远超那些常常需要额外图像预处理的开源方案。

---

## 常见问题及规避方法

| 问题 | 症状 | 解决方案 |
|-------|---------|-----|
| 低分辨率 TIFF | 缺失字符、置信度低 | 在 OCR 前将图像放大至 ≥150 DPI (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| 语言设置错误 | 文字乱码，尤其是非英文文本 | 在 `Recognize()` 前设置 `ocrEngine.Language = Language.Spanish`（或相应语言） |
| 大文件导致内存不足 | `OutOfMemoryException` | 分批处理页面：遍历 `ocrEngine.Image.Pages` 并调用 `RecognizePage(i)` |
| 未应用许可证 | 输出中出现 “Evaluation” 水印 | 注册许可证：`License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## 完整可运行示例（复制粘贴即用）

下面是完整的程序代码，可直接放入新的控制台项目中。它包含了我们讨论的所有环节——初始化、加载、识别以及保存。

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

将文件保存为 `Program.cs`，运行 `dotnet run`，即可在控制台看到 JSON 与 XML 的保存路径。就这样，你已经完成了一个**OCR 引擎示例**，实现了从 TIFF 中提取文本。

---

## 后续步骤与相关主题

- **批量处理：** 将上述逻辑包装在 `foreach` 循环中，自动处理数十个 TIFF 文件。  
- **搜索集成：** 将 JSON 推送至 Elasticsearch 或 Azure Cognitive Search，实现对扫描文档的全文检索。  
- **图像预处理：** 探索 Aspose 的 `ImageProcessing` API，对图像进行去倾斜、去噪或对比度调整后再进行 OCR。  
- **其他输出形式：** 如仅需原始字符串，可使用 `ocrResult.ToPlainText()`，省去元数据。  

如果你对其他图像格式感兴趣，同样的模式也适用于 PDF（只需更换源文件）或 PNG。关键在于，一旦引擎配置好，后续步骤即可重复使用。

---

## 结论

我们已经完整演示了一个**OCR 引擎示例**，使用 Aspose OCR **从 TIFF 文件中提取文本**，并输出整洁的 JSON 与可选的 XML，供任何下游工作流使用。代码自包含，解释覆盖了每一步背后的“为什么”。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}