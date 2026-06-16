---
category: general
date: 2026-02-22
description: 使用 Aspose OCR 生成可搜索的 PDF 并从图像中提取文本。学习如何将图像转换为 PDF 并在单个教程中输出纯文本。
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: zh
og_description: 使用 Aspose OCR 将扫描图像生成可搜索的 PDF。本指南展示了如何从图像中提取文本、输出纯文本以及将图像转换为 PDF。
og_title: 从图像生成可搜索的 PDF – 完整 C# 教程
tags:
- C#
- OCR
- PDF generation
- Aspose
title: 使用 C# 从图像生成可搜索 PDF – 步骤指南
url: /zh/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中从图像生成可搜索 PDF – 完整教程

是否曾需要 **从扫描图片生成可搜索 PDF**，却不知从何入手？你并不孤单——大多数开发者在第一次接触 OCR 时都会遇到这个难题。好消息是，使用 Aspose OCR 只需几行 C# 代码，就能 **从图像中提取文本**、**输出纯文本**，以及 **将图像转换为 PDF**。

本指南将完整演示从加载 PNG 文件到保存可搜索 PDF 与纯文本文件的全过程。阅读完毕后，你将拥有一段可在任何 .NET 项目中直接使用的代码片段。没有冗余，只提供真正能完成任务的内容。

## 你将学到

- 如何在 .NET 控制台应用中设置 **Aspose.OCR**。  
- **输出纯文本** 与 **可搜索 PDF** 两种模式的区别。  
- 如何 **从图像中提取文本** 并写入 `.txt` 文件。  
- 如何 **将图像转换为 PDF**，在保留原始位图的同时添加隐藏的文本层。  
- 处理大批量文件的技巧、常见陷阱，以及提升识别准确度的设置位置。

> **先决条件** – 需要 .NET 6+（或 .NET Framework 4.7+）、Visual Studio 2022（或任意编辑器）以及 Aspose OCR 许可证（或免费试用版）。不需要其他第三方库。

![generate searchable pdf example](image-placeholder.png "生成的可搜索 PDF 示例")

## 步骤 1：安装 Aspose OCR 并创建引擎

首先——将 NuGet 包添加到项目中：

```bash
dotnet add package Aspose.OCR
```

现在我们可以实例化 OCR 引擎，并指定要识别的语言。默认是英文，你可以通过修改 `Language` 枚举切换到法语、西班牙语等。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**为什么重要：** 引擎保存所有配置——语言、输出格式以及可选的预处理标志。一次性设置并复用可以避免为每个文件创建新实例的开销。

## 步骤 2：提取文本并保存为纯文本

如果只需要原始字符，将引擎切换为 `OutputFormat.Text`。这会让 Aspose OCR 完全跳过 PDF 生成，直接返回字符串。

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**小技巧：** `plainTextResult.Text` 已经去除了 OCR 布局中的换行。如果需要保留原始间距，请改用 `plainTextResult.TextBlocks`。

### 预期结果

打开 `output.txt`，你应该看到类似如下内容：

```
Hello, world!
This is a sample scanned document.
```

这就是本教程的 **输出纯文本** 部分——快速、轻量，且非常适合后续处理（例如建立索引）。

## 步骤 3：切换到可搜索 PDF 模式

接下来创建 **可搜索 PDF**。引擎会嵌入原始位图，并在其下层叠加 OCR 生成的文本，使文档在任何 PDF 查看器中均可搜索。

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**为什么要重新识别：** OCR 引擎会缓存最近一次识别的图像，但输出格式决定返回的数据类型。切换格式会强制进行一次全新的识别，以生成隐藏的文本层。

### PDF 的显示效果

在 Adobe Reader 或任意阅读器中打开 `output.pdf`，尝试选取文本。你会发现可以复制、搜索、甚至高亮显示内容——尽管视觉上仍是原始位图。这正是 **将扫描图像转换为 PDF** 的核心特性。

## 步骤 4：处理多个文件（可选）

实际项目很少只处理单张图片。下面的循环示例会遍历文件夹中的所有 PNG，生成对应的 `.txt` 与 `.pdf` 文件。

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**边缘情况说明：** 大尺寸图像可能导致内存耗尽。如果出现 `OutOfMemoryException`，可以在识别前使用 `Image.Resize` 降低分辨率，或将文件分批处理。

## 步骤 5：微调 OCR 准确度

Aspose OCR 提供了若干可调参数：

| 设置 | 功能说明 | 适用场景 |
|------|----------|----------|
| `ocrEngine.PageSegmentationMode` | 控制引擎如何将图像划分为文本块。 | 多列布局的文档。 |
| `ocrEngine.Deskew` | 自动纠正轻微倾斜的页面。 | 未完全对齐的扫描件。 |
| `ocrEngine.RemoveNoise` | 尝试清除噪点和背景杂质。 | 低质量扫描或传真页。 |

示例：

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

开启这些选项可能会增加处理时间，但在 **从图像中提取文本** 的质量提升上往往值得。

## 步骤 6：以编程方式验证输出

有时需要断言 PDF 实际包含可搜索文本（例如在自动化测试中）。最简单的检查是验证 PDF 字节数组非空且 `RawData` 长度大于图像大小。

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

若需更深入的验证，可使用 PDF 库（如 iTextSharp）提取文本流，并与 `plainTextResult.Text` 进行比对。

## 常见陷阱与规避方法

- **缺少许可证** – 未提供有效的 Aspose 许可证时，库会以评估模式运行，在 PDF 上添加水印。请尽早注册许可证 (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`)。  
- **路径错误** – 硬编码绝对路径只能在本机运行，迁移后会失效。使用 `Path.Combine` 与 `AppDomain.CurrentDomain.BaseDirectory` 组合路径以提升可移植性。  
- **不支持的图像格式** – GIF 与多页 TIFF 需要特殊处理 (`Image.LoadMultiPage`)。如果只需第一页，请先转换为 PNG/JPEG。  
- **性能瓶颈** – 在循环中反复创建 `OcrEngine` 开销很大。保持单实例并仅在需要时切换 `OutputFormat`，如前文所示。

## 小结

我们已经完整演示了使用 Aspose OCR **从扫描图像生成可搜索 PDF** 的全部流程：

1. 安装 NuGet 包并创建 `OcrEngine`。  
2. 将 `OutputFormat.Text` 设置为 **输出纯文本**，并写入 `.txt` 文件。  
3. 切换到 `OutputFormat.SearchablePdf`，实现 **将图像转换为 PDF** 并嵌入隐藏文本层。  
4. 保存 PDF 字节，必要时对目录进行批量处理。  
5. 通过去倾斜、去噪和页面分割等选项微调识别准确度。  

以上代码简洁自包含，直接复制粘贴到 Visual Studio 即可使用。

## 接下来可以尝试什么？

- **批量处理** 并配合 UI 前端（WinForms 或 WPF），实现文件拖拽。  
- **语言检测** – Aspose OCR 支持自动语言识别；尝试 `ocrEngine.Language = Language.AutoDetect`。  
- **后处理** – 将提取的文本导入搜索索引（ElasticSearch、Azure Cognitive Search），实现即时文档检索。  
- **其他输出格式** – 使用 `OutputFormat.Hocr` 获取基于 HTML 的 OCR 结果，适合网页预览。

欢迎尝试不同的分辨率、颜色模式和 OCR 设置。玩得越多，你对速度与准确度之间的权衡就会越了解。

---

**祝编码愉快！** 如遇任何问题，欢迎在下方留言或查阅 Aspose OCR 文档获取更深入的内容。无论是发票、档案归档，还是构建可搜索的知识库，下一个项目都将变得轻而易举。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}