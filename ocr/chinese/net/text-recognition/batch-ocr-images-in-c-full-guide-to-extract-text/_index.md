---
category: general
date: 2026-02-24
description: 使用 Aspose.OCR 在 C# 中快速批量 OCR 图像。了解如何从目录读取文件、识别图像中的文本并将图像转换为文本，只需几个步骤。
draft: false
keywords:
- batch OCR images
- extract text from images
- read files from directory
- recognize text from image
- convert image to text
language: zh
og_description: 使用 Aspose.OCR 在 C# 中批量 OCR 图像。本教程展示了如何从目录读取文件、识别图像中的文本并高效地将图像转换为文本。
og_title: 使用 C# 批量 OCR 图像——完整的逐步指南
tags:
- C#
- OCR
- Aspose
title: 在 C# 中批量 OCR 图像 – 提取文本的完整指南
url: /zh/net/text-recognition/batch-ocr-images-in-c-full-guide-to-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# 批量 OCR 图像 – 完整提取文本指南

是否曾经需要**批量 OCR 图像**但不知从何入手？你并不孤单——许多开发者在首次尝试**批量提取图像中的文本**时都会遇到同样的难题。好消息是，只需几行 C# 代码和 Aspose.OCR，就能把整文件夹的图片快速转换为整洁的 `.txt` 文件。

在本教程中，我们将完整演示整个流程：从目录读取文件，将每张图片送入 OCR 引擎，最后**将图像转换为文本**文件，供索引、搜索或输入下游流水线使用。完成后，你将拥有一个可独立运行的控制台应用，可直接嵌入任何 .NET 解决方案。

## 所需条件

- **.NET 6+**（示例在 .NET 6 上编译，但任何较新的版本都可工作）
- **Aspose.OCR** NuGet 包 (`Install-Package Aspose.OCR`)
- 需要处理的图像文件夹（如 `.png`、`.jpg` 等）
- Visual Studio、Rider 或你喜欢的编辑器

无需额外的配置文件，也不依赖外部服务——仅是本地运行的纯 C# 代码。

## 批量 OCR 图像 – 项目设置

首先，创建一个新的控制台项目：

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

该命令会搭建一个最小项目并引入 OCR 库。恢复完成后，你即可添加核心逻辑。

### 从目录读取文件

我们需要告诉应用源图像所在位置以及生成的文本文件应保存到何处。使用 `System.IO` 可以轻松实现。

```csharp
using System;
using System.IO;
using Aspose.OCR;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Define input and output folders
        string inputFolder  = @"C:\Images\ToProcess";   // <-- change to your source folder
        string outputFolder = @"C:\Images\OcrResults"; // <-- change to your target folder

        // 2️⃣ Ensure the output folder exists
        Directory.CreateDirectory(outputFolder);
```

> **此步骤重要原因：** 如果输出目录不存在，程序在尝试写入 `.txt` 文件时会抛出异常。`CreateDirectory` 是幂等的——如果文件夹已存在则不做任何操作，因此每次运行都安全调用。

### 从图像识别文本并将图像转换为文本

现在我们启动 OCR 引擎并遍历所有找到的文件。循环使用带通配符 (`*.*`) 的 `Directory.GetFiles`，因此会获取*所有*文件，但如果需要可以将过滤器改为 `*.png` 或 `*.jpg`。

```csharp
        // 3️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 4️⃣ Process each image file in the input folder
        foreach (var imagePath in Directory.GetFiles(inputFolder, "*.*", SearchOption.TopDirectoryOnly))
        {
            // 5️⃣ Recognise text from the current image
            var ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 6️⃣ Save the recognised text to a .txt file in the output folder
            string textFilePath = Path.Combine(
                outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, ocrResult.Text);
        }

        Console.WriteLine("✅ All images processed. Check the output folder!");
    }
}
```

**这里发生了什么？**  
- `ocrEngine.RecognizeImage(imagePath)` 读取位图，运行 OCR 算法，并返回一个 `OcrResult` 对象。  
- `ocrResult.Text` 包含引擎能够识别的纯文本内容。  
- `File.WriteAllText` 创建一个新文件（或覆盖已有文件），写入提取的文本。

这就是完整的 **批量 OCR 图像** 流程，代码行数不足 30 行。

## 专业技巧与边缘情况

| 情形 | 建议 |
|-----------|----------------|
| 图像体积大（ > 5 MB ） | 将其预缩放至约 1500 px 宽，以加快识别速度且不损失准确性。 |
| 需要支持 PDF | 首先将每页 PDF 转为图像（例如使用 `Aspose.PDF`），再喂入同一循环。 |
| 有些文件不是图像（如 `.txt`） | 添加简单过滤：`if (!imagePath.EndsWith(".png") && !imagePath.EndsWith(".jpg")) continue;` |
| 想要多语言支持 | 在循环前设置 `ocrEngine.Language = Language.English | Language.Spanish;` |
| 需要进度报告 | 在 foreach 中写入 `Console.WriteLine($"Processing {Path.GetFileName(imagePath)}...");` |

> **专业提示：** 将 OCR 调用包装在 `try/catch` 中。偶尔损坏的图像会导致 `RecognizeImage` 抛异常，捕获后可防止整个批次中止。

## 预期输出

程序执行完毕后，`outputFolder` 中会为每个原始图像生成一个 `.txt` 文件：

```
C:\Images\OcrResults\invoice1.txt
C:\Images\OcrResults\receipt_2024-01-15.txt
C:\Images\OcrResults\signage.png.txt   <-- note the .txt extension
```

每个文件保存引擎提取的原始文本，例如：

```
Invoice #12345
Date: 01/15/2024
Total: $1,250.00
Thank you for your business!
```

现在你可以将这些文件导入搜索索引、进行情感分析，或仅仅出于合规目的进行归档。

## 常见问题

**Q: 这在 Linux 上能运行吗？**  
A: 当然可以。Aspose.OCR 是跨平台的，这里使用的 `System.IO` API 与操作系统无关。只需调整文件夹路径（如 `/home/user/images`）。

**Q: 如果需要**递归读取目录中的文件**怎么办？**  
A: 将 `SearchOption.TopDirectoryOnly` 改为 `SearchOption.AllDirectories`。注意深层文件夹的权限问题。

**Q: OCR 的准确率如何？**  
A: 准确率取决于图像质量、字体和语言。为获得最佳效果，请使用高分辨率扫描和干净的背景。你也可以调节 `ocrEngine.Config`，启用去倾斜或降噪等功能。

## 总结

你刚刚学习了如何使用 Aspose.OCR 在 C# 中 **批量 OCR 图像**，从读取目录文件到 **从图像识别文本**，再到最终 **将图像转换为文本** 文件，以便存储或进一步处理。上面的完整可运行示例应可直接使用，技巧部分为你提供了扩展或定制该方案的路线图。

下一步？尝试使用 WinForms 或 WPF 添加简易 UI，将输出集成到 Azure Cognitive Search，或尝试 Aspose.OCR 支持的其他语言。一旦掌握核心循环，想象空间无限。

祝编码愉快，愿你的 OCR 批处理无错误！  

![Diagram of batch OCR images process](batch-ocr-images-diagram.png "Batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}