---
category: general
date: 2026-02-13
description: 如何使用 Aspose OCR 快速读取收据并使用正则表达式提取金额。学习使用 OCR 步骤式处理收据。
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: zh
og_description: 如何使用 Aspose OCR 和正则表达式在 C# 中读取收据。本指南展示了如何使用 OCR 处理收据并提取总金额。
og_title: 如何在 C# 中读取收据 – 完整的 OCR 与正则表达式教程
tags:
- OCR
- C#
- Regex
- Aspose
title: 如何在 C# 中读取收据 – OCR + 正则表达式指南
url: /zh/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

no images.

Proceed.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中读取收据 – OCR + 正则指南

有没有想过 **如何读取收据** 图像而不需要手动输入每一行？在许多小型业务应用中，你需要从收据照片中提取总金额，手动操作就失去了自动化的意义。好消息是？使用 Aspose OCR，你可以让引擎完成繁重的工作，然后用一个简单的正则表达式定位总额。在本教程中，我们将演示 **使用 OCR 处理收据** 的完整流程，使用正则提取金额，并得到一个可直接使用的总值。

你将看到一个完整、可运行的示例，了解收据语言模型为何重要，并获取处理边缘情况（如不同货币符号或缺少 “Total” 标签）的技巧。无需外部文档——所有内容都在这里。

## 你将学到

- 如何为收据专用识别设置 Aspose OCR（`Receipt` 语言模型会自动去倾斜和去噪图像）。  
- 如何应用正则表达式 **使用正则提取金额**，该模式适用于大多数美国风格的收据。  
- 如何处理常见变体，如 “TOTAL”、 “Total:” 或 “Grand Total – $12.34”。  
- 如何安全输出结果以及在未找到匹配时的处理方式。  

**先决条件**：.NET 6+（或 .NET Framework 4.7+），有效的 Aspose OCR 许可证或试用版，以及本地保存的收据图像。仅此即可——不需要除 Aspose.OCR 之外的额外 NuGet 包。

---

## 第 1 步 – 安装 Aspose OCR 并准备项目

### 为什么重要

Aspose OCR 提供了专为 **使用 OCR 处理收据** 设计的模型，能够将皱巴巴的纸张拉直并忽略背景噪声。使用通用文本模型会导致更多错误，尤其是在低分辨率扫描时。

### 代码

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **专业提示：** 将许可证文件放在源码控制目录之外，以避免意外提交。

---

## 第 2 步 – 为收据识别配置 OCR 引擎

### 为什么重要

`Receipt` 语言模型内置去倾斜和去噪功能，显著提升了对经常折叠或皱起的真实收据的识别准确率。

### 代码

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## 第 3 步 – 从收据图像中识别文本

### 为什么重要

在应用任何正则之前，你需要原始文本。`RecognizeImage` 方法返回一个包含完整字符串、置信度分数等信息的 `OcrResult`，如果以后需要可以进一步使用。

### 代码

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**预期的 OCR 输出（示例）**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## 第 4 步 – 构建正则以 **使用正则提取金额**

### 为什么重要

收据格式多种多样，但 “Total” （或其变体）后跟美元金额是可靠的锚点。下面的模式容忍可选空格、冒号、连字符以及可选的 `$` 符号。

### 代码

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**模式解释**

| 部分 | 含义 |
|------|------|
| `Total` | 匹配单词 “Total”（不区分大小写）。 |
| `\s*[:\-]?` | 允许任意空白，后跟可选的冒号或连字符。 |
| `\s*\$?` | 可选空白和可选美元符号。 |
| `(\d+(\.\d{2})?)` | 捕获一个或多个数字，后可跟小数点和两位小数。 |

---

## 第 5 步 – 输出提取的总额或处理缺失数据

### 为什么重要

即使是最好的 OCR 也可能漏掉某个词，尤其是在模糊的收据上。提供优雅的回退可以防止崩溃，并为自定义逻辑（例如让用户确认）提供钩子。

### 代码

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**示例控制台输出**

```
Total: $12.25
```

---

## 完整工作示例 – 所有步骤合并在一个文件中

下面是一个可以直接复制粘贴到控制台项目中的完整自包含程序。它包含注释、错误处理以及可选的许可证加载代码。

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**运行程序**

1. 创建一个新的控制台项目（`dotnet new console -n ReceiptReader`）。  
2. 添加 Aspose.OCR NuGet 包（`dotnet add package Aspose.OCR`）。  
3. 将 `YOUR_DIRECTORY/receipt.jpg` 替换为实际的收据图像路径。  
4. 构建并运行（`dotnet run`）。  

如果一切顺利，你将看到 OCR 输出后紧跟 `Total: $xx.xx`。

---

## 处理边缘情况与常见变体

### 1. 不同的货币符号

如果你处理欧元（€）或英镑（£），可以扩展模式：

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. 缺少 “Total” 标签

有些收据只显示 “Grand Total”。可以添加交替匹配：

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. 多个总额（例如 “Subtotal” 与 “Total”）

如果正则匹配到第一个出现的，总额可能在后面。此时可以取 **最后** 一个匹配：

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. 低分辨率图像

- 扫描时提高 DPI（`300 DPI` 是一个不错的折中）。  
- 在将图像送入 Aspose 之前使用简单的去模糊滤波进行预处理（本指南范围之外，但值得探索）。

---

## 实战项目的专业技巧

- **缓存 OCR 结果**，如果需要提取多个字段（税额、商品等）——只需一次 OCR 开销。  
- **将原始 OCR 文本记录到数据库**，这会成为争议费用的宝贵审计轨迹。  
- 在构建 Web API 时，**在后台工作者中运行 OCR**；它可能需要几百毫秒，异步处理可以接受，但不适合同步请求。  
- **在持久化前根据业务规则验证提取的金额**（例如金额必须 > 0）。

---

## 结论

我们已经介绍了 **如何在 C# 中读取收据** 图像并使用 Aspose OCR，然后 **使用正则提取金额** 以可靠地找到总额行。通过利用 `Receipt` 语言模型，你可以获得去倾斜、去噪的文本，而简洁的正则表达式能够处理大多数格式差异。上面的完整代码片段可以直接放入任何 .NET 控制台或服务项目，额外的边缘情况建议为生产使用奠定了坚实基础。

准备好下一步了吗？尝试扩展解决方案以提取单项商品、自动计算税额，或与费用跟踪 API 集成。如果遇到破坏模式的收据，记住 **正则查找总额** 只是起点——你随时可以根据特定地区调整模式。

祝编码愉快，愿你的收据处理快速、准确、全自动！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}