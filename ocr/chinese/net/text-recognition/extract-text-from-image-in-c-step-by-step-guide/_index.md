---
category: general
date: 2026-05-06
description: 使用 Aspose OCR 在 C# 中从图像提取文本。了解如何将 JPG 转换为文本，设置 OCR 语言，并高效读取 JPG 中的文本。
draft: false
keywords:
- extract text from image
- convert jpg to text
- image to text c#
- read text from jpg
- set OCR language
language: zh
og_description: 使用 Aspose OCR 在 C# 中提取图像文本。本指南展示了如何将 JPG 转换为文本、设置 OCR 语言以及读取 JPG 中的文本。
og_title: 在 C# 中从图像提取文本 – 完整教程
tags:
- OCR
- C#
- Aspose
title: 在 C# 中从图像提取文本 – 步骤指南
url: /zh/net/text-recognition/extract-text-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本（C#）– 完整编程演练

是否曾经需要**从图像中提取文本**却不确定该选哪个库？你并不孤单——开发者们经常会问：“如何在不将数据发送到云端的情况下将 JPG 转换为文本？”好消息是，Aspose OCR 为你提供了一个完全离线的解决方案，直接在你的 .NET 应用中运行。

在本教程中，我们将一步步演示你需要了解的所有内容：从安装 Aspose OCR NuGet 包、**设置 OCR 语言**（以俄文为例），到**从 JPG 读取文本**。结束后，你将拥有一段可复用的代码片段，直接粘贴到任意 C# 项目中，即可即时从图像中提取文本。

> **你将收获**  
> • 一个清晰、可运行的示例，**从图像文件中提取文本**。  
> • 使用 Aspose OCR 引擎**将 JPG 转换为文本**的完整流程。  
> • 配置**设置 OCR 语言**以支持多语言场景的技巧。  
> • 对不可读图像和缺失语言包的边缘情况处理方案。

## 前置条件

在开始之前，请确保你具备以下条件：

| 前置条件 | 为什么重要 |
|-------------|----------------|
| .NET 6.0 或更高版本（任意近期 .NET 运行时） | Aspose OCR 目标为 .NET Standard 2.0+，更新的运行时可提供最佳性能。 |
| Visual Studio 2022（或带 C# 扩展的 VS Code） | 友好的 IDE 能帮助你快速调试 OCR 流程。 |
| **一次** 网络连接用于下载 Aspose OCR NuGet 包 | 首次安装后可启用**离线资源**，后续无需再下载。 |
| 包含俄文文本的示例 JPG 图像（`input.jpg`），或你计划使用的任意语言图像 | 本教程使用俄文示例，你可以替换为已安装语言包对应的任意语言。 |

如果上述内容对你来说陌生，请不要慌张。安装 NuGet 包只需一条命令，其余步骤对所有 Aspose 支持的图像格式均适用。

## 解决方案概览

从宏观上看，整个流程如下：

1. **创建** 一个带离线资源的 `OcrEngine`，防止库在运行时下载语言数据。  
2. **设置** 所需语言（例如 Russian），使用 `OcrLanguage` 枚举。  
3. **调用** `RecognizeImage` 对本地 JPG 文件进行识别。  
4. **打印** 提取的字符串到控制台，或将其传递给你的业务流程。

下面是一张快速示意图，展示数据流向：

![从图像中提取文本（使用 Aspose OCR 在 C# 中）](https://example.com/placeholder-image.png){.align-center alt="从图像中提取文本（使用 Aspose OCR 在 C# 中）"}

*该示意图仅用于说明，实际工作由代码完成。*

## 从图像中提取文本 – 核心概念

在编写代码之前，先了解几个常让开发者卡壳的概念：

- **OfflineResources** – 当设为 `true` 时，Aspose OCR 会查找你预先下载好的语言包，避免在生产环境启动时出现“自动下载”导致的延迟。  
- **OcrLanguage** – 该枚举包含数十种语言标识（`English`、`Russian`、`Japanese` …），正确选择可显著提升识别准确率，因为引擎会应用对应语言的启发式算法。  
- **图像质量** – OCR 在高对比、无噪声的图像上表现最佳。如果得到乱码结果，考虑在送入引擎前进行二值化等预处理。

掌握这些要点后，你就能判断何时需要**手动设置 OCR 语言**，以及为何**将 JPG 转换为文本**并非一行代码即可完成。

## 第一步：安装 Aspose OCR NuGet 包

在项目文件夹的终端中运行：

```bash
dotnet add package Aspose.OCR
```

*小技巧：* 第一次安装后，添加 `-v latest` 参数可确保始终获取最新的稳定版本。该包大小约为 15 MB，适合大多数桌面或服务器部署。

## 第二步：Convert JPG to Text – 初始化引擎

库已就位后，创建一个离线工作的 `OcrEngine`。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine with offline resources.
        // This prevents the SDK from trying to download language data at runtime.
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            OfflineResources = true   // <-- crucial for production stability
        });

        // Step 2.2: Choose the language pack you need.
        // Here we use Russian; replace with OcrLanguage.English for English text.
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 2.3: Perform OCR on a local JPG file.
        // The file path can be absolute or relative to the executable.
        var result = ocrEngine.RecognizeImage("YOUR_DIRECTORY/input.jpg");

        // Step 2.4: Output the extracted text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(result.Text);
    }
}
```

### 为什么这样做很重要

- **离线模式**保证启动时间可预测——部署到受限服务器时不会出现意外的网络请求。  
- **设置语言**（`OcrLanguage.Russian`）让引擎使用俄文字形，干净图像的识别准确率可从约 70 % 提升至 >95 %。  
- 方法 `RecognizeImage` 接受 Aspose 支持的任意图像格式（`.jpg`、`.png`、`.tiff` …），因此我们可以**直接从 JPG 读取文本**，无需额外转换。

## 第三步：Set OCR Language – 处理多语言

有时需要处理包含多种语言的文档（例如俄文和英文混排）。Aspose OCR 允许你指定*回退*语言数组：

```csharp
// Example: Russian primary, English secondary
ocrEngine.Language = OcrLanguage.Russian;
ocrEngine.AdditionalLanguages = new[] { OcrLanguage.English };
```

当主语言无法识别某个字符时，引擎会自动检查额外的语言列表。这在发票等混合西里尔字母和英文产品代码的场景中特别有用。

> **注意：** 语言包必须放在项目的 `Resources` 文件夹中。如果出现 `FileNotFoundException`，请从 Aspose 门户下载缺失的语言包并放置在可执行文件旁。

## 第四步：Read Text from JPG – 常见陷阱与解决方案

即使语言包正确，也可能遇到以下问题：

| 问题 | 常见表现 | 快速解决方案 |
|-------|-----------------|-----------|
| 对比度低 | 输出乱码或为空 | 使用 `System.Drawing` 在 OCR 前应用简单的对比度拉伸滤镜。 |
| 图像旋转 | 文本横向显示 | 在调用 `RecognizeImage` 前设置 `ocrEngine.ImageRotation = OcrRotation.Rotate90;`（或 180/270）。 |
| 文件过大 | 识别慢、内存占用高 | 将最长边限制在 2000 px 以内；OCR 质量仍然保持良好。 |

下面提供一个紧凑的帮助方法，用于在送入引擎前对图像进行缩放和增强：

```csharp
using System.Drawing;
using System.Drawing.Imaging;

static string PreprocessAndRead(string jpgPath)
{
    // Load the original image
    using var original = new Bitmap(jpgPath);

    // Resize while preserving aspect ratio (max 2000px)
    int maxDim = 2000;
    int newWidth, newHeight;
    if (original.Width > original.Height)
    {
        newWidth = maxDim;
        newHeight = original.Height * maxDim / original.Width;
    }
    else
    {
        newHeight = maxDim;
        newWidth = original.Width * maxDim / original.Height;
    }

    using var resized = new Bitmap(original, new Size(newWidth, newHeight));

    // Optional: increase contrast (simple linear stretch)
    var contrast = new ImageAttributes();
    float[][] matrix = {
        new float[] {1.2f, 0, 0, 0, 0},
        new float[] {0, 1.2f, 0, 0, 0},
        new float[] {0, 0, 1.2f, 0, 0},
        new float[] {0, 0, 0, 1, 0},
        new float[] {0, 0, 0, 0, 1}
    };
    contrast.SetColorMatrix(new ColorMatrix(matrix));

    using var graphics = Graphics.FromImage(resized);
    graphics.DrawImage(resized, new Rectangle(0, 0, newWidth, newHeight), 0, 0, newWidth, newHeight, GraphicsUnit.Pixel, contrast);

    // Save to a temporary file (Aspose OCR works with file paths)
    string tempPath = Path.GetTempFileName() + ".jpg";
    resized.Save(tempPath, ImageFormat.Jpeg);

    // Run OCR
    var engine = new OcrEngine(new OcrEngineSettings { OfflineResources = true });
    engine.Language = OcrLanguage.Russian;
    var res = engine.RecognizeImage(tempPath);
    File.Delete(tempPath); // clean up
    return res.Text;
}
```

现在可以调用 `Console.WriteLine(PreprocessAndRead("YOUR_DIRECTORY/input.jpg"));`，获得更清晰的识别结果。

## 完整工作示例 – 一文件实现全部步骤

以下是可直接复制到 `Program.cs` 的*完整*程序示例，包含安装说明、语言配置、预处理以及错误处理。

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        string imagePath = "YOUR_DIRECTORY/input.jpg";

        try
        {

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}