---
category: general
date: 2026-03-28
description: 学习如何在 C# 中批量进行 OCR，并轻松将 TIFF 转换为文本。本分步指南展示了使用 Aspose OCR 从 TIFF 文件提取文本。
draft: false
keywords:
- how to batch ocr
- convert tiff to text
- extract text from tiff
- c# ocr tutorial
language: zh
og_description: 如何在 C# 中批量 OCR？请跟随本完整教程，使用 Aspose OCR 将多页 TIFF 文件转换为可搜索的文本。
og_title: 如何在 C# 中批量 OCR – 将多页 TIFF 转换为文本
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中批量 OCR – 将多页 TIFF 转换为文本
url: /zh/net/text-recognition/how-to-batch-ocr-in-c-convert-multi-page-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR – 将多页 TIFF 转换为文本

是否曾经想过 **如何批量 OCR** 一堆扫描页，而不必为每张图像写一个循环？你并不是唯一有此困惑的人。在许多项目中——比如发票处理或档案数字化——**将 TIFF 转换为文本** 的需求每天都会出现，而一次只处理一页很快就会变成噩梦。

好消息是？只需几行 C# 代码和 Aspose OCR，你就可以把整个多页 TIFF 输入引擎，得到一个页面编号映射到提取字符串的字典。在本教程中，我们将完整演示一个可运行的示例，展示 **如何批量 OCR**、**如何从 TIFF 中提取文本**，以及为什么这种方法优于手动方式。

## 你将学到

- 在 .NET 项目中设置 Aspose OCR 库。  
- 使用 `Image.FromMultiPageFile` 加载多页 TIFF 文件。  
- 运行 `RecognizeBatch` 获取 `Dictionary<int,string>` 的逐页结果。  
- 以整洁、可读的格式打印输出。  

完成后，你将拥有一个可直接运行的控制台应用程序，能够把任意多页 TIFF 转换为纯文本——无需额外工具。

### 前置条件

- .NET 6.0 SDK（或任意近期的 .NET 版本）。  
- Visual Studio 2022 或 VS Code——你喜欢的 IDE 都行。  
- 有效的 Aspose OCR 许可证或免费评估密钥（API 在没有许可证的情况下仍可工作，但会添加水印）。  
- 一个名为 `multipage.tif` 的示例多页 TIFF，放在可引用的文件夹中。

> **专业提示：** 如果你使用 Windows，默认的项目文件夹是放置 TIFF 的便利位置；在 Linux/macOS 上只需相应调整路径即可。

## 第一步：安装 Aspose OCR NuGet 包

在编写任何代码之前，我们需要先获取 OCR 库。打开项目文件夹的终端并运行：

```bash
dotnet add package Aspose.OCR
```

这会拉取最新的稳定版本（截至 2026 年 3 月的 v23.9），并将必要的 DLL 添加到项目中。对于简单的控制台应用程序，无需额外配置。

## 第二步：创建控制台应用程序骨架

先搭建一个最小程序，引用 OCR 引擎。`using` 指令至关重要——缺少它们编译器会报缺少类型的错误。

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Required for Image class
```

> **为什么重要：** `Image` 类位于子命名空间中，忘记导入 `ImageProcessing` 会导致 “类型或命名空间未找到” 错误，浪费大量调试时间。

现在添加 `Main` 方法并写一段简短注释说明目的：

```csharp
/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        // Implementation will go here
    }
}
```

## 第三步：初始化 OCR 引擎

`OcrEngine` 是核心工作马。只实例化一次并在所有页面上复用，既省内存又快。

```csharp
// Step 3: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **底层发生了什么？** 引擎会加载语言模型并预配置默认设置（例如英语、自动旋转）。你可以稍后微调这些设置，但默认值对大多数文档已经足够稳健。

## 第四步：加载多页 TIFF

Aspose 让加载多帧图像变得轻而易举。提供完整路径或相对于可执行文件工作目录的相对路径即可。

```csharp
// Step 4: Load a multi‑page TIFF image
string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // ← replace with your actual path
var multiPageImage = Image.FromMultiPageFile(tiffPath);
```

如果文件未找到，`FromMultiPageFile` 会抛出 `FileNotFoundException`。如果需要优雅的错误处理，可将其包装在 `try/catch` 中——我们将在下一步演示。

## 第五步：执行批量 OCR

重头戏来了：`RecognizeBatch`。它返回一个 `Dictionary<int,string>`，键为页面索引（从 0 开始），值为识别出的文本。

```csharp
// Step 5: Perform batch OCR on all pages
Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);
```

> **边缘情况：** 有些 TIFF 包含空白页。Aspose 会为这些页面返回空字符串，你可以在后续过滤掉，以免输出中出现杂乱。

## 第六步：显示结果

最后，遍历字典并打印每页的文本。使用插值字符串可以让代码更简洁。

```csharp
// Step 6: Output the recognized text for each page
foreach (var pageResult in ocrResults)
{
    Console.WriteLine($"--- Page {pageResult.Key + 1} ---"); // +1 for human‑friendly numbering
    Console.WriteLine(pageResult.Value);
    Console.WriteLine(); // Blank line for readability
}
```

运行程序后应得到类似如下的输出：

```
--- Page 1 ---
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
...

--- Page 2 ---
Terms and Conditions
...
```

如果出现乱码，请再次确认源 TIFF 未损坏且文本语言与引擎默认语言（英语）匹配。对于非英文文档，你可以设置 `ocrEngine.Language = OcrLanguage.Spanish;`。

## 完整工作示例

将所有代码片段组合起来，下面是可以直接复制到 `Program.cs` 并运行的完整程序：

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Needed for Image class

/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        try
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Load a multi‑page TIFF image
            string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // Change to your actual file location
            var multiPageImage = Image.FromMultiPageFile(tiffPath);

            // Step 3: Perform batch OCR on all pages
            Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);

            // Step 4: Output the recognized text for each page
            foreach (var pageResult in ocrResults)
            {
                Console.WriteLine($"--- Page {pageResult.Key + 1} ---");
                Console.WriteLine(pageResult.Value);
                Console.WriteLine(); // Extra line for visual separation
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

保存、构建并运行：

```bash
dotnet run
```

你应该会在控制台看到每页提取的内容。这就是你所需的完整 **c# ocr tutorial**。

## 常见问题与边缘案例

### 我的 TIFF 有几十页怎么办？

`RecognizeBatch` 会一次性处理所有帧，但内存使用会随页面数量线性增长。对于非常大的文档（数百页），可以考虑分块处理：

```csharp
for (int i = 0; i < multiPageImage.PageCount; i += 50)
{
    var subImage = multiPageImage.GetPages(i, Math.Min(50, multiPageImage.PageCount - i));
    var partialResults = ocrEngine.RecognizeBatch(subImage);
    // Merge partialResults into the main dictionary...
}
```

### 能否将提取的文本保存为文件而不是打印？

完全可以。将 `Console.WriteLine` 部分替换为文件 I/O：

```csharp
string outputFolder = "ExtractedText";
Directory.CreateDirectory(outputFolder);

foreach (var pageResult in ocrResults)
{
    string filePath = Path.Combine(outputFolder, $"Page_{pageResult.Key + 1}.txt");
    File.WriteAllText(filePath, pageResult.Value);
}
```

这样每页都会生成一个 `.txt` 文件——非常适合后续索引。

### 如何更改输出语言或启用自动旋转？

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
ocrEngine.AutoRotate = true;             // Detects rotated text automatically
```

这些设置必须在调用 `RecognizeBatch` **之前** 应用。

## 结论

我们已经展示了如何使用 Aspose OCR 在 C# 中 **批量 OCR** 多页 TIFF。只需一次加载图像，调用 `RecognizeBatch`，遍历返回的字典，即可在几秒钟内 **将 TIFF 转换为文本**。示例还演示了 **从 TIFF 中提取文本**、错误处理以及可选的文件写入——全部封装在一个简洁的自包含控制台应用中。

准备好下一步了吗？尝试将此方法与 PDF 生成库结合，生成可搜索的 PDF，或将输出写入数据库以构建可检索的档案。你也可以通过将 `Image.FromMultiPageFile` 替换为 `Image.FromFile` 来实验其他图像格式（PNG、JPEG）。

对 OCR、授权或性能调优还有其他疑问？在下方留言，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}