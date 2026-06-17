---
category: general
date: 2026-03-21
description: 了解如何使用 Aspose OCR 对图像文件进行去倾斜并识别文本图像。只需几行 C# 代码即可将 jpg 转换为文本并纠正图像旋转。
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: zh
og_description: 如何使用 Aspose OCR 对图像进行去倾斜并从 JPEG 中提取文本。请按照本分步指南将 JPG 转换为文本并校正图像旋转。
og_title: 如何在 C# 中校正图像倾斜 – 快速 Aspose OCR 教程
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中去除图像倾斜 – 使用 Aspose OCR 的完整指南
url: /zh/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中去倾斜图像 – 使用 Aspose OCR 的完整指南

是否曾经想过 **how to deskew image** 文件在扫描仪倾斜的情况下输出？你并不孤单——许多开发者在尝试从收据、发票或手写笔记中提取文本时都会遇到这个问题。好消息是，使用 Aspose OCR，你可以纠正图像旋转，并仅用几行代码提取干净、可搜索的文本。

在本教程中，我们将完整演示整个过程：从安装库、启用自动去倾斜，到识别文本图像，最后将 JPG 转换为文本。完成后，你将拥有一个可直接运行的控制台应用程序，能够 **recognize text jpg** 文件，而无需手动旋转它们。

## 你需要的环境

- **.NET 6.0** 或更高（代码在 .NET Core 和 .NET Framework 上均可运行）  
- **Aspose.OCR for .NET** NuGet 包 – 推荐使用 23.12 或更新的版本  
- 一个示例 **skewed JPEG**（例如 `skewed_receipt.jpg`），放在应用程序可以读取的位置  
- Visual Studio、VS Code 或任何你喜欢的 C# 编辑器  

不需要其他第三方工具。该库内部处理去倾斜、OCR 以及语言检测。

![how to deskew image example](/images/deskew-example.png "how to deskew image using Aspose OCR")

## 步骤 1：设置项目并安装 Aspose.OCR

为了保持整洁，先创建一个全新的控制台项目：

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

`dotnet add package` 命令会拉取 **Aspose.OCR** 二进制文件以及所有本机依赖。如果你在 Windows 上，会自动获取本机 DLL；在 Linux/macOS 上可能需要手动安装 `libgdiplus` 包，但这只需一次安装。

## 步骤 2：启用自动去倾斜（纠正图像旋转）

现在打开 `Program.cs`，将其内容替换为下面的代码。关键行是 `ocrEngine.Settings.Deskew = true;` —— 该标志告诉引擎自动 **how to deskew image**。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### 为什么要启用 Deskew？

当扫描仪以倾斜角度送入页面时，文本基线会倾斜。传统 OCR 引擎会把每个字符当作倾斜的版本来读取，导致准确率大幅下降。通过设置 `Deskew = true`，Aspose OCR 在内部运行快速的 Hough 变换，将位图旋转回水平，然后进行识别。其效果等同于你在 Photoshop 中手动旋转图像——但更快且全自动。

## 步骤 3：识别文本图像并将 JPG 转换为文本

`Recognize` 调用一次性完成两件事：

1. **Deskews** 图像（因为我们打开了该标志）。  
2. **Extracts** 文本内容，并以 `OcrResult` 对象返回。

你可以将 `ocrResult.Text` 当作普通字符串使用，写入文件，或传递给后续处理管道。如果需要每个单词的原始置信度分数，`ocrResult.Words` 会提供包含 `Confidence` 值的集合。

### 示例输出

假设 `skewed_receipt.jpg` 是一张简单的收据，你可能会看到类似以下的输出：

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

请注意，尽管原始图像大约旋转了 7°，数字仍然对齐得很好。这正是库中内置的 **correct image rotation**（纠正图像旋转）的魔力。

## 步骤 4：运行示例并验证结果

编译并运行：

```bash
dotnet run
```

如果一切配置正确，你会在控制台看到提取的文本。如果出现 `FileNotFoundException` 等异常，请再次确认 JPEG 的路径并确保文件可读。

### 常见陷阱与专业提示

- **Large Images** – OCR 的内存使用随图像尺寸增长。请在将文件送入引擎前将过大的文件（例如宽度 > 3000 px）进行缩放。  
- **Non‑Latin Scripts** – 默认情况下引擎假设使用英语。如果需要在其他字母表中 **recognize text image**，请设置 `ocrEngine.Settings.Language = OcrLanguage.French;`（或任何受支持的语言）。  
- **Batch Processing** – 对于大量文件，复用同一个 `OcrEngine` 实例；为每个文件创建新引擎会产生不必要的开销。  
- **Quality Check** – 去倾斜后，你可以通过 `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` 导出校正后的位图，以目视验证旋转修正。

## 完整工作示例（全部代码）

下面是完整的、独立的程序示例，你可以直接复制粘贴到 `Program.cs` 中。它包含注释、错误处理，以及一个可选的步骤用于保存去倾斜后的图像。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

运行该程序将 **recognize text jpg** 文件，自动纠正任何倾斜，并在控制台打印干净、可搜索的文本。

## 总结

现在你拥有一个稳健、可用于生产环境的代码片段，展示了使用 Aspose OCR **how to deskew image** 文件并提取其内容。该方法适用于收据、发票、扫描的合同或任何文本未完全水平的 JPEG。

下一步你可能想探索：

- **Batch processing** 对文件夹中的 JPEG 进行批处理，并将每个结果写入 `.txt` 文件（关联到 *convert jpg to text*）。  
- 将 OCR 步骤集成到 ASP.NET Core API 中，以便客户端上传图像并接收 JSON 格式的文本。  
- 尝试不同的 OCR 设置，如 `ocrEngine.Settings.Language` 或 `ocrEngine.Settings.RecognitionMode`，以提升非英文文档的准确率。

试一试，调整设置，让引擎完成繁重的工作。和往常一样，如果遇到问题或有巧妙的优化想分享，请在下方留言。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}