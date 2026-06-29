---
category: general
date: 2026-06-28
description: 使用 Aspose.OCR 在 C# 中对图像执行 OCR。学习如何识别图像中的文本、从发票中提取文本、加载图像进行 OCR 并将 JSON
  写入文件。
draft: false
keywords:
- perform OCR on image
- recognize text from image
- write JSON to file
- extract text from invoice
- load image for OCR
language: zh
og_description: 使用 Aspose.OCR 在 C# 中对图像执行 OCR。本指南展示了如何识别图像中的文本、提取发票中的文本并将 JSON 写入文件。
og_title: 在 C# 中对图像进行 OCR – Aspose OCR 教程
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Perform OCR on image using Aspose.OCR in C#. Learn to recognize text
    from image, extract text from invoice, load image for OCR and write JSON to file.
  headline: Perform OCR on Image in C# – Complete Aspose Guide
  type: TechArticle
- description: Perform OCR on image using Aspose.OCR in C#. Learn to recognize text
    from image, extract text from invoice, load image for OCR and write JSON to file.
  name: Perform OCR on Image in C# – Complete Aspose Guide
  steps:
  - name: What if the image contains multiple languages?
    text: 'Aspose.OCR automatically detects the language based on the character set.
      If you need to force a specific language (e.g., English for most invoices),
      set the `Language` property on the engine:'
  - name: How do I handle large PDFs with many pages?
    text: Convert each page to an image first (using a PDF‑to‑image library) and then
      loop through the images, applying the same **perform OCR on image** routine.
      Aggregate the JSON results into a single array if you want a consolidated output.
  - name: Can I stream the JSON instead of writing a whole file?
    text: 'Yes. If you’re building a web API, you can return `json` directly as the
      response body:'
  - name: What about performance?
    text: The OCR engine runs synchronously in the example above. For high‑throughput
      scenarios, wrap the recognition call in `Task.Run` or use the asynchronous versions
      (if available) to keep your UI responsive or to parallelize batch processing.
  type: HowTo
tags:
- Aspose.OCR
- C#
- JSON
- ImageProcessing
title: 在 C# 中对图像执行 OCR – 完整的 Aspose 指南
url: /zh/net/text-recognition/perform-ocr-on-image-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中对图像执行 OCR – 完整 Aspose 指南

是否曾需要 **perform OCR on image** 文件，却不确定哪个 .NET 库能够提供干净、结构化的结果？你并不孤单——开发者经常询问如何 **recognize text from image** 资源，尤其是在处理发票或收据时。在本教程中，我们将通过一个动手示例，演示如何 **load image for OCR**、**extract text from invoice** 并 **write JSON to file** 以供后续处理。

阅读完本指南后，你将拥有一个可直接运行的控制台应用程序，它能够：

* 实例化 Aspose OCR 引擎，
* 加载 PNG（或 JPG）图像，
* 识别文本内容，
* 将结果序列化为格式化的 JSON，
* 将该 JSON 保存到磁盘。

无需外部服务，无隐藏魔法——仅仅是可以复制、粘贴并运行的纯 C# 代码。

## 前置条件

在开始之前，请确保你拥有：

* .NET 6 SDK 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）。
* 有效的 Aspose.OCR 许可证或临时评估密钥（免费试用可用于测试）。
* Visual Studio 2022、VS Code 或任意你喜欢的 IDE。
* 一张图像文件，例如 `invoice.png`，放置在可以通过完整或相对路径引用的位置。

> **专业提示：** 如果你处理的是扫描的发票，建议在将图像送入 OCR 引擎之前进行预处理（去倾斜、提升对比度）。Aspose.OCR 会自动处理许多步骤，但干净的源图像始终能获得更好的结果。

---

## 第 1 步：设置项目并安装 Aspose.OCR

首先，创建一个新的控制台项目并引入 Aspose.OCR NuGet 包。

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
dotnet add package Aspose.OCR
```

> **为什么这一步很重要：** `Aspose.OCR` 程序集提供了我们将要使用的 `OcrEngine` 类，以 **perform OCR on image** 数据。没有此包，编译器将无法识别任何 OCR 相关的类型。

---

## 第 2 步：加载图像进行 OCR

接下来，我们编写代码来 **load image for OCR**。`OcrImage.FromFile` 方法接受绝对或相对路径，并将位图包装成引擎可理解的格式。

```csharp
using Aspose.OCR;
using System.IO;

// Replace with the actual path to your invoice image
string imagePath = @"YOUR_DIRECTORY\invoice.png";

// Step 2: Load the image
OcrImage image = OcrImage.FromFile(imagePath);
```

> **说明：** 将路径单独存入变量可以保持代码整洁，并且在后续（例如日志或调试）需要引用同一图像时更加方便。如果文件未找到，`FromFile` 会抛出 `FileNotFoundException`，你可以捕获它并给出友好的错误提示。

---

## 第 3 步：对图像执行 OCR 并识别文本

拥有图像后，我们创建 `OcrEngine` 实例并让它 **recognize text from image**。这一步是本教程的核心——真正的 OCR 魔法在此发生。

```csharp
// Step 3: Create OCR engine and recognize text
using var ocrEngine = new OcrEngine();   // IDisposable, so we use 'using'
OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **为什么使用 `using var`：** `OcrEngine` 持有非托管资源（本机库）。将其放在 `using` 块中可确保正确释放，防止内存泄漏——在长时间运行的服务中尤为重要。

> **返回内容：** `ocrResult` 包含原始文本、置信度分数以及布局信息（行、词、边界框）。对于大多数发票处理流水线来说，`Text` 属性已足够使用，但额外的元数据可用于校验或可视化调试。

---

## 第 4 步：将结果转换为格式化的 JSON

Aspose.OCR 通过 `OcrResult` 的 `ToJson` 方法让 **write JSON to file** 变得非常简单。传入 `indent: true` 即可得到人类可读的输出，这在后续 **extract text from invoice** 时非常便利。

```csharp
// Step 4: Serialize OCR result to JSON
string json = ocrResult.ToJson(indent: true);
```

> **示例 JSON 片段**（为简洁起见已截断）：

```json
{
  "Text": "Invoice #12345\nDate: 2026-06-01\nTotal: $1,250.00",
  "Confidence": 0.97,
  "Regions": [...]
}
```

> **边缘情况说明：** 如果 OCR 引擎未检测到任何文本，`ocrResult.Text` 将为空字符串，但 JSON 仍会包含图像尺寸等元数据。写文件前可先检查结果是否为空，以避免生成无效文件。

---

## 第 5 步：将 JSON 写入文件

现在我们终于 **write JSON to file**。使用 `File.WriteAllText` 可确保一次性原子写入整个字符串。

```csharp
// Step 5: Save JSON output
string jsonPath = @"YOUR_DIRECTORY\invoice.json";
File.WriteAllText(jsonPath, json);
Console.WriteLine($"JSON saved to {jsonPath}");
```

> **生产环境提示：** 考虑在文件名中追加时间戳（如 `invoice_20260628_1500.json`），以避免覆盖之前的结果。同时，建议将写入操作放在 try/catch 中，以优雅地处理权限问题。

---

## 第 6 步：完整工作示例

将所有代码片段组合起来，下面就是可以直接编译运行的完整程序。将 `YOUR_DIRECTORY` 替换为包含 `invoice.png` 的文件夹路径。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        using var ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        string imagePath = @"YOUR_DIRECTORY\invoice.png";
        OcrImage image = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR and recognize text from image
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 4: Convert the recognition result to pretty‑printed JSON
        string json = ocrResult.ToJson(indent: true);

        // Step 5: Write JSON to file
        string jsonPath = @"YOUR_DIRECTORY\invoice.json";
        File.WriteAllText(jsonPath, json);

        // Step 6: Inform the user
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

**预期输出** 当你运行程序时：

```
JSON saved to C:\Invoices\invoice.json
```

打开 `invoice.json`，你将看到格式良好的 OCR 数据表示，已准备好进行下游解析或存储。

---

## 常见问题与边缘情况

### 如果图像包含多种语言怎么办？

Aspose.OCR 会根据字符集自动检测语言。如果需要强制指定语言（例如大多数发票使用英文），请在引擎上设置 `Language` 属性：

```csharp
ocrEngine.Language = OcrLanguage.English;
```

### 如何处理包含多页的大型 PDF？

先使用 PDF‑to‑image 库将每页转换为图像，然后遍历这些图像，使用相同的 **perform OCR on image** 例程。若希望得到统一的输出，可将各页的 JSON 结果聚合为一个数组。

### 能否在写入完整文件之前直接流式返回 JSON？

可以。如果你在构建 Web API，只需直接将 `json` 作为响应体返回：

```csharp
return Results.Json(ocrResult);
```

### 性能方面有什么建议？

示例中的 OCR 引擎是同步调用。对于高吞吐场景，可将识别调用包装在 `Task.Run` 中，或使用异步版本（若有）来保持 UI 响应或并行处理批量任务。

---

## 结论

我们已经完整演示了一个端到端的解决方案，能够 **perform OCR on image** 文件、**recognize text from image**、**extract text from invoice**，并最终使用 Aspose.OCR 在 C# 中 **write JSON to file**。代码故意保持简洁，便于你根据更复杂的工作流进行扩展——无论是添加图像预处理、将 JSON 写入数据库，还是通过 REST 接口暴露结果。

准备好下一步了吗？尝试将 PNG 换成 JPEG，实验不同的 OCR 设置（如 `ocrEngine.Dpi`），或集成 PDF‑to‑image 步骤以处理整批发票。掌握基础后，可能性无限。

祝编码愉快，愿你的 OCR 结果始终清晰精准！

## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并探索项目中的替代实现方式。

- [如何在图像识别中使用 Aspose OCR 获取 JSON 结果](/ocr/english/net/text-recognition/get-result-as-json/)
- [使用 Aspose.OCR 在 C# 中提取图像文本并选择语言](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [从图像中提取文本 – 使用 Aspose.OCR 识别行](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}