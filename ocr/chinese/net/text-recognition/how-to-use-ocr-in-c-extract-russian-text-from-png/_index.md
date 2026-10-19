---
category: general
date: 2026-02-20
description: 如何在 C# 中使用 OCR 读取 PNG 图像中的文本——学习将图像转换为文本并快速提取俄文文本。
draft: false
keywords:
- how to use ocr
- read text from png
- convert image to text
- recognize image text
- extract russian text
language: zh
og_description: 如何在 C# 中使用 OCR 已在第一句中说明——逐步指南，读取 PNG 中的文本，将图像转换为文本，并提取俄文文本。
og_title: 如何在 C# 中使用 OCR – 完整指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 OCR – 从 PNG 中提取俄文文本
url: /zh/net/text-recognition/how-to-use-ocr-in-c-extract-russian-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中使用 OCR – 从 PNG 中提取俄文文本

有没有想过在 .NET 项目中 **如何使用 OCR**，而不需要花数周时间寻找合适的库？你并不孤单。在许多真实场景的应用中，我们需要 **从 PNG 中读取文本**，将这些图片转换为可搜索的字符串，有时还需要提取俄语处理所需的西里尔字符。

在本教程中，我们将通过一个动手示例，向你展示如何使用 Aspose.OCR **将图像转换为文本**，然后 **识别用俄语书写的图像文本**。完成后，你将拥有一个可直接运行的控制台程序，能够 **从 PNG 文件中提取俄文文本**，并附带一些后续可能遇到的边缘情况的提示。

---

## 您需要的环境

- .NET 6 SDK 或更高版本（代码同样适用于 .NET Core 3.1+）  
- Visual Studio 2022 或任意你喜欢的编辑器（VS Code 也可）  
- **Aspose.OCR** NuGet 包（`Install-Package Aspose.OCR`）  
- 包含俄文字符的示例 PNG（我们将其命名为 `sample_russian.png`）

就这些——无需额外的本机 DLL、外部服务，也不需要疯狂的配置文件。准备好了吗？让我们开始吧。

---

## 第一步 – 初始化 OCR 引擎 (how to use ocr)

当你想 **使用 OCR** 时，首先要做的就是创建一个引擎实例。Aspose 为你完成繁重的工作，包括在首次请求时下载西里尔语言包。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;

// Create the OCR engine – this also triggers a one‑time download of language data
OcrEngine ocrEngine = new OcrEngine();
```

> **为什么这很重要：** 引擎保存所有内部状态（如语言模型），并提供后续将调用的 `Recognize` 方法。只实例化一次并在多张图片之间复用，比为每个文件创建新对象更高效。

---

## 第二步 – 加载 PNG 图像 (read text from png)

引擎准备好后，你需要提供一张图像。**从 PNG 中读取文本** 的步骤相当直接，但有几个需要注意的地方：

1. **文件路径** – 确保路径是绝对路径或相对于可执行文件工作目录的相对路径。  
2. **资源释放** – `Image` 实现了 `IDisposable`；请使用 `using` 块包装以避免内存泄漏。

```csharp
string imagePath = @"YOUR_DIRECTORY\sample_russian.png";

using (Image russianImage = Image.FromFile(imagePath))
{
    // The image is now loaded and will be disposed automatically
}
```

> **小技巧：** 如果你使用流（例如上传的文件），请使用 `Image.FromStream(stream)` 而不是 `FromFile`。

---

## 第三步 – 选择西里尔语言包 (extract russian text)

Aspose 附带了许多语言包，但默认是英文。由于我们的目标是 **提取俄文文本**，必须显式告诉引擎使用西里尔模型。

```csharp
ocrEngine.Language = Language.Cyrillic;   // Switches the OCR engine to Cyrillic
```

> **为什么这至关重要：** 未设置 `Language.Cyrillic` 时，引擎会尝试将字形解释为拉丁字符，导致输出乱码。首次调用可能需要几秒钟下载语言数据——之后会本地缓存。

---

## 第四步 – 识别并将图像转换为文本 (convert image to text)

本教程的核心：将图片转换为纯文本字符串。`Recognize` 方法正是完成此操作的。

```csharp
using (Image russianImage = Image.FromFile(imagePath))
{
    // Perform OCR – this returns the detected text as a string
    string recognizedText = ocrEngine.Recognize(russianImage);

    // Show the result in the console
    Console.WriteLine("=== Recognized Russian Text ===");
    Console.WriteLine(recognizedText);
}
```

**预期的控制台输出**（实际文本会根据 PNG 内容而异）：

```
=== Recognized Russian Text ===
Привет, мир! Это пример текста на русском языке.
```

如果看到问号或随机符号，请再次确认图像分辨率足够高，并且已正确设置 `Language.Cyrillic`。

---

## 第五步 – 显示并验证识别结果 (recognize image text)

在真实应用中，你可能会将结果持久化到数据库、写入搜索索引，或传递给翻译 API。对于本教程来说，简单的 `Console.WriteLine` 已足以证明我们能够可靠地 **识别图像文本**。

```csharp
Console.WriteLine("\nDone! The OCR engine has extracted the Russian text.");
```

> **边缘情况：** 如果 PNG 中没有文本（或文本过于模糊），`Recognize` 会返回空字符串。务必做好相应检查：

```csharp
if (string.IsNullOrWhiteSpace(recognizedText))
{
    Console.WriteLine("No readable text found – try a clearer image or adjust DPI.");
}
```

---

## 完整工作示例

下面是完整的程序代码，可直接复制粘贴到新建的控制台项目（`dotnet new console`）中。它包含所有 using 语句、正确的资源释放以及少量错误处理。

```csharp
// ------------------------------------------------------------
// Full OCR example – extract Russian text from a PNG file
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine (downloads Cyrillic pack on first run)
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Path to the PNG that contains Russian text
        string imagePath = @"YOUR_DIRECTORY\sample_russian.png";

        // 3️⃣ Tell the engine to use Cyrillic (necessary for Russian)
        ocrEngine.Language = Language.Cyrillic;

        // 4️⃣ Load the image and run OCR
        using (Image russianImage = Image.FromFile(imagePath))
        {
            string recognizedText = ocrEngine.Recognize(russianImage);

            // 5️⃣ Output the result
            Console.WriteLine("=== Recognized Russian Text ===");
            Console.WriteLine(recognizedText);

            // Simple validation
            if (string.IsNullOrWhiteSpace(recognizedText))
            {
                Console.WriteLine("\n⚠️ No text detected – check image quality or language settings.");
            }
            else
            {
                Console.WriteLine("\n✅ OCR succeeded!");
            }
        }
    }
}
```

保存文件，运行 `dotnet run`，即可在控制台看到嵌入 PNG 中的俄语句子。 🎉

---

## 实用技巧与常见坑点

| 情况 | 处理办法 |
|-----------|------------|
| **图像分辨率低** | 在 OCR 前提升 DPI（`new Bitmap(image, new Size(width*2, height*2))`）。 |
| **文本旋转** | 使用 `ocrEngine.RotateImage` 或利用 `System.Drawing` 预处理去倾斜。 |
| **单张图像包含多语言** | 设置 `ocrEngine.Language = Language.Cyrillic | Language.English;` 以启用混合检测。 |
| **大量文件批处理** | 重复使用同一个 `OcrEngine` 实例；每次迭代只需释放 `Image` 对象。 |
| **在 Linux 上运行** | 确保已安装 `libgdiplus`（`apt-get install -y libgdiplus`），因为 `System.Drawing.Common` 依赖它。 |

---

## 可视化概览

![在 C# 中使用 OCR 的控制台输出，显示提取的俄文文本](ocr_console_output.png "在 C# 中使用 OCR – 示例输出")

*上图展示了程序运行结束后的控制台窗口，确认我们成功 **从 PNG 中读取文本** 并 **将图像转换为文本**。*

---

## 结论

我们已经完整演示了在 C# 中 **如何使用 OCR**：从初始化引擎、加载 PNG、切换到西里尔语言包、执行识别，到最终显示提取的俄语句子。这个简短的程序展示了完整的 **将图像转换为文本** 工作流，并说明了如何可靠地 **识别图像文本**。

接下来？  
- 尝试从多页 PDF 中提取文本（Aspose.OCR 也支持）。  
- 试验其他语言包（`Language.Arabic`、`Language.ChineseSimplified` 等）。  
- 将输出接入翻译服务或搜索索引，让你的应用真正实现多语言。

对噪声扫描的处理或在 Web API 中集成 OCR 有疑问吗？欢迎留言，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}