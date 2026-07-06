---
category: general
date: 2026-03-23
description: 使用 Aspose OCR 将图像生成可搜索的 PDF。了解如何将 TIFF 转换为高压缩率的 PDF，并在几分钟内识别图像文字。
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- high compression pdf
- recognize image text
- searchable pdf from image
language: zh
og_description: 使用 Aspose OCR 将图像创建可搜索的 PDF。本教程展示了如何将 TIFF 转换为 PDF，添加可搜索的文本层，并应用高压缩。
og_title: 从图像创建可搜索 PDF – 完整 C# 指南
tags:
- Aspose OCR
- C#
- PDF generation
title: 从图像创建可搜索的 PDF – 完整 C# 指南
url: /zh/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像创建可搜索 PDF – 完整 C# 指南

是否曾需要 **创建可搜索 pdf**，但不知道从何入手？你并不孤单——许多开发者在将 TIFF 扫描件转换为可搜索 PDF 时都会遇到同样的难题。好消息是，使用 Aspose OCR 你可以 **convert tiff to pdf**，在其上添加隐藏的文本层，并通过 **high compression pdf** 选项进一步压缩文件大小，全部只需几行 C# 代码。

在本教程中，我们将完整演示整个过程：从安装所需的 NuGet 包、加载 TIFF 图像、识别其文本，到最终导出可搜索 PDF。完成后，你将拥有一个可运行的控制台应用程序，能够 **recognize image text** 并生成体积小、可搜索的 PDF，准备好进行索引。无需额外工具，无需手动 OCR 步骤——只需干净的代码和一点说明。

## 前置条件 & 你需要的东西

- **.NET 6+**（或 .NET Framework 4.6+）。API 在两者上均可运行，但 .NET 6 提供最新的运行时改进。  
- **Visual Studio 2022** 或你喜欢的任何 IDE。  
- **Aspose.OCR** 与 **Aspose.OCR.Gpu** NuGet 包（GPU 包为可选，但在支持的硬件上可加速识别）。  
- 一个示例 TIFF 文件（例如 `invoice.tif`），放置在你可控制的文件夹中。  

如果你已经拥有这些项目，太好了——直接跳到下一步。如果没有，下面的安装步骤会涵盖全部内容。

## 第 1 步：安装 Aspose OCR 包

首先，在终端中打开项目文件夹并运行：

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

这些命令会同时拉取核心 OCR 引擎和 GPU 加速库。后者并非强制；如果找不到兼容的 GPU，引擎会回退到 CPU 模式。  

> **专业提示：** 在面向生产环境时，请在 `csproj` 中锁定包版本，以避免意外的破坏性更改。

## 第 2 步：搭建项目骨架

创建一个新的控制台应用（如果还没有的话）：

```bash
dotnet new console -n PdfExportDemo
cd PdfExportDemo
```

将自动生成的 `Program.cs` 替换为后面完整示例中的代码。程序将会：

1. 使用 GPU 支持初始化 `OcrEngine`。  
2. 加载 TIFF 图像。  
3. 运行 OCR 并在失败时优雅退出。  
4. 为可搜索层和 **high compression** 配置 **PdfExportOptions**。  
5. 写入输出文件。

## 第 3 步：编写完整代码（完整示例）

下面是 *全部* 源文件。复制粘贴到 `Program.cs` 中。注释解释了每行代码背后的 “为什么”，而不仅仅是 “做什么”。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;

class PdfExport
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Initialise OCR engine with GPU acceleration.
        //    GpuMode.Enabled tells Aspose to use the GPU if one is present.
        //    If no compatible GPU exists, the engine automatically falls back
        //    to CPU mode—no extra code required.
        // ------------------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine(GpuMode.Enabled))
        {
            // ------------------------------------------------------------
            // 2️⃣ Load the source image.
            //    ImageStream.FromFile supports many formats; here we use TIFF.
            // ------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\invoice.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // ------------------------------------------------------------
            // 3️⃣ Perform OCR recognition.
            //    Recognize() returns false if the engine cannot read the image.
            //    Exiting early prevents us from creating an empty PDF.
            // ------------------------------------------------------------
            if (!ocrEngine.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return;
            }

            // ------------------------------------------------------------
            // 4️⃣ Configure PDF export options.
            //    IncludeTextLayer = true adds an invisible, searchable text layer.
            //    CompressionLevel = High reduces file size dramatically.
            // ------------------------------------------------------------
            PdfExportOptions pdfExportOptions = new PdfExportOptions
            {
                IncludeTextLayer = true,
                CompressionLevel = PdfCompression.High
            };

            // ------------------------------------------------------------
            // 5️⃣ Save the searchable PDF.
            //    The output will be a compact, searchable PDF ready for indexing.
            // ------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\invoice.pdf";
            ocrEngine.Save(outputPath, pdfExportOptions);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### 为什么这样可行

- **GPU 加速** 能将识别时间从秒级降至毫秒级——在批量处理时非常有用。  
- **IncludeTextLayer** 将 OCR 生成的文本以不可见方式嵌入，允许 PDF 查看器在不改变视觉外观的前提下搜索文档。  
- **High compression** 对图像流使用 Flate（ZIP）压缩，虽为无损但能显著缩小文件体积——非常适合归档成千上万张发票。

## 第 4 步：运行应用并验证输出

在项目文件夹内打开终端并执行：

```bash
dotnet run
```

如果一切配置正确，你会看到：

```
Searchable PDF saved to: YOUR_DIRECTORY\invoice.pdf
```

在任意 PDF 阅读器（Adobe Acrobat、Edge 或浏览器）中打开 `invoice.pdf`。尝试搜索原始 TIFF 中出现的词，例如 “Total”。即使该词位于图像中，查看器也应能高亮显示。这正是 **searchable pdf** 的标志。

### 预期文件大小

一张典型的扫描发票（≈300 KB TIFF）在使用 `PdfCompression.High` 后通常会压缩至 **约 80 KB**。具体大小取决于图像复杂度，但你会明显看到体积下降。

## 第 5 步：常见变体 & 边缘情况

| 情形 | 需要调整的地方 | 原因 |
|-----------|----------------|-----|
| **没有 GPU 可用** | 将 `new OcrEngine(GpuMode.Enabled)` 改为 `new OcrEngine(GpuMode.Disabled)` | 防止引擎尝试 GPU 初始化，从而避免短暂的延迟。 |
| **多页（多页 TIFF）** | 设置 `ocrEngine.Image = ImageStream.FromFile("multi.tif", PageRange.All);` | 加载所有帧；Aspose 会逐页处理并生成多页 PDF。 |
| **需要非英文 OCR 语言** | `ocrEngine.Language = Language.French;`（或任意受支持语言） | 提升非英文文档的识别准确率。 |
| **想要可见的文本覆盖层而非隐藏层** | `pdfExportOptions.IncludeTextLayer = false;` 并手动添加 `TextFragment` 对象。 | 当你希望 OCR 文本以可选中形式显示在图像上方时使用。 |
| **极致小体积 PDF** | 将 `PdfCompression.High` 与 `ImageResolution = 150` DPI 结合使用，放在识别前。 | 降低 DPI 减少图像数据，进一步压缩 PDF，代价是视觉清晰度下降。 |

> **注意：** 在大规模部署前，请先在小样本上测试边缘情况。OCR 准确度会受图像质量、噪声和语言等因素影响。

## 第 6 步：生产环境实现技巧

1. **错误日志** – 用正式的日志框架（Serilog、NLog）替换 `Console.WriteLine`，便于诊断。  
2. **批量处理** – 将核心逻辑封装为接受输入/输出路径的方法，然后遍历目录中的 TIFF 文件。  
3. **异步 I/O** – 虽然 Aspose OCR 本身是同步的，但文件的加载与保存可以使用异步方式，以保持 UI 线程响应。  
4. **安全性** – 若通过 Web API 暴露此功能，请验证文件路径并限制文件大小，以防滥用。  
5. **版本锁定** – 使用确切的版本号（`<PackageReference Include="Aspose.OCR" Version="23.12.0" />`）确保不同构建之间行为一致。

## 结论

我们刚刚构建了一个 **完整的端到端解决方案**，能够 **create searchable pdf**，**convert tiff to pdf**，并通过 **high compression pdf** 设置在 **recognize image text** 时保持高准确率。生成的 **searchable pdf from image** 轻量、可搜索，适用于后续的索引、归档或电子取证等工作流。

有一批发票要处理？把方法放进循环，指向文件夹，让 Aspose OCR 完成繁重工作。想尝试不同的压缩级别或语言包？代码足够模块化，几秒钟即可切换选项。

---

*准备好升级了吗？* 试着添加水印、嵌入元数据，甚至将多个 OCR 处理后的 PDF 合并。Aspose 系列提供了众多扩展——探索文档，保持动力。祝编码愉快！

![从图像创建可搜索 PDF 示例截图](https://example.com/images/create-searchable-pdf.png "创建可搜索 PDF 示例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}