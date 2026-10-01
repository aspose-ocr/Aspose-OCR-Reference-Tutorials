---
category: general
date: 2026-01-04
description: 學習如何在 C# 中啟用表單並使用 OCR 從圖像中提取表格。此一步一步的教學亦會示範如何執行 OCR 圖像及偵測表格。
draft: false
keywords:
- how to enable forms
- how to extract tables
- run OCR image
- use OCR C#
- detect tables OCR
language: zh-hant
og_description: 逐步指南：如何啟用表單、提取表格、執行 OCR 圖像以及使用 C# 偵測表格 OCR。
og_title: 如何在 C# 中啟用表單並使用 OCR 擷取表格
tags:
- OCR
- C#
- Computer Vision
title: 如何在 C# 中啟用表單並使用 OCR 提取表格 – 完整指南
url: /zh-hant/net/image-and-drawing-recognition/how-to-enable-forms-and-extract-tables-with-ocr-in-c-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中啟用表單與 OCR 抽取表格 – 完整指南

有沒有想過在掃描發票、收據或任何結構化文件時**如何啟用表單**？你並不孤單。在許多實務專案中，最大的阻礙往往是讓 OCR 同時理解表單欄位**以及**表格，而不需要寫上百行的自訂解析程式碼。

在本教學中，我們將一步步示範一個實用的端對端解決方案，說明**如何啟用表單**、**如何抽取表格**，甚至**如何在單一 C# 程式中執行 OCR 影像**處理。完成後，你將擁有一段可直接執行的程式碼，能以 OCR 方式偵測表格、擷取鍵值對，並將結果輸出到主控台。

> **先備條件** – .NET 6+（或 .NET Framework 4.7+）、已參考的 OCR SDK（範例假設有一個通用的 `OcrEngine` 類別），以及一張包含表格或表單的影像檔（`invoice_table.png`）。不需要其他外部函式庫。

![如何在 C# 中使用 OCR 啟用表單](image.png)

## 本教學涵蓋內容

- **啟用表單辨識**，讓「發票號碼」或「日期」等欄位自動被識別。  
- **抽取表格**，取得列/欄數量與儲存格內容。  
- **執行 OCR 影像** 處理，只需一次呼叫即可取得結果，並以程式方式處理。  
- 針對 **detect tables OCR** 的邊緣案例提供技巧，例如合併儲存格或缺少邊框的情況。  

讓我們開始吧。

## 步驟 1：設定 OCR 引擎 – 如何啟用表單

在任何辨識發生之前，你必須先建立 OCR 引擎實例。大多數 SDK 都提供簡單的建構子；我們也會指出之後可以調整的設定選項。

```csharp
using System;
using System.Linq;

// Assume the OCR SDK namespace is OcrSdk
using OcrSdk;

public class OcrDemo
{
    public static void Main()
    {
        // Create the OCR engine – this is where “how to enable forms” starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that contains a table or form.
        // Replace the path with the actual location of your PNG/JPEG/TIFF file.
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");
```

**為什麼重要：** 建立引擎會分配內部資源（例如語言模型）。若省略此步驟，之後的 `Recognize` 呼叫會拋出 `NullReferenceException`。

## 步驟 2：開啟結構化抽取 – 如何抽取表格 & detect tables OCR

現在我們啟用兩個核心功能：表格辨識與表單欄位抽取。現代 OCR 引擎通常提供布林旗標或更細緻的 `Config` 物件。

```csharp
        // Enable structured extraction features.
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms
```

**專業提示：** 若只需要其中一項功能，關閉另一項可提升最高 20 % 的效能。

## 步驟 3：執行 OCR 影像並取得結果 – run OCR image

引擎設定完成後，只要一次方法呼叫即可完成繁重工作。回傳的 `OcrResult` 包含表格與表單欄位的集合。

```csharp
        // Run OCR – this is the “run OCR image” step.
        OcrResult ocrResult = ocrEngine.Recognize();

        // -----------------------------------------------------------------
        // Step 4: Process Detected Tables – how to extract tables
        // -----------------------------------------------------------------
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");

            // Show the first row for a quick sanity check.
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // -----------------------------------------------------------------
        // Step 5: Process Detected Form Fields – how to enable forms
        // -----------------------------------------------------------------
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

### 預期的主控台輸出

```
Table 1: 5 rows, 4 columns
Item | Qty | Price | Total
InvoiceNumber: INV-2025-001
Date: 2025-12-31
Customer: Acme Corp.
```

具體數字會依你的來源影像而異，但你應該會看到每個表格的摘要列，接著是第一列的儲存格值，最後列出表單欄位的鍵值對。

## 步驟 4：處理 Detect Tables OCR 的邊緣案例

即使 `EnableTableRecognition = true`，OCR 仍可能在以下情況卡住：

| 問題 | 為何會發生 | 快速解決方案 |
|------|------------|--------------|
| **合併儲存格** | 引擎將合併區域視為單一儲存格。 | 後處理列時：偵測異常寬的儲存格，並依空白字元切割。 |
| **缺少邊框** | 表格線條太淡或斷裂。 | 在送入引擎前提升影像對比度（`ocrEngine.PreprocessImage`）。 |
| **表格旋轉** | 文件掃描時有角度。 | 使用 `ocrEngine.Config.AutoRotate = true`（若支援）。 |

**小技巧：** 在存取索引前，務必先驗證 `table.Rows.Count` 與 `table.Columns.Count`，以避免 `IndexOutOfRangeException`。

## 步驟 5：完整整合 – 可執行範例

以下是完整程式碼，你可以直接貼到新的 Console 專案中。內容包括 `using` 指示、引擎設定以及前述的處理邏輯。

```csharp
using System;
using System.Linq;
using OcrSdk;   // Replace with your actual OCR SDK namespace

public class OcrDemo
{
    public static void Main()
    {
        // 1️⃣ Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the target image
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");

        // 3️⃣ Enable structured extraction (forms + tables)
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms

        // 4️⃣ Run OCR – “run OCR image”
        OcrResult ocrResult = ocrEngine.Recognize();

        // 5️⃣ Process tables – “how to extract tables”
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // 6️⃣ Process form fields – “how to enable forms”
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

執行程式（`dotnet run` 或在 Visual Studio 按 `Ctrl+F5`），即可看到前面說明的主控台輸出。

## 常見問題 (FAQ)

**Q: 這能處理 PDF 輸入嗎？**  
A: 大多數 OCR SDK 會在內部將 PDF 每頁光柵化。只要改呼叫 `ocrEngine.LoadPdf("file.pdf")` 取代 `LoadImage` 即可。

**Q: 若影像同時包含表格*與*簽名該怎麼辦？**  
A: 簽名會被視為獨立的影像區塊。你可以檢查 `ocrResult.Images`，針對信心度低的文字區域予以忽略。

**Q: 能把表格匯出成 CSV 嗎？**  
A: 當然可以。遍歷 `table.Rows` 時，將每個 `cell.Text` 用逗號連接寫入 `StringBuilder`，最後存成 `.csv` 檔案。

## 結論

現在你已掌握**如何啟用表單**、**如何抽取表格**，以及使用 C# **run OCR image** 處理的完整步驟。此範例示範了從建立引擎、設定、到結果處理的全流程，讓你能直接把程式碼搬入自己的專案。

接下來，試著把範例影像換成多頁發票 PDF，實驗 `ocrEngine.Config.AutoRotate`，或將抽取的資料寫入資料庫。這些延伸練習將深化你對 **detect tables OCR** 與 **use OCR C#** 在實務環境中的運用。

若遇到任何問題，歡迎在下方留言。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}