---
category: general
date: 2026-04-03
description: 學習如何在 C# 中使用 Aspose.OCR 進行批次 OCR。本指南將示範如何從 PNG 圖像提取文字，並高效地將圖像轉換為文字。
draft: false
keywords:
- how to batch ocr
- extract text png
- convert images to text
- Aspose OCR
- C# parallel processing
language: zh-hant
og_description: 了解如何在 C# 中批量執行 OCR，從 PNG 圖像中擷取文字，並使用 Aspose.OCR 將圖像轉換為文字。提供完整程式碼。
og_title: 如何在 C# 中批次 OCR – 快速指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中批次 OCR – 快速提取 PNG 檔案文字
url: /zh-hant/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批次 OCR – 快速提取 PNG 檔案文字

有沒有想過 **如何批次 OCR** 整個資料夾的螢幕截圖，而不必為每個檔案寫迴圈？你並非唯一有此需求的人。在許多專案中——例如發票數位化或掃描收據的歸檔——你會面對數十甚至數百個需要提取文字的 PNG 檔案。好消息是？使用 Aspose.OCR，你可以 **extract text PNG** 圖片並行處理，整個流程只需幾行 C# 程式碼即可完成。

在本教學中，我們將一步步示範完整、可直接執行的範例，說明如何使用批次處理器 **convert images to text**。我們會列出前置條件、解釋每一行程式碼的意義，並提供一些實用小技巧，避免日後常見的陷阱。

## 前置條件

在開始之前，請確保你已具備：

- **.NET 6.0**（或更新版本）已安裝於你的機器上。較舊的執行環境亦可使用，但最新版在效能與 async 支援上更佳。
- **Aspose.OCR for .NET** 套件。可透過 NuGet 取得：`dotnet add package Aspose.OCR`。
- 一個放有欲處理 **PNG** 圖片的資料夾，我們在教學中會以 `YOUR_DIRECTORY` 代表。
- 適度的記憶體——批次 OCR 若平行度過高會較耗記憶體，但使用 `Environment.ProcessorCount` 可保持安全。

> **Pro tip:** 若你在 CI/CD 流程中執行，請將 Aspose 授權檔以機密方式加入，以避免免費評估版的 20 頁限制。

現在，讓我們動手實作。

## 步驟 1：設定批次 OCR 處理器（標題中的主要關鍵字）

首先，你需要建立一個 `BatchOcrProcessor` 實例。此類別將執行緒的細節抽象化，讓你只需關注每張圖片的處理方式。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Create a batch OCR processor and tell it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };
```

**為什麼這很重要：**  
- `Engine = new OcrEngine()` 為每個執行緒提供全新的 OCR 引擎，避免資源競爭。  
- `MaxDegreeOfParallelism = Environment.ProcessorCount` 會自動依 CPU 核心數調整平行度，讓效能達到最佳而不需手動調校。

## 步驟 2：掛接進度事件（協助追蹤提取狀態）

在處理上百個檔案時，顯示進度相當重要。`ProgressChanged` 事件會在每個檔案完成後觸發，讓你記錄當前狀態。

```csharp
        // Subscribe to progress updates so we know which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");
```

**你會喜歡的原因：**  
- 即時回饋可避免你懷疑程式是否卡住。  
- 若需暫停或取消，已經有 `e.Current` 與 `e.Total` 可供檢查。

## 步驟 3：定義資料夾掃描與檔案模式（Extract Text PNG）

接下來告訴處理器要搜尋哪裡、挑選什麼類型的檔案。`"*.png"` 模式確保只處理 PNG 圖片。

```csharp
        // Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"YOUR_DIRECTORY",          // folder containing the images
            "*.png",                    // file pattern
            (imagePath, ocrText) =>     // callback for each processed file
            {
                // Step 4 is inside this callback – see next section
            });
```

**此步驟的關鍵所在：**  
- 使用 glob 模式讓程式更具彈性；日後若需處理 JPEG，只要把 `*.png` 改成 `*.jpg` 即可。  
- 回呼函式同時取得圖片路徑與辨識文字，讓你能自行決定後續動作。

## 步驟 4：將辨識文字儲存於原檔旁（Convert Images to Text）

在回呼函式內，我們會把 OCR 輸出寫入與原 PNG 同目錄的 `.txt` 檔案。這是 **convert images to text** 最簡單的方式，方便後續處理。

```csharp
                // Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
```

**為什麼選擇並排的 `.txt` 檔案：**  
- 關係一目了然——打開 PNG，同時打開 TXT 進行比對。  
- 小規模專案不需要資料庫或額外的儲存層。

## 步驟 5：以友善的完成訊息收尾

簡潔的主控台訊息會告訴你全部工作已完成。

```csharp
        // Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

執行程式後，你會看到類似以下的輸出：

```
Processed 1/27: C:\Images\invoice1.png
Processed 2/27: C:\Images\invoice2.png
...
Batch processing completed.
```

每個 PNG 現在都有相對應的 `.txt` 檔，內含提取出的文字。

## 完整可執行範例（結合所有步驟）

以下是可直接貼到新 Console 專案的完整程式碼。只要將 `YOUR_DIRECTORY` 替換成圖片的絕對路徑即可。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create a batch OCR processor and configure it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 2: Subscribe to progress updates to see which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");

        // Step 3: Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"C:\MyImages",          // folder containing the images
            "*.png",                // file pattern
            (imagePath, ocrText) => // callback for each processed file
            {
                // Step 4: Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
            });

        // Step 5: Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

### 預期結果

- 對於 `C:\MyImages` 中的每個 `image.png`，都會在旁邊產生 `image.txt`。  
- 主控台會列印進度行，方便監控大量批次。  
- 不需要自行寫迴圈或管理執行緒——`BatchOcrProcessor` 會處理所有細節。

## 常見問題與邊緣情況

### 我的圖片不是 PNG 該怎麼辦？

只要將 `ProcessFolder` 的第二個參數改成 `"*.jpg"` 或 `"*.*"`，即可包含所有檔案。OCR 引擎支援大多數點陣圖格式。

### 這會消耗多少記憶體？

`BatchOcrProcessor` 會在每個執行緒載入一張圖片。若 `Environment.ProcessorCount` 為 8 核心，則同時會有八張圖片佔用記憶體。若遇到 OutOfMemory 例外，請降低平行度：

```csharp
MaxDegreeOfParallelism = 4; // or any number that fits your machine
```

### 可以自訂 OCR 語言嗎？

當然可以。建立引擎後，設定其 `Language` 屬性：

```csharp
Engine = new OcrEngine { Language = Language.English };
```

Aspose 支援多種語言；如有需要，只要加入相應的 NuGet 套件即可。

### 錯誤處理該怎麼做？

在回呼函式中加入 try/catch，將失敗情況記錄下來。處理器會繼續處理下一個檔案，避免單一損壞的圖片中斷整個執行。

```csharp
(imagePath, ocrText) =>
{
    try
    {
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, ocrText);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {imagePath}: {ex.Message}");
    }
}
```

## 大規模擴充的實用技巧

- **分批資料夾**：若檔案數量達到數萬，請將它們切分成子資料夾，依序執行多個批次工作。  
- **使用雲端 VM**：核心數更多的機器（例如 32 核心）可大幅縮短完成時間。記得同步調整授權限制。  
- **後處理文字**：提取完畢後，可能需要使用正規表達式抽取發票號碼或日期。`.txt` 檔正好是此類管線的理想輸入。

## 結論

你現在已掌握一套完整、可投入生產環境的 **how to batch OCR** 方案，能夠批次處理 PNG 目錄、**extract text PNG** 檔案，並使用 Aspose.OCR 在 C# 中 **convert images to text**。此範例自給自足，說明了每行程式碼背後的「為什麼」，同時提供了處理更大工作負載或不同檔案類型的技巧。

準備好進一步了嗎？可以改寫回呼函式，將結果寫入資料庫，或在 OCR 前加入影像前處理（例如去斜）。此模式具備良好擴充性，能因應任何批次處理情境。

祝開發順利，願你的 OCR 流程快速且零錯誤！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}