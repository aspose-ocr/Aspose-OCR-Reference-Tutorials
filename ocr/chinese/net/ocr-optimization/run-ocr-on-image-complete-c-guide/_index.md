---
category: general
date: 2026-05-28
description: 使用 C# 对图像进行 OCR，快速读取图像中的文字并提取收据文本。了解 GPU 选项和加载技术。
draft: false
keywords:
- run ocr on image
- read text from image
- extract text from receipt
- load image for ocr
language: zh
og_description: 使用 C# 对图像进行 OCR。本教程展示了如何读取图像中的文字、提取收据文本以及优化 GPU 使用。
og_title: 在图像上运行 OCR – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  headline: Run OCR on Image – Complete C# Guide
  type: TechArticle
- description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  name: Run OCR on Image – Complete C# Guide
  steps:
  - name: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
    text: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
  - name: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
    text: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
  - name: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
    text: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
  - name: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
    text: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Computer Vision
title: 在图像上运行 OCR – 完整 C# 指南
url: /zh/net/ocr-optimization/run-ocr-on-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在图像上运行 OCR – 完整 C# 指南

是否曾经需要 **run OCR on image** 文件，却不知从何入手？你并不孤单；许多开发者在首次尝试从图像数据读取文本时都会遇到这个难题。好消息是，只需几行 C# 代码，你就可以从收据扫描件、PDF 或任何图片中提取文本。在本指南中，我们将演示一个完整、可直接运行的示例，展示如何 **load image for OCR**、利用 GPU 加速，并安全地限制内存使用。

阅读完本教程后，你将能够：

* 在 C# 中初始化 OCR 引擎  
* **Load image for OCR** 从磁盘或流中加载图像  
* 使用可选的 GPU 支持 **Read text from image**  
* **Extract text from receipt** 并将结果输出到控制台  

无需外部服务——只需本地库和一张示例收据图片。

---

## 你需要的准备

| 前置条件 | 原因 |
|--------------|--------|
| .NET 6.0 SDK 或更高版本 | 现代运行时，支持最新语言特性 |
| 提供 `OcrEngine` 类的 OCR 库（例如 IronOCR、Tesseract .NET 包装器） | 提供下文使用的 `Configuration` 和 `Recognize` 方法 |
| 支持 CUDA 的 GPU（可选） | 启用 `EnableGpu` 标志以加速处理 |
| 示例收据图片（`receipt.jpg`） | 演示 **extract text from receipt** 步骤 |
| 任意 C# IDE（Visual Studio、Rider、VS Code） | 用于快速编译和调试 |

如果没有 GPU，代码会自动回退到 CPU 模式——无需担心。

---

![在图像上运行 OCR 示例输出](https://example.com/ocr-output.png "在图像上运行 OCR – 示例控制台输出")

*Alt text: 在图像上运行 OCR 示例输出，显示识别后的收据文本。*

---

## 步骤 1：Run OCR on Image – 设置引擎

首先：创建 OCR 引擎的实例。该对象是整个流程的核心，保存所有配置细节并执行繁重的识别工作。

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

*为什么重要：* `OcrEngine` 类封装了底层 OCR 引擎（Tesseract、IronOCR 等）。一次实例化后在多张图片间复用，可降低开销并提供统一的设置入口。

---

## 步骤 2：Load Image for OCR

在引擎能够读取之前，需要向它提供图像。库的 `Image` 属性接受流或文件路径，具体取决于实现。

```csharp
// Step 2: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

*提示：* 若处理用户上传的文件，请将此代码包裹在 `try/catch` 中并先验证文件类型。不支持的格式会抛出异常，可进行优雅处理。

---

## 步骤 3：启用 GPU 加速（可选）

如果机器上装有兼容的 CUDA 或 OpenCL 运行时，开启 GPU 模式可以为每次识别节省数秒。

```csharp
// Step 3: Enable GPU acceleration (requires CUDA/OpenCL runtime)
ocrEngine.Configuration.EnableGpu = true;
```

*专业提示：* 并非所有 GPU 都表现相同。老旧显卡可能因驱动开销导致轻微变慢。请同时测试 `EnableGpu = true/false` 两种路径，找出最适合你硬件的方案。

---

## 步骤 4：限制 GPU 内存使用（可选）

有时你不希望 OCR 进程占用全部 GPU 内存，尤其在与深度学习推理等其他工作共享 GPU 时。

```csharp
// Step 4: (Optional) Limit the amount of GPU memory the engine can use (in MB)
ocrEngine.Configuration.GpuMemoryLimit = 1024; // 1 GB limit
```

*使用时机：* 若运行的 Web 服务需要并发处理大量图片，设定内存上限可防止因内存耗尽导致的崩溃。

---

## 步骤 5：Recognize Text and Read Text from Image

现在引擎已准备就绪。调用 `Recognize()` 会运行 OCR 流程并返回提取的字符串。

```csharp
// Step 5: Perform OCR and retrieve the recognized text
string recognizedText = ocrEngine.Recognize();
```

*为何是核心：* 这行代码内部隐藏了一系列预处理（二值化、去倾斜）以及字符分类。返回的 `recognizedText` 为普通 Unicode 文本，可直接用于后续处理。

---

## 步骤 6：Extract Text from Receipt – 输出

最后，将结果写入控制台或存储到需要的位置。对于收据，你后续可能会解析商品行、总计或日期等信息。

```csharp
// Step 6: Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

**预期的控制台输出（为简洁起见已截断）：**

```
=== OCR Result ===
Store Name
123 Main St.
Date: 04/27/2026
Item   Qty   Price
Apple   2    1.20
Bread   1    2.50
Total          3.70
Thank you!
```

如果 OCR 在特定收据布局上表现不佳，可考虑调整预处理选项（例如 `ocrEngine.Configuration.Deskew = true`）或使用更高分辨率的图像。

---

## 常见边缘情况及处理办法

| 情况 | 建议解决方案 |
|-----------|----------------|
| **空图像** – `ocrEngine.Image` 为 `null` | 在赋值前验证文件路径；若缺失抛出明确的 `ArgumentException`。 |
| **GPU 不可用** – `EnableGpu = true` 抛出 `PlatformNotSupportedException` | 将 GPU 启用代码放入 `try/catch`，在捕获异常后回退到 CPU 模式。 |
| **大尺寸收据（> 10 MB）** 导致内存压力 | 使用 `GpuMemoryLimit` 或将图像分块处理（`ocrEngine.Configuration.TileSize`）。 |
| **语言检测错误** – 输出乱码 | 设置 `ocrEngine.Configuration.Language = "eng"`（或相应的 ISO 代码）以强制使用英文。 |

---

## 生产环境 OCR 的专业建议

1. **批处理**：对一批图像复用同一个 `OcrEngine` 实例；它会缓存语言模型并降低延迟。  
2. **预过滤**：在将图像交给引擎前进行简单的灰度转换和对比度提升——许多库提供 `Preprocess` 方法。  
3. **错误日志**：在每次 `Recognize()` 调用后捕获 `ocrEngine.LastError`（若可用），以便在不崩溃服务的情况下诊断失败原因。  
4. **线程安全**：大多数 OCR 引擎 **不是** 线程安全的。如果需要并行处理，请为每个线程创建独立的引擎实例或使用并发队列。

---

## 结论

我们已经完整演示了在 C# 中 **run OCR on image** 的工作流。从创建引擎、**load image for OCR**、切换 GPU 加速，到最终 **extract text from receipt**，你现在拥有了构建更复杂文档处理流水线的坚实基础。

后续可以考虑：

* 将收据文本解析为结构化的 JSON（使用正则或自然语言库）——适用于 **read text from image** 自动化。  
* 将 OCR 步骤集成到 ASP .NET Core API 中，让用户通过 HTTP 上传收据。  
* 试验不同的 OCR 后端（Tesseract 与商业 SDK）以比较准确率。

尝试使用不同的收据布局，调节配置，你会惊讶于将模糊照片转化为可操作数据的速度。祝编码愉快，愿你的图像始终清晰！

## 相关教程

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}