---
category: general
date: 2026-03-26
description: 使用 Aspose OCR 於 C# 識別 PNG 圖片中的文字並提取收據資料。將圖像轉換為 JSON‑L，並在完整範例中以 OCR 處理收據。
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中辨識 PNG 文字，將收據轉換為 JSON‑L。完整逐步程式碼與技巧。
og_title: 從 PNG 識別文字 – Aspose OCR C# 指南
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: 從 PNG 識別文字 – Aspose OCR C# JSON‑L 教程
url: /zh-hant/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 png 識別文字 – 完整 Aspose OCR C# 指南

有沒有曾經需要 **從 png 識別文字** 檔案，但不確定哪個函式庫能提供乾淨、逐行的結果？你並不孤單。在許多小型企業應用程式中，收據以 PNG 圖片形式存在，提取金額、日期或商家名稱是每日的痛點。

好消息是？只要幾行 C# 程式碼加上 **Aspose OCR** 函式庫，你就能 **從收據中擷取文字**，再 **將影像轉換為 jsonl** 供下游分析使用。在本教學中，我們將一步步走過完整流程——載入 PNG、執行 OCR，並將每一行寫入 JSON‑L 檔案——讓你可以立即 **使用 OCR 處理收據**。

我們會涵蓋所有必備項目：需要的 NuGet 套件、完整可執行的程式、每一步驟的重要說明，以及在收據雜亂時你會感激的實用小技巧。無需額外文件，只要複製、執行、再依需求調整即可。

---

## 你將學會

- 如何使用 `Aspose.OCR` **從 png 識別文字**。
- 如何 **從收據中擷取文字** 的行物件並取得信心分數。
- 如何 **將影像轉換為 jsonl**，使每一行 OCR 結果成為獨立的 JSON 物件。
- 如何 **使用 OCR 端對端處理收據**，包括空白影像或低信心行的例外處理。
- 常見 OCR 問題的除錯技巧與提升準確度的方法。

### 前置條件

- .NET 6.0 或更新版本（此程式碼同樣支援 .NET Core 與 .NET Framework）。
- Visual Studio 2022 或任意你慣用的 IDE。
- 有效的 Aspose OCR 授權（可從 Aspose.com 取得免費暫時授權）。
- 一張存於你可控制資料夾中的範例收據 `receipt.png`。

---

## 步驟 1：使用 Aspose OCR **從 png 識別文字**

首先，我們需要一個已初始化的 `OcrEngine`。此物件負責 OCR 引擎的設定（語言、偵測模式等）。預設使用英文並自動偵測頁面版面，對大多數收據皆能正常運作。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**為什麼這很重要：**  
`OcrEngine` 是執行大量運算的核心元件；只建立一次並在多張影像間重複使用，可減少記憶體開銷。若需其他語言（例如西班牙文收據），可在呼叫 `Recognize` 前設定 `ocrEngine.Language = OcrLanguage.Spanish;`。

---

## 步驟 2：**從收據行擷取文字**

`OcrResult` 內含名為 `Lines` 的集合。每一行都保存原始文字與信心分數（0‑100）。將它們取出即可細部控制——可以捨棄低信心行，或標記為需人工審核。

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**為什麼要轉義 JSON：**  
收據文字可能包含雙引號 (`"`) 或反斜線 (`\`) ，若直接寫入會破壞 JSON 結構。`EscapeJson` 方法確保每行都是有效的 JSON。

**輸出範例：**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

每一行都是獨立記錄，非常適合串流至資料湖或餵入機器學習模型。

---

## 步驟 3：**將影像轉換為 JSONL** – 處理例外情況

當批次處理收據時，可能會遇到空白、損毀或信心極低的影像。讓我們把流程寫得更健全。

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**為什麼要過濾：**  
印在淡紙上的收據常會產生低信心的雜訊字元。將信心低於 80 % 的行過濾掉，通常能去除噪音，同時保留有用資料。

---

## 步驟 4：**使用 OCR 端對端處理收據** 範例

把所有步驟整合起來，以下是 **完整、可直接執行** 的程式。將 `YOUR_DIRECTORY` 替換為放置 PNG 檔案的資料夾路徑。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**執行方式：**  
1. 在專案資料夾開啟終端機。  
2. `dotnet add package Aspose.OCR` – 安裝函式庫。  
3. `dotnet run` – 你應該會看到成功訊息，並產生 `receipt.jsonl` 檔案。

**預期結果：** 每行為一筆 JSON，對應收據中的每一行，並附帶信心分數。現在你可以將此檔案匯入 Power BI、Elastic，或任何支援 JSON‑L 的分析工具。

---

## 常見問題與專業小技巧

| 問題 | 為什麼會發生 | 快速解決方案 |
|------|--------------|--------------|
| **輸出為空白** | 影像路徑錯誤或檔案不是 PNG。 | 再次確認路徑，使用 `File.Exists(imagePath)` 檢查。 |
| **出現雜訊字元** | DPI 太低或 PNG 壓縮過度。 | 使用至少 300 dpi 掃描；避免過度的 JPEG 壓縮。 |
| **低信心行過多** | 收據印在熱感紙上且已退色。 | 提高 `minConfidence` 閾值，或在前置處理時調整對比度/閾值。 |
| **JSON 解析錯誤** | 收據文字中有未轉義的引號。 | 保留 `EscapeJson` 輔助函式，或改用 `System.Text.Json` 進行序列化。 |

**專業技巧：** 若需抽取特定欄位（例如總金額），可在取得 JSON‑L 後對每個 `line.Text` 執行簡單正規表達式。這樣可將 OCR 與業務邏輯分離，除錯也更容易。

---

## 延伸應用

- **批次處理：** 將 `Main` 內的邏輯包在 `foreach`，遍歷資料夾內所有 PNG 檔案。
- **多語言支援：** 在 `Recognize` 前設定 `ocrEngine.Language = OcrLanguage.Spanish;`（或其他支援語言）。
- **結構化輸出：** 除了逐行 JSON，亦可建立 `Receipt` 物件，包含 `Date`、`Merchant`、`Total` 等屬性，最後一次序列化。

以上變化仍以 **將影像轉換為 jsonl** 為核心，讓你在不改動 OCR 部分的情況下，輕鬆切換下游消費者。

---

## 結論

我們已示範如何使用 Aspose OCR **從 png 識別文字**、**從收據中擷取文字**，以及 **將影像轉換為 jsonl**，以便進行後續處理。完整、獨立的 C# 程式展示了從載入 PNG、處理例外情況，到寫入乾淨 JSON‑L 檔案的全流程，讓你能立即在專案中 **使用 OCR 處理收據**。

試著用幾張範例收據跑一遍，調整信心門檻，你會發現雜亂的影像堆疊很快就能變成可供分析的結構化資料。熟練後，可探索批次處理或加入小型機器學習模型，自動分類費用類別。

有任何問題或發現妙招嗎？歡迎在下方留言——祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}