---
category: general
date: 2026-06-03
description: 使用 Aspose.OCR 对图像执行 OCR 并提取图像中的文本。在一个 C# 示例中学习如何检测拼写错误并获取拼写建议。
draft: false
keywords:
- perform OCR on image
- extract text from image
- detect misspelled words
- get spelling suggestions
- how to extract text
language: zh
og_description: 使用 Aspose.OCR 在 C# 中对图像执行 OCR 以提取文本，然后检测拼写错误并获取拼写建议。
og_title: 在 C# 中对图像进行 OCR 并检测拼写错误的单词
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on image and extract text from image using Aspose.OCR.
    Learn how to detect misspelled words and get spelling suggestions in a single
    C# demo.
  headline: Perform OCR on Image and Detect Misspelled Words in C#
  type: TechArticle
tags:
- Aspose OCR
- C#
- Spell Checking
title: 在 C# 中对图像执行 OCR 并检测拼写错误的单词
url: /zh/net/text-recognition/perform-ocr-on-image-and-detect-misspelled-words-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中对图像执行 OCR 并检测拼写错误的单词

有没有想过如何 **对图像执行 OCR** 而不抓狂？你并不是唯一的。无论是数字化旧信件、扫描收据，还是构建智能文档工作流，从图片中提取干净的文本都是第一道难关。好消息是？使用 Aspose.OCR，你可以在几分钟内搭建一个解决方案，而且还能 **检测拼写错误的单词** 并 **获取拼写建议**，一次完成。

在本教程中，我们将演示一个完整、可直接运行的 C# 控制台应用程序，它 **从图像提取文本**、运行英文拼写检查器，并将每个错误以及相应的纠正建议打印出来。阅读完毕后，你将清楚 **如何提取文本**、**如何调用拼写检查 API**，以及预期的控制台输出是什么样子。

## 你将构建的内容

- 加载包含拼写错误的位图（或 PNG）。  
- 使用 Aspose.OCR **对图像执行 OCR** 并获取原始字符串数据。  
- 初始化内置的英文拼写检查器。  
- **检测拼写错误的单词** 并 **获取每个单词的拼写建议**。  
- 将整洁的报告打印到控制台。

无需外部服务，无需繁琐的 HTTP 调用——只需一个 NuGet 包和几行代码。

## 前置条件

- .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Framework 4.7+）。  
- Visual Studio 2022（或任意你喜欢的编辑器）。  
- Aspose.OCR for .NET NuGet 包（`Aspose.OCR`）。  
- 一张图片文件（`letter_with_typos.png`），放在项目可以引用的位置。

如果你从未使用过 Aspose，别担心——安装包就像运行下面的命令一样简单：

```bash
dotnet add package Aspose.OCR
```

现在让我们深入实现细节。

## 第一步：创建项目并安装 Aspose.OCR

创建一个新的控制台项目并引入 OCR 库：

```bash
dotnet new console -n OcrSpellDemo
cd OcrSpellDemo
dotnet add package Aspose.OCR
```

恢复完成后，打开 `Program.cs`。我们稍后会用完整的演示代码替换默认内容，但先来聊聊每个命名空间的作用。

- `Aspose.OCR` – 核心 OCR 引擎和图像处理。  
- `Aspose.OCR.SpellCheck` – 随库提供的拼写检查工具。  
- `System` – 标准 .NET 基础类（例如 `Console`）。

## 第二步：加载图像并对图像执行 OCR

真正的工作是把图像喂给 OCR 引擎。Aspose.OCR 支持多种格式（PNG、JPEG、TIFF）。下面的代码片段完成了这项重活：

```csharp
// Step 2: Load the image that contains the text to be recognized
var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

// Step 3: Perform OCR to extract the raw text from the image
var ocrEngine = new OcrEngine();
var ocrResult = ocrEngine.Recognize(image);
```

> **为什么重要：** `OcrImage.FromFile` 抽象掉像素级细节，而 `OcrEngine.Recognize` 则运行训练好的神经模型，将可视字符转换为 Unicode。`ocrResult.Text` 属性现在保存了原始字符串——这正是你需要的 **从图像提取文本**。

> **小技巧：** 如果图像包含多种语言，可以在调用 `Recognize` 之前设置 `ocrEngine.Language = OcrLanguage.Multilingual;`。

## 第三步：初始化英文拼写检查器

Aspose.OCR 自带的拼写检查引擎开箱即用英文。初始化只需一行代码：

```csharp
// Step 4: Initialise the English spell‑checker
var spellChecker = new SpellChecker(OcrLanguage.English);
```

> **为什么这一步至关重要：** OCR 输出可能包含误识别的字符（例如 “l” 与 “1”）或源文档本身的拼写错误。拼写检查器会扫描字符串，定位可疑词并提供替代方案。

## 第四步：检测拼写错误的单词并获取拼写建议

现在把 OCR 文本传给检查器：

```csharp
// Step 5: Check the recognized text for misspelled words and obtain suggestions
var misspellings = spellChecker.Check(ocrResult.Text);
```

`misspellings` 是一个集合，每个条目包含错误单词以及可能的纠正数组。

## 第五步：输出结果

最后，遍历集合并打印出人类可读的报告：

```csharp
// Step 6: Output each misspelled word together with its suggested corrections
foreach (var entry in misspellings)
{
    Console.WriteLine($"Misspelled: {entry.Word}");
    Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
}
```

### 预期的控制台输出

假设 `letter_with_typos.png` 包含以下句子：

```
Ths is an exampel of a lettter with som misspelled wrds.
```

运行演示后会得到类似下面的输出：

```
Misspelled: Ths
  Suggestions: This, Thus, The
Misspelled: exampel
  Suggestions: example, exemplar, exampell
Misspelled: lettter
  Suggestions: letter, litter, lett
Misspelled: som
  Suggestions: some, sum, son
Misspelled: wrds
  Suggestions: words, wards, wryds
```

可以看到每个拼写错误都配有若干合理的修正——这正是构建用户友好纠正 UI 时所需要的。

## 完整可运行示例

下面是 **完整、可直接复制粘贴** 的程序。将 `YOUR_DIRECTORY` 替换为你的图片实际路径。

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Load the image that contains the text to be recognized
        var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

        // Step 2: Perform OCR to extract the raw text from the image
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(image);

        // Step 3: Initialise the English spell‑checker
        var spellChecker = new SpellChecker(OcrLanguage.English);

        // Step 4: Check the recognized text for misspelled words and obtain suggestions
        var misspellings = spellChecker.Check(ocrResult.Text);

        // Step 5: Output each misspelled word together with its suggested corrections
        foreach (var entry in misspellings)
        {
            Console.WriteLine($"Misspelled: {entry.Word}");
            Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
        }

        // Optional: Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

> **需要考虑的边界情况**  
> - **空图像：** 如果 OCR 引擎返回空字符串，`spellChecker.Check` 将返回空集合——不会崩溃。  
> - **非英文文本：** 将 `OcrLanguage.English` 替换为 `OcrLanguage.French`（或任何受支持的语言），即可 **检测其他语言的拼写错误**。  
> - **大文档：** 对于多页 PDF，需要遍历每页，执行 OCR，然后在拼写检查前聚合结果。

## 可视化概览（图片替代文字）

![展示对图像执行 OCR、从图像提取文本，然后检测拼写错误并提供拼写建议的流程图](perform-ocr-on-image-flow.png)

*上图展示了端到端的流水线：图像 → OCR 引擎 → 原始文本 → 拼写检查器 → 建议。*

## 常见问题 & 专业技巧

| 问题 | 答案 |
|----------|--------|
| **是否需要互联网连接？** | 不需要。Aspose.OCR 完全本地运行，适合离线或安全环境。 |
| **拼写检查器的准确度如何？** | 使用约 15 万英文单词的词典并结合模糊匹配，能够捕获大多数常见错别字。 |
| **可以自定义词典吗？** | 可以。`SpellChecker.AddUserDictionary("custom.txt")` 允许加载领域专用词汇（例如产品名称）。 |
| **如果图像倾斜怎么办？** | OCR 引擎会自动检测方向，但对于顽固情况，你可以手动调用 `ocrEngine.ImagePreprocessing.Rotate(angle)`。 |
| **有没有办法在 UI 中高亮建议？** | 获得 `misspellings` 集合后，可将每个 `entry.Word` 映射回 `ocrResult.Text` 中的位置，并在 RichTextBox 或网页视图中下划线标记。 |

## 结论

我们已经演示了 **如何对图像执行 OCR**、**从图像提取文本**，以及随后 **检测拼写错误的单词** 并 **获取拼写建议**——全部使用简洁的 C# 控制台应用。核心思路很简单：让 Aspose.OCR 完成字符识别的重活，再让其内置的拼写检查器清理输出。接下来，你可以把演示扩展为完整的文档处理服务，集成到 Web API，或嵌入桌面编辑器。

准备好下一步了吗？尝试切换语言为西班牙语，处理多页 PDF，或构建一个小型 WPF 前端，让用户点击单词接受建议。构建块已经就位——尽情实验吧。

如果在使用过程中遇到任何问题或有扩展想法，欢迎在下方留言。祝编码愉快！

## 接下来你可以学习什么？

以下教程与本指南紧密相关，帮助你进一步掌握 API 功能并探索在项目中的其他实现方式，每篇都包含完整可运行的代码示例和逐步解释。

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}