---
category: general
date: 2026-02-20
description: 使用 Aspose.OCR 在 C# 中对图像 OCR 进行预处理。学习如何应用中值滤波、降低图像噪声，并高效提取文本图像。
draft: false
keywords:
- preprocess image OCR
- apply median filter
- extract text image
- reduce image noise
- c# ocr example
language: zh
og_description: 使用 Aspose.OCR 对图像 OCR 进行预处理。本教程展示了如何使用 C# 应用中值滤波、降低图像噪声以及提取文本图像。
og_title: 在 C# 中预处理图像 OCR – 完整指南
tags:
- OCR
- C#
- Image Processing
title: 在 C# 中对图像 OCR 进行预处理 – 完整的逐步指南
url: /zh/net/ocr-optimization/preprocess-image-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中预处理图像 OCR – 完整分步指南

是否曾因为扫描的照片返回乱码而需要 **预处理图像 OCR**？你并不孤单。在许多真实项目中——比如收据、身份证或手写笔记——原始图像很少能直接用于识别。好消息是，几个简单的预处理步骤就能显著提升准确率，而且全部可以在 C# 中使用 Aspose.OCR 完成。

本教程将通过一个实战示例，展示如何 **应用中值滤波**、**降低图像噪声**，以及最终 **提取文本图像** 并得到干净、可读的结果。完成后，你将拥有一个可直接运行的 C# 控制台应用，能够放入任意 .NET 解决方案中。没有模糊的引用，只有你需要的代码以及每行代码背后的“为什么”。

---

## 你需要准备的东西

- **Aspose.OCR for .NET**（撰写时的最新版本 23.12）。可通过 NuGet 获取：`Install-Package Aspose.OCR`。
- .NET 6.0 或更高版本（示例使用控制台应用，相同逻辑同样适用于 ASP.NET、WPF 等）。
- 一张需要清理的示例图片，例如 `skewed_photo.jpg`。  
- 基本的 C# 经验；即使是初级开发者也能轻松掌握这些概念。

> **专业提示：** 如果你使用的是公司机器，请确保 NuGet 源已配置为允许外部包，否则安装会失败。

---

## 第一步 – 创建 OCR 引擎实例  

首先要做的是实例化一个 `OcrEngine`。该对象保存识别设置，随后会处理预处理后的位图。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image handling
using System;

class PreprocessExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is the core component that will read text.
        OcrEngine ocrEngine = new OcrEngine();

        // ... we’ll continue with loading and preprocessing the image below.
```

**为什么要这样做？**  
一次创建引擎并在多张图片间复用可以降低开销。它还能让你在后期无需重新构建整个管道的情况下，调整语言或识别模式。

---

## 第二步 – 加载源图像  

需要一个指向原始文件的 `System.Drawing.Image` 对象。在真实项目中你可能会接受流，但为保持清晰，这里直接从磁盘读取。

```csharp
        // Load the image that requires preprocessing.
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");
```

> **注意：** 将 `YOUR_DIRECTORY` 替换为实际的文件夹路径。如果文件未找到，将抛出 `FileNotFoundException`——如需更优雅的错误处理，请自行捕获。

---

## 第三步 – 去倾斜并旋转图像  

大多数扫描文档都会有轻微倾斜。`DeskewAndRotate` 滤镜会自动检测倾斜角度并将图片旋转至正立。

```csharp
        // Correct orientation – crucial for accurate OCR.
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());
```

**这有什么意义？**  
OCR 引擎默认文字行是水平的。即使是 2 度的倾斜，也可能导致识别准确率下降 15‑20 %。去倾斜是最划算的提升手段。

---

## 第四步 – 应用中值滤波以降低图像噪声  

噪声表现为斑点或随机像素，尤其在低光照照片中更为明显。中值滤波可以在保留边缘的同时平滑噪声，这正是 OCR 前所需要的。

```csharp
        // Reduce noise – radius of 2 is a good balance for most photos.
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));
```

**为什么选中值滤波？**  
不同于均值（平均）滤波，中值滤波会用邻域像素的中位数替代当前像素。这意味着孤立噪声会被消除，而文字笔画不会被模糊——是 **降低图像噪声** 的经典技术。

---

## 第五步 – 通过拉伸增强对比度  

去噪后，接下来要提升文字与背景之间的差异。对比度拉伸会将像素强度拉伸到完整的 0‑255 范围。

```csharp
        // Stretch contrast to make dark text pop against a light background.
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());
```

**为什么要拉伸？**  
OCR 引擎依赖清晰的前景‑背景分离。如果图像显得灰暗，文字可能被当作背景处理。对比度拉伸可以在不进行手动阈值化的情况下解决这个问题。

---

## 第六步 – 对预处理后的图像执行 OCR  

现在图像已经矫正、清洁且高对比，我们把它交给 OCR 引擎。

```csharp
        // Recognize the text from the cleaned image.
        string extractedText = ocrEngine.Recognize(processedImage);
```

**你将得到：**  
`extractedText` 包含 Aspose.OCR 检测到的原始 Unicode 字符串。必要时可以进一步后处理（如 trim、正则等）。

---

## 第七步 – 输出识别后的文本  

最后，将结果写入控制台或文件——根据你的工作流自行选择。

```csharp
        // Show the result in the console.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

### 预期输出

如果 `skewed_photo.jpg` 中包含 “Hello World” 这句话，你会看到类似如下的输出：

```
=== Extracted Text ===
Hello World
```

如果图像仍然噪声较多，可能会出现乱码——此时返回第 4 步，增大中值滤波半径，或尝试额外的滤镜如 `GaussianBlur`。

---

## 完整可运行示例（复制‑粘贴即用）

下面是完整程序代码，直接编译即可。只需替换文件路径即可运行。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;
using System;

class PreprocessExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image that needs preprocessing
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");

        // Step 3: Deskew and rotate the image to correct orientation
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());

        // Step 4: Reduce noise with a median filter (radius = 2)
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));

        // Step 5: Enhance contrast using contrast stretching
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());

        // Step 6: Perform OCR on the preprocessed image
        string extractedText = ocrEngine.Recognize(processedImage);

        // Step 7: Output the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

> **边缘情况提示：** 如果图像中包含彩色文字且背景也是彩色，建议在使用 `ContrastStretch` 前先转换为灰度。可以在管道中调用 `Preprocess.Grayscale()` 实现。

---

## 常见问题与变体  

### 如果图像是倒置的怎么办？  
`DeskewAndRotate` 会自动检测 180 度旋转，但你也可以在去倾斜前使用 `Preprocess.Rotate(angle: 180)` 强制旋转。

### 可以跳过中值滤波吗？  
可以，但 **降低图像噪声** 的效果会大打折扣。高分辨率扫描可能不需要此滤波；而低光手机拍摄的照片通常离不开它。

### 与直接使用 `Apply(Preprocess.Binarize())` 有何区别？  
二值化会把图像转为纯黑白，可能对细小字体过于苛刻。我们的做法保留灰度细节后再拉伸对比度——对混合大小的字体往往效果更好。

### 能否只对感兴趣的区域应用 **中值滤波**？  
Aspose.OCR 的 `Apply` 会作用于整张位图，但你可以先裁剪图像（`sourceImage.Clone(new Rectangle(...), sourceImage.PixelFormat)`），再对裁剪得到的子图像应用滤波。

---

## 后续步骤 – 超越基础预处理  

- **语言包：** 若需提取法语或日语字符，可通过 `ocrEngine.Language = Language.French;` 加载相应语言模型。  
- **自定义阈值化：** 对极低对比度的扫描，可在中值滤波后尝试 `Preprocess.AdaptiveThreshold()`。  
- **批量处理：** 将上述步骤放入 `foreach (string file in Directory.GetFiles(...))` 循环，并将每个结果写入 `.txt` 文件。  
- **性能调优：** 复用单个 `OcrEngine` 实例并预分配 `Bitmap` 缓冲区，可避免在处理成千上万张图片时出现 GC 峰值。

---

## 结论  

我们已经完整演示了如何在 C# 中 **预处理图像 OCR**：加载图片、去倾斜、**应用中值滤波**、提升对比度，最后使用 Aspose.OCR **提取文本图像**。完整代码可直接嵌入任何项目，配套的解释帮助你理解每一步背后的原理，从而针对自己的特殊场景进行参数微调。

尝试不同的照片，调节滤波半径，观察识别准确率的提升。当你熟练后，可进一步探索上文提到的高级技巧，成为团队中 OCR 流水线的首选专家。

祝编码愉快，愿你的 OCR 永远干净可读！

![预处理图像 OCR 示例](/images/preprocess-image-ocr.png "预处理图像 OCR – 前后对比")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}