---
category: general
date: 2026-03-17
description: c# OCR 教程——了解如何从图像文件中提取文本，读取 WebP 照片中的文字，并使用简单的 OcrEngine 将图像转换为文本。
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: zh
og_description: C# OCR 教程向您展示如何从图像文件中提取文本、读取 WebP 照片中的文本，并使用几行代码将图像转换为文本。
og_title: C# OCR 教程 – 在几分钟内从图像中提取文本
tags:
- C#
- OCR
- Image Processing
title: C# OCR 教程：从图像（WebP、照片）提取文本 – 快速指南
url: /zh/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教程 – 从图像中提取文本（WebP，照片）

是否曾经需要**从图像中提取文本**但不确定在 C# 中该如何开始？也许你有一张 WebP 截图、一张收据的 JPEG，或是一页已扫描的 PDF，而你只想获取其中的文字。在本**c# OCR 教程**中，我们将演示一个完整、可直接运行的示例，读取照片中的文本，处理 WebP 以及其他现代格式，并将图像转换为纯文本——只需几行代码。

**有什么收益？** 你将能够将任何文字图片转换为可搜索的字符串，输入到数据库，或传递给下游的 AI 流程。没有魔法，只有可靠的 OCR 引擎、一些 .NET API，以及对每一步“为什么”进行的清晰解释。

## 你需要的环境

- **.NET 6 SDK**（或更高）。下面的代码使用 .NET 6+ 编译，并可在 Windows、Linux 或 macOS 上运行。
- **Visual Studio 2022** 或你喜欢的任何编辑器（VS Code 也可以）。
- **`Microsoft.Windows.SDK.Contracts`** NuGet 包（提供 `Windows.Media.Ocr`）。使用以下方式安装：

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- 你想要处理的图像文件——本教程中我们使用名为 `photo.webp` 的 **WebP** 照片，放在 `YOUR_DIRECTORY` 文件夹中。

> 小技巧：如果你在非 Windows 平台上，可以将 `OcrEngine` 替换为跨平台库如 **Tesseract**。其余代码基本保持不变。

## 步骤 1：设置 C# OCR 教程项目

首先，创建一个全新的控制台应用。打开终端并运行：

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

按照上面所示添加所需的包，然后在 IDE 中打开项目。这些脚手架为 **c# OCR 教程** 提供了一个干净的起点。

## 步骤 2：导入命名空间并准备图像

我们需要一些 `using` 指令，让编译器知道 `OcrEngine`、`SoftwareBitmap` 和图像加载辅助类的位置。

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **为什么需要这些命名空间？**  
> `Windows.Media.Ocr` 包含实际执行识别的 `OcrEngine` 类。`Windows.Graphics.Imaging` 让我们能够将图像（包括 WebP）解码为 `SoftwareBitmap`，供引擎使用。`System.IO` 和 `Windows.Storage.Streams` 辅助类使文件加载变得轻松。

现在，加载图像。内置解码器可以处理 WebP、HEIF、PNG、JPEG 等，因此你可以**从 WebP 中读取文本**而无需额外插件。

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **边缘情况：** 如果你的图像已经是黑白的，可以跳过转换步骤。灰度转换可以略微提升性能，并且常常在噪声较大的照片上改善识别效果。

## 步骤 3：运行 OCR 引擎 – 从照片中识别文本

下面是 **c# OCR 教程** 的核心。我们创建 `OcrEngine` 实例，将位图传入，并提取识别出的文本。

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**发生了什么？**  
- `TryCreateFromUserProfileLanguages()` 会选择 Windows 用户配置文件中设置的语言（通常包括英语、西班牙语等）。如果需要特定语言，可使用 `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`。  
- `RecognizeAsync` 在后台线程执行繁重的工作，返回包含原始字符串、单词边界框和置信度分数的 `OcrResult`。  
- 最后，我们打印 `ocrResult.Text`，为你提供 **convert image to text** 的结果，可进一步传递。

## 步骤 4：完整、可运行的示例

将所有内容整合在一起，下面是一个可直接复制粘贴到 `Program.cs` 的独立程序。它可以编译、运行，并打印从 `photo.webp` 提取的文本。

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### 预期输出

如果 `photo.webp` 包含句子 “Hello, world! This is a test.”，你会看到类似如下的输出：

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

具体的换行取决于源图像的布局，但 **extract text from image** 的结果始终是一个纯字符串，供后续操作。

## 常见问题与边缘情况

### 这能用于其他图像格式吗？

当然可以。使用的解码器（`BitmapDecoder`）会自动检测 JPEG、PNG、BMP、GIF、**WebP**、HEIF 等。因此，你可以**从 WebP**、JPEG，甚至 TIFF 中读取文本，而无需更改代码。

### 如果 OCR 引擎返回低置信度怎么办？

你可以检查 `ocrResult.Lines` 以及每个 `OcrWord` 的 `ConfidenceScore`。如果分数低于阈值（例如 0.6），可以考虑：

- 对图像进行预处理（提升对比度、锐化、去倾斜）。
- 使用更高分辨率的源图像。
- 切换到专用库如 **Tesseract** 以获得多语言支持。

### 如何处理同一图像中的多语言？

为每种语言创建单独的 `OcrEngine` 实例并顺序运行，或使用支持混合语言检测的库。对于内置引擎，你可以传入 `Language` 对象：

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### 我可以在 Linux/macOS 上运行吗？

`Windows.Media.Ocr` API 仅限 Windows。非 Windows 平台上，请将 OCR 部分替换为 **Tesseract**（通过 `Tesseract.Net.SDK`）。加载和预处理代码保持不变，因此本 **c# OCR 教程** 的其余部分仍然适用。

## 提高准确性的专业技巧

- **Resize** 大图像，使最长边不超过 2000 px——OCR 引擎在适中尺寸下运行更快。
- **Denoise**：如果照片颗粒感强，可使用简单的高斯模糊去噪。
- **Deskew**：如果文字不是完全水平，可对位图进行去倾斜；在传递给 `OcrEngine` 前，可使用 `SoftwareBitmap` 进行旋转。
- **Cache**：如果批量处理大量图像，请缓存 `OcrEngine` 实例；反复创建会增加开销。

## 相关主题探索

- 使用 **Tesseract** 将 **Convert image to text** 用于跨平台项目。
- 通过先将每页渲染为图像，**Extract text from PDF**。
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}