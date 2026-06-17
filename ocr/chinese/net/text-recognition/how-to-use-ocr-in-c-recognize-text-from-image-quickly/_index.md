---
category: general
date: 2026-02-16
description: 如何在 C# 中使用 OCR 识别图像中的文本、从 JPEG 中提取文本，并使用 Aspose OCR 将图像转换为文本。一步一步的指南。
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from jpeg
- convert image to text
- how to extract text
language: zh
og_description: 学习如何在 C# 中使用 OCR 识别图像文字、提取 JPEG 文本并将图像转换为文本，附完整代码和技巧。
og_title: 如何在 C# 中使用 OCR – 从图像识别文本
tags:
- C#
- Aspose OCR
- Image Processing
title: 如何在 C# 中使用 OCR – 快速识别图像中的文字
url: /zh/net/text-recognition/how-to-use-ocr-in-c-recognize-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 快速识别图像中的文字

有没有想过在 .NET 项目中 **how to use OCR** 从图片中提取文字？你并不孤单。许多开发者在需要 *recognize text from image*（从图像中识别文字）时，尤其是 JPEG 文件，常常卡住，最终只能寻找一个“神奇”的代码片段来实现。

事实是——Aspose OCR 让整个过程轻而易举。在本教程中，我们将逐步演示如何 **convert image to text**，从 JPEG 中提取文字，并且——是的——你将在控制台上看到确切的输出。没有模糊的引用，只有完整可运行的示例。

## 您将学习

- 安装 Aspose OCR NuGet 包。
- 在 **online mode**（在线模式）下初始化 OCR 引擎，以便自动获取缺失的语言包。
- 加载西里尔文语言模型（或任何你需要的其他语言）。
- 将 JPEG 图像提供给引擎并 **recognize text from image**。
- 处理常见的陷阱，如文件缺失或不受支持的格式。
- 查看可以直接复制粘贴到 Visual Studio 的完整代码。

> **Pro tip:** 如果你在处理扫描的 PDF，可以将每页提取为图像并喂给同一个引擎——代码无需任何更改。

---

## 前置条件

在开始之前，请确保你拥有：

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | Aspose  OCR 目标是现代运行时。 |
| Visual Studio 2022 (or any IDE you like) | 方便的调试和 IntelliSense。 |
| A JPEG image containing text (e.g., `cyrillic_sample.jpg`) | 我们将在演示中 **extract text from JPEG**。 |
| Internet connection (for the first run) | 引擎在 **online mode** 下下载语言包。 |

如果缺少其中任何一项，教程仍然可以编译，但 OCR 引擎可能会在找不到语言模型时抛出异常。

## 步骤 1 – 安装 Aspose OCR NuGet 包

首先需要的是库本身。打开 **Package Manager Console** 并运行：

```powershell
Install-Package Aspose.OCR
```

或者，如果你更喜欢使用 UI，在 NuGet 包管理器中搜索 “Aspose.OCR” 并点击 **Install**。这会拉取所有必需的 DLL，包括核心 OCR 引擎以及可以按需获取的语言模型。

> **Why this step matters:** 没有此包，`OcrEngine` 或 `LanguageModel` 等类将不存在，代码将无法编译。

## 步骤 2 – 初始化 OCR 引擎（主要关键词）

现在库已经就绪，我们可以通过创建 `OcrEngine` 实例来 **how to use OCR**。使用 `ResourceMode.Online` 会让 Aspose 自动获取任何缺失的语言包，这对于快速原型非常合适。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine in online mode.
// This will download language packs if they aren’t already present.
OcrEngine ocrEngine = new OcrEngine(ResourceMode.Online);
```

> **What’s happening under the hood?** 引擎会联系 Aspose 的 CDN，检查你请求的语言模型，并将必要的文件拉取到本地缓存。后续运行将离线进行，加快处理速度。

## 步骤 3 – 加载所需的语言模型

如果处理的是英文文本，默认是 `LanguageModel.English`。在我们的示例中我们将加载 **Cyrillic**，但你可以替换为任何受支持的语言。

```csharp
// Load the Cyrillic language model so the engine knows which characters to look for.
ocrEngine.LoadLanguage(LanguageModel.Cyrillic);
```

> **Edge case:** 如果尝试加载不受支持的语言（例如 `LanguageModel.Klingon`），将抛出 `UnsupportedLanguageException`。如果你正在构建允许用户实时选择语言的 UI，请将调用包装在 try‑catch 块中。

## 步骤 4 – 提供图像（次要关键词：extract text from jpeg）

这里我们将引擎指向包含我们想读取文字的 JPEG 文件。`ImageStream.FromFile` 接受 Aspose 能解码的任何图像格式，但 JPEG 是照片和截图中最常用的。

```csharp
// Replace the path with the actual location of your JPEG image.
string imagePath = @"C:\Images\cyrillic_sample.jpg";

if (!File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Load the image into the OCR engine.
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **Why this matters:** 提供不存在的路径会导致 `FileNotFoundException`。上面的防护代码防止程序崩溃，并向用户提供明确的提示信息。

## 步骤 5 – 从图像中识别文字并输出

**how to use OCR** 的核心是 `Recognize` 方法。它返回一个普通字符串，包含所有检测到的字符，并在可能的情况下保留换行。

```csharp
try
{
    // Perform the OCR operation.
    string recognizedText = ocrEngine.Recognize();

    // Output the extracted text to the console.
    Console.WriteLine("📝 Recognized Text:");
    Console.WriteLine(recognizedText);
}
catch (Exception ex)
{
    Console.WriteLine($"⚠️ OCR failed: {ex.Message}");
}
```

### 预期的控制台输出

如果 JPEG 包含短语 “Привет мир”（俄语的 Hello world），你会看到类似如下的输出：

```
📝 Recognized Text:
Привет мир
```

如果图像模糊，输出可能会出现乱码——这时预处理（例如提升对比度）可以帮助，我们稍后会提到。

## 步骤 6 – 完整可运行示例（所有步骤合并）

下面是完整的程序代码，你可以复制到新的 **Console App** 项目中。它包含了从包安装到错误处理的全部内容，直接运行即可。

```csharp
// ------------------------------------------------------------
// Complete OCR Example – How to use OCR in C#
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine (online mode auto‑downloads language packs)
            OcrEngine ocrEngine = new OcrEngine(ResourceMode.Online);

            // 2️⃣ Load the language model you need (Cyrillic in this demo)
            try
            {
                ocrEngine.LoadLanguage(LanguageModel.Cyrillic);
            }
            catch (Exception langEx)
            {
                Console.WriteLine($"❌ Language load error: {langEx.Message}");
                return;
            }

            // 3️⃣ Provide the image – this is where we **extract text from jpeg**
            string imagePath = @"YOUR_DIRECTORY\cyrillic_sample.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Cannot find image at {imagePath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Recognize text – the heart of **how to use OCR**
            try
            {
                string recognizedText = ocrEngine.Recognize();

                // 5️⃣ Output – **convert image to text** and display it
                Console.WriteLine("📝 Recognized Text:");
                Console.WriteLine(recognizedText);
            }
            catch (Exception ocrEx)
            {
                Console.WriteLine($"⚠️ OCR operation failed: {ocrEx.Message}");
            }
        }
    }
}
```

> **Quick test:** 将 `YOUR_DIRECTORY\cyrillic_sample.jpg` 替换为实际包含清晰文字的 JPEG 路径。运行项目（F5），观察控制台打印提取的字符串。

## 步骤 7 – 提示、边缘情况和常见问题

### 如何 **recognize text from image** 除了 JPEG 之外的文件？

Aspose OCR 支持 PNG、BMP、TIFF，甚至是 PDF 页面（先将其转换为图像）。只需在 `ImageStream.FromFile` 中更改文件扩展名。相同的代码即可工作——无需额外配置。

### 如果图像分辨率低怎么办？

OCR 准确率在低于 300 dpi 时会显著下降。你可以通过以下方式提升效果：

1. 使用类似 **ImageSharp** 的库对图像进行放大。
2. 应用二值阈值以提升对比度。
3. 设置 `ocrEngine.Settings.Deskew = true` 来校正倾斜文字。

```csharp
ocrEngine.Settings.Deskew = true; // Auto‑corrects rotated text
```

### 我可以批量 **convert image to text** 吗？

当然可以。将识别逻辑包装在遍历图像文件夹的 `foreach` 循环中。记得复用同一个 `OcrEngine` 实例——它会缓存语言包并加速批处理。

```csharp
string[] files = Directory.GetFiles(@"C:\Images", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    string txt = ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), txt);
}
```

### 这在 Linux/macOS 上可用吗？

可以。只要安装了 .NET 运行时，Aspose OCR 就是跨平台的。唯一的限制是图像解码的本地依赖，这些已随 NuGet 包一起打包。

### 如何在保留布局的情况下 **extract text from jpeg**？

设置 `ocrEngine.Settings.PreserveFormatting = true`。这会保留换行和简单表格，使输出更易阅读。

```csharp
ocrEngine.Settings.PreserveFormatting = true;
```

## 结论

通过几个步骤，我们展示了在 C# 中 **how to use OCR**，以及如何使用 Aspose OCR **recognize text from image**、**extract text from JPEG** 和 **convert image to text**。完整示例开箱即用，能够处理文件缺失，并在控制台上即时反馈。

接下来你可以：

- 将 `LanguageModel.Cyrillic` 替换为其他语言（English、Arabic、Chinese 等）。
- 批量处理图像文件夹，实现数据录入自动化。
- 将 OCR 与自然语言处理结合，索引扫描文档。

现在就动手吧——尝试代码，实验不同的图像质量，让引擎完成繁重的工作。如果遇到问题，社区（以及 Aspose 的文档）随时可查。祝编码愉快！

---

![如何使用 OCR 示例截图](placeholder-image.png "C# 中如何使用 OCR 示例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}