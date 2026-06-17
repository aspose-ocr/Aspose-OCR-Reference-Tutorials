---
category: general
date: 2026-03-13
description: 如何在 C# 中使用 OCR 提取扫描件文本。学习使用 Aspose OCR 将 TIFF 转换为文本、GPU 加速以及一步步的代码示例。
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: zh
og_description: 如何在 C# 中使用 OCR 从扫描件中提取文本。本指南展示了如何使用 Aspose OCR 和 GPU 加速将 TIFF 转换为文本。
og_title: 如何在 C# 中使用 OCR – 快速从扫描中提取文本
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中使用 OCR – 快速从扫描件中提取文本
url: /zh/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 快速从扫描件中提取文本

Ever wondered **how to use OCR** to pull readable text out of a stack of scanned TIFF files? You're not the only one. In many real‑world projects—think invoice digitisation, archival of historic documents, or simply making PDFs searchable—developers need a reliable way to **extract text from scans** without breaking a sweat.

The good news? With Aspose OCR and a few lines of C# you can convert TIFF to text in a matter of seconds, even on a modest workstation. Below you’ll get a complete, ready‑to‑run example, plus the reasoning behind each choice so you can adapt it to your own workflow.

## 您需要的准备

Before we dive in, make sure you have the following on hand:

| 前置条件 | 为什么重要 |
|--------------|----------------|
| .NET 6+ (or .NET Framework 4.7+) | Aspose OCR NuGet 包面向现代 .NET 运行时。 |
| Visual Studio 2022 (or any IDE you like) | 提供 IntelliSense 和便捷的调试功能。 |
| A CUDA‑compatible GPU & driver (optional) | 通过 `ocrEngine.UseGpu = true` 为大批量处理提供显著的速度提升。 |
| A folder of TIFF images you want to process | 本教程使用 `*.tif` 文件，你可以自行调整匹配模式。 |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | 执行核心 OCR 功能的库。 |

If you’re missing any of these, grab them now—no point in reading further only to hit a missing dependency later.

## 方案概览

At a high level the program does three things:

1. **Create an OCR engine** and optionally turn on GPU acceleration.  
2. **Iterate over every TIFF file** in a directory, run recognition, and capture the resulting plain‑text.  
3. **Write the text** to a `.txt` file sitting next to the original image.

That’s it. The code is deliberately tiny, yet it showcases best practices like explicit language selection, proper resource disposal, and error handling for the most common edge cases.

![如何在 C# 中使用 OCR 示例](/images/how-to-use-ocr-csharp.png "展示如何在 C# 中使用 OCR 从扫描件中提取文本的示意图")

## 步骤 1：初始化 OCR 引擎（How to Use OCR）

The first thing you need is an instance of `OcrEngine`. This object is the gateway to all Aspose OCR functionality. By default it works on the CPU, but setting `UseGpu = true` tells the library to offload the heavy matrix calculations to your graphics card—provided you have a CUDA‑compatible driver installed.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Why this matters:**  
- **GPU acceleration** can cut processing time by up to 70 % for high‑resolution scans.  
- **Explicit language selection** avoids the engine guessing and improves accuracy, especially for non‑Latin scripts.

## 步骤 2：指向扫描文件所在位置（Convert TIFF to Text）

Next we tell the program where to look for the images. Using `Directory.GetFiles` with a `*.tif` filter keeps the logic simple and avoids pulling in unrelated files like `.jpg` or `.png`.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Edge case note:** If the directory is empty, the loop below simply never executes, which is perfectly fine. You’ll see a friendly “No files found” message later.

## 步骤 3：处理每个 TIFF 文件（Extract Text from Scans）

Now the heart of the program: loading each image, running OCR, and persisting the output. The `ImageStream.FromFile` helper streams the file directly into memory, which is more efficient than loading a `Bitmap` first.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Why we wrap each iteration in a `try/catch`:**  
Scanning a batch of documents is messy; a corrupted TIFF or an out‑of‑memory hiccup shouldn’t abort the whole run. The catch block logs the problem and moves on, keeping the pipeline robust.

### 预期输出

For every `example.tif` you’ll find a sibling `example.txt` containing something like:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

If the OCR engine can’t read a line, it will simply leave a blank line or a garbled character—nothing crashes.

## 步骤 4：清理与释放（Best Practice）

`OcrEngine` implements `IDisposable`, so it’s polite to free native resources when you’re done. In a short console app you could rely on the GC, but explicit disposal is a habit worth forming.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## 完整可运行示例（Copy‑Paste Ready）

Below is the complete program you can paste into a new Console App project. It compiles as‑is, assuming you’ve added the Aspose.OCR NuGet package.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### 快速检查清单

- **GPU 标志** – 如果没有 CUDA 驱动，请删除或设为 `false`。  
- **语言** – 将 `Language.English` 替换为其他受支持的语言。  
- **文件模式** – 如扫描文件为其他格式，可将 `"*.tif"` 改为 `"*.png"` 或 `"*.*"`。  

## 常见陷阱与专业提示（c# OCR tutorial）

| 陷阱 | 如何避免 |
|---------|-----------------|
| **Out‑of‑memory errors** on huge batches | 将文件分批处理，或在每处理 50 个文件后调用 `GC.Collect()`（通常不必）。 |
| **GPU not detected** but `UseGpu = true` | 引擎会静默回退到 CPU，你可以在构造后检查 `ocrEngine.IsGpuAvailable`。 |
| **Wrong language pack** leads to garbled output | 始终显式设置 `ocrEngine.Language`；默认可能是 `Language.Unknown`。 |
| **File path contains Unicode characters** | 使用 `Path.GetFullPath` 进行规范化，或在 Windows 上对超长路径前缀 `@"\\?\"`。 |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}