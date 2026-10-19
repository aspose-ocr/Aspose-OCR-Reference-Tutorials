---
category: general
date: 2026-02-14
description: 如何在 C# 中使用 Aspose.OCR 执行 OCR —— 学习从图像中提取文本、从文件加载图像并快速对图像进行 OCR。
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image from file
- recognize text from jpg
- run OCR on image
language: zh
og_description: 如何在 C# 中使用 Aspose.OCR 执行 OCR。本指南向您展示如何从图像中提取文本、从文件加载图像以及高效地对图像进行 OCR。
og_title: 如何在 C# 中实现 OCR – 完整编程教程
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中进行 OCR – 步骤指南
url: /zh/net/text-recognition/how-to-perform-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中执行 OCR – 完整编程教程

有没有想过 **如何在手机拍摄的图片上执行 OCR**？也许你需要从 JPEG 中提取街道标志的文字用于导航应用，或者你有一批扫描的合同想把它们转换为可搜索的文本。简而言之，你想要 *从图像中提取文本*，且不将任何数据发送到云端。

好消息是，你完全可以使用 Aspose.OCR for .NET 在本地完成这些操作。在本教程中，我们将演示如何从文件加载图像、从 JPG 识别文字，最终 **在离线环境下对图像运行 OCR**。完成后，你将拥有一段可直接运行的代码片段，能够在控制台打印出识别出的阿拉伯文文本。

> **你将获得：** 一个自包含、可运行的 C# 程序，对每行代码意义的解释，以及处理常见边缘情况（如资源缺失或不支持的语言）的技巧。

## 前置条件

在开始之前，请确保你具备以下条件：

| 要求 | 原因 |
|------|------|
| .NET 6.0 或更高（或 .NET Framework 4.7+） | Aspose.OCR 目标是 .NET Standard 2.0，任何现代运行时均可。 |
| Visual Studio 2022（或带 C# 扩展的 VS Code） | IDE 能方便管理 NuGet 包并运行控制台应用。 |
| Aspose.OCR NuGet 包（`Aspose.OCR`） | 该库负责实际的 OCR 工作。 |
| 包含离线 OCR 资源的文件夹（从 Aspose 下载） | 离线资源避免在识别过程中进行任何 HTTP 调用。 |
| 一张图像文件（例如 `arabic_sign.jpg`） | 我们将使用包含阿拉伯文字的 JPEG，其他语言同样适用。 |

如果缺少上述任意项，请立即获取——别等到教程进行到一半才发现依赖缺失。

## 步骤 1：安装 Aspose.OCR 并准备资源

首先，将 Aspose.OCR 包添加到项目中：

```bash
dotnet add package Aspose.OCR
```

安装完包后，从 Aspose 官网下载 **离线 OCR 资源包**。解压到本机的某个文件夹，例如：

```
C:\OCRResources\
```

> **为什么重要：** 在启动时一次性加载资源可以消除网络延迟，并且符合 GDPR 要求，因为数据不会离开本机。

## 步骤 2：创建 OCR 引擎并指向资源文件夹

接下来实例化 `Engine` 类，并告诉它资源所在的位置。这就是 **如何在本地执行 OCR** 的核心。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Step 2: Initialize the OCR engine with the offline resource folder
Engine ocrEngine = new Engine
{
    // Replace with the path you used in the previous step
    ResourceFolder = @"C:\OCRResources"
};

// Load the resources into memory – this prevents any hidden HTTP calls
ocrEngine.LoadResources();
```

> **小技巧：** 如果你担心文件夹路径可能错误，可以将 `LoadResources` 调用包装在 try‑catch 块中。异常信息会明确指出缺失的文件。

## 步骤 3：从文件加载图像

随后，我们需要 **从文件加载图像**，以便引擎进行分析。Aspose.OCR 使用其自有的 `ImageStream` 包装器。

```csharp
// Step 3: Load the JPEG you want to recognize
ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");
```

如果图像位于其他位置，只需修改路径即可。`ImageStream` 类抽象了底层位图处理，你无需关心 GDI+ 兼容性。

## 步骤 4：使用语言设置识别 JPG 中的文字

现在进入 **如何执行 OCR** 的核心——实际识别字符。我们将请求阿拉伯语识别，你也可以将 `Language.Arabic` 替换为其他受支持的语言。

```csharp
// Step 4: Run OCR specifying the desired language (Arabic in this example)
OcrResult ocrResult = ocrEngine.Recognize(
    image,
    new OcrOptions { Language = Language.Arabic }
);
```

> **为什么要指定语言？** OCR 引擎会使用语言特定的词典和字符模型。提供正确的语言能够显著提升准确率，尤其是像阿拉伯语这样形状复杂的脚本。

## 步骤 5：显示提取的文本

最后，让我们 **从图像中提取文本** 并打印出来。这是验证 OCR 是否成功的最简方式。

```csharp
// Step 5: Output the recognized text to the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrResult.Text);
```

运行程序后，控制台应显示标牌上的阿拉伯语短句。如果输出乱码，请再次确认已选择正确的语言，并检查资源文件夹中是否包含阿拉伯语数据文件。

## 完整可运行示例

下面是完整的、可直接编译的程序，整合了上述所有步骤。复制粘贴到新建的控制台项目（`dotnet new console`）中，然后按 **F5** 运行。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Configure the OCR engine with offline resources
            // -------------------------------------------------
            Engine ocrEngine = new Engine
            {
                ResourceFolder = @"C:\OCRResources" // <-- change to your folder
            };
            ocrEngine.LoadResources(); // Loads language packs, fonts, etc.

            // -------------------------------------------------
            // Step 2: Load the image you want to process
            // -------------------------------------------------
            ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");

            // -------------------------------------------------
            // Step 3: Recognize text – specify language to improve accuracy
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(
                image,
                new OcrOptions { Language = Language.Arabic } // Change as needed
            );

            // -------------------------------------------------
            // Step 4: Output the result
            // -------------------------------------------------
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**预期输出（示例）：**

```
=== OCR Result ===
مطار القاهره الدولي
```

如果将图像换成英文标牌并设置 `Language.English`，相同代码将输出英文文本。这展示了 **在图像上运行 OCR** 的灵活性。

## 从图像中提取文本 – 常见场景处理

### 1. 多页或多帧图像

某些图像格式（如 TIFF）可能包含多页。要在这种情况下 **从图像中提取文本**，可以遍历每一帧：

```csharp
for (int i = 0; i < image.FramesCount; i++)
{
    image.CurrentFrame = i;
    OcrResult pageResult = ocrEngine.Recognize(image, new OcrOptions { Language = Language.English });
    Console.WriteLine($"Page {i + 1}: {pageResult.Text}");
}
```

### 2. 低分辨率图像

当分辨率低于 70 dpi 时，OCR 准确率会急剧下降。如果出现模糊结果，考虑先对图像进行放大：

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;

// Load as Bitmap, resize, then wrap back into ImageStream
Bitmap bmp = new Bitmap(@"C:\OCRResources\lowres.jpg");
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
ImageStream highResStream = ImageStream.FromBitmap(highRes);
```

### 3. 缺失语言包

如果出现类似 *“Language data not found”* 的异常，请确认对应的 `.dat` 文件已存在于你的 `ResourceFolder` 中。Aspose 为每种语言提供单独的 zip 包。

## 在图像上运行 OCR – 性能技巧

- **缓存 Engine 实例：** 为每张图像创建新的 `Engine` 会增加开销。保持单实例用于批量处理可提升性能。
- **安全并行化：**在 `LoadResources` 之后，`Engine` 对只读操作是线程安全的。可以启动多个任务，各自对不同图像调用 `Recognize`。
- **使用完毕后释放：** 虽然 `Engine` 实现了 `IDisposable`，.NET GC 最终会回收，但在 `using` 块中显式调用 `ocrEngine.Dispose()` 是个好习惯。

```csharp
using (Engine ocrEngine = new Engine { ResourceFolder = @"C:\OCRResources" })
{
    ocrEngine.LoadResources();
    // run recognitions here
}
```

## 识别 JPG – 需要注意的边缘情况

| 场景 | 检查要点 | 解决办法 |
|------|----------|----------|
| **JPEG 损坏** | `ImageStream.FromFile` 抛出 `FileNotFoundException` 或 `ArgumentException`。 | 验证文件完整性，必要时使用图形编辑器重新保存图像。 |
| **不支持的语言** | `Language` 枚举中没有你的目标语言。 | 更新 Aspose.OCR 至最新版本；新语言会定期加入。 |
| **混合脚本图像**（例如 English + Arabic） | 单一语言选项可能遗漏次要脚本。 | 分别使用不同语言选项运行 OCR，再将结果拼接。 |

## 小结 – 现在你已经掌握了在 C# 中执行 OCR 的方法

本指南从安装 NuGet 包到打印识别文本，完整演示了使用 Aspose.OCR **执行 OCR** 的全过程。你学会了 **从文件加载图像**、**从图像中提取文本**、**识别 JPG 中的文字**，以及在生产环境中安全 **在图像上运行 OCR**。

### 接下来可以做什么？

- **尝试其他文件格式** 如 PNG 或 BMP——只需更改文件扩展名即可。
- **与数据库集成**，将 OCR 结果存入可搜索的存档。
- **结合计算机视觉**（例如在 OCR 前检测文字区域）以提升速度。

随意调整语言设置、批量处理文件夹，或将输出接入 Web API。OCR 只是构建块，真正的价值在于将其融入更大的工作流。

祝编码愉快，愿你的图像始终清晰如新！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}