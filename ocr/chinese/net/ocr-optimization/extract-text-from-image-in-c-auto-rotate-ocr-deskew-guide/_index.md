---
category: general
date: 2026-03-29
description: 使用 Aspose OCR 在 C# 中从图像提取文本。学习自动旋转 OCR 以及如何对扫描图像进行去倾斜，以获得完美效果。
draft: false
keywords:
- extract text from image
- auto rotate ocr
- how to deskew scanned image
- Aspose OCR C#
- image preprocessing OCR
language: zh
og_description: 使用 Aspose OCR 从图像中提取文本。本指南展示了自动旋转 OCR 以及如何在 C# 中对扫描图像进行去倾斜。
og_title: 在 C# 中从图像提取文本 – 自动旋转 OCR 与去倾斜
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 在 C# 中从图像提取文本 – 自动旋转 OCR 与去倾斜指南
url: /zh/net/ocr-optimization/extract-text-from-image-in-c-auto-rotate-ocr-deskew-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本（C#） – 自动旋转 OCR 与去倾斜指南

是否曾经需要**从图像中提取文本**，但文件却以奇怪的角度出现？这是一种常见的麻烦——尤其是当你处理扫描的发票、拍摄的收据或倾斜的 PDF 时。好消息是，你不必自己编写自定义旋转算法。通过使用 Aspose OCR 内置的 *auto rotate OCR* 功能，你可以让引擎自动校正图片，然后在一步完成**从图像中提取文本**。

在本教程中，我们将逐步演示一个完整的、可直接运行的 C# 程序，该程序能够：

* 初始化 OCR 引擎，启用自动方向校正和去倾斜，
* 识别旋转或倾斜的图片，
* 返回检测到的旋转角度以及提取的文本。

无需外部服务，无需繁琐的数学计算——只需几行代码，并提供在需要时*如何去倾斜扫描图像*的清晰说明。

## 所需条件

| 前置条件 | 为什么重要 |
|--------------|----------------|
| .NET 6.0 or later (or .NET Framework 4.6+) | Aspose OCR 以 NuGet 包形式提供，支持这些运行时。 |
| Visual Studio 2022 (or any C# editor) | 便于添加 NuGet 包并运行控制台应用程序。 |
| A sample image (`rotated_document.jpg`) | 文件应为 JPEG、PNG、BMP 或 TIFF，且不是完全正立的。 |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | 提供 `OcrEngine`、`PreprocessingFilters` 以及相关类型。 |

如果这些条件都已满足，你就可以开始了。否则，请从 NuGet 获取最新的 Aspose OCR——只需一次点击即可安装。

---

## 第一步 – 初始化 OCR 引擎（主要关键词演示）

我们首先创建一个 `OcrEngine` 实例，并指示它对任何输入图片执行 **auto rotate OCR** 和 **deskew**。这两个标志通过位或运算符 (`|`) 组合，因为 `PreprocessingFilters` 是带有 `[Flags]` 特性的枚举。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine with English language and preprocessing options
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Enable both auto‑rotate and auto‑deskew
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };
```

> **为什么重要：**  
> *Auto‑rotate OCR* 检查图像的文字基线，猜测正确的方向，并在识别前内部旋转图像。*Auto‑deskew* 对扫描文档中常见的轻微倾斜执行相同操作。启用这两者，可确保在无需手动编辑图像的情况下获得最佳的 **extract text from image** 结果。

---

## 第二步 – 识别图像并获取结果

现在我们将文件路径交给引擎。`RecognizeImage` 方法返回一个 `OcrResult` 对象，其中包含检测到的旋转角度、置信度分数以及纯文本输出。

```csharp
        // Recognise the image file and obtain the OCR result
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/rotated_document.jpg");
```

> **提示：** 如果使用流（例如上传的文件），请改用 `ocrEngine.RecognizeImage(Stream)`。相同的预处理标志仍然适用，因此仍可获得 **auto rotate OCR** 的优势。

---

## 第三步 – 显示旋转角度和提取的文本

最后，我们在控制台打印两条信息：引擎认为图片需要旋转的角度，以及实际提取的文本。

```csharp
        // Show the detected rotation and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**预期输出**（根据输入图像，数值会有所不同）：

```
Detected rotation: 12.3°
----- Extracted Text -----
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

如果图像已经正立，旋转角度将为 `0°`，并且由于 *auto‑deskew* 算法，你仍然会得到干净的文本。

---

## 第四步 – 理解如何去倾斜扫描图像（次要关键词深度探讨）

当 OCR 引擎报告非零旋转时，你可能会想知道 *how to deskew scanned image*。在内部，Aspose OCR 使用 **Hough 变换** 检测主要文字行的方向，然后按该角度的相反方向旋转位图，从而有效地校正文字。

**何时重要？**  
* 纸张进纸时略有倾斜的扫描仪（在办公环境中常见）。  
* 手持拍摄的手机照片——水平线很少完美。

**边缘情况处理：**  
如果结果的 `RotationAngle` 异常大（例如 > 45°），引擎可能误判了图像（可能是标志或非文字图形）。此时你可以：

1. 在将图像送入引擎前，使用 `System.Drawing` 手动旋转图像，或  
2. 禁用 `AutoRotate`，仅保留 `AutoDeskew`，前提是你确认文档已经正立。

```csharp
// Example: manually rotate 90° clockwise before OCR
using (var img = Aspose.OCR.Image.Load("rotated_document.jpg"))
{
    img.Rotate(90);
    OcrResult result = ocrEngine.RecognizeImage(img);
    Console.WriteLine(result.Text);
}
```

---

## 第五步 – 常见陷阱与专业技巧（E‑E‑A‑T 实践）

| 陷阱 | 为什么会出现 | 解决方案 |
|---------|----------------|-----|
| **模糊或低分辨率的图像** | OCR 准确率会显著下降；旋转检测可能失败。 | 使用至少 300 dpi 的扫描；在 OCR 前应用锐化滤镜。 |
| **混合语言** | 引擎默认使用英语，外文字符会出现乱码。 | 设置 `Language = Language.English | Language.Spanish`（或相应组合）。 |
| **大文件（> 10 MB）** | 内存压力可能导致 `OutOfMemoryException`。 | 先缩小图像，或使用 `OcrEngine.RecognizeRegion` 分块处理。 |
| **文件路径错误** | `FileNotFoundException` 会终止程序。 | 使用 `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")` 提高鲁棒性。 |

> **专业提示：** 始终记录 `ocrResult.RotationAngle` 和 `ocrResult.Confidence`（如果可用）。这些指标可帮助你判断是否值得使用不同的预处理设置重新尝试。

---

## 第六步 – 扩展示例（下一步是什么？）

现在你已经可以通过自动旋转和去倾斜 **extract text from image**，可以考虑以下后续步骤：

* **批量处理** – 遍历文件夹中的图像，将每个结果存入数据库，并对 `RotationAngle > 5°` 的图像标记为手动审核。  
* **PDF 转换** – 使用 Aspose.PDF 将提取的文本与原始图像合并为可搜索的 PDF。  
* **语言检测** – 使用 Aspose.OCR 的 `AutoDetectLanguage` 标志，让引擎自动选择最佳语言。  

上述每一步都基于同一核心原则：让库处理方向问题，而你专注于业务逻辑。

---

## 完整可运行示例（复制粘贴即可）

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine with auto‑rotate and auto‑deskew
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };

        // 2️⃣ Recognise the image – replace the path with your own file
        string imagePath = "YOUR_DIRECTORY/rotated_document.jpg";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 3️⃣ Output the rotation angle and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

将文件保存为 `Program.cs`，运行 `dotnet add package Aspose.OCR`，然后执行 `dotnet run`。你应当在控制台看到旋转角度和干净的文本输出。

---

## 结论

我们刚刚演示了如何在 C# 中 **extract text from image**，并让 Aspose OCR 处理 *auto rotate OCR* 与棘手的 *how to deskew scanned image* 问题。通过启用这两个预处理标志，引擎会自动校正倾斜的图片，检测正确的方向，并输出准确的文本——无需手动编辑图像。

欢迎尝试更大批量、不同语言，甚至将输出集成到可搜索的 PDF 中。一旦 OCR 引擎承担了繁重的工作，可能性就无限。

**准备提升你的文档处理流程了吗？** 获取代码，指向你的扫描件，观察旋转角度消失。如果遇到任何问题，请在下方留言——祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}