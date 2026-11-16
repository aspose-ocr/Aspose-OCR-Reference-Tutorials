---
category: general
date: 2026-04-26
description: 快速使用 C# 從 PNG 檔案提取文字。學習如何將圖像轉換為文字、讀取 PNG 檔案、遍歷圖像，以及在幾分鐘內批次進行 OCR 圖像處理。
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: zh-hant
og_description: 使用 C# 快速從 PNG 檔案提取文字。本指南說明如何將圖像轉換為文字、讀取 PNG 檔案、遍歷圖像以及批次 OCR 圖像。
og_title: 從 PNG 擷取文字 – 完整 C# 批次 OCR 教學
tags:
- C#
- OCR
- Aspose
title: 從 PNG 擷取文字 – 完整 C# 批次 OCR 教學
url: /zh-hant/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 PNG 取出文字 – 完整 C# 批次 OCR 教學

有沒有需要 **從 PNG 檔案取出文字**，卻不知道從哪裡開始？你並不孤單——許多開發者在第一次嘗試對一整資料夾的螢幕截圖做 OCR 時，都會卡在這裡。好消息是，只要寫幾行 C# 程式結合 Aspose OCR，就能把影像轉成文字、讀取 PNG 檔、遍歷影像，並一次批次處理全部。

在本教學中，我們會一步步示範一個可直接執行的 Console 應用程式。完成後，你將擁有一個自包含的解決方案，能把目錄中每一個 PNG 的文字抽取出來，並在同一位置產生對應的 `.txt` 檔案。無需額外腳本、無需手動複製貼上——純粹靠程式碼。

## 需要的環境

- **.NET 6 SDK**（或更新的 .NET 版本）。免費、快速，且可在任何平台執行。
- **Aspose.OCR for .NET**（NuGet 套件）。若有相容的 GPU，函式庫會自動使用 GPU 加速，否則會自動回退至 CPU。
- 一個放有若干 **PNG 影像** 的資料夾，供你測試處理。
- 文字編輯器或 IDE——Visual Studio、VS Code、Rider，隨你喜好。

就這些。如果你已經備妥，就可以開始了。

![從 PNG 取出文字範例](image.png "使用 C# 批次 OCR 從 PNG 取出文字示範截圖")

*圖片說明：「使用 C# 批次 OCR 從 PNG 取出文字」*

## 步驟 1 – 建立專案並安裝 Aspose.OCR

首先，建立一個新的 Console 專案，並加入 Aspose OCR 套件。

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

為什麼使用 Console 應用程式？它是執行批次工作最簡單的宿主，你可以從命令列執行，或以排程工具安排。如果日後需要 UI，只要把核心邏輯搬到類別庫即可。

## 步驟 2 – 初始化 GPU 加速的 OCR 引擎（或 CPU 回退）

Aspose 提供 `GpuOcrEngine`，會自動偵測相容的 GPU。若找不到 GPU，會自動切換回一般的 CPU 引擎——不需要額外程式碼。

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

**小技巧：** 若在沒有 GPU 的無頭伺服器上執行，只要把 `GpuOcrEngine` 換成 `OcrEngine`，程式行為完全相同。

## 步驟 3 – 在目標目錄中遍歷影像

我們需要 **遍歷影像**，且只挑選 PNG 檔。`Directory.GetFiles` 會負責大部分工作，我們也會防止資料夾為空的情況。

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

請注意使用 `SearchOption.TopDirectoryOnly`。如果之後需要遞迴子資料夾，只要改成 `AllDirectories`。這個小變更就能讓你 **將影像轉成文字**，在整個目錄樹中一次完成。

## 步驟 4 – 執行 OCR 並儲存結果

現在進入 **批次 OCR 影像** 工作流程的核心。載入每一個 PNG、呼叫 `Recognize()`，再把取得的字串寫入與影像同名的 `.txt` 檔。

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

**為什麼要包在 try/catch 裡？** 真實的影像批次常會遇到損毀檔或使用不常見色彩配置的 PNG。捕捉例外可以避免整個執行中斷，並繼續處理剩餘檔案。

## 步驟 5 – 執行應用程式並驗證輸出

編譯並執行程式：

```bash
dotnet run
```

你應該會在主控台看到類似以下的日誌：

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

打開任一產生的 `.txt` 檔案——那就是抽取出的文字。若檔案為空，請檢查影像品質；OCR 在清晰且高對比的文字上表現最佳。

### 快速驗證腳本（可選）

如果想確認每個 PNG 都已產生對應的文字檔，可以執行以下簡短的 PowerShell 單行指令：

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## 常見變化與邊緣案例

| 情境 | 需要調整的地方 |
|-----------|----------------|
| **非拉丁語系**（例如西里爾文） | 設定 `ocrEngine.Language = Language.Cyrillic;` |
| **大量影像（>10 000 檔）** | 使用 `Parallel.ForEach` 加速處理，但需留意 GPU 記憶體使用量。 |
| **必須保留原始影像順序** | 在 `foreach` 前先對 `pngFiles` 排序（`Array.Sort(pngFiles);`）。 |
| **在沒有 GPU 的 CI 伺服器上執行** | 改用 `OcrEngine` 取代 `GpuOcrEngine`，避免 GPU 初始化錯誤。 |
| **只想處理包含特定關鍵字的檔案** | 取得 `result.Text` 後，先檢查 `result.Text.Contains("Invoice")` 再寫檔。 |

透過這些調整，你可以把 **將影像轉成文字** 的流程套用到幾乎所有可能的情境。

## 完整原始碼（可直接複製貼上）

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

將此檔案存為 `Program.cs`，執行 `dotnet run`，即可看到魔法發生。

## 結語

現在你已掌握 **使用 C# 從 PNG 檔案完整、可投入生產環境的文字抽取方法**。本教學涵蓋了從建立專案、初始化 GPU 加速 OCR 引擎、**遍歷影像**、到 **批次 OCR 影像** 並將結果存為純文字的全部步驟。

如果想進一步探索，可以嘗試：

- **將影像轉成文字** 的其他格式（JPG、BMP）

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}