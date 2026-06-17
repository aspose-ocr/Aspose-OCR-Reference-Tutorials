---
category: general
date: 2026-03-18
description: 使用 Aspose OCR 在 C# 中从图像提取文本。了解如何提取文本、运行 OCR 识别以及在无需互联网的情况下识别西里尔文文本。
draft: false
keywords:
- extract text from image
- how to extract text
- run OCR recognition
- recognize cyrillic text
- offline OCR with Aspose
language: zh
og_description: 使用 Aspose OCR 从图像中提取文本。一步步指南，教您运行 OCR 识别、如何提取文本以及离线识别西里尔文文本。
og_title: 在 C# 中从图像提取文本 – 离线 OCR 教程
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 在 C# 中从图像提取文本 – 完整离线 OCR 指南
url: /zh/net/text-recognition/extract-text-from-image-in-c-complete-offline-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本 – 完整离线 OCR 指南

是否曾经需要 **从图像中提取文本**，却担心网络延迟或授权限制？你并不是唯一的遇到这种情况的人。许多开发者在应用必须在受限环境中运行，却仍需要可靠的 OCR 时会卡住。好消息是？使用 Aspose OCR，你可以在本地运行完整的流水线，**从图像中提取文本**，而无需触及互联网。

在本教程中，我们将通过一个实用示例演示 **如何提取文本**、搭建离线引擎、**运行 OCR 识别**，甚至 **识别西里尔文**。完成后，你将拥有一个可直接运行的 C# 控制台应用程序，能够将检测到的字符串直接打印到控制台。

## 你需要准备的内容

- .NET 6.0 SDK（或任意近期的 .NET 版本）  
- Visual Studio 2022 或 VS Code – 任选其一  
- Aspose.OCR for .NET NuGet 包  
- 包含 Aspose OCR 模型文件的文件夹（从 Aspose 门户下载一次）  
- 一张包含英文和西里尔字符的图像文件（例如 `cyrillic_doc.jpg`）

无需外部服务，无需运行时隐藏下载——所有内容都在你的磁盘上。

## 第一步：安装 Aspose.OCR 并准备资源

首先，将 Aspose.OCR NuGet 包添加到项目中：

```bash
dotnet add package Aspose.OCR
```

接着，在机器上的任意位置创建一个名为 `AsposeOCRResources` 的文件夹，并将从 Aspose 下载的模型文件复制进去。OCR 引擎会在该目录中查找语言包，请确保路径正确。

> **专业提示：** 将资源文件夹放在 `.csproj` 文件旁边；这可以简化开发期间的路径处理。

## 第二步：构建离线 OCR 引擎

现在我们实例化引擎并指向资源文件夹。这一步至关重要，使我们能够 **离线运行 OCR 识别**。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell the engine where the language models live
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // 3️⃣ Load the languages you need – English and Cyrillic
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);
```

为什么要显式加载语言？因为我们让引擎保持离线，它不会去 Aspose 服务器获取缺失的语言包。如果忘记加载某种语言，来自该脚本的字符将被忽略。

## 第三步：将图像输入引擎

引擎准备好后，我们提供要处理的图像。`ImageStream.FromFile` 辅助方法会将文件读取为 OCR 引擎能够理解的格式。

```csharp
        // 4️⃣ Load the target image (make sure the path points to your file)
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");
```

如果图像较大，建议事先对其进行缩放，以提升速度和准确性。OCR 引擎在约 300 DPI 时表现最佳。

## 第四步：执行识别过程

调用 `Recognize` 即可完成繁重的工作。该方法返回一个 `OcrResult` 对象，包含提取的字符串、置信度分数等信息。

```csharp
        // 5️⃣ Run the OCR recognition
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

在幕后，Aspose 会解析位图，运行针对特定语言的神经网络，并将字符拼接起来。因为我们已经加载了英文和西里尔文，混合脚本文档能够无缝处理。

## 第五步：显示提取的文本

最后，我们输出结果。在真实应用中，你可能会将其存入数据库或传递给其他服务，但在本演示中我们仅打印出来。

```csharp
        // 6️⃣ Show the extracted text on the console
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

运行程序后，你应该会看到类似如下的输出：

```
=== OCR Output ===
This is an English line.
Это строка на кириллице.
```

如果出现乱码，请再次确认西里尔语言包已正确放置在资源文件夹中，并且图像没有过于模糊。

![从图像提取文本示例](extract_text_image.png "从图像提取文本")

*图片替代文字：从图像提取文本 – OCR 结果显示英文和西里尔文行。*

## 常见问题处理

### 缺少语言包

如果出现 “Language data not found” 异常，说明引擎未能定位模型文件。请检查 `ResourcesPath`，并确保文件夹中包含 `english.dat`、`cyrillic.dat`（或同名文件）。

### 置信度分数低

有时 OCR 引擎会对某些字符返回低置信度，尤其是图像噪声较多时。你可以通过以下方式提升准确性：

- 在将图像送入引擎前先转换为灰度图  
- 使用中值滤波器降低斑点噪声  
- 确保文本水平对齐（必要时旋转）

### 大图像

处理 10 MP 照片可能会很慢。将宽度最大限制在 2000 像素并保持纵横比缩放；引擎仍能准确捕获大多数字符。

## 扩展示例

- **批量处理：** 将识别逻辑包装在循环中，遍历目录下的所有文件。  
- **输出格式：** `OcrResult` 还提供 `TextLines` 集合，包含边界框信息——在 UI 应用中高亮文本时非常有用。  
- **其他语言：** 只需使用 `LoadLanguage` 调用任意受支持的枚举值（例如 `Language.French`）即可。

所有这些扩展仍遵循 **如何提取文本** 的原则——只需加载相应的语言包，让引擎完成其余工作。

## 完整源码回顾

下面是完整的、可直接复制粘贴的程序。将 `YOUR_DIRECTORY` 替换为你机器上的实际路径。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Point the engine to the folder that contains OCR model files
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // Step 3: Load the languages you need (no automatic download will occur)
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);

        // Step 4: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");

        // Step 5: Run the recognition process
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 6: Display the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

将其保存为 `Program.cs`，运行 `dotnet run`，即可在控制台看到引擎从图像中提取的文本。就这样，你已经成功 **离线从图像中提取文本**。

## 结论

我们已经覆盖了使用 Aspose OCR 在完全离线场景下 **从图像中提取文本** 所需的全部内容。指南展示了 **如何提取文本**、演示了 **运行 OCR 识别**，并证明了在无需任何网络调用的情况下 **识别西里尔文** 与英文并存。

从设置 NuGet 包到处理缺失语言包等边缘情况，你现在拥有了在任何 .NET 应用中构建 OCR 功能的坚实基础。

接下来可以尝试处理 PDF、扫描多页文档，或将输出与搜索索引集成。一旦掌握离线 OCR，可能性无限。

祝编码愉快，愿你的图像永远清晰！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}