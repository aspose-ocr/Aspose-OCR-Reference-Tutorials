---
category: general
date: 2026-04-03
description: 使用 Aspose OCR 在 C# 中提取图像文本。学习如何转换扫描图像、在 C# 中加载图像文件，以及异步识别 TIF 文本。
draft: false
keywords:
- extract text from image
- convert scanned image
- how to ocr image
- load image file c#
- recognize text from tif
language: zh
og_description: 使用 Aspose OCR 在 C# 中从图像提取文本。本指南展示了如何转换扫描图像、加载图像文件（C#），以及使用异步调用从 TIF
  识别文本。
og_title: 在 C# 中从图像提取文字 – 异步 OCR 教程
tags:
- OCR
- C#
- Aspose
- Async
title: 在 C# 中从图像提取文本 – 异步 OCR 教程
url: /zh/net/text-recognition/extract-text-from-image-in-c-async-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中从图像提取文本 – 异步 OCR 教程

需要快速**从图像提取文本**吗？使用 Aspose OCR，您可以在 C# 中通过异步调用完成此操作，整个过程在您喝完咖啡之前就已结束。  
如果您还想了解如何**转换扫描图像**文件或在 C# 中加载图像文件而毫不费力，那么您来对地方了。

在本指南中，我们将逐步演示每一步——从磁盘读取 TIF 到获取干净、可搜索的文本。完成后，您将能够**从 TIF 识别文本**，了解加载不同图像格式的细节，并拥有一个可在任何 .NET 项目中复用的可靠异步模式。

## 您将学习

* 如何为异步使用设置 Aspose OCR 引擎。  
* 加载图像文件的**C#**代码示例，包括对缺失文件的错误处理。  
* 将**扫描图像**PDF 或 TIFF 转换为 Aspose 可读取的位图的方法。  
* 为什么 async OCR（`RecognizeAsync`）比同步方式更快、更具可扩展性。  
* 预期的控制台输出以及如何验证提取的文本与源文件匹配。

> **专业提示：** 如果您一次处理数十页，请保持 OCR 引擎在多次调用之间存活——每次创建新实例会带来不必要的开销。

---

## 异步提取图像文本

解决方案的核心位于一个 async `Main` 方法中。使用 `await` 可以让 UI 线程保持空闲（在控制台应用中则释放线程池），而 OCR 引擎完成繁重的工作。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.Threading.Tasks;

class AsyncDemo
{
    static async Task Main()
    {
        // 1️⃣ Create an instance of the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        Image inputImage = Image.FromFile(@"YOUR_DIRECTORY/input.tif");

        // 3️⃣ Run asynchronous OCR recognition (returns a Task<string>)
        string recognizedText = await ocrEngine.RecognizeAsync(inputImage);

        // 4️⃣ Display the OCR result
        Console.WriteLine("Async OCR result:");
        Console.WriteLine(recognizedText);
    }
}
```

**为什么使用 async？** OCR 操作可能涉及网络 I/O（如果引擎使用云服务）或密集的 CPU 计算。`RecognizeAsync` 释放调用线程，使其他工作——例如处理更多文件——能够继续进行。

### 预期输出

```
Async OCR result:
The quick brown fox jumps over the lazy dog.
```

如果图像包含多行，每行将通过换行符分隔。如果需要持久化存储，可以使用 `File.WriteAllText("output.txt", recognizedText);` 将结果写入文件。

---

## 将扫描图像转换为可用格式

有时您会收到扫描的 PDF 或多页 TIFF。Aspose OCR 最适合处理 `System.Drawing.Image`，因此可能需要先进行转换。

```csharp
using Aspose.OCR;
using System.Drawing;
using System.Drawing.Imaging;

// Load a multi‑page TIFF and pick the first frame
Image tiff = Image.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
tiff.SelectActiveFrame(FrameDimension.Page, 0); // Grab page 0

// Optionally, change DPI for better accuracy
var bitmap = new Bitmap(tiff);
bitmap.SetResolution(300, 300); // 300 DPI is a sweet spot for OCR
```

> **为什么要更改 DPI？** 更高的分辨率为 OCR 引擎提供更多细节，减少模糊扫描的误识别。只需避免超过 600 DPI——大多数引擎在此之后不会提升准确度，却会占用更多内存。

---

## 加载图像文件 C# – 处理不同格式

您可能会倾向于硬编码 `.tif` 路径，但一个健壮的工具应接受**任何**图像类型（`.png`、`.jpg`、`.bmp`）。下面是一个简短的帮助类，用于抽象加载逻辑：

```csharp
static Image LoadImage(string path)
{
    if (!File.Exists(path))
        throw new FileNotFoundException($"Image not found: {path}");

    // Let .NET decide the correct decoder based on file header
    using (var stream = File.OpenRead(path))
    {
        return Image.FromStream(stream);
    }
}
```

使用方式如下：

```csharp
Image img = LoadImage(@"YOUR_DIRECTORY/input.tif");
string text = await ocrEngine.RecognizeAsync(img);
```

现在，您已经覆盖了**加载图像文件 C#**的场景，而无需担心具体的扩展名。

---

## 从 TIF 识别文本 – 您需要了解的内容

TIF 文件常包含多页或使用某些压缩方式，导致部分库无法正确解析。以下两点可帮助您获得可靠的结果：

1. **选择正确的帧**——如前文使用 `SelectActiveFrame` 所示。  
2. **标准化颜色**——转换为 24 位 RGB 位图可以消除异常调色板。

```csharp
static Image PrepareTif(string tifPath, int pageIndex = 0)
{
    Image tif = Image.FromFile(tifPath);
    tif.SelectActiveFrame(FrameDimension.Page, pageIndex);
    // Convert to 24‑bit RGB to avoid palette issues
    Bitmap rgb = new Bitmap(tif.Width, tif.Height, PixelFormat.Format24bppRgb);
    using (Graphics g = Graphics.FromImage(rgb))
    {
        g.DrawImage(tif, 0, 0, tif.Width, tif.Height);
    }
    return rgb;
}
```

将返回的 `Image` 直接传入 `RecognizeAsync`，即使源文件使用 CCITT Group 4 压缩，您也能可靠地**从 TIF 识别文本**。

---

## 完整端到端示例

将所有内容组合在一起，即可得到一个可直接放入控制台项目并运行的单文件示例。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        try
        {
            // Step 1 – Initialize OCR engine (reuse if processing many files)
            OcrEngine ocrEngine = new OcrEngine();

            // Step 2 – Load and prepare the image (handles TIF, PNG, JPG, etc.)
            Image img = PrepareImage(@"YOUR_DIRECTORY/input.tif");

            // Step 3 – Run async recognition
            string result = await ocrEngine.RecognizeAsync(img);

            // Step 4 – Output the result
            Console.WriteLine("Async OCR result:");
            Console.WriteLine(result);

            // Optional: Save to a text file
            File.WriteAllText("ocr-output.txt", result);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // Helper that decides how to load based on extension
    static Image PrepareImage(string path)
    {
        string ext = Path.GetExtension(path).ToLowerInvariant();
        return ext switch
        {
            ".tif" or ".tiff" => PrepareTif(path),
            _ => LoadImage(path)
        };
    }

    static Image LoadImage(string path)
    {
        if (!File.Exists(path))
            throw new FileNotFoundException($"Image not found: {path}");

        using var stream = File.OpenRead(path);
        return Image.FromStream(stream);
    }

    static Image PrepareTif(string tifPath, int page = 0)
    {
        Image tif = Image.FromFile(tifPath);
        tif.SelectActiveFrame(FrameDimension.Page, page);
        Bitmap rgb = new Bitmap(tif.Width, tif.Height, PixelFormat.Format24bppRgb);
        using var g = Graphics.FromImage(rgb);
        g.DrawImage(tif, 0, 0, tif.Width, tif.Height);
        return rgb;
    }
}
```

**您应该看到的结果：** 控制台打印提取的文本，同时在可执行文件旁生成名为 `ocr-output.txt` 的文件，内容与控制台输出相同。

---

## 常见问题与边缘情况

| Question | Answer |
|----------|--------|
| *Can I OCR a PDF directly?* | Aspose OCR 只能处理图像，因此您需要先将每页 PDF 转换为图像（例如使用 Aspose.PDF 或 `PdfRenderer`）。 |
| *What if the image is huge?* | 在 OCR 前将宽高最大限制为 2500 px；Aspose 会在内部自动调整大小，但您可以节省内存。 |
| *Is the async method thread‑safe?* | 是的，但仅在不并发调用 `RecognizeAsync` 时复用同一 `OcrEngine` 实例。并行处理时请为每个任务创建独立的引擎。 |
| *Do I need a license?* | Aspose OCR 提供带水印的免费评估版。生产环境请购买许可证，并通过 `License license = new License(); license.SetLicense("Aspose.OCR.lic");` 进行设置。 |

---

## 结论

您现在已经掌握了使用 Aspose OCR 异步 API 在 C# 中**从图像提取文本**的方法。通过处理图像加载、可选的扫描图像转换以及 TIF 文件的特殊情况，这一方案既稳健又适合投入生产。

接下来您可以：

* **转换扫描图像** PDF 为 PNG 再进行 OCR，以提升准确度。  
* 探索**如何直接对图像流进行 OCR**，从 Web API 直接读取，省去临时文件。  
* 在 `Parallel.ForEach` 循环中复用 `OcrEngine` 实例，批量处理数十个文件。  

尝试这些变体，您会快速体会到异步 OCR 对文档密集型应用的颠覆性优势。祝编码愉快，如有问题欢迎留言交流！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}