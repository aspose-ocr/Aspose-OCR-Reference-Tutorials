---
category: general
date: 2026-02-11
description: 学习如何在 C# 中使用 Aspose OCR 对多页 TIFF 进行 OCR。将 TIFF 转换为文本，提取 TIFF 中的文字，并快速识别图像中的文字。
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: zh
og_description: 如何在 C# 中使用 Aspose OCR 对多页 TIFF 进行 OCR。一步步指南，教您将 TIFF 转换为文本、从 TIFF
  中提取文本以及识别图像中的文字。
og_title: 如何对多页 TIFF 图像进行 OCR – 完整 C# 教程
tags:
- OCR
- C#
- Aspose
- TIFF
title: 使用 Aspose OCR 在多页 TIFF 图像上运行 OCR – C# 指南
url: /zh/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR 对多页 TIFF 图像进行 OCR

有没有想过 **如何运行 OCR** 在包含多页的扫描 TIFF 上？你并不孤单——许多开发者在需要从旧文档中提取可搜索文本时都会遇到这个问题。好消息是？使用 Aspose OCR，你只需几行 C# 代码就能识别图像文件中的文本，最终得到可用于索引或进一步处理的纯文本串。

在本教程中，我们将完整演示工作流：从安装 Aspose OCR 包、加载多页 TIFF、将 TIFF 转换为文本，到最终显示提取的内容。完成后，你将能够 **从 TIFF 中提取文本**、**从图像中识别文本**，甚至在批处理作业中自动处理数十个文件。没有魔法，只有清晰实用的步骤。

## 您将学习的内容

- 如何为英文语言识别设置 Aspose OCR 引擎。  
- 使用 `OcrEngine` 类进行 **将 TIFF 转换为文本** 的完整代码。  
- 处理多页图像的技巧，确保每页正确分隔。  
- 常见陷阱（如缺少本机依赖）以及如何避免它们。  

**先决条件** – 需要 .NET 6 或更高版本、Visual Studio（或任意 C# 编辑器），以及用于自动资源下载功能的网络连接。仅此而已；无需额外的本机库。

---

## 第一步 – 安装 Aspose OCR NuGet 包

在 **对图像执行 OCR** 之前，必须将库添加到项目中。

```bash
dotnet add package Aspose.OCR
```

> **专业提示：** 如果你在 Visual Studio 中工作，也可以右键点击项目 → *Manage NuGet Packages* → 搜索 “Aspose.OCR” 并点击 *Install*。

该包包含你所需的一切，并且通过设置 `AutomaticResourceDownload = true`，引擎会在运行时自动获取语言包。

---

## 第二步 – 初始化 OCR 引擎（如何运行 OCR）

现在库已经就位，我们创建并配置一个 `OcrEngine` 实例。这是 **如何运行 OCR** 场景的核心。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**为什么重要：** 设置 `Language` 告诉引擎期望的字符集，而 `AutomaticResourceDownload` 免去了手动在服务器上放置语言文件的步骤。将 `OutputFormat` 设置为 `Text` 可得到简单的字符串——非常适合 **将 TIFF 转换为文本** 的流水线。

---

## 第三步 – 加载多页 TIFF（从图像识别文本）

TIFF 可以包含多个帧，每个帧代表一页。`System.Drawing.Image` 类为我们抽象了这一点。

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **如果文件不在同一文件夹怎么办？** 只需提供完整的绝对路径，或使用 `Path.Combine` 与 `AppContext.BaseDirectory`。  
> **内存使用情况如何？** `using` 语句在处理完后会释放图像，防止泄漏——在批量处理大量大型 TIFF 时尤为关键。

`Recognize` 调用会自动遍历 TIFF 中的每一页，并使用换行符连接结果。这就是为什么在打印 `ocrResult.Text` 时会看到每页被分隔开的原因。

---

## 第四步 – 完整工作示例（所有步骤在一个文件中）

下面是一个完整的、可直接运行的控制台应用程序。复制粘贴到新的 .NET 控制台项目中并按 **F5** 运行。

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**预期输出**（为简洁起见已截断）：

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

每页都会单独占一行，因为 `OcrOutputFormat.Text` 会在帧之间插入换行符。如果需要不同的分隔符，可以使用 `String.Replace` 对 `result.Text` 进行后处理。

---

## 第五步 – 处理常见边缘情况

### 5.1 大型 TIFF 文件  
处理 GB 级别的 TIFF 时，将整个文件加载到内存可能会出现问题。一种变通方法是逐帧处理：

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. 非英文文档  
如果需要在西班牙语或法语等语言的 **从图像识别文本**，只需更改 `Language` 属性：

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Aspose 会自动下载相应的语言资源。

### 5. 保存输出  
通常你会想要 **将 TIFF 转换为文本** 并将结果存储为 `.txt` 文件：

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

你也可以使用 `String.Split(Environment.NewLine)` 按页拆分输出，并将每段写入单独的文件。

---

## 专业技巧与注意事项

- **AutomaticResourceDownload** 在首次运行应用时有效；后续运行可离线使用。  
- 如果出现乱码，请再次检查 `Language` 设置；语言包不匹配会导致识别错误。  
- 对于已被光栅化为 TIFF 的 PDF，建议提升 `ocrEngine.Dpi`（默认 300），以获得更高的准确度。  
- 始终在 `using` 块中包装 `Image.FromFile`；否则会锁定文件，导致后续无法删除或移动。

---

## 常见问题

**Q: 这能用于单页 TIFF 吗？**  
A: 完全可以。引擎对单帧 TIFF 的处理方式相同，只会返回一行文本。

**Q: 我可以用同样的方式处理 PNG 或 JPEG 文件吗？**  
A: 可以——只需更改文件扩展名。`Recognize` 方法接受任何 `System.Drawing.Image` 支持的格式。

**Q: 如果我需要 OCR 结果为 PDF 而不是纯文本怎么办？**  
A: 将 `OutputFormat = OcrOutputFormat.Pdf`，`ocrResult` 将包含可写入磁盘的 PDF 字节数组。

---

## 结论

现在，你已经拥有一个完整的端到端解决方案，能够使用 Aspose OCR 在 C# 中 **运行 OCR** 对多页 TIFF 文件进行处理。通过配置引擎、加载图像并调用 `Recognize`，你可以 **从 TIFF 中提取文本**、**将 TIFF 转换为文本**，以及 **从图像中识别文本**，仅需几行代码。欢迎根据自己的批处理需求调整语言、输出格式或逐帧处理方式。

准备好下一步了吗？尝试将此方法与文件夹监视服务结合，自动 **对图像执行 OCR**，当文件落入投递文件夹时即进行处理，或将输出集成到搜索索引中，实现即时全文检索。可能性无限，而你刚看到的代码是坚实的基础。

如果遇到任何问题，欢迎在下方留言或在 GitHub 上联系我。祝编码愉快，享受将顽固的 TIFF 转换为可搜索文本的过程！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}