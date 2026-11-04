---
category: general
date: 2026-02-09
description: 学习如何在 C# 中进行 OCR，从图像中提取文本，识别 PNG 文本，并快速写入 JSON 文件。
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: zh
og_description: 如何在 C# 中执行 OCR？请遵循此一步步指南，从图像中提取文本，识别 PNG 中的文字，并高效地在 C# 中写入 JSON 文件。
og_title: 如何在 C# 中执行 OCR – 提取文本并写入 JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: 如何在 C# 中进行 OCR —— 提取文本并写入 JSON
url: /zh/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中执行 OCR – 完整指南

在 C# 中执行 OCR 是一个常见的难题，尤其是当你需要**extract text from image**文件时。在本指南中，我们将演示如何识别 PNG 中的文本、将详细结果导出为 JSON 字符串，最后以**write JSON file C#**的方式写入文件。是否曾盯着扫描的表单，想把那些乱七八糟的字符转换为可搜索的文本？你并不孤单；许多开发者在早期都会遇到这个问题。

我们将使用 Aspose.OCR 库，因为它开箱即提供每个符号的置信度，并且能很好地与 .NET 6+ 项目配合。完成本教程后，你将拥有一个可直接运行的控制台应用程序，能够加载 PNG、提取每个字符，并保存整洁的 JSON 文件，供数据库或 AI 模型使用。没有神秘的“查看文档”快捷方式——只有一个独立完整的解决方案。

## 你需要的环境

- **.NET 6 SDK**（或更高）– 撰写时的当前 LTS 版本。
- **Aspose.OCR for .NET** NuGet 包 – `Install-Package Aspose.OCR`。
- 你想要扫描的 PNG 图像（例如 `form.png`）。
- 任意 IDE 或编辑器 – Visual Studio、VS Code、Rider – 任选其一。

就这些。如果你已经准备好这些组件，就可以开始了。

![如何执行 OCR 示例](ocr-example.png "在 C# 中执行 OCR")

*图片替代文字：展示 C# 控制台应用处理 PNG 的 OCR 示意图。*

## 步骤 1：设置项目并添加依赖

首先，创建一个新的控制台项目并引入 Aspose OCR 库。

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **技巧提示：** 如果想显式锁定目标框架，请使用 `--framework net6.0` 标志。

此步骤重要的原因：NuGet 包包含我们将依赖的 `OcrEngine`、`ImageStream` 和 `JsonExporter` 类。没有它，编译器根本不知道“OCR”是什么。

## 步骤 2：编写核心 OCR 逻辑

打开 `Program.cs`（或新建文件），并用以下内容替换其内容。每个部分都有注释，方便你了解其作用。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### 为什么每个部分都很重要

- **OcrEngine**：可以把它看作整个操作的大脑。它加载语言模型并建立推理管线。
- **ImageStream.FromFile**：处理任何 PNG、JPEG、BMP 等格式，抽象掉文件 I/O 的细节。
- **RecognitionResult**：保存原始文本及置信度分数。这里提供了下游验证所需的细粒度数据。
- **JsonExporter**：将丰富的 `RecognitionResult` 转换为干净的 JSON 负载，十分适合 API 使用。
- **File.WriteAllText**：使用 .NET 的直接方式**write JSON file C#**，无需额外依赖。

## 步骤 3：运行应用并验证输出

编译并执行程序：

```bash
dotnet run
```

你应该会看到类似以下的控制台信息：

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

打开 `form.json` —— 你会看到类似如下内容：

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

**extract text from image** 步骤已成功完成，你现在拥有每个字符的机器可读 JSON 表示。

## 步骤 4：处理常见边缘情况

### 文件缺失或损坏

如果 PNG 路径错误，`ImageStream.FromFile` 会抛出 `FileNotFoundException`。请将加载代码放入 try‑catch 块中：

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### 低置信度分数

有时对于噪声较多的扫描，OCR 会返回低置信度。你可以在导出前过滤符号：

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

这可确保 JSON 只包含相对可靠的字符——在将数据输送至下游验证管道时非常有用。

### 大文件与内存

处理多兆字节的 PNG 可能会导致内存使用激增。可以考虑分块流式读取图像，或使用 `OcrEngine.RecognizeAsync`（在新版 Aspose 中可用）以保持 UI 响应。

## 步骤 5：扩展解决方案（可选）

- **批量处理**：遍历 PNG 目录，为每个文件生成对应的 JSON。
- **数据库存储**：将 JSON 插入 SQL 的 `NVARCHAR(MAX)` 列，以便后续分析。
- **语言选择**：如果需要非英文支持，可设置 `ocrEngine.Language = OcrLanguage.Spanish;`。

所有这些扩展都遵循我们建立的相同 **how to perform OCR** 模式——初始化、识别、导出和持久化。

## 常见问题

**Q: 这能用于 JPG 或 TIFF 吗？**  
A: 当然可以。`ImageStream.FromFile` 会自动检测格式，所以你可以用任何受支持的光栅图像替代 PNG。

**Q: 如果需要从 PDF 中提取文本怎么办？**  
A: 首先将每页 PDF 转换为图像（例如使用 `Aspose.PDF`），然后将生成的 PNG 输入到这里描述的 OCR 流程中。

**Q: 能否将 OCR 结果导出为 XML 而不是 JSON？**  
A: 可以。Aspose.OCR 还提供 `XmlExporter`。将 `JsonExporter` 替换为 `XmlExporter` 并相应修改文件扩展名即可。

## 结论

我们已经完整演示了在 C# 中**how to perform OCR**的全过程，展示了如何**extract text from image**、**recognize text from PNG**以及**write JSON file C#**而无需任何障碍。完整可运行的示例位于上面的代码片段中，你现在也理解了每一步背后的原因——初始化引擎、处理边缘情况以及持久化结果。

接下来，你可以探索批量 OCR 流程、将 JSON 输出集成到 Azure Cognitive Search，或尝试自定义语言模型。一旦掌握了 C# 中 OCR 的基础，想象空间无限。

如果你遇到任何问题或有进一步扩展的想法，欢迎在下方留言。祝编码愉快，尽情将像素化的扫描件转化为干净、可搜索的数据吧！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}