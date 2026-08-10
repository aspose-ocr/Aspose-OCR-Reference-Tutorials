---
category: general
date: 2026-04-26
description: 使用 Aspose.OCR 在 C# 中提取图像文字，并在几分钟内学习如何将图像转换为 JSON 和 XML 格式。
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: zh
og_description: 使用 Aspose.OCR 在 C# 中提取图像文本。一步步学习如何即时将结果转换为 JSON 和 XML。
og_title: 在 C# 中从图像提取文本 – 转换为 JSON 和 XML
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: 在 C# 中从图像提取文本 – 转换为 JSON 和 XML
url: /zh/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本（C#）– 转换为 JSON 与 XML

是否曾经需要在 .NET 项目中 **从图像中提取文本**，但对“到底如何获取数据？”感到束手无策？你并不孤单。在许多真实场景的应用中——比如发票处理、收据扫描或徽章验证——从图片中提取原始字符是第一步，也是关键步骤。  

好消息是？使用 Aspose.OCR，你只需几行代码即可完成，然后立即 **将图像转换为 JSON** 或 **将图像转换为 XML**，供下游系统使用。在本指南中，我们将逐步演示完整的可直接运行的代码，解释每一步的意义，并提供一些避免常见陷阱的技巧。

---

## 您需要的条件

- **.NET 6+**（任何近期的 SDK 都可使用；示例目标为 .NET 6）
- **Aspose.OCR for .NET** NuGet 包  
  ```bash
  dotnet add package Aspose.OCR
  ```
- 一张包含可打印文本的图像文件（PNG、JPG 等），这里以 `invoice.png` 为例。
- 一个代码编辑器——Visual Studio、VS Code 或 Rider——任选其一。

就这些。无需额外的 OCR 引擎，也不需要外部服务，只需一个 NuGet 包。

---

## 步骤 1：设置 OCR 引擎 – 如何从图像中提取文本

首先我们创建一个 `OcrEngine` 实例并指向图像文件。此步骤是基础；如果图像未正确加载，引擎将无法识别任何内容。

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**为什么这很重要：**  
- `OcrEngine` 封装了所有低层的图像预处理（二值化、去倾斜）。  
- 通过 `ImageStream.FromFile` 加载图像可确保引擎读取到精确的字节，保留 DPI 和色深——这两者都会影响识别准确率。  

> **专业提示：** 如果你的源图像来自流（例如通过 Web API 上传），请使用 `ImageStream.FromStream(yourStream)` 而不是 `FromFile`。

---

## 步骤 2：告知引擎预期的语言 – 准确提取图像文本

Aspose.OCR 支持多种字母表。指定正确的语言可以缩小字符集范围并提升准确度。

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**原因：**  
当你将 `Language.Latin` 设置为目标语言时，OCR 引擎会忽略西里尔字母或亚洲字符，从而减少误报。如果以后需要处理多语言文档，可以切换为 `Language.Multilingual` 或组合多种语言。

---

## 步骤 3：运行识别过程 – 一次调用提取图像文本

现在我们真正进行文字识别。`Recognize` 方法返回一个 `RecognitionResult` 对象，里面包含原始文本、置信度分数，甚至布局数据。

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**原因：**  
只需调用一次 `Recognize` 即可，因为引擎内部已经完成了预处理、分割和字符分类。`Text` 属性提供纯字符串表示，便于日志记录或快速验证。

---

## 步骤 4：将结果转换为 JSON – 轻松将图像转换为 JSON

许多现代服务更倾向于使用 JSON 负载。Aspose.OCR 提供了便捷的 `ToJson` 方法，可序列化整个 `RecognitionResult`，包括置信度值和边界框。

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**为什么可能需要 JSON：**  
- **互操作性：** 前端应用（React、Angular）可以直接消费该 JSON。  
- **调试：** JSON 包含每个字符的置信度，便于将低置信度的词标记为人工复核。  

> **边缘情况：** 如果下游系统只需要纯文本，你可以提取 `recognitionResult.Text` 并自行封装成自定义的 JSON 对象，而无需使用完整的 Aspose 负载。

---

## 步骤 5：将结果转换为 XML – 为传统系统将图像转换为 XML

一些企业仍然依赖 XML 架构进行数据交换。`ToXml` 方法与 `ToJson` 类似，只是输出为 XML。

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**为什么使用 XML：**  
- **模式验证：** 你可以定义与 Aspose 输出结构相匹配的 XSD，确保合同合规。  
- **集成：** 旧版 ERP 或文档管理系统通常能够开箱即用地解析 XML。

---

## 完整可运行示例 – 一站式代码

下面是将所有步骤串联起来的完整程序。复制粘贴到新建的控制台项目（`dotnet new console`）中并运行。

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**预期输出（控制台）：**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

JSON 和 XML 文件将包含更丰富的结构，例如：

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

---

## 常见问题与边缘案例

### 如果图像模糊或旋转怎么办？

Aspose.OCR 会自动去倾斜大多数图像，但在极端情况下，你可能需要使用 `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)` 进行预处理。适当提升对比度（`ImageProcessor.AdjustContrast`）也能提升置信度分数。

### 能否从 PDF 中提取文本？

可以——先将每页 PDF 转为图像（例如使用 Aspose.PDF 或免费库 PDFium），然后将这些图像输入相同的 OCR 流程。

### 如何在同一文档中处理多种语言？

设置 `ocrEngine.Language = Language.Multilingual;` 或组合特定语言：

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

请注意，语言集合越宽泛，可能会

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}