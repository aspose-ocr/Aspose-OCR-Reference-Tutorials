---
category: general
date: 2026-04-17
description: 学习如何在 C# 中实现 OCR，识别图像中的文字，提取 JPG 中的文本，并快速将图像转换为文字。
draft: false
keywords:
- how to perform OCR
- recognize text from image
- extract text from jpg
- convert image to text
- how to extract text
language: zh
og_description: 如何在 C# 中实现 OCR？本指南将向您展示如何从图像中识别文字、从 JPG 中提取文本，以及在几分钟内将图像转换为文字。
og_title: 如何在 C# 中执行 OCR – 从图像识别文本
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中进行 OCR – 从图像中识别文字
url: /zh/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中执行 OCR – 从图像识别文本

是否曾好奇 **how to perform OCR**（如何执行 OCR）在从扫描仪或手机获取的图片上？在许多项目中，你需要 **recognize text from image**（从图像识别文本）文件——无论是收据、手写笔记，还是转换成 JPEG 的 PDF 页面。好消息是，使用 Aspose.OCR，你可以仅用几行 C# **extract text from jpg**（从 jpg 提取文本）并 **convert image to text**（将图像转换为文本）。

在本教程中，我们将完整演示整个过程，从安装库到处理诸如缺少语言等 edge‑cases（边缘情况）。完成后，你将确切了解 **how to perform OCR**，并拥有一个可直接运行的程序，它会将提取的字符串打印到控制台。没有模糊的 “see the docs” 快捷方式——只有完整的、独立的解决方案。

## 你需要的环境

- **.NET 6+**（代码同样适用于 .NET Framework，但 .NET 6 是当前的 LTS）
- **Aspose.OCR for .NET** NuGet 包 – 使用 `dotnet add package Aspose.OCR` 安装
- 你想要测试的图像文件（JPEG、PNG、BMP）——我们将其命名为 `input.jpg`
- 任意你喜欢的 IDE（Visual Studio、Rider、VS Code）

就这些。无需额外配置、外部服务，也没有隐藏步骤。

## 步骤 1：安装 Aspose.OCR 并添加引用

首先，将 OCR 库引入你的项目。打开项目文件夹中的终端并运行：

```bash
dotnet add package Aspose.OCR
```

该命令会获取最新的稳定版本（截至 2026 年 4 月为 **23.9.0**），并更新你的 `.csproj`。随后，在文件顶部添加 using 指令：

```csharp
using Aspose.OCR;
```

> **Pro tip:** 如果你使用 Visual Studio，NuGet 包管理器 UI 同样有效——只需搜索 *Aspose.OCR*。

## 步骤 2：加载要识别的图像

现在我们需要告诉 OCR 引擎读取哪张图片。Aspose 提供了便利的 `OcrImage.FromFile` 方法，支持大多数常见格式。

```csharp
// Step 2: Load the image you want to recognize
var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

将 `YOUR_DIRECTORY` 替换为实际路径，或将图像放在可执行文件旁边并使用相对路径。如果文件不存在，方法会抛出 `FileNotFoundException`，你可以在后面捕获它。

## 步骤 3：创建 OCR 引擎（平台感知）

Aspose.OCR 会自动为你运行的操作系统（Windows、Linux、macOS）选择最佳底层引擎。在 `using` 块中创建它可确保正确释放资源。

```csharp
// Step 3: Create the OCR engine (auto‑selects best engine for the platform)
using var ocrEngine = new OcrEngine();
```

为什么使用 `using`？引擎持有本机资源（如非托管内存），需要释放。如果忘记释放，尤其在循环处理大量图像时，可能导致内存泄漏。

## 步骤 4：（可选）设置语言 – 默认英文

如果图像包含英文文本，你可以跳过此步骤，因为默认是 `OcrLanguage.English`。对于其他语言，只需赋予相应的枚举值即可。

```csharp
// Step 4: (Optional) Specify the language – English is the default
ocrEngine.Language = OcrLanguage.English;
```

> **Did you know?** Aspose.OCR 支持超过 30 种语言，包括阿拉伯语、中文和俄语。切换语言只需更改枚举即可。

## 步骤 5：运行识别过程

调用 `Recognize` 完成繁重的工作——像素分析、字符分割和词典查找都在内部完成。

```csharp
// Step 5: Run the recognition process on the loaded image
var ocrResult = ocrEngine.Recognize(ocrImage);
```

如果引擎未找到任何文本，`ocrResult.Text` 将是空字符串。你可能需要在继续之前检查 `ocrResult.HasText`（布尔值）。

## 步骤 6：获取并显示纯文本结果

最后，提取字符串并写入控制台。这正是你实际 **convert image to text**（将图像转换为文本）的地方。

```csharp
// Step 6: Retrieve the plain‑text result and display it
string recognizedText = ocrResult.Text;
Console.WriteLine("Recognized text:");
Console.WriteLine(recognizedText);
```

输出大致如下：

```
Recognized text:
Invoice #12345
Date: 04/15/2026
Total: $256.78
```

如果你需要进一步处理文本（例如保存到文件、写入数据库或运行正则表达式），它已经在 `recognizedText` 变量中。

## 完整工作示例

下面是完整的程序，你可以复制粘贴到新的控制台应用（`dotnet new console`）中。它包含了对最常见问题的错误处理。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load the image you want to recognize
            var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.jpg");

            // 2️⃣ Create the OCR engine (auto‑selects best engine for the platform)
            using var ocrEngine = new OcrEngine();

            // 3️⃣ (Optional) Set language – English is default
            ocrEngine.Language = OcrLanguage.English;

            // 4️⃣ Run the recognition process
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // 5️⃣ Check if any text was found
            if (!ocrResult.HasText || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be extracted from the image.");
                return;
            }

            // 6️⃣ Retrieve and display the plain‑text result
            string recognizedText = ocrResult.Text;
            Console.WriteLine("Recognized text:");
            Console.WriteLine(recognizedText);
        }
        catch (FileNotFoundException)
        {
            Console.WriteLine("The specified image file was not found. Double‑check the path.");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"An unexpected error occurred: {ex.Message}");
        }
    }
}
```

> **Expected output:** 控制台会打印 OCR 引擎检测到的精确字符。如果源图像清晰且高分辨率，准确率通常超过 95 %。

## 处理常见边缘情况

### 1️⃣ 多语言图像  
如果你有双语收据，将 `ocrEngine.Language` 设置为 `OcrLanguage.Multilingual`。引擎会自动尝试检测每种语言。

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### 2️⃣ 低分辨率或倾斜图像  
在将图像提供给 Aspose 之前进行预处理（旋转、调整大小、增加对比度）。库提供了 `OcrImage` 的方法，如 `Resize` 和 `Rotate`。

```csharp
ocrImage = ocrImage.Rotate(0.0); // placeholder – replace with actual angle if needed
```

### 3️⃣ 大批量处理  
处理数十个文件时，复用同一个 `OcrEngine` 实例，而不是在每次循环中创建新实例。只需在批处理完成后记得释放它。

```csharp
using var batchEngine = new OcrEngine();
foreach (var file in Directory.GetFiles(@"images", "*.jpg"))
{
    var img = OcrImage.FromFile(file);
    var result = batchEngine.Recognize(img);
    // handle result…
}
```

### 4️⃣ Linux 容器的内存限制  
如果在内存受限的 Docker 容器中运行，设置 `ocrEngine.MaxMemoryUsage`（如果 API 提供此属性）以避免 OOM 崩溃。

## 专业技巧与注意事项

- **File Encoding:** 返回的字符串是 UTF‑16（.NET 中的 `string`）。如果需要 UTF‑8 写入文件，请使用 `Encoding.UTF8.GetBytes(recognizedText)`。
- **Performance:** 对单张图像而言，引擎初始化的开销可以忽略不计。对于批量任务，初始化一次（参见批处理示例）可节省约 30 % 的处理时间。
- **Debugging:** 如果 OCR 结果出现乱码，检查 `ocrResult.Words`（单词对象集合）以查看置信度分数。低置信度通常意味着图像模糊。
- **License:** Aspose.OCR 在未授权的评估模式下可用，但会在输出文本中添加水印。请注册许可证文件（`Aspose.OCR.lic`）以用于生产环境。

## 可视化概览

![在 C# 中执行 OCR 示例](ocr-example.png "在 C# 中执行 OCR 示例")

*该截图显示运行示例代码后完整的控制台输出。*

## 结论

现在，你已经牢牢掌握了使用 Aspose.OCR 在 C# 中 **how to perform OCR** 的方法，并且可以自信地 **recognize text from image** 文件、**extract text from jpg**，以及 **convert image to text**，以用于任何后续处理。示例涵盖了关键步骤，解释了每一步的重要性，并且还暗示了诸如多语言支持和批量处理等高级场景。

接下来怎么办？尝试将 JPEG 换成 PNG，实验 `OcrLanguage.Multilingual`，或将提取的文本管道到自然语言处理流水线中。当你能够将图片转化为可搜索、可编辑的字符串时，可能性无穷。

有问题或遇到困难？在下方留言吧，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}