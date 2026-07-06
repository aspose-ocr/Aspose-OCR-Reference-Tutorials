---
category: general
date: 2026-04-06
description: 使用 Aspose OCR 在 C# 中识别图像文字。学习如何提取文本、加载图像文件（C#），以及在 C# 中写入 JSON，提供一个简单的逐步示例。
draft: false
keywords:
- recognize image text
- how to extract text
- write json in c#
- load image file c#
language: zh
og_description: 使用 Aspose OCR 在 C# 中识别图像文字。本指南展示如何提取文本、加载图像文件（C#），以及快速在 C# 中写入 JSON。
og_title: 在 C# 中识别图像文字 – 完整的逐步指南
tags:
- OCR
- C#
- Aspose
title: 在 C# 中识别图像文字 – 完整指南与 JSON 导出
url: /zh/net/text-recognition/recognize-image-text-in-c-full-guide-with-json-export/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中识别图像文字 – 完整分步指南

是否曾经需要从扫描的收据中**recognize image text**，但不确定该选哪个库？你并不是唯一的遇到这种情况的人。在许多实际应用中——费用跟踪器、发票处理器，甚至辅助工具——从图片中提取文字是第一道难关。  

在本教程中，我们将手把手演示一个使用 Aspose OCR 库的**recognize image text**解决方案，展示**how to extract text**的用法，正确演示**load image file c#**，最后**write json in c#**，以便您可以存储或传输结果。完成后，您将拥有一个可直接运行的控制台应用程序，能够将任意 PNG 转换为整洁的 JSON 负载。

---

## 您需要的环境

- **.NET 6+**（代码同样适用于 .NET Framework 4.8，但 .NET 6 是最佳选择）。
- **Aspose.OCR for .NET** NuGet 包。使用 `dotnet add package Aspose.OCR` 安装。
- 一个示例图像（`input.png`），放在应用程序能够读取的位置。  
- Visual Studio 2022 或您喜欢的任何编辑器——无需花哨的 IDE 技巧。

> 小技巧：将图像文件放在项目内部名为 `Resources` 的文件夹中；这样路径更整洁，避免“文件未找到”的麻烦。

## 步骤 1：recognize image text – 加载图像文件

在 OCR 引擎发挥魔力之前，您必须安全地**load image file c#**。如果路径错误或文件格式不受支持，`Image.FromFile` 方法会抛出异常，因此我们需要对此进行防护。

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // Verify the image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // Load the image – this is the “load image file c#” step
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // Continue to OCR...
        }
    }
}
```

*为什么重要*：在 `using` 块中加载图像可确保非托管的 GDI+ 资源及时释放，防止长期运行的服务出现内存泄漏。

## 步骤 2：使用 Aspose OCR 提取文字

现在位图已在内存中，我们将其交给**recognize image text**引擎。Aspose 的 `OcrEngine` 使用非常直接：实例化后调用 `Recognize`，即可得到包含原始文本、置信度分数，甚至边界框的 `OcrResult` 对象。

```csharp
// Inside the using block from Step 1
var ocrEngine = new OcrEngine();

// Perform OCR – this is the core “how to extract text” operation
OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

// Quick sanity check
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("⚠️ No text detected. Try a clearer image.");
    return;
}
Console.WriteLine("✅ OCR succeeded. Extracted text:");
Console.WriteLine(ocrResult.Text);
```

*说明*：`Recognize` 方法运行内置的神经网络。它在高对比度、300 DPI 的图像上表现最佳。如果输入模糊的照片，置信度会下降——在生产代码中请考虑预处理（去倾斜、二值化）。

## 步骤 3：在 C# 中写入 JSON – 导出 OCR 结果

大多数 API 期待 JSON，因此我们将使用 Aspose 的 `JsonExport` **write json in c#**。该库会序列化整个 `OcrResult`，保留行信息和置信度值。

```csharp
// Still inside the same using block
string jsonResult = JsonExport.ToJson(ocrResult);

// Persist the JSON to disk
File.WriteAllText(outputPath, jsonResult);
Console.WriteLine($"💾 JSON written to {outputPath}");
```

### 预期的 JSON 输出

```json
{
  "Text": "Total: $12.34\r\nDate: 2026-04-01\r\n...",
  "Words": [
    { "Text": "Total", "Confidence": 0.98, "Rectangle": { "X": 10, "Y": 15, "Width": 50, "Height": 12 } },
    { "Text": "$12.34", "Confidence": 0.96, "Rectangle": { "X": 70, "Y": 15, "Width": 45, "Height": 12 } }
    // … more words …
  ]
}
```

*为什么使用 JSON*？它与语言无关，易于反序列化，并保留您在后续验证中可能需要的详细 OCR 元数据。

## 步骤 4：完整、可运行的程序

将各部分组合起来，这里是完整的控制台应用程序。复制粘贴，恢复 NuGet 包，然后按 **F5** 运行。

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Configuration – adjust these paths as needed
        // -------------------------------------------------
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // -------------------------------------------------
        // Validate input file
        // -------------------------------------------------
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // -------------------------------------------------
        // Load image (load image file c#)
        // -------------------------------------------------
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // -------------------------------------------------
            // Initialize OCR engine and recognize text
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("⚠️ No text detected. Try a clearer image.");
                return;
            }

            Console.WriteLine("✅ OCR succeeded. Sample output:");
            Console.WriteLine(ocrResult.Text.Substring(0, Math.Min(100, ocrResult.Text.Length)) + "...");

            // -------------------------------------------------
            // Convert result to JSON (write json in c#)
            // -------------------------------------------------
            string jsonResult = JsonExport.ToJson(ocrResult);
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"💾 JSON written to {outputPath}");
        }
    }
}
```

运行程序并打开 `Resources/output.json`——您应该能看到引擎识别的所有内容的结构良好的 JSON 表示。

## 处理常见边缘情况

| Situation | What to Do | Why |
|-----------|------------|-----|
| **图像为空或损坏** | 在 `Image.FromFile` 周围使用 try/catch 并记录异常。 | 防止应用崩溃并提供清晰的错误信息。 |
| **置信度分数低** | 检查 `ocrResult.Words[i].Confidence`。如果低于 0.75，考虑进行预处理（提升 DPI，锐化）。 | 提升下游流程（如金额提取）的可靠性。 |
| **大文件（>10 MB）** | 在 OCR 前缩小图像尺寸（`receiptImage = new Bitmap(receiptImage, new Size(width/2, height/2))`）。 | 降低内存压力并加快识别速度。 |
| **多语言文档** | 设置 `ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;` | 使引擎能够检测两种语言的字符。 |

## 额外：可视化 OCR 结果（可选）

如果您想查看每个单词在图像上的位置，可以绘制边界框：

```csharp
using (Graphics g = Graphics.FromImage(receiptImage))
{
    foreach (var word in ocrResult.Words)
    {
        var rect = new Rectangle(word.Rectangle.X, word.Rectangle.Y,
                                 word.Rectangle.Width, word.Rectangle.Height);
        g.DrawRectangle(Pens.Red, rect);
    }
    receiptImage.Save(Path.Combine("Resources", "annotated.png"));
}
```

生成的 `annotated.png` 将在每个识别的单词周围显示红色矩形——对调试非常有帮助。

## 结论

我们已经在 C# 中完整地**recognize image text**：从加载图像文件、调用 Aspose OCR **how to extract text**，到最终**write json in c#**，使数据可以随处传输。完整示例开箱即用，额外的技巧帮助您处理模糊收据、大文件或多语言扫描。

接下来可以做什么？尝试将 Aspose 替换为其他引擎（如 Tesseract、Microsoft OCR）并比较置信度分数，或将 JSON 导入数据库用于费用报表。您还可以将控制台应用扩展为接受图像上传并即时返回 JSON 的 ASP .NET Core Web API。

关于扩展、错误处理或与 Azure Functions 集成有疑问？在评论区留言或在 GitHub 上联系我。祝编码愉快，愿您的 OCR 始终清晰！

---

![OCR JSON 输出截图 – recognize image text 示例](https://example.com/ocr-example.png "recognize image text 示例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}