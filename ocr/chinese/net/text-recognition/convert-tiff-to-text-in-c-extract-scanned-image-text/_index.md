---
category: general
date: 2026-03-05
description: 使用 Aspose OCR 在 C# 中将 TIFF 转换为文本——快速提取扫描图像文件中的文字，并学习如何在 C# 中加载图像文件进行
  OCR 处理。
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: zh
og_description: 使用 Aspose OCR 在 C# 中将 TIFF 转换为文本。了解从扫描图像提取文本并高效加载图像文件的完整工作流程。
og_title: 在 C# 中将 TIFF 转换为文本 – 提取扫描图像文本
tags:
- OCR
- C#
- Aspose
title: 在 C# 中将 TIFF 转换为文本 – 提取扫描图像文字
url: /zh/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中将 TIFF 转换为文本 – 提取扫描图像文本

需要 **在 C# 中将 TIFF 转换为文本** 吗？你并不是唯一一个与顽固的多页扫描图像搏斗、这些图像拒绝转换为可搜索字符串的人。  
在本指南中，我们将逐步演示一个完整、即开即用的解决方案，该方案读取 TIFF 文件，将其送入 Aspose OCR，并输出纯文本——无需额外服务，也没有隐藏的魔法。

> **专业提示：** 如果你处理的是高分辨率扫描，启用 GPU 处理可以为每页节省数秒。

我们还将展示如何 **提取扫描图像文本** 文件以及将 **C# 加载图像文件** 到 OCR 引擎的最佳方式，这样你就可以将此逻辑嵌入到任何 .NET 项目中。

---

## 您需要的条件

在我们开始之前，请确保你的机器上具备以下条件：

| Requirement | Reason |
|-------------|--------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | 现代运行时，支持 `Span<T>` 和异步 I/O |
| Aspose.OCR for .NET (NuGet package `Aspose.OCR`) | 我们将使用的 OCR 引擎 |
| A valid Aspose OCR license file (`Aspose.OCR.lic`) | 没有它你将受到评估限制 |
| A TIFF file (single‑ or multi‑page) to test | 使用的示例：`scanned_multi_page.tif` |
| GPU with CUDA 11+ (optional) | 当 `EngineMode = Gpu` 时加速识别 |

如果缺少其中任何项，请立即获取 NuGet 包：

```bash
dotnet add package Aspose.OCR
```

---

## 第一步：设置项目并导入命名空间

创建一个新的控制台应用程序（或将代码添加到现有项目中）。我们首先要做的是导入所需的类。

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **为什么这很重要：** 导入 `Aspose.OCR.Image` 为我们提供了 `ImageStream` 工厂，它可以直接从磁盘或流读取 TIFF 文件。跳过此步骤将导致编译时错误。

---

## 第二步：初始化 OCR 引擎并选择处理模式

必须在分配任何图像之前配置 OCR 引擎。此时我们决定是使用 CPU 还是利用 GPU。

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*如果你在没有显卡的无头服务器上，请将 `Gpu` 改为 `Cpu` 或 `Auto`。*  
引擎模式会影响内存分配和速度；在大型高分辨率 TIFF 上，GPU 模式可快 2‑3 倍。

---

## 第三步：应用你的 Aspose OCR 许可证

未使用许可证运行时会限制页面数量并添加水印。请尽早加载许可证，以便后续所有操作都不受限制。

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **常见陷阱：** 在 `Recognize()` 之后调用 `SetLicense` 会导致该次调用回退到试用模式。

---

## 第四步：加载 TIFF 文件 – 处理单页和多页图像

Aspose OCR 开箱即支持读取多页 TIFF，但需要提供正确的流。以下是适用于两种情况的稳健模式。

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### 为什么使用 `ImageStream.FromFile`？

- 它抽象了底层的 `FileStream`，在内部处理 TIFF 页枚举。  
- 它同样支持 `MemoryStream`，因此可以从数据库或 Web API 加载图像而无需触碰文件系统。

### 边缘情况：超大 TIFF

如果你的 TIFF 超过 200 MB，建议逐页加载以避免内存不足异常：

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## 第五步：验证输出

运行程序后，你应该会看到类似如下的输出：

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

如果文本出现乱码，请再次检查：

1. **分辨率** – OCR 在 300 dpi 或更高时效果最佳。  
2. **EngineMode** – 如果 GPU 驱动过旧，请切换为 `Cpu`。  
3. **License** – 确认许可证文件路径正确且文件可读。

---

## 常见问题 (FAQ)

### 这可以用于其他图像格式吗？

当然可以。`ImageStream.FromFile` 支持 JPEG、PNG、BMP，甚至通过 Aspose.PDF 支持 PDF。只需更换文件扩展名即可。

### 如果需要处理存储在数据库中的图像怎么办？

将 BLOB 读取到 `MemoryStream`，然后传递给 `ImageStream.FromStream(memoryStream)`。OCR 引擎会将其视为基于文件的流。

### 我可以在 Linux 上运行吗？

可以——Aspose OCR 是跨平台的。安装相应的 .NET 运行时，并确保 GPU（如果使用）所需的本机库可用。

---

## 完整可运行示例（复制粘贴即可）

下面是完整的程序代码，已准备好编译。请将 `YOUR_DIRECTORY` 和许可证文件路径替换为实际位置。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

将其保存为 `Program.cs`，运行 `dotnet run`，即可看到文本输出

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}