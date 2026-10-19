---
category: general
date: 2026-03-17
description: 学习如何在 C# 中实现 OCR，以提取阿拉伯文文本、识别图像中的文字并将图像转换为文本，并附有完整的代码示例。
draft: false
keywords:
- how to perform OCR
- extract arabic text
- recognize text from image
- convert image to text
- extract text from image
language: zh
og_description: 如何在 C# 中执行 OCR？本指南将向您展示如何提取阿拉伯文文本、从图像中识别文字以及将图像转换为文本，仅需几个步骤。
og_title: 如何在 C# 中进行 OCR – 提取阿拉伯语文本
tags:
- OCR
- C#
- Arabic
- ImageProcessing
title: 如何在 C# 中进行 OCR – 从图像中提取阿拉伯文字
url: /zh/net/text-recognition/how-to-perform-ocr-in-c-extract-arabic-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中执行 OCR – 从图像中提取阿拉伯文文本

是否曾好奇 **如何执行 OCR** 来处理阿拉伯发票或扫描文档？你并不孤单——许多开发者在需要从位图中提取阿拉伯字符时会遇到瓶颈。好消息是，只需几行 C# 代码，你就可以识别图像文件中的文本，将图像转换为文本，并最终 **提取阿拉伯文本** 以供后续处理。

在本教程中，我们将逐步演示一个完整且可运行的示例，向你展示如何准确执行 OCR、每一步为何重要，以及在处理从右到左的脚本时需要注意的事项。完成后，你将能够 **从图像中提取文本**，支持阿拉伯语、乌尔都语、库尔德语或 OCR 引擎支持的任何语言。

## 前提条件

- .NET 6.0 或更高版本（代码同样可以在 .NET Core 上编译）  
- 对提供 `OcrEngine` 的 OCR 库的引用（例如 `MyOcrSdk.dll`）。  
- 包含阿拉伯文文本的图像文件，例如 `invoice_arabic.png`。  
- 对 C# 控制台应用有基本了解。  

> **专业提示：**如果你手头没有 OCR SDK，*MyOcrSdk* 的免费社区版可用于测试，并支持我们将使用的语言。

---

## 第一步 – 设置项目并导入 OCR 命名空间

在我们能够 **从图像中识别文本** 之前，需要先搭建项目框架并添加正确的 `using` 指令。

```csharp
using System;
using MyOcrSdk;          // <-- Replace with the actual namespace of your OCR library
using MyOcrSdk.IO;       // For ImageStream helper class

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the OCR workflow will go here
        }
    }
}
```

*为什么重要：* 导入正确的命名空间后，你才能使用 `OcrEngine`、`Language` 和 `ImageStream`。跳过此步骤会导致编译时错误，对新手来说非常令人沮丧。

---

## 第二步 – 创建 OCR 引擎实例（包含主要关键字）

现在我们通过实例化引擎来实际 **执行 OCR**。

```csharp
// Step 2: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

`OcrEngine` 对象是整个操作的核心；它保存配置，执行繁重的计算，并返回包含提取字符串的结果对象。可以把它看作会 **将图像转换为文本** 的“大脑”。

---

## 第三步 – 选择识别语言

Arabic, Urdu, Kurdish… all share the same script family, so we must tell the engine which language to expect. This improves accuracy dramatically.

```csharp
// Step 3: Choose the language for recognition (Arabic, Urdu, Kurdish, etc.)
ocrEngine.Config.Language = Language.Arabic;   // You can switch to Language.Urdu, etc.
```

*为什么重要：* OCR 引擎依赖语言模型。选择正确的模型可以显著降低相似字符的误识别，尤其是对从右到左的脚本。

---

## 第四步 – 加载包含文本的图像

We need a bitmap that the engine can analyse. The helper `ImageStream.FromFile` abstracts away the file‑IO details.

```csharp
// Step 4: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_arabic.png");
```

确保路径指向 **有效的图像**。如果文件缺失或损坏，引擎会抛出异常，导致 **从图像中提取文本** 失败。

---

## 第五步 – 运行 OCR 过程并获取结果

Finally, we call `Recognize()` and display the extracted string.

```csharp
// Step 5: Perform the OCR operation
var ocrResult = ocrEngine.Recognize();

// Step 6: Display the extracted text
Console.WriteLine("=== Extracted Arabic Text ===");
Console.WriteLine(ocrResult.Text);
```

`ocrResult.Text` 属性保存引擎能够读取的纯文本表示。大多数情况下，你会看到阿拉伯字符与数字的混合，非常适合后续的数据库插入或翻译等处理。

### 预期输出

```
=== Extracted Arabic Text ===
فاتورة رقم: 12345
التاريخ: 2026/03/15
المبلغ: 2500.00 ريال
...
```

如果出现乱码，请再次检查语言设置并确保图像分辨率足够（300 dpi 以上为理想）。

---

## 完整可运行示例

Below is the **complete, self‑contained program** you can copy‑paste into a new console project and run right away.

```csharp
// Full OCR demo – extracts Arabic text from an image
using System;
using MyOcrSdk;
using MyOcrSdk.IO;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Set language – Arabic (change to Urdu or Kurdish if needed)
            ocrEngine.Config.Language = Language.Arabic;

            // 3️⃣ Load the source image
            // Replace YOUR_DIRECTORY with the folder that holds your PNG/JPG
            string imagePath = @"YOUR_DIRECTORY/invoice_arabic.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            try
            {
                // 4️⃣ Run OCR
                var result = ocrEngine.Recognize();

                // 5️⃣ Output the text
                Console.WriteLine("=== Extracted Arabic Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – useful when you need to **extract text from image** in batch jobs
                Console.Error.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

> **注意：**如果你的 OCR SDK 需要授权，请在第 1 步之前初始化授权（例如 `OcrEngine.SetLicense("YOUR_LICENSE_KEY");`）。此行为简洁起见已省略。

---

## 处理常见边缘情况

| 情况 | 为什么会发生 | 快速解决方案 |
|-----------|----------------|-----------|
| **模糊或低分辨率图像** | OCR 准确率下降到 70 % 以下 | 以 300 dpi 扫描，或在送入引擎前使用双三次算法放大。 |
| **混合语言（阿拉伯语 + 英语）** | 引擎可能在第一个语言块后停止 | 启用多语言模式：`ocrEngine.Config.Language = Language.Arabic | Language.English;` |
| **从右到左显示问题** | 控制台左到右打印字符，导致阿拉伯文显示颠倒 | 使用 `Console.OutputEncoding = System.Text.Encoding.UTF8;` 并使用支持 RTL 脚本的终端。 |
| **大型 PDF 拆分为多页** | 内存消耗激增 | 一次处理一页：将每页加载为单独的图像并重复 OCR 流程。 |
| **特殊符号（货币、日期）** | 某些 OCR 模型将其视为噪声 | 使用正则表达式对 `ocrResult.Text` 进行后处理，以规范已知模式。 |

---

## 扩展解决方案 – 从 OCR 到数据提取

既然你已经 **了解如何执行 OCR**，可能会想：*提取的阿拉伯文本可以做什么？* 以下是一些自然衍生的思路：

1. **解析发票** – 使用正则表达式提取发票号码、日期和总额。  
2. **调用翻译 API** – 将阿拉伯字符串发送至 Azure Translator 或 Google Cloud Translate。  
3. **存入数据库** – 将清理后的文本插入 SQL 表用于报表。  
4. **触发工作流** – 与消息队列（如 RabbitMQ）结合，启动下游处理。  

所有这些场景都基于相同的核心操作：**将图像转换为文本**，随后对结果进行处理。

## 结论

我们已经覆盖了在 C# 中 **如何执行 OCR** 以 **提取图像中的阿拉伯文本** 所需的全部知识。从项目设置、实例化 `OcrEngine`、配置语言、加载位图、运行识别到打印结果，我们一步步演示。我们还讨论了常见陷阱，并展示了如何将基本流程扩展到实际生产线中。

动手试试吧——更换图像路径、改为乌尔都语，或将输出接入数据库。一旦你能够可靠地 **从图像中识别文本** 并 **将图像转换为文本**，就没有限制。

### 你可能想要了解的相关主题

- **使用 Tesseract OCR（开源替代）提取图像文本**  
- **批量 OCR 处理** 用于数千个扫描 PDF  
- **通过图像预处理（阈值化、去噪）提升 OCR 准确率**  
- **在 .NET UI 框架（WPF、WinForms）中处理从右到左脚本**  

如果遇到任何问题，欢迎留言，或分享你在项目中如何改编此模式。祝编码愉快！  

![how to perform OCR example](images/ocr_flow.png "how to perform OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}