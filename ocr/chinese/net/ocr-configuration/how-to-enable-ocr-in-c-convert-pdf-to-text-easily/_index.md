---
category: general
date: 2026-02-27
description: 如何在 C# 中启用 OCR 将 PDF 转换为文本。了解如何使用 Aspose OCR 从多语言 PDF 中提取文本。
draft: false
keywords:
- how to enable ocr
- convert pdf to text
- how to extract text
- how to recognize pdf
- recognize pdf text c#
language: zh
og_description: 如何在 C# 中启用 OCR 并将 PDF 转换为文本。使用 Aspose OCR 的逐步指南，提取并识别 PDF 文本。
og_title: 如何在 C# 中启用 OCR – 将 PDF 转换为文本
tags:
- OCR
- C#
- PDF
- Aspose
title: 如何在 C# 中启用 OCR – 轻松将 PDF 转换为文本
url: /zh/net/ocr-configuration/how-to-enable-ocr-in-c-convert-pdf-to-text-easily/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中启用 OCR – 轻松将 PDF 转换为文本

如何在 C# 中启用 OCR 是许多开发者在需要从 PDF 中提取文本时常问的问题。如果你曾盯着一张扫描的发票并想知道 *“怎么在不手动重新输入的情况下提取文本？”*，那么你来对地方了。在本教程中，我们将逐步演示一个完整、可直接运行的解决方案，既展示 **如何启用 OCR**，又演示 **如何将 PDF 转换为文本**、**如何从多语言文档中提取文本**，以及 **如何使用 C# 识别 PDF** 内容。

我们将使用 Aspose.OCR 库，它开箱即支持数十种语言，无需为英文、阿拉伯文、日文或其他脚本分别准备引擎。阅读完本指南后，你将拥有一个 **识别 PDF 文本 C#** 的单一方法，能够将结果打印到控制台，并可直接嵌入任何 .NET 项目。

## 前置条件 – 开始前需要准备的内容

- .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）
- Visual Studio 2022（或你喜欢的任意编辑器）
- **Aspose.OCR for .NET** 的许可证或免费试用版 – 可从 Aspose 官网获取临时密钥
- 一个包含多语言的示例 PDF（我们将其命名为 `multilang.pdf`）

如果缺少上述任意项，请从 Microsoft 官网下载 SDK 并安装 NuGet 包：

```bash
dotnet add package Aspose.OCR
```

以上即完成所有准备工作。准备好了吗？让我们开始吧。

## 如何在 C# 中启用 OCR – 设置与配置

首先要做的就是创建 OCR 引擎实例并告知它你期望的语言。这一步就是 **如何启用 OCR**，为后续工作提供支持。

```csharp
using Aspose.OCR;
using System;

public class OcrDemo
{
    public static void Main()
    {
        // Step 1: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Enable the languages you need (English, Arabic, Japanese)
        ocrEngine.Language = OcrLanguage.English |
                             OcrLanguage.Arabic |
                             OcrLanguage.Japanese;

        // Step 3: Recognize text from the PDF file
        string recognizedText = ocrEngine.RecognizeFromFile("YOUR_DIRECTORY/multilang.pdf");

        // Step 4: Output the extracted text
        Console.WriteLine(recognizedText);
    }
}
```

**为什么重要：** 通过显式设置 `Language` 属性，你可以引导引擎加载正确的字符模型，从而显著提升准确率——尤其是对混合脚本的 PDF。若跳过此步骤（或保持默认），引擎将自行猜测，往往导致输出乱码。

> **小技巧：** 如果你的文档只包含单一语言，请将标志限制为该语言。这可以将处理速度提升最高约 30 %。

### 图片 – 启用 OCR 的可视化概览  
![Screenshot of OCR engine configuration showing how to enable OCR in C#](/images/enable-ocr-csharp.png)

*Alt text: Diagram illustrating how to enable OCR in C# using Aspose.OCR.*

## 使用 Aspose OCR 将 PDF 转换为文本

现在 **如何启用 OCR** 已经完成，接下来讨论实际的转换过程。`RecognizeFromFile` 方法负责全部工作：打开 PDF、在每页上运行 OCR 引擎，并返回包含所有提取字符的单个字符串。

### 方法内部到底做了什么？

1. **页面光栅化** – 将每个 PDF 页面转换为位图，因为 OCR 只能在图像上工作。
2. **语言模型选择** – 根据前面设置的标志，引擎挑选相应的神经网络。
3. **文本行检测** – 引擎即使在文本倾斜的情况下也能找到文本行。
4. **字符解码** – 最终将像素模式映射为 Unicode 字符。

由于该方法返回普通字符串，你可以在一行代码中 **将 PDF 转换为文本**。如果需要更细粒度的处理（例如逐页处理），可以在循环中调用 `RecognizeFromStream`。

## 如何从多语言 PDF 中提取文本

假设你的 PDF 包含英文标题、阿拉伯文正文和日文脚注。前面展示的代码已经能够处理这种情况，但你可能想知道 **如何仅提取特定语言段落的文本**。

可以使用简单的字符串操作或正则表达式对结果进行过滤。下面是一个快速示例，仅提取英文部分：

```csharp
using System.Text.RegularExpressions;

// After recognizing the whole document...
string allText = ocrEngine.RecognizeFromFile("YOUR_DIRECTORY/multilang.pdf");

// Regex to keep only ASCII characters (roughly English)
string englishOnly = Regex.Replace(allText, @"[^\u0000-\u007F]+", string.Empty);

Console.WriteLine("English extracted:");
Console.WriteLine(englishOnly);
```

**为什么要过滤？** 在许多业务流程中，你只需要拉丁脚本部分用于索引，而其余内容会存放在别处。此模式展示了 **如何提取文本**，且无需进行第二次 OCR。

## 如何识别 PDF – 处理边缘情况

即使是最优秀的 OCR 引擎也会在某些 PDF 上出现问题。以下列出常见陷阱及对应解决方案：

| 问题 | 症状 | 解决方案 |
|------|------|----------|
| 低分辨率扫描 (<150 dpi) | 缺失字符、乱码 | 使用 `ocrEngine.ImageProcessingOptions.Dpi = 300;` 预处理 PDF |
| 页面旋转 | 文本横向显示 | 设置 `ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;` |
| 加密 PDF | `RecognizeFromFile` 抛出异常 | 传入密码：`ocrEngine.RecognizeFromFile(path, "myPassword");` |
| 超大文件 (>100 页) | 内存溢出崩溃 | 分块处理：一次加载 10 页并拼接结果 |

实现这些微调后，你的解决方案即可 **识别 PDF** 内容，可靠度大幅提升。

```csharp
// Example of handling low‑resolution and rotation
ocrEngine.ImageProcessingOptions.Dpi = 300;
ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;
```

## Recognize PDF Text C# – 完整可运行示例

将所有内容整合在一起，下面是一段可直接复制到控制台应用的完整程序。它演示了 **如何启用 OCR**、**将 PDF 转换为文本**、**提取特定语言片段**，以及 **处理常见边缘情况**。

```csharp
using Aspose.OCR;
using System;
using System.Text.RegularExpressions;

namespace PdfOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create OCR engine instance
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable languages (English, Arabic, Japanese)
            ocrEngine.Language = OcrLanguage.English |
                                 OcrLanguage.Arabic |
                                 OcrLanguage.Japanese;

            // Optional: improve accuracy for low‑res PDFs
            ocrEngine.ImageProcessingOptions.Dpi = 300;
            ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;

            // 3️⃣ Path to your multi‑language PDF
            string pdfPath = @"C:\Docs\multilang.pdf";

            // 4️⃣ Recognize all text
            string fullText = ocrEngine.RecognizeFromFile(pdfPath);
            Console.WriteLine("=== Full extracted text ===");
            Console.WriteLine(fullText);
            Console.WriteLine();

            // 5️⃣ Extract only English (as an example of how to extract text)
            string englishOnly = Regex.Replace(fullText, @"[^\u0000-\u007F]+", string.Empty);
            Console.WriteLine("=== English‑only excerpt ===");
            Console.WriteLine(englishOnly);
        }
    }
}
```

**预期输出**（为节省篇幅已截断）：

```
=== Full extracted text ===
Welcome to our report…
مرحبا بكم في تقريرنا…
ようこそ、私たちのレポートへ…

=== English‑only excerpt ===
Welcome to our report...
```

运行程序，指向你的 PDF，即可在控制台看到完整的多语言文本以及过滤后的英文片段。

## 常见问题（快速解答）

- **这能在 .NET Framework 4.7 上运行吗？**  
  能。Aspose.OCR NuGet 包目标为 .NET Standard 2.0，兼容 .NET Core 与 .NET Framework。

- **如果我要 OCR 图像而不是 PDF，怎么办？**  
  使用 `ocrEngine.RecognizeFromImage("image.png")`。语言标志同样适用，仍然是 **如何启用 OCR** 的一步。

- **可以把输出写入 .txt 文件吗？**  
  完全可以。将 `Console.WriteLine(fullText);` 替换为 `File.WriteAllText("output.txt", fullText);`。

- **有没有办法获取置信度分数？**  
  Aspose.OCR 提供 `OcrResult` 对象，可读取每个单词的 `Confidence`。请参考 API 文档中的 `RecognizeFromFile(..., out OcrResult result)`。

## 结论

我们已经完整覆盖了 **如何在 C# 中启用 OCR**，展示了 **如何将 PDF 转换为文本**，解释了 **如何从特定语言段落提取文本**，并演示了 **如何可靠地识别 PDF** 文件。上面的可运行代码为你在任何 .NET 应用中集成 OCR 打下坚实基础——无论是文档管理系统、自动化发票处理器，还是多语言搜索索引。

下一步？尝试将语言标志切换为中文或韩文，实验 `ImageProcessingOptions` 以处理噪声扫描，或将提取的文本输送到自然语言处理管道中。所有这些扩展仍然依赖同一个核心原则：在开始时 **正确地启用 OCR**。

祝编码愉快，愿你的 PDF 永远可搜索！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}