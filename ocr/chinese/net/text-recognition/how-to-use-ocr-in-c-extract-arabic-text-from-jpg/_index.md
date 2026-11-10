---
category: general
date: 2026-03-21
description: 如何在 C# 中使用 OCR 识别图像文件中的文本。学习从 JPG 中提取阿拉伯语文本并将其转换为纯文本。
draft: false
keywords:
- how to use OCR
- extract arabic text
- recognize text from image
- image to text c#
- convert jpg to text
language: zh
og_description: 如何在 C# 中使用 OCR 识别图像文件中的文本。本指南展示了如何从 JPG 中提取阿拉伯语文本并将其转换为可编辑的文本。
og_title: 如何在 C# 中使用 OCR — 从 JPG 中提取阿拉伯语文本
tags:
- OCR
- C#
- Aspose
- Arabic
title: 如何在 C# 中使用 OCR – 从 JPG 中提取阿拉伯文文本
url: /zh/net/text-recognition/how-to-use-ocr-in-c-extract-arabic-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 从 JPG 中提取阿拉伯文文本

有没有想过 **如何使用 OCR**，当你手头有一张存放在硬盘上的阿拉伯文字图片时？你并不是唯一的遇到这种情况的人。许多开发者都会碰到同样的难题：他们有一张 JPEG，需要获取其中的文字，却不想从头手写神经网络。

好消息是？只需几行 C# 代码，你就可以 **从图像识别文本**，提取出每一个阿拉伯字符，并得到一个干净的字符串，方便存储、搜索或显示。在本教程中，我们将完整演示整个过程——安装库、配置语言模型、运行扫描，最后打印结果。完成后，你将能够在几秒钟内 **将 JPG 转换为文本**。

## 你将学到

- 为 .NET 安装 Aspose.OCR NuGet 包。
- 在 CPU 模式下初始化 OCR 引擎（适合小型任务）。
- 自动加载阿拉伯语言模型。
- 对 JPEG 图像执行 OCR 并获取识别的文本。
- 处理常见的坑，如大文件或缺少语言数据。

不需要任何 OCR 经验；只要对 C# 和 Visual Studio 有基本了解即可。准备好了吗？让我们开始吧。

## 为 .NET 安装 Aspose OCR

在运行任何代码之前，你需要先获取 Aspose.OCR 库。它以 NuGet 包的形式提供，安装只需一条命令：

```bash
dotnet add package Aspose.OCR
```

或者，如果你更喜欢 Visual Studio UI，打开 **Tools → NuGet Package Manager → Manage NuGet Packages for Solution**，搜索 **Aspose.OCR**，然后点击 **Install**。该包会把所有必需的内容都拉进来，包括引擎首次使用时会下载的语言数据文件。

> **专业提示：** 将项目目标设为 .NET 6 或更高版本；旧版框架仍可工作，但会错失性能提升。

## 初始化 OCR 引擎

库已经就位后，我们可以创建 `OcrEngine` 实例。对于大多数小规模任务，默认的 CPU 模式已经足够——它使用主机的处理器，避免了 GPU 加速所需的额外配置。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialise the OCR engine (CPU mode is sufficient for small jobs)
var ocrEngine = new OcrEngine();
```

为什么每次都创建一个新引擎？`OcrEngine` 对象保存了语言、DPI、输出格式等配置信息。将其限定在单次操作的作用域内，可确保状态干净，避免不同语言模型之间的意外交叉。

## 加载阿拉伯语言模型

Aspose 会按需提供语言包。第一次为 `Language.Arabic` 赋值时，库会下载大约 30 MB 的数据到本机的缓存文件夹。此一次性下载后，后续运行将快如闪电。

```csharp
// Choose the language model to load.
// The first assignment triggers an automatic download of the language data (~30 MB).
ocrEngine.Settings.Language = Language.Arabic;
```

如果以后需要支持其他脚本（比如英文或印地语），只需更改枚举值——无需额外代码。引擎会为每种语言单独缓存。

## 对 JPG 图像执行 OCR

引擎准备好且阿拉伯模型已加载后，指向你想处理的图像即可。路径可以是绝对或相对的，只要确保文件存在且可读。

```csharp
// Run OCR on the input image.
var recognitionResult = ocrEngine.Recognize(@"YOUR_DIRECTORY/arabic_doc.jpg");
```

**边缘情况：** 如果你的 JPEG 很大（超过 5 MB），建议先将其缩小。大图会增加内存占用并减慢识别速度。使用 `System.Drawing` 或 `ImageSharp` 进行快速预缩放可以显著缩短处理时间。

## 获取并显示识别的文本

`Recognize` 方法返回一个 `OcrResult` 对象。其 `Text` 属性包含引擎能够读取的纯文本表示。

```csharp
// Retrieve the recognised text and output it.
string extractedText = recognitionResult.Text;
Console.WriteLine(extractedText);
```

运行程序后，你应该能在控制台看到阿拉伯字符，保持原始顺序和换行。如果想把文本写入文件，只需使用 `File.WriteAllText`。

### 完整可运行示例

将上述步骤整合起来，下面是一个完整的、可直接运行的控制台应用示例：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine (CPU mode works fine for most cases)
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the Arabic language pack – triggers a one‑time download (~30 MB)
        ocrEngine.Settings.Language = Language.Arabic;

        // 3️⃣ Specify the image path – replace with your actual file location
        string imagePath = @"YOUR_DIRECTORY/arabic_doc.jpg";

        // 4️⃣ Run OCR and capture the result
        var result = ocrEngine.Recognize(imagePath);

        // 5️⃣ Extract the text and display it
        string extractedText = result.Text;
        Console.WriteLine("=== Extracted Arabic Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**预期输出（示例）：**

```
=== Extracted Arabic Text ===
هذا نص تجريبي باللغة العربية
تم استخراج هذا النص بنجاح
```

如果输出出现乱码，请再次确认图像清晰且语言已设置为 `Arabic`。模糊的扫描或旋转的页面是 OCR 常见的失败原因。

## 常见问题与技巧

- **如果图像同时包含阿拉伯文和英文怎么办？**  
  设置 `ocrEngine.Settings.Language = Language.Multilingual;` 让 Aspose 自动检测多种脚本。

- **能用 GPU 加速处理吗？**  
  可以——如果你的机器配备兼容的显卡并已安装 CUDA 运行时，使用 `new OcrEngine(OcrEngineMode.Gpu)` 替代默认引擎。

- **如何在 UI 中处理从右到左的渲染？**  
  原始字符串是 Unicode；大多数现代 UI 框架（WinForms、WPF、ASP.NET）在设置相应的 `FlowDirection` 后会自动支持 RTL 布局。

- **图像大小有没有限制？**  
  技术上没有，但分辨率越高内存消耗越大。对于超大扫描（例如整本书），建议一次处理一页。

## 可视化概览

下面是一张简易示意图，展示了从图像文件到提取文本的流程。

![如何使用 OCR 流程图 – 图像转文本转换](/images/ocr-flow.png)

*Alt text:* *展示在 C# 中将图像转换为文本的 OCR 流程图。*

## 后续步骤

现在你已经掌握了 **如何在 C# 中使用 OCR** 来 **从阿拉伯文 JPEG 中提取文本**，可以进一步扩展解决方案：

- **批量处理：** 遍历文件夹中的图像，为每个结果写入单独的 `.txt` 文件。
- **后处理：** 使用正则表达式清理多余的标点或换行。
- **集成：** 将提取的字符串导入搜索索引（如 Azure Cognitive Search），实现对扫描文档的全文检索。

如果想尝试其他语言，只需替换 `Language` 枚举值。想要提取表格或手写笔记？Aspose.OCR 还提供 `LayoutAnalysis` 功能，可在识别前对块进行分割。

---

### TL;DR

你现在已经了解 **如何在 C# 中使用 OCR** 来 **从 JPEG 中提取阿拉伯文文本**，即 **从图像识别文本** 并 **将 JPG 转换为文本**。上面的完整可运行示例演示了从安装 NuGet 包到打印最终字符串的每一步。拿一张示例图片，粘贴代码，观看魔法发生——无需外部服务。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}