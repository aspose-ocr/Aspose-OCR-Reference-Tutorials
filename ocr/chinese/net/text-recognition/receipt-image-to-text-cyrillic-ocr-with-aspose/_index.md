---
category: general
date: 2026-04-01
description: 学习如何使用 Aspose OCR 将收据图像转换为文本。本指南展示了如何提取西里尔文文本、加载用于 OCR 的图像，以及高效识别西里尔字符。
draft: false
keywords:
- receipt image to text
- extract cyrillic text
- load image for ocr
- recognize cyrillic characters
- create OCR engine
language: zh
og_description: 使用 Aspose OCR 将收据图像转换为文本。学习提取西里尔文文本、加载图像进行 OCR，并在 C# 中识别西里尔字符。
og_title: 收据图片转文字 – 使用 Aspose 的西里尔文 OCR
tags:
- OCR
- C#
- Aspose
- Cyrillic
title: 收据图像转文本 – 使用 Aspose 的西里尔文 OCR
url: /zh/net/text-recognition/receipt-image-to-text-cyrillic-ocr-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 收据图像转文本 – 使用 Aspose 的西里尔文 OCR

是否曾需要将 **收据图像转文本**，但字符全是西里尔字母？你并不是唯一为此抓狂的人。在许多零售或会计应用中，收据可能是俄语、保加利亚语或塞尔维亚语脚本，而你仍然希望得到干净、可搜索的字符串。

在本教程中，我们将逐步演示如何 **从收据照片中提取西里尔文文本**、**加载图像进行 OCR**，以及使用 Aspose OCR 库 **识别西里尔字符**。完成后，你将拥有一个可直接运行的 C# 程序，能够将 OCR 结果写入 `.txt` 文件。

## 你需要准备的环境

- **.NET 6**（或任何近期的 .NET 版本）——代码同样适用于 .NET Framework 4.7 及以上。  
- **Aspose.OCR for .NET** NuGet 包 – `Install-Package Aspose.OCR`。  
- 一张包含西里尔文字的示例收据图像（例如 `cyrillic_receipt.jpg`）。  
- 开发环境 – Visual Studio、VS Code 或 Rider 都可以。  

无需额外的本地依赖；Aspose 已内置语言模型并在内部完成繁重的工作。

## receipt image to text – 设置 OCR 引擎

首先我们需要 **创建 OCR 引擎** 实例，并指定我们关注的语言。Aspose 让这一步变得非常简单：

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;   // language and resource handling
using System.Drawing;      // Image class
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Tell Aspose we want Cyrillic support
        ocrEngine.Language = Language.Cyrillic;

        // Optional: Pre‑load the model if you’ll run offline later
        // ResourceManager.Preload(Language.Cyrillic);
```

> **专业提示：** 预加载模型可以避免程序首次运行时的网络请求，这对桌面或嵌入式场景非常有用。

## 如何提取西里尔文文本 – 加载收据图像

引擎准备好后，我们需要 **加载图像进行 OCR**。`System.Drawing.Image` 类能够完美支持大多数位图格式。

```csharp
        // Step 3: Point to your receipt image
        string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

        // Step 4: Load the image inside a using block (ensures disposal)
        using (var image = Image.FromFile(imagePath))
        {
            // Step 5: Run the OCR process
            var recognitionResult = ocrEngine.Recognize(image);
```

如果文件未找到，`Image.FromFile` 会抛出 `FileNotFoundException`。在生产代码中，你可能需要将整段代码包裹在 `try…catch` 块中。

## 识别西里尔字符 – 获取文本

`recognitionResult` 对象包含原始文本、置信度分数，甚至还有边界框（如果你后续需要）。对于简单的 “收据图像转文本” 转换，只需将 `Text` 属性写入文件即可：

```csharp
            // Step 6: Write the extracted text to a .txt file
            string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
            File.WriteAllText(outputPath, recognitionResult.Text);

            // Quick verification: print to console
            Console.WriteLine("OCR completed. Extracted text:");
            Console.WriteLine(recognitionResult.Text);
        }
    }
}
```

运行程序后，你应该会看到类似以下的输出：

```
OCR completed. Extracted text:
СЧЕТ № 12345
Дата: 01/04/2026
Товар      Кол-во   Цена
Хлеб       2        30,00
Молоко     1        45,00
Итого:               105,00
```

这就是你期待的 **收据图像转文本** 结果。

![收据图像转文本示例](receipt-ocr-example.png "收据图像转换为文本的示例")

*图片说明：收据图像转文本转换示例，展示了 Aspose OCR 提取的西里尔字符。*

## 边缘情况与常见问题

### 如果语言模型尚未下载怎么办？

当你第一次设置 `ocrEngine.Language = Language.Cyrillic;` 时，Aspose 会自动下载所需模型。如果机器没有网络，预加载步骤会失败。此时，你可以手动提供模型（参见 Aspose 文档），或确保设备能够访问 `download.aspose.com`。

### 如何在同一张收据中处理多种语言？

可以传入逗号分隔的列表：

```csharp
ocrEngine.Language = Language.Cyrillic | Language.English;
```

Aspose 将尝试识别两套字符集。

### 我的收据模糊不清——如何提升准确率？

Aspose OCR 提供基础的图像预处理功能：

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Sharpen = true,
    Binarize = true,
    Denoise = true
};
```

在调用 `Recognize` 之前先执行上述处理。

### 大批量处理怎么办？

将识别循环包装在 `Parallel.ForEach` 中，并复用同一个 `OcrEngine` 实例（模型加载后它是线程安全的）。如果遇到线程安全问题，请对引擎加锁。

## 完整工作示例（所有步骤合并）

下面是完整的、可直接复制粘贴的程序示例，已包含可选的预加载和基础错误处理：

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        try
        {
            // Create OCR engine and select Cyrillic language
            var ocrEngine = new OcrEngine();
            ocrEngine.Language = Language.Cyrillic;

            // Optional: preload model for offline use
            // ResourceManager.Preload(Language.Cyrillic);

            // Path to the receipt image
            string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

            // Verify the file exists
            if (!File.Exists(imagePath))
                throw new FileNotFoundException("Receipt image not found.", imagePath);

            using (var image = Image.FromFile(imagePath))
            {
                // Perform OCR
                var result = ocrEngine.Recognize(image);

                // Output path for extracted text
                string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
                File.WriteAllText(outputPath, result.Text);

                Console.WriteLine("✅ receipt image to text conversion succeeded.");
                Console.WriteLine("Extracted text saved to: " + outputPath);
                Console.WriteLine("\n--- Extracted Text ---\n");
                Console.WriteLine(result.Text);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine("❌ An error occurred: " + ex.Message);
        }
    }
}
```

在项目文件夹中运行程序（`dotnet run`），即可得到一个包含 **收据图像转文本** 输出的 `.txt` 文件。

## 结论

现在，你已经拥有一个完整的端到端解决方案，能够使用 Aspose OCR 将 **收据图像转文本**——尤其是西里尔文脚本——转换为可用的文本。我们介绍了如何 **创建 OCR 引擎**、**加载图像进行 OCR**、**提取西里尔文本**，以及在几行 C# 代码中 **识别西里尔字符**。

接下来可以尝试批量处理收据文件夹，使用 `ImagePreprocessor` 提升识别率，或将 OCR 输出与数据库结合，实现自动记账。如果需要处理其他字母表，只需替换 `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}