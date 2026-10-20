---
category: general
date: 2026-04-04
description: 學習如何使用 C# 的 OCR 引擎範例從 TIFF 檔案中提取文字。一步一步的指南，提供 JSON 與 XML 輸出。
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: zh-hant
og_description: 使用 OCR 引擎在 C# 中提取 TIFF 檔案文字的範例。詳細步驟、完整程式碼，以及 JSON/XML 輸出的技巧。
og_title: 使用 Aspose OCR 引擎從 TIFF 提取文字 – 完整指南
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 使用 Aspose OCR 引擎從 TIFF 擷取文字 – 完整範例
url: /zh-hant/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 TIFF 提取文字 – 完整 OCR 引擎範例（C#）

是否曾需要 **從 TIFF 提取文字** 圖片，但不確定哪個函式庫能在不需要繁雜變通的情況下處理多頁檔案？你並非唯一有此需求的人。在許多舊有系統中，文件以多頁 TIFF 掃描檔的形式出現，而提取原始文字是搜尋、合規或資料輸入自動化的必備功能。

好消息是？使用 Aspose OCR，你只需幾行程式碼即可完成——不必與低階像素緩衝區糾纏。本教學將帶你完成一個 **完整的 OCR 引擎範例**，載入多頁 TIFF、辨識每一頁，並輸出格式化的 JSON 以及可選的 XML。完成後，你將擁有一個可直接執行的 C# 主控台應用程式，能在數秒內從 TIFF 檔案中提取文字。

## 你將學到

- 如何在 .NET 專案中設定 Aspose OCR 引擎。  
- 提取 **從 TIFF 提取文字** 檔案的完整程式碼，包括多頁處理。  
- 為何你可能需要 JSON 而非 XML 輸出，以及如何同時產生兩者。  
- 排除常見問題的技巧（例如影像 DPI、記憶體使用）。  

### 前置條件

- .NET 6.0 SDK 或更新版本（程式碼相容於 .NET Core 與 .NET Framework）。  
- 有效的 Aspose OCR 授權（或免費試用金鑰）。  
- Visual Studio 2022 或任何你偏好的 C# 編輯器。  
- 一個範例多頁 TIFF 檔案（範例中命名為 `multi-page.tiff`）。  

> **專業提示：** 若預算有限，免費試用仍允許你每月提取最多 100 頁文字——非常適合測試。

---

## 第一步 – 初始化 OCR 引擎（ocr engine example）

在我們能 **從 TIFF 提取文字** 之前，需要先建立 OCR 引擎的實例。此物件保存了所有日後可能調整的設定（語言、解析度等）。

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*為何這很重要：* `OcrEngine` 類別抽象化了繁重的工作。只建立一次實例並在多張影像間重複使用，比每頁都新建引擎更省記憶體。

---

## 第二步 – 載入多頁 TIFF（extract text from TIFF）

現在我們將引擎指向來源檔案。`ImageStream.FromFile` 支援 TIFF、JPEG、PNG 等多種格式，但本教學聚焦於 TIFF。

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **注意：** 請將 `YOUR_DIRECTORY` 替換為你機器上的實際資料夾路徑。  
> **提示：** 若你的 TIFF DPI 較低（低於 150），建議先行前處理以提升 OCR 準確度。

---

## 第三步 – 辨識所有頁面

呼叫 `Recognize()` 會對 TIFF 中的 **每一頁** 執行 OCR 演算法。結果物件包含原始文字、信心分數以及逐頁的分割資訊。

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*你會得到什麼：* `ocrResult` 包含一系列 `PageResult` 物件。每頁的文字可透過 `ocrResult.Pages[i].Text` 取得。引擎同時提供信心等級，可用於品質檢查。

---

## 第四步 – 以 JSON（及可選 XML）儲存結果

大多數現代工作流程偏好 JSON，但舊有系統仍使用 XML。以下示範如何產生兩者，且格式化美觀。

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### 範例 JSON 輸出（截斷）

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

JSON 為人類可讀格式，讓除錯變得輕鬆。若需要，XML 會呈現相同的結構。

---

## 第五步 – 驗證提取結果（extract text from TIFF）

檔案寫入後，快速的合理性檢查可確保沒有出錯。

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

若看到印出的片段，表示你已成功 **從 TIFF 提取文字** 並將其保存。接下來，你可以將 JSON 輸入搜尋索引、資料庫或任何下游服務。

---

## 為何使用 Aspose OCR 來提取 TIFF 文字？

- **即時支援多頁** – 無需手動拆分 TIFF。  
- **高準確度**，得益於專有的神經網路模型。  
- **跨平台** – 可於 Windows、Linux 與 macOS .NET 執行環境運行。  
- **豐富的輸出格式**（JSON、XML、純文字），適用於現代與舊有系統。  

如果你仍在猶豫，請在範例文件上試用免費版。你會發現相較於常需額外影像前處理的開源方案，速度與簡易度都有明顯優勢。

---

## 常見問題與避免方法

| 問題 | 徵兆 | 解決方式 |
|------|------|----------|
| 低解析度 TIFF | 缺字，信心分數低 | 在 OCR 前將影像升級至 ≥150 DPI（`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)`） |
| 語言設定錯誤 | 文字亂碼，特別是非英文文本 | 在 `Recognize()` 前設定 `ocrEngine.Language = Language.Spanish`（或相應語言） |
| 大型檔案記憶體不足 | `OutOfMemoryException` | 分批處理頁面：遍歷 `ocrEngine.Image.Pages` 並呼叫 `RecognizePage(i)` |
| 未套用授權 | 輸出中出現 “Evaluation” 水印 | 註冊授權：`License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## 完整可執行範例（可直接複製貼上）

以下是完整程式碼，可直接放入新的主控台專案。它包含了我們討論的所有部分——初始化、載入、辨識與儲存。

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

將檔案另存為 `Program.cs`，執行 `dotnet run`，即可在主控台看到 JSON 與 XML 的儲存位置。就這樣——你已完成一個 **ocr engine example**，能從 TIFF 提取文字。

---

## 後續步驟與相關主題

- **批次處理：** 將上述邏輯包在 `foreach` 迴圈中，以自動處理數十個 TIFF 檔案。  
- **搜尋整合：** 將 JSON 推送至 Elasticsearch 或 Azure Cognitive Search，實現掃描文件的全文搜尋。  
- **影像前處理：** 探索 Aspose 的 `ImageProcessing` API，於 OCR 前進行去斜、去雜訊或調整對比度。  
- **其他輸出：** 若只需純文字而無中繼資料，可使用 `ocrResult.ToPlainText()`。  

如果你對其他影像格式感興趣，同樣的流程也適用於 PDF（只需更換來源檔案）或 PNG。關鍵在於，一旦引擎設定完成，之後的流程即可重複使用。

---

## 結論

我們已完整示範一個 **完整的 OCR 引擎範例**，讓你使用 Aspose OCR **從 TIFF 檔案提取文字**，並輸出整潔的 JSON 以及可選的 XML，供任何下游工作流程使用。程式碼自成一體，說明亦涵蓋每一步的「為何」原因。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}