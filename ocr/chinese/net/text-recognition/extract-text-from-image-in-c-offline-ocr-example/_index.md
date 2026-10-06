---
category: general
date: 2026-02-09
description: 使用 C# 离线 OCR 从图像中提取文本。完整的 C# OCR 示例展示了如何加载用于 OCR 的图像、识别西里尔文文本以及从护照中提取文本。
draft: false
keywords:
- extract text from image
- c# ocr example
- load image for ocr
- recognize cyrillic text
- recognize text from passport
language: zh
og_description: 使用 C# 离线 OCR 从图像中提取文本。学习一步一步的 C# OCR 示例，加载图像进行 OCR，识别西里尔文文本并从护照中提取文本。
og_title: 在 C# 中从图像提取文本 – 离线 OCR 指南
tags:
- OCR
- C#
- Aspose
title: 在 C# 中从图像提取文本 – 离线 OCR 示例
url: /zh/net/text-recognition/extract-text-from-image-in-c-offline-ocr-example/
---


{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中从图像提取文本 – 离线 OCR 示例

是否曾需要 **从图像中提取文本**，却被依赖网络的 API 卡住？你并不孤单。许多开发者在 OCR 服务尝试在运行时下载语言包时会遇到障碍，尤其是在受限环境中。

在本指南中，我们将演示一个 **c# ocr example**，它完全离线运行，加载图像进行 OCR，并识别护照中的西里尔文文本。完成后，你将拥有一个可直接运行的程序，能够将任意受支持图像的纯文本内容直接打印到控制台。

## 你将学到的内容

- 如何为离线处理设置 Aspose.OCR。  
- 从磁盘 **load image for OCR** 的完整代码。  
- 如何配置引擎以 **recognize cyrillic text**。  
- 一个完整的、可直接复制粘贴的 **c# ocr example**，用于从护照风格的照片中提取文本。  

不需要任何 Aspose 经验；只要有 .NET 6（或更高）SDK 和 Visual Studio 2022（或 VS Code）即可。

---

![Extract text from image using Aspose OCR on a passport photo](/images/ocr-passport.jpg "extract text from image")

## 步骤 1：设置项目以从图像提取文本

在编写任何代码之前，确保已将 Aspose.OCR NuGet 包添加到项目中：

```bash
dotnet add package Aspose.OCR
```

> **专业提示：** 使用 `--version` 标志锁定到最新的稳定版本（例如 `13.9.0`），这可以保证与 .NET 6 的兼容性。

创建一个新的控制台应用非常简单：

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
```

现在你拥有一个干净的起点，接下来我们将在 **extract text from image** 时完全不触碰网络。

## 步骤 2：加载用于 OCR 的图像 – 读取护照照片

OCR 引擎首先需要一个表示图片的位图或流。在本例中，我们将 **load image for OCR** 从本地文件 `cyrillic_passport.jpg` 中读取。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 2: Load the image file (this is the “load image for ocr” part)
var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

// Validate the file exists – helpful when the path is wrong.
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// ImageStream abstracts the underlying format; it works with JPEG, PNG, etc.
var image = ImageStream.FromFile(imagePath);
```

> **为何重要：** 提供流而不是原始 `Bitmap`，可以让 Aspose 在内部处理格式检测，减少样板代码和潜在错误。

## 步骤 3：配置离线模式并选择西里尔文语言

Aspose.OCR 可以在运行时下载语言模型，但这违背了离线解决方案的初衷。关闭网络调用，并显式告知引擎使用哪种语言。

```csharp
// Step 3: Create the OCR engine and switch to offline mode
var ocrEngine = new OcrEngine
{
    Configuration =
    {
        OfflineMode = true,               // No network traffic – perfect for secure environments
        Language = new[] { OcrLanguage.Cyrillic } // We want to **recognize cyrillic text**
    }
};
```

> **边缘情况：** 如果以后需要在同一文档中识别拉丁字符，只需在数组中添加 `OcrLanguage.English`。引擎会自动处理多语言检测。

## 步骤 4：运行 OCR 引擎并识别西里尔文文本

现在我们真正 **recognize text from passport**‑style 图像。`Recognize` 方法返回一个丰富的结果对象，包含纯文本、置信度分数和边界框信息。

```csharp
// Step 4: Perform the OCR operation
OcrResult result = ocrEngine.Recognize(image);

// Step 5: Output the plain text – this is where we finally **extract text from image**
Console.WriteLine("📝 Extracted Text:");
Console.WriteLine("-------------------");
Console.WriteLine(result.PlainText);
```

### 预期的控制台输出

```
📝 Extracted Text:
-------------------
ПАСПОРТ РФ
Иванов Иван Иванович
01.01.1990
...
```

如果结果出现乱码，请再次确认源图像清晰，并且 Aspose 安装文件夹（通常是 `\Aspose.OCR\resources\languages`）中已存在西里尔文的 `OfflineMode` 语言包。

## 完整 C# OCR 示例 – 完整源代码

下面是完整的 **c# ocr example**。将其复制粘贴到 `Program.cs` 中并运行 `dotnet run`。所有用于 **extract text from image** 的代码都在这里。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class OfflineExample
{
    static void Main()
    {
        // --------------------------------------------------------------
        // Step 1: Create the OCR engine (offline mode)
        // --------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Configuration =
            {
                OfflineMode = true,                     // No network calls
                Language = new[] { OcrLanguage.Cyrillic } // Recognize Cyrillic text
            }
        };

        // --------------------------------------------------------------
        // Step 2: Load the image for OCR (passport photo)
        // --------------------------------------------------------------
        var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ Image not found at {imagePath}");
            return;
        }

        var image = ImageStream.FromFile(imagePath);

        // --------------------------------------------------------------
        // Step 3: Recognize the text
        // --------------------------------------------------------------
        var result = ocrEngine.Recognize(image);

        // --------------------------------------------------------------
        // Step 4: Output the plain text (the final extraction)
        // --------------------------------------------------------------
        Console.WriteLine("📝 Extracted Text:");
        Console.WriteLine("-------------------");
        Console.WriteLine(result.PlainText);
    }
}
```

### 运行示例

```bash
dotnet run
```

你应该会在控制台看到护照信息以西里尔文形式打印出来。这就是你的 **extract text from image** 流程成功运行的标志。

## 常见陷阱及解决方案

| 症状 | 可能原因 | 解决办法 |
|---------|--------------|-----|
| `PlainText` 为空 | 语言模型错误或图像过暗 | 确保 `OfflineMode` 包含 `Cyrillic`，并提升图像对比度 |
| `System.DllNotFoundException` | 缺少 Aspose OCR 本地二进制文件 | 重新安装 NuGet 包或将 `Aspose.OCR.Native.dll` 复制到输出文件夹 |
| 大图像性能慢 | 引擎处理完整分辨率 | 在传入 `ImageStream` 前将图像缩小至宽度 ≤ 1500 px |
| 字符乱码 | 图像旋转不正确 | 在创建流之前使用 `Image.RotateFlip(RotateFlipType.Rotate90FlipNone)` 进行旋转 |

## 后续步骤 – 扩展离线 OCR 工作流

- 在 ASP.NET Core 中处理上传文件时，使用 **load image for OCR** 从 `MemoryStream` 加载。  
- 通过遍历护照扫描文件夹，实现 **recognize text from passport** 的批量模式。  
- 将结果与 **regular expressions** 结合，提取护照号码、出生日期等字段。  
- 试验 `ocrEngine.Configuration.UseParallelProcessing = true` 以利用多核加速。

---

### 结论

我们已经展示了如何使用完全离线的 C# OCR 流程 **extract text from image**。这个简短、独立的 **c# ocr example** 加载图像、配置引擎以 **recognize cyrillic text**，并将提取的护照数据打印出来——整个过程不需要任何网络请求。

欢迎随意修改代码，添加更多语言，或将输出接入数据库。一旦掌握了加载图像进行 OCR 和识别护照风格照片中文本的基础，可能性就无限了。

有问题或想分享自己的改动吗？在下方留言吧，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}