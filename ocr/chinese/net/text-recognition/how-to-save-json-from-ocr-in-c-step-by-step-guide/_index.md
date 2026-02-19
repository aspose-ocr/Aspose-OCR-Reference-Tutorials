---
category: general
date: 2026-02-19
description: 如何在 C# 中保存 OCR 输出的 JSON —— 学习从图像提取文本、在 C# 中写入 JSON 文件，以及使用 Aspose OCR
  将图像转换为 JSON。
draft: false
keywords:
- how to save json
- extract text from image
- write json file c#
- convert image to json
- c# ocr tutorial
language: zh
og_description: 在 C# 中保存 OCR 结果的 JSON 很简单。请按照本教程从图像中提取文本并以 C# 风格写入 JSON 文件。
og_title: 如何在 C# 中从 OCR 保存 JSON – 完整指南
tags:
- C#
- OCR
- JSON
title: 如何在 C# 中从 OCR 保存 JSON – 步骤指南
url: /zh/net/text-recognition/how-to-save-json-from-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中保存 OCR 的 JSON – 完整教程

在 C# 中将 OCR 结果保存为 JSON 是将扫描的纸质文件转化为结构化数据的常见需求。在本指南中，你将看到如何从图像中提取文本、将其转换为 JSON，最后以 C# 方式写入 JSON 文件——不废话，只给出可运行的解决方案。

有没有尝试过用扫描仪读取收据，却得到一张模糊的图片，根本无法搜索？这正是许多开发者在从图像中提取数据时遇到的问题。阅读完本文后，你将拥有一个小型控制台应用，能够读取图像、使用 Aspose OCR 提取文本，并保存一份干净的 JSON 文件，供后续任何服务使用。

我们将覆盖所有内容：所需的 NuGet 包、完整可运行且带有大量注释的代码、常见坑点以及快速验证输出的方法。无需任何 OCR 经验——只要具备基本的 C# 与 .NET 知识即可。

## 前置条件

在开始之前，请确保你已经拥有：

- .NET 6 SDK 或更高版本（代码面向 .NET 6，但在 .NET 5+ 也可运行）
- Visual Studio 2022、VS Code 或任意你喜欢的编辑器
- 一张待处理的图像文件（`input.png`）
- 能够访问互联网以获取 **Aspose.OCR** NuGet 包

如果缺少上述任意项，请立即获取，否则后面会浪费时间。  

> **专业提示：** Aspose OCR 提供免费试用密钥——非常适合在没有许可证的情况下进行实验。

## 第一步：安装 Aspose OCR NuGet 包

首先，添加负责核心工作的库。在项目文件夹的终端中运行：

```bash
dotnet add package Aspose.OCR
```

这条命令会下载最新的 Aspose OCR 二进制文件并在你的 `.csproj` 中添加引用。  

> **为什么这一步重要：** 没有此包，`OcrEngine` 类根本不存在，编译时会报错。  

包装好后，我们来创建控制台应用的基本结构。

## 第二步：搭建项目结构

如果还没有创建控制台项目，请执行：

```bash
dotnet new console -n JsonExportOcr
cd JsonExportOcr
```

在 `Program.cs` 中用下面的完整示例替换默认内容。稍后我们会逐行讲解，但先把文件准备好可以避免复制时漏掉大括号。

## 第三步：初始化 OCR 引擎（从图像提取文本）

第一行真正的代码创建了 OCR 引擎并指定使用英文字符。你可以切换为 `Language.Spanish` 或其他受支持的语言，但英文是最常见的情况。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;
using System.IO;

class JsonExport
{
    static void Main()
    {
        // Step 3.1: Create an OCR engine and set the language to English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // Step 3.2: Recognize text from the input image
        // Replace the path with where your image actually lives
        string inputPath = @"YOUR_DIRECTORY/input.png";
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);
```

**发生了什么？**  
- `OcrEngine` 是 Aspose OCR 的入口点。  
- 设置 `Language` 能提升准确率，因为引擎会应用语言特定的启发式算法。  
- `RecognizeImage` 返回一个 `OcrResult` 对象，里面包含所有识别出的单词、置信度以及边界框。

如果图像缺失或损坏，防护代码会打印友好的提示并中止——这一步可以避免后面出现难以定位的空引用错误。

## 第四步：将 OCR 结果转换为 JSON（将图像转为 JSON）

Aspose OCR 附带了一个名为 `JsonResultWriter` 的帮助类。它会把 `OcrResult` 序列化为干净的 JSON 字符串，结构与 REST API 返回的格式相同。

```csharp
        // Step 4: Convert the OCR result to a JSON string
        string jsonResult = JsonResultWriter.Write(ocrResult);
```

**为什么使用 `JsonResultWriter`？**  
- 它会自动处理复杂对象（如嵌套的 `Word` 集合）。  
- 省去自行编写序列化代码的麻烦，避免遗漏置信度等细节字段。

此时 `jsonResult` 大致如下（已做美化便于阅读）：

```json
{
  "PageCount": 1,
  "Pages": [
    {
      "PageNumber": 1,
      "Words": [
        {
          "Text": "Hello",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 50, "Height": 15 }
        },
        // … more words …
      ]
    }
  ]
}
```

你可以把这段代码复制到 JSON 查看器中，探索其结构。  

> **边缘情况：** 如果图像包含多页，JSON 中会出现 `Pages` 数组——确保下游消费者能够处理该数组。

## 第五步：将 JSON 写入磁盘（如何保存 JSON）

下面进入本教程的核心：**如何将 JSON 保存到磁盘**。`.NET` 的 `File` 类可以一行代码搞定，但我们会加入少量错误处理以提升鲁棒性。

```csharp
        // Step 5: Write the JSON string to an output file
        string outputPath = @"YOUR_DIRECTORY/output.json";
        try
        {
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"JSON saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to write JSON: {ex.Message}");
        }
```

至此，你终于回答了 *如何保存 JSON* 这个问题——文件会被创建，若已存在则会被覆盖，并在控制台输出明确的成功提示。

## 第六步：验证结果

程序运行完毕后，用任意编辑器（VS Code、Notepad++ 或浏览器）打开 `output.json`。你应该能看到格式良好的 JSON，展示 OCR 的输出。如果看到空的 `"Words": []` 数组，请检查图像质量——OCR 对低对比度或噪声较大的图像表现不佳。

你也可以在命令行快速做一次检查：

```bash
dotnet run
```

预期输出：

```
JSON saved to YOUR_DIRECTORY/output.json
```

如果出现错误，控制台会告知是输入文件缺失还是写入操作失败。

## 完整可运行示例

下面是 **完整** 程序代码，可直接复制到 `Program.cs` 中。将 `YOUR_DIRECTORY` 替换为包含 `input.png` 的文件夹路径。除此之外不需要其他文件。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;
using System.IO;

class JsonExport
{
    static void Main()
    {
        // Step 3: Initialize OCR engine (extract text from image)
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // Define file paths
        string inputPath = @"YOUR_DIRECTORY/input.png";
        string outputPath = @"YOUR_DIRECTORY/output.json";

        // Validate input image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        // Recognize text
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Convert OCR result to JSON (convert image to json)
        string jsonResult = JsonResultWriter.Write(ocrResult);

        // Write JSON to disk (how to save json)
        try
        {
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"JSON saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to write JSON: {ex.Message}");
        }
    }
}
```

运行程序，打开生成的文件，你就成功完成了一个 **c# ocr 教程**，展示了 **如何保存 JSON**。

## 常见坑点与技巧（Write JSON File C#）

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| **`Words` 数组为空** | 图像过暗或分辨率太低 | 预处理图像（提升对比度、使用更高 DPI） |
| **`File.WriteAllText` 抛出 UnauthorizedAccessException** | 写入只读文件夹 | 选择可写目录（如 `%TEMP%` 或项目文件夹） |
| **缺少 NuGet 包** | 忘记执行 `dotnet add package Aspose.OCR` | 重新运行该命令并重新编译 |
| **JSON 为单行** | `WriteAllText` 直接写入未格式化的字符串 | 若有重载，使用 `JsonResultWriter.Write(ocrResult, true)`，或通过 `JsonSerializer` 并设置 `WriteIndented = true` |

这些快速检查可以让你的 **write json file c#** 工作流更加顺畅，避免出现“什么都没发生”的尴尬。

## 后续步骤（Extract Text from Image & More）

既然已经掌握了 **如何保存 JSON**，接下来你可能想要：

- **存储…**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}