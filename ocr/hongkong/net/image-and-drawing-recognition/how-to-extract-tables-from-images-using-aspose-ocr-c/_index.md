---
category: general
date: 2026-03-28
description: 學習如何使用 Aspose OCR 在 C# 中從圖像中提取表格。本指南涵蓋如何在圖像中偵測表格、載入圖像進行 OCR 以及從 PNG 檔案中提取表格。
draft: false
keywords:
- how to extract tables
- extract table from image
- detect tables in image
- load image for ocr
- extract tables from png
language: zh-hant
og_description: 逐步教學：如何使用 Aspose OCR 在 C# 中從圖像中提取表格。包括程式碼、說明以及檢測圖像檔案中表格的技巧。
og_title: 如何使用 Aspose OCR (C#) 從圖像中提取表格
tags:
- Aspose OCR
- C#
- Table Extraction
title: 如何使用 Aspose OCR（C#）從圖片中提取表格
url: /zh-hant/net/image-and-drawing-recognition/how-to-extract-tables-from-images-using-aspose-ocr-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR (C#) 從圖像中提取表格

有沒有想過 **如何從掃描的發票或試算表截圖中提取表格**？你並不是唯一有此需求的人。在許多實務專案中，我們需要把表格的圖片轉換成可查詢的資料——通常是 CSV 或 DataTable。好消息是，Aspose OCR 讓這件事變得非常簡單，只需幾行 C# 程式碼即可完成。

在本教學中，我們將完整示範整個流程：從 **載入圖像以進行 OCR**、**偵測圖像中的表格**，最後 **從圖像中提取表格** 並儲存為 CSV 檔案。完成後，你將擁有一個可直接執行的 Console 應用程式，能夠 **從 PNG**（或任何支援的點陣圖）檔案中 **零困難提取表格**。

## 前置條件

在開始之前，請確保你已具備以下環境：

- .NET 6.0 SDK 或更新版本（此程式碼同樣支援 .NET Framework）
- Visual Studio 2022（或任何你慣用的 IDE）
- Aspose.OCR for .NET 授權檔（可先使用免費試用版）
- 一張包含表格的範例圖像（例如 `invoice_table.png`）

如果上述項目對你來說陌生，別擔心——只要安裝 .NET SDK 並取得 NuGet 套件，即可立即開始。

## 解決方案概觀

高層次的工作流程如下：

1. **載入要處理的圖像**。  
2. **執行 OCR 辨識**，讓引擎知道文字所在位置。  
3. **建立 TableExtractor**，掃描 OCR 結果以找出格狀結構。  
4. **提取所有偵測到的表格**，並挑選需要的那一個。  
5. **將表格儲存為 CSV**（或其他你偏好的格式）。

以下將逐步說明每個步驟，並提供完整可直接複製貼上的程式碼片段。

<img src="table_extraction_example.png" alt="從圖像中提取表格範例" width="600">

*（上圖顯示我們將要提取的範例發票表格）*

## 步驟 1 – 載入圖像以進行 OCR

首先必須告訴 Aspose OCR 要讀取哪個檔案。此函式庫支援 PNG、JPEG、BMP、TIFF 等多種格式。以下為最簡化的程式碼：

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image.FromFile

// ...

// Load the image that contains the table
var ocrEngine = new OcrEngine
{
    Image = Image.FromFile(@"C:\Images\invoice_table.png") // <-- adjust the path
};
```

**為什麼這一步很重要：**  
`Image.FromFile` 會將 PNG（或其他點陣圖）解碼成 OCR 引擎可理解的格式。如果省略此步驟或傳入損毀的檔案，之後的 `Recognize()` 呼叫將拋出例外。

> **小技巧：** 若要處理大型 PDF，請先將每頁轉為圖像——否則 OCR 引擎可能會因記憶體不足而失敗。

## 步驟 2 – 辨識頁面（表格偵測前的必要步驟）

辨識會把原始像素資料轉換成可搜尋的文字版面。沒有這一步，`TableExtractor` 就無法運作。

```csharp
// Perform OCR recognition – this populates internal structures
ocrEngine.Recognize();
```

**底層發生了什麼？**  
Aspose OCR 會使用神經網路文字偵測器，接著建立 `Page`、`Paragraph`、`Word` 物件的層級結構。表格偵測器稍後會檢查這些文字之間的空間關係。

如果你在迴圈中處理大量圖像，建議重複使用同一個 `OcrEngine` 實例，僅更換 `Image` 屬性——這樣可減少記憶體配置開銷。

## 步驟 3 – 建立 TableExtractor 並偵測圖像中的表格

OCR 資料已產生後，我們可以請 Aspose 幫忙找出表格。`TableExtractor` 類別正是為此而設。

```csharp
using Aspose.OCR.Table;

// ...

// Initialize the TableExtractor with the recognized engine
var tableExtractor = new TableExtractor(ocrEngine);

// Extract all tables detected on the page
List<Table> extractedTables = tableExtractor.ExtractAll();
```

**為什麼要使用 `ExtractAll()`？**  
單張圖像可能包含多個表格（例如多段報告）。`ExtractAll()` 會回傳 `List<Table>`，讓你可以遍歷、挑選或甚至合併表格。

如果只需要第一個表格，直接使用 `extractedTables[0]` 即可，但務必先檢查列表是否為空，以避免 `IndexOutOfRangeException`。

```csharp
if (extractedTables.Count == 0)
{
    Console.WriteLine("No tables were detected. Check the image quality or try adjusting OCR settings.");
    return;
}
```

## 步驟 4 – 將提取的表格儲存為 CSV（或其他格式）

Aspose 的匯出功能非常簡單。`Table` 類別內建 `SaveCsv`、`SaveXls`、`SaveJson` 方法。以下示範如何寫入 CSV 檔案：

```csharp
// Save the first detected table to CSV
string outputPath = @"C:\Output\invoice_table.csv";
extractedTables[0].SaveCsv(outputPath);

Console.WriteLine($"Table extraction completed. CSV saved to {outputPath}");
```

**CSV 內容長什麼樣？**  
假設原圖像為 4 × 3 的格子，產生的 CSV 可能如下：

```
Item,Quantity,Price
Widget A,2,19.99
Widget B,5,9.50
Service C,1,150.00
```

你可以在 Excel、Power BI 中開啟此檔，或直接將它匯入資料管線。

## 完整端對端範例

以下是完整、可自行編譯的程式。將它貼到新建的 Console 專案（`dotnet new console`）中執行。別忘了安裝 NuGet 套件 `Aspose.OCR`（`dotnet add package Aspose.OCR`）。

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;          // For Image
using Aspose.OCR;
using Aspose.OCR.Table;

namespace TableExtractTutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the image that contains the table
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                Image = Image.FromFile(@"C:\Images\invoice_table.png")
            };

            // -------------------------------------------------
            // Step 2: Recognize the page (required before table detection)
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 3: Create a TableExtractor and detect tables
            // -------------------------------------------------
            var tableExtractor = new TableExtractor(ocrEngine);
            List<Table> extractedTables = tableExtractor.ExtractAll();

            // Guard against no tables found
            if (extractedTables.Count == 0)
            {
                Console.WriteLine("No tables detected. Verify image quality or OCR settings.");
                return;
            }

            // -------------------------------------------------
            // Step 4: Save the first extracted table as CSV
            // -------------------------------------------------
            string csvPath = @"C:\Output\invoice_table.csv";
            extractedTables[0].SaveCsv(csvPath);

            Console.WriteLine($"Table extraction completed. CSV saved at: {csvPath}");
        }
    }
}
```

### 預期輸出

執行程式後，你應該會看到類似以下的訊息：

```
Table extraction completed. CSV saved at: C:\Output\invoice_table.csv
```

打開 `invoice_table.csv`，即可看到與原圖相同的列與欄。

## 常見問題與特殊情況

### 圖像是 JPEG 而不是 PNG，該怎麼辦？

程式碼完全相同，只要把 `Image.FromFile` 的副檔名改成 JPEG 即可。Aspose OCR 會自動偵測格式，所以 **extract tables from png** 並非硬性需求，任何支援的點陣圖皆可使用。

### 我的表格有合併儲存格，會被保留嗎？

合併儲存格在 CSV 輸出時會被視為獨立的欄位，因為 CSV 本身不支援跨欄合併。若需要保留合併效果（例如 Excel），請改用 `SaveXls`：

```csharp
extractedTables[0].SaveXls(@"C:\Output\invoice_table.xls");
```

### 偵測不到某一欄，如何提升準確度？

- 提高圖像解析度（≥300 dpi 為佳）。  
- 前置處理圖像：轉為灰階、提升對比度或使用去斜角濾鏡。  
- 調整 Aspose OCR 設定，如 `PageSegMode` 或 `Language`（若表格含非拉丁文字）。

### 能直接從 PDF 提取表格嗎？

可以。先將每頁 PDF 轉為圖像（使用 `Aspose.PDF` 或其他 PDF‑to‑image 套件），再套用相同的工作流程。

## 進階生產環境實作建議

1. **將 OCR 包在 try/catch** —— 網路授權環境可能拋出授權例外。  
2. **釋放 `Image` 物件** —— 使用 `using` 區塊以釋放原生資源。  
3. **記錄信心分數** —— `TableExtractor` 會提供 `Table.Confidence`，可用於品質監控。  
4. **批次處理** —— 處理數百張發票時，可平行化 OCR 呼叫，但請遵守授權的執行緒安全規範。

## 後續發展方向

了解 **如何從圖像中提取表格** 後，你可以進一步探索：

- **在影片中偵測表格**（對每一幀使用 Aspose 的 `TableExtractor`）。  
- **從 Web API 載入圖像以進行 OCR**，打造雲端表格提取服務。  
- **從 Azure Blob Storage 中的 PNG 檔案提取表格**，結合 Azure Functions 實作無伺服器處理。

盡情嘗試不同檔案格式、微調 OCR 參數，或直接把 CSV 輸出寫入資料庫。可能性無限。

---

*祝開發順利！若在實作過程中遇到問題或有改進建議，歡迎在下方留言，我們一起解決。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}