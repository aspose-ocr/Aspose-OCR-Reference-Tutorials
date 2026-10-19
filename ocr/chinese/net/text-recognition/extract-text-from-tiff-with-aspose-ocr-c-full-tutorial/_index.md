---
category: general
date: 2026-01-09
description: 使用 Aspose OCR 在 C# 中提取 TIFF 文件的文本。了解如何在本分步教程中获取每个结果的前 50 个字符。
draft: false
keywords:
- extract text from tiff
- get first 50 characters
- aspose ocr c# tutorial
language: zh
og_description: 使用 Aspose OCR 在 C# 中从 TIFF 提取文本。本指南逐步展示如何获取每个 OCR 结果的前 50 个字符。
og_title: 使用 Aspose OCR 从 TIFF 提取文本 – 完整 C# 指南
tags:
- Aspose OCR
- C#
- TIFF processing
title: 使用 Aspose OCR C# 从 TIFF 提取文本 – 完整教程
url: /zh/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-c-full-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 TIFF 中提取文本 – 完整 Aspose OCR C# 教程

是否曾经需要 **从 TIFF 图像中提取文本**，却不确定该使用哪个库？你并不孤单。许多开发者在尝试从多页 TIFF 中提取可搜索文本时会卡住，尤其是对性能有要求的时候。

在本 **aspose ocr c# tutorial** 中，我们将演示一个可直接运行的示例，它不仅可以提取完整文本，还会展示如何 **获取每页的前 50 个字符** 以便快速预览。完成后，你将拥有一个可直接放入任何 .NET 项目的独立程序。

## 你需要准备的环境

- .NET 6（或任何近期的 .NET 版本）——代码可在 .NET Core 和 .NET Framework 上编译。  
- 有效的 Aspose.OCR for .NET 许可证（可先使用免费试用版）。  
- 包含一个或多个 `.tif` 文件的文件夹，用于处理。  
- Visual Studio、VS Code 或任意你喜欢的 IDE——示例为纯 C#，编辑器选择并不影响。

> **专业提示：** 如果你在 CI 服务器上运行，直接在项目文件中添加 Aspose.OCR NuGet 包 (`Aspose.OCR`)；该库为完全托管的，不依赖本机组件。

## 第一步：安装 Aspose OCR NuGet 包

首先，把 OCR 引擎引入项目。打开解决方案文件夹的终端，运行：

```bash
dotnet add package Aspose.OCR
```

该命令会拉取最新的稳定版本（截至 2026 年 1 月为 23.9），并自动更新你的 `.csproj`。无需手动管理 DLL。

## 第二步：初始化 OCR 引擎

接下来创建 `OcrEngine` 实例。把它想象成读取每页 TIFF 的“大脑”。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: tweak recognition settings if you know the language
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300; // higher DPI can improve accuracy
```

为什么只实例化一次引擎？因为 `RecognizeImages` 可以接受文件路径集合，让引擎复用内部缓冲区，从而显著加速批量处理。

## 第三步：一次性获取所有 TIFF 文件

我们不手动遍历目录，而是让 .NET 完成繁重工作。`Directory.GetFiles` 方法返回 `IEnumerable<string>`，可以直接喂给 OCR 调用。

```csharp
            // Step 3: Collect all TIFF images from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }
```

> **如果我的图像是 JPEG 或 PNG 呢？** 只需更改搜索模式（`"*.jpg"` 或 `"*.*"`）。Aspose OCR 支持所有常见的光栅格式。

## 第四步：对整个集合执行 OCR

下面这行代码一次性处理所有文件。该方法返回一个字典，键为文件路径，值为包含识别文本的 `OcrResult` 对象。

```csharp
            // Step 4: Perform OCR on the entire collection in one call
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);
```

为什么采用批处理？它减少了重复加载 OCR 引擎的开销，并且在多核机器上，Aspose 会内部并行化工作，带来明显的速度提升。

## 第五步：显示预览 – 获取前 50 个字符

大多数 UI 场景只需要片段，而不是完整文档。我们将提取前 50 个字符（如果页面较短则更少），并将其与文件名一起打印。

```csharp
            // Step 5: Display each file name with a preview of the recognized text
            foreach (var entry in ocrResults) // entry.Key = file path, entry.Value = OcrResult
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;
                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));

                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

`Math.Min(50, fullText.Length)` 这行代码确保不会超出字符串范围——这是一个小小的防护，防止在 OCR 结果短于 50 字符时抛出 `ArgumentOutOfRangeException`。

### 预期的控制台输出

假设目录中有两个 TIFF 文件（`invoice1.tif` 和 `receipt2.tif`），控制台可能显示：

```
invoice1.tif → Invoice Number: 2025-07-14 Date: 07/14/...
receipt2.tif → Store: QuickMart Total: $23.45 Date: ...
```

每行以省略号（`...`）结尾，表示预览仅为更长文本块的开头。

## 第六步：处理边缘情况和常见陷阱

### 空文件或损坏文件

如果文件无法读取，`RecognizeImages` 仍会返回一个 `Text` 属性为空的条目。你可以过滤掉这些条目：

```csharp
if (string.IsNullOrWhiteSpace(fullText))
{
    Console.WriteLine($"{fileName} → (No recognizable text)");
    continue;
}
```

### 大批量处理

处理成千上万的 TIFF 可能会占用大量内存。此时可以使用接受 `Stream` 的重载，或将列表分成更小的块处理：

```csharp
var batches = imageFiles.Chunk(100); // .NET 6+ extension
foreach (var batch in batches)
{
    var batchResults = ocrEngine.RecognizeImages(batch);
    // handle batchResults...
}
```

### 语言与字体支持

如果文档包含非拉丁字符，请在调用 `RecognizeImages` 前设置语言：

```csharp
ocrEngine.Language = Language.Spanish; // or Language.MultiLanguage
```

这个小改动可以显著提升识别准确率。

## 第七步：完整可运行示例（复制粘贴即用）

下面是完整程序代码，你可以将其粘贴到新建的控制台项目（`dotnet new console`）中直接运行（只需将 `YOUR_DIRECTORY/Batch` 替换为实际路径）。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: set language or DPI for better accuracy
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300;

            // Collect all TIFF files from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }

            // Perform OCR on the entire collection
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);

            // Show a preview – get first 50 characters of each result
            foreach (var entry in ocrResults)
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;

                if (string.IsNullOrWhiteSpace(fullText))
                {
                    Console.WriteLine($"{fileName} → (No recognizable text)");
                    continue;
                }

                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));
                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

使用 `dotnet run` 运行程序。你应该会看到每个 TIFF 文件的简要预览，证明你已经成功 **从 TIFF 中提取文本**，并使用 Aspose OCR 完成了整个过程。

## 常见问题解答 (FAQ)

**问：这能处理多页 TIFF 吗？**  
答：可以。Aspose OCR 在内部将每页视为独立图像，因此多页 TIFF 会产生每个文件对应的单个合并字符串。需要时可以自行拆分。

**问：开箱即用的 OCR 准确率如何？**  
答：对于干净的高分辨率扫描（300 DPI 及以上），英文文本的准确率可超过 95%。通过预处理（去倾斜、二值化）可以进一步提升。

**问：我可以把结果输出为 CSV 文件吗？**  
答：完全可以。将 `Console.WriteLine` 替换为 `StreamWriter`，写入 `fileName,preview` 行即可。记得对预览文本中的逗号进行转义。

## 后续步骤与相关主题

- **持久化 OCR 结果** – 将完整文本存入数据库，实现可搜索的档案。  
- **结合 PDF 转换** – 使用 Aspose.PDF 将提取的文本嵌入可搜索的 PDF 中。  
- **在 Azure Functions 上批处理** – 在无需管理服务器的情况下横向扩展 OCR 工作负载。  

所有这些扩展都围绕着 **高效从 TIFF 中提取文本** 的核心思想，同时仍然让你 **获取前 50 个字符** 以便快速 UI 预览。

---

*祝编码愉快！如果遇到任何奇怪的问题，欢迎在下方留言，我会尽力帮助你微调 OCR 流程。* 

![使用 Aspose OCR 从 TIFF 提取文本](https://example.com/images/extract-text-from-tiff.png "使用 Aspose OCR 从 TIFF 提取文本")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}