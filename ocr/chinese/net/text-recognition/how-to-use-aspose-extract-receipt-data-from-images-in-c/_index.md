---
category: general
date: 2026-04-04
description: 学习如何使用 Aspose 提取收据数据、加载收据图像并对收据图像进行 OCR，完整的 C# 示例。为开发者提供的逐步指南。
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: zh
og_description: 如何使用 Aspose 从扫描的收据图像中提取收据数据。完整的 C# 代码、解释以及 OCR 收据图像处理技巧。
og_title: 如何使用 Aspose – 从图像中提取收据数据
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: 如何使用 Aspose —— 在 C# 中从图像提取收据数据
url: /zh/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose – 从图像中提取收据数据（C#）

是否曾想过 **how to use Aspose** 从收据照片中提取结构化信息？你并非唯一。无论是构建费用跟踪应用还是自动化发票录入，痛点都是相同的：你有一张 PNG 或 JPEG，需要商家名称、日期和总金额，而不想手动输入。

事实是——Aspose.OCR 让整个流程变得轻而易举。在本教程中，我们将演示如何加载收据图像、运行 OCR，并最终使用几行 C# 提取收据数据。完成后，你将拥有一个可运行的控制台程序，直接在控制台打印商家、日期和总金额。

> **快速上手：** 如果你只需要代码，请直接跳到底部的“Complete Working Example”章节并复制粘贴。

## 所需条件

- **.NET 6.0 或更高**（API 支持 .NET Core 和 .NET Framework）
- **Aspose.OCR for .NET** NuGet 包 (`Install-Package Aspose.OCR`)
- 本地保存的示例收据图像（PNG、JPG 或 BMP）
- Visual Studio 2022 或任何支持 C# 项目的编辑器

不需要其他第三方库。唯一的前提是对 C# 控制台应用有基本了解——如果你已经写过 “Hello World”，就可以开始了。

## 第一步 – 安装并引用 Aspose.OCR

要 **how to use Aspose**，首先需要在项目中添加该库。打开 Package Manager Console 并运行：

```powershell
Install-Package Aspose.OCR
```

或者，使用 NuGet UI 搜索 “Aspose.OCR”。安装后，在文件顶部添加所需的命名空间：

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **专业提示：** 保持 NuGet 包为最新。截止今天（2026 年 4 月），最新稳定版是 23.11.0，包含对高分辨率收据 OCR 的性能改进。

## 第二步 – 加载收据图像

当你 **load receipt image** 文件时，通常有两种来源：本地路径或来自网络请求的流。为了本教程的简洁，我们将直接从磁盘读取：

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

将 `YOUR_DIRECTORY/receipt.png` 替换为收据文件的实际路径。如果处理用户上传，可以将 `MemoryStream` 传递给 `ImageStream.FromStream`。

> **为什么重要：** 指定语言（English）告诉 OCR 引擎预期的字符集，减少误识别——在 **ocr receipt image** 包含数字和符号时尤为重要。

## 第三步 – 运行 OCR 并捕获布局信息

OCR 步骤不仅仅输出原始文本；它还捕获布局，这对后续的结构化提取至关重要。

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

`Recognize()` 完成后，`ocrEngine` 包含纯文本以及每个单词的位置数据。这是下一步的基础，我们将让 Aspose 自动“**how to extract receipt**”字段。

## 第四步 – 初始化 Layout Recognizer

Aspose 提供了 `LayoutRecognizer` 类，了解收据通常的组织方式（商家在顶部，日期行，合计在底部）。只需传入已配置的 OCR 引擎：

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

在内部，识别器使用一系列启发式规则——例如查找货币符号或日期模式——将原始文本映射到语义字段。

## 第五步 – 提取结构化收据数据

现在进入精彩部分：**extract receipt data**。一次方法调用即可完成繁重工作：

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

`receiptData` 是类型为 `ReceiptData`（定义在 `Aspose.OCR.Structured`）的对象。它包含三个主要属性：

- `Merchant` – 商店名称
- `Date` – 购买日期，类型为 `DateTime`（如果检测到）
- `TotalAmount` – 总金额，类型为 `decimal`

如果引擎未找到某个字段，属性将为 `null` 或 `0`。如有需要，可添加回退逻辑（例如提示用户确认）。

## 第六步 – 显示提取的信息

最后，将结果输出到控制台。在这里你可以看到劳动的成果：

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

格式字符串（`:d` 和 `:C`）分别生成短日期和货币字符串，使输出易于阅读。

### 预期输出

假设收据属于 “Coffee Corner”，日期为 2025‑12‑01，总额为 $4.75，控制台将显示：

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

如果某个字段缺失，你会看到空行或默认值——这对调试非常有帮助。

## 边缘情况与常见陷阱

### 1. 低分辨率图像

如果收据图像模糊或低于 150 dpi，OCR 准确率会显著下降。在将图像传递给 Aspose 之前，使用简单的双线性过滤器进行放大可以提升效果。

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. 非英文收据

主要示例使用 `Language.English`。对于多语言收据，将 `Language` 设置为相应的枚举（例如 `Language.French`），如果不确定，可使用 `Language.AutoDetect`。

### 3. 单张图像中包含多张收据

Aspose 的布局识别器期望每张图像只有一张收据。如果你有多张收据并排的照片，需要预处理图像——在运行 OCR 前将每张收据裁剪为单独的文件。

### 4. 缺少货币符号

有时总金额没有 `$` 符号。识别器仍能捕获数字，但可能需要后处理字符串以确保小数点位置正确。

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## 生产环境的专业提示

- **缓存 OCR 引擎**，如果批量处理大量收据；复用同一个实例可减少分配开销。
- **记录原始 OCR 文本** (`ocrEngine.Text`) 以便审计。当某字段提取失败时，这很有用。
- **将整个流程包裹在 try/catch 中**，并提供友好的错误信息（例如 “Unable to read receipt, please upload a clearer image”）。

## 完整工作示例

下面是一个完整的控制台应用程序示例，可直接编译运行。只需替换图像路径，即可使用。

```csharp
// ------------------------------------------------------------
// How to Use Aspose – Extract Receipt Data from Images (C#)
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Structured;

namespace ReceiptExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create and configure the OCR engine for English language
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the receipt image you want to process
            // 👉 Make sure the file exists; otherwise an exception will be thrown.
            const string imagePath = "YOUR_DIRECTORY/receipt.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Run OCR – this also captures layout information
            ocrEngine.Recognize();

            // 4️⃣ Initialize the layout recognizer with the OCR engine
            var layoutRecognizer = new LayoutRecognizer(ocrEngine);

            // 5️⃣ Extract structured receipt data (merchant, date, total amount)
            var receiptData = layoutRecognizer.ExtractReceiptData();

            // 6️⃣ Display the extracted information
            Console.WriteLine($"Merchant: {receiptData.Merchant ?? "Not detected"}");
            Console.WriteLine($"Date:     {(receiptData.Date == DateTime.MinValue ? "Not detected" : receiptData.Date.ToShortDateString())}");
            Console.WriteLine($"Total:    {(receiptData.TotalAmount == 0 ? "Not detected" : receiptData.TotalAmount.ToString("C"))}");

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**运行代码**

1. 创建一个新的 .NET 控制台项目 (`dotnet new console -n ReceiptExtractor`)。
2. 添加 Aspose.OCR 包 (`dotnet add package Aspose.OCR`)。
3. 用上面的代码片段替换生成的 `Program.cs`。
4. 将收据图像放置在你指定的路径下。
5. 构建并运行 (`dotnet run`)。

你应该会看到商家、日期和总额，正如前面示例所示。

## 总结

在本指南中，我们介绍了 **how to use Aspose** 来 **load receipt image**，运行 **ocr receipt image**，并最终使用几行代码 **extract receipt data**。关键点是 Aspose.OCR 完成了繁重工作——配置好 OCR 引擎后，`LayoutRecognizer` 能将原始文本转换为可靠的结构化对象。

下一步？尝试将提取的值写入数据库，生成 PDF 收据摘要，甚至将其输入机器学习模型进行费用分类。你还可以尝试其他结构化文档类型，如发票或运单——Aspose 的 `ExtractInvoiceData` 以非常相似的方式工作。

对边缘情况有疑问或想了解如何处理多页 PDF？请留言或查阅官方 Aspose.OCR 文档获取高级案例。祝编码愉快，尽情享受 **how to use Aspose** 在收据自动化中的简便！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}