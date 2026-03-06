---
category: general
date: 2026-03-05
description: 使用 Aspose OCR 在 C# 中提取图像文本。学习在 C# 中读取图像文件、将 DJVU 转换为文本，并快速获取 OCR 图像转字符串的结果。
draft: false
keywords:
- extract text from image
- read image file c#
- convert djvu to text
- ocr image to string
- recognize text from djvu
language: zh
og_description: 使用 Aspose OCR 在 C# 中从图像提取文本。本指南展示了如何在 C# 中读取图像文件、将 DJVU 转换为文本，以及轻松实现
  OCR 图像转字符串。
og_title: 在 C# 中从图像提取文本 – 完整的 Aspose OCR 指南
tags:
- Aspose OCR
- C#
- Image Processing
title: 在 C# 中从图像提取文本 – Aspose OCR 逐步教程
url: /zh/net/text-recognition/extract-text-from-image-in-c-aspose-ocr-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中从图像提取文本 – 完整 Aspose OCR 指南

是否曾经需要**从图像中提取文本**却不确定使用哪个库才能得到可靠的结果？也许你手头有一批 DJVU 扫描文件，只想直接得到纯文本而不想使用第三方工具。本文将在几分钟内使用 Aspose OCR for .NET 为你解决这个问题。

我们将演示如何在 C# 中读取图像文件、将 DJVU 文档转换为文本，以及将任意 OCR 图像转化为干净的字符串。完成后，你将拥有一个可直接运行的控制台应用程序，能够将识别出的文本打印到控制台。没有模糊的“参考文档”链接——只有完整的复制粘贴解决方案。

## 你需要准备的环境

- **.NET 6.0** 或更高版本（代码同样适用于 .NET Framework 4.6+）。  
- **Aspose.OCR for .NET** NuGet 包（免费试用许可证即可用于测试）。  
- 一个 DJVU 文件或任意受支持的图像（PNG、JPEG、BMP 等）。  
- Visual Studio、Rider 或你喜欢的编辑器。

如果缺少上述任意项，只需安装 NuGet 包：

```bash
dotnet add package Aspose.OCR
```

就这么简单。下面开始吧。

## 第一步：初始化 OCR 引擎 – 从图像提取文本

首先创建一个 `OcrEngine` 实例。把它想象成读取像素并将其转换为字符的大脑。

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

为什么要在加载文件之前实例化引擎？Aspose 的设计将配置（如授权）与实际图像数据分离，这样你可以在多个文件之间复用同一个引擎，而无需重复创建对象——这能带来一点性能提升。

## 第二步：应用 Aspose OCR 授权（可选但推荐）

如果你拥有商业授权，请在此设置。跳过此步骤会进入演示模式，输出会带有水印并限制页数。

```csharp
        // Apply license – remove this line if you’re using the free trial
        ocrEngine.SetLicense("Aspose.OCR.lic");
```

**小贴士：** 将授权文件放在源码控制之外（例如通过环境变量），以免意外提交。

## 第三步：加载图像 – 轻松读取图像文件 C#

Aspose 能读取多种格式，包括少见的 DJVU。我们将使用 `ImageStream.FromFile` 辅助方法将文件加载到引擎中。

```csharp
        // Load the image (DJVU, PNG, JPEG, etc.)
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.djvu");
```

如果你更倾向于使用 `byte[]`（例如图像来自数据库），可以改用 `ImageStream.FromBytes(byteArray)`。当需要**从流而非磁盘读取图像文件 C#**时，这种灵活性非常有用。

## 第四步：执行 OCR – 一次调用将图像转为字符串

现在魔法开始了。调用 `Recognize()` 会运行 OCR 引擎并返回一个 `RecognitionResult`，其中包含提取的文本、置信度分数等信息。

```csharp
        // Run OCR and get the result
        var result = ocrEngine.Recognize();

        // Extract plain text
        string recognizedText = result.Text;
```

为什么不直接调用 `Recognize().Text`？将调用拆分后，你可以在后续检查 `result.Confidence` 或 `result.Regions`，获取更细粒度的数据——这对调试或构建高亮低置信度词汇的 UI 很有帮助。

## 第五步：显示提取的文本 – 最终输出

最后，将文本写入控制台。在真实项目中，你可能会写入文件、数据库，或通过 API 发送。

```csharp
        // Show the result
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

**预期输出**（为简洁起见已截断）：

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

如果 OCR 引擎未能识别任何字符，`recognizedText` 将是空字符串。此时请检查图像质量，或尝试调整引擎的语言设置（例如 `ocrEngine.Language = Language.English;`）。

## 将 DJVU 转换为文本 – 批量识别 djvu 文本

如果你有成百上千个 DJVU 文件需要处理，可以将前面的逻辑放入循环：

```csharp
string[] files = Directory.GetFiles("YOUR_DIRECTORY", "*.djvu");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    string text = ocrEngine.Recognize().Text;
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), text);
    Console.WriteLine($"Converted {Path.GetFileName(file)} → {Path.GetFileNameWithoutExtension(file)}.txt");
}
```

此代码段**自动将 DJVU 转为文本**，在每个源文件旁生成相应的 `.txt` 文件。它是将旧版扫描文档快速构建可搜索归档的利器。

## 处理边缘情况 – 图像噪声怎么办？

当图像模糊、对比度低或背景有颜色时，OCR 准确率会下降。Aspose OCR 提供了预处理选项：

```csharp
// Example: Binarize the image to improve contrast
ocrEngine.Image = ImageProcessing.Binarize(ocrEngine.Image, threshold: 128);
```

另外，你可以让引擎自动检测语言：

```csharp
ocrEngine.Language = Language.Detect; // Detects language based on content
```

这些调优往往能把 60% 的准确率提升到 95%。如果遇到问题，可尝试 `Threshold`、`Denoise` 或 `Deskew` 方法。

## 完整可运行示例 – 复制、粘贴、运行

下面是完整程序代码，直接编译即可。将 `"YOUR_DIRECTORY/input.djvu"` 替换为你的文件路径，并确保授权文件可访问。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Apply license (optional)
        // ocrEngine.SetLicense("Aspose.OCR.lic"); // Uncomment if you have a license

        // 3️⃣ Load the image (DJVU, PNG, JPEG, etc.)
        string imagePath = "YOUR_DIRECTORY/input.djvu";
        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 4️⃣ Perform OCR
        var result = ocrEngine.Recognize();
        string recognizedText = result.Text;

        // 5️⃣ Output the text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

使用以下命令运行：

```bash
dotnet run
```

你应该会在控制台看到提取的文本，效果与前面的示例完全一致。

## 常见问题与注意事项

- **这能处理 PDF 文件吗？**  
  不能直接。Aspose OCR 只处理光栅图像；若要处理 PDF，需要先使用 Aspose.PDF 将每页转换为图像，然后再交给 OCR 引擎。

- **如果在服务器上批量处理大量文件怎么办？**  
  实例化**单个** `OcrEngine` 并在多个线程间复用。该引擎对只读操作是线程安全的，但请避免同时共享同一个 `Image` 实例。

- **能提取带格式的信息（字体、大小）吗？**  
  Aspose OCR 只返回纯 Unicode 文本。若需保留布局，需要使用更高级的解决方案，如 OCR‑ML 或能够保持布局的 PDF 库。

## 后续步骤 – 扩展工作流

现在你已经能够**可靠地从图像中提取文本**，可以考虑：

- 将结果存入 Elasticsearch，实现全文检索。  
- 将文本输入语言模型进行摘要。  
- 使用 ASP.NET Core 构建简易 UI，实现文件上传并即时查看 OCR 结果。  

所有这些都基于我们刚才讲的核心代码，你已经具备了进一步扩展的基础。

---

### 快速回顾

- 我们**初始化**了 `OcrEngine`（Aspose OCR 的核心）。  
- 应用了**授权**以解锁全部功能。  
- 使用 `ImageStream.FromFile` **加载**了 DJVU 文件。  
- 调用了 `Recognize()` 获得**ocr image to string**结果。  
- 将**提取的文本**打印到控制台。  

这就是使用 C# 将任何受支持的图像（包括 DJVU）转换为可搜索文本的完整配方。

---

欢迎尝试不同的图像格式，调节预处理设置，或将此代码与其他 Aspose 库链式调用。如果遇到问题，欢迎在下方留言——祝编码愉快！  

![从图像提取文本示例](/images/ocr-example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}