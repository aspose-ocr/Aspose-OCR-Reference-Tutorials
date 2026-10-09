---
category: general
date: 2026-03-07
description: 使用 C# 从 PNG 文件中提取文本。学习如何将图像转换为文本（C#），并快速读取扫描图像中的文字。
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: zh
og_description: 使用 C# 从 PNG 文件中提取文本。本指南展示了如何使用 C# 将图像转换为文本，以及如何使用 Aspose OCR 从扫描图像中读取文本。
og_title: 在 C# 中从 PNG 提取文本 – 完整 OCR 指南
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 在 C# 中从 PNG 提取文本 – 完整 OCR 指南
url: /zh/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 PNG 中提取文本 – 完整 OCR 指南

是否曾需要 **从 PNG 提取文本**，却不知从何入手？你并不孤单——大多数开发者在第一次面对需要转化为可搜索文本的扫描图形或截图时都会卡住。好消息是，只需几行 C# 代码和 Aspose OCR，你就能瞬间把任意 PNG 转换为可编辑的字符串。

在本教程中，我们将完整演示整个流程：从磁盘定位 PNG、并行启动 OCR 任务、到展示每个结果的整洁预览。结束时，你将掌握 **convert image to text C#** 的实现方式，能够高效 **read text from scanned images**，并了解在不阻塞 UI 线程的情况下 **run OCR on images** 的最佳方法。

## 你需要准备的环境

- .NET 6.0 或更高（代码同样适用于 .NET Core 和 .NET Framework）  
- Aspose.OCR NuGet 包（`Install-Package Aspose.OCR`）  
- 一个包含待处理 *.png* 文件的文件夹  
- 任意你喜欢的 IDE（Visual Studio、VS Code、Rider 等）

无需额外配置；库已自带解码 PNG、JPEG、TIFF 等所需的一切。

## 第一步：定位所有 PNG 文件 – “Extract Text from PNG” 开始

首先必须找到所有准备进行 OCR 的 PNG。使用 `Directory.GetFiles` 既快捷又可靠。

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*为什么重要：* 只扫描一次目录即可让后续流水线保持简洁，且提前检查可以避免后期调试时出现的“无输出”沉默情况。

## 第二步：并行启动 OCR 任务 – 高效 **run OCR on images**

顺序执行 OCR 对少量文件还行，但实际项目常常要处理数十甚至数百张。为每张图片启动一个 `Task`，即可在库进行重计算时让 CPU 保持忙碌。

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*小技巧：* `Task.Run` 会把工作转移到线程池，这意味着你的 UI（如果有的话）保持响应。如果在服务器上，同样的模式可以很好地跨核扩展。

## 第三步：等待所有任务完成 – 收集结果

现在我们等待每个 OCR 操作结束。`Task.WhenAll` 返回的数组顺序与原文件顺序一致，便于将结果与文件名对应。

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*边缘情况说明：* 如果任意单张图片抛异常（文件损坏、不支持的格式），整个 `WhenAll` 会抛出异常。你可以在内部的 `Task.Run` 包裹 try/catch，并在需要容错时返回空字符串或诊断信息。

## 第四步：显示预览 – 验证 **convert image to text C#** 输出

快速预览可以帮助你在将数据持久化之前确认 OCR 是否成功。

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

典型的控制台输出如下：

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

如果预览出现乱码，请检查图像质量或考虑预处理（例如二值化）——但对大多数清晰的 PNG，Aspose OCR 在第一次就能正确识别。

## 可选：将结果保存为 CSV – 实际业务场景

大多数项目需要将提取的文本以结构化格式保存。下面是一个小工具，可将文件名和完整 OCR 文本写入 CSV 文件。

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

现在你可以把 CSV 导入 Excel、Power BI，或任何需要 **read text from scanned images** 的下游系统。

## 常见问题

**如果我的 PNG 很大（超过 5 MB）怎么办？**  
Aspose OCR 会自动对大图进行降采样，以保持内存使用合理；如果需要，你也可以使用 `engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);` 将宽度限制在 2000 像素，同时保持纵横比。

**可以在 Linux 上运行吗？**  
可以。Aspose OCR 是跨平台的，只需确保已安装本机依赖（如某些发行版的 `libgdiplus`）。

**OCR 语言默认是英文吗？**  
是的。如果需要其他语言，在调用 `Recognize()` 前设置 `engine.Language = OcrLanguage.French;`（或任意受支持的枚举）。

**如何处理包含 PNG 的受密码保护的 PDF？**  
先使用 Aspose PDF 或其他库将 PDF 页面转换为图像，然后将生成的 PNG 送入同一流水线。**how to run OCR on images** 的原理保持不变。

## 完整工作示例（Async Main）

下面是一个可直接复制到控制台项目的完整程序。它包含上述所有代码块，并附带一个小助手用于验证输入文件夹。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**预期输出**（两张 PNG 的示例）：

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## 小结

我们已经完整演示了如何使用 C# **extract text from PNG** 文件。从定位文件、并行启动 OCR 任务、预览字符串，到将结果持久化为 CSV——本指南为 **convert image to text C#** 场景提供了可直接投入生产的模式。

如果你准备好进一步探索，可以尝试让同一流水线处理 JPEG 或 TIFF 文件，实验不同的 OCR 语言，或将结果接入搜索索引，以实现即时 **read text from scanned images**。  

对边缘情况、性能调优或授权有疑问？欢迎留言或在 Aspose 社区提问——祝编码愉快！

![提取 PNG 文本示例](extract-text-png.png "使用 Aspose OCR 提取 PNG 文本")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}