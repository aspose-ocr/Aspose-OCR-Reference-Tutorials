---
category: general
date: 2026-04-06
description: 如何在 C# 中使用 OCR 从 JPG 图像中提取纯文本，包括西里尔字符。学习加载图像进行 OCR，识别 JPG 文本并获得可靠的结果。
draft: false
keywords:
- how to use OCR
- extract plain text
- extract cyrillic text
- recognize text jpg
- load image for OCR
language: zh
og_description: 如何在 C# 中使用 OCR 从 JPG 文件中提取纯文本。本指南展示了如何加载用于 OCR 的图像、识别 JPG 文本以及处理西里尔文文本。
og_title: 如何在 C# 中使用 OCR – 从图像中提取纯文本
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 如何在 C# 中使用 OCR – 从图像中提取纯文本
url: /zh/net/text-recognition/how-to-use-ocr-in-c-extract-plain-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 从图像中提取纯文本

是否曾经想过 **如何使用 OCR** 在 .NET 项目中而不必与本地库斗争？也许你有一堆扫描的收据文件夹、一 handful of screenshots with Cyrillic captions，或者只是需要快速分析 JPEG 中的文字。好消息是 Aspose OCR 让整个过程变得轻而易举。

在本教程中，我们将演示一个完整、可运行的示例，展示 **如何使用 OCR** 来 **提取纯文本** 从 JPEG 图像，**加载图像进行 OCR**，以及在源语言不是拉丁文时 **提取西里尔文文本**。完成后，你将拥有一个小型控制台应用程序，直接在控制台打印识别出的文本——无需额外文件，也没有神秘的副作用。

> **你将获得**  
> * 一份可以直接复制粘贴到 Visual Studio 的分步指南。  
> * 对每行代码 **为何** 重要的解释，而不仅仅是 **做了什么**。  
> * 处理大图像、多语言以及常见陷阱的技巧。

## 前置条件

在开始之前，请确保你已经具备：

* .NET 6 SDK 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）。  
* Visual Studio 2022（或你喜欢的任何编辑器）。  
* 第一次运行示例时需要联网——Aspose OCR 会按需下载语言包。  

如果缺少 Aspose OCR NuGet 包，我们将在第一步中进行说明。

## 第一步 – 通过 NuGet 安装 Aspose OCR（以及它为何重要）

**加载图像进行 OCR** 的步骤必须在库存在的前提下才能进行。使用 NuGet 能确保你获得最新的、已修补安全漏洞的二进制文件，并自动拉取所有必需的依赖。

```bash
dotnet add package Aspose.OCR
```

*为何这很重要*：Aspose OCR 只随附一个体积极小的核心 DLL，语言数据只有在你请求时才会下载。这使得你的应用保持轻量，避免捆绑数兆字节的未使用语言文件。

## 第二步 – 初始化 OCR 引擎（**如何使用 OCR** 的核心）

创建 `OcrEngine` 实例是 **如何使用 OCR** 的第一行关键代码。引擎默认采用“按需”模式，这意味着第一次请求特定语言时会下载对应的语言包。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create the engine – it will fetch language data when needed.
var ocrEngine = new OcrEngine();
```

> **专业提示**：如果你在公司代理后面工作，请在第一次识别调用之前设置 `OcrEngine.Proxy`，以确保下载能够成功。

## 第三步 – 选择语言 – 需要时 **提取西里尔文文本**

Aspose OCR 支持数十种脚本。要 **提取西里尔文文本**，只需将 `Language` 属性设为 `OcrLanguage.Cyrillic`。第一次运行此行代码时，西里尔文模块（≈ 5 MB）会从 Aspose 的 CDN 拉取。

```csharp
// Step 3: Tell the engine which language to look for.
// This will automatically download the Cyrillic language pack on first use.
ocrEngine.Language = OcrLanguage.Cyrillic;
```

如果你的图像仅包含拉丁字符，可以将 `Cyrillic` 替换为 `English`。相同的模式适用于任何受支持的语言。

## 第四步 – **加载图像进行 OCR** – 来自磁盘或流

现在我们真正 **加载图像进行 OCR**。`System.Drawing.Image` 类能够处理大多数常见格式（JPG、PNG、BMP）。如果你在非 Windows 平台上，考虑使用 `ImageSharp`，但在本教程中内置类型已足够。

```csharp
using System.Drawing;

// Step 4: Load the picture that holds the text.
using var image = Image.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

> **为何这很重要**：在 `using` 块中加载图像可确保非托管的 GDI+ 资源及时释放，防止长时间运行的服务出现内存泄漏。

## 第五步 – **识别 JPG 文本** – 运行 OCR 过程

在引擎配置好且图像已加载后，我们终于 **识别 JPG 文本**。`Recognize` 方法返回一个 `OcrResult`，其中包含纯字符串、置信度分数，甚至在需要时的边界框信息。

```csharp
// Step 5: Perform the recognition.
var ocrResult = ocrEngine.Recognize(image);
```

如果想微调准确度，可以调整 `ocrEngine.Config`（例如启用 `AutoRotate` 或设置 `TextOrientation`）。对于大多数简单场景，默认设置已经相当出色。

## 第六步 – **提取纯文本** – 显示结果

**如何使用 OCR** 的最后一步是从 `ocrResult` 中取出识别后的字符串并进行处理。这里我们仅将其写入控制台，同时演示如何 **提取纯文本**。

```csharp
// Step 6: Output the plain text to the console.
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

### 预期输出

如果 `cyrillic_sample.jpg` 包含短语 “Привет мир”（Hello world），你应该看到：

```
=== Recognized Text ===
Привет мир
```

如果图像模糊或文字过小，输出可能会出现错误；你可以检查 `ocrResult.Confidence` 来决定是否使用更高分辨率的源图像重新尝试。

## 完整、可直接运行的示例

下面是完整程序。将其复制到新的控制台应用项目（`dotnet new console`）中并运行。除你指向的图像文件外，无需其他文件。

```csharp
// ---------------------------------------------------------------
// How to Use OCR in C# – Complete Example
// ---------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet first (dotnet add package Aspose.OCR)

        // 2️⃣ Initialize the OCR engine – on‑demand language download.
        var ocrEngine = new OcrEngine();

        // 3️⃣ Select Cyrillic to **extract Cyrillic text**.
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 4️⃣ **Load image for OCR** – change the path to your own file.
        using var image = Image.FromFile(@"YOUR_DIRECTORY\cyrillic_sample.jpg");

        // 5️⃣ **Recognize text jpg** – run the engine.
        var ocrResult = ocrEngine.Recognize(image);

        // 6️⃣ **Extract plain text** – display it.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **注意**：将 `YOUR_DIRECTORY\cyrillic_sample.jpg` 替换为实际的 JPEG 文件路径。

## 常见问题与边缘情况

### 如果我需要从流而不是文件 **识别 JPG 文本**，该怎么办？

可以直接传入 `MemoryStream`：

```csharp
using var ms = new MemoryStream(File.ReadAllBytes("myImage.jpg"));
using var img = Image.FromStream(ms);
var result = ocrEngine.Recognize(img);
```

### 如何处理同一图像中的多种语言？

将 `ocrEngine.Language` 设置为 `OcrLanguage.Multilingual`。引擎会自动检测每种脚本，非常适合收据中混合英文和西里尔文的情况。

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### 我的图像很大（超过 5 MP），引擎会卡吗？

大图像会增加内存占用并可能减慢识别速度。预先快速缩放可以帮助：

```csharp
var resized = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
var result = ocrEngine.Recognize(resized);
```

### 能否获取每行的置信度分数？

可以——`ocrResult.Lines` 包含每行的 `Confidence`。遍历这些行即可过滤低置信度的结果。

```csharp
foreach (var line in ocrResult.Lines)
{
    if (line.Confidence > 0.8)
        Console.WriteLine(line.Text);
}
```

## 生产级 OCR 的专业技巧

* **缓存语言包**——首次下载可能需要几秒钟；将文件存放在已知文件夹并设置 `ocrEngine.LanguageDataPath` 以复用。  
* **批量处理**——为多张图像复用同一个 `OcrEngine` 实例；为每个文件创建新引擎会产生不必要的开销。  
* **错误处理**——将 `Recognize` 调用包装在 try/catch 中。Aspose 会在图像损坏或不支持的格式时抛出 `OcrException`。  
* **日志记录**——记录 `ocrResult.Confidence`，以便后续审计哪些页面需要人工复核。

## 结论

我们已经介绍了 **如何在 C# 中使用 OCR** 来 **提取纯文本** 从 JPEG，演示了 **加载图像进行 OCR** 的步骤，展示了 **识别 JPG 文本** 的方法，并成功 **提取西里尔文文本**。该示例功能完整，仅需一个 NuGet 包，即可扩展以处理多语言文档、批量作业或实时扫描场景。

准备好迎接下一个挑战了吗？尝试将西里尔语言换成阿拉伯语，实验 `AutoRotate` 标志，或将输出集成到搜索索引中。可能性无限。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}