---
category: general
date: 2026-05-02
description: c# OCR 教程，展示如何在 C# 中提取图像文本并识别 PNG 文本，然后使用 JsonSerializer C# 编写带缩进的 JSON。面向开发者的逐步指南。
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: zh
og_description: c# OCR 教程，演示如何在 C# 中提取图像文字并识别 PNG 文本，然后使用 JsonSerializer 将结果写入带缩进的
  JSON。完整、可运行的示例。
og_title: C# OCR 教程 – 提取文本并导出为缩进的 JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: c# OCR 教程 – 从图像提取文本并导出为缩进的 JSON
url: /zh/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr 教程 – 从图像提取文本并导出为缩进的 JSON

是否曾经需要一个 **c# ocr 教程**，直接把文字图片转换为格式良好的 JSON 文件？你并不孤单。在许多项目中——比如发票扫描、收据解析，甚至简单的 meme 文本提取——你会得到一个 PNG 文件，却不知道如何在不编写自定义识别器的情况下提取其中的文字。

本指南提供了动手解决方案：我们将使用 Aspose.OCR **提取文本图像 c#**，**识别 png 文本**，然后使用 C# 中的 `JsonSerializer` **写入缩进的 json**。完成后，你将拥有一个可直接放入任何 .NET 解决方案的独立控制台应用程序。没有模糊的“参考文档”链接，只有完整的、可复制粘贴的示例。

## 需要的环境

- **.NET 6**（或任意较新的 .NET 版本）。旧版框架也能工作，但示例语法针对 .NET 6+。
- **Aspose.OCR for .NET** – 通过 NuGet 安装：`dotnet add package Aspose.OCR`。
- 一张包含清晰、机器可读文字的 PNG 示例图片（`text.png`）。
- 你喜欢的 IDE 或编辑器 – Visual Studio、VS Code、Rider 等。

> **专业提示：** 如果需要处理大量图片，建议复用同一个 `OcrEngine` 实例，而不是为每个文件创建新实例。这样可以降低开销并提升吞吐量。

## 第一步：创建 c# ocr 教程项目

首先，创建一个控制台项目。以下命令会生成项目骨架并引入 OCR 库：

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

现在打开生成的 `Program.cs`。我们稍后会把完整示例代码粘进去，暂时只需确保项目能够成功编译：

```bash
dotnet build
```

如果没有错误，即可继续下一步。

## 第二步：识别 PNG 图片中的文字

任何 **c# ocr 教程** 的核心都是 OCR 引擎本身。Aspose.OCR 把底层细节封装起来，提供了简洁的 `OcrEngine` 类。下面的代码创建引擎，指向 PNG 文件，并请求识别文字。

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### 为什么这样可行

- **`RecognizeImage`** 支持多种格式（PNG、JPEG、BMP）。我们专门 **recognize png text**，因为 PNG 保留无损细节，非常适合 OCR。
- 返回的 `OcrResult` 不仅包含纯文本，还提供每个字形的置信度分数，若后续需要过滤低置信度字符非常有用。

## 第三步：使用 JsonSerializer c# 写入缩进的 JSON

现在我们已经拥有 `ocrResult`，在 **c# ocr 教程** 中接下来的自然步骤是将该对象转换为人类可读的 JSON。内置的 `System.Text.Json` 序列化器可以完成此任务，我们会配置它 **write indented json** 以提升可读性。

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### 正确使用 `JsonSerializer`

- `WriteIndented` 标志是 **write indented json** 的最简方式，无需引入第三方库。
- 若需要驼峰式属性名，可在选项中加入 `PropertyNamingPolicy = JsonNamingPolicy.CamelCase`。
- `jsonOutput` 字符串可以通过 `File.WriteAllText("result.json", jsonOutput);` 保存——这在实际流水线中非常实用。

## 第四步：运行并验证输出

编译并运行程序：

```bash
dotnet run
```

假设 `text.png` 中的文字为 *“Hello, OCR World!”*，你应该会看到类似以下内容：

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

该 JSON 已 **缩进**，便于在日志中阅读或交给下游服务。

### 边缘情况与技巧

| 场景 | 处理方式 |
|-----------|------------|
| **图片模糊** | 在调用 `RecognizeImage` 前提升 `ocrEngine.Config.Dpi`（例如 `ocrEngine.Config.Dpi = 300`）。 |
| **非英文语言** | 设置 `ocrEngine.Config.Language = OcrLanguage.German`（或任意受支持语言）。 |
| **大批量文件** | 遍历目录时复用同一 `OcrEngine` 实例；为每个 JSON 结果使用唯一文件名保存。 |
| **只需要高置信度文本** | 在序列化前过滤 `ocrResult.Lines`，仅保留 `Confidence` ≥ 0.95 的行。 |

## 完整可运行示例（复制粘贴即用）

下面是 *完整* 程序代码，直接放入 `Program.cs` 即可。它包含所有步骤、错误处理以及说明性注释，代码本身易于理解。

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

运行代码，检查控制台输出或生成的 `.json` 文件，你会看到提取的文字以及对应的置信度分数，全部 **缩进** 整齐。

## 结论

现在，你已经掌握了一个完整的 **c# ocr 教程**，展示了如何 **extract text image c#**、**recognize png text**，以及使用 `JsonSerializer` **write indented json**。该示例完整、可运行，并提供了面向真实场景的实用技巧。

下一步可以尝试将 Aspose.OCR 替换为其他引擎（例如 Tesseract），观察 `OcrResult` 的结构变化，或将生成的 JSON 发送至下游 API，存入数据库。你也可以探索 **use jsonserializer c#** 的高级选项，如自定义转换器用于日期格式化或枚举处理。

祝编码愉快，愿你的 OCR 流程始终精准！  

---  

![c# ocr 教程示意图](image.png "展示 OCR 流程的图示")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}