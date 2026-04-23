---
category: general
date: 2026-03-17
description: 使用 Aspose OCR 在 C# 中从 PNG 提取文本。学习读取图像文字、处理收据 OCR，并创建具备 GPU 加速的 OCR 引擎。
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: zh
og_description: 使用 Aspose OCR 从 PNG 中提取文本。本指南展示了如何从图像读取文本、处理收据 OCR，以及高效创建 OCR 引擎。
og_title: 从 PNG 中提取文本 – 使用 OCR 读取图像文字
tags:
- OCR
- CSharp
- Aspose
title: 从 PNG 中提取文本 – 使用 OCR 读取图像文字
url: /zh/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 PNG 中提取文本 – 使用 OCR 读取图像文字

是否曾经需要 **从 PNG 中提取文本**，却不确定哪个库能够提供可靠的结果？你并不是唯一的提问者——开发者们经常会问：“如何在不编写自定义神经网络的情况下读取收据等图像文件中的文字？”好消息是，Aspose OCR 已经为你完成了繁重的工作，并且你甚至可以启用 GPU 来提升速度。

在本教程中，我们将一步步演示 **处理收据 OCR** 所需的全部内容，从安装 NuGet 包到创建能够识别 PNG 文件的 OCR 引擎。完成后，你将拥有一个独立的控制台应用程序，能够读取收据图像、打印识别出的文字，并展示如何为不同场景微调引擎。无需外部文档，仅有纯代码和清晰说明。

## 前置条件

- .NET 6.0 SDK（或任意近期的 .NET 版本）  
- Visual Studio 2022 或带有 C# 扩展的 VS Code  
- 支持的 NVIDIA GPU 并安装最新驱动（可选，但推荐用于 GPU 模式）  
- **Aspose.OCR** NuGet 包（`dotnet add package Aspose.OCR`）  

如果没有 GPU，仍然可以在 CPU 模式下运行示例——只需跳过 GPU 配置代码行。

## 第一步：安装 Aspose.OCR 并创建项目

首先，创建一个新的控制台项目并引入 Aspose OCR 库。

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

为什么要这么做：`Aspose.OCR` 包含 OCR 引擎、图像加载器以及可选的 GPU 支持。通过 NuGet 添加可确保获取最新的稳定版本（截至 2026 年 3 月为 23.10）。

## 第二步：导入命名空间并创建 OCR 引擎

现在打开 **Program.cs**，添加所需的 `using` 指令，然后实例化引擎。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**小贴士：** 在没有 GPU 的机器上如果遇到 `System.DllNotFoundException`，只需注释掉设置 `EngineMode` 和 `GpuDeviceId` 的两行代码。引擎会自动回退到 CPU。

## 第三步：加载要提取文本的 PNG 图像

Aspose OCR 可以直接从文件路径、流或字节数组读取图像。此演示中我们将加载本地的收据图像。

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

请注意我们对文件缺失的防护。在实际项目中，你可能会显示友好的 UI 提示，而不是直接退出。

## 第四步：执行 OCR 识别

实际的文本提取只需一次方法调用。引擎会返回一个 `OcrResult` 对象，其中包含原始字符串、置信度分数以及布局信息。

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

为什么要检查 `ocrResult.Text`：有时质量较低的 PNG 会返回空字符串，最好让用户知道而不是悄然无声地输出空结果。

## 第五步：输出识别后的文本

最后，将提取的字符串打印到控制台。你也可以将其写入文件、数据库，或传递给其他服务。

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

运行程序（`dotnet run`）后，你应该会看到类似如下的输出：

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

这就是使用 Aspose OCR **完整的从 PNG 文件提取文本** 的解决方案，你已经学会了如何 **从图像文件读取文字**，尤其是看起来像收据的图像。

## 可选：微调 OCR 引擎（高级）

如果需要针对特定字体或噪声背景获得更高的准确率，可考虑调整以下设置：

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

这些调优在批量 **处理收据 OCR** 时尤为有用，因为有些扫描件并不完美。

## 常见陷阱及解决办法

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| **缺少 GPU 驱动** | 引擎尝试加载 CUDA 但找不到对应 DLL。 | 安装最新的 NVIDIA 驱动，或通过删除 `EngineMode.Gpu` 行切换到 CPU 模式。 |
| **图像路径错误** | `ImageStream.FromFile` 在文件未找到时抛异常。 | 始终验证路径（参见第 3 步），或使用 `Path.Combine` 以确保跨平台安全。 |
| **模糊收据置信度低** | OCR 引擎无法区分字符。 | 启用 `EnableImagePreprocessing`，并在送入引擎前适当提升图像 DPI。 |
| **长时间运行的服务出现内存泄漏** | 每个 `OcrEngine` 持有非托管资源。 | 使用完后释放引擎：`using var ocrEngine = new OcrEngine();` |

## 完整工作示例（复制粘贴）

下面是可以直接粘贴到 `Program.cs` 的 **完整程序**。其中所有可选调优均已注释，便于随时启用。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

保存后运行 `dotnet run`，即可在控制台看到收据内容的打印结果。

![从 PNG 中提取文本示例](receipt.png "从 PNG 中提取文本示例")

*上图展示了代码可以处理的示例收据 PNG。*

## 小结

我们已经介绍了如何使用 Aspose OCR **从 PNG 文件提取文本**，演示了如何 **从图像文件读取文字**，并完整走完了一个 **处理收据 OCR** 的流程，包括可选的 GPU 加速。通过 **自行创建 OCR 引擎**，你可以完全掌控配置、性能和错误处理。

## 接下来可以探索什么？

- **批量处理**：遍历 PNG 收据目录，将每个结果写入 CSV 文件。  
- **与 Azure Functions 集成**：将此控制台应用改造为接受图像上传的无服务器端点。  
- **多语言支持**：将 `Language.English` 替换为 `Language.Spanish`，或添加自定义词典。  
- **后处理**：使用正则表达式从原始 OCR 字符串中提取总金额、日期或税号等字段。

尽情实验吧——一旦掌握了正确的调节手段，OCR 将是一把非常灵活的工具。如果遇到任何问题，欢迎在下方留言或查阅 Aspose OCR API 参考文档以获取更深入的内容。

祝编码愉快，玩转那些顽固的 PNG 收据，让它们变成可搜索的文本！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}