---
category: general
date: 2026-04-26
description: 使用 C# 快速从 PNG 文件中提取文本。了解如何将图像转换为文本、读取 PNG 文件、遍历图像以及在几分钟内批量进行 OCR。
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: zh
og_description: 使用 C# 快速从 PNG 文件中提取文本。本指南展示了如何将图像转换为文本、读取 PNG 文件、遍历图像以及批量 OCR 图像。
og_title: 从 PNG 中提取文本 – 完整的 C# 批量 OCR 教程
tags:
- C#
- OCR
- Aspose
title: 从 PNG 中提取文本 – 完整的 C# 批量 OCR 教程
url: /zh/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 PNG 中提取文本 – 完整的 C# 批量 OCR 教程

是否曾经需要**从 PNG 文件中提取文本**却不知从何入手？你并不孤单——很多开发者在第一次对一整文件夹的截图进行 OCR 时都会遇到这个难题。好消息是，只需几行 C# 代码和 Aspose OCR，你就可以将图像转换为文本，读取 PNG 文件，遍历图像，并一次性批量处理所有文件。

在本教程中，我们将逐步演示一个可直接运行的控制台应用程序，完成上述全部操作。完成后，你将拥有一个独立的解决方案，能够把目录中每个 PNG 的文本提取出来，并在每张图片旁生成对应的 `.txt` 文件。无需额外脚本，无需手动复制粘贴——纯代码实现。

## 所需环境

- **.NET 6 SDK**（或任意更新的 .NET 版本）。免费、快速、跨平台。
- **Aspose.OCR for .NET**（NuGet 包）。如果机器配备兼容的 GPU，库会自动使用 GPU 加速；否则会自动回退到 CPU。
- 一个包含若干**PNG 图像**的文件夹，供你处理。  
- 任意文本编辑器或 IDE——Visual Studio、VS Code、Rider——随你喜欢。

就这些。如果你已经准备好上述环境，即可开始。

![从 PNG 中提取文本示例](image.png "从 PNG 中提取文本演示截图")

*图片说明：“使用 C# 批量 OCR 提取 PNG 文本”*

## 步骤 1 – 创建项目并安装 Aspose.OCR

首先，创建一个新的控制台项目并引入 Aspose OCR 包。

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

为什么使用控制台应用？它是批处理作业最简洁的宿主，你可以在命令行运行或通过任务调度器安排执行。如果以后需要 UI，只需把核心逻辑迁移到类库即可。

## 步骤 2 – 初始化 GPU 加速的 OCR 引擎（或 CPU 回退）

Aspose 提供了 `GpuOcrEngine`，会自动检测支持的 GPU。如果未检测到 GPU，则会回退到普通的 CPU 引擎——无需额外代码。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**小技巧：**如果在没有 GPU 的无头服务器上运行，只需把 `GpuOcrEngine` 替换为 `OcrEngine`，代码行为完全相同。

## 步骤 3 – 遍历目标目录中的图像

我们需要**遍历图像**并仅挑选 PNG 文件。`Directory.GetFiles` 方法负责大部分工作，我们还会对空文件夹进行防护。

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

请注意使用了 `SearchOption.TopDirectoryOnly`。如果以后需要递归子文件夹，只需改为 `AllDirectories`。这一个小改动就能让你**将图像转换为文本**，遍历整个目录树。

## 步骤 4 – 执行 OCR 并保存结果

下面进入**批量 OCR 图像**工作流的核心。我们加载每个 PNG，调用 `Recognize()`，并将提取的字符串写入与之同名的 `.txt` 文件。

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**为什么要用 try/catch 包裹？**真实的图像批次常常会出现损坏文件或使用不常见色彩配置的 PNG。捕获异常可以防止整个运行崩溃，并继续处理剩余文件。

## 步骤 5 – 运行应用并验证输出

构建并启动应用：

```bash
dotnet run
```

你应该会看到类似下面的控制台日志：

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

打开任意生成的 `.txt` 文件——文本已被提取。如果文件为空，请检查图像质量；OCR 在清晰、高对比度的文字上表现最佳。

### 快速验证脚本（可选）

如果想确认每个 PNG 都生成了对应的文本文件，可以运行下面这行 PowerShell 单行脚本：

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## 常见变体与边缘情况

| 场景 | 需要更改的内容 |
|-----------|----------------|
| **非拉丁语言**（例如西里尔文） | 设置 `ocrEngine.Language = Language.Cyrillic;` |
| **大规模图像集（>10 000 文件）** | 使用 `Parallel.ForEach` 加速处理，但需关注 GPU 内存使用。 |
| **需要保持原始图像顺序** | 在 `foreach` 之前对 `pngFiles` 进行排序（`Array.Sort(pngFiles);`）。 |
| **在没有 GPU 的 CI 服务器上运行** | 将 `GpuOcrEngine` 替换为 `OcrEngine`，避免 GPU 初始化错误。 |
| **只想处理包含特定关键字的文件** | 在获取 `result.Text` 后，检查 `result.Text.Contains("Invoice")` 再决定是否写文件。 |

通过这些微调，你可以将**将图像转换为文本**的流水线几乎适配任何场景。

## 完整源代码（可直接复制粘贴）

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

将其保存为 `Program.cs`，运行 `dotnet run`，即可看到奇迹发生。

## 结论

现在，你已经掌握了使用 C# **完整、可投产的从 PNG 文件中提取文本**的方法。本教程涵盖了从项目搭建、初始化 GPU 加速 OCR 引擎、**遍历图像**、到**批量 OCR 图像**并保存为纯文本的全部步骤。

如果你想进一步探索，可以尝试：

- 为其他格式（JPG、BMP 等）**将图像转换为文本**...

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}