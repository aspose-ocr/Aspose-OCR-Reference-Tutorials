---
category: general
date: 2026-03-02
description: 学习如何在使用 Aspose OCR 从图像提取文本的同时保存 JSON。包括写入 JSON 文件的代码、加载位图图像的技巧以及完整的 C#
  示例。
draft: false
keywords:
- how to save json
- extract text from image
- write json file
- how to extract text
- load bitmap image
language: zh
og_description: 了解如何在使用 Aspose OCR 从图像提取文本时保存 JSON。完整的 C# 代码、写入 JSON 文件的步骤以及实用技巧。
og_title: 如何在 C# 中从 OCR 保存 JSON – 完整编程教程
tags:
- C#
- OCR
- Aspose
- JSON
title: 如何在 C# 中从 OCR 保存 JSON – 完整的逐步指南
url: /zh/net/ocr-configuration/how-to-save-json-from-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中保存 OCR 的 JSON – 完整分步指南

是否曾经想过 **如何保存 JSON**，其中包含刚从图片中提取的文本？你并不是唯一有这种困惑的人。许多开发者在需要 *从图像中提取文本* 并将其持久化为整齐的 JSON 文件时会卡住。好消息是？只要准备好合适的组件，解决方案相当直接。

在本教程中，我们将通过一个真实场景演示：使用 Aspose.OCR **从图像中提取文本**，然后 **写入 JSON 文件**，最后 **将 JSON 保存到磁盘**。过程中我们还会展示如何 **正确加载位图图像** 对象，并覆盖一些可能遇到的边缘情况。完成后，你将拥有一个自包含的 C# 控制台应用，能够从加载图片到生成可直接使用的 JSON 文档全部自动化。

## 你需要准备的环境

- .NET 6.0 或更高（代码同样适用于 .NET Core 和 .NET Framework）
- Aspose.OCR for .NET（可获取免费试用的 NuGet 包）
- 包含英文文本的 PNG 或 JPG 示例图片
- Visual Studio、VS Code 或任意支持 C# 的 IDE

不需要额外的库——只需使用标准的 `System.Drawing` 命名空间处理位图，以及 `System.Text.Json` 进行序列化。

---

## 第一步 – 加载位图图像（“load bitmap image” 部分）

在进行任何 OCR 之前，必须先将图像以 `Bitmap` 形式加载到内存中。这相当于在阅读之前先打开一本书。

```csharp
using System.Drawing;

// Replace the placeholder with the actual path to your image file
string imagePath = @"C:\Images\sample-page.png";

// Load the image – this is the “load bitmap image” step
Bitmap bitmapImage = new Bitmap(imagePath);
```

> **小贴士：** 如果图像体积较大，建议先进行缩放以提升性能。OCR 引擎在 2 MB 以下的图像上运行更快。

---

## 第二步 – 配置 Aspose OCR 引擎

位图准备好后，我们需要一个 `OcrEngine`。该对象负责 **从图像中提取文本**，并可选地提供几何信息（如边界框）。

```csharp
using Aspose.OCR;

// Create the OCR engine with English language and enable bounding boxes
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    ExportBoundingBoxes = true // adds geometry info to the result
};
```

为什么要启用 `ExportBoundingBoxes`？如果你需要在 UI 中高亮显示单词，这些坐标非常有价值。如果不需要，可将该标志设为 `false`，生成的 JSON 会更精简。

---

## 第三步 – 执行 OCR 并获取结构化结果

引擎配置完成后，接下来就是实际的 **如何提取文本** 操作。`RecognizeToOcrResult` 方法返回一个丰富的对象，包含识别的文本、置信度分数以及可选的布局数据。

```csharp
// Run OCR – this is the core “how to extract text” call
var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);
```

现在 `ocrResult` 变量中已经包含了所有需要的信息。如果在调试器中检查它，你会看到 `Page`、`Paragraph`、`Line`、`Word` 对象的层级结构，每个对象都有自己的 `Text` 属性。

---

## 第四步 – 将结果序列化为格式化的 JSON 字符串

这里就是 **如何保存 json** 的核心魔法。我们使用 `System.Text.Json`，因为它内置、快速，并且默认支持美化输出。

```csharp
using System.Text.Json;

// Serialize with indentation for readability
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

如果需要不同的命名约定（例如 camelCase），只需在选项中加入 `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` 即可。

---

## 第五步 – 将 JSON 写入磁盘（“write json file” 步骤）

最后，我们真正 **写入 JSON 文件** 到文件系统。这就是在 C# 环境中 **如何保存 json** 的具体实现。

```csharp
using System.IO;

// Choose where you want the JSON output
string jsonPath = @"C:\Images\sample-page.json";

// Save the JSON string – this completes the “how to save json” workflow
File.WriteAllText(jsonPath, jsonResult);
```

此行代码执行完毕后，你将在原始图片旁边看到一个格式良好的 `sample-page.json`。使用任意文本编辑器打开，或将其传递给其他服务——你的 OCR 数据已经可以随处使用。

---

## 第六步 – 验证输出（会看到什么？）

运行程序后，控制台会打印一条简短的确认信息：

```csharp
Console.WriteLine("OCR result saved as JSON.");
```

打开生成的 JSON 文件，你会看到类似如下的内容：

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello, world!",
          "Words": [
            { "Text": "Hello,", "Confidence": 0.99 },
            { "Text": "world!", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

如果 `ExportBoundingBoxes` 为 true，每个单词还会包含 `Rectangle` 坐标。这对于后续的 UI 开发非常便利。

---

## 常见问题与边缘情况

### 如果图片路径无效怎么办？

将位图加载代码放在 `try/catch` 块中，并抛出明确的错误信息：

```csharp
try
{
    Bitmap bitmapImage = new Bitmap(imagePath);
}
catch (FileNotFoundException)
{
    Console.Error.WriteLine($"Image not found: {imagePath}");
    return;
}
```

### 如何处理非英文语言？

只需更改 `Language` 属性：

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Aspose 支持超过 50 种语言，选择与你的源材料相匹配的即可。

### 是否需要手动释放 `Bitmap` 对象？

需要。`Bitmap` 实现了 `IDisposable`，因此请使用 `using` 语句及时释放本机资源。

```csharp
using (Bitmap bitmapImage = new Bitmap(imagePath))
{
    // OCR code here
}
```

### 如果想要紧凑的 JSON（不带缩进）怎么办？

替换 `JsonSerializerOptions`：

```csharp
new JsonSerializerOptions { WriteIndented = false }
```

这样可以减小文件体积——在带宽受限的场景下非常有用。

---

## 完整可运行示例（复制粘贴即用）

下面是整合了所有步骤、错误处理以及最佳实践的完整程序。将其保存为 `Program.cs` 并通过命令行或 IDE 运行。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1 – Load the bitmap image (load bitmap image)
        // -------------------------------------------------
        string imagePath = @"C:\Images\page.png";
        string jsonPath  = @"C:\Images\page.json";

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Error: Image file not found at {imagePath}");
            return;
        }

        using Bitmap bitmapImage = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2 – Configure the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ExportBoundingBoxes = true // optional, adds geometry info
        };

        // -------------------------------------------------
        // Step 3 – Perform OCR (how to extract text)
        // -------------------------------------------------
        var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);

        // -------------------------------------------------
        // Step 4 – Serialize to JSON (how to save json)
        // -------------------------------------------------
        string jsonResult = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true }
        );

        // -------------------------------------------------
        // Step 5 – Write JSON file (write json file)
        // -------------------------------------------------
        try
        {
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"OCR result saved as JSON at {jsonPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to write JSON file: {ex.Message}");
        }
    }
}
```

**该示例实现了：**  
1. 检查图片是否存在。  
2. 使用 `using` 块安全加载图片。  
3. 运行 OCR 以 **从图像中提取文本**。  
4. 将结果序列化为格式化的 JSON 字符串。  
5. 将该字符串保存到磁盘，回答核心问题 **如何保存 json**。

运行 `dotnet run`（或在 Visual Studio 中按 F5），文件写入成功后即可在控制台看到确认信息。

---

## 结论

现在，你已经掌握了一套完整、可投入生产的 **如何保存 JSON** 的方案，整个过程从加载位图图像到写入整洁的 JSON 文件都有详细解释，并阐明了每段代码背后的 “为什么”，方便你在自己的项目中灵活调整。

如果你想进一步探索，可以考虑：

- **如何从 PDF 中提取文本**——先将每页转换为图像再使用 OCR。  
- 利用边界框数据在 WPF 或 WinForms UI 中高亮显示单词。  
- 将 JSON 直接流式传输到 Web API（使用 `HttpClient`），而不是写入本地文件。

动手试一试，调节选项，让 OCR 数据为你的应用提供动力。有什么问题欢迎留言，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}