---
category: general
date: 2026-03-13
description: 如何在 C# 中使用 OcrEngine 执行 OCR 并从图像中提取文本。通过完整的分步指南快速学习将图像转换为文本。
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- read text from picture
- how to extract text
language: zh
og_description: 如何在 C# 中执行 OCR？本指南向您展示如何从图像中提取文本、将图像转换为文本，以及使用 OcrEngine 从图片读取文本。
og_title: 如何在 C# 中进行 OCR – 从图像提取文本
tags:
- OCR
- C#
- Image Processing
title: 如何在 C# 中进行 OCR – 从图像提取文本
url: /zh/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中执行 OCR – 从图像提取文本

在 C# 中执行 OCR 是需要 **从图片读取文本** 的开发者常见的问题。在本指南中，我们将带您使用 `OcrEngine` 库从图像中提取文本，只需几行代码即可将图片转换为可搜索的字符串。

如果您曾经盯着扫描的发票、手写的便条或截图并想知道 *“如何提取文本？”*，那么您来对地方了。我们还会涉及批量处理的图像转文本方法，让您能够自动化整个工作流。

---

## 您需要的准备

在开始之前，请确保您拥有：

- **.NET 6.0 或更高版本**（我们使用的 API 兼容 .NET Standard 2.0+）
- **OcrEngine** NuGet 包（或任何提供 `Language`、`Image`、`Recognize` 和 `Text` 属性的兼容 OCR 库）
- 一个示例图像文件，例如 `hindi_page.jpg`，放在代码可以引用的文件夹中
- 对 C# 语法的基本了解 – 不需要高级技巧

就这些。无需外部服务、无需 API 密钥，只需一个本地库即可完成繁重的工作。

---

## 步骤实现

下面我们将过程拆分为若干逻辑块。每个章节都有明确的标题、简短的代码片段以及 **为什么** 这一步重要的解释，而不仅仅是 **做了什么**。

### 如何执行 OCR – 核心步骤

整体流程可以概括为五个动作：

1. **创建** OCR 引擎实例
2. **选择** 要识别的语言
3. **加载** 包含文本的图像
4. **运行** 识别算法
5. **读取** 提取出的文本

这就是骨架，接下来的章节会对其进行 fleshing。

---

### 从图像提取文本 – 创建引擎

首先，我们需要一个能够与 OCR 引擎交互的对象。

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

*为什么重要：* 实例化 `OcrEngine` 会分配所有内部缓冲区并加载图像分析所需的本机 DLL。跳过此步骤会导致后续没有可调用的识别器。

> **小贴士：** 如果计划连续处理多张图像，保持同一个 `ocrEngine` 实例存活。它会复用语言模型并加快后续调用的速度。

---

### 将图像转为文本 – 选择语言

OCR 的准确性在很大程度上取决于您提供的语言模型。针对 Hindi、Tamil 或其他脚本，请相应设置 `Language` 属性。

```csharp
// Step 2: Select the language of the text to recognize (e.g., Hindi)
ocrEngine.Language = Language.Hindi;   // You can also use Language.Tamil, Language.English, etc.
```

*为什么重要：* 引擎会使用特定语言的字符集和统计模型。提供错误的语言往往会产生乱码，尤其是非拉丁脚本。

> **边缘情况：** 如果需要多语言支持，有些库允许您设置回退列表，例如 `ocrEngine.Language = Language.Multilingual;`。

---

### 从图片读取文本 – 加载源图像

现在我们把引擎指向保存可视文本的文件。

```csharp
// Step 3: Load the image that contains the text
ocrEngine.Image = ImageStream.FromFile(@"C:\OCR\Samples\hindi_page.jpg");
```

*为什么重要：* `ImageStream.FromFile` 会把原始文件转换为 OCR 核心能够理解的位图格式。提供损坏或不受支持的格式（如 SVG）会抛出异常。

> **注意：** 大图像会消耗大量内存。如果处理高分辨率扫描件，考虑在传递给引擎之前使用 `Image.Resize` 降低分辨率。

---

### 将图像转为文本 – 运行识别

在引擎准备好且图像已加载后，我们最终调用 OCR 过程。

```csharp
// Step 4: Perform the OCR operation
ocrEngine.Recognize();
```

*为什么重要：* `Recognize` 会触发一系列内部步骤——预处理、分割、字符分类以及后处理。此调用是阻塞的，意味着线程会等待文本准备完毕。

> **性能提示：** 在普通桌面上，识别一页 300 dpi 的文档通常耗时 < 1 秒。在服务器上，建议将其放入后台任务，以免阻塞 UI。

---

### 如何提取文本 – 获取结果

识别完成后，引擎会把纯文本输出存放在 `Text` 属性中。

```csharp
// Step 5: Output the recognized text
Console.WriteLine(ocrEngine.Text);
```

*为什么重要：* `Text` 属性为您提供了一个干净的 UTF‑8 字符串，您可以将其写入文件、写入数据库，或传递给后续的 NLP 流程。

> **预期输出：** 对于示例 Hindi 页面，您可能会看到类似以下内容  
> `यह एक उदाहरण पाठ है जो OCR द्वारा पहचाना गया है।`  
> （具体输出取决于图像质量和语言模型。）

---

## 真实项目的额外考虑

下面列出了一些在生产环境中 **从图像提取文本** 时可能遇到的 “如果‑怎么办” 场景。

### 在循环中处理多张图像

如果需要 **将图像转为文本** 处理数十个文件，可在 `foreach` 循环中包装这些步骤，并复用同一个 `ocrEngine`：

```csharp
string[] files = Directory.GetFiles(@"C:\OCR\Batch\", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), ocrEngine.Text);
}
```

### 处理低质量扫描件

- 使用二值化 (`Image.Binarize()`)、去噪或去倾斜进行 **预处理**。
- 扫描时 **提高 DPI**（300 dpi 是安全基准）。
- 选择支持该脚本连字的语言模型（例如 Hindi 的 Devanagari）。

### 在 Web 上读取图片中的文本

当图像来自 URL 时，先将其下载到内存流中：

```csharp
using (HttpClient client = new())
{
    byte[] data = await client.GetByteArrayAsync(imageUrl);
    using var ms = new MemoryStream(data);
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
    Console.WriteLine(ocrEngine.Text);
}
```

### 线程安全与并行

大多数 OCR 库默认 **不** 具备线程安全。如果计划 **并发读取图片中的文本**，请为每个线程创建独立的 `OcrEngine` 实例，或使用生产者‑消费者队列来序列化访问。

---

## 完整工作示例

将所有步骤组合在一起，下面是一个可直接运行的控制台应用程序，演示了 **如何执行 OCR**、**从图像提取文本** 以及 **读取图片中的文本** 的完整流程。

```csharp
using System;
using OcrLibrary;               // Adjust to your OCR library's namespace
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Choose the language (Hindi in this case)
        ocrEngine.Language = Language.Hindi;

        // Load the image file
        string imagePath = @"C:\OCR\Samples\hindi_page.jpg";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // Run the recognition process
        ocrEngine.Recognize();

        // Output the extracted text
        string result = ocrEngine.Text;
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(result);

        // Optional: Save to a .txt file
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, result);
        Console.WriteLine($"Text saved to {txtPath}");
    }
}
```

**您将看到的结果：** 控制台会打印出从 `hindi_page.jpg` 提取的 Hindi 句子，并确认文本文件已创建。如果图像干净，输出几乎与原始打印文本完全一致。

---

## 结论

现在，您已经掌握了在 C# 中 **如何执行 OCR** 的完整流程，了解了 **从图像提取文本**、**将图像转为文本**、以及 **读取图片中的文本** 的实现方式。创建、设置语言、加载、识别、读取这五步模式覆盖了大多数使用场景，而额外的技巧则帮助您处理批量作业、低质量扫描以及基于网络的来源。

准备好迎接下一个挑战了吗？尝试将语言切换为英文，处理渲染为图像的 PDF 页面，或将 OCR 输出接入搜索索引管道。一旦掌握了 C# 中 OCR 的基础，可能性无限。

有问题或遇到顽固的图像无法识别？在下方留言，让我们一起排查。祝编码愉快！  

![how to perform OCR example](images/ocr-example.png "how to perform OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}