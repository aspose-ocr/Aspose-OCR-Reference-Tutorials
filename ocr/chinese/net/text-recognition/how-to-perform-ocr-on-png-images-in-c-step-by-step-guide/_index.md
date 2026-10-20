---
category: general
date: 2026-03-29
description: 如何在 C# 中进行 OCR 并读取 PNG 文件中的文本。学习提取俄文文本、读取 PNG 文本，以及如何使用 Aspose OCR 提取文本。
draft: false
keywords:
- how to perform ocr
- read text from png
- how to extract text
- extract russian text
- c# ocr tutorial
language: zh
og_description: 如何在 C# 中使用 Aspose OCR 执行 OCR。本指南展示了如何从 PNG 读取文本、提取俄语文本，并实现完整的 C# OCR
  解决方案。
og_title: 如何在 C# 中进行 OCR – 完整的 PNG 文本提取
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中对 PNG 图像进行 OCR – 步骤指南
url: /zh/net/text-recognition/how-to-perform-ocr-on-png-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中对 PNG 图像执行 OCR – 完整教程

是否曾经需要在截图或扫描文档上**执行 OCR**，但不确定在 C# 中该从何入手？你并非唯一有此困惑的开发者。大家经常问：“如何在不将 PNG 文件发送到外部服务的情况下读取文本？”好消息是，使用 Aspose.OCR，你可以**提取俄文文本**、**读取 png 文本**，并仅用几行代码获得干净的字符串。

在本教程中，我们将逐步演示你需要的全部内容：设置库、选择合适的语言模型、运行识别以及处理常见陷阱。结束时，你将能够**从任何 PNG 图像中提取文本**，无论是英文、俄文，还是 Aspose 支持的 70 多种语言之一。没有冗余，只提供一个实用、可直接在控制台应用中运行的示例。

---

## 你将学到

- 安装并引用 Aspose.OCR NuGet 包。
- 在默认自动下载模式下初始化 OCR 引擎。
- 使用西里尔字母语言模型**提取俄文文本**。
- 对本地 PNG 文件运行 OCR 并显示结果。
- 解决缺少语言文件以及提升准确率的技巧。

**先决条件**：.NET 6+（或 .NET Framework 4.7.2+），Visual Studio 2022 或 VS Code，以及首次运行时的网络连接（语言模型会自动下载）。

---

## 第一步 – 安装 Aspose.OCR 包

要开始使用，请将 Aspose.OCR 库添加到项目中。打开项目文件夹的终端并运行：

```bash
dotnet add package Aspose.OCR
```

或者，如果你更喜欢 Visual Studio UI，右键 **Dependencies → Manage NuGet Packages**，搜索 **Aspose.OCR**，然后点击 **Install**。

> **专业提示**：该包只有几兆大小，语言模型按需获取，因此不会让你的应用因不必要的文件而臃肿。

---

## 第二步 – 初始化 OCR 引擎（关键字示例）

创建引擎非常简单。构造函数会自动启用*自动下载模式*，这意味着第一次请求本地不存在的语言时，Aspose 会为你下载。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine – it will download missing models automatically.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Choose the language model – Russian Cyrillic (downloads if missing).
        ocrEngine.Language = Language.RussianCyrillic;

        // 3️⃣ Run OCR on the PNG image.
        var ocrResult = ocrEngine.RecognizeImage("sample_russian.png");

        // 4️⃣ Output the recognized text.
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **为什么重要**：使用默认的自动下载模式可以避免手动处理文件。如果以后需要在其他语言下**读取 png 文本**，只需将 `Language.RussianCyrillic` 更改为相应的枚举值即可。

---

## 第三步 – 准备你的 PNG 图像

确保要处理的图像在运行时可访问。将 `sample_russian.png` 放在编译后的 `.exe` 同一文件夹下，或使用绝对路径。图像应为清晰的扫描或截图；模糊或高度压缩的 PNG 会显著降低 OCR 准确率。

**常见边缘情况**：如果 PNG 包含多种语言，可设置 `ocrEngine.Language = Language.Multilingual;` 让引擎自动检测每个块的语言。

---

## 第四步 – 运行应用并验证输出

编译并运行程序：

```bash
dotnet run
```

你应该在控制台看到提取的俄文文本，例如：

```
Привет, мир! Это пример текста на русском языке.
```

如果得到空字符串，请检查：

1. 文件路径是否正确。  
2. 图像是否全白或全黑。  
3. 语言模型是否已成功下载（在用户配置文件下查找 `Aspose.OCR` 文件夹）。

---

## 第五步 – 提升准确率的高级调优

默认设置已能满足大多数场景，但你可能想进一步微调引擎：

| 设置 | 功能说明 | 适用场景 |
|------|----------|----------|
| `ocrEngine.PreprocessOptions.Deskew = true;` | 校正轻微旋转 | 扫描件未完全对齐 |
| `ocrEngine.PreprocessOptions.RemoveNoise = true;` | 去除背景噪点 | 来自手机摄像头的低质量 PNG |
| `ocrEngine.RecognitionOptions.CharWhitelist = "0123456789";` | 限定字符集为数字 | 从发票中提取数字 |

在调用 `RecognizeImage` 之前加入任意上述代码：

```csharp
ocrEngine.PreprocessOptions.Deskew = true;
ocrEngine.PreprocessOptions.RemoveNoise = true;
```

---

## 第六步 – 将结果导出到文件（可选）

如果需要将**提取文本**保存到文件以便后续处理，只需将结果写入磁盘：

```csharp
System.IO.File.WriteAllText("ocr_output.txt", ocrResult.Text);
Console.WriteLine("OCR output saved to ocr_output.txt");
```

现在你拥有了持久化的副本，可供数据库、搜索索引或翻译引擎使用。

---

## 常见问题

**Q: 这能用于 JPEG、BMP 等其他图像格式吗？**  
A: 完全可以。`RecognizeImage` 接受 .NET `System.Drawing` 库支持的任何格式，包括 JPEG、BMP 和 TIFF。

**Q: 如果同一次运行中需要提取英文文本怎么办？**  
A: 创建第二个 `OcrEngine` 实例并使用 `Language.English`，或在不同调用之间切换 `Language` 属性。

**Q: 能在 Web API 中异步运行 OCR 而不阻塞主线程吗？**  
A: 可以。将识别调用包装在 `Task.Run` 中，或使用 `RecognizeImageAsync`（在新版 Aspose 中可用）。

**Q: PNG 的尺寸有没有限制？**  
A: 库能够处理大图像，但随分辨率提升内存占用也会增加。如果遇到 `OutOfMemoryException`，请先对图像进行降采样。

---

## 完整可运行示例（复制粘贴即用）

下面是完整程序代码，直接粘贴到新建的控制台项目（`dotnet new console`）中，安装 NuGet 包后即可运行。

```csharp
// File: Program.cs
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize OCR engine – auto‑download enabled.
            var ocrEngine = new OcrEngine();

            // Choose Russian Cyrillic language model.
            ocrEngine.Language = Language.RussianCyrillic;

            // Optional: improve accuracy for skewed or noisy images.
            ocrEngine.PreprocessOptions.Deskew = true;
            ocrEngine.PreprocessOptions.RemoveNoise = true;

            // Path to the PNG file you want to read.
            string imagePath = "sample_russian.png";

            // Perform OCR.
            OcrResult result = ocrEngine.RecognizeImage(imagePath);

            // Output the recognized text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);

            // Save to a text file for later use.
            System.IO.File.WriteAllText("ocr_output.txt", result.Text);
            Console.WriteLine("Result saved to ocr_output.txt");
        }
    }
}
```

**预期的控制台输出**（假设示例中包含短语 “Привет, мир!”）：

```
=== OCR Result ===
Привет, мир! Это пример текста на русском языке.
Result saved to ocr_output.txt
```

---

## 结论

我们已经完整演示了如何在 C# 中对 PNG 图像**执行 OCR**，从安装 Aspose.OCR 到自定义预处理选项以及导出结果。现在，你已经掌握了**读取 png 文本**、**提取文本**以及使用最少代码**提取俄文文本**的技巧。

准备好迎接下一个挑战了吗？尝试将 OCR 输出喂给语言检测库，或与 Azure Cognitive Services 结合实现翻译。只要将可靠的 OCR 引擎与 C# 强大的生态系统结合，可能性无限。

如果你觉得这篇 **c# ocr 教程** 有帮助，请点星、分享给团队成员，或在评论区留下你的经验。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}