---
category: general
date: 2025-12-30
description: 学习如何使用 C# 从图像中提取 OCR 文本。本教程涵盖从图像文件提取文本、读取 PNG 文本，并提供完整的 C# OCR 教程。
draft: false
keywords:
- how to extract ocr
- extract text from image
- read text from png
- c# ocr tutorial
language: zh
og_description: 如何使用 C# 从图像中提取 OCR 文本。遵循此 C# OCR 教程，轻松读取 PNG 文件中的文字并从图像中提取文本。
og_title: 如何在 C# 中提取 OCR 文本 – 完整指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中提取 OCR 文本 – 完整的逐步指南
url: /zh/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中提取 OCR 文本 – 完整分步指南

有没有想过 **如何提取 OCR**，在不花费数小时编写自定义解析器的情况下，从扫描表单中获取文本？你并不是唯一有此困惑的人。在许多真实项目中——比如发票处理、护照扫描或旧档案数字化——你都需要一种可靠的方法，从图像文件中提取文字。好消息是？使用 Aspose.OCR，只需几行 C# 代码即可实现。

在本教程中，我们将演示一个 **c# ocr tutorial**，展示如何 **extract text from image**（以 PNG 为例），以及如何 **read text from png** 并保留每个字符的元数据。完成后，你将拥有一个可直接运行的控制台应用程序，打印出包含 Aspose 捕获的所有信息的格式化 JSON 字符串。

> **先决条件**  
> • 已安装 .NET 6.0 或更高版本  
> • Visual Studio 2022（或你喜欢的任何 IDE）  
> • Aspose.OCR for .NET NuGet 包（`Aspose.OCR`）  

如果你已经满足上述条件，让我们开始吧。

---

## 如何在 C# 中提取图像 OCR 文本 – 项目设置

在开始编写代码之前，我们需要一个干净的项目以及正确的依赖。

```bash
# Create a new console app
dotnet new console -n OcrDemo
cd OcrDemo

# Add Aspose.OCR package
dotnet add package Aspose.OCR
```

> **专业提示：** 如果你使用 Visual Studio，可以通过 NuGet 包管理器 UI 添加包——只需搜索 “Aspose.OCR”。

安装包后，打开 `Program.cs`。你会看到默认的 `Main` 方法，准备好填入代码。

---

## 第一步 – 初始化 OCR 引擎（为何重要）

OCR 引擎是整个过程的核心。初始化它可以告诉 Aspose 你后续将使用的语言模型。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance
            var ocrEngine = new OcrEngine();

            // The rest of the steps will follow here...
        }
    }
}
```

*为何需要这一步？*  
创建 `OcrEngine` 对象会分配进行图像分析所需的资源。没有它，你就没有可以输入图像的对象，库也无法应用其复杂的模式识别算法。

---

## 第二步 – 加载英文语言模型（从图像提取文本）

Aspose 附带多个语言包。加载正确的语言模型可以显著提升准确率。

```csharp
// Step 2: Load the English language model
ocrEngine.LoadLanguage(LanguageModel.English);
```

如果你需要 **read text from png** 并且其中包含其他语言，只需将 `LanguageModel.English` 替换为相应的枚举值（例如 `LanguageModel.French`）。这种灵活性正是 Aspose 在全球化应用中受欢迎的原因。

---

## 第三步 – 识别 PNG 文件中的文本（从 PNG 读取文本）

现在我们把引擎指向实际的图像。演示时，请将名为 `form_image.png` 的 PNG 放在相对于可执行文件的 `YOUR_DIRECTORY` 文件夹中。

```csharp
// Step 3: Perform OCR on the image
var recognitionResult = ocrEngine.Recognize("YOUR_DIRECTORY/form_image.png");
```

> **如果文件未找到会怎样？**  
> `Recognize` 方法会抛出 `FileNotFoundException`。在生产环境中，你可以将调用包装在 try‑catch 块中，以实现优雅的错误处理。

---

## 第四步 – 将结果转换为美化的 JSON（为何使用 JSON？）

Aspose 返回一个丰富的 `RecognitionResult` 对象，除了纯文本外，还包含边界框、置信度分数和行信息。序列化为 JSON 便于记录、存储或通过 API 发送。

```csharp
// Step 4: Serialize the result to a nicely indented JSON string
string json = JsonResult.FromRecognitionResult(recognitionResult)
                        .ToString(prettyPrint: true);

// Optional: Write the JSON to a file for later inspection
System.IO.File.WriteAllText("ocr_output.json", json);
```

`prettyPrint: true` 标志会添加换行和缩进，非常适合调试。如果你只需要原始文本，可以直接使用 `recognitionResult.Text`。

---

## 第五步 – 显示 JSON 输出（查看结果）

最后，将 JSON 打印到控制台，以便验证一切正常。

```csharp
// Step 5: Output the JSON to the console
Console.WriteLine(json);
```

运行程序后，输出应类似于下面的片段（为简洁起见已截断）：

```json
{
  "Text": "John Doe\n123 Main St\nAnytown, USA",
  "Characters": [
    {
      "Value": "J",
      "Confidence": 0.99,
      "Bounds": { "X": 12, "Y": 8, "Width": 10, "Height": 14 }
    },
    // ... more character objects ...
  ],
  "Lines": [
    { "Text": "John Doe", "Confidence": 0.98 },
    { "Text": "123 Main St", "Confidence": 0.97 },
    { "Text": "Anytown, USA", "Confidence": 0.96 }
  ]
}
```

请注意每个字符的元数据——这正是 Aspose 相较于许多免费 OCR 库提供的额外价值。现在，你可以过滤低置信度字符，或将文本映射回原始图像进行高亮显示。

---

## 完整工作示例（一步到位）

下面是完整的、可直接复制粘贴的程序代码，确保没有遗漏。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Step 2: Load the English language model
            ocrEngine.LoadLanguage(LanguageModel.English);

            // Step 3: Recognize text from the PNG image
            var recognitionResult = ocrEngine.Recognize("YOUR_DIRECTORY/form_image.png");

            // Step 4: Convert the result to pretty‑printed JSON
            string json = JsonResult.FromRecognitionResult(recognitionResult)
                                    .ToString(prettyPrint: true);

            // Optional: Save JSON to a file
            System.IO.File.WriteAllText("ocr_output.json", json);

            // Step 5: Display the JSON output
            Console.WriteLine(json);
        }
    }
}
```

将其保存为 `Program.cs`，放入你的 PNG，运行 `dotnet run`，即可在控制台看到打印的 JSON。

---

## 常见问题与边缘情况（解答 “如果……”）

### 如果图像是 JPEG 而不是 PNG？

`Recognize` 方法接受 Aspose 支持的任何格式（JPEG、BMP、TIFF 等）。只需在路径中更改文件扩展名即可。

### 如何提升低分辨率扫描的准确度？

1. **预处理图像** – 增加对比度、转换为灰度或使用锐化滤镜。  
2. **使用更高分辨率的源文件** – OCR 引擎通常需要至少 300 dpi 才能获得可靠结果。  
3. **启用自动旋转** – 在识别前调用 `ocrEngine.AutoRotate = true;`。

### 能否仅提取纯文本而不生成 JSON？

可以。识别后，只需读取 `recognitionResult.Text`：

```csharp
Console.WriteLine(recognitionResult.Text);
```

### 是否有办法从多页 PDF 中提取文本？

Aspose.OCR 只能处理图像，但你可以结合 Aspose.PDF 将每页 PDF 栅格化为图像，然后在循环中将这些图像喂给 OCR 引擎。

---

## 稳健的 c# OCR 教程的专业技巧

- **释放引擎资源**：如果要处理大量图像，请在 `using` 块中包装 `OcrEngine`，及时释放本机资源。  
- **批量处理**：对于大型文件夹，可使用 `Directory.GetFiles` 枚举文件，并在 try‑catch 中逐个处理，防止单个错误导致整个运行中止。  
- **日志记录**：持久化置信度分数；在需要人工审查低质量结果时，这些分数非常有价值。  
- **线程安全**：`OcrEngine` 实例 **不是**线程安全的。如果并行处理，请为每个线程创建独立实例。

---

## 结论

你已经学会了 **如何在 C# 中提取 OCR** 文本。通过初始化 OCR 引擎、加载相应语言模型、识别 PNG 并将结果序列化为美化的 JSON，你现在拥有了任何文档数字化项目的坚实基础。本 **c# ocr tutorial** 同时涵盖了 **extract text from image**、**read text from png** 以及常见的坑点处理。

准备好下一步了吗？尝试将一批扫描发票输入同一流水线，实验不同语言包，或将 JSON 输出集成到可搜索的数据库中。前路无限，而你刚写的代码正是起飞的助推器。

如果本指南对你有帮助，欢迎分享给团队成员、给仓库加星，或在评论区留下你的 OCR 成功案例。祝编码愉快！

![how to extract ocr example](https://example.com/ocr-demo.png "how to extract ocr example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}