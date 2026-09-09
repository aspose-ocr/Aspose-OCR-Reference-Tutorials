---
category: general
date: 2026-01-10
description: 学习如何使用 Aspose OCR 在 C# 中识别图像中的文本、提取文本坐标，并将收据转换为 JSON。一步一步的教程。
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: zh
og_description: 使用 Aspose OCR 在 C# 中识别图像中的文本。本指南展示了如何提取文本、获取坐标以及将收据转换为 JSON。
og_title: 从图像识别文本 – 完整的 C# OCR 教程
tags:
- OCR
- C#
- Aspose
title: 在 C# 中从图像识别文本 – OCR 与 JSON 完全指南
url: /zh/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 识别图像文字 – 完整 C# OCR 教程

是否曾需要从图像中识别文字，却不确定该选哪个库？你并不孤单。在许多实际应用中——费用追踪器、收据扫描仪或文档归档系统——可靠地提取文字是第一道难关。

在本教程中，我们将演示 **如何提取文字**、获取其边界框，并最终使用 Aspose.OCR for .NET **将收据转换为 JSON**。完成后，你将拥有一个独立的 C# 项目，能够读取收据照片并输出包含置信度分数和坐标的整洁 JSON 文件。

## 你需要准备的环境

在开始之前，请确保你的机器上已具备以下条件：

- **.NET 6.0 SDK**（或更高版本）。旧版框架也可使用，但 .NET 6 是现代库的最佳选择。
- **Visual Studio 2022** 或带有 C# 扩展的 VS Code。
- **Aspose.OCR for .NET** NuGet 包（`Aspose.OCR` 和 `Aspose.OCR.Output`）。可通过包管理控制台安装：

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- 一张示例收据图片（例如 `receipt.jpg`），放在稍后会引用的文件夹中。

就这些——无需额外 SDK、无需本地二进制文件，纯托管代码即可。

## 第一步：创建新控制台项目

首先，创建一个控制台应用程序。这是测试 OCR 而不涉及 UI 的最快方式。

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **小贴士：** 保持项目文件夹整洁；创建一个名为 `Resources` 的子文件夹并将 `receipt.jpg` 放进去。这样处理路径会更轻松。

## 第二步：加载收据图片

现在我们真正 **识别图像文字**。第一步是让 OCR 引擎指向该文件。

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

为什么要在加载时做一次存在性检查？因为在生产环境中，你经常会处理可能缺失或损坏的用户上传文件。提前捕获问题可以避免后期出现难以理解的异常。

## 第三步：执行 OCR – **识别图像文字**

图片已加载到内存后，我们让 Aspose **识别图像文字**。此操作是同步的，并返回丰富的结果集。

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

在幕后，Aspose 运行一个在数百万字符上训练的神经网络。引擎会填充 `ocrEngine.Text`、`ocrEngine.RecognitionResult`，以及包含坐标的 `OcrRegion` 集合。这正是我们后续步骤所需的。

## 第四步：**如何提取文字** – 获取原始字符串

如果你只关心纯文本（例如快速搜索），可以直接从引擎中获取：

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

你会看到 OCR 检测到段落边界的换行符。在许多收据扫描场景中，原始字符串足以通过简单的正则表达式提取总额、日期或商家名称。

## 第五步：**提取文字坐标** – 每个单词的边界框

通常你需要知道文本在图像中的 **位置**——例如在 UI 中高亮显示总金额。Aspose 通过 `OcrRegion` 对象提供这些信息。

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

请注意，我们在遍历 **提取文字坐标** 时，对每个识别的片段进行循环。坐标是相对于原始图像的，你可以在图形画布或 HTML `<canvas>` 元素上进行叠加显示。

## 第六步：**将收据转换为 JSON** – 保存详细结果

现在进入关键环节：我们希望得到一个机器可读的结构，包含文字、置信度分数以及边界框。Aspose 提供的 `JsonSaveOptions` 让这一步变得轻而易举。

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

生成的文件大致如下（为简洁起见已截取）：

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

现在你拥有了一个 **将收据转换为 JSON** 的产物，可供下游服务使用——比如费用报销 API、分析管道，甚至是一个简单的 UI，用于在每个单词周围绘制矩形。

## 完整工作示例

将所有代码片段组合起来，下面是可以直接复制粘贴到项目中的完整 `Program.cs`：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

运行程序（`dotnet run`）并观察控制台输出。打开 `Resources/receipt.json` 验证结构是否正确。

## 常见问题与边缘情况

- **如果图片模糊怎么办？**  
  Aspose OCR 在 300 dpi 或更高分辨率下表现最佳。如果置信度分数偏低，考虑在送入引擎前先应用锐化滤镜。

- **能识别多种语言吗？**  
  可以。在调用 `Recognize()` 之前设置 `ocrEngine.Language = Language.English | Language.Spanish;`。

- **如何只输出数字（例如总额）？**  
  获取纯文本后，可使用正则表达式 `\d+\.\d{2}` 在 `ocrEngine.Text` 上匹配。因为我们已经拥有坐标，可以将匹配的字符串映射回对应的区域，以实现可视化高亮。

- **JSON 格式可以自定义吗？**  
  `JsonSaveOptions` 类提供若干标志位。如果需要完全自定义的结构，可以遍历 `ocrEngine.RecognitionResult.Regions`，并使用 `System.Text.Json` 手动序列化对象。

## 结论

我们已经演示了如何在 C# 中使用 Aspose.OCR **识别图像文字**、**提取文字**、获取 **提取文字坐标**，并最终 **将收据转换为 JSON**。整个流程封装在一个易于运行的控制台应用中，非常适合作为原型或更大系统的构建块。

接下来可以尝试将 JSON 输入前端，以绘制边界框，或将输出接入费用报销服务。也可以尝试不同的图像格式（PNG、TIFF）或批量处理整个收据文件夹。

对 OCR、Aspose 或 JSON 处理还有其他疑问？欢迎在下方留言，祝编码愉快！

![识别图像文字的收据示例](receipt.jpg "收据图像示例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}