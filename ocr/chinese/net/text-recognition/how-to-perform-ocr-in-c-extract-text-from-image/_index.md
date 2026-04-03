---
category: general
date: 2026-04-03
description: 学习如何在 C# 中使用 Aspose OCR 执行 OCR 并从图像中提取文本，同时进行俄语拼写检查。
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- how to spell check
- ocr russian language
language: zh
og_description: 学习如何在 C# 中执行 OCR 并使用 Aspose OCR 从图像中提取文本，支持俄语拼写检查。
og_title: 如何在 C# 中进行 OCR – 从图像中提取文本
tags:
- OCR
- C#
- Aspose
- SpellCheck
title: 如何在 C# 中进行 OCR – 从图像中提取文本
url: /zh/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中执行 OCR – 从图像中提取文本

是否曾好奇 **如何执行 OCR** 来识别手写笔记的照片？也许你有一张扫描的收据、一块外语标志，或是一页无法复制粘贴的 PDF。好消息是，只需几行 C# 代码和 Aspose OCR 库，就能瞬间把图片转换为可编辑的文本。

在本指南中，我们不仅会展示 **如何执行 OCR**，还会演示 **从图像中提取文本**、**将图像转换为文本**，以及在处理俄语文档时 **如何进行拼写检查**。听起来很多？别担心——我们会一步步拆解。

## 你将学到

完成本教程后，你将能够：

* 为俄语设置 Aspose OCR 支持。  
* 加载图像文件并运行光学字符识别以 **从图像中提取文本**。  
* 使用内置的拼写检查器自动纠正拼写错误——完美回答 “**如何进行拼写检查**” OCR 输出的问题。  
* 将清理后的字符串打印到控制台，便于后续处理或存储。

**先决条件** – 你需要：

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.8）。  
* 有效的 Aspose OCR 许可证或临时评估密钥。  
* 包含俄语文本的图像文件（演示中我们使用 `russian_note.jpg`）。

如果这些对你来说陌生，也无需担心。下面的步骤已包含获取 Aspose OCR 的完整 NuGet 命令，代码也是完全自包含的。

![如何执行 OCR 示例](/images/ocr-demo.png "C# 中如何执行 OCR 示例")

## 第一步 – 安装 Aspose OCR 并添加命名空间

首先，需要获取库。在项目文件夹的终端中运行：

```bash
dotnet add package Aspose.OCR
```

该命令会拉取最新的稳定版本（截至 2026 年 4 月为 22.9）。包恢复完成后，在 C# 文件顶部添加所需的 `using` 指令：

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;
```

*小技巧*：如果使用 Visual Studio，IDE 会在你键入第一个类名时自动提示添加这些引用。

## 第二步 – 为俄语初始化 OCR 引擎

**如何执行 OCR** 的关键在于创建 `OcrEngine` 实例。通过指定 `OcrLanguage.Russian`，我们告诉引擎加载西里尔字符集及语言特定的启发式算法。

```csharp
// Step 2: Initialise OCR engine for Russian
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Russian   // Enables Russian language support
};
```

为什么要这么做？如果不设置语言，引擎默认使用英语，会误判大量西里尔字符，导致输出乱码。显式配置语言可以显著提升准确率。

## 第三步 – 加载图像并 **将图像转换为文本**

现在把图片加载到内存中。`Image.FromFile` 方法支持大多数常见格式（JPG、PNG、BMP）。加载后，调用 `Recognize` 以 **将图像转换为文本**。

```csharp
// Step 3: Load the image that contains Russian text
Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

// Step 4: Perform OCR – this is the core “how to perform OCR” call
string rawText = ocrEngine.Recognize(sourceImage);
```

`rawText` 变量现在保存了原始 OCR 输出，仍可能包含拼写错误或识别错误的字符。你可以打印它来查看引擎捕获的内容：

```csharp
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

## 第四步 – **如何进行拼写检查** OCR 结果

俄语 OCR 往往噪声较多，尤其是低分辨率扫描。Aspose 提供了 `SpellChecker` 类，内置俄语词典。下面演示如何调用：

```csharp
// Step 5: Initialise the spell checker
SpellChecker spellChecker = new SpellChecker();

// Step 6: Correct spelling mistakes in the recognized text
string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);
```

`CheckAndCorrect` 方法返回一个新字符串，拼写错误的单词会被最可能的正确形式替换。它同样会保留标点符号，避免出现一整块没有间隔的文本。

*边缘情况*：如果 OCR 输出为空（例如图像全白），`CheckAndCorrect` 将直接返回空字符串。若计划将结果写入文件，建议先做空值检查。

## 第五步 – 显示清理后的结果

最后，输出纠正后的字符串。在真实项目中，你可能会把它写入数据库、JSON API 或 Word 文档。演示中，直接在控制台打印即可：

```csharp
// Step 7: Show the corrected result
Console.WriteLine("\nCorrected text:");
Console.WriteLine(correctedText);
```

运行程序后，你应看到类似如下的输出：

```
Raw OCR output:
Привeт мир! Этo тeкcт c русcкoй оcнoвнoй.

Corrected text:
Привет мир! Это текст с русской основой.
```

注意拼写检查器将 “Привeт”（混合了拉丁字母 ‘e’）纠正为正确的西里尔字母 “Привет”。这正是 **如何进行拼写检查** OCR 输出的魔力所在。

## 完整可运行示例

下面是把所有步骤串联起来的完整可运行程序。复制粘贴到新的控制台项目中，按 **F5** 运行。

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine configured for Russian language
        OcrEngine ocrEngine = new OcrEngine { Language = OcrLanguage.Russian };

        // Step 2: Load the image that contains the text to be recognized
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

        // Step 3: Perform OCR to extract raw text from the image
        string rawText = ocrEngine.Recognize(sourceImage);

        // Optional: Show raw OCR output
        System.Console.WriteLine("Raw OCR output:");
        System.Console.WriteLine(rawText);

        // Step 4: Initialise the spell checker
        SpellChecker spellChecker = new SpellChecker();

        // Step 5: Correct spelling mistakes in the recognized text
        string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);

        // Step 6: Display the corrected result
        System.Console.WriteLine("\nCorrected text:");
        System.Console.WriteLine(correctedText);
    }
}
```

### 预期输出

使用清晰、高分辨率的俄语手写照片运行程序，通常会得到一条干净、可读的句子。如果图像模糊，仍可能出现部分正确的单词，但拼写检查器会平滑大多数明显错误。

## 常见问题与技巧

| 问题 | 产生原因 | 解决方案 / 避免方法 |
|------|----------|-------------------|
| **乱码字符** | DPI 低或背景噪声大 | 在调用 `Recognize` 前对图像进行预处理（提高对比度，调整至 ≥300 dpi）。 |
| **输出为空** | 文件路径错误或不支持的格式 | 核实路径，并在 `Image.FromFile` 外层使用 `try/catch` 捕获异常。 |
| **拼写检查未捕获错误** | 词典中缺少罕见词汇 | 通过 `spellChecker.AddUserDictionary("mywords.txt")` 加载自定义词表。 |
| **大批量处理性能下降** | OCR 计算密集 | 将 OCR 放在后台线程执行，或使用 `Parallel.ForEach` 并行处理多张图像。 |
| **许可证异常** | 评估版超出试用期 | 购买许可证并在创建 `OcrEngine` 前调用 `License license = new License(); license.SetLicense("Aspose.Total.lic");`。 |

## 后续步骤 – 超越基础 OCR

掌握了 **如何执行 OCR** 后，你可以尝试以下扩展：

* **批量处理** – 遍历文件夹中的所有图像，并将每个纠正后的文本写入 `.txt` 文件。  
* **PDF 转换** – 使用 Aspose PDF 将提取的文本嵌入可搜索的 PDF 中。  
* **语言检测** – 若需处理多语言，先检查 OCR 结果，再相应切换 `OcrLanguage`。  
* **与 Azure Cognitive Services 集成** – 将 Aspose 的结果与 Microsoft OCR API 对比，形成混合方案。

所有这些主题自然会涉及次要关键词 **extract text from image**、**convert image to text**、以及 **how to spell check**，因此

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}