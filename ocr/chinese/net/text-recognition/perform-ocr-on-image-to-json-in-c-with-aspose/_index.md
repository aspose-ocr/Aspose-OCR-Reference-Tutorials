---
category: general
date: 2026-04-08
description: 学习如何使用 Aspose OCR 在 C# 中对图像进行 OCR 并生成 JSON 文件。本 Aspose OCR C# 教程展示了将
  OCR 图像转换为包含置信度值的 JSON。
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: zh
og_description: 在 C# 中对图像执行 OCR 并将结果导出为 JSON 文件。本教程涵盖完整的 Aspose OCR C# 工作流，包括置信度分数。
og_title: 在 C# 中将图像 OCR 转换为 JSON – Aspose OCR 指南
tags:
- Aspose
- OCR
- C#
- JSON
title: 在 C# 中使用 Aspose 将图像 OCR 转换为 JSON
url: /zh/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中使用 Aspose 将图像 OCR 转换为 JSON

是否曾经需要 **对图像文件执行 OCR**，但不确定如何将结果以结构化的形式获取？你并不孤单——开发者经常会问：“如何把扫描的图片转化为可用的数据？”好消息是 Aspose.OCR 能让这件事变得轻而易举，而且你甚至可以 **写 JSON 文件 C#**‑风格，并包含置信度分数。

在本指南中，我们将完整演示一个 **aspose OCR C# tutorial**，涵盖从加载图像到将识别的文本导出为 JSON 的全部步骤。完成后，你将拥有一个可运行的控制台应用程序，**对图像执行 OCR**，将输出转换为 JSON（包括置信度值），并仅用一行代码保存。没有隐藏步骤，没有外部脚本——纯粹的 C#。

## 前置条件

在开始之前，请确保你已经具备：

- .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）
- Visual Studio 2022（或你喜欢的任何编辑器）
- 有效的 **Aspose.OCR for .NET** 许可证或免费临时许可证（免费试用可用于测试）
- 一张你想要处理的图像文件（`input.png`），任意常见格式——PNG、JPG、BMP 都可以

就这些。如果缺少任何一项，请立即获取；后续教程默认这些已经就绪。

## 第一步：安装 Aspose.OCR NuGet 包

首先——将库添加到项目中。在项目文件夹的终端运行：

```bash
dotnet add package Aspose.OCR
```

这会拉取最新版本（截至 2026 年 4 月为 23.12），并将必要的 DLL 添加到 `bin` 文件夹。无需额外配置。

## 第二步：初始化 OCR 引擎（对图像执行 OCR）

现在我们创建一个 `OcrEngine` 实例，并指定使用的语言。英语（`"en"`）是最常用的，你也可以换成 `"fr"`、`"de"` 或任何受支持的语言。

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**为什么在这里初始化：** `OcrEngine` 包含识别过程所需的所有配置。提前设置语言可确保引擎使用正确的字符集，从而显著提升准确率。

## 第三步：识别图像并获取置信度

引擎准备好后，我们将图像文件传入。`RecognizeImage` 方法返回一个 `OcrResult` 对象，里面包含提取的文本以及每个单词的置信度分数。

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**内部到底发生了什么？** Aspose 使用基于神经网络的识别器，分析每个像素块，将其与语言模型匹配，并附加一个置信度值（0‑100），告诉你对每个单词的确信程度。

## 第四步：将结果转换为 JSON（OCR Image to JSON）

Aspose 让转换变得毫不费力。通过传入 `includeConfidence: true`，我们得到的 JSON 负载如下所示：

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

下面的代码生成了 JSON 字符串：

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**为什么要包含置信度？** 如果你计划将数据传递给下游流程（例如验证、UI 高亮），了解哪些单词不够可靠可以让你决定是否需要让用户确认。

## 第五步：写入 JSON 文件 C#‑风格

现在我们真正 **写 JSON 文件 C#**。`File.WriteAllText` 方法是原子操作，跨平台工作，非常适合控制台应用。

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

这就是完整的工作流——五个简洁步骤即可 **对图像执行 OCR**、将输出转为 JSON 并持久化。

## 完整示例代码

下面是可以直接复制到 `Program.cs` 的完整程序。确保 `input.png` 与编译后的二进制文件位于同一文件夹，或相应调整路径。

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### 预期输出

运行程序（`dotnet run`）后，你会看到类似如下的输出：

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

而 `output.json` 将包含前面展示的结构化 JSON，且每个单词都有置信度百分比。

## 专业技巧与边缘情况

- **文件缺失处理：** 如果路径可能是动态的，请在 `RecognizeImage` 调用外层使用 `try/catch` 捕获 `FileNotFoundException`。
- **不同语言：** 将 `ocrEngine.Language = "fr"` 设置为法语，或通过 `ocrEngine.LoadLanguage("custom.lang")` 加载自定义语言包。
- **大文档：** 对于多页 PDF，先使用 `Aspose.PDF` 将每页转换为图像，然后循环执行 OCR 步骤。
- **性能调优：** 若只需快速结果，可切换到 `RecognitionMode.Fast`——会略微降低准确度，但提升速度。
- **JSON 格式化：** 想要美化的 JSON？在反序列化 Aspose 的 JSON 字符串后，使用 Newtonsoft 的 `JsonConvert.SerializeObject` 并传入 `Formatting.Indented`。

## 常见问题

**Q: 这在 .NET Framework 上能工作吗？**  
A: 当然可以。相同的 NuGet 包目标为 .NET Standard 2.0，因而可以在 .NET Framework 4.6.1 及以上版本中引用。

**Q: 如果我需要整篇文档的整体置信度，而不是每个单词的置信度怎么办？**  
A: `OcrResult` 还提供 `OverallConfidence`。你可以手动将其加入 JSON：

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**Q: 能否直接将 JSON 流式发送到 Web API？**  
A: 可以。将 `File.WriteAllText` 替换为使用 `HttpClient` 的 POST 请求，发送 `jsonResult` 即可。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}