---
category: general
date: 2026-03-26
description: 使用 Aspose OCR 在 C# 中识别 PNG 文本并提取收据数据。将图像转换为 JSON‑L，并在完整示例中通过 OCR 处理收据。
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: zh
og_description: 使用 Aspose OCR 在 C# 中识别 PNG 文本并将收据转换为 JSON‑L。提供完整的逐步代码和技巧。
og_title: 从 PNG 识别文本 – Aspose OCR C# 指南
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: 从 PNG 识别文本 – Aspose OCR C# JSON‑L 教程
url: /zh/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 PNG 识别文本 – 完整 Aspose OCR C# 指南

是否曾经需要**从 png 文件中识别文本**，却不确定哪个库能提供干净、逐行的结果？你并不孤单。在许多小型业务应用中，收据以 PNG 图像形式存在，提取金额、日期或商户名称是日常的痛点。

好消息是？只需几行 C# 代码和**Aspose OCR**库，你就可以**从收据中提取文本**，随后**将图像转换为 jsonl**，供下游分析使用。在本教程中，我们将完整演示整个流程——加载 PNG、运行 OCR、将每行写入 JSON‑L 文件——让你能够**使用 OCR 处理收据**。

我们会覆盖所有必需内容：所需的 NuGet 包、完整可运行的程序、每一步为何重要的解释，以及在收据杂乱时你会感激的实用技巧。无需查阅外部文档；只需复制、粘贴、运行并根据需要调整。

---

## 你将学到

- 如何使用 `Aspose.OCR` **从 png 识别文本**。
- 如何 **从收据中提取文本** 行对象并获取置信度分数。
- 如何 **将图像转换为 jsonl**，使每个 OCR 行成为单独的 JSON 对象。
- 如何 **端到端处理收据**，并处理空图像或低置信度行等边缘情况。
- 常见 OCR 问题的排查技巧以及提升准确率的方法。

### 前置条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）。
- Visual Studio 2022 或任意你喜欢的 IDE。
- 有效的 Aspose OCR 许可证（可从 Aspose.com 获取免费临时许可证）。
- 将示例收据保存为 `receipt.png`，放在你可控制的文件夹中。

---

## 第一步：使用 Aspose OCR 识别 png 文本

我们首先需要一个已初始化的 `OcrEngine`。该对象保存 OCR 引擎的设置（语言、检测模式等）。默认使用英语并自动检测页面布局，足以处理大多数收据。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**为何重要：**  
`OcrEngine` 是核心组件；只创建一次并在多张图片间复用，可降低内存开销。如果需要其他语言（例如西班牙语收据），可在调用 `Recognize` 前设置 `ocrEngine.Language = OcrLanguage.Spanish;`。

---

## 第二步：从收据行中提取文本

`OcrResult` 包含一个名为 `Lines` 的集合。每行都保存原始文本和置信度分数（0‑100）。提取这些信息后，你可以对低置信度行进行丢弃或标记，以便人工复核。

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**为何要转义 JSON：**  
收据文本可能包含引号（`"`）或反斜杠（`\`），会导致普通 JSON 字符串破裂。`EscapeJson` 方法确保生成有效的 JSON 行。

**输出示例：**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

每行都是独立记录，完美适用于流式写入数据湖或喂入机器学习模型。

---

## 第三步：将图像转换为 JSONL – 处理边缘情况

在批量处理收据时，可能会遇到空白、损坏或置信度极低的图片。让我们让管道更健壮一些。

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**为何要过滤：**  
在褪色纸张上打印的收据会产生低置信度的杂散字符。通常将阈值设为 80 % 以下的行剔除，可去除噪声且保留有用数据。

---

## 第四步：端到端处理收据示例

将所有内容整合，下面是**完整、可直接运行**的程序。将 `YOUR_DIRECTORY` 替换为存放 PNG 文件的文件夹路径。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**运行代码步骤：**  
1. 在项目文件夹打开终端。  
2. `dotnet add package Aspose.OCR` – 安装库。  
3. `dotnet run` – 你应看到成功信息，并生成 `receipt.jsonl` 文件。

**预期结果：** 一个按行分隔的 JSON 文件，每行对应收据中的一行文本，并包含置信度分数。现在可以将该文件导入 Power BI、Elastic 或任何支持 JSON‑L 的分析工具。

---

## 常见问题与专业技巧

| 问题 | 产生原因 | 快速解决方案 |
|------|----------|--------------|
| **输出为空** | 图像路径错误或文件不是 PNG。 | 检查路径，使用 `File.Exists(imagePath)`。 |
| **出现乱码** | DPI 过低或 PNG 压缩过度。 | 使用至少 300 dpi 的扫描；避免强力 JPEG 压缩。 |
| **低置信度行过多** | 热敏纸打印的收据褪色。 | 提高 `minConfidence` 阈值或对图像进行预处理（对比度/阈值化）。 |
| **JSON 解析错误** | 收据文本中未转义的引号。 | 保留 `EscapeJson` 辅助方法，或改用 `System.Text.Json` 实现更稳健的序列化。 |

**专业技巧：** 若需提取特定字段（如总金额），可在生成 JSON‑L 文件后，对每个 `line.Text` 使用简单正则表达式。这种做法将 OCR 与业务逻辑分离，调试更方便。

---

## 扩展方案

- **批量处理：** 将 `Main` 逻辑包装在对目录下所有 PNG 文件的 `foreach` 循环中。  
- **多语言支持：** 在 `Recognize` 前设置 `ocrEngine.Language = OcrLanguage.Spanish;`（或任意受支持语言）。  
- **结构化输出：** 与其逐行 JSON，不如构建 `Receipt` 对象，包含 `Date`、`Merchant`、`Total` 等属性，然后一次性序列化。

所有这些变体仍然在核心上**将图像转换为 jsonl**，因此可以在不改动 OCR 部分的前提下，随意替换下游消费者。

---

## 结论

我们已经演示了如何使用 Aspose OCR **从 png 文件中识别文本**、**从收据中提取文本**，以及**将图像转换为 jsonl**，以便轻松进行下游处理。完整的、独立的 C# 程序展示了整个工作流——从加载 PNG、处理边缘情况，到写入干净的 JSON‑L 文件——让你能够立即在项目中**使用 OCR 处理收据**。

尝试使用几张示例收据，调整置信度阈值，你会发现嘈杂的图像堆快速转化为结构化数据，准备好进行分析。当你熟悉后，可探索批量处理或加入小型机器学习模型，实现自动费用类别分类。

有问题或发现了巧妙的改进？欢迎在下方留言——祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}