---
category: general
date: 2026-01-15
description: 使用 Aspose OCR 在 C# 中将图像转换为 JSON。了解如何从图像中提取文本、获取 JSON 边界框并识别收据图像。
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: zh
og_description: 使用 Aspose OCR 在 C# 中将图像转换为 JSON。一步一步的指南，提取图像中的文本，识别收据图像，并获取 JSON 边界框。
og_title: 使用 Aspose OCR C# 指南将图像转换为 JSON
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: 使用 Aspose OCR C# 将图像转换为 JSON 指南
url: /zh/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR C# 将图像转换为 JSON 的指南

是否曾经需要 **将图像转换为 JSON**，但不确定哪个库既能提供原始文本又能提供精确的单词坐标？你并不孤单。许多开发者在尝试从图像文件（尤其是收据）中提取文本，同时需要机器可读的 JSON 负载用于下游处理时，都会遇到这个难题。

在本教程中，我们将完整演示一个 **Aspose OCR C# 示例**，展示如何从图像中提取文本、识别收据图像，并为每个单词输出 **JSON 边界框**。完成后，你将拥有一个可直接运行的控制台应用，它会打印格式良好的 JSON 字符串，供任何 API、数据库或分析管道使用。

> **学习成果**  
> • 一个完整的 C# 项目，能够 **将图像转换为 JSON**  
> • 了解为何要启用 `IncludeBoundingBoxes`（它是 `json bounding boxes` 的关键）  
> • 处理不同图像格式和语言的技巧  

让我们开始吧。

---

## 你需要准备的环境

在编写代码之前，请确保已安装以下前置条件：

- **.NET 6.0 SDK**（或更高版本）——代码以 .NET 6 为目标，也可在 .NET Framework 4.7+ 上运行。  
- **Aspose.OCR for .NET** NuGet 包——可通过 `dotnet add package Aspose.OCR` 添加。  
- 一个示例收据图像（`receipt.jpg`），放置在项目可以引用的文件夹中。  
- Visual Studio 2022、VS Code 或任意你喜欢的 IDE。

无需其他外部服务；所有操作均在本地完成。

---

## 将图像转换为 JSON – 概览

核心思路很简单：加载图像，指示 Aspose OCR 识别英文（或任何受支持的语言），启用边界框输出，最后以 **JSON** 格式获取结果。库会完成所有繁重工作——OCR、版面分析以及 JSON 序列化。

下面是一张高层次的流程图（想象一张小图片）：

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

这张小图概括了我们即将实现的完整流水线。

---

## 第一步：创建项目并安装 Aspose OCR

首先，新建一个控制台项目并引入 Aspose OCR 包。

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **专业提示：** 如果使用 Visual Studio，右键点击项目 → *Manage NuGet Packages* → 搜索 **Aspose.OCR** 并安装最新稳定版（当前 23.12）。

---

## 第二步：加载待识别的图像

我们将使用 `OcrImage.FromFile` 方法读取收据图像。确保路径指向真实文件，否则会抛出 `FileNotFoundException`。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

如果你的图像与 `.csproj` 位于同一目录，只需使用 `"receipt.jpg"` 即可。

---

## 第三步：配置 OCR 选项以获取 JSON 边界框

当我们同时设置 `OutputFormat = OutputFormat.Json` **以及** `IncludeBoundingBoxes = true` 时，魔法就会发生。前者指示 Aspose 将结果序列化为 JSON，后者为每个单词添加 `x、y、width、height`，正是你需要的 `json bounding boxes`。

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

如果需要更高分辨率或其他语言，也可以调整 `ocrOptions.Dpi` 或 `ocrOptions.Language`。

---

## 第四步：执行识别 – 从图像中提取文本

现在调用 `Recognize`。该方法返回一个包含 JSON 字符串、原始文本等信息的 `OcrResult` 对象。

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

若需识别其他语言，只需将 `Language.English` 替换为 `Language.Spanish`、`Language.French` 等。Aspose 开箱即支持超过 30 种语言。

---

## 第五步：输出结果 – 你的 JSON 负载

最后，我们将 JSON 打印到控制台。实际项目中，你可能会将其写入文件或推送到服务。

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

运行程序后，应生成类似下方代码块的 JSON 文档。

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

请注意，每个单词现在都携带了 **JSON 边界框**——这对于在 UI 上叠加显示或供下游解析器使用非常理想。

---

## 完整可运行示例

下面是完整的、可直接复制粘贴的程序代码。没有隐藏部分，也没有外部调用——纯粹的 C# 示例。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **注意事项：**  
> • **文件路径错误** – 请再次确认图像所在位置。  
> • **缺少 NuGet 包** – 确保已引用 `Aspose.OCR`。  
> • **不受支持的图像格式** – 为获得最佳效果，请使用 JPEG、PNG、BMP 或 TIFF。

---

## 常见问题与边缘情况

### 能否将 **PDF 页面** 转换为 JSON，而不是 JPEG？

可以。先使用（例如）`Aspose.PDF` 将 PDF 页面转换为图像，然后将该图像输入相同的 OCR 流程。由于 OCR 步骤只关心栅格数据，JSON 输出将保持一致。

### 收据模糊不清怎么办？

提升 `ocrOptions` 中的 DPI。例如：

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

更高的 DPI 可能会增加内存占用，需要在质量与性能之间取得平衡。

### 同一张收据上需要 **多语言**（如英文 + 西班牙文）怎么办？

可以传入语言数组：

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose 会按指定顺序尝试识别每种语言。

### 如何将 JSON 写入文件？

只需将 `Console.WriteLine` 那行代码替换为：

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

这样就会生成一个持久化文件，便于交付给其他服务使用。

---

## 可视化概览

![将图像转换为 JSON 示例](convert-image-to-json.png "将图像转换为 JSON 示例")

*该截图展示了运行演示后控制台输出的 JSON 负载。*

---

## 结论

我们已经演示了如何使用 Aspose OCR 在 C# 中 **将图像转换为 JSON**。通过配置 `OutputFormat` 与 `IncludeBoundingBoxes`，你可以 **从图像中提取文本**、**识别收据图像**，并为每个单词获取精确的 **JSON 边界框**。完整、可运行的代码已在上方代码块中提供，直接复制到任意 .NET 项目即可使用。

接下来可以尝试将 JSON 输入前端查看器，实现单词高亮；或将数据送入机器学习模型，对收据的项目进行分类。你也可以探索其他语言、更高 DPI 设置，或在循环中批量处理多张图像。

如果遇到问题，请记得检查文件路径、DPI 设置以及语言数组等细节。欢迎在你为此演示创建的 GitHub 仓库中留言或提交 Issue。祝编码愉快，玩转图片到结构化 JSON 的转换！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}