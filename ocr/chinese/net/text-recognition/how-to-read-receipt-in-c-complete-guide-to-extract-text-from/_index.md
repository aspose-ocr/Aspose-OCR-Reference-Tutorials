---
category: general
date: 2026-02-20
description: 学习如何在 C# 中通过从图像提取文本并将其转换为 JSON 来读取收据。使用 Aspose OCR 的逐步代码示例。
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: zh
og_description: 了解如何在 C# 中读取收据：加载图像文件，使用 Aspose OCR 提取文本，并将结果转换为 JSON。完整代码示例。
og_title: 如何在 C# 中读取收据 – 提取文本并转换为 JSON
tags:
- C#
- OCR
- Image Processing
- JSON
title: 如何在 C# 中读取收据 – 完整的图像文字提取指南
url: /zh/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中读取收据 – 完整指南

你是否曾经想过**如何读取收据**图像？也许你正在构建一个费用跟踪应用，需要从超市收据的照片中提取项目行。根据我的经验，最大的问题是把模糊的 JPEG 转换为可用的结构化数据。好消息是？只需几行 C# 代码和 Aspose OCR，你就可以**从图像中提取文本**，然后**将图像转换为 JSON**，几乎像魔法一样。

在本教程中，你将获得一个可直接运行的解决方案，**加载图像文件 C#**，执行 OCR，并输出详细的 JSON 负载。无需外部服务，也不需要繁琐的 REST 调用——只需纯 .NET 代码，可直接放入任何控制台或 ASP.NET 项目。完成后，你将了解每一步为何重要，如何处理常见的边缘情况（如非标准收据尺寸），以及 JSON 输出的实际样子。

## 你需要的条件

- **.NET 6.0 或更高** – 代码使用 `System.Drawing.Common`，该库在 Windows、Linux 和 macOS 上受支持。
- **Aspose.OCR for .NET** – 你可以获取免费试用的 NuGet 包 (`Aspose.OCR`)，如果有许可证也可以使用已授权的副本。
- 一个 **sample receipt image** (`receipt.jpg`)，放在应用能够读取的位置。
- 任意你喜欢的 IDE（Visual Studio、Rider、VS Code）。

就是这样。无需额外配置，也不需要 API 密钥。

## 第一步 – 加载图像文件 C#（主要关键词实践）

在 OCR 引擎发挥魔力之前，你必须先将图片加载到内存中。这是许多开发者常常忽视的经典“加载图像文件 C#”步骤。

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**为什么这很重要：**  
`Image.FromFile` 会*一次*读取文件并保持句柄打开，这对于快速 OCR 处理非常合适。如果你在循环中处理大量收据，考虑使用 `Image.FromStream` 以避免锁定文件。

> **专业提示：** 如果遇到 *FileNotFoundException*，请再次检查路径并确保图像确实存在。相对路径也可使用（`"./receipt.jpg"`），但在生产环境中使用绝对路径更安全。

## 第二步 – 创建并配置 OCR 引擎

Aspose OCR 附带即用的 `OcrEngine`。你无需训练模型；库已经能够读取印刷文本，这正是大多数收据使用的文本。

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**为什么要设置这些选项：**  
`DetectOrientation` 告诉引擎如果收据是倒置扫描的，则自动旋转图像。设置语言可以缩小字符集，从而提升准确度——尤其是当你只需要英文字母数字数据时。

## 第三步 – 识别图像并转换为 JSON

现在进入有趣的部分：在一次调用中**从图像中提取文本**并**将图像转换为 JSON**。

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

`RecognizeToJson` 方法返回一个丰富的 JSON 结构，其中包括：

- `Text`：纯粹的连接文本。
- `Lines`：包含坐标的行对象数组。
- `Words`：每个单词及其置信度分数。
- `Regions`：检测到的文本块的边界框。

如果需要强类型访问，你可以将此 JSON 反序列化为 C# 对象，但在多数场景下直接打印原始 JSON 已足够。

## 第四步 – 输出 JSON（或存储）

让我们看看输出并讨论后续处理方式。

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### 示例输出

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**接下来该怎么做？**  
解析 `Lines` 数组以提取 `Total` 金额，或将 JSON 输入到下游服务以存储费用条目。由于结果已经是 JSON，你可以直接将其接入任何 NoSQL 数据库、Azure Function 或 Power Automate 流程。

## 第五步 – 处理常见边缘情况

即使是最好的 OCR 引擎也会在某些方面出现问题。以下是你在学习**如何读取收据**图像时可能遇到的情形。

| Situation | Fix / Recommendation |
|-----------|----------------------|
| **低分辨率收据 (≤ 150 dpi)** | 使用 `Bitmap` 和 `Graphics`（`InterpolationMode.HighQualityBicubic`）先放大图像。 |
| **旋转或倾斜的收据** | 保持 `DetectOrientation = true`。对于严重倾斜，可使用 `Image.RotateFlip` 或第三方库如 OpenCV 进行预处理。 |
| **彩色背景（例如，收据放在桌子上）** | 在 OCR 前转换为灰度并提高对比度（`ImageAttributes`）。 |
| **一张照片中有多张收据** | 手动裁剪每个收据区域，或使用 `ocrEngine.Config.RecognizeMultipleRegions = true`。 |
| **大文件导致 OutOfMemory** | 使用 `using` 语句及时释放 `Image` 对象，或分块处理。 |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

## 第六步 – 完整工作示例（可复制粘贴）

下面是你现在即可编译的*完整*程序。它包含所有步骤、正确的 `using` 指令以及优雅的错误处理。

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**运行它：**  
在项目文件夹中执行 `dotnet run`。如果一切配置正确，你将在控制台看到打印的 JSON，并且它会保存到收据图像旁边。

## 结论

我们已经完整介绍了在 C# 中**如何读取收据**图像的全过程。通过加载图像、配置 Aspose OCR 并调用 `RecognizeToJson`，你可以几乎无需任何样板代码就**从图像中提取文本**并**将图像转换为 JSON**。该方法具备可扩展性——从单张收据演示到每晚处理数百张收据的批处理程序。

接下来你可能想探索的方向：

- **解析 JSON** 以提取日期、总额和项目行（使用 `System.Text.Json` 或 `Newtonsoft.Json`）。
- **集成数据库**（SQL、Cosmos DB），自动存储费用记录。
- **添加 UI**（WinForms、WPF 或 Blazor），让用户可以拖放收据。
- **将 Aspose OCR 替换**为其他引擎（Tesseract、Microsoft Azure OCR），如果许可证是问题——只需保持相同的“加载图像文件 C#”模式。

随意尝试、打破常规，然后回来这里复习。如果遇到困难，社区（以及 Aspose 论坛）是提问的好地方。祝编码愉快，享受将纸质收据转化为干净、可搜索数据的过程！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}