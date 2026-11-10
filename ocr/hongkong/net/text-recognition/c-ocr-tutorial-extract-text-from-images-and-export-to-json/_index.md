---
category: general
date: 2026-01-01
description: c# OCR 教學，示範如何提取文字、載入影像進行 OCR，並使用 Aspose.OCR 將 JSON 寫入檔案 – 步驟說明指南.
draft: false
keywords:
- c# OCR tutorial
- how to extract text
- write json to file
- load image for OCR
- OCR image to JSON
language: zh-hant
og_description: c# OCR 教學，逐步說明如何從圖像中提取文字、載入圖像以進行 OCR，並使用 Aspose.OCR 將 JSON 寫入檔案。
og_title: c# OCR 教學 – 提取文字並匯出為 JSON
tags:
- Aspose.OCR
- C#
- Text Extraction
title: c# OCR 教學 – 從圖像提取文字並匯出為 JSON
url: /zh-hant/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教學 – 從圖像提取文字並匯出為 JSON

有沒有想過如何從掃描的發票中提取文字，而不需要花上數小時編寫自訂解析器？你並不孤單。在本 **c# OCR 教學** 中，我們將向你展示如何載入圖像進行 OCR、執行辨識引擎，然後 **將 JSON 寫入檔案**，以便將資料輸入下游系統。

想像你有一個收據資料夾，每個檔案分別命名為 `receipt1.png`、`receipt2.png`，而你需要一個快速的方法將它們轉換為可搜尋的 JSON 記錄。這就是我們要解決的問題，完成後你將擁有一個即時可執行的主控台應用程式，能做到上述功能。除了 Aspose.OCR 之外不需要額外的相依性，也沒有魔法—只有清晰、可重現的步驟。

> **你將學會**
> - 如何使用 Aspose.OCR **載入圖像進行 OCR**。
> - 最佳的 **提取文字** 方法以及取得信心分數。
> - 將 OCR 結果轉換為結構良好的 **OCR 圖像轉 JSON** 負載。
> - 安全地 **將 JSON 寫入檔案** 並驗證輸出。

## 前置條件

- .NET 6 SDK 或更新版本（此程式碼亦可在 .NET Core 上執行）。  
- Visual Studio 2022 或任何你偏好的編輯器。  
- Aspose.OCR NuGet 套件（`Install-Package Aspose.OCR`）。  
- 想要處理的圖像檔案（PNG、JPG、BMP）— 示範中我們使用 `invoice.png`。

如果缺少上述任一項，請從 Microsoft 網站取得 SDK，並透過套件管理員主控台加入 NuGet 套件：

```powershell
Install-Package Aspose.OCR
```

現在基礎已就緒，讓我們深入實作細節。

## 步驟 1：c# OCR 教學 – 初始化 OCR 引擎

在我們能 **載入圖像進行 OCR** 之前，需要先建立一個驅動辨識流程的引擎實例。`OcrEngine` 類別相當輕量，但將其包在 `using` 區塊中是一個好習慣，能即時釋放資源。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine – this is the heart of the c# OCR tutorial
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow…
```

*小技巧：* 若計畫批次處理大量圖像，請重複使用同一個 `OcrEngine` 實例，而非每次都新建。這樣可減少記憶體開銷並提升速度。

## 步驟 2：載入圖像進行 OCR

現在我們真正 **載入圖像進行 OCR**。Aspose.OCR 支援多種格式，你可以指向 PNG、JPEG，甚至是多頁 TIFF。`OcrImage.FromFile` 方法會讀取檔案並為辨識做準備。

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the folder that holds your invoice.png
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);
```

> **為什麼這很重要：** 單獨載入圖像讓你可以檢查其尺寸、DPI，或在送入引擎前先行前處理（例如二值化）。若圖像損毀，`FromFile` 會拋出明確的例外，你可以捕捉並記錄。

## 步驟 3：提取文字 – 執行辨識

手上有圖像後，我們終於可以 **提取文字** 了。`Recognize` 方法會回傳一個 `OcrResult` 物件，內含純文字、每個字的座標資料以及信心分數。

```csharp
        // Step 3: Perform OCR – this is the core of how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);
```

*邊緣情況：* 某些 PDF 包含隱藏的文字層。若將 PDF 頁面渲染成圖像後送入，引擎可能什麼也看不到。此時可先使用 Aspose.PDF 抽取隱藏層，必要時再使用 OCR。

## 步驟 4：OCR 圖像轉 JSON – 轉換結果

`OcrResult` 類別提供便利的 `ToJson()` 輔助方法，將整個結果集合（包括每個字的邊框與信心）序列化為 JSON 字串。這是實現 **OCR 圖像轉 JSON** 而不需自行編寫序列化程式的最簡潔方式。

```csharp
        // Step 4: Convert the OCR result to JSON (includes words, confidence, locations)
        string jsonResult = ocrResult.ToJson();
```

如果你偏好自訂結構，可遍歷 `ocrResult.Words` 並自行組成物件，但在大多數情況下內建的 JSON 已足夠且結構良好。

## 步驟 5：將 JSON 寫入檔案

現在來到最後一步：持久化 JSON 負載。`File.WriteAllText` 方法可確保檔案以原子方式建立（或覆寫）。請確認目標目錄已存在，否則會拋出 `DirectoryNotFoundException`。

```csharp
        // Step 5: Save the JSON output – this demonstrates write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);
```

*提示：* 若需要帶 BOM 的 UTF‑8 或其他編碼，請使用接受 `Encoding` 參數的重載方法。

## 步驟 6：驗證輸出

簡單的 `Console.WriteLine` 可告訴我們流程已成功完成。你也可以在檢視器中開啟 JSON 檔案以確認結構。

```csharp
        // Step 6: Inform the user that the JSON file has been saved
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### 預期的 JSON 片段

```json
{
  "Text": "Invoice #12345\nDate: 2025-12-31\nTotal: $250.00",
  "Words": [
    { "Text": "Invoice", "Confidence": 0.98, "Location": { "X": 10, "Y": 15, "Width": 80, "Height": 20 } },
    { "Text": "#12345", "Confidence": 0.96, "Location": { "X": 95, "Y": 15, "Width": 60, "Height": 20 } }
    // … more words …
  ]
}
```

JSON 包含每個字的位置信息，若之後想在 UI 中高亮顯示文字會很方便。

## 完整範例程式

以下是完整、可直接複製貼上的程式。將 `YOUR_DIRECTORY` 替換為實際存放圖像的路徑。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to recognize
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR – how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 4: Convert the result to JSON (OCR image to JSON)
        string jsonResult = ocrResult.ToJson();

        // Step 5: Write JSON to file – write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);

        // Step 6: Verify
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

執行程式（在專案資料夾中執行 `dotnet run`），你會在原始 PNG 旁看到 `invoice.json`。

## 常見陷阱與避免方法

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **FileNotFoundException** when loading the image | 路徑拼寫錯誤或檔案遺失 | 使用 `Path.Combine` 並在呼叫 `FromFile` 前檢查 `File.Exists`。 |
| **Low confidence scores** | 圖像品質差、DPI 低 | 使用 `ocrImage.AdjustContrast` 前處理，或將圖像升級至 300 DPI。 |
| **JSON file empty** | `ocrResult` 回傳 null（引擎失敗） | 確認圖像格式受支援，且授權（若有）正確套用。 |
| **Performance bottleneck on large batches** | 每次迭代重新建立 `OcrEngine` | 在整個批次中重複使用單一 `OcrEngine` 實例，僅在最後釋放。 |

## 往後步驟

既然你已掌握 **c# OCR 教學**，接下來可能想要：

- **批次處理** 整個資料夾，並將 JSON 檔案彙總至單一資料庫。
- **整合** 輸出至 Azure Cognitive Search，以實現可搜尋的 PDF。
- **新增語言支援**，透過設定 `ocrEngine.Language = OcrLanguage.Spanish`（或任何支援的語言）。
- **後處理** JSON，使用正規表達式抽取表格或鍵值對。

上述每個延伸功能皆建立在我們所討論的核心概念上：載入圖像進行 OCR、提取文字、轉換為 JSON，並將 JSON 寫入磁碟。

### 結論

在本 **c# OCR 教學** 中，我們逐步說明了 **載入圖像進行 OCR**、**提取文字**、將結果轉換為 **OCR 圖像轉 JSON** 負載，最後 **將 JSON 寫入檔案** 的全部流程。完整的程式碼範例可直接嵌入任何 .NET 專案，說明則提供了你在實務情境中調整解決方案所需的背景。

試著使用你自己的收據或發票來執行——調整圖像前處理、嘗試不同語言，觀察 JSON 輸出如何變化。若遇到任何問題，請回顧陷阱表或在下方留言。祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}