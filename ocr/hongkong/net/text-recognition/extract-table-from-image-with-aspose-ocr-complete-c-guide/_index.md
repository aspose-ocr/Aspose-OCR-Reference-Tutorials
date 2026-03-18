---
category: general
date: 2026-03-18
description: 使用 Aspose OCR 在 C# 中從圖像提取表格。學習如何將表格轉換為 JSON、取得表格 JSON，並在數分鐘內從圖像中擷取文字。
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: zh-hant
og_description: 使用 Aspose OCR 於 C# 從圖像提取表格。學習將表格轉換為 JSON、取得表格 JSON，並快速從圖像中提取文字。
og_title: 使用 Aspose OCR 從圖像提取表格 – 完整 C# 指南
tags:
- Aspose OCR
- C#
- Table Extraction
title: 使用 Aspose OCR 從圖像提取表格 – 完整 C# 教學
url: /zh-hant/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像提取表格 – 完整 C# 指南

是否曾需要 **extract table from image**，卻不確定哪個函式庫能在不需要大量手動解析的情況下完成？你並不孤單。在許多發票處理或收據掃描專案中，真正的痛點是將雜訊較多的點陣圖轉換成下游系統可使用的結構化表格。  

好消息是？使用 Aspose OCR，你只需幾行程式碼即可 **convert table to JSON**，同時還能取得整張圖像的純文字，因此 **extract text from image** 成為額外收穫。在本教學中，我們將逐步說明完整流程——從載入圖像到取得偵測到的表格的整齊 JSON 表示。

> **快速收穫：** 完成後，你將擁有一個可執行的 C# 主控台應用程式，會同時印出原始 OCR 文字與可直接寫入資料庫或 API 的 JSON 字串。

## 前置條件

- .NET 6.0 SDK（或任何較新的 .NET 版本）已安裝。  
- 有效的 Aspose OCR 授權或免費試用版（函式庫在未授權時仍可使用，但會加上浮水印）。  
- 一張實際包含表格的圖像，例如 `invoice_table.png`。  
- Visual Studio 2022、VS Code，或任何你喜歡的編輯器。

除了 `Aspose.OCR` 之外，無需其他 NuGet 套件。

## 第一步：設定專案並安裝 Aspose  OCR

首先，建立一個新的主控台專案，並加入 OCR 函式庫。

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **專業提示：** 若使用公司代理伺服器，請加入 `--no-restore` 參數，之後再以正確的環境變數執行 `dotnet restore`。

## 第二步：初始化 OCR 引擎並啟用表格辨識

此解決方案的核心是 `OcrEngine`。透過切換 `EnableTableRecognition`，我們告訴 Aspose  OCR 去尋找類似格線的結構，而不是將所有內容視為純文字。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;

class TableJsonDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable table detection – this is what lets us get a JSON table later
        ocrEngine.Settings.EnableTableRecognition = true;
```

為什麼這一步至關重要？若未啟用表格辨識，引擎會將圖像展平成單一字串，導致之後無法重建行與列。啟用後會加入輕量的版面分析階段，幾乎不影響效能，卻能帶來巨大的下游效益。

## 第三步：載入圖像並執行辨識

現在我們將引擎指向包含表格的檔案。`ImageStream.FromFile` 支援大多數常見格式（PNG、JPEG、TIFF）。

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

若圖像過大，建議先調整大小以加快處理速度。Aspose  OCR 會自動偵測 DPI，但 300 DPI 的掃描對大多數表格而言是最佳選擇。

## 第四步：提取純文字 – “extract text from image”

即使我們的主要目標是表格，仍常需要原始文字作為記錄或備援處理。

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

`Text` 屬性會將引擎辨識到的所有內容串接起來，保留換行。當你需要驗證 OCR 是否正確讀取表格區域外的標題或頁腳時，這非常方便。

## 第五步：取得偵測到的表格 JSON – “convert table to json” & “get table json”

這裡就是魔法發生的地方。`GetTableAsJson()` 會將偵測到的行、列與儲存格內容序列化為整潔的 JSON 字串。

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

產生的 JSON 會類似以下（為了易讀而格式化）：

```json
{
  "Rows": [
    {
      "Cells": [
        { "Text": "Item", "ColumnIndex": 0 },
        { "Text": "Quantity", "ColumnIndex": 1 },
        { "Text": "Price", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget A", "ColumnIndex": 0 },
        { "Text": "10", "ColumnIndex": 1 },
        { "Text": "$5.00", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget B", "ColumnIndex": 0 },
        { "Text": "7", "ColumnIndex": 1 },
        { "Text": "$8.50", "ColumnIndex": 2 }
      ]
    }
  ]
}
```

為什麼 JSON 是首選格式？它與語言無關、易於反序列化為物件，且非常適合現代 Web API。若需要 CSV，只要遍歷行並以逗號串接儲存格文字即可。

## 第六步：（可選）將 JSON 轉換為 .NET 物件 – “convert image to json”

如果你偏好使用強型別，請使用 `System.Text.Json` 反序列化 JSON。

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

你需要定義 `TableModel`、`RowModel` 與 `CellModel` 以符合 JSON 結構。此步驟示範如何從 **convert image to json** 直接得到具型別的物件，讓下游驗證變得輕鬆。

## 完整範例程式

將所有步驟整合起來，以下是完整、可直接執行的程式。請將其儲存為 `Program.cs`，放在先前建立的專案資料夾內。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;
using System.Text.Json;

class TableJsonDemo
{
    static void Main()
    {
        // Step 1: Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable table recognition
        ocrEngine.Settings.EnableTableRecognition = true;

        // Step 3: Load image containing a table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Step 4: Run OCR
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Print full text (extract text from image)
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);

        // Step 6: Get table as JSON (convert table to json, get table json)
        string tableJson = ocrResult.GetTableAsJson();
        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);

        // Optional: Deserialize JSON to C# objects (convert image to json)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
    }
}

// Helper classes matching Aspose's JSON structure
public class TableModel
{
    public RowModel[] Rows { get; set; }
}
public class RowModel
{
    public CellModel[] Cells { get; set; }
}
public class CellModel
{
    public string Text { get; set; }
    public int ColumnIndex { get; set; }
}
```

### 預期輸出

執行 `dotnet run` 後，應會看到類似以下的輸出：

```
Full text:
Item Quantity Price
Widget A 10 $5.00
Widget B 7 $8.50

Detected table (JSON):
{
  "Rows":[
    {"Cells":[{"Text":"Item","ColumnIndex":0},{"Text":"Quantity","ColumnIndex":1},{"Text":"Price","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget A","ColumnIndex":0},{"Text":"10","ColumnIndex":1},{"Text":"$5.00","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget B","ColumnIndex":0},{"Text":"7","ColumnIndex":1},{"Text":"$8.50","ColumnIndex":2}]}
  ]
}

First cell value: Item
```

若輸出為空，請再次確認 `EnableTableRecognition` 已設為 `true`，且圖像確實包含清晰的格線。

## 常見陷阱與避免方法

| 問題 | 發生原因 | 解決方法 |
|------|----------|----------|
| **未返回 JSON** | 表格偵測未啟用或圖像對比度過低。 | 確保 `ocrEngine.Settings.EnableTableRecognition = true`，並提升圖像品質（增加對比度、二值化）。 |
| **行列不完整** | OCR 被合併儲存格或旋轉文字搞混。 | 預先處理圖像：去除傾斜（`ImageProcessor.Rotate`）或手動分割合併儲存格。 |
| **Unicode 雜訊** | 字型未被辨識（例如手寫）。 | 透過 `ocrEngine.Language = Language.English;` 切換語言套件，或改用其他 OCR 引擎處理手寫文字。 |
| **效能下降** | 圖像過大（>5 MP）。 | 將寬度縮減至約 1500 px，同時保留 DPI。 |

## 往後步驟：深入進階

現在你已能 **extract table from image** 並 **convert table to JSON**，可以考慮以下延伸應用：

- **將 JSON 持久化** 到資料庫，使用 Entity Framework。  
- **後處理** JSON 以正規化貨幣格式（例如去除 `$`）。  
- **批次處理** 資料夾內的發票，使用 `Directory.GetFiles` 並以 `Parallel.ForEach` 平行化。  
- **整合** Azure Functions 或 AWS Lambda，打造無伺服器 OCR 流程。

上述每個主題自然會涉及其他次要關鍵字，例如 **convert image to json**（將完整 OCR 結果傳送至雲端端點）以及 **get table json** 用於下游分析。

---

### 結論

我們剛剛示範了如何使用 Aspose OCR **extract table from image**，將表格轉換為乾淨的 JSON，甚至反序列化為 C# 物件。相同的模式

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}