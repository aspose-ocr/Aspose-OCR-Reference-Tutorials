---
category: general
date: 2026-03-23
description: 使用 Aspose OCR 在 C# 中提取图像文本。了解如何加载图像进行 OCR 并异步创建 OCR 引擎。
draft: false
keywords:
- extract text from image
- load image for OCR
- create OCR engine
- asynchronous OCR C#
- Aspose OCR guide
- C# image processing
language: zh
og_description: 使用 Aspose OCR 在 C# 中从图像提取文本。本教程展示了如何加载用于 OCR 的图像以及创建用于异步识别的 OCR 引擎。
og_title: 从图像提取文本 – C# 异步 OCR 指南
tags:
- OCR
- C#
- Aspose
title: 在 C# 中从图像提取文本 – 异步 OCR 教程
url: /zh/net/text-recognition/extract-text-from-image-in-c-async-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本 – 完整的 C# 异步 OCR 指南

是否曾需要**从图像中提取文本**却不确定该选哪个 API？你并不孤单。在许多实际项目中——比如发票扫描器、收据应用或快速查看工具——从图片中提取文字是日常需求。

在本教程中，我们将完整演示如何使用 Aspose.OCR **从图像中提取文本**，涵盖从**加载图像进行 OCR**到**创建 OCR 引擎**并异步运行整个过程。完成后，你将拥有一个可直接运行的程序，它会在控制台打印识别出的文本，并且你会明白每一步的意义。

## 你将学到

- 如何安全地**创建 OCR 引擎**并正确释放资源。  
- 使用 Aspose 的 `ImageStream` 正确**加载图像进行 OCR**。  
- 如何调用 `RecognizeAsync()` 并处理成功或失败的情况。  
- 常见陷阱的排查技巧（缺少字体、不支持的格式等）。  
- 预期的控制台输出，以便验证一切正常。

### 前置条件

- .NET 6.0 SDK 或更高版本（代码在 .NET Core 和 .NET Framework 上均可编译）。  
- Visual Studio 2022 或任何支持 C# 的编辑器。  
- 已在项目中添加 Aspose.OCR NuGet 包（`Aspose.OCR`）。  
- 一个示例 PNG/JPG 图像（`input.png`），放置在可引用的文件夹中。

无需额外库——Aspose 已经处理了所有繁重的工作。

![从图像中提取文本示例](https://example.com/ocr-result.png "截图显示提取的文本 – 从图像中提取文本")

## 第一步 – 安装 Aspose.OCR 并设置项目

在我们能够**创建 OCR 引擎**之前，需要先确保库已经可用。

```bash
dotnet new console -n AsyncOcrDemo
cd AsyncOcrDemo
dotnet add package Aspose.OCR
```

> **专业提示：** 保持 NuGet 包为最新版本。截至 2026 年 3 月的最新 Aspose.OCR 版本已对异步调用进行性能优化。

## 第二步 – 创建 OCR 引擎（并确保正确释放）

下面的代码块演示了如何在 `using` 语句中**创建 OCR 引擎**。这能保证非托管资源被释放，对于长期运行的服务至关重要。

```csharp
using Aspose.OCR;
using System;
using System.Threading.Tasks;

class AsyncDemo
{
    static async Task Main()
    {
        // Step 2.1: Instantiate the OCR engine – this is where we **create OCR engine**
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // The rest of the steps go here…
        }
    }
}
```

**为什么要使用 `using`？**  
`OcrEngine` 包装了原生代码；如果忘记释放，它可能导致内存或文件句柄泄漏，在处理大量图像时会出现间歇性崩溃。

## 第三步 – 加载图像进行 OCR

现在我们来**加载图像进行 OCR**。Aspose 提供的 `ImageStream.FromFile` 抽象了位图处理，并支持大多数常见格式。

```csharp
// Step 3.1: Define the path to the picture you want to process
string imagePath = "YOUR_DIRECTORY/input.png";

// Step 3.2: Feed the image into the engine
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **注意：** 如果路径错误或文件损坏，`RecognizeAsync()` 将返回 `false`。在调用 OCR 方法前务必确认文件存在。

## 第四步 – 运行异步 OCR 识别

调用 `RecognizeAsync()` 会将繁重的图像分析工作转移到后台线程，从而保持 UI 响应或 Web 接口非阻塞。

```csharp
// Step 4.1: Perform the async recognition
bool recognitionSucceeded = await ocrEngine.RecognizeAsync();
```

**内部到底发生了什么？**  
Aspose 会将图像划分为多个区域，对每个区域运行神经网络，然后合并结果。异步版本仅仅是把整个流水线包装成一个 `Task`，让 .NET 线程池管理执行。

## 第五步 – 获取并显示提取的文本

如果异步调用成功，`Text` 属性现在就保存了你想要**从图像中提取的文本**。我们把它打印出来。

```csharp
// Step 5.1: Show the outcome
if (recognitionSucceeded)
    Console.WriteLine("Async OCR result:\n" + ocrEngine.Text);
else
    Console.WriteLine("Async recognition failed.");
```

### 预期输出

```
Async OCR result:
Hello, world!
This is a sample image containing text.
```

如果看到上述内容（或你自己的图像内容），说明你已经成功使用 Aspose OCR **从图像中提取文本**。

## 完整、可运行的示例

将所有代码组合在一起，下面的完整程序可以直接复制到 `Program.cs` 并运行。

```csharp
using Aspose.OCR;
using System;
using System.Threading.Tasks;

class AsyncDemo
{
    static async Task Main()
    {
        // Step 1: Create OCR engine (ensures proper disposal)
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // Step 2: Load the image you want to process – this is how we **load image for OCR**
            string imagePath = "YOUR_DIRECTORY/input.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Step 3: Run the asynchronous recognition – this is the core of **extract text from image**
            bool recognitionSucceeded = await ocrEngine.RecognizeAsync();

            // Step 4: Display the result or an error message
            if (recognitionSucceeded)
                Console.WriteLine("Async OCR result:\n" + ocrEngine.Text);
            else
                Console.WriteLine("Async recognition failed.");
        }
    }
}
```

运行方式：

```bash
dotnet run
```

如果一切配置正确，控制台将打印出提取的文本。

## 常见问题与边缘情况

### 如果需要处理 JPEG 而不是 PNG 怎么办？

`ImageStream.FromFile` 会自动检测格式，所以只需把 `imagePath` 指向 `photo.jpg`，无需更改代码。请确保文件大小不要过大——Aspose 建议图像尺寸不超过 5 MB，以获得最佳速度。

### 能否更改语言或字符集？

可以。创建引擎后，设置 `ocrEngine.Language = OcrLanguage.English;`（或其他受支持语言）。这会提升非拉丁文字的识别准确度。

### 如何处理多页（例如多页 TIFF）？

Aspose.OCR 可以逐页处理。遍历每一页，将其分配给 `ocrEngine.Image`，并对每一次迭代调用 `RecognizeAsync()`。如果需要单一输出字符串，可将结果收集到 `StringBuilder` 中。

### 如果异步调用一直不返回怎么办？

这通常意味着内存不足或图像损坏。可以使用 `try/catch` 包裹调用，并通过 `Task.WhenAny` 设置超时：

```csharp
var recognitionTask = ocrEngine.RecognizeAsync();
if (await Task.WhenAny(recognitionTask, Task.Delay(5000)) == recognitionTask)
{
    // success path
}
else
{
    Console.WriteLine("Recognition timed out.");
}
```

## 性能技巧

- 在批量处理大量图像时**复用 OCR 引擎**；为每个文件创建新引擎会增加开销。  
- 在送入引擎前**将大图像缩放至最大宽度 2000 像素**；这能加快分析速度且不会显著影响准确度。  
- 如许可证允许，可通过设置 `ocrEngine.UseGpu = true;` **启用硬件加速**。

## 结论

现在你拥有一个完整的端到端示例，展示了如何在 C# 中使用 Aspose OCR **从图像中提取文本**。通过学习**加载图像进行 OCR**、**创建 OCR 引擎**以及运行 `RecognizeAsync()`，你可以将可靠的文本提取功能集成到桌面应用、Web 服务或后台任务中。

准备好下一步了吗？尝试替换为 PDF，实验不同语言，或将 OCR 输出写入搜索索引。可能性几乎无限，而使用异步模式可以让你在后台完成繁重工作时不阻塞主线程。

祝编码愉快，愿你的图像始终足够清晰以实现精准 OCR！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}