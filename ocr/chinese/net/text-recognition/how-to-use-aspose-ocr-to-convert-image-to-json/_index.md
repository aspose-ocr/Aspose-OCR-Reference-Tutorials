---
category: general
date: 2026-03-15
description: 如何在 C# 中使用 Aspose OCR 从图像提取文本并将图像转换为 JSON。学习快速识别 PNG 中的文字并获取结构化输出。
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: zh
og_description: 如何使用 Aspose OCR 从图像中提取文本并在 C# 中将图像转换为 JSON。本指南将带您逐步识别 PNG 中的文本并获取结构化输出。
og_title: 如何使用 Aspose OCR 将图像转换为 JSON
tags:
- Aspose
- OCR
- C#
- JSON
title: 如何使用 Aspose OCR 将图像转换为 JSON
url: /zh/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR 将图像转换为 JSON

当开发者需要从图片中提取文本时，如何使用 Aspose OCR 是一个常见问题。如果您想 **将图像转换为 JSON** 或 **从 PNG 识别文本**，本指南为您提供完整的实用解决方案——没有冗余，只是一步到位的实践。

接下来几分钟，我们将逐步演示您所需的一切：安装库、配置引擎以输出 JSON、加载收据 PNG、运行 OCR，最后将结果写入 `.json` 文件。完成后，您只需一次方法调用即可 **从图像中提取文本**，并且会了解每一步的意义。

> **小贴士：** Aspose OCR 支持多种图像格式（PNG、JPEG、BMP、TIFF）。下面的相同代码即可处理所有这些格式，无需编写特定格式的逻辑。

## 您需要的条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.6+）  
- 有效的 Aspose.OCR NuGet 包（免费试用或已授权）  
- 您想要处理的图像文件（例如 `receipt.png`）  
- Visual Studio、VS Code 或您偏好的任何 C# 编辑器  

就这些——没有额外的依赖，也没有外部服务。准备好了吗？让我们开始吧。

![如何使用 Aspose OCR 引擎](image-placeholder.png "如何使用 Aspose OCR 引擎")

## 如何使用 Aspose OCR – 配置 JSON 输出

在 **如何使用 aspose** 进行 OCR 时，首先需要做的事是创建一个 `OcrEngine` 实例并让它输出 JSON。这个小小的配置开关可以让您免去后续手动序列化结果的步骤。

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**为什么这很重要：** 将 `OutputFormat` 设置为 `Json` 表示 OCR 引擎已经将文本组织为页面、行和单词的层级结构。您以后无需解析原始字符串，这使得下游处理——例如将数据写入数据库——更加简洁。

## 使用 Aspose OCR 将图像转换为 JSON

引擎配置完成后，让我们更详细地讨论 **将图像转换为 JSON** 的部分。

1. **加载图像** – `Image.FromFile` 适用于任何受支持的格式。如果您处理的是流（例如上传的文件），可以改用 `Image.FromStream`。  
2. **运行 `Recognize`** – 此方法返回一个 `OcrResult` 对象。由于我们将输出设置为 JSON，`ocrResult.Text` 已经包含 JSON 字符串。  
3. **写入文件** – `File.WriteAllText` 是持久化 JSON 最简单的方式。如果需要将其存储到云存储桶，只需将此行替换为相应的 SDK 调用。

### 预期的 JSON 输出

典型的 JSON 负载如下（为简洁起见已截断）：

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

现在，您可以将此结构输入到任何下游系统——无论是报表工具、机器学习模型，还是简单的日志文件。

## 使用 Aspose OCR 从图像中提取文本

如果您只需要原始字符串（即不关心 JSON），只需将输出格式切换回纯文本：

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**何时选择纯文本？**  
- 快速调试或控制台输出。  
- 需要进行自定义后处理的场景（例如正则表达式提取）。  

但请记住，使用 JSON **从图像中提取文本** 能提供位置信息——这对于在 UI 中高亮文本或与表单字段对齐非常有用。

## 从 PNG 文件识别文本

PNG 是一种无损格式，相比高度压缩的 JPEG，往往能获得更好的 OCR 准确率。以下是快速检查清单，帮助您在 **从 PNG 识别文本** 时获得最佳效果：

| 检查项               | 帮助原因                                             |
|----------------------|------------------------------------------------------|
| 使用 300 DPI 以上    | 更高的分辨率为引擎提供更多像素，提升识别效果。       |
| 保持图像为灰度       | 降低噪声；Aspose OCR 会自动转换，但预处理可以加快速度。 |
| 去除背景杂乱         | 干净的背景可提升置信度分数。                         |

如果遇到置信度分数偏低，可尝试提高 DPI 或在将图像传入 Aspose 前使用简单的阈值过滤。

## 编程方式提取 OCR 结果

除了保存 JSON，您可能还想以编程方式读取特定字段——例如收据上的总金额。由于 JSON 包含层级结构，您可以将其反序列化为 C# 对象：

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

现在，您可以使用 LINQ 查询 `ocrData`：

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**为什么可行：** JSON 已经指明了每个单词在页面上的位置，即使布局略有变化，您也能可靠地定位字段。

## 边缘情况与常见陷阱

- **空结果：** 如果 `ocrEngine.Recognize` 返回 `null`，可能是图像不受支持或已损坏。务必进行检查：

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **大文件：** 对于多兆字节的图像，考虑在 OCR 前对图像进行流式处理或调整大小，以避免占用过多内存。

- **许可证问题：** 试用版会在输出中添加水印。确保在程序开始时加载许可证：

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **非拉丁脚本：** Aspose OCR 支持多种语言，但必须相应设置 `Language` 属性（例如 `ocrEngine.Configuration.Language = Language.English;`）。

## 完整工作示例（可直接复制）

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}