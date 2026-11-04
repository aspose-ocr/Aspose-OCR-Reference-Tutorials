---
category: general
date: 2026-04-01
description: 如何在 C# 中将 OCR 输出转换为 JSON 和 XML —— 学习使用 Aspose.OCR 从图像提取文本并生成 JSON 文件。
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: zh
og_description: 如何使用 C# 将 OCR 结果转换为结构化的 JSON 和 XML 文件。一步步指南，提取图像中的文本并生成 JSON 文件（C#）。
og_title: 如何在 C# 中将 OCR 转换为 JSON 和 XML – 写入 JSON 文件
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中将 OCR 转换为 JSON 与 XML – 写入 JSON 文件
url: /zh/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中将 OCR 转换为 JSON 与 XML – 写入 JSON 文件

**如何将 OCR** 结果转换为可实际使用的形式是许多开发者常问的问题。在本指南中，我们将展示如何从图像中提取文本，将 OCR 输出转换为格式良好的 JSON 与 XML，并使用 C# 将这些文件写入磁盘。

如果你曾盯着原始 OCR 字符串感叹“一定有更好的存储方式”，那么这里正是你的目标。阅读完本教程后，你将拥有一个完整、可运行的程序，它不仅 **从图像文件中提取文本**，还能 **写入 JSON 文件 C#** 与 **写入 XML 文件 C#**，轻松搞定。

## 你需要准备的东西

- **.NET 6.0** 或更高版本（代码同样适用于 .NET Framework 4.6+）。  
- **Aspose.OCR** NuGet 包 – 使用 `dotnet add package Aspose.OCR` 安装。  
- 包含文字的图像（例如 `invoice.png`）。  
- 任意你喜欢的 IDE – Visual Studio、Rider 或 VS Code 都可以。

> **小贴士：** 将图像文件放在专用文件夹中（例如 `Resources/`），以保持路径整洁。

## 第一步：设置 OCR 引擎 – 如何转换 OCR

首先，创建一个 `OcrEngine` 实例并指定要识别的语言。大多数情况下 English 已足够，但你可以将 `Language.English` 替换为任意受支持的语言。

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **为什么重要：** 使用正确的语言初始化引擎可以显著提升准确率，尤其是对非拉丁文字脚本。

## 第二步：识别文本 – 从图像中提取文字

现在将图像传给引擎。`Recognize` 方法返回一个 `OcrResult` 对象，其中包含原始文字以及位置信息。

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

如果找不到图像，`Recognize` 会抛出 `FileNotFoundException`。为了演示简洁，这里假设路径正确，但在生产环境中应使用 try‑catch 包裹。

## 第三步：将结果转换为 JSON – 写入 JSON 文件 C#

Aspose.OCR 的序列化非常简便。`ToJson` 方法接受一个 `indent` 标志，用于生成美化后的输出，这在你想用文本编辑器打开文件时非常合适。

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### 预期的 JSON 示例

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **如何提取文字**：`Text` 属性返回纯字符串，你可以将其传递给其他服务（搜索索引、数据库等）。

## 第四步：持久化 JSON – 写入 JSON 文件 C#（续）

JSON 字符串准备好后，只需使用 `File.WriteAllText` 将其写入文件。默认使用 UTF‑8 编码。

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

现在，`invoice.json` 已经与图像文件并列，随时可供后续处理。

## 第五步：将结果转换为 XML – 写入 XML 文件 C#

如果你更倾向于使用 XML（针对旧系统），`ToXml` 方法可以完成大部分工作。和 `ToJson` 一样，它也支持美化输出。

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### 预期的 XML 示例

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## 第六步：持久化 XML – 写入 XML 文件 C#（续）

保存 XML 的方式与 JSON 完全相同，只需将文件扩展名改为 `.xml`。

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### 完整工作示例

把所有代码组合在一起，下面是可以直接复制到控制台应用程序中的完整程序：

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

运行程序后，你会在指定位置看到两个新文件——`invoice.json` 与 `invoice.xml`。打开它们即可验证结构是否与上面的示例相符。

## 常见问题与边缘情况

| Question | Answer |
|----------|--------|
| **如果图像包含多种语言怎么办？** | 为每种语言创建单独的 `OcrEngine` 实例，或在受支持时使用 `Language.Multi`。 |
| **我能控制输出格式吗（例如排除区域数据）？** | 可以。`ToJson` 与 `ToXml` 都接受可选参数用于过滤字段，详情请查阅 Aspose.OCR 文档中的 `ExportOptions`。 |
| **如何处理包含多页的大型 PDF？** | 对每页单独处理，汇总结果后再一次性序列化。 |
| **输出是否安全的 UTF‑8？** | 绝对安全——Aspose.OCR 在内部使用 Unicode，`File.WriteAllText` 默认写入 UTF‑8。 |
| **性能如何？** | OCR 对 CPU 需求较高。批量作业可考虑跨核并行或使用 Aspose 的云 API。 |

## 结论

现在你已经掌握了 **如何将 OCR** 结果转换为 JSON 与 XML 的完整流程，并使用 C# **提取图像文字**、**写入 JSON 文件 C#** 与 **写入 XML 文件 C#**。只需几行代码，这种方法既快速又可靠，适用于 Aspose.OCR 支持的任何图像类型。

准备好迎接下一个挑战了吗？尝试将

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}