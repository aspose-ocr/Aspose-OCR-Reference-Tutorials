---
category: general
date: 2026-05-25
description: 如何在 C# 中使用 OCR 从图像文件中提取文本。学习使用 Aspose.OCR 通过几个简单步骤识别 JPG 中的中文字符。
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from jpg
- recognize chinese characters
- ocr chinese simplified
language: zh
og_description: 如何在 C# 中使用 OCR 从图像文件中提取文本。本指南展示了如何使用 Aspose.OCR 从 JPG 中识别中文字符。
og_title: 如何在 C# 中使用 OCR – 从 JPG 识别中文文本
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  headline: How to Use OCR in C# – Recognize Chinese Text from JPG
  type: TechArticle
- description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  name: How to Use OCR in C# – Recognize Chinese Text from JPG
  steps:
  - name: What’s happening under the hood?
    text: '- **`OcrEngine.Language`** tells Aspose which dictionary to use. By picking
      `ChineseSimplified`, we instruct the engine to look for the Simplified Chinese
      language pack. - **First‑time download**: When `Recognize` runs, the SDK reaches
      out to Aspose’s CDN, pulls the ≈6 MB language file, caches it lo'
  - name: 5.1 Dealing with Low‑Quality Images
    text: 'OCR accuracy drops when the source image is blurry, noisy, or has poor
      lighting. A quick fix is to pre‑process the image:'
  - name: 5.2 Running in a Headless Environment
    text: 'If you’re deploying to a Linux container without a GUI, make sure the `libgdiplus`
      library (required for `System.Drawing`) is installed:'
  - name: 5.3 Caching the Language Pack Manually
    text: You can download the language file once and point Aspose to it via the `License`
      API, which eliminates the one‑time network call. This is handy for offline scenarios.
  - name: Expected Output
    text: 'If the JPG contains the phrase “欢迎光临”, the console will print:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中使用 OCR – 从 JPG 识别中文文本
url: /zh/net/text-recognition/how-to-use-ocr-in-c-recognize-chinese-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 从 JPG 识别中文文本

有没有想过 **如何使用 OCR** 从手机拍摄的图片中提取文字？你并不孤单。在许多实际项目中——比如收据扫描器、翻译应用或自动数据录入——你需要快速且可靠地 **从图像中提取文本**。

在本教程中，我们将演示一个完整且可运行的示例，能够 **从 JPG 文件中识别文本**，甚至能够处理使用 **OCR Chinese Simplified** 语言包的 **识别中文字符** 的棘手情况。完成后，你将拥有一个独立的控制台应用程序，它会将检测到的字符串打印到控制台，无需额外手动下载。

> **快速提示：** 该代码适用于 Aspose.OCR ≥ 23.7，它会在首次使用时自动获取语言资源。如果你使用的是较旧的版本，则需要手动添加语言。

## 前置条件

- .NET 6.0 SDK 或更高版本（示例针对 .NET 6，但 .NET 5 也可使用）
- 最近版本的 Visual Studio 2022 或带有 C# 扩展的 VS Code
- 首次语言下载所需的互联网连接
- 包含简体中文文本的 JPG 图像（我们将其命名为 `chinese_sign.jpg`）

就是这样——无需笨重的 OCR 引擎，也不需要处理本机 DLL。只需几条 NuGet 命令和几行代码。

## 步骤 1：通过 NuGet 安装 Aspose.OCR

首先：我们需要 OCR 库。在项目文件夹中打开终端并运行：

```bash
dotnet add package Aspose.OCR
```

或者，如果你更喜欢 Visual Studio UI，右键点击 **Dependencies → Manage NuGet Packages**，搜索 “Aspose.OCR”，然后点击 **Install**。

**专业提示：** 保持你的包为最新版本。每个小版本都会加入新的语言包和性能改进。

## 步骤 2：创建新的控制台项目（如果尚未创建）

如果你从头开始，创建一个全新的控制台应用程序：

```bash
dotnet new console -n OcrChineseDemo
cd OcrChineseDemo
```

现在你已经拥有一个准备好放置 OCR 代码的 `Program.cs` 文件。

## 步骤 3：编写 OCR 代码 – 从 JPG 识别简体中文

打开 `Program.cs` 并将其内容替换为以下代码。每行都带有注释，帮助你了解我们 *为什么* 要这么做，而不仅仅是 *做了什么*。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;   // Required for Image.FromFile

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // --------------------------------------------------------------
            // 1️⃣  Initialise the OCR engine and request the Simplified Chinese
            //     language. This language isn’t bundled in the core package,
            //     so Aspose.OCR will download it the first time you call
            //     Recognize().
            // --------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                // The enum value maps to the language pack name.
                Language = OcrLanguage.ChineseSimplified
            };

            // --------------------------------------------------------------
            // 2️⃣  Load the image you want to process. Replace the path with
            //     the actual location of your JPG file.
            // --------------------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";
            using var image = Image.FromFile(imagePath);

            // --------------------------------------------------------------
            // 3️⃣  Perform the recognition. The first call may take a few
            //     seconds because the language resources are being fetched.
            // --------------------------------------------------------------
            string recognizedText = ocrEngine.Recognize(image);

            // --------------------------------------------------------------
            // 4️⃣  Output the result to the console.
            // --------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### 背后发生了什么？

- **`OcrEngine.Language`** 告诉 Aspose 使用哪个词典。通过选择 `ChineseSimplified`，我们指示引擎使用简体中文语言包。
- **首次下载**：当调用 `Recognize` 时，SDK 会访问 Aspose 的 CDN，下载约 6 MB 的语言文件并在本地缓存，然后继续进行 OCR。后续调用则是瞬时完成。
- **`Image.FromFile`** 支持 .NET 能解码的任何栅格格式——JPG、PNG、BMP——因此你可以 **从图像中提取文本**，不仅限于 JPG。

## 步骤 4：运行应用并验证输出

构建并运行：

```bash
dotnet run
```

你应该会看到类似如下的输出：

```
=== Recognized Text ===
欢迎光临
```

如果控制台打印出乱码或空字符串，请仔细检查以下事项：

1. 图像确实包含清晰、高对比度的中文字符。
2. 文件路径正确（没有多余的空格或缺少扩展名）。
3. 你的机器能够访问 `https://download.aspose.com` 以获取语言包。

## 步骤 5：处理边缘情况和常见陷阱

### 5.1 处理低质量图像

当源图像模糊、噪声大或光照不足时，OCR 的准确率会下降。一个快速的解决方案是对图像进行预处理：

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
var gray = new Bitmap(image.Width, image.Height);
using (var g = Graphics.FromImage(gray))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}
        });
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(image, new Rectangle(0,0,image.Width,image.Height),
                0,0,image.Width,image.Height, GraphicsUnit.Pixel, attributes);
}

// Use the processed bitmap for OCR
string recognizedText = ocrEngine.Recognize(gray);
```

### 5.2 在无头环境中运行

如果你将应用部署到没有 GUI 的 Linux 容器，请确保已安装 `libgdiplus` 库（`System.Drawing` 所需）：

```bash
apt-get update && apt-get install -y libgdiplus
```

### 5.3 手动缓存语言包

你可以一次性下载语言文件，并通过 `License` API 将其指向 Aspose，这样就消除了首次网络请求。对于离线场景非常实用。

```csharp
// Assuming you have the .dat file downloaded to /opt/ocr/langs/
ocrEngine.SetLicense("Aspose.OCR.lic"); // optional if you have a paid license
ocrEngine.LoadLanguage(@" /opt/ocr/langs/ChineseSimplified.dat");
```

## 完整工作示例（全功能）

下面是可以直接复制粘贴到 `Program.cs` 的 *完整* 程序。没有隐藏代码，也没有外部脚本。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialise OCR engine with Simplified Chinese language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified
            };

            // Path to the JPG image containing Chinese text
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";

            // Load the image (ensure the file exists)
            using var image = Image.FromFile(imagePath);

            // Recognize text – first call may download the language pack
            string recognizedText = ocrEngine.Recognize(image);

            // Display the result
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### 预期输出

如果 JPG 包含短语 “欢迎光临”，控制台将输出：

```
=== Recognized Text ===
欢迎光临
```

随意将图像替换为其他简体中文标志、街道名称或产品标签——引擎会尽力识别。

## 结论

我们刚刚介绍了在 C# 中 **如何使用 OCR** 来 **从图像中提取文本**，特别是解决在 **JPG** 中 **识别中文字符** 的挑战。通过利用 Aspose.OCR 的即时语言下载，你可以保持部署轻量化，同时开箱即支持 **OCR Chinese Simplified**。

接下来可以尝试以下想法：

- **批量处理**：遍历文件夹中的图像并将每个结果写入 CSV。
- **结合翻译 API**：将识别的字符串输入 Azure Translator，实现实时多语言应用。
- **探索其他语言**：将 `OcrLanguage.ChineseSimplified` 替换为 `Japanese` 或 `Arabic`，观察相同代码的适配情况。

对性能调优、授权或将 OCR 集成到 Web 服务有疑问？在下方留言——祝编码愉快！ 

---

![显示如何在 C# 中使用 OCR 从 JPG 图像识别中文文本的控制台输出截图](ocr-chinese-demo.png "如何使用 OCR 控制台输出")

## 相关教程

- [使用 Aspose.OCR 进行语言选择的 C# 图像文本提取](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [使用 Aspose OCR 识别多语言图像文本](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [通过准备矩形在 OCR 中提取图像文本的方法](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}