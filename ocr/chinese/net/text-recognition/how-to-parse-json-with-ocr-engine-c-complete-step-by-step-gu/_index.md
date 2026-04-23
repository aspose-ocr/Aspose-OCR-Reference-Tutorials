---
category: general
date: 2026-03-17
description: 学习如何在 C# 中解析 OCR 结果的 JSON。本教程涵盖如何提取文本、加载用于 OCR 的图像、运行 OCR 识别，以及高效使用 OCR
  引擎 C#。
draft: false
keywords:
- how to parse json
- how to extract text
- load image for OCR
- run OCR recognition
- use OCR engine C#
language: zh
og_description: 如何在 C# 中解析 OCR 输出的 JSON。按照我们的指南提取文本、加载 OCR 图像、运行 OCR 识别，并使用 OCR 引擎
  C#。
og_title: 如何使用 OCR 引擎 C# 解析 JSON – 完整教程
tags:
- C#
- OCR
- JSON
- Image Processing
title: 如何使用 OCR 引擎 C# 解析 JSON – 完整的逐步指南
url: /zh/net/text-recognition/how-to-parse-json-with-ocr-engine-c-complete-step-by-step-gu/
---

shortcode.

Make sure to preserve all markdown formatting.

Let's produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 OCR 引擎 C# 解析 JSON – 完整分步指南

有没有想过 **how to parse json** 直接来自 OCR 引擎的 JSON？你并不孤单。大多数开发者都会遇到同样的难题——获取原始 JSON 后，如何提取有用的信息，如置信度分数或实际文本。在本指南中，我们将一步步演示如何加载用于 OCR 的图像、运行 OCR 识别，最后 **how to parse json** 并以干净、可维护的方式进行解析。

完成本教程后，你将能够：

* 只用几行代码加载用于 OCR 的图像。  
* 使用 C# OCR 引擎运行 OCR 识别。  
* **How to extract text** 并从 JSON 负载中获取其他元数据。  
* 处理常见的边缘情况（缺失字段、意外格式），避免崩溃。

无需外部文档——所有内容都在这里。

## 前置条件

在开始之前，请确保你已经具备：

* .NET 6.0 或更高版本（代码同样可以在 .NET Framework 4.7+ 上编译）。  
* 对所使用的 OCR 库的引用（示例使用了一个假设的 `OcrEngine` 类）。  
* 用于 JSON 处理的 `Newtonsoft.Json` NuGet 包（`Install-Package Newtonsoft.Json`）。  
* 一张图像文件（例如 `passport.png`），放置在应用程序可以读取的位置。

> **专业提示：** 如果你使用的是商业 OCR SDK，请检查 JSON 输出格式是否已启用——大多数供应商都通过类似 `ocrEngine.Config.OutputFormat` 的配置属性来暴露它。

## 第 1 步 – 创建并配置 OCR 引擎（主要关键词出现）

首先需要实例化 OCR 引擎并告诉它返回 JSON。这正是 **how to parse json** 在代码中首次出现的地方，因为引擎会返回一个我们随后要解析的 JSON 字符串。

```csharp
using System;
using Newtonsoft.Json.Linq;   // For JSON parsing
// Assume OcrEngine, OutputFormat, and ImageStream live in the OCR SDK namespace
using OcrSdk;                  // <-- replace with the real namespace

// Step 1: Create an OCR engine instance and set JSON output
var ocrEngine = new OcrEngine();
ocrEngine.Config.OutputFormat = OutputFormat.Json;
```

**为什么这很重要：** 将 `OutputFormat` 设置为 `Json` 可确保响应中既包含识别的文本 **and** 有用的元数据，如置信度分数。如果忘记此步骤，你将只得到纯文本，**how to parse json** 就变得毫无意义。

## 第 2 步 – 加载用于 OCR 的图像

现在我们加载要分析的图片。这正是次要关键词 **load image for OCR** 发光的地方。

```csharp
// Step 2: Load the image you want to recognize
// Make sure the path points to a real file; otherwise an exception is thrown.
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\passport.png");
```

> **如果文件不存在怎么办？** 将调用包装在 `try/catch` 中并显示友好的提示——这样应用不会崩溃，用户也能知道出了什么问题。

## 第 3 步 – 运行 OCR 识别

引擎准备就绪且图像已加载后，接下来合乎逻辑的步骤就是实际运行识别过程。这满足了次要关键词 **run OCR recognition**。

```csharp
// Step 3: Execute OCR and get the raw result object
var ocrResult = ocrEngine.Recognize();
```

`ocrResult.Text` 属性现在包含一个 JSON 字符串。如果将其打印到控制台，你会看到类似下面的内容：

```json
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}
```

## 第 4 步 – 从 JSON 中提取文本（以及其他字段）

本教程的核心：**how to parse json** 与 **how to extract text** 从 OCR 负载中提取信息。我们将使用 `Newtonsoft.Json.Linq.JObject`，因为它非常灵活。

```csharp
// Step 4: Output the raw JSON (optional, helps debugging)
Console.WriteLine("Raw OCR JSON:");
Console.WriteLine(ocrResult.Text);
Console.WriteLine();

// Step 5: Parse the JSON into a JObject
JObject jsonObject = JObject.Parse(ocrResult.Text);

// Extract the overall confidence score
var overallConfidence = jsonObject["OverallConfidence"]?.Value<double>() ?? 0.0;
Console.WriteLine($"Overall confidence: {overallConfidence:P0}");

// Extract the text from the first page (how to extract text)
string pageText = jsonObject["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
Console.WriteLine("Extracted text:");
Console.WriteLine(pageText);
```

**为什么使用 `JObject`？** 它允许你在不定义完整 C# 模型类的情况下安全地遍历 JSON 树。空值条件运算符 (`?.`) 能在 OCR 引擎遗漏字段时防止 `NullReferenceException`。

### 处理边缘情况

* **缺失字段：** `?.Value<T>() ?? default` 模式会返回一个合理的默认值。  
* **多页文档：** 如果预期有多个页面，遍历 `jsonObject["Pages"]`。  
* **非数值置信度：** 当 SDK 有时返回字符串时，使用 `double.TryParse`。

## 第 5 步 – 将所有逻辑封装为可复用方法

为了避免重复粘贴相同的样板代码，将整个流程封装到一个帮助方法中。这也演示了 **use OCR engine C#** 的干净、可复用用法。

```csharp
public static void RunOcrAndParseJson(string imagePath)
{
    // 1️⃣ Create engine & set JSON output
    var engine = new OcrEngine();
    engine.Config.OutputFormat = OutputFormat.Json;

    // 2️⃣ Load image (load image for OCR)
    engine.Image = ImageStream.FromFile(imagePath);

    // 3️⃣ Run OCR (run OCR recognition)
    var result = engine.Recognize();

    // 4️⃣ Show raw JSON (optional)
    Console.WriteLine("=== Raw JSON ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();

    // 5️⃣ Parse JSON (how to parse json)
    JObject obj = JObject.Parse(result.Text);

    // 6️⃣ Extract useful data (how to extract text)
    double confidence = obj["OverallConfidence"]?.Value<double>() ?? 0.0;
    string text = obj["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;

    Console.WriteLine($"Overall confidence: {confidence:P0}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(text);
}
```

现在你可以在 `Main` 或应用程序的其他部分调用 `RunOcrAndParseJson(@"C:\Images\passport.png");`。

## 完整可运行示例

下面是一个完整的、独立的控制台程序示例，你可以直接复制粘贴到新的 `.csproj` 中。它包含了我们讨论的所有部分，并加入了一点错误处理。

```csharp
// File: Program.cs
using System;
using Newtonsoft.Json.Linq;
using OcrSdk;               // Replace with the actual namespace of your OCR library

class Program
{
    static void Main()
    {
        try
        {
            // Adjust the path to point at a real image on your machine
            string imagePath = @"YOUR_DIRECTORY\passport.png";

            RunOcrAndParseJson(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Unexpected error: {ex.Message}");
        }
    }

    /// <summary>
    /// Demonstrates how to parse JSON returned by an OCR engine,
    /// and how to extract text, confidence, and other metadata.
    /// </summary>
    /// <param name="imagePath">Full path to the image file.</param>
    public static void RunOcrAndParseJson(string imagePath)
    {
        // 1️⃣ Initialize OCR engine (use OCR engine C#)
        var engine = new OcrEngine();
        engine.Config.OutputFormat = OutputFormat.Json;

        // 2️⃣ Load image for OCR
        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Run OCR recognition
        var result = engine.Recognize();

        // 4️⃣ Print raw JSON (helps debugging)
        Console.WriteLine("=== Raw OCR JSON ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // 5️⃣ Parse JSON (how to parse json)
        JObject json = JObject.Parse(result.Text);

        // 6️⃣ Extract overall confidence
        double overallConf = json["OverallConfidence"]?.Value<double>() ?? 0.0;
        Console.WriteLine($"Overall confidence: {overallConf:P0}");

        // 7️⃣ Extract text from first page (how to extract text)
        string firstPageText = json["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(firstPageText);
    }
}
```

**预期输出**（假设 OCR 成功）：

```
=== Raw OCR JSON ===
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}

Overall confidence: 92%
=== Extracted Text ===
John Doe
Passport No: 123456789
```

如果图像无法读取，SDK 会抛出异常，我们在 `Main` 中捕获并打印友好的错误信息，而不是让程序崩溃。

## 常见问题解答 (FAQs)

**问：如果 OCR 引擎返回的是页面数组怎么办？**  
答：遍历 `json["Pages"]` 并将每个 `["Text"]` 值拼接起来，或根据实际需求单独处理每页。

**问：我可以将 JSON 反序列化为强类型的 C# 类吗？**  
答：完全可以。定义一个与 JSON 架构匹配的类结构，然后使用 `JsonConvert.DeserializeObject<YourRootClass>(result.Text)`。这样可以获得编译时安全性，但需要保持模型与 SDK 输出同步。

**问：这能与异步 OCR API 一起使用吗？**  
答：可以。将 `engine.Recognize()` 替换为 `await engine.RecognizeAsync()`，并将 `RunOcrAndParseJson` 改为 `async Task`。JSON 解析部分保持不变。

**问：如何将 JSON 保存到文件以便后续分析？**  
答：在获取 `result.Text` 后，调用 `File.WriteAllText(@"output.json", result.Text);`。随后可使用 `JObject.Parse(File.ReadAllText(...))` 重新加载。

## 接下来

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}