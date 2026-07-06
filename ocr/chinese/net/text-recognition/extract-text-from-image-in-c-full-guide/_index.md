---
category: general
date: 2026-03-23
description: 使用 Aspose OCR 在 C# 中提取图像文本，并学习如何添加控制台日志记录以实现实时反馈。
draft: false
keywords:
- extract text from image
- add console logger
language: zh
og_description: 使用 Aspose OCR 从图像中提取文本，并添加控制台日志记录器以监控过程。一步一步的 C# 教程。
og_title: 在 C# 中从图像提取文本 – 完整编程指南
tags:
- OCR
- C#
- logging
title: 在 C# 中从图像提取文本 – 完整指南
url: /zh/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从图像中提取文本（C#） – 完整指南

需要快速且可靠地**从图像中提取文本**吗？使用 Aspose OCR，您只需几行 C# 代码即可实现。  
我们还将向您展示如何**添加控制台日志记录器**，以便在终端实时查看 OCR 引擎的进度。

想象一下，您有一张扫描的收据、一张手写笔记，或是保存为 PNG 的 PDF 页面。您希望在不打开笨重 UI 的情况下获取原始字符。本教程将手把手带您完成一个完整的复制粘贴解决方案，适用于 .NET 6+ 以及最新的 Aspose OCR 库。

通过本指南，您将能够：

* 加载图像文件并运行 OCR，以**从图像中提取文本**数据。  
* 将控制台日志记录器挂接到 Aspose AI，以便看到库在后台的实际操作。  
* 使用内置的拼写检查后处理器清理 OCR 错误。  

> **先决条件** – 一个可用的 .NET 开发环境（Visual Studio 2022、VS Code 或 Rider），.NET 6 SDK 或更高版本，以及 Aspose OCR 许可证（或免费试用）。不需要其他第三方包。

---

## 您需要的内容

| 项目 | 为什么重要 |
|------|------------|
| **Aspose.OCR** NuGet 包 | 提供实际读取图像的 `OcrEngine` 类。 |
| **Aspose.OCR.AI** NuGet 包 | 为您提供 `AsposeAI` 后处理框架，包括拼写检查。 |
| **Microsoft.Extensions.Logging**（可选） | 为**添加控制台日志记录器**步骤提供 `ILogger` 接口。 |
| **输入图像** (`input.png`) | 我们将**从图像中提取文本**的源文件。 |

您可以通过终端安装这些包：

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

---

## Step 1 – 使用 Aspose OCR 提取图像文本

首先，我们将图像交给 OCR 引擎。此代码块完成繁重的工作，并返回可能仍包含拼写错误的原始字符串。

```csharp
using Aspose.OCR;
using System;

class OcrDemo
{
    static string PerformOcr(string imagePath)
    {
        // Initialise the OCR engine
        using (OcrEngine ocr = new OcrEngine())
        {
            // Load the image – replace with your own path if needed
            ocr.Image = ImageStream.FromFile(imagePath);

            // Run recognition; if it fails we return an empty string
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }

            // The engine populates the Text property with the recognised characters
            string rawText = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + rawText);
            return rawText;
        }
    }
}
```

**为什么这样有效：**`OcrEngine` 抽象了所有低层图像预处理（二值化、倾斜校正等）。当 `Recognize()` 返回 `true` 时，`Text` 属性已经包含了最佳猜测的字符。  

> **提示：**如果图像较大，考虑在将其送入引擎前将最长边缩放至 ≤ 2000 px。这样可以加快处理速度且不影响准确性。

---

## Step 2 – 添加控制台日志记录器以获得实时洞察

现在我们引入**添加控制台日志记录器**的部分。日志不仅用于调试，还能让您看到模型下载、AI 处理步骤以及库可能发出的任何警告。

```csharp
using Microsoft.Extensions.Logging;
using System;

public class ConsoleLogger : ILogger
{
    // Minimal ILogger implementation that writes to the console.
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool IsEnabled(LogLevel logLevel) => true;

    public void Log<TState>(LogLevel logLevel, EventId eventId,
        TState state, Exception exception, Func<TState, Exception, string> formatter)
    {
        Console.WriteLine($"[{logLevel}] {formatter(state, exception)}");
    }
}
```

您现在可以将此日志记录器插入 Aspose AI：

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**您将看到的内容：**当拼写检查模型自动下载时，控制台会打印类似以下的行：

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

这就是**添加控制台日志记录器**的优势——您再也不必猜测后台操作是否成功。

---

## Step 3 – 配置并注册拼写检查后处理器

Aspose AI 附带一个实用的拼写检查后处理器，可清理常见的 OCR 错误（例如 “rec0gn1ze” → “recognize”）。我们将对其进行配置，可选地告诉库模型的存放位置，然后注册它。

```csharp
// Create the built‑in spell‑check processor
SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

// Optional: tell AsposeAI where to keep downloaded models
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY/Models"
};

// Register the processor with the AI engine
ai.SetPostProcessor(spellProcessor, modelConfig);
```

**为何可能需要自定义路径：**在 CI/CD 流水线中，您通常希望将模型缓存到已知目录，以避免重复下载。`AllowAutoDownload` 标志确保首次运行代码时会获取模型。

---

## Step 4 – 在 OCR 结果上运行后处理器

手握 OCR 文本并准备好拼写检查处理器后，我们将原始字符串交给 `AsposeAI`。引擎运行模型，处理器在内部保存校正后的文本。

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

调用此方法后，`spellProcessor` 将持有一组 `RecognitionResult` 对象，每个对象的 `RecognitionText` 属性包含已清理的版本。

---

## Step 5 – 获取并显示校正后的文本

最后，我们从处理器中提取校正后的字符串并打印。这正是您真正感受到 OCR 与**添加控制台日志记录器**工作流双重优势的时刻。

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**预期输出**（假设图像包含短语 “Aspose OCR demo”，且出现了一些 OCR 小错误）：

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

请注意日志记录器告诉我们模型已就绪，校正后的行也变得整洁。

---

## Step 6 – 清理资源

`AsposeAI` 与 `OcrEngine` 都实现了 `IDisposable`。释放它们可以释放本机内存和文件句柄，这在长期运行的服务中尤为重要。

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

---

## 完整可运行示例

下面是完整程序，您可以将其复制粘贴到新的控制台项目（`dotnet new console`）中。将 `"YOUR_DIRECTORY"` 替换为您机器上的实际文件夹路径。

```csharp
using Aspose.OCR;
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;
using Microsoft.Extensions.Logging; // optional logger
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // ---------- Step 1: OCR ----------
        string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");
        if (string.IsNullOrEmpty(ocrResult)) return;

        // ---------- Step 2: Initialise AI with console logger ----------
        ILogger consoleLogger = new ConsoleLogger(); // implements ILogger
        AsposeAI ai = new AsposeAI(consoleLogger);

        // ---------- Step 3: Spell‑check processor ----------
        SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

        // ---------- Step 4: Model configuration (optional) ----------
        AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
        {
            AllowAutoDownload = true,
            DirectoryModelPath = "YOUR_DIRECTORY/Models"
        };

        // ---------- Step 5: Register and run ----------
        ai.SetPostProcessor(spellProcessor, modelConfig);
        ai.RunPostprocessor(new[] { ocrResult });

        // ---------- Step 6: Show corrected text ----------
        string correctedText = spellProcessor.GetResult()[0].RecognitionText;
        Console.WriteLine("\nCorrected OCR output:\n" + correctedText);

        // ---------- Clean up ----------
        ai.Dispose();
    }

    static string PerformOcr(string imagePath)
    {
        using (OcrEngine ocr = new OcrEngine())
        {
            ocr.Image = ImageStream.FromFile(imagePath);
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }
            string raw = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + raw);
            return raw;
        }
    }
}

// Minimal console logger implementation
public class ConsoleLogger : ILogger
{
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}