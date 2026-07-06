---
category: general
date: 2026-02-19
description: c# OCR 教程——学习如何从图像中提取文本、读取图像文字、将图像转换为文本，并在几分钟内使用 Aspose.OCR 识别图像文字。
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- read image text
- convert image to text
- recognize image text
language: zh
og_description: c# OCR 教程向您展示如何从图像中提取文本、读取图像文字、将图像转换为文本，以及使用 Aspose OCR 识别图像文字。
og_title: C# OCR 教程 – 使用 Aspose OCR 从图像提取文本
tags:
- OCR
- C#
- Aspose
title: C# OCR 教程：使用 Aspose OCR 从图像中提取文本
url: /zh/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr 教程 – 使用 Aspose OCR 从图像中提取文本

是否曾想过在纯 C# 环境中 **从图像中提取文本**？这正是本 **c# ocr 教程** 所要解决的。只需几步，您就能学习读取图像文本、将图像转换为文本，甚至使用 Aspose.OCR 库识别不同语言的图像文本。

在本指南中，我们将逐步讲解您需要的全部内容：从安装 NuGet 包到处理许可证、设置语言以及打印结果。完成后，您将拥有一个可直接运行的控制台应用程序，可将任何图片——例如扫描的发票或截图——转换为可搜索的文本。

## 您需要的环境

- .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Framework 4.7+）  
- Visual Studio 2022（或您喜欢的任何编辑器）  
- Aspose.OCR 许可证文件 *optional* ——库在评估模式下也能工作，但许可证可去除水印。  
- 一张示例图片（例如 `cyrillic_sample.jpg`），放置在磁盘的任意位置。

无需其他第三方工具；Aspose.OCR 在内部完成所有繁重工作。

---

![c# ocr 教程示例图像，显示西里尔文字](/images/ocr-sample.jpg "c# ocr 教程 – OCR 示例图像")

## c# ocr 教程 – 设置 Aspose OCR

首先，将 Aspose.OCR 包添加到项目中：

```bash
dotnet add package Aspose.OCR
```

> **技巧提示：** 如果您使用 Visual Studio，也可以右键单击项目 → **管理 NuGet 包** 并搜索 *Aspose.OCR*。

### 为什么许可证很重要

Aspose.OCR 在没有许可证的情况下以 30 天评估模式运行。`License` 类只需指向您的 `.lic` 文件；设置后，引擎将停止在输出中插入评估页脚。

```csharp
// Optional: apply your Aspose.OCR license to unlock full features
// new License().SetLicense("Aspose.OCR.lic");
```

如果在开发期间跳过此行，OCR 仍然可以工作——只需记住评估提示会出现在提取的文本中。

## 从图像提取文本 – 创建 OCR 引擎

任何 **c# ocr 教程** 的核心都是 `OcrEngine` 对象。它抽象了整个识别流水线。

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Step 1: (Optional) Apply your license – see above
        // new License().SetLicense("Aspose.OCR.lic");

        // Step 2: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 3: Choose the language you want to recognize
        // For this demo we use Cyrillic, but you can pick English, Arabic, etc.
        ocrEngine.Language = Language.Cyrillic;

        // Step 4: Run OCR on the target picture
        var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/cyrillic_sample.jpg");

        // Step 5: Output the recognized text to the console
        Console.WriteLine("Recognized text:");
        Console.WriteLine(result.Text);
    }
}
```

### 代码实际做了什么

- **实例化 `OcrEngine`** 会创建一个全新的处理上下文。  
- **设置 `Language`** 告诉 Aspose 预期的字符集；这大幅提升准确率，因为引擎可以应用特定语言的启发式算法。  
- `RecognizeImage` 加载文件，执行一系列图像预处理步骤（去倾斜、二值化、去噪），最后运行神经网络识别器。  
- `result.Text` 保存纯文本表示——非常适合 **将图像转换为文本** 的场景。

## 读取图像文本 – 处理不同文件类型

Aspose.OCR 不仅限于 JPEG。它支持 PNG、BMP、TIFF，甚至 PDF 页面（作为图像）。如果需要批量处理，可将调用包装在简单循环中：

```csharp
string[] files = Directory.GetFiles(@"YOUR_DIRECTORY", "*.*", SearchOption.TopDirectoryOnly)
                          .Where(f => f.EndsWith(".jpg") || f.EndsWith(".png") || f.EndsWith(".tif"))
                          .ToArray();

foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"--- {Path.GetFileName(file)} ---");
    Console.WriteLine(res.Text);
}
```

### 边缘情况：空或损坏的图像

如果 `RecognizeImage` 收到 null 或不可读取的文件，它会抛出 `ArgumentException`。快速的防护可以让您的 **c# ocr 教程** 更加健壮：

```csharp
if (!File.Exists(file))
{
    Console.WriteLine($"File not found: {file}");
    continue;
}
```

## 识别图像文本 – 精细调优以提升准确度

有时默认设置会漏掉一些字符，尤其是在低对比度扫描时。Aspose.OCR 提供了一些可调参数：

| Property                                   | 功能                                         | 典型使用场景      |
|--------------------------------------------|--------------------------------------------|-----------------|
| `ocrEngine.PreprocessingOptions.Deskew`    | 旋转图像以纠正倾斜                           | 扫描文档          |
| `ocrEngine.PreprocessingOptions.NoiseRemoval` | 去除斑点                                     | 旧照片            |
| `ocrEngine.Language`                       | 语言模型（西里尔文、英文等）                 | 多语言 OCR       |

启用去倾斜的示例：

```csharp
ocrEngine.PreprocessingOptions.Deskew = true;
```

这些调整可帮助您 **从图像中提取文本** 的文件，即使它们未完全对齐，从而提升 **读取图像文本** 操作的成功率。

## 预期输出

对 `cyrillic_sample.jpg`（其中包含短语 “Привет мир”）运行示例代码，得到类似以下内容：

```
Recognized text:
Привет мир
```

如果处于评估模式，您还会看到一行尾部信息：

```
--- Evaluation version. Use a licensed copy for production. ---
```

只要提供有效的许可证文件，该行即会消失。

---

## 常见陷阱及避免方法

1. **语言设置错误** – 在西里尔文字上使用 `Language.English` 会返回乱码。务必将语言与源文本匹配。  
2. **大图像** – 处理 10 MP 照片可能很慢。如果速度比像素完美更重要，请先缩小图像（`Bitmap.Resize`）。  
3. **缺少依赖** – Aspose.OCR 附带本机二进制文件；确保输出文件夹中包含 `Aspose.OCR.Native.dll`（NuGet 会处理此问题，但自定义构建流水线可能需要复制步骤）。

## 下一步 – 超越基础

- **批量转换**：将前述循环与异步 `Task.Run` 结合，以加速大型文件夹的处理。  
- **导出为 PDF**：在 **将图像转换为文本** 之后，将字符串传递给 PDF 生成器（例如 Aspose.PDF），创建可搜索的 PDF。  
- **集成 Azure Functions**：将 OCR 逻辑转化为无服务器端点，实时处理上传。

所有这些扩展都在实际应用中延续了 **从图像中提取文本** 和 **读取图像文本** 的主题。

---

## 结论

您刚刚完成了一个 **c# ocr 教程**，展示了如何使用 Aspose.OCR 读取图像文本、将图像转换为文本以及识别图像文本。上面的完整可运行示例演示了每一步——从许可证到语言选择再到错误处理——因此您可以将此代码直接嵌入任何 .NET 项目，立即开始提取文本。

随意尝试不同语言、调节预处理选项，或将输出接入数据库以实现可搜索的归档。如果遇到问题，Aspose 文档是可靠的参考，但此处的代码在大多数场景下应能开箱即用。

祝编码愉快，愿您的图像始终可读！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}