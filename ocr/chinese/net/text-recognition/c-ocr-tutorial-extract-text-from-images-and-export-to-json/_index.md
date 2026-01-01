---
category: general
date: 2026-01-01
description: C# OCR 教程，展示如何提取文本、加载图像进行 OCR，并使用 Aspose.OCR 将 JSON 写入文件——一步一步的指南。
draft: false
keywords:
- c# OCR tutorial
- how to extract text
- write json to file
- load image for OCR
- OCR image to JSON
language: zh
og_description: c# OCR 教程，逐步演示如何从图像中提取文本、加载图像进行 OCR，以及使用 Aspose.OCR 将 JSON 写入文件。
og_title: c# OCR tutorial – Extract Text and Export to JSON
tags:
- Aspose.OCR
- C#
- Text Extraction
title: C# OCR 教程 – 从图像提取文本并导出为 JSON
url: /zh/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教程 – 从图像提取文本并导出为 JSON

是否曾想过如何在不花费数小时编写自定义解析器的情况下，从扫描的发票中提取文本？你并不孤单。在本 **c# OCR 教程** 中，我们将向你展示如何为 OCR 加载图像、运行识别引擎，然后 **将 JSON 写入文件**，以便将数据馈送到下游系统。

想象一下，你有一个收据文件夹，每个文件名为 `receipt1.png`、`receipt2.png`，你需要一种快速方法将它们转换为可搜索的 JSON 记录。这就是我们要解决的问题，完成后你将拥有一个可直接运行的控制台应用程序，专门用于此目的。无需除 Aspose.OCR 之外的额外依赖，也没有魔法——只有清晰、可复现的步骤。

> **你将学到**
> - 如何使用 Aspose.OCR **加载图像进行 OCR**。
> - **提取文本** 并获取置信度分数的最佳方式。
> - 将 OCR 结果转换为结构良好的 **OCR 图像到 JSON** 负载。
> - 安全 **将 JSON 写入文件** 并验证输出。

## 前置条件

- .NET 6 SDK 或更高版本（代码同样适用于 .NET Core）。  
- Visual Studio 2022 或你喜欢的任意编辑器。  
- Aspose.OCR NuGet 包（`Install-Package Aspose.OCR`）。  
- 一张你想要处理的图像文件（PNG、JPG、BMP）——演示中我们使用 `invoice.png`。

如果缺少上述任意项，请从 Microsoft 官网下载 SDK，并通过包管理器控制台添加 NuGet 包：

```powershell
Install-Package Aspose.OCR
```

现在基础工作已经就绪，让我们深入实际实现。

## 第一步：c# OCR 教程 – 初始化 OCR 引擎

在 **加载图像进行 OCR** 之前，需要一个驱动识别过程的引擎实例。`OcrEngine` 类体积轻巧，但最好将其放在 `using` 块中，以便及时释放资源。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine – this is the heart of the c# OCR tutorial
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow…
```

*小贴士*：如果计划批量处理大量图像，建议复用同一个 `OcrEngine` 实例，而不是每次都创建新实例。这样可以降低内存消耗并提升速度。

## 第二步：加载图像进行 OCR

现在我们真正 **加载图像进行 OCR**。Aspose.OCR 支持多种格式，你可以指向 PNG、JPEG，甚至是多页 TIFF。`OcrImage.FromFile` 方法读取文件并为识别做好准备。

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the folder that holds your invoice.png
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);
```

> **为何重要**：单独加载图像可以让你检查其尺寸、DPI，或在送入引擎前进行预处理（例如二值化）。如果图像损坏，`FromFile` 会抛出明确的异常，你可以捕获并记录。

## 第三步：提取文本 – 运行识别

手握图像后，终于可以 **提取文本** 了。`Recognize` 方法返回一个 `OcrResult` 对象，除了纯文本外，还包含每个单词的位置数据和置信度分数。

```csharp
        // Step 3: Perform OCR – this is the core of how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);
```

*边缘情况*：某些 PDF 包含不可见的文本层。如果你将 PDF 页面渲染为图像后再送入引擎，可能会什么也看不到。此时可以先使用 Aspose.PDF 提取隐藏层，再在必要时回退到 OCR。

## 第四步：OCR 图像到 JSON – 转换结果

`OcrResult` 类提供了便利的 `ToJson()` 方法，可将整个结果集（包括每个单词的边界框和置信度）序列化为 JSON 字符串。这是实现 **OCR 图像到 JSON** 的最简洁方式，无需自行编写序列化器。

```csharp
        // Step 4: Convert the OCR result to JSON (includes words, confidence, locations)
        string jsonResult = ocrResult.ToJson();
```

如果你需要自定义模式，也可以遍历 `ocrResult.Words` 并自行构建对象，但在大多数场景下内置的 JSON 已经足够且结构良好。

## 第五步：将 JSON 写入文件

现在进入最后一步：持久化 JSON 负载。`File.WriteAllText` 方法确保文件以原子方式创建（或覆盖）。请确保目标目录已存在，否则会抛出 `DirectoryNotFoundException`。

```csharp
        // Step 5: Save the JSON output – this demonstrates write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);
```

*提示*：如果需要带 BOM 的 UTF‑8 或其他编码，可使用接受 `Encoding` 参数的重载。

## 第六步：验证输出

一个简短的 `Console.WriteLine` 即可告诉我们过程是否成功。你也可以在查看器中打开 JSON 文件，以确认其结构。

```csharp
        // Step 6: Inform the user that the JSON file has been saved
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### 预期的 JSON 片段

```json
{
  "Text": "Invoice #12345\nDate: 2025-12-31\nTotal: $250.00",
  "Words": [
    { "Text": "Invoice", "Confidence": 0.98, "Location": { "X": 10, "Y": 15, "Width": 80, "Height": 20 } },
    { "Text": "#12345", "Confidence": 0.96, "Location": { "X": 95, "Y": 15, "Width": 60, "Height": 20 } }
    // … more words …
  ]
}
```

JSON 包含每个单词的位置，对于后续在 UI 中高亮显示文本非常有用。

## 完整工作示例

下面是完整的、可直接复制粘贴的程序。将 `YOUR_DIRECTORY` 替换为实际存放图像的路径。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to recognize
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR – how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 4: Convert the result to JSON (OCR image to JSON)
        string jsonResult = ocrResult.ToJson();

        // Step 5: Write JSON to file – write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);

        // Step 6: Verify
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

在项目文件夹中运行程序（`dotnet run`），你会在原始 PNG 同目录下看到 `invoice.json`。

## 常见陷阱及规避方法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| **FileNotFoundException** 在加载图像时 | 路径拼写错误或文件缺失 | 使用 `Path.Combine` 并在调用 `FromFile` 前检查 `File.Exists`。 |
| **置信度分数低** | 图像质量差、DPI 低 | 使用 `ocrImage.AdjustContrast` 进行预处理，或将图像放大至 300 DPI。 |
| **JSON 文件为空** | `ocrResult` 为 null（引擎失败） | 确认图像格式受支持，且许可证（如有）已正确应用。 |
| **大批量处理性能瓶颈** | 每次迭代重新创建 `OcrEngine` | 在批处理期间复用单个 `OcrEngine` 实例，结束后再一次性释放。 |

## 后续步骤

掌握了 **c# OCR 教程** 后，你可能想要：

- **批量处理** 整个文件夹，并将所有 JSON 汇总到单个数据库中。  
- **集成** 输出到 Azure Cognitive Search，实现可搜索的 PDF。  
- **添加语言支持**，例如 `ocrEngine.Language = OcrLanguage.Spanish`（或任何受支持的语言）。  
- **后处理** JSON，使用正则表达式提取表格或键值对。

上述每个扩展都基于我们已覆盖的核心概念：加载图像进行 OCR、提取文本、转换为 JSON、并将 JSON 写入磁盘。

---

### 结论

在本 **c# OCR 教程** 中，我们逐步演示了如何 **加载图像进行 OCR**、**提取文本**、将结果转化为 **OCR 图像到 JSON** 负载，最后 **将 JSON 写入文件**。完整代码示例可直接嵌入任何 .NET 项目，配套的解释帮助你将方案适配到真实业务场景。

尝试使用自己的收据或发票进行实验——调整图像预处理、切换不同语言，观察 JSON 输出的变化。如遇到问题，可回顾上表中的陷阱或在下方留言。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}