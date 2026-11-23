---
category: general
date: 2026-08-22
description: 学习使用 Aspose.OCR 识别图像中的文本。本指南还涵盖 OCR 将图像转换为文本，并在几个步骤中从 JPG 提取文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- ocr image to text
- extract text from jpg
- convert image to text
- read cyrillic text image
language: zh
lastmod: 2026-08-22
og_description: 使用 Aspose.OCR 在 C# 中识别图像中的文本。按照本教程将图像 OCR 为文本，提取 JPG 中的文字，并读取西里尔文图像文本。
og_image_alt: Screenshot of C# console output showing recognized Cyrillic text from
  a JPG image
og_title: 使用 Aspose.OCR 从图像识别文本 – 步骤详解 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-08-22'
  description: Learn to recognize text from image using Aspose.OCR. This guide also
    covers OCR image to text and extract text from jpg in a few steps.
  headline: How to recognize text from image with Aspose.OCR in C#
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 Aspose.OCR 识别图像中的文本
url: /zh/net/text-recognition/how-to-recognize-text-from-image-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.OCR 识别图像中的文本 – 完整 C# 教程

如果您需要在 .NET 项目中识别图像中的文本，本教程将向您展示一个可直接运行的解决方案。您将看到如何设置 OCR 引擎、选择正确的语言模块以及输出提取的字符。示例还演示了如何将西里尔文图片的图像 OCR 为文本，涵盖了读取西里尔文文本图像文件的常见情况。

除了核心步骤外，您还将学习如何从 jpg 文件中提取文本、将图像转换为其他格式的文本，以及处理需要自动下载语言模块的情况。除了 Aspose.OCR NuGet 包外，不需要任何外部服务。

## 前提条件

- .NET 6.0 SDK 或更高版本已安装  
- Visual Studio 2022（或任何支持 C# 的编辑器）  
- 首次运行需要互联网访问（西里尔文语言模块按需获取）  
- Aspose.OCR NuGet 包 (`dotnet add package Aspose.OCR`)  

这些项目使您能够在无需额外配置的情况下编译并运行代码。

## 第一步：创建新的控制台项目

打开终端并执行以下命令以搭建一个最小的控制台应用程序：

```bash
dotnet new console -n ImageOcrDemo
cd ImageOcrDemo
dotnet add package Aspose.OCR
```

`dotnet new console` 命令会创建一个 `Program.cs` 文件和一个引用 Aspose.OCR 库的项目文件。添加该包会解决所有必需的程序集。

## 第二步：导入 Aspose.OCR 命名空间

编辑 **Program.cs** 并在文件顶部添加 `using Aspose.OCR;` 指令。这使得 OCR 类可以在不使用完全限定名的情况下使用。

```csharp
using System;
using Aspose.OCR;
```

`using` 语句提升了可读性，并使代码专注于 OCR 工作流。

## 第三步：初始化 OCR 引擎

实例化 `OcrEngine`。该引擎保存语言模块和识别设置等配置。

```csharp
// Initialise the OCR engine
var ocrEngine = new OcrEngine();
```

在每个应用程序中只创建一次引擎是高效的，因为底层本机库只会加载一次。

## 第四步：选择语言模块

对于西里尔文文本，将 `Language` 属性设置为 `Language.Cyrillic`。如果缺少模块，Aspose.OCR 会自动下载，因此首次执行可能需要几秒钟。

```csharp
// Choose Cyrillic language module – it will be downloaded if absent
ocrEngine.Language = Language.Cyrillic;
```

如果以后需要将图像 OCR 为其他语言的文本（例如 English 或 Arabic），请将 `Language.Cyrillic` 替换为相应的枚举值。这种灵活性使您能够将图像转换为任何受支持脚本的文本。

## 第五步：从 JPG 文件识别文本

使用图像的完整路径调用 `RecognizeImage`。该方法返回包含提取字符串的 `OcrResult`。

```csharp
// Path to the source image – replace with your own file
string imagePath = @"YOUR_DIRECTORY/sample_image.jpg";

// Perform OCR – this extracts text from the JPG file
OcrResult result = ocrEngine.RecognizeImage(imagePath);
```

此调用适用于 Aspose.OCR 支持的任何栅格图像格式（JPG、PNG、BMP、TIFF）。使用 JPG 可确保您能够直接从 jpg 文件中提取文本，无需额外的转换步骤。

## 第六步：输出识别的文本

最后，将识别的文本写入控制台。这演示了一种读取西里尔文图像并显示的简易方法。

```csharp
// Show the recognised text in the console
Console.WriteLine("Recognised text:");
Console.WriteLine(result.Text);
```

运行程序后，您应该会看到西里尔字符如同源图片中那样被准确打印出来。

## 完整工作示例

下面是完整的 **Program.cs** 文件，您可以直接复制、粘贴并运行。

```csharp
using System;
using Aspose.OCR;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Choose the language module required for recognition (Cyrillic in this case)
            // The language module will be downloaded automatically if not present
            ocrEngine.Language = Language.Cyrillic;

            // Step 3: Provide the path to the image you want to process
            // You can replace the file name with any JPG, PNG, BMP, or TIFF image
            string imagePath = @"YOUR_DIRECTORY/sample_image.jpg";

            // Step 4: Recognise text from the image file
            OcrResult result = ocrEngine.RecognizeImage(imagePath);

            // Step 5: Output the recognised text
            Console.WriteLine("Recognised text:");
            Console.WriteLine(result.Text);
        }
    }
}
```

### 预期输出

```
Recognised text:
Пример текста на кириллице
```

确切的输出取决于 `sample_image.jpg` 的内容。如果图像包含英文文本，只要将 `ocrEngine.Language = Language.English;` 设置为相应值，相同的代码将返回英文字符串。

## 处理常见陷阱

| 问题 | 原因 | 解决办法 |
|------|------|----------|
| 未找到语言模块 | 首次运行尝试下载模块，但由于防火墙限制导致下载失败。 | 确保机器能够访问 `https://downloads.aspose.com/ocr`，或手动从 Aspose 门户下载模块并放置在默认文件夹 (`%APPDATA%\Aspose\OCR\`) 中。 |
| 噪声图像准确率低 | OCR 引擎依赖文本与背景之间的清晰对比。 | 在调用 `RecognizeImage` 之前对图像进行预处理（例如，提高对比度、转换为灰度）。Aspose.OCR 提供 `ImagePreprocessing` 选项，可供探索。 |
| 非 JPG 格式 | 部分开发者认为代码只能处理 JPG 文件。 | API 同样支持 PNG、BMP 和 TIFF。相应地更改 `imagePath` 中的文件扩展名即可。 |
| 大文件导致处理时间长 | 更大的图像需要更多的内存和 CPU 周期。 | 在识别前将图像调整到合理分辨率（例如 1500 × 1500）。 |

这些技巧帮助您在不同场景下可靠地将图像转换为文本。

## 扩展解决方案

一旦能够识别图像中的文本，您可能想要：

- **将结果保存到文件** – 将 `result.Text` 写入 `.txt` 或 `.docx` 文档。  
- **批量处理文件夹** – 遍历目录中的所有文件并应用相同的 OCR 逻辑。  
- **结合正则表达式** – 从识别的字符串中提取电话号码、日期或其他模式。  

所有这些扩展都复用相同的核心代码，使实现保持简洁。

## 结论

您现在拥有使用 Aspose.OCR 在 C# 中识别图像文本的完整指南。教程涵盖了如何设置项目、初始化 OCR 引擎、选择西里尔文语言模块以及从 JPG 文件中提取文本。通过遵循这些步骤，您还可以对其他语言进行图像 OCR、从 jpg 文件提取文本，并在任何 .NET 应用程序中实现图像转文本。

欢迎尝试其他语言、更大的批处理或后处理逻辑。如果您需要在不同的场景（例如 Web API 或 Windows 服务）中读取西里尔文图像，使用相同的模式即可。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，构建在本指南展示的技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方法。

- [使用 Aspose.OCR 进行语言选择的 C# 图像文本提取](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [使用 Aspose OCR 进行多语言图像文本识别](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [OCR 预处理管道 – 如何在 C# 中识别图像文本](/ocr/english/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}