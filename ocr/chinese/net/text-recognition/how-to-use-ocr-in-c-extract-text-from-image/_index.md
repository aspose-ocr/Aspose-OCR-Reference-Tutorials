---
category: general
date: 2026-03-05
description: 如何在 C# 中使用 OCR 从图像中提取文本。学习将图像转换为文本，读取韩文字符，并快速加载图像进行 OCR。
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: zh
og_description: 如何在 C# 中使用 OCR 并即时从图像中提取文本。本指南展示了如何将图像转换为文本、读取韩文字符以及加载图像进行 OCR。
og_title: 如何在 C# 中使用 OCR – 从图像提取文本
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 OCR – 从图像中提取文本
url: /zh/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 从图像提取文本

有没有想过在截屏中满是韩文时，**如何使用 OCR** 并获取纯文本字符串？你并不是唯一为此困惑的人。在本教程中，我们将演示一个完整、可直接运行的示例，能够**从图像中提取文本**、**将图像转换为文本**，并展示如何使用 Aspose.OCR **读取韩文字**。

我们还会介绍经常被忽视的 **加载图像进行 OCR** 步骤，避免后期出现“文件未找到”的意外。完成后，你将拥有一个可直接嵌入任何 .NET 项目的独立程序。

## 你需要的环境

- .NET 6+（或 .NET Framework 4.7.2 及更高）——代码在两者上均可运行。
- Aspose.OCR for .NET ——可从 Aspose 官网获取免费试用版。
- 一个包含韩文的示例图片（`korean_doc.png`）。
- 你喜欢的 IDE（Visual Studio、Rider、VS Code ——随你选择）。

不需要其他第三方库。

## 第一步：设置项目并添加 Aspose.OCR

首先，创建一个新的控制台应用程序：

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

然后添加 Aspose.OCR NuGet 包：

```bash
dotnet add package Aspose.OCR
```

> **专业提示：** 如果你有许可证文件，请将其放在项目根目录；否则免费试用版也能运行，但会在输出中添加水印。

## 第二步：如何使用 OCR – 初始化引擎

现在我们来编写 C# 代码。**如何使用 OCR** 的第一步是实例化 `OcrEngine`。该对象是库的核心，保存了后续需要的所有设置。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**为什么重要：** 没有正确的引擎实例，你无法设置语言、加载图像或获取结果。引擎还负责内部资源管理，创建一次并重复使用比不断新建对象更高效。

## 第三步：选择语言 – 读取韩文字

下一行告诉引擎要识别哪种语言。因为我们的目标是 **读取韩文字**，所以将 `OcrLanguage.Korean` 设为语言。根据实际需求，你也可以改为阿拉伯语、泰语、古吉拉特语等。

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**重要性说明：** 语言选择能显著提升准确率。OCR 引擎使用特定语言的词典和字符模型，若提供错误的语言会导致输出乱码。

## 第四步：加载图像进行 OCR – 将图像转换为文本

在引擎执行任何操作之前，需要 **加载图像进行 OCR**。`ImageStream.FromFile` 方法将文件读取为引擎可识别的格式。

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

如果图像位于其他文件夹，只需修改路径。记得将文件的 *Build Action* 设置为 “Copy if newer”，以便运行时可找到该文件。

> **常见坑点：** 在字符串字面量中直接使用反斜杠 (`\`) 而未进行转义会导致编译错误。请使用双反斜杠 (`\\`) 或逐字字符串 (`@"C:\\path\\file.png"`)。

## 第五步：执行 OCR – 从图像提取文本

现在开始真正的工作。调用 `Recognize()` 会运行 OCR 算法，`Text` 属性则返回原始字符串。

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

此时你已经 **从图像中提取文本**，并实现了 **将图像转换为文本**。如果原始布局包含换行，结果中也会出现换行符。

## 第六步：显示结果 – 验证输出

最后，将结果打印到控制台，以便验证是否成功。

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

Run the program:

```bash
dotnet run
```

### 预期输出

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

如果看到与图像相似的韩文字，恭喜你——已经掌握了使用 Aspose.OCR 的 **如何使用 OCR**！

![展示从加载图像到打印识别文本流程的 OCR 示例图](image.png)

## 边缘情况与变体

### 1. 处理多页

如果需要 **从图像中提取文本** 的文件包含多页（例如多页 TIFF），可遍历每页并对每个 `ImageStream` 实例调用 `Recognize()`。

### 2. 处理低质量扫描

低分辨率图像会影响准确率。在调用 `Recognize()` 之前，可使用 Aspose 的预处理工具提升图像质量：

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. 动态切换语言

假设文档包含多种语言。可以在每次识别之间更改 `ocrEngine.Language`：

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. 将结果保存到文件

如果想 **将图像转换为文本** 并保存，只需将字符串写入 `.txt` 文件：

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## 常见问题

- **运行此代码是否需要许可证？**  
  不需要。免费试用版可用于实验，但会在输出中添加水印。购买许可证后可去除水印并解锁全部性能。

- **可以在 Linux 上使用吗？**  
  完全可以。Aspose.OCR 跨平台，只需确保已安装所需的本机依赖（Linux 上 .NET Core 需要 libgdiplus）。

- **如果我的图像是流而不是文件怎么办？**  
  使用 `ImageStream.FromStream(yourStream)` ——该 API 接受任意 `System.IO.Stream`。

## 结论

我们已一步步演示了在 C# 中 **如何使用 OCR** 来 **从图像中提取文本**、**将图像转换为文本**，以及 **读取韩文字**，并正确 **加载图像进行 OCR**。上述完整可运行的示例应可直接使用，额外的技巧为更高级的场景提供了路线图。

准备好迎接下一个挑战了吗？尝试更换语言、逐页处理 PDF，或将 OCR 调用集成到 Web API 中，让用户上传图片即可即时获取文本结果。可能性无限，而你已经拥有了坚实的基础。

祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}