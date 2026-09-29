---
category: general
date: 2026-02-19
description: 學習如何在 C# 中使用 Aspose.OCR 進行批次 OCR。本指南將向您展示如何從圖像中提取文字，並有效地將圖像轉換為 txt。
draft: false
keywords:
- how to batch ocr
- extract text from images
- convert images to txt
- Aspose OCR batch processing
- C# image to text conversion
language: zh-hant
og_description: 如何在 C# 中使用 Aspose.OCR 批次 OCR。只需幾個簡單步驟，即可從圖像提取文字並將圖像轉換為 txt。
og_title: 如何在 C# 中批次 OCR – 快速圖像轉文字轉換
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中批次 OCR – 快速從圖像提取文字
url: /zh-hant/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批次 OCR – 完整步驟指南

有沒有想過 **如何批次 OCR** 整個資料夾的圖片，而不必為每個檔案寫一個獨立程式？你並不是唯一有此需求的人。許多開發者在需要從數十甚至數千張掃描頁面、收據或螢幕截圖中擷取文字時，都會卡關。好消息是：使用 Aspose.OCR，你可以自動化整個流程，**從影像中擷取文字**，並 **將影像轉換成 txt**，只需幾行程式碼。

本教學將示範一個完整、可直接執行的範例，說明如何建立 OCR 批次處理器、調整前置處理、處理平行運算，並將每個結果寫入 `.txt` 檔案。完成後，你將擁有一個可放入任何 .NET 專案的自包含主控台應用程式。

## 需求

- .NET 6.0 或更新版本（程式碼同樣支援 .NET Core 與 .NET Framework）
- Aspose.OCR for .NET NuGet 套件（`Aspose.OCR`）  
- 一個放有欲處理影像檔案（`.png`、`.jpg` 等）的資料夾
- 适度的記憶體；示範使用 4 個平行執行緒，你可自行調整

不需要外部服務、也不需要隱藏的設定檔——只有純粹的 C# 程式碼，今天就能編譯執行。

![說明批次 OCR 處理流程的圖示](/images/how-to-batch-ocr-flow.png "批次 OCR 流程圖示")

## 步驟 1：安裝 Aspose.OCR 並建立專案

首先，將 Aspose.OCR 套件加入專案：

```bash
dotnet add package Aspose.OCR
```

為什麼要這麼做：Aspose.OCR 內含 OCR 引擎、語言資料與前置處理工具，無需額外第三方二進位檔。安裝套件後，建立一個新的主控台應用程式（或將程式碼加入既有專案），並引用必要的命名空間：

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
```

這些 `using` 陳述式讓你可以使用批次處理類別與便利的 I/O 輔助工具。

## 步驟 2：設定 OCR 批次處理器

接下來，我們會實例化 `OcrBatchProcessor`，並告訴它要辨識的語言、如何清理影像，以及平行執行的執行緒數量。這就是 **如何批次 OCR** 的核心。

```csharp
// Step 2: Create and configure the OCR batch processor
var ocrBatch = new OcrBatchProcessor
{
    // Language selection – English is the most common, but you can change it
    Language = Language.English,

    // Preprocessing improves accuracy; Deskew removes rotation
    Preprocessing = new PreprocessingOptions
    {
        Deskew = DeskewAdvanced.Enable()
    },

    // Parallelism – adjust based on your CPU/GPU capabilities
    MaxDegreeOfParallelism = 4
};
```

**為什麼要啟用 Deskew？** 許多掃描文件並非完全對齊；Deskew 演算法會將它們旋轉回水平基線，通常能提升 10‑15 % 的辨識率。

## 步驟 3：掛接結果回呼以儲存文字檔

批次處理器會在每張影像完成後觸發事件。我們訂閱 `ResultProcessed`，將每筆 OCR 結果寫入 `.txt` 檔——相當於 **將影像轉換成 txt**。

```csharp
// Step 3: Register a callback to save each OCR result as a text file
ocrBatch.ResultProcessed += (sender, args) =>
{
    // Change the original file extension to .txt
    string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");

    // Write the recognized text to the new file
    File.WriteAllText(txtPath, args.Result.Text);

    // Inform the console for debugging / progress monitoring
    Console.WriteLine($"Processed: {args.ImagePath}");
};
```

小技巧：若需保留原始資料夾結構，可自行修改 `txtPath`，加入子資料夾或指定輸出目錄。

## 步驟 4：對影像資料夾執行批次處理

最後，只要把處理器指向放有欲 **從影像中擷取文字** 的資料夾即可。`ProcessFolder` 會遞迴掃描子資料夾，讓你一次拋入整個掃描樹，剩下的交給函式庫處理。

```csharp
// Step 4: Run the batch on all image files in the target folder
ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
```

執行程式時，主控台會顯示類似以下的輸出：

```
Processed: C:\Path\To\Your\Images\invoice1.png
Processed: C:\Path\To\Your\Images\receipt_2024.jpg
...
```

每張影像現在都會在同目錄產生對應的 `.txt` 檔，內含擷取出的文字。

## 完整範例

以下是可直接貼到 `Program.cs` 的完整程式碼：

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR batch processor
        var ocrBatch = new OcrBatchProcessor
        {
            Language = Language.English,
            Preprocessing = new PreprocessingOptions
            {
                Deskew = DeskewAdvanced.Enable()
            },
            // Step 2: Define the level of parallelism (adjust for your CPU/GPU)
            MaxDegreeOfParallelism = 4
        };

        // Step 3: Register a callback to save each OCR result as a text file
        ocrBatch.ResultProcessed += (sender, args) =>
        {
            string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");
            File.WriteAllText(txtPath, args.Result.Text);
            Console.WriteLine($"Processed: {args.ImagePath}");
        };

        // Step 4: Run the batch on all image files in the target folder
        ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
    }
}
```

### 預期輸出

- 對於來源目錄中的每個 `*.png` 或 `*.jpg`，旁邊會出現相對應的 `*.txt` 檔案。
- 主控台會為每個檔案印出一行訊息，提供即時回饋。
- 若影像無法讀取（檔案損毀、格式不支援），Aspose.OCR 會記錄錯誤但繼續處理其他檔案——批次引擎具備內建的韌性。

## 常見問題與特殊情境

### 若要處理 PDF 而非影像該怎麼辦？

Aspose.OCR 能將 PDF 頁面內部轉為影像，但必須先使用例如 Aspose.PDF 之類的工具將 PDF 轉成 raster 影像（如 PNG）。取得 PNG 後，批次程式碼即可直接使用，無需變更。

### 可以即時切換語言嗎？

可以。`Language` 屬性接受任何 `Language` 列舉值（西班牙文、法文、中文等）。若文件包含多語言，建議分兩次執行——每次指定一種語言，或使用 `Language.AutoDetect` 自動偵測。

### 如何限制批次只處理特定檔案類型？

`ProcessFolder` 支援可選的 `SearchOption` 與 `string[] extensions` 參數。例如：

```csharp
ocrBatch.ProcessFolder(@"C:\Images", new[] { ".png", ".tif" });
```

### 有 GPU 加速嗎？

Aspose.OCR 支援透過 `OcrEngine` 設定使用 GPU，但批次處理器的 `MaxDegreeOfParallelism` 仍是主要的併發控制參數。若有相容的 GPU，請在建立 `OcrBatchProcessor` 前於引擎設定中啟用。

### 面對極大型資料夾（數萬檔）該怎麼處理？

- 謹慎提升 `MaxDegreeOfParallelism`；過多執行緒會耗盡記憶體。
- 使用專屬的輸出資料夾，以免產生雜亂。
- 定期將日誌寫入磁碟，防止記憶體膨脹。

## 高品質 OCR 的專業技巧

- **DPI 重要**：300 DPI 以上的影像可獲得最佳準確度。若掃描解析度較低，可在處理前使用雙三次濾波上採樣。
- **降噪**：若來源影像顆粒感強，請開啟 `Preprocessing.NoiseRemoval`。
- **檔名**：保持檔名簡短且僅含英數字；特殊字元可能會干擾回呼路徑邏輯。
- **日誌**：在正式環境建議將 `Console.WriteLine` 換成正式的日誌框架（如 `Serilog`）。

## 後續步驟

掌握 **如何批次 OCR** 後，你可以進一步：

- **從影像中擷取文字**，將結果寫入搜尋索引（例如 Elasticsearch）以支援全文檢索。
- **將影像轉換成 txt**，再利用自然語言處理（NLP）自動分類文件。
- 嘗試 **不同語言套件** 或自訂詞典，以因應特定產業術語。

若想了解後續處理，可參考「使用正規表達式解析 OCR 輸出」或「將 OCR 結果儲存至 SQL 資料庫」等教學。

---

**祝開發順利！** 歡迎自行調整平行度、加入更多前置處理步驟，或將整個流程包裝成 Windows 服務以實現持續監控。結合 Aspose.OCR 的批次功能與 .NET 的創意，天地無限。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}