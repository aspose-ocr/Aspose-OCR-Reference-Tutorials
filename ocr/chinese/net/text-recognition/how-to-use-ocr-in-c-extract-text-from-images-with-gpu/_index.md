---
category: general
date: 2026-02-13
description: 学习如何在 C# 中使用 OCR 从图像文件中提取文本，启用 GPU 处理，并快速将扫描件转换为文本。
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: zh
og_description: 如何在 C# 中使用 OCR？本指南向您展示如何从图像文件中提取文本、启用 GPU 处理，以及将扫描件转换为文本。
og_title: 如何在 C# 中使用 OCR – 使用 GPU 从图像中提取文本
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: 如何在 C# 中使用 OCR – 使用 GPU 从图像中提取文本
url: /zh/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

keep code values unchanged.

Also the blockquote > **Pro tip:** etc.

Also the "Common question:" blockquote.

Also alt text.

Let's produce.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 使用 GPU 从图像中提取文本

有没有想过 **如何使用 OCR** 在不费力的情况下从扫描文档中提取文本？你并不是唯一有这种疑问的人——开发者经常会问：“如何高效地从图像文件中提取文本？”好消息是，使用 Aspose.OCR 你完全可以做到，而且还能 **启用 GPU 处理**，在支持的硬件上显著提升速度。

在本教程中，我们将完整演示一个端到端的示例，展示 **如何使用 OCR**、**如何从图像中提取文本**、**如何将扫描转换为文本**，以及在 GPU 不可用时的处理方式。完成后，你将拥有一个可直接运行的 C# 控制台应用程序，它会打印识别出的文本并告诉你是否实际使用了 GPU。

## 你需要准备的内容

- .NET 6 SDK 或更高版本（代码同样适用于 .NET Core）  
- Visual Studio 2022 或任意你喜欢的编辑器  
- Aspose.OCR for .NET 包（可通过 NuGet 获取）  
- 一张高分辨率的图像文件（例如 `highres_scan.tif`）用于测试  

无需复杂的环境搭建——只需几条 NuGet 命令即可开始。

## 第一步：安装 Aspose.OCR 并准备项目

首先，你需要将 OCR 库引入项目。打开解决方案文件夹中的终端，运行：

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

该命令会创建一个名为 **OcrDemo** 的全新控制台项目，并添加 `Aspose.OCR` NuGet 包。库中包含我们将使用的 `OcrEngine` 类。

> **专业提示：** 如果你的机器配有独立 GPU，请确保已安装最新的显卡驱动；否则库会自动回退到 CPU 模式。

## 第二步：编写完整的 OCR 代码

现在打开 `Program.cs`，将其内容替换为以下代码。每行都已添加注释，帮助你了解 *为什么* 要这么做。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### 为什么这样可行

- **ProcessingMode = Gpu** 告诉引擎优先尝试 GPU。库已经封装了底层的 CUDA/OpenCL 调用，你无需自行管理设备上下文。  
- **IsGpuEnabled** 是一个布尔值，用于确认 GPU 路径是否成功。如果显示 `false`，说明引擎已自动回退到 CPU——无需惊慌。  
- **RecognizeImage** 完成所有核心工作：加载图像、运行 OCR 模型并返回纯文本结果。除非有特殊需求（例如去倾斜），否则无需手动预处理位图。

## 第三步：运行应用并验证输出

编译并执行：

```bash
dotnet run
```

如果一切配置正确，你会看到类似如下的输出：

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

如果 GPU 不可用，第一行会显示 `GPU used: False`，但提取的文本仍会出现——这得益于优雅的回退机制。

> **常见问题：** *如果我的图像是 JPEG 而不是 TIFF，该怎么办？*  
> `RecognizeImage` 方法接受 .NET `System.Drawing` 支持的任何格式（JPEG、PNG、BMP 等）。只需在 `imagePath` 中更改文件扩展名即可。

## 第四步：可选 – 调整设置以提升准确率

Aspose.OCR 提供了若干可调参数：

| 设置 | 功能说明 | 使用场景 |
|------|----------|----------|
| `ocrEngine.Language` | 强制使用特定语言（例如 `OcrLanguage.English`） | 已知文档语言时 |
| `ocrEngine.PageSegMode` | 控制引擎如何将页面划分为块 | 多列布局时 |
| `ocrEngine.DetectOrientation` | 自动旋转非正向文本 | 可能倒置的扫描件 |

可以在调用 `RecognizeImage` 之前设置这些属性。例如：

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## 第五步：可视化流程（带 Alt 文本的图片）

下面是一张简易示意图，展示 **如何使用 OCR** 并可选地启用 GPU 加速。它并非代码运行的必需部分，但有助于你把握整体流程。

![Diagram showing how to use OCR with GPU processing](/images/ocr-gpu-flow.png)

*Alt text:* *Diagram showing how to use OCR with GPU processing, highlighting the fallback to CPU when needed.*

## 边缘情况与故障排除

1. **GPU 内存不足** – 超大图像可能超出 GPU 内存限制。此时库会自动回退到 CPU。你可以预先缩放图像以降低内存占用。  
2. **不支持的图像格式** – 若 `RecognizeImage` 抛出 *NotSupportedException*，请检查文件扩展名并确认图像未损坏。转换为 PNG 往往能解决此问题。  
3. **置信度分数低** – 当 OCR 结果出现大量不可读字符时，考虑进行预处理（二值化、去噪）或使用更高分辨率的扫描件。  

## 小结：我们完成了什么

我们已经演示了 **如何在 C# 控制台应用中使用 OCR**，展示了 **如何从图像文件中提取文本**，并说明了 **如何启用 GPU 处理** 以获得更快的结果。现在，你知道了 **如何将扫描转换为文本**、如何验证 GPU 是否真正被使用，以及在特定场景下如何微调设置。

### 后续步骤

- 将输出导入 **搜索索引**（例如 Elasticsearch），让扫描的 PDF 也能被搜索。  
- 尝试 **批量处理**——遍历文件夹中的图像并将每个结果写入 `.txt` 文件。  
- 将 OCR 与 **翻译 API** 结合，实现对扫描的外文文档自动翻译。  

还有其他问题吗？欢迎留言，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}