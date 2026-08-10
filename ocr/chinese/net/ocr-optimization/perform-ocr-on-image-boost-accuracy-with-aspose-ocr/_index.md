---
category: general
date: 2026-03-15
description: 使用 Aspose OCR 在 C# 中对图像执行 OCR。了解如何在 OCR 之前对图像进行预处理，以提高 OCR 准确率，并高效地识别图像中的文本。
draft: false
keywords:
- perform OCR on image
- recognize text from image
- improve OCR accuracy
- preprocess image before OCR
language: zh
og_description: 使用 Aspose OCR 对图像执行 OCR。本指南展示了如何在 OCR 之前对图像进行预处理、提高 OCR 准确率，以及在 C#
  中识别图像中的文本。
og_title: 对图像进行 OCR – 使用 Aspose OCR 提升准确性
tags:
- C#
- Aspose OCR
- Image Processing
title: 在图像上执行 OCR – 使用 Aspose OCR 提升准确率
url: /zh/net/ocr-optimization/perform-ocr-on-image-boost-accuracy-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 对图像执行 OCR – 使用 Aspose OCR 提升准确率

是否曾经需要 **对图像执行 OCR**，却总是得到乱码输出？你并不孤单。在许多真实项目中，噪声多、倾斜的扫描件会让即使是最好的 OCR 引擎也束手无策，导致文本看起来像是猫在键盘上走了一圈后留下的。

关键在于：原始图片只是成功的一半。通过 **在 OCR 前预处理图像**，你可以显著 **提升 OCR 准确率**，最终可靠地 **从图像中识别文本**。在本教程中，我们将演示一个完整、可直接运行的 C# 示例，展示如何使用 Aspose.OCR 完成上述操作。

我们将覆盖：

* 安装 Aspose.OCR NuGet 包。  
* 构建预处理流水线（去倾斜、去噪、对比度提升、二值化）。  
* 运行 OCR 引擎并打印识别出的文本。  

没有废话，没有“稍后查看文档”的捷径——只提供一个可以直接放入控制台应用的完整解决方案。

---

## 需要的环境

在开始之前，请确保你拥有：

* **.NET 6+**（或 .NET Framework 4.6.2+）。  
* 最近的 **Aspose.OCR** NuGet 包（v23.10 或更高）。  
* 一张稍显混乱的图像文件——比如倾斜、噪声大、对比度低的扫描件。  
* Visual Studio、VS Code 或任意你喜欢的 IDE。

就这些。如果缺少 NuGet 包，请运行：

```bash
dotnet add package Aspose.OCR
```

现在让我们动手实践。

---

## ## 对图像执行 OCR – 设置引擎

第一步是创建 `OcrEngine` 实例。该对象是 Aspose OCR 的核心，负责保存配置、流水线以及实际的识别逻辑。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System.Drawing;          // For Image class
using System;                  // For Console

// Step 1: Instantiate the OCR engine
var ocrEngine = new OcrEngine();
```

> **为什么重要：**  
> 实例化引擎相当于提供了一块干净的画布。之后你可以随时更换设置（语言、识别模式等），而无需修改其他代码。

---

## ## 在 OCR 前预处理图像 – 构建流水线

原始扫描很少完美。一个好的预处理流水线可以在某些情况下 **提升 OCR 准确率** 高达 30 %。下面我们链式调用四个过滤器：

| Filter | 功能说明 | 常用取值 |
|--------|----------|----------|
| `DeskewFilter` | 检测并纠正旋转角度 | `Angle = 0.0`（自动检测） |
| `DenoiseFilter` | 去除斑点和颗粒噪声 | `Strength = 70`（满分 100） |
| `ContrastBoostFilter` | 让暗文字更突出 | `Strength = 40` |
| `BinarizationFilter` | 将图像转为纯黑白 | `Threshold = 128` |

```csharp
// Step 2: Create a preprocessing pipeline
var preprocessingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { Angle = 0.0 })               // auto‑detect skew angle
    .Add(new DenoiseFilter { Strength = 70 })           // reduce noise
    .Add(new ContrastBoostFilter { Strength = 40 })     // enhance contrast
    .Add(new BinarizationFilter { Threshold = 128 });   // convert to B/W

// Attach the pipeline to the OCR engine
ocrEngine.Configuration.PreProcessing = preprocessingPipeline;
```

> **小技巧：** 如果你的源图像已经相当干净，可以跳过 `DenoiseFilter`，或降低其 `Strength`。过度过滤有时会抹掉细小字符。

---

## ## 加载图像 – 文件位置

接下来将引擎指向我们要读取的图片。`Image.FromFile` 方法支持 System.Drawing 能处理的所有格式（JPEG、PNG、BMP 等）。

```csharp
// Step 3: Load the image you want to recognize
var inputImagePath = @"C:\Images\skewed_noisy.jpg";   // change to your path
var inputImage = Image.FromFile(inputImagePath);
```

> **边缘情况：** 如果文件路径包含空格或 Unicode 字符，请像上面示例那样使用逐字字符串 (`@"..."`) 包裹。另外，在生产代码中务必捕获 `FileNotFoundException`。

---

## ## 从图像中识别文本 – 运行 OCR 引擎

引擎配置完毕、图像加载后，实际识别只需一行代码。返回结果包含提取的文本以及后续可检查的置信度指标。

```csharp
// Step 4: Perform OCR and get the result
var ocrResult = ocrEngine.Recognize(inputImage);

// Display the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

运行程序后，你应当看到类似下面的输出：

```
=== OCR Output ===
Invoice #12345
Date: 03/12/2026
Total: $1,250.00
```

如果输出异常，请调节流水线的强度或尝试不同的 `Threshold` 值。微小的调整往往能带来巨大差异。

---

## ## 常见坑点及解决方案

1. **结果为空或大部分是乱码**  
   *检查流水线。* 过于激进的去噪会抹掉细线笔画。降低 `Strength` 或暂时注释掉该过滤器。

2. **倾斜未被纠正**  
   `DeskewFilter` 最适用于文本基线基本水平的文档。如果图像旋转超过 15°，可能需要先使用 `RotateFlip` 手动旋转。

3. **非拉丁字符未被识别**  
   默认情况下 Aspose OCR 使用英文语言模型。调用 `Recognize` 前，将 `ocrEngine.Configuration.Language` 设置为相应的 ISO 代码（例如 `"fr"` 表示法语）。

```csharp
ocrEngine.Configuration.Language = "fr";   // for French text
```

4. **性能感觉慢**  
   若一次处理数百页，请复用同一个 `OcrEngine` 实例，并在循环中仅替换 `Image` 对象。每次新建引擎会带来不必要的开销。

---

## ## 可视化结果 – 预处理后的图像长什么样

下面是一张前后对比示意图（实际输出可能有所不同）。

![对图像执行 OCR 结果](https://example.com/ocr-before-after.png "对图像执行 OCR – 预处理前后对比")

*Alt text:* “Perform OCR on Image – 原始噪声扫描与预处理后准备进行 OCR 的版本对比”。

---

## ## 收尾：完整可运行示例

将下面的完整代码片段复制到新建的控制台项目（`dotnet new console`）中，按 **F5** 运行。它会编译、执行，并在控制台打印识别出的文本。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System.Drawing;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build a preprocessing pipeline (improve OCR accuracy)
        var preprocessingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { Angle = 0.0 })               // auto‑detect skew angle
            .Add(new DenoiseFilter { Strength = 70 })           // reduce noise
            .Add(new ContrastBoostFilter { Strength = 40 })     // enhance contrast
            .Add(new BinarizationFilter { Threshold = 128 });   // convert to B/W

        ocrEngine.Configuration.PreProcessing = preprocessingPipeline;

        // 3️⃣ Load the image you want to read
        var imagePath = @"YOUR_DIRECTORY\skewed_noisy.jpg";   // ← update this path
        var inputImage = Image.FromFile(imagePath);

        // 4️⃣ Run OCR – recognize text from image
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Show the result
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**预期输出：** 控制台会打印出图片上内容的纯文本版本——无论是发票、护照扫描件，还是手写便条。

---

## ## 后续步骤 – 深入探索

* **批量处理：** 将识别调用包装在 `foreach` 循环中，以处理整个文件夹的图像。  
* **语言包：** 从 Aspose 安装额外的语言数据，以 **在图像中识别文本**（西班牙语、德语、中文等）。  
* **自定义后处理：** 使用正则表达式从 OCR 字符串中提取日期、金额或 ID。  
* **替代库对比：** 将结果与 Tesseract 或 Microsoft Azure Computer Vision 进行比较，看看 **在 OCR 前预处理图像** 在不同平台上的表现如何。

---

## ## 结论

我们已经演示了如何使用 Aspose OCR **对图像执行 OCR**，构建了智能的预处理流水线，并看到 **在 OCR 前预处理图像** 能显著 **提升 OCR 准确率**。按照上述步骤，你现在可以在任何 C# 应用中可靠地 **从图像中识别文本**——再也不必为乱码输出苦恼。

欢迎尝试不同的过滤强度、图像格式，或将此代码集成到更大的文档处理服务中。只要 OCR 流水线稳固，可能性无限。

有问题或酷炫的使用案例？在下方留言，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}