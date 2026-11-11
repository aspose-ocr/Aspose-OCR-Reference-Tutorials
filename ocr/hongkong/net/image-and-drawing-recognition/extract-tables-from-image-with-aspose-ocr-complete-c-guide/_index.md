---
category: general
date: 2026-05-31
description: 使用 Aspose OCR 於 C# 從圖像提取表格。了解如何將圖像轉換為表格、啟用表格偵測，並高效輸出結果。
draft: false
keywords:
- extract tables from image
- convert image to table
- OCR table extraction
- Aspose OCR C#
- image to spreadsheet conversion
- table detection in OCR
language: zh-hant
og_description: 使用 Aspose OCR 從圖像中提取表格。本指南說明如何將圖像轉換為表格、啟用表格偵測，以及在 C# 中處理結果。
og_title: 從圖像提取表格 – 步驟式 C# 教程
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  headline: Extract Tables from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  name: Extract Tables from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: Expected Output
    text: 'Assuming the source image contains a 3 × 4 table of invoice line items,
      you might see something like:'
  - name: Low‑Resolution Images
    text: 'When your source picture is under 150 dpi, the table detection algorithm
      may miss cell boundaries. A quick fix is to upscale the image using `System.Drawing`
      before feeding it to Aspose:'
  - name: Skewed Tables
    text: 'If the table is rotated even a few degrees, enable auto‑deskew:'
  - name: Multiple Tables on One Page
    text: Aspose OCR returns each table as a separate object in `result.Tables`. You
      can treat them individually, or merge them into a single DataTable if you need
      a unified view.
  - name: Exporting to Excel
    text: 'Once you have a `DataTable`, exporting to an `.xlsx` file is a breeze with
      `ClosedXML`:'
  type: HowTo
- questions:
  - answer: Yes. Convert each PDF page to an image first (`PdfRenderer` or `Ghostscript`),
      then feed the bitmap to Aspose OCR.
    question: Does this work with PDFs?
  - answer: Absolutely. The `ImageStream.FromFile` method accepts JPEG, PNG, BMP,
      and TIFF out of the box.
    question: Can I extract tables from a JPG?
  - answer: Aspose OCR treats merged cells as separate logical cells; you may need
      to post‑process the output to combine them based on confidence or content patterns.
    question: What if my table has merged cells?
  - answer: Practically, the engine handles tables up to several hundred rows. Performance
      degrades linearly, so consider chunking very large scans.
    question: Is there a limit on table size?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- Data Extraction
title: 使用 Aspose OCR 從圖片中提取表格 – 完整 C# 指南
url: /zh-hant/net/image-and-drawing-recognition/extract-tables-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像提取表格 – 完整 C# 指南

是否曾需要 **從圖像提取表格**，卻不知從何開始？您並不孤單；許多開發人員在嘗試將掃描的發票或收據轉換為可用資料時，都會碰到這個問題。好消息是？使用 Aspose OCR，您只需幾行 C# 程式碼即可 **將圖像轉換為表格**。

在本教學中，我們將示範一個實務範例：載入包含表格的 PNG 圖片，將視覺佈局轉換為結構化的格子，並列印每個儲存格的內容與信心分數。完成後，您將擁有一段可直接放入任何 .NET 專案的完整可執行程式碼片段，並提供處理邊緣案例與擴展解決方案的技巧。

## 您需要的條件

- **.NET 6.0** 或更新版本（程式碼同樣支援 .NET Framework 4.6 以上）
- **Aspose.OCR** NuGet 套件（`Install-Package Aspose.OCR`）
- 一個實際包含表格的影像檔（例如 `invoice_with_table.png`）
- 基本的 C# IDE（Visual Studio、Rider，或安裝 C# 擴充功能的 VS Code）

就這樣—不需要額外的 OCR 引擎，也不需要龐大的相依套件。準備好了嗎？讓我們開始吧。

## 步驟 1：初始化 OCR 引擎以 **從圖像提取表格**

首先，我們建立一個 `OcrEngine` 實例，並指向來源影像。可以將引擎想像成閱讀每個像素並嘗試理解版面的“大腦”。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine with the input image
OcrEngine engine = new OcrEngine
{
    // ImageStream.FromFile loads the image from disk
    Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
};
```

> **為什麼這很重要：** 若未正確初始化引擎，OCR 引擎將無事可分析，您永遠不會從圖片中取得任何表格。`ImageStream.FromFile` 呼叫同時處理常見的格式問題（PNG、JPEG、BMP），因此不需要額外的轉換步驟。

## 步驟 2：啟用表格偵測 – **將圖像轉換為表格** 的關鍵

Aspose OCR 能從影像讀取純文字，但除非告訴它要尋找表格，否則不會自動辨識行與列。這時 `DetectTables` 旗標就派上用場了。

```csharp
// Turn on table detection in the OCR options
engine.Options = new OcrOptions
{
    DetectTables = true   // This activates the table extraction algorithm
};
```

> **專業提示：** 若只需要原始文字，請將 `DetectTables` 保持為 `false`。啟用它會增加少量負擔，但可獲得乾淨、結構化的結果，直接匯入試算表或資料庫。

## 步驟 3：執行 OCR 辨識 – 真相時刻

現在我們請求引擎實際讀取影像。`Recognize` 方法會回傳一個 `OcrResult` 物件，內含純文字以及任何偵測到的表格。

```csharp
// Execute the OCR process
OcrResult result = engine.Recognize();
```

> **底層發生了什麼？** Aspose 會先執行一系列影像前處理步驟（去斜、二值化），再套用其基於神經網路的文字辨識器。若 `DetectTables` 為 true，還會進行版面分析，將字元分組為行與列。

## 步驟 4：遍歷偵測到的表格 – **從圖像提取表格** 實作

如果引擎找到任何表格，它們會出現在 `result.Tables` 中。我們將遍歷每個表格，再遍歷每列與每欄，列印儲存格文字與信心百分比。

```csharp
// Loop over every detected table
foreach (var table in result.Tables)
{
    Console.WriteLine("Table found:");
    for (int r = 0; r < table.Rows; r++)
    {
        for (int c = 0; c < table.Columns; c++)
        {
            var cell = table[r, c];
            // Show cell text and its confidence level
            Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
        }
        Console.WriteLine(); // New line after each row
    }
}
```

> **為什麼要檢查信心值？** OCR 並非完美，特別是低解析度的掃描。`Confidence` 值（0‑100）讓您決定是否直接接受該儲存格，或標記為需人工審核。對於關鍵資料，常見的門檻是 80 %。

### 預期輸出

假設來源影像包含 3 × 4 的發票項目表格，您可能會看到類似以下的輸出：

```
Table found:
Item (conf:96%)   Qty (conf:94%)   Price (conf:97%)   Total (conf:95%)
Pen (conf:99%)    10 (conf:98%)    1.20 (conf:97%)    12.00 (conf:96%)
Notebook (conf:95%) 5 (conf:93%)  3.50 (conf:94%)    17.50 (conf:92%)
...
```

如果未偵測到表格，`result.Tables` 會是空的——不會有任何輸出，但程式仍會正常結束。

## 步驟 5：處理邊緣案例與常見陷阱

### 低解析度影像

當來源圖片低於 150 dpi 時，表格偵測演算法可能會遺漏儲存格邊界。快速解決方法是使用 `System.Drawing` 將影像放大後再交給 Aspose：

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load and upscale
Bitmap bmp = new Bitmap(@"YOUR_DIRECTORY/invoice_with_table.png");
Bitmap resized = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
engine.Image = ImageStream.FromBitmap(resized);
```

### 斜置表格

若表格旋轉了幾度，請啟用自動去斜：

```csharp
engine.Options.Deskew = true; // Turns on automatic deskewing
```

### 單頁多表格

Aspose OCR 會將每個表格作為 `result.Tables` 中的獨立物件回傳。您可以分別處理，或在需要統一檢視時將它們合併為單一 DataTable。

```csharp
// Example: Merge all tables into one DataTable
var merged = new System.Data.DataTable();
foreach (var tbl in result.Tables)
{
    // Simple merge logic – assumes same column count
    // Add rows from each table
    for (int r = 0; r < tbl.Rows; r++)
    {
        var row = merged.NewRow();
        for (int c = 0; c < tbl.Columns; c++)
        {
            row[c] = tbl[r, c].Text;
        }
        merged.Rows.Add(row);
    }
}
```

### 匯出至 Excel

取得 `DataTable` 後，使用 `ClosedXML` 匯出為 `.xlsx` 檔案非常簡單：

```csharp
using ClosedXML.Excel;

var workbook = new XLWorkbook();
var worksheet = workbook.Worksheets.Add(merged, "ExtractedTable");
workbook.SaveAs("ExtractedTable.xlsx");
```

現在您已真正 **將圖像轉換為表格**，並可將試算表交給後續流程使用。

## 完整範例 – 從頭到尾

以下是完整、可直接執行的程式碼，將所有步驟整合在一起。將其貼到新的主控台專案中，替換檔案路徑，然後按 **F5**。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;
using System.Data;
using ClosedXML.Excel;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine with the image
        OcrEngine engine = new OcrEngine
        {
            Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
        };

        // 2️⃣ Enable table detection (key to convert image to table)
        engine.Options = new OcrOptions
        {
            DetectTables = true,
            Deskew = true // Helps with slightly rotated scans
        };

        // 3️⃣ Perform recognition
        OcrResult result = engine.Recognize();

        // 4️⃣ Process each detected table
        DataTable merged = new DataTable();
        bool firstTable = true;

        foreach (var table in result.Tables)
        {
            Console.WriteLine("Table found:");
            for (int r = 0; r < table.Rows; r++)
            {
                // Ensure DataTable has enough columns
                if (firstTable && merged.Columns.Count < table.Columns)
                {
                    for (int i = merged.Columns.Count; i < table.Columns; i++)
                        merged.Columns.Add($"Col{i + 1}");
                }

                DataRow dr = merged.NewRow();
                for (int c = 0; c < table.Columns; c++)
                {
                    var cell = table[r, c];
                    Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
                    dr[c] = cell.Text; // Populate DataTable for Excel export
                }
                Console.WriteLine();
                merged.Rows.Add(dr);
            }
            firstTable = false;
            Console.WriteLine(); // Blank line between tables
        }

        // 5️⃣ Optional: Export merged result to Excel
        if (merged.Rows.Count > 0)
        {
            using var wb = new XLWorkbook();
            wb.Worksheets.Add(merged, "ExtractedTables");
            wb.SaveAs("ExtractedTables.xlsx");
            Console.WriteLine("\nExcel file 'ExtractedTables.xlsx' created successfully.");
        }
        else
        {
            Console.WriteLine("\nNo tables were detected in the image.");
        }
    }
}
```

**流程說明**

1. **引擎設定** – 載入影像並告訴 Aspose 要偵測表格。  
2. **選項調校** – `DetectTables` 承擔主要工作；`Deskew` 提升斜角掃描的準確度。  
3. **辨識** – 回傳純文字以及 `Table` 物件集合。  
4. **遍歷** – 列印每個儲存格的信心值，同時建立 `DataTable` 供之後匯出。  
5. **匯出** – 使用 `ClosedXML`（輕量且不需 interop 的函式庫）寫入 `.xlsx` 檔案——非常適合後續分析或報表。

## 常見問題

- **這能用於 PDF 嗎？**  
  可以。先將每頁 PDF 轉換為影像（使用 `PdfRenderer` 或 `Ghostscript`），再將位圖交給 Aspose OCR。

- **可以從 JPG 提取表格嗎？**  
  當然可以。`ImageStream.FromFile` 方法原生支援 JPEG、PNG、BMP 與 TIFF。

- **如果我的表格有合併儲存格怎麼辦？**  
  Aspose OCR 會將合併儲存格視為獨立的邏輯儲存格；您可能需要根據信心值或內容模式在後處理時將它們合併。

- **表格大小有上限嗎？**  
  實務上，引擎可處理數百列的表格。效能會線性下降，對於非常大的掃描檔，建議分塊處理。

## 總結

我們剛剛示範了如何

## 接下來您可以學習什麼？

- [如何使用 Aspose.OCR for .NET 從圖像提取表格](/ocr/english/net/text-recognition/recognize-table/)
- [從圖像提取文字 – 使用 Aspose.OCR for .NET 進行 OCR 最佳化](/ocr/english/net/ocr-optimization/)
- [透過在 OCR 中準備矩形來提取圖像文字](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}