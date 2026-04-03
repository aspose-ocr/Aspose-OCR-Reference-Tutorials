---
category: general
date: 2026-04-03
description: 使用 Aspose OCR 在 C# 中识别图像文本。学习加载图像进行 OCR、从图像提取文本、在 C# 中写入 JSON 文件，以及对
  PNG 执行 OCR。
draft: false
keywords:
- recognize text from image
- write json file c#
- load image for ocr
- extract text from image
- perform ocr on png
language: zh
og_description: 使用 Aspose OCR 在 C# 中识别图像文本。一步步指南：加载图像进行 OCR、从图像中提取文本、使用 C# 写入 JSON
  文件，以及对 PNG 执行 OCR。
og_title: 在 C# 中识别图像文字 – 完整的 Aspose OCR 教程
tags:
- OCR
- C#
- Aspose
title: 在 C# 中从图像识别文本 – 完整 Aspose OCR 指南
url: /zh/net/text-recognition/recognize-text-from-image-in-c-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中识别图像文字 – 完整的 Aspose OCR 教程

是否曾经需要**识别图像文字**但不确定该选哪个库？也许你有一批扫描的收据、一张 PNG 截图，或是一张手写笔记，想把它们转换为可搜索的数据。好消息是：使用 Aspose.OCR 只需几行 C# 代码，就能完成，而且还能得到一个整洁的 JSON 文件，方便导入其他系统。

在本教程中，我们将逐步演示如何加载图像进行 OCR、从图像中提取文字、将结果序列化为 JSON 文件，最后轻松处理 PNG 文件。完成后，你将拥有一个可直接运行的控制台应用程序，能够**识别图像文字**并将输出写入 *output.json*。

## 你需要的环境

- .NET 6.0 或更高（代码同样适用于 .NET Framework）
- Aspose.OCR NuGet 包 (`Install-Package Aspose.OCR`)
- 需要处理的 PNG（或任何受支持的格式）文件
- Visual Studio、VS Code 或你喜欢的任何 C# 编辑器

无需额外的第三方库——只需 Aspose OCR 引擎和内置的 `System.Text.Json` 序列化器。

## 步骤 1：使用 Aspose OCR 识别图像文字

首先需要创建一个 `OcrEngine` 实例。该对象在后台完成繁重的工作。

```csharp
using Aspose.OCR;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this is where the magic starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image for OCR – replace the path with your own file.
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/input.png");

        // Perform OCR on the loaded image and get a structured result.
        OcrResult ocrResult = ocrEngine.RecognizeToResult(sourceImage);

        // Serialize the result into a nicely indented JSON string.
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // Write JSON file C# – this will create output.json next to your exe.
        File.WriteAllText(@"YOUR_DIRECTORY/output.json", json);
    }
}
```

**为什么重要：**一次实例化 `OcrEngine` 并重复使用，比为每个文件创建新引擎更高效。`RecognizeToResult` 调用返回的 `OcrResult` 对象已经包含提取的文字、置信度分数和边界框——非常适合后续处理。

## 步骤 2：加载图像进行 OCR – 处理不同格式

Aspose OCR 能读取 PNG、JPEG、BMP 以及许多其他格式。如果处理的 PNG 包含透明通道，建议先将其展平，以避免出现意外的空白。

```csharp
// Optional: flatten PNG with transparency to a white background.
if (sourceImage.RawFormat.Equals(System.Drawing.Imaging.ImageFormat.Png))
{
    Bitmap flat = new Bitmap(sourceImage.Width, sourceImage.Height);
    using (Graphics g = Graphics.FromImage(flat))
    {
        g.Clear(Color.White);
        g.DrawImage(sourceImage, 0, 0);
    }
    sourceImage = flat;
}
```

**技巧提示：**始终检查图像尺寸是否合理（例如，宽度 > 50 px）。尺寸过小的图像可能导致 OCR 引擎漏字符，从而产生低置信度分数。

## 步骤 3：在 C# 中写入 JSON 文件 – 让输出易于使用

`System.Text.Json` 序列化器速度快且内置，但如果需要自定义转换器，也可以换成 `Newtonsoft.Json`。上面的示例已经使用 `WriteIndented = true`，因此生成的文件易于阅读。

```csharp
// Expected output (truncated):
{
  "Text": "Hello World",
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello World",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 120, "Height": 30 }
        }
      ]
    }
  ]
}
```

将 OCR 数据保存为 JSON 可轻松导入数据库、通过 HTTP 发送，或供机器学习流水线使用。

## 步骤 4：验证结果 – 快速检查

程序运行后，打开 `output.json` 并查找 `"Text"` 字段。如果其中包含预期的字符串，说明你已经成功**提取图像文字**。如果置信度较低，可考虑对图像进行预处理（例如，提高对比度或应用二值化阈值）。

```csharp
Console.WriteLine($"Extracted text: {ocrResult.Text}");
Console.WriteLine($"Overall confidence: {ocrResult.Confidence:P2}");
```

运行控制台程序会输出类似如下内容：

```
Extracted text: Hello World
Overall confidence: 98.00%
```

这表明 OCR 按预期工作，结果可靠。

## 常见陷阱与边缘情况

| Issue | Why it Happens | How to Fix |
|-------|----------------|------------|
| **空白输出** | 图像过暗或使用了不受支持的颜色空间 | 转换为灰度图、提升亮度，或展平 PNG（参见步骤 2） |
| **乱码字符** | DPI 过低（< 72）或噪声过多 | 放大图像或在传递给 `RecognizeToResult` 前使用去噪滤波器 |
| **大文件导致内存压力** | 将多兆像素的 PNG 加载到 `Bitmap` 中会消耗大量内存 | 分块处理图像或在保持可读性的前提下降低分辨率 |
| **JSON 序列化错误** | `OcrResult` 包含循环引用（可能性小） | 使用 `JsonSerializerOptions { ReferenceHandler = ReferenceHandler.IgnoreCycles }` |

## 进阶：在批处理循环中对 PNG 执行 OCR

如果你有一个包含大量 PNG 文件的文件夹，可以扩展示例代码，对它们进行遍历处理：

```csharp
string[] pngFiles = Directory.GetFiles(@"YOUR_DIRECTORY", "*.png");
foreach (var file in pngFiles)
{
    Image img = Image.FromFile(file);
    OcrResult res = ocrEngine.RecognizeToResult(img);
    string outPath = Path.ChangeExtension(file, ".json");
    File.WriteAllText(outPath, JsonSerializer.Serialize(res, new JsonSerializerOptions { WriteIndented = true }));
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(outPath)}");
}
```

现在程序能够**对 PNG 文件批量执行 OCR**，并为每张图像生成对应的 JSON 文件。

## 结论

你已经学习了如何在 C# 中使用 Aspose OCR **识别图像文字**、**加载图像进行 OCR**、**提取图像文字**，以及 **在 C# 中写入 JSON 文件** 来存储结果。完整且可运行的示例涵盖了关键步骤，解释了每一步的重要性，并展示了如何处理 PNG 的特定细节。

下一步可以尝试将 JSON 导入搜索索引，结合语言检测，或集成到实时处理上传的 Web API 中。如果你的场景需要手写识别，也可以探索 Aspose 对手写文字的支持。

对边缘情况或性能调优有疑问？欢迎在下方留言——祝编码愉快！ 

![recognize text from image demo](/images/ocr-demo.png "Diagram showing how Aspose OCR recognizes text from image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}