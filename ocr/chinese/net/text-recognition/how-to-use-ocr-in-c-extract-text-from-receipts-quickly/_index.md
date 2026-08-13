---
category: general
date: 2026-03-05
description: 如何在 C# 中使用 OCR 从收据图像中提取文本。学习如何加载图像进行 OCR，并在几分钟内识别收据图像。
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: zh
og_description: 如何在 C# 中使用 OCR 提取收据文本。请按照本分步指南加载图像进行 OCR，并高效识别收据图像。
og_title: 如何在 C# 中使用 OCR – 快速收据文本提取
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: 如何在 C# 中使用 OCR – 快速提取收据文本
url: /zh/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 快速提取收据文本

有没有想过 **how to use OCR** 从杂货收据的照片中直接提取数据？你并不是唯一有这种想法的人。在许多小型企业应用中，瓶颈在于将模糊的 PNG 转换为可实际使用的结构化文本。  

好消息是？只需几行 C# 代码和 Aspose.OCR，你就可以 **load image for OCR**，运行引擎，并在一分钟内 **recognize receipt image**。下面你会看到一个完整的、可直接运行的示例，以及大多数教程忽略的技巧。

## 本指南涵盖内容

我们将逐步讲解你需要了解的所有内容：

* 安装 Aspose.OCR NuGet 包。  
* 设置 OCR 引擎 – 正确使用 **how to use OCR** 的核心。  
* 加载收据文件（即 **load image for OCR** 步骤）。  
* 运行识别过程并提取 JSON 和 XML 布局数据。  
* 处理常见陷阱，如缺少许可证或不受支持的图像格式。  

完成后，你将拥有一个独立的程序，能够提取放入文件夹的任何收据的文本。无需外部服务，也没有隐藏的魔法。

## 前提条件

* .NET 6 SDK 或更高版本（代码也可在 .NET Core 上编译）。  
* 有效的 Aspose.OCR 许可证文件 (`Aspose.OCR.lic`)。如果还没有，可以从 Aspose 获取免费试用。  
* 示例收据图像 – `receipt.png` 可用，任何常见的光栅格式都可以。  

如果你已经准备好这些，太好了 – 让我们开始吧。

![how to use OCR example](https://example.com/ocr-receipt.png "how to use OCR example")

## 步骤 1：安装 Aspose.OCR 并创建新项目

首先，你需要实际完成繁重工作的库。在项目文件夹中打开终端并运行：

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

该命令会创建一个控制台应用并拉取最新的 Aspose.OCR 包。根据我的经验，保持项目名称简短可以让生成的路径更易阅读，尤其是在同时处理多个演示应用时。

## 步骤 2：初始化 OCR 引擎 – **how to use OCR** 的核心

现在我们将编写代码来回答 “**how to use OCR** 在 C# 中如何实现” 这个问题。打开 `Program.cs` 并用下面的代码片段替换其内容。注意注释——它们解释了每行代码背后的 *原因*，而不仅仅是 *做了什么*。

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### 为什么这样有效

* `OcrEngine` 是入口点；它保存了所有你以后可能会调整的配置（语言、DPI 等）。  
* `SetLicense` 移除评估水印 —— 当你计划发布代码时这是关键步骤。  
* `ImageStream.FromFile` 完成 **load image for OCR** 工作，支持 PNG、JPEG、BMP、TIFF 等格式。  
* `Recognize()` 是实际执行 **recognize receipt image** 的方法。内部会进行二值化、分割和字符分类。  
* 导出为 JSON 和 XML 可同时获得人类可读的转储和机器友好的结构，便于后续解析器使用。

## 步骤 3：运行示例并验证输出

编译并执行：

```bash
dotnet run
```

如果一切配置正确，你会看到类似如下的输出：

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

控制台会打印纯文本，而 `receipt.json` 和 `receipt.xml` 则包含详细的布局信息（坐标、置信度分数等）。如果以后需要将每行映射到数据库字段，这些文件非常有用。

## 边缘情况与专业技巧

### 1️⃣ 缺失或无效的许可证

如果 `SetLicense` 失败，引擎会回退到试用模式，输出中会出现水印。将调用包装在 try/catch 中并记录友好的提示信息：

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ 不受支持的图像格式

Aspose.OCR 支持大多数光栅格式，但如果你提供 PDF 或多页 TIFF，则需要先将感兴趣的页面转换为图像。`Aspose.PDF` 库可以完成此转换。

### 3️⃣ 大尺寸收据与性能

处理 10 MB 的图像可能会很慢。将分辨率降低后再送入引擎：

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

`Resize` 方法保持宽高比（高度设为 `0`），显著降低文件大小，同时不影响典型收据的 OCR 精度。

### 4️⃣ 语言与字体问题

收据可能包含特殊字符（€, ¥ 等）。如果已知地区，请显式设置语言：

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

对于混合语言的收据，你可以启用多语言模式：

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ 提取结构化数据

原始文本有用，但大多数应用需要结构化字段（日期、总额、商品等）。JSON 布局包含每个单词的 `BoundingBox` 坐标。你可以这样后处理：

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

该代码片段展示了思路；在生产环境中你可能会使用正则表达式或小型规则引擎。

## 常见问题

**Q: 我可以在 Linux 上运行吗？**  
A: 当然可以。Aspose.OCR 是跨平台的；只需在你的 Linux 机器上安装 .NET 运行时，代码即可正常工作。

**Q: 如果我需要每分钟处理数十张收据怎么办？**  
A: 启动一个 `Parallel.ForEach` 循环并复用同一个 `OcrEngine` 实例 —— 对只读操作是线程安全的。记得处理许可证的并发限制。

**Q: 这能处理倾斜拍摄的手机照片吗？**  
A: 引擎自带基本的去倾斜功能，但对于严重倾斜的图像，你可能需要先使用图像处理库（例如 OpenCV）进行预处理，将收据校正。

## 完整可运行示例（复制粘贴）

下面是可以直接粘贴到 `Program.cs` 的 *完整* 程序。除许可证和收据图像外，无需其他文件。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}