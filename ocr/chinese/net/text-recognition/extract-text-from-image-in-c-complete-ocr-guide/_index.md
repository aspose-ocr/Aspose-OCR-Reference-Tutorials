---
category: general
date: 2026-07-21
description: 使用 C# OCR 从图像中提取文本——学习将 PNG 转换为文本、加载图像进行 OCR，并使用 Aspose 识别西里尔文文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- c# ocr example
- load image for ocr
- recognize cyrillic text
language: zh
lastmod: 2026-07-21
og_description: 使用 C# OCR 从图像中提取文本。本指南展示了如何将 PNG 转换为文本、加载图像进行 OCR，以及使用 Aspose.OCR
  识别西里尔文字。
og_image_alt: Screenshot of C# code extracting text from an image using Aspose OCR
og_title: 在 C# 中从图像提取文本 – 完整 OCR 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using C# OCR – learn to convert PNG to text,
    load image for OCR, and recognize Cyrillic text with Aspose.
  headline: Extract Text from Image in C# – Complete OCR Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
- Cyrillic
title: 在 C# 中从图像提取文本 – 完整 OCR 指南
url: /zh/net/text-recognition/extract-text-from-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中从图像提取文本 – 完整 OCR 指南

是否曾想过在不离开 C# 项目的情况下 **从图像文件中提取文本**？也许你有一批扫描的收据、一组西里尔字母标识，或只是需要将 PNG 截图转换为可搜索文本。简而言之，你需要一个可靠的 OCR 引擎，能够 *即时将 PNG 转换为文本*。

好消息——Aspose.OCR 只需几行代码即可实现。下面你将看到一个 **C# OCR 示例**，它加载图像进行 OCR，执行识别，并打印结果，即使源语言是西里尔文也能正常工作。

## 本教程涵盖内容

- 为西里尔文识别设置 Aspose.OCR 引擎。  
- **从文件路径或流中加载图像进行 OCR**。  
- **将 PNG 转换为文本** 并输出纯字符串。  
- 处理识别西里尔文时的失败情况和常见陷阱。  

阅读完本指南后，你将拥有一个可直接运行的自包含程序，以及一些保持 OCR 流程稳健的技巧。

> **先决条件**  
> - .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）。  
> - 有效的 Aspose.OCR 许可证或 30 天评估密钥。  
> - 已安装 `Aspose.OCR` NuGet 包（`dotnet add package Aspose.OCR`）。  

如果缺少上述任意项，请先获取——除此之外无需其他准备。

---

## 从图像提取文本 – 步骤 1：安装并初始化 OCR 引擎

首先，需要创建 OCR 引擎实例，并告知它期望的语言。Aspose 支持超过 70 种语言，西里尔文使用 `OcrLanguage.Cyrillic`。

```csharp
using Aspose.OCR;
using System;

// Step 1: Create the engine and set the language to Cyrillic.
OcrEngine engine = new OcrEngine
{
    Language = OcrLanguage.Cyrillic
};
```

> **为什么要设置语言？**  
> 如果引擎猜错了脚本，OCR 准确率会大幅下降。显式指定西里尔文可以让引擎 *抢先一步*——它会缩小需要考虑的字符集，从而加快处理速度并减少误识别。

---

## 将 PNG 转换为文本 – 步骤 2：加载图像进行 OCR

现在我们真正 **加载图像进行 OCR**。示例使用 PNG 文件，Aspose 同时支持 JPEG、BMP、TIFF，甚至 PDF 页面。

```csharp
// Step 2: Load the PNG you want to convert to text.
engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.png");
```

如果你更倾向于使用 `MemoryStream`（例如图像来自 Web 请求），只需将上面的代码行替换为：

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes("sample_cyrillic.png")))
{
    engine.Image = ImageStream.FromStream(ms);
}
```

> **提示：** 为获得最佳效果，请将图像分辨率保持在至少 300 dpi。低分辨率的截图常导致输出乱码，尤其是非拉丁字母时更为明显。

---

## C# OCR 示例 – 步骤 3：执行识别

引擎准备就绪且图像已加载后，实际的 OCR 工作只需一次方法调用。

```csharp
// Step 3: Run the recognition engine.
bool success = engine.Recognize();
```

`Recognize()` 方法在找到可识别文本时返回 `true`。如果返回 `false`，则需要调查原因——可能是图像过于模糊或语言设置不正确。

---

## 识别西里尔文文本 – 步骤 4：获取并使用结果

假设识别成功，你现在可以 **从图像中提取文本** 并进行任意处理：存入数据库、喂入搜索索引，或直接显示。

```csharp
if (success)
{
    // Step 4: Grab the plain text.
    string plainText = engine.Text;
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(plainText);
}
else
{
    // Step 5: Handle recognition failure gracefully.
    Console.WriteLine("Recognition failed. Check image quality or language settings.");
}
```

### 预期输出

对清晰的西里尔文 PNG 运行完整程序后，输出类似如下：

```
=== OCR RESULT ===
Пример текста на кириллице
```

如果图像中同时包含英文和西里尔文，只要语言设置为 Cyrillic，Aspose 会同时输出两种脚本（它包含拉丁子集）。

---

## 常见陷阱与专业技巧

| 问题 | 产生原因 | 解决办法 |
|------|----------|----------|
| **模糊或低分辨率 PNG** | OCR 引擎依赖清晰的字符边缘。 | 将图像放大至 300 dpi，或在送入 Aspose 前使用锐化滤镜。 |
| **语言设置错误** | 引擎尝试将字符匹配到错误的脚本。 | 始终将 `engine.Language` 设置为期望的语言，例如 `OcrLanguage.Cyrillic`。 |
| **大文件导致内存压力** | 将巨大的图像加载到 `MemoryStream` 可能耗尽堆内存。 | 使用 `engine.Image = ImageStream.FromFile(path)` 进行磁盘处理，或分块处理页面。 |
| **识别返回空字符串** | 引擎可能未检测到任何文本区域。 | 在 `Recognize()` 前调用 `engine.SetImageProcessingOptions(new ImageProcessingOptions { DetectTextRegions = true })`。 |

> **专业技巧：** 如果需要批量 **从图像文件中提取文本**，可将上述逻辑包装在 `Parallel.ForEach` 循环中——只需确保每个线程各自创建 `OcrEngine` 实例。该引擎并非线程安全。

---

## 扩展示例：多语言与异步调用

上述代码为同步实现，专注于西里尔文。实际项目中可能需要在同一文档中同时支持英文和西里尔文。Aspose 允许设置 *语言数组*：

```csharp
engine.Language = OcrLanguage.Cyrillic | OcrLanguage.English;
```

对于需要保持 UI 响应的应用，可调用 `RecognizeAsync()`：

```csharp
await engine.RecognizeAsync();
string result = engine.Text; // same property, now filled after await
```

如果走这条路，请将 `Main` 方法标记为 `async Task`。

---

## 完整可运行示例

下面是完整的、可直接复制粘贴的程序。保存为 `Program.cs`，添加 Aspose.OCR NuGet 包，然后在命令行运行。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine and set language to Cyrillic.
        OcrEngine engine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic
        };

        // 2️⃣ Load the PNG you want to convert to text.
        //    Replace the path with your actual file location.
        string imagePath = "YOUR_DIRECTORY/sample_cyrillic.png";

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }

        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Perform the recognition.
        bool success = engine.Recognize();

        // 4️⃣ Retrieve and display the result.
        if (success)
        {
            string plainText = engine.Text;
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(plainText);
        }
        else
        {
            Console.WriteLine("Recognition failed. Verify image quality and language settings.");
        }
    }
}
```

**运行方式：**  

```bash
dotnet run
```

你应该会在控制台看到提取出的西里尔文文本。

---

## 结论

我们通过一个 **C# OCR 示例**，展示了如何使用 Aspose.OCR **从图像文件中提取文本**，特别是 PNG。通过设置语言为西里尔文、正确加载图像以及处理成功与失败两条路径，你现在拥有了进行任何文本提取任务的坚实基础——无论是为搜索索引将 PNG 转换为文本，还是构建多语言文档扫描器。

准备好下一步了吗？尝试将 `OcrLanguage.Cyrillic` 替换为 `OcrLanguage.English` 观察差异，或尝试使用 `ImageProcessingOptions` 改善噪声扫描的准确度。如果遇到问题，Aspose 文档和社区论坛都是深入探索的好去处。

祝编码愉快，愿你的 OCR 结果始终晶莹剔透！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在自己的项目中进一步掌握 API 功能并探索替代实现方式。

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}