---
category: general
date: 2026-02-25
description: 如何在 C# 中快速使用 OCR 从图像提取文本，加载图像进行 OCR，并使用 Aspose OCR 设置 OCR 语言。一步一步的指南。
draft: false
keywords:
- how to use OCR
- extract text from image
- load image for OCR
- set OCR language
language: zh
og_description: 学习如何在 C# 中使用 OCR 从图像中提取文本、加载图像进行 OCR，并使用 Aspose OCR 设置 OCR 语言。完整的异步示例。
og_title: 如何在 C# 中使用 OCR – 完整的异步指南
tags:
- C#
- Aspose OCR
- async programming
title: 如何在 C# 中使用 OCR – 异步从图像提取文本
url: /zh/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-asynchronously/
---

, and happy coding!" translate.

Then closing shortcodes.

Make sure to keep all placeholders unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 异步从图像提取文本

是否曾经需要在收据、发票或扫描表单上**使用 OCR**，却发现找到的代码示例要么不完整，要么停留在同步的世界？你并非唯一遇到这种情况。在许多真实场景的应用中，你希望**从图像中提取文本**而不冻结 UI，同时还能灵活选择合适的识别语言。

在本教程中，我们将逐步演示一个完整、可运行的示例，向你展示如何**加载图像进行 OCR**、配置**设置 OCR 语言**选项，并异步执行识别。结束时，你将拥有一个独立的控制台应用程序，能够将识别的文本打印到控制台，并提供一些处理边缘情况和扩展解决方案的技巧。

## 前置条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）  
- 已安装 Aspose.OCR NuGet 包（`Aspose.OCR`）  
- 将示例图像文件（例如 `receipt.jpg`）放置在可引用的文件夹中  
- 基础 C# 知识——不需要任何高级 async 技巧，只需掌握基本概念  

如果缺少上述任意项，可使用 `dotnet add package Aspose.OCR` 获取 NuGet 包，并为测试图像创建一个简单文件夹。无需复杂操作。

---

## 如何使用 OCR：逐步实现

下面我们将过程拆分为四个逻辑步骤。每个步骤都有自己的 H2 标题，首个标题重复主要关键词以满足 SEO。

### 步骤 1 – 初始化 OCR 引擎（How to Use OCR）

首先需要一个 `OcrEngine` 实例。可以把它看作是整个操作的大脑；它保存配置、图像以及结果。

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Enums;

public class AsyncExample
{
    public static async Task RunAsync()
    {
        // Create the OCR engine – this object will manage everything.
        var ocrEngine = new OcrEngine();

        // Next steps will configure it further.
```

**为什么这很重要：**  
一次创建引擎并重复使用可以在处理大量图像时提升性能。它还为你提供了一个统一的地方来设置全局选项，例如语言。

### 步骤 2 – 设置 OCR 语言（Set OCR Language Properly）

如果跳过语言选择，Aspose OCR 默认使用英文，这对收据可能够用，但对外文文档就不合适了。设置语言只需一行代码：

```csharp
        // Set the recognition language to English.
        // You can change OcrLanguage.French, OcrLanguage.Spanish, etc.
        ocrEngine.Config.Language = OcrLanguage.English;
```

**专业提示：**  
当需要多语言支持时，可以传入语言数组（`OcrLanguage.English | OcrLanguage.French`）。引擎会按顺序尝试每种语言，适用于混合语言的收据。

### 步骤 3 – 加载图像进行 OCR（Load Image for OCR Efficiently）

现在将引擎指向我们想要读取的文件。Aspose 提供的 `ImageStream.FromFile` 抽象了底层流的处理。

```csharp
        // Load the image you want to analyze.
        // Replace the path with the actual location of your image file.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

**边缘情况：**  
如果文件路径错误或图像格式不受支持，`FromFile` 会抛出异常。构建稳健的 UI 时请使用 try/catch 包裹。

### 步骤 4 – 执行异步识别（Extract Text from Image）

这里就是魔法发生的地方。`RecognizeAsync` 方法在后台线程上运行 OCR，释放调用线程——非常适合 UI 或 Web 应用。

```csharp
        // Run OCR asynchronously.
        var ocrResult = await ocrEngine.RecognizeAsync();

        // Display the recognized text.
        Console.WriteLine("OCR completed:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**你将看到的结果：**  
如果 `receipt.jpg` 包含文字 “Total: $12.34”，控制台输出将是：

```
OCR completed:
Total: $12.34
```

**为什么使用 async？**  
同步 OCR 可能会阻塞线程数秒，尤其是高分辨率图像。使用 `await` 能保持应用响应，并且与 ASP.NET Core 请求管道良好配合。

---

## 完整可运行示例

将下面的代码片段复制到新建的控制台项目（`dotnet new console`）中并运行。记得将 `YOUR_DIRECTORY/receipt.jpg` 替换为实际的图像路径。

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Enums;

public class AsyncExample
{
    public static async Task Main(string[] args)
    {
        await RunAsync();
    }

    public static async Task RunAsync()
    {
        // Step 1: Create the OCR engine.
        var ocrEngine = new OcrEngine();

        // Step 2: Set the OCR language (English by default).
        ocrEngine.Config.Language = OcrLanguage.English;

        // Step 3: Load the image you want to process.
        // Ensure the file exists; otherwise an exception is thrown.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // Step 4: Perform asynchronous OCR recognition.
        var ocrResult = await ocrEngine.RecognizeAsync();

        // Output the recognized text.
        Console.WriteLine("OCR completed:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**预期输出**（假设图像包含可读的英文文本）：

```
OCR completed:
Your extracted text appears here, line by line.
```

如果看到空字符串，请检查图像是否清晰以及语言设置是否匹配文本。

---

## 常见陷阱及规避方法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| **空白结果** | 低分辨率图像或语言设置错误 | 使用更高分辨率的扫描，或将 `ocrEngine.Config.Language` 设置为正确的语言 |
| **`FromFile` 异常** | 路径错误或不支持的格式 | 检查路径，使用绝对路径，或先将图像转换为 PNG/JPEG |
| **性能延迟** | 大批量同步处理 | 使用 `Task.WhenAll` 并复用单个 `OcrEngine` 实例并行处理图像 |
| **内存泄漏** | 自定义加载代码中未释放流 | 依赖 `ImageStream.FromFile` 自动处理释放，或在手动加载时使用 `using` 块 |

**额外提示：**  
如果需要提取结构化数据（例如收据中的键值对），可以对 `ocrResult.Text` 进行正则表达式或轻量级 NLP 库的后处理。

---

## 扩展解决方案

既然已经掌握了**如何使用 OCR**处理单张图像，可能会想：“如果每晚有数十张收据怎么办？”

- **批处理：** 将 `RunAsync` 逻辑包装在循环中并将结果收集到列表中。  
- **并行处理：** 使用 `Parallel.ForEach`（在 .NET 6 中使用 `Parallel.ForEachAsync`）进行异步支持，以同时运行多个识别。  
- **持久化结果：** 将 `ocrResult.Text` 存入数据库，或写入 CSV 以供后续分析。  

所有这些扩展仍然基于我们覆盖的核心步骤：初始化引擎、设置语言、加载图像以及调用 `RecognizeAsync`。

---

## 可视化概览

![如何使用 OCR 示例](/images/ocr-example.png "在 C# 中使用 Aspose OCR 的 OCR 示例")

*上图展示了从加载图像到获取识别文本的流程。*

---

## 结论

我们刚刚完整演示了一个可投入生产的示例，展示了**如何在 C# 中使用 OCR**来**从图像中提取文本**、**加载图像进行 OCR**以及**正确设置 OCR 语言**——同时通过异步调用保持 UI 响应。

在这个独立脚本中，你已经拥有了从图片、收据或任何扫描文档中提取文本所需的一切。接下来，你可以扩展到批量处理、添加错误处理，或将结果集成到更大的工作流中。

准备好迈出下一步了吗？尝试将 `OcrLanguage.English` 替换为其他语言，实验不同的图像格式，或将输出挂接到简单的数据库。可能性与待阅读的文档一样广阔。

有问题或遇到卡点？在下方留言，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}