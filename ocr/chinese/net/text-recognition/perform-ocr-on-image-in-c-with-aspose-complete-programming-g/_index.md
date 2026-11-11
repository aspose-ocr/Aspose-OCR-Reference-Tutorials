---
category: general
date: 2026-06-16
description: 使用 Aspose OCR 在 C# 中对图像进行 OCR。一步一步学习如何获取 JSON 结果、处理文件以及排除常见问题。
draft: false
keywords:
- perform OCR on image
- Aspose OCR C#
- JSON result handling
- C# image recognition
- OCR engine configuration
language: zh
og_description: 使用 Aspose OCR 在 C# 中对图像进行 OCR。本指南将带您了解 JSON 输出、引擎设置及实用技巧。
og_title: 在 C# 中对图像进行 OCR – 完整的 Aspose OCR 教程
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Perform OCR on image using Aspose OCR in C#. Learn step‑by‑step how
    to get JSON results, handle files, and troubleshoot common issues.
  headline: Perform OCR on Image in C# with Aspose – Complete Programming Guide
  type: TechArticle
- questions:
  - answer: Aspose.OCR handles PNG, JPEG, BMP, TIFF, and GIF. If you need to work
      with PDFs, convert each page to an image first (Aspose.PDF can help).
    question: What image formats are supported?
  - answer: Yes – set `ocrEngine.Settings.ResultFormat = ResultFormat.Text;`. JSON
      is preferred when you need more metadata.
    question: Can I get plain text instead of JSON?
  - answer: Feed each page image to `RecognizeImage` in a loop and concatenate the
      results, or use `RecognizePdf` which returns a combined JSON structure.
    question: How do I handle multi‑page documents?
  - answer: For batch processing, reuse a single `OcrEngine` instance rather than
      creating a new one per image. Also, enable `RecognitionMode.Fast` if accuracy
      can be traded for speed.
    question: Performance concerns?
  - answer: Without a license, the output JSON will include a watermark field. Apply
      your license early in `Main` with `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.
    question: License warnings?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: 使用 Aspose 在 C# 中对图像执行 OCR – 完整编程指南
url: /zh/net/text-recognition/perform-ocr-on-image-in-c-with-aspose-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中对图像执行 OCR – 完整编程指南

是否曾需要**对图像文件执行 OCR**，却不确定如何将原始像素转换为可用文本？你并不孤单。无论是扫描收据、从护照中提取数据，还是数字化旧文档，能够以编程方式**对图像执行 OCR**对任何 .NET 开发者来说都是改变游戏规则的利器。

在本教程中，我们将通过一个动手示例，展示如何使用 Aspose.OCR 库**对图像执行 OCR**，将结果捕获为 JSON，并将其保存以供后续处理。完成后，你将拥有一个可直接运行的控制台应用程序、每个配置步骤的清晰解释，以及避免常见陷阱的若干专业技巧。

## 前置条件

在开始之前，请确保你具备以下条件：

- 已安装 .NET 6.0 SDK 或更高版本（可从 Microsoft 官网下载）。  
- 有效的 Aspose.OCR 许可证或免费试用版——库在没有许可证的情况下仍可使用，但会添加水印。  
- 一张你想要**对图像执行 OCR**的图片文件（PNG、JPEG 或 TIFF），本指南使用 `receipt.png` 作为示例。  
- Visual Studio 2022、VS Code 或任意你喜欢的编辑器。

除 `Aspose.OCR` 之外，无需其他 NuGet 包。

## 第一步：创建项目并安装 Aspose.OCR

首先，创建一个新的控制台项目并引入 OCR 库。

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

> **专业提示：** 如果你使用 Visual Studio，可以通过 NuGet 包管理器 UI 添加该包。它会自动恢复依赖，省去后续手动执行 `dotnet restore` 的步骤。

现在打开 `Program.cs`——我们将用实际**对图像执行 OCR**的代码替换其内容。

## 第二步：创建并配置 OCR 引擎

任何 Aspose OCR 工作流的核心都是 `OcrEngine` 类。下面我们实例化它，并将引擎的输出格式设置为 JSON——这种格式后续解析非常方便。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonResultDemo
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2.2: Tell the engine we want JSON output.
        ocrEngine.Settings.ResultFormat = ResultFormat.Json;

        // Optional: tweak language or recognition speed.
        // ocrEngine.Settings.Language = Language.English; // default is English
        // ocrEngine.Settings.RecognitionMode = RecognitionMode.Fast; // or Accurate
```

**为什么将 `ResultFormat` 设置为 JSON？**  
JSON 与语言无关，可在 C#、JavaScript、Python 或任何你可能集成的环境中反序列化为强类型对象。它还保留置信度分数和边界框坐标，便于后续验证。

## 第三步：对图像执行 OCR 并捕获 JSON

引擎准备就绪后，我们通过调用 `RecognizeImage` 实际**对图像执行 OCR**。该方法返回包含 JSON 负载的字符串。

```csharp
        // Step 3: Perform OCR on the image and capture the JSON output.
        // Replace the path with the location of your own image file.
        string imagePath = "YOUR_DIRECTORY/receipt.png";
        string jsonResult = ocrEngine.RecognizeImage(imagePath);
```

> **边缘情况：** 如果图像损坏或路径错误，`RecognizeImage` 会抛出 `FileNotFoundException`。如需优雅的错误处理，请将调用包装在 `try/catch` 块中。

## 第四步：保存 JSON 结果以便后续处理

将 OCR 输出保存下来，可让你后续将其写入数据库、API 或 UI 组件。下面是一种直接将 JSON 写入磁盘的简洁方式。

```csharp
        // Step 4: Save the JSON result for later use.
        string outputPath = "YOUR_DIRECTORY/receipt.json";
        File.WriteAllText(outputPath, jsonResult);
```

如果你在云环境中工作，可以将 `File.WriteAllText` 替换为 Azure Blob Storage 或 AWS S3 的调用——JSON 字符串的使用方式保持不变。

## 第五步：通知用户并清理

一条简短的控制台消息确认所有操作成功。在真实项目中，你可能会将其记录到文件或发送到监控服务。

```csharp
        // Step 5: Inform the user that the JSON file has been saved.
        Console.WriteLine("JSON result saved to " + outputPath);
    }
}
```

这就是完整流程！使用 `dotnet run` 运行程序，你应当看到确认信息，并在同目录下生成一个 `receipt.json` 文件，内容类似于：

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $23.45",
          "Confidence": 0.98,
          "Rectangle": { "X": 120, "Y": 340, "Width": 150, "Height": 20 }
        }
      ]
    }
  ]
}
```

## 完整可运行示例

为确保完整，这里提供可以直接复制粘贴到 `Program.cs` 的*完整*文件。没有任何缺失。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonResultDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2: Configure the engine to return results in JSON format.
        ocrEngine.Settings.ResultFormat = ResultFormat.Json;

        // Optional: adjust language or recognition mode if needed.
        // ocrEngine.Settings.Language = Language.English;
        // ocrEngine.Settings.RecognitionMode = RecognitionMode.Accurate;

        // Step 3: Perform OCR on the image and capture the JSON output.
        string imagePath = "YOUR_DIRECTORY/receipt.png";
        string jsonResult = ocrEngine.RecognizeImage(imagePath);

        // Step 4: Save the JSON result for further processing.
        string outputPath = "YOUR_DIRECTORY/receipt.json";
        File.WriteAllText(outputPath, jsonResult);

        // Step 5: Notify that the JSON file has been saved.
        Console.WriteLine($"JSON result saved to {outputPath}");
    }
}
```

> **提示：** 将 `YOUR_DIRECTORY` 替换为绝对路径或基于项目根目录的相对路径。使用 `Path.Combine(Environment.CurrentDirectory, "receipt.png")` 可以避免在 Windows 与 Linux 上硬编码分隔符的问题。

## 常见问题与注意事项

- **支持哪些图像格式？**  
  Aspose.OCR 支持 PNG、JPEG、BMP、TIFF 和 GIF。如果需要处理 PDF，请先将每页转换为图像（可使用 Aspose.PDF）。

- **可以只获取纯文本而不是 JSON 吗？**  
  可以——将 `ocrEngine.Settings.ResultFormat = ResultFormat.Text;`。当只需要文本而不需要元数据时，可使用纯文本。

- **如何处理多页文档？**  
  在循环中对每页图像调用 `RecognizeImage` 并拼接结果，或使用 `RecognizePdf`，它会返回合并后的 JSON 结构。

- **性能方面的考虑？**  
  对于批量处理，复用同一个 `OcrEngine` 实例，而不是为每张图像创建新实例。同时，如果可以在精度与速度之间做权衡，可启用 `RecognitionMode.Fast`。

- **许可证警告？**  
  未使用许可证时，输出的 JSON 将包含水印字段。请在 `Main` 方法开头尽早加载许可证：`License license = new License(); license.SetLicense("Aspose.OCR.lic");`。

## 可视化概览

下面是一张快速示意图，展示了从图像文件 → OCR 引擎 → JSON 输出 → 存储的整体数据流。帮助你了解每一步在更大管道中的位置。

![Perform OCR on Image workflow diagram](https://example.com/ocr-workflow.png "Perform OCR on Image")

*Alt text: Diagram showing how to perform OCR on image using Aspose OCR, converting to JSON and saving to file.*

## 扩展示例

现在你已经掌握了如何**对图像执行 OCR**并获取 JSON 负载，接下来可以考虑：

- 使用 `System.Text.Json` 或 `Newtonsoft.Json` **解析 JSON**，提取特定字段。  
- **将文本插入数据库**，实现可搜索的档案。  
- **集成 Web API**，让客户端上传图像并即时返回 OCR 结果。  
- 使用 `Aspose.Imaging` 对图像进行**预处理**（去倾斜、增强对比度），提升识别准确率。

上述所有主题都基于我们已经搭建的基础，`OcrEngine` 实例可以在它们之间复用。

## 结论

你已经学会了如何在 C# 中使用 Aspose OCR **对图像执行 OCR**，配置引擎以 JSON 输出，并将结果持久化以供后续使用。教程覆盖了每一行代码，解释了每个设置的意义，并指出了生产环境中可能遇到的边缘情况。

接下来，你可以尝试不同的语言（`ocrEngine.Settings.Language`），调整 `RecognitionMode`，或将 JSON 接入下游分析管道。当可靠的 OCR 与现代 .NET 工具相结合时，可能性无限。

如果本指南对你有帮助，请考虑给 Aspose.OCR 的 GitHub 仓库加星，分享本文给团队成员，或在评论中留下你的技巧。祝编码愉快！


## 接下来你可以学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你在自己的项目中进一步探索 API 功能和替代实现方式，每篇都提供完整可运行的代码示例和逐步解释。

- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}