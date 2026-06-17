---
category: general
date: 2026-03-21
description: 在 C# 中簡易批次 OCR——學習從圖像提取文字、將圖像轉換為文字，並以語言設定將 OCR 結果儲存為文字。
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: zh-hant
og_description: 在 C# 中批量 OCR 可讓您輕鬆從圖像提取文字、將圖像轉換為文字，並在設定 OCR 語言時將 OCR 結果儲存為文字。
og_title: 如何在 C# 中批次執行 OCR – 快速指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中批次 OCR – 快速從圖像提取文字
url: /zh-hant/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批次 OCR – 快速從圖像提取文字

Ever wondered **how to batch OCR** when you have hundreds of pictures sitting in a folder?  You’re not alone—developers constantly ask how to extract text from images without writing a loop for each file.  The good news is that Aspose.OCR gives you a clean, parallel‑ready way to **convert images to text** in just a few lines of C#.

In this tutorial we’ll walk through a complete, ready‑to‑run example that shows you how to **save OCR as text**, pick the right language, and crank up parallel processing for speed.  By the end you’ll have a self‑contained solution you can drop into any .NET project.

## 需要的環境

- .NET 6 或更新版本（API 支援 .NET Core 與 .NET Framework）
- Aspose.OCR for .NET（NuGet 套件 `Aspose.OCR`）
- 想要處理的圖像資料夾（PNG、JPEG、TIFF 等）
- 對平行程式設計有點好奇（可選，但有助於理解）

No extra services, no cloud keys—just pure C# code that runs locally.

---

![批次 OCR 工作流程](placeholder.png){alt="批次 OCR 工作流程圖"}

## 步驟 1：設定專案並安裝 Aspose.OCR

First things first, spin up a console app (or reuse an existing one) and add the Aspose.OCR package:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **專業提示：** 如果你使用 Visual Studio，右鍵點擊專案 → *Manage NuGet Packages* → 搜尋 *Aspose.OCR* 並安裝最新的穩定版。

This gives you access to `OcrBatchProcessor`, `OcrEngineSettings`, and the enum `Language`.

## 步驟 2：定義輸入與輸出資料夾

The batch processor needs to know where the source images live and where the extracted text files should be written.  Keep the paths absolute or relative to the project root—just make sure the folders exist before you run the code.

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

> **Why this matters:** If the output folder is missing the processor will throw an exception, interrupting the whole batch. Creating it ahead of time guarantees a smooth run.

## 步驟 3：設定 OCR 參數（含語言）

Here’s where you **set OCR language** for the entire batch.  Aspose.OCR supports dozens of languages; English is the default, but you can switch to French, Spanish, etc., by changing the `Language` enum value.

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

If you ever need to process different languages per image, you can later override this setting per file—more on that later.

## 步驟 4：建立 `OcrBatchProcessor` 物件

Now we tie everything together.  The `OcrBatchProcessor` lets you specify the input folder, output folder, output format, parallel options, and the shared settings we just created.

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

> **Why parallelism?**  When you have dozens or hundreds of images, processing them one‑by‑one can be painfully slow.  Setting `MaxDegreeOfParallelism` to 4 lets the runtime use four CPU cores simultaneously, dramatically cutting total time on a typical workstation.

## 步驟 5：執行批次作業

With the processor configured, execution is a single method call.  The library handles file enumeration, OCR, and writing the results automatically.

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

When the console prints *“Batch OCR completed.”* you’ll find a `.txt` file next to each original image inside `BatchResults`.  Each text file contains the raw characters extracted from its source image—exactly what you need to **extract text from images** for downstream processing.

### 預期輸出

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

Open any of those files and you’ll see the plain‑text representation of the image content.

## 步驟 6：驗證結果（可選）

It’s a good habit to double‑check a few files to make sure the OCR performed as expected.  A quick way is to read the first line of each generated file and print it to the console:

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

If you notice garbled characters, consider switching the `Language` setting or tweaking the image quality (e.g., increase DPI, convert to grayscale).

## 進階變化與邊緣案例

### 1. 每檔案語言覆寫
Sometimes a batch contains multilingual documents.  You can inspect each image name and assign a language on the fly:

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. 不同的輸出格式
If you need searchable PDFs instead of plain text, change `OutputFormat`:

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

That will **convert images to text** inside a PDF container, preserving the original layout.

### 3. 處理大型圖像
Very high‑resolution images can blow memory.  To keep the process lightweight, enable image down‑sampling:

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. 錯誤記錄
The processor throws exceptions for unreadable files.  Wrap `Execute` in a try/catch and log the problematic filenames:

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## 完整範例程式

Putting everything together, here’s the complete, copy‑and‑paste‑ready program:

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

Save this as `Program.cs`, build the project, and run `dotnet run`.  You’ll see the console output confirming completion, followed by a short preview of the extracted text.

---

## 結論

We’ve just covered **how to batch OCR** in C# using Aspose.OCR, showing you how to **extract text from images**, **convert images to text**, and **save OCR as text** while **setting OCR language** to match your content.  The example is fully functional, includes parallel processing for speed, and offers hooks for advanced scenarios like per‑file language overrides or PDF output.

Ready for the next step? Try swapping `OcrOutputFormat.PlainText` for `SearchablePdf` and see how easy it is to generate searchable PDFs.  Or experiment with different `MaxDegreeOfParallelism` values to squeeze out every last millisecond on a multi‑core machine.

If you run into hiccups, double‑check the folder paths, ensure the images are readable, and verify the language enum matches the text in your pictures.  Happy coding, and may your OCR batches be swift and accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}