---
category: general
date: 2026-04-26
description: 如何快速批次 OCR PNG 圖像。學習從 PNG 提取文字、將圖像轉換為文字、寫入識別文字，以及使用 Aspose OCR 讀取 PNG
  目錄。
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: zh-hant
og_description: 如何在 C# 中使用 Aspose OCR 批量 OCR PNG 圖像。本指南示範如何從 PNG 中擷取文字、將圖像轉換為文字，並高效寫入辨識出的文字。
og_title: 如何在 C# 中批次 OCR PNG 圖片 – 逐步說明
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中批次 OCR PNG 圖像 – 完整指南
url: /zh-hant/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR PNG 圖像 – 完整指南

有沒有想過 **如何批量 OCR** 整個 PNG 檔案資料夾，而不必為每張圖片寫一個獨立的程式？你並不是唯一要處理數十張螢幕截圖、掃描收據或圖形，並將它們轉換成可搜尋文字的人。在本教學中，我們將一步步示範一個實作方案，能 **從 PNG 提取文字**、**將影像轉換為文字**，以及 **將辨識出的文字寫入個別檔案**——同時自動讀取 PNG 目錄。

閱讀完本指南後，你將擁有一個可直接執行的 C# 主控台應用程式，能一次處理任意數量的影像。無需額外腳本、無需手動複製貼上——只要純粹的程式碼為你完成繁重工作。

## 你需要的條件

- **.NET 6.0** 或更新版本（此程式碼在 .NET Framework 也能正常執行）。  
- **Aspose.OCR for .NET** NuGet 套件（免費試用版可用於測試）。  
- 一個包含若干 *.png* 檔案的資料夾，這些檔案是你想要 OCR 的對象。  
- Visual Studio 2022 或任何你偏好的 C# IDE。

如果你已具備上述條件，我們就可以直接進入實作階段。

## 步驟 1 – 準備輸入與輸出資料夾 *(讀取 PNG 目錄)*

首先，我們要讓程式指向包含影像的資料夾，並決定最終 *.txt* 檔案的存放位置。使用 `Directory.GetFiles` 可以取得目錄中所有 PNG 檔案的乾淨可列舉集合。

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**為什麼這很重要：**  
- 使用通配符 (`*.png`) 可確保只處理影像檔案，忽略其他雜項文件。  
- 即時建立輸出資料夾可避免之後拋出 `DirectoryNotFoundException`。

> **專業提示：** 若需支援其他格式（JPEG、BMP），只要擴充搜尋模式或使用 `Directory.EnumerateFiles` 並傳入多個副檔名即可。

## 步驟 2 – 初始化 OCR 引擎 *(將影像轉換為文字)*

Aspose.OCR 內建兩種引擎類型：基於 CPU 的 `OcrEngine` 與 GPU 加速的 `GpuOcrEngine`。對於大多數批次工作，CPU 引擎已足夠，但若你有支援的 GPU，僅需更換類別名稱即可。

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**為什麼這很重要：**  
- 指定語言可大幅提升準確度，因為引擎會根據預期的字元集進行辨識。  
- 若在大批次處理時遇到效能瓶頸，只需一行程式碼即可切換至 `GpuOcrEngine`。

## 步驟 3 – 建立批次辨識器

Aspose 提供便利的 `BatchRecognizer`，可接受檔案路徑的可列舉集合，並逐一回傳結果。這樣可避免一次將所有影像載入記憶體——對於大型資料夾而言是關鍵細節。

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**為什麼這很重要：**  
- 批次辨識器封裝了迴圈邏輯，讓我們只需關注如何處理每筆結果，而不必擔心安全的遍歷方式。

## 步驟 4 – 對所有影像執行 OCR 並寫入輸出 *(寫入辨識文字)*

現在我們真正執行 OCR。`Recognize` 方法會回傳 `IEnumerable<RecognitionResult>`，其中每筆結果都包含提取的文字及其他中繼資料。

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**為什麼這很重要：**  
- 使用 `File.WriteAllText` 可確保文字預設以 UTF‑8 編碼儲存，保留特殊字元。  
- 遞增的命名方式（`out_0.txt`、`out_1.txt`）與處理順序相符，對除錯很有幫助。

> **邊緣情況：** 若某張影像無法 OCR（例如檔案損毀），`RecognitionResult.Text` 會是空字串。你可以在迴圈內加入簡單檢查，以記錄失敗情形：

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## 步驟 5 – 完整整合 – 完整可執行範例

以下是完整程式碼，你可以直接複製貼上到新的主控台專案中。它包含 `using` 指令、資料夾驗證，以及一個小型的主控台 UI，讓你知道批次何時完成。

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**預期輸出：**  
執行程式時會印出類似以下內容：

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

而且你會在輸出資料夾中看到 `out_0.txt` … `out_11.txt`，每個檔案都包含對應影像的純文字版本。

## 常見問題與技巧

| Question | Answer |
|----------|--------|
| *我可以同時 OCR 子資料夾嗎？* | 可以——將 `Directory.GetFiles` 改為 `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`。 |
| *如果我需要其他語言呢？* | 設定 `ocrEngine.Language = Language.Spanish;`（或任何支援的列舉值）。 |
| *如何處理巨量批次（上千個檔案）？* | 可考慮分批處理，或使用 `Parallel.ForEach` 並限制平行度，以免耗盡記憶體。 |
| *輸出永遠是 UTF‑8 嗎？* | `File.WriteAllText` 預設為 UTF‑8（無 BOM），適用於大多數拉丁語系。對於亞洲文字可能需要明確設定 `Encoding.UTF8`。 |
| *我可以取得信心分數嗎？* | `RecognitionResult` 提供 `Confidence` 屬性——你可以將其與文字一起記錄，以作品質控制。 |

## 視覺概覽 *(批量 OCR 流程圖)*

![批量 OCR 工作流程圖，顯示輸入資料夾 → OCR 引擎 → 批次辨識器 → 輸出 txt 檔案](https://example.com/diagram-how-to-batch-ocr.png "批量 OCR")

*Alt 文字包含主要關鍵字，符合 SEO 圖片需求。*

## 結語

我們剛剛說明了 **如何批量 OCR** PNG 檔案目錄，從讀取 PNG 目錄到寫入每個辨識文字檔案。此解決方案完整自足，能在任何現代 .NET 執行環境上運作，且可擴充為 GPU 加速、多語言支援或平行處理。

準備好進一步了嗎？試著將 `Language.Latin` 換成其他語言，或將輸出整合至搜尋索引，讓文件即時可搜尋。只要掌握了批次 OCR，想像空間無限。

祝程式開發順利，若遇到任何問題，歡迎在留言中告訴我！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}