---
category: general
date: 2026-01-09
description: c# OCR 教程，展示如何使用 Aspose.OCR 从图像文件提取文本并将 DJVU 转换为文本。几分钟内即可学习分步提取。
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- how to extract text
- convert djvu to text
- extract text from djvu
language: zh
og_description: c# OCR 教程，快速演示如何使用 Aspose.OCR 从图像文件提取文本并将 DJVU 转换为文本。请按照指南获取可行的解决方案。
og_title: c# OCR 教程 – 从图像和 DJVU 中提取文本
tags:
- OCR
- C#
- Aspose
title: C# OCR 教程：从图像和 DJVU 文件中提取文本
url: /zh/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教程 – 从图像和 DJVU 文件中提取文本

是否曾经想过如何在不抓狂的情况下从图像文件中提取文本？在本 **c# OCR 教程** 中，我们将演示一个完整的、可直接运行的示例，能够从普通图片 *以及* DJVU 文档中提取文本。  

如果你也在寻找一种快速的 **将 DJVU 转换为文本** 的方法，你来对地方了——无需额外的转换器，只需纯 C# 代码。

## 你将学到

- 如何在 .NET 项目中设置 Aspose.OCR 库。  
- 提取图像文本所需的完整代码 **extract text from image**。  
- 一种简洁的 **extracting text from DJVU** 文件的方法（是的，同一个引擎即可）。  
- 常见的陷阱（大文件、缺少字体、授权）以及如何避免它们。  

你只需要一个最新的 .NET SDK 和网络连接来获取 NuGet 包。无需任何 OCR 经验。

## 前提条件

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 或更高 | Aspose.OCR 目标是 .NET Standard 2.0，因此 .NET 6+ 能提供最佳性能。 |
| Visual Studio 2022（或 VS Code） | IDE 让包管理变得轻松，但任何编辑器都可以使用。 |
| NuGet 包 **Aspose.OCR** | 这就是实际执行繁重任务的引擎。 |
| 示例图像 (`sample.png`) 和 DJVU 文件 (`sample.djvu`) | 我们将使用它们来演示两种提取场景。 |

你可以使用以下命令安装该包：

```bash
dotnet add package Aspose.OCR
```

> **技巧提示：** 如果你在 CI 服务器上构建，请在构建步骤中添加 `--no-restore`，并在开始时一次性恢复，以加快速度。

## 步骤 1：初始化 OCR 引擎 – c# OCR 教程的核心

我们首先要做的是创建一个 `OcrEngine` 实例。可以把它想象成在软件中打开扫描仪。

```csharp
using Aspose.OCR;

var ocrEngine = new OcrEngine();
```

为什么每次都创建新的引擎？因为引擎会保存配置（语言、检测模式等）。重新创建可以避免旧设置在不同运行之间泄漏。

## 步骤 2：加载并识别图像 – 如何从图像中提取文本

现在我们将把普通位图（PNG、JPEG、BMP…）输入到引擎中。`RecognizeImage` 方法返回检测到的字符串。

```csharp
// Path to your image file
string imagePath = @"C:\OCR\sample.png";

// Perform OCR
string imageText = ocrEngine.RecognizeImage(imagePath);

// Show the result
Console.WriteLine("=== Text extracted from image ===");
Console.WriteLine(imageText);
```

需要注意的几点：

* **文件存在性** – 如果路径错误，方法会抛出 `FileNotFoundException`。如果预期用户提供路径，请使用 `try/catch` 包裹。
* **图像质量** – OCR 在 300 dpi 或更高时效果最佳。低分辨率扫描可能导致输出乱码。
* **语言支持** – 默认情况下 Aspose.OCR 假设英文。若要更改，需在 `RecognizeImage` 之前设置 `ocrEngine.Language = Language.Spanish;`。

## 步骤 3：识别 DJVU 文档中的文本 – 将 DJVU 转换为文本

DJVU 是一种可以容纳多页的容器格式。Aspose.OCR 能直接处理，只需指向该文件即可。

```csharp
// Path to your DJVU file
string djvuPath = @"C:\OCR\sample.djvu";

// Perform OCR on the DJVU file
string djvuText = ocrEngine.RecognizeImage(djvuPath);

// Output the result
Console.WriteLine("\n=== Text extracted from DJVU ===");
Console.WriteLine(djvuText);
```

在内部，引擎会将每页提取为图像并运行相同的识别流水线。这就是为什么你不需要单独的 “将 DJVU 转换为文本” 步骤——OCR 引擎已经为你完成。

### 处理多页 DJVU 文件

如果你的 DJVU 包含多页，`RecognizeImage` 会按顺序将它们连接起来。若需要每页单独处理，可使用返回 `List<string>` 的重载：

```csharp
var pagesText = ocrEngine.RecognizeImage(djvuPath, true); // true = return per‑page list
for (int i = 0; i < pagesText.Count; i++)
{
    Console.WriteLine($"\n--- Page {i + 1} ---");
    Console.WriteLine(pagesText[i]);
}
```

## 步骤 4：微调引擎以提升准确率 – 为什么这很重要

开箱即用的结果尚可，但通过调整几个设置可以进一步提升。

```csharp
ocrEngine.Language = Language.English;      // set detection language
ocrEngine.Dpi = 300;                        // enforce 300 DPI processing
ocrEngine.IsDetectOrientation = true;      // auto‑rotate tilted pages
ocrEngine.IsDetectSkew = true;              // correct slanted text
```

这些标志在 **how to extract text** 从先保存为 DJVU 的扫描 PDF 时尤为有用。开启方向检测可免去手动旋转图像的步骤。

## 步骤 5：处理授权和运行时错误

Aspose.OCR 附带免费试用版，在输出几页后会加上 “Demo” 水印。要去除水印，请添加你的授权文件：

```csharp
// Assuming you have a license.xml in the project root
var license = new Aspose.OCR.License();
license.SetLicense("license.xml");
```

如果忘记此步骤，引擎仍可工作，但结果中会出现 “Demo”。另外，处理超大 DJVU 文件时要留意 `OutOfMemoryException`——可考虑如前所示逐页处理。

## 完整、可运行的示例

下面是一个独立的控制台程序，整合了所有步骤。复制粘贴，调整文件路径，然后点击 **Run**。

```csharp
// Complete c# OCR tutorial – extract text from image and DJVU
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Set up licensing (optional, removes demo watermark)
            // var license = new License();
            // license.SetLicense("license.xml");

            // 2️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = Language.English,
                Dpi = 300,
                IsDetectOrientation = true,
                IsDetectSkew = true
            };

            // 👉 Extract text from a regular image
            string imagePath = @"C:\OCR\sample.png";
            try
            {
                string imageText = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("=== Text extracted from image ===");
                Console.WriteLine(imageText);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Image OCR failed: {ex.Message}");
            }

            // 👉 Extract text from a DJVU file (convert DJVU to text)
            string djvuPath = @"C:\OCR\sample.djvu";
            try
            {
                // Single string for all pages
                string djvuText = ocrEngine.RecognizeImage(djvuPath);
                Console.WriteLine("\n=== Text extracted from DJVU ===");
                Console.WriteLine(djvuText);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"DJVU OCR failed: {ex.Message}");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**预期输出**（假设文件中包含短语 “Hello World”）：

```
=== Text extracted from image ===
Hello World

=== Text extracted from DJVU ===
Hello World
```

如果源文件包含多行，它们将与原始文档完全一致地显示。

## 常见问题与边缘案例处理

* **如果图像是黑白的怎么办？**  
  OCR 能正常工作，但可以通过 `ocrEngine.ImagePreprocessOptions = ImagePreprocessOptions.Contrast;` 提高对比度。

* **我只能提取数字吗？**  
  可以——在调用 `RecognizeImage` 前设置 `ocrEngine.CharWhitelist = "0123456789";`。

* **文件大小有上限吗？**  
  引擎会将整个文件读取到内存中。对于大于约 100 MB 的文件，请采用逐页处理（参见步骤 3 的列表重载）。

* **这与 Tesseract 有何不同？**  
  Aspose.OCR 是商业库，内置 DJVU 支持且无本地依赖，而 Tesseract 需要本地二进制文件和单独的 DJVU 转换工具。

## 结论

你刚刚完成了一个 **c# OCR 教程**，展示了如何使用 Aspose.OCR **从图像文件中提取文本** 并无缝 **将 DJVU 转换为文本**。示例涵盖了从包安装到授权、从单页图像提取到多页 DJVU 处理，甚至包括提升准确率的技巧。  

接下来，你可以探索 **how to extract text** 从 PDF 中提取文本、将 OCR 步骤集成到 Web API，或尝试多语言文档的语言包。可能性无限——只需记住关键要点：设置引擎、提供文件、读取返回的字符串。  

还有其他问题吗？留下评论，在自己的文档上尝试代码，祝编码愉快！ 

![c# OCR 教程截图显示控制台输出](/images/csharp-ocr-tutorial.png "c# OCR 教程 – 控制台输出示例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}