---
category: general
date: 2026-03-21
description: c# OCR 教程：学习如何使用 C# 中的 OCR 从 PNG 图像中提取乌尔都语文本。包括逐步代码、语言设置和实用技巧。
draft: false
keywords:
- c# ocr tutorial
- extract urdu text
- recognize text image
- how to extract urdu
- ocr from png file
language: zh
og_description: c# OCR 教程：学习如何使用 C# 中的 OCR 从 PNG 图像中提取乌尔都语文本。完整指南，附代码和技巧。
og_title: C# OCR 教程 – 从 PNG 图像中提取乌尔都文文本
tags:
- OCR
- C#
- Urdu
- Image Processing
title: C# OCR 教程 – 从 PNG 图像中提取乌尔都文文本
url: /zh/net/text-recognition/c-ocr-tutorial-extract-urdu-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr 教程 – 从 PNG 图像中提取乌尔都语文本

是否曾经需要一个 **c# ocr 教程** 能够真正从 PNG 文件中提取乌尔都语文本？你并不孤单。在许多项目中——发票处理、文档归档，甚至是快速翻译工具——你都会遇到必须识别图像中的文字，而语言又至关重要的情况。

在本指南中，我们将逐步演示一个完整、可直接运行的解决方案，使用 OCR 引擎从 PNG 中提取乌尔都语文本。你将了解每行代码的作用，如何处理缺失的语言包，以及当图像不完美时该怎么办。阅读完本教程后，你将有信心将代码适配到其他语言或文件类型。

## 你将学到

- 如何设置 C# OCR 库（没有隐藏的魔法）  
- **从 PNG 文件中提取 urdu text** 的完整步骤  
- 为什么将语言配置为乌尔都语很重要，以及引擎如何自动下载缺失的数据  
- 验证输出并排查常见问题的方法  

不需要外部文档链接——所有内容都在这里。

## 前置条件（开始之前需要准备的）

| 要求 | 为什么重要 |
|------|------------|
| .NET 6.0+（或 .NET Core 3.1） | 现代 API 与 async 支持 |
| Visual Studio 2022（或带 C# 扩展的 VS Code） | 带 IntelliSense 的 IDE 能让代码更清晰 |
| 提供 `OcrEngine` 的 OCR 库（例如 **Microsoft.Windows.SDK.Contracts** 或第三方 NuGet 包） | 提供 `Language.Urdu` 和 `Recognize` 方法 |
| 包含乌尔都语文本的 PNG 图像（例如 `urdu_invoice.png`） | **recognize text image** 操作的源文件 |

如果你还没有 OCR 包，请在 Package Manager Console 中运行以下单行命令：

```powershell
Install-Package Microsoft.Windows.SDK.Contracts
```

这将引入我们后面要使用的 `OcrEngine` 类。

> **小贴士：** SDK 会在首次使用时自动下载语言数据，无需手动下载乌尔都语语言包。

## 步骤 1：安装并引用 OCR 库

在创建引擎之前，项目必须引用 OCR 包。在文件顶部添加以下 `using` 指令：

```csharp
using System;
using Windows.Media.Ocr;          // Core OCR classes
using Windows.Graphics.Imaging;   // For loading PNG files
using Windows.Storage;            // File handling helpers
```

这些命名空间让我们能够访问 `OcrEngine`、`Language` 和图像加载工具。如果你使用的是其他库，请寻找相应的命名空间。

## 步骤 2：创建 OCR 引擎实例  

现在我们真正启动引擎。可以把引擎想象成将像素模式解释为字符的大脑。

```csharp
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));
if (ocrEngine == null)
{
    Console.WriteLine("Failed to create OCR engine for Urdu. Check your language pack.");
    return;
}
```

**原因说明：** `TryCreateFromLanguage` 在语言数据不存在时返回 `null`，这让我们能够在后期崩溃之前快速失败。

## 步骤 3：加载 PNG 图像  

OCR 引擎使用 `SoftwareBitmap` 对象，而不是原始文件路径。下面的辅助方法从磁盘加载 PNG 并转换为所需格式。

```csharp
// Step 3: Load the PNG image into a SoftwareBitmap
async Task<SoftwareBitmap> LoadImageAsync(string path)
{
    StorageFile file = await StorageFile.GetFileFromPathAsync(path);
    using var stream = await file.OpenReadAsync();
    var decoder = await BitmapDecoder.CreateAsync(stream);
    // Convert to Gray8 for best OCR accuracy
    return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
}
```

**边缘情况：** 如果 PNG 为彩色图像，转换为灰度 (`Gray8`) 往往能提升识别率，尤其是对乌尔都语这种带有细微变音符号的文字。

## 步骤 4：从图像中识别文本  

这就是 **c# ocr 教程** 的核心——让引擎读取图像。

```csharp
// Step 4: Perform OCR on the loaded bitmap
async Task<string> RecognizeUrduAsync(string imagePath)
{
    SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
    OcrResult result = await ocrEngine.RecognizeAsync(bitmap);
    return result.Text;
}
```

`OcrResult.Text` 属性包含原始的 Unicode 字符串。因为我们之前已经将语言设置为乌尔都语，引擎会应用正确的脚本规则。

## 步骤 5：输出并验证提取的文本  

最后，我们将结果打印到控制台。在真实应用中，你可能会将其存入数据库或传递给翻译服务。

```csharp
// Step 5: Run the OCR and display the result
static async Task Main(string[] args)
{
    string imageFile = @"C:\Images\urdu_invoice.png"; // adjust path as needed
    string extracted = await RecognizeUrduAsync(imageFile);
    Console.WriteLine("=== Extracted Urdu Text ===");
    Console.WriteLine(extracted);
}
```

**预期结果：** 如果图像清晰，你会看到类似下面的输出：

```
=== Extracted Urdu Text ===
بل نمبر: 12345
تاریخ: 21/03/2026
کل رقم: 5,000 روپے
```

如果输出出现乱码，请检查图像质量（对比度、噪声），并考虑进行预处理（例如二值化）。

## 如何从 PNG 文件中提取乌尔都语文本 – 常见陷阱  

1. **对比度低** – 前景与背景颜色相近时 OCR 会表现不佳。使用图像编辑工具在运行代码前提升对比度。  
2. **DPI 不正确** – 以 300 dpi 或更高的分辨率扫描，可为引擎提供更多细节。  
3. **缺少语言包** – 第一次调用 `TryCreateFromLanguage` 可能会触发下载；确保机器能够联网。  

解决这些问题可以显著提升 **recognize text image** 的成功率。

## Recognize Text Image：扩展到其他格式  

虽然本教程聚焦于 PNG，但相同的工作流同样适用于 JPEG、BMP 或 TIFF——只需更改文件扩展名并确保解码器支持即可。关键代码仍然是 `await ocrEngine.RecognizeAsync(bitmap);`。

## PNG 文件 OCR 小技巧 – 性能与扩展  

- **批量处理：** 将多个图像加载到列表中，使用 `Task.WhenAll` 并行识别。  
- **缓存引擎：** 创建单个 `OcrEngine` 实例并在多次调用中复用；频繁构造会增加开销。  
- **内存管理：** 使用完 `SoftwareBitmap` 后调用 `bitmap.Dispose()`，保持进程轻量。

## 完整可运行示例（复制‑粘贴即用）

下面是可以直接编译运行的完整程序示例，包含所有 using 语句、async 处理以及错误检查。

```csharp
// Full C# OCR tutorial – Extract Urdu text from a PNG file
using System;
using System.Threading.Tasks;
using Windows.Media.Ocr;
using Windows.Graphics.Imaging;
using Windows.Storage;

class Program
{
    // Initialize the OCR engine for Urdu
    private static OcrEngine _ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));

    static async Task Main(string[] args)
    {
        if (_ocrEngine == null)
        {
            Console.WriteLine("Urdu language pack not available. Ensure internet connectivity for automatic download.");
            return;
        }

        string imagePath = @"C:\Images\urdu_invoice.png"; // <-- change to your image location
        string text = await RecognizeUrduAsync(imagePath);
        Console.WriteLine("=== Extracted Urdu Text ===");
        Console.WriteLine(text);
    }

    // Load PNG and convert to grayscale bitmap
    private static async Task<SoftwareBitmap> LoadImageAsync(string path)
    {
        StorageFile file = await StorageFile.GetFileFromPathAsync(path);
        using var stream = await file.OpenReadAsync();
        var decoder = await BitmapDecoder.CreateAsync(stream);
        return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
    }

    // Perform OCR and return the recognized text
    private static async Task<string> RecognizeUrduAsync(string imagePath)
    {
        SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
        OcrResult result = await _ocrEngine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

**预期输出：** 控制台会打印图像中找到的乌尔都语字符，保持从右到左的顺序。

## 结论  

你刚刚完成了一个 **c# ocr 教程**，演示了如何 **extract urdu text** 从 PNG 中提取、配置语言并安全处理结果。安装库、创建引擎、加载图像、识别文本、输出结果这几个步骤构成了一个可复用的模式，适用于任何脚本或文件类型。

接下来，可以尝试在多页 PDF（先将每页转换为 PNG）上进行 **recognize text image**，或集成翻译 API 将提取的乌尔都语自动翻译成英文。掌握了这套核心工作流后，想象空间无限。

祝编码愉快，愿你的 OCR 结果清晰如晶！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}