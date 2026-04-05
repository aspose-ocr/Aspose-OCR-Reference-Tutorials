---
category: general
date: 2026-04-04
description: 如何在 C# 中使用 Aspose.OCR 進行批量 OCR。學習從圖像提取文字、匯出 CSV 摘要，並高效處理大量圖像 OCR。
draft: false
keywords:
- how to batch ocr
- extract text images
- how to export csv
- bulk image ocr
- batch ocr images
language: zh-hant
og_description: 如何在 C# 中使用 Aspose.OCR 進行批次 OCR。獲取從圖像提取文字並匯出 CSV 摘要的完整解決方案。
og_title: 如何在 C# 中批量 OCR – 完整逐步教學
tags:
- OCR
- C#
- Aspose
- Automation
title: 如何在 C# 中批次執行 OCR – 大量圖像文字提取完整指南
url: /zh-hant/net/text-recognition/how-to-batch-ocr-in-c-complete-guide-for-bulk-image-text-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何批量 OCR – 完整功能的 C# 教程

有沒有想過 **如何批量 OCR** 整個資料夾的圖片，而不必為每個檔案寫一個單獨的程式？你並不是唯一有此需求的人。在許多實務專案中——例如發票處理、掃描書籍的歸檔，或大量數位化收據——開發者需要一種快速且可靠的方式，從數十甚至數千張影像中擷取文字。

在本指南中，我們將一步步示範一個完整、可直接執行的範例，說明 **如何批量 OCR**、**擷取文字影像**，以及使用 Aspose.OCR **匯出 CSV 摘要**。完成後，你將擁有一個單一的 C# 程式，能夠處理任意目錄的圖片，將其轉換為可搜尋的文字檔，並產生整潔的 CSV 報告。沒有神祕，只要清晰的程式碼與實用技巧。

## 你將學會什麼

- 設定 Aspose.OCR 引擎以使用英文（或任何支援的語言）。  
- 一次處理整個影像資料夾——非常適合大量影像 OCR。  
- 將每個 OCR 結果儲存為 `.txt` 檔，同時可選擇產生 CSV 檔，列出每張來源影像及其擷取文字的長度。  
- 處理常見的例外情況，例如不支援的檔案類型、空資料夾以及 Unicode 字元。  

**先決條件** – 需要 .NET 6+（或 .NET Framework 4.7.2+）、Visual Studio 2022 或任意你慣用的 IDE，並且擁有有效的 Aspose.OCR 授權（免費試用版可用於示範）。不需要其他第三方函式庫。

![批量 OCR 圖示](https://example.com/ocr-flow.png "批量 OCR 流程圖")

## 步驟 1：安裝 Aspose.OCR 並建立新的 Console 專案

首先，將 Aspose.OCR NuGet 套件加入你的專案：

```bash
dotnet add package Aspose.OCR
```

> **小技巧：** 若使用 Visual Studio，你也可以右鍵點擊專案 → *Manage NuGet Packages* → 搜尋 *Aspose.OCR* → 安裝。

建立一個全新的 Console 應用程式 (`dotnet new console -n BulkOcrDemo`) 並開啟 `Program.cs`。這裡將是所有程式碼的入口。

## 步驟 2：初始化 OCR 引擎 – 選擇正確的語言

OCR 引擎必須知道要辨識哪種語言。英文是最常見的，但你可以透過更改 `Language.English` 來改成西班牙文、法文等其他語言。

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

// Step 2: Set up the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // You can switch to Language.Spanish, Language.French, etc.
    Language = Language.English
};
```

**為什麼這很重要：** 指定語言可提升辨識準確度，因為引擎會套用語言特定的字典與字元集。若省略此設定，將使用通用模型，可能會誤判字元。

## 步驟 3：定義來源、輸出與可選的 CSV 路徑

我們需要三個資料夾：

| 路徑 | 用途 |
|------|---------|
| `sourceFolder` | 原始圖片所在的位置。 |
| `outputFolder` | 每個 OCR 結果 (`.txt`) 將被儲存的地方。 |
| `csvSummaryPath` |（可選）記錄每張圖片名稱與擷取文字長度的 CSV 檔案。 |

```csharp
// Step 3: Folder locations – update these to match your environment
string sourceFolder = @"C:\OcrDemo\Images\Bulk";
string outputFolder = @"C:\OcrDemo\Output\BulkResults";
string csvSummaryPath = Path.Combine(outputFolder, "summary.csv"); // optional
```

> **提示：** 使用 `Path.Combine` 可確保跨平台相容性，會自動插入正確的目錄分隔符。

## 步驟 4：執行批次處理器

Aspose.OCR 內建一個方便的 `BatchProcessor`，負責繁重的工作。它會遍歷所有支援的影像 (`.png`, `.jpg`, `.tif` 等)，執行 OCR，並寫入結果。

```csharp
// Step 4: Process the entire folder
BatchProcessor.ProcessFolder(
    sourceFolder: sourceFolder,
    outputFolder: outputFolder,
    engine: ocrEngine,
    csvSummaryPath: csvSummaryPath);
```

### 背後發生了什麼？

1. **檔案搜尋** – 處理器掃描 `sourceFolder` 內的影像檔。  
2. **OCR 執行** – 每張影像都會送入 `ocrEngine`。  
3. **文字儲存** – 辨識出的文字會以相同檔名的 `.txt` 檔寫入 `outputFolder`。  
4. **CSV 記錄** – 若提供 `csvSummaryPath`，處理器會追加一行：`ImageName,CharactersExtracted,ProcessingTimeMs`。

## 步驟 5：加入錯誤處理與例外支援

一個穩健的批次工作必須能容忍遺失檔案、不支援的格式以及空目錄。將處理呼叫包在 `try/catch` 區塊中，並先行驗證輸入。

```csharp
try
{
    // Validate folders
    if (!Directory.Exists(sourceFolder))
        throw new DirectoryNotFoundException($"Source folder not found: {sourceFolder}");

    Directory.CreateDirectory(outputFolder); // ensures output exists

    // Optional: clean previous CSV
    if (File.Exists(csvSummaryPath))
        File.Delete(csvSummaryPath);

    // Run the batch
    BatchProcessor.ProcessFolder(
        sourceFolder: sourceFolder,
        outputFolder: outputFolder,
        engine: ocrEngine,
        csvSummaryPath: csvSummaryPath);

    Console.WriteLine("✅ Batch OCR completed successfully!");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ An error occurred: {ex.Message}");
}
```

**為什麼要這樣做？** 若未進行驗證，程式可能會悄悄失敗，留下空的輸出資料夾卻不知原因。明確的訊息能讓除錯變得輕鬆。

## 步驟 6：驗證結果 – 會看到什麼

執行完畢後，開啟 `outputFolder`。你應該會看到每張影像對應的 `.txt` 檔案：

```
C:\OcrDemo\Output\BulkResults\invoice_001.txt
C:\OcrDemo\Output\BulkResults\receipt_2023-03-15.txt
...
```

每個檔案都包含原始的 OCR 輸出——純文字，可直接供搜尋索引、資料庫或進一步的 NLP 流程使用。

如果你提供了 `csvSummaryPath`，開啟 `summary.csv`，內容大致如下：

```
ImageName,CharactersExtracted,ProcessingTimeMs
invoice_001.png,1245,312
receipt_2023-03-15.jpg,378,98
...
```

CSV 讓產生報表、發現異常短的結果（可能是掃描失敗）或將指標輸入監控儀表板變得非常簡單。

## 步驟 7：擴充解決方案 – 常見變化

### 7.1 變更輸出格式

如果不想只輸出純 `.txt`，也可以改成 PDF 或 JSON。`BatchProcessor` 允許你提供自訂的回呼函式：

```csharp
BatchProcessor.ProcessFolder(
    sourceFolder,
    outputFolder,
    ocrEngine,
    csvSummaryPath,
    (imagePath, ocrResult) =>
    {
        // Example: save as JSON
        var json = System.Text.Json.JsonSerializer.Serialize(new { Text = ocrResult.Text });
        string jsonPath = Path.ChangeExtension(Path.Combine(outputFolder,
                              Path.GetFileNameWithoutExtension(imagePath)), ".json");
        File.WriteAllText(jsonPath, json);
    });
```

### 7.2 處理多語言

若資料夾內包含混合語言的文件，你可以在每張影像上偵測語言，或執行兩次處理：

```csharp
ocrEngine.Language = Language.Spanish; // first pass
BatchProcessor.ProcessFolder(...);
ocrEngine.Language = Language.English; // second pass
BatchProcessor.ProcessFolder(...);
```

### 7.3 優雅地跳過損毀檔案

在迴圈內加入過濾（或使用接受 predicate 的重載），忽略會拋出例外的檔案：

```csharp
BatchProcessor.ProcessFolder(
    sourceFolder,
    outputFolder,
    ocrEngine,
    csvSummaryPath,
    filter: path => !Path.GetFileName(path).StartsWith("ignore_"));
```

## 完整範例程式

以下是完整的 `Program.cs`，可直接複製貼上到新的 Console 專案。請自行替換資料夾路徑。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BulkOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine – set language to English
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Define folders – adjust these for your environment
            string sourceFolder = @"C:\OcrDemo\Images\Bulk";
            string outputFolder = @"C:\OcrDemo\Output\BulkResults";
            string csvSummaryPath = Path.Combine(outputFolder, "summary.csv"); // optional

            try
            {
                // 3️⃣ Validate folders
                if (!Directory.Exists(sourceFolder))
                    throw new DirectoryNotFoundException($"Source folder not found: {sourceFolder}");

                Directory.CreateDirectory(outputFolder); // creates if missing

                // 4️⃣ Clean previous CSV (optional)
                if (File.Exists(csvSummaryPath))
                    File.Delete(csvSummaryPath);

                // 5️⃣ Run the batch OCR
                BatchProcessor.ProcessFolder(
                    sourceFolder: sourceFolder,
                    outputFolder: outputFolder,
                    engine: ocrEngine,
                    csvSummaryPath: csvSummaryPath);

                Console.WriteLine("✅ Batch OCR completed successfully!");
                Console.WriteLine($"📂 Text files are in: {outputFolder}");
                Console.WriteLine($"📄 CSV summary (if requested) at: {csvSummaryPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ An error occurred during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### 預期的 Console 輸出

```
✅ Batch OCR completed successfully!
📂 Text files are in: C:\OcrDemo\Output\BulkResults
📄 CSV summary (if requested) at: C:\OcrDemo\Output\BulkResults\summary.csv
```

開啟其中一個產生的 `.txt` 檔，你應該會看到已擷取的文字，準備進行後續處理。

## 常見問題

**這能處理 PDF 輸入嗎？**  
Aspose.OCR 可以在先將 PDF 頁面轉成影像（例如使用 Aspose.PDF）後處理。批次處理器本身只會搜尋光柵影像格式。

**如果我要處理 10,000 張影像怎麼辦？**  
內建的 `BatchProcessor` 會一次串流處理單一檔案，保持低記憶體使用量。若工作量極大，可考慮平行處理子資料夾，但請注意 OCR 本身是 CPU 密集型工作，需留意機器的核心數量。

**我可以調整 OCR 的準確度設定嗎？**  
可以。`ocrEngine` 提供 `Resolution`、`PreprocessOptions` 等屬性。調整這些參數可在低品質掃描上提升結果，但會犧牲速度。

**如何為正式環境授權 Aspose.OCR？**  
將授權檔 (`Aspose.OCR.lic`) 放在執行檔目錄，並在啟動時載入：

```csharp
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

## 結論

現在你已擁有一個 **完整、可投入生產的批量 OCR 解決方案**，使用 C# 實作。本文涵蓋了從安裝 Aspose.OCR、初始化引擎、處理整個資料夾，到匯出 CSV 摘要的全部步驟。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}