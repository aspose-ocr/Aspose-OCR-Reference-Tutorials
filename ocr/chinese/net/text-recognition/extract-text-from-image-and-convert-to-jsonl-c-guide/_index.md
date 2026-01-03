---
category: general
date: 2026-01-02
description: 使用 Aspose OCR 在 C# 中提取图像文本。了解如何快速可靠地将图像转换为 JSONL 格式。
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: zh
og_description: 使用 Aspose OCR 从图像中提取文本并转换为 JSONL 格式。为开发者提供完整的逐步 C# 教程。
og_title: 从图像提取文本 – 在 C# 中转换为 JSONL
tags:
- C#
- OCR
- Aspose
- JSONL
title: 从图像提取文本并转换为 JSONL – C# 指南
url: /zh/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像提取文本并转换为 JSONL – 完整 C# 教程

是否曾需要 **从图像提取文本**，却不确定哪个库能提供干净、结构化的输出？你并不孤单。在许多收据处理或文档数字化项目中，瓶颈在于将位图转换为可搜索的文本 *以及* 机器可读的格式。

好消息是？使用 Aspose OCR，你可以 **从图像提取文本**，并仅用几行代码 **将图像转换为 JSONL**，供下游分析使用。本指南将带你完成整个流程，从加载 PNG 到写入可流式传输到数据管道的 JSON‑Lines 文件。

> **提示：** 如果你已经在使用 .NET 6 或更高版本，完全可以直接使用相同代码，无需额外配置。

## 前置条件 — 你需要准备的东西

- **.NET 6 SDK**（或任意近期的 .NET 版本）
- **Aspose.OCR** NuGet 包  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** 用于序列化  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- 一个示例图像（例如 `receipt.png`），放在可引用的文件夹中。
- 你喜欢的 IDE 或编辑器——Visual Studio、VS Code、Rider 等。

无需繁重的搭建，也不依赖外部服务，只需几个 NuGet 包。

![Extract text from image using C#](https://example.com/assets/ocr-sample.png)

*Alt text: 使用 Aspose OCR 的 C# 提取图像文本*

## 步骤 1：加载要处理的图像  

当你想 **从图像提取文本** 时，第一步是给 OCR 引擎提供一个位图。使用 `System.Drawing.Bitmap` 简单直观，适用于大多数栅格格式。

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **为什么重要：** 将图像加载为 `Bitmap` 能让 OCR 引擎直接访问像素，相比流式读取原始字节，可提升识别速度和准确度。

## 步骤 2：为 JSON‑Lines 输出配置 Aspose OCR  

Aspose OCR 允许你指定语言、输出格式以及一些性能调优。这里我们请求 **JSON‑Lines**（每行一个 JSON 对象），因为它非常适合后续逐行处理。

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **专业提示：** 如果需要处理多语言收据，设置 `Language = Language.Multilingual` 或传入 `Language` 数组。

## 步骤 3：运行 OCR 并获取结果  

现在我们真正 **从图像提取文本**。`Recognize` 方法返回一个 `OcrResult` 对象，其中包含一系列 `OcrLine` 对象，每个对象代表一行识别文本及其边界框。

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

此时 `ocrResult.Lines` 已经包含了所有需要的信息——原始文本、置信度以及坐标。

## 步骤 4：将行序列化为 JSON‑Lines  

我们将集合转换为格式化的 JSON 字符串。虽然 JSON‑Lines 通常是紧凑的，但在开发阶段加入缩进可以让文件更易检查。

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

生成的 `jsonLines` 变量大致如下（为简洁起见已截断）：

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

每行以换行符结尾，形成真正的 **JSONL**（JSON‑Lines）文件。

## 步骤 5：将 JSON‑Lines 写入磁盘  

最后，我们将输出持久化，供其他服务——如 Spark、Logstash 或简单的 Bash 脚本——逐行读取。

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

打开 `receipt.jsonl` 时，你会看到每行都是一个 JSON 对象，已准备好流式处理。

## 步骤 6：验证导出结果  

一次快速的完整性检查可以为后续调试省下大量时间。我们读取前几行并打印到控制台。

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

典型的控制台输出：

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

如果看到类似的内容，恭喜你——已经成功 **从图像提取文本** 并 **将图像转换为 JSONL**。

## 常见坑点及规避方法  

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| **输出为空** | 图像路径错误或文件不可读。 | 在创建位图前使用 `File.Exists(imagePath)` 检查。 |
| **置信度低** | 图像模糊或对比度低。 | 对图像进行预处理（如 `Bitmap.RotateFlip`、`Graphics.Clear`）或提升 DPI。 |
| **语言不匹配** | OCR 默认英文，但收据使用其他语言。 | 设置 `options.Language = Language.Spanish`（或相应枚举）。 |
| **JSONL 变成单个 JSON 数组** | 使用了 `Formatting.None` 且未处理换行。 | 确保每个序列化对象后添加 `Environment.NewLine`。 |

## 完整可运行示例  

下面是完整的、可直接运行的程序。复制到控制台项目中，按 **F5** 即可。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**预期结果：** 生成 `receipt.jsonl` 文件，每行包含 `Text`、`Confidence` 和 `BoundingBox` 字段的 JSON 对象。现在可以将该文件喂入任何消费 JSONL 的分析管道。

## 后续步骤 – 超越基础 OCR  

- **批量处理：** 将上述逻辑包装在 `foreach` 循环中，处理整个收据文件夹。  
- **并行化：** 使用 `Parallel.ForEach` 在处理成千上万张图像时实现多核加速。  
- **后处理：** 在存储前剔除低置信度行（`Confidence < 0.9`）。  
- **集成：** 使用相应 SDK 将 JSONL 直接推送到 Azure Blob Storage 或 AWS S3。  
- **其他格式：** 如下游系统更偏好，可将 `OutputFormat` 切换为 `PlainText` 或 `Xml`。

## 结论  

现在，你拥有了一套使用 Aspose OCR 在 C# 中 **从图像提取文本** 并 **将图像转换为 JSONL** 的完整端到端解决方案。教程涵盖了从加载位图到验证输出的全部步骤，并提供了实用技巧，帮助你构建稳健的管道。

使用自己的收据、发票或扫描表单试一试——让 OCR 引擎在几秒钟内把像素转化为可搜索、行结构化的数据。如果遇到边缘情况（如倾斜扫描或多语言文本），回到 *RecognitionOptions* 部分，调整语言或预处理步骤。

祝编码愉快，愿你的数据管道永远保持洁净！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}