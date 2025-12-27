---
category: general
date: 2025-12-27
description: 在 C# 中建立主控台記錄器，並使用 AsposeAI 啟用自動下載至正確的表格。學習如何在幾個步驟內顯示已校正的表格輸出。
draft: false
keywords:
- create console logger
- enable auto download
- how to correct tables
- setup console logger
- display corrected table
language: zh-hant
og_description: 建立 C# 主控台記錄器，並使用 AsposeAI 啟用自動下載至正確的表格。遵循此指南，即可快速顯示已校正的表格輸出。
og_title: 使用 AsposeAI 建立控制台記錄器並校正表格
tags:
- AsposeAI
- C#
- OCR
- Table processing
title: 使用 AsposeAI 創建控制台記錄器並校正表格
url: /zh-hant/net/ocr-optimization/create-console-logger-and-correct-tables-with-asposeai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 Console Logger 並使用 AsposeAI 校正表格

有沒有曾經想 **建立 Console Logger** 來記錄 C# AI 流程，但不知從何下手？本教學將一步步說明如何建立 Console Logger、啟用模型檔案自動下載，最後 **校正 OCR 產生的表格**。完成後，你只需幾行程式碼，即可在 Console 中 **顯示校正後的表格** 結果。

我們會從最初的 Logger 設定講到最後的清理工作，讓你不必在零散的文件中搜尋。即使沒有 AsposeAI 的使用經驗，只要具備基本的 C# 與 .NET 知識即可。過程中，我們也會提供 **設定 Console Logger** 的最佳實踐、說明常見邊緣案例，並示範預期的輸出樣式。

---

## 前置條件

在開始之前，請確保你已具備以下環境：

- .NET 6.0 或更新版本（程式碼使用了現代語言功能）
- Visual Studio 2022 或任何支援 C# 專案的 IDE
- 已安裝 **Aspose.AI** NuGet 套件 (`Install-Package Aspose.AI`)
- 已安裝 **Aspose.OCR** NuGet 套件 (`Install-Package Aspose.OCR`)
- 先前透過 Aspose.OCR 取得的範例 OCR 結果物件 (`ocrResult`)

若缺少任何項目，請先完成安裝與設定，之後再繼續。

---

## 步驟 1：建立 Console Logger 並初始化 AsposeAI

首先，我們需要一個直接寫入 Console 的 logger。這樣可以在 AI 引擎執行時即時取得除錯資訊。

```csharp
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

// Step 1: Create a logger that writes to the console
ILogger consoleLogger = new ConsoleLogger();

// Step 2: Initialise the AsposeAI engine with the logger
AsposeAI asposeAI = new AsposeAI(consoleLogger);
```

**為什麼這很重要：**  
`ConsoleLogger` 實作了 `ILogger` 介面，所有來自 AsposeAI 的內部訊息（模型載入、後處理狀態、錯誤）都會即時顯示在終端機上。這是 **設定 Console Logger** 的最簡方式，且不需額外引入外部日誌框架。

> **小技巧：** 若日後需要寫入檔案，只要將 `ConsoleLogger` 換成自訂實作 `ILogger` 的 logger，其他程式碼即可保持不變。

---

## 步驟 2：啟用 AI 模型的自動下載

AsposeAI 能在執行時即時下載所需的模型檔案。開啟此功能可免除手動下載大型二進位檔的麻煩。

```csharp
// Step 3: (Optional) Configure automatic model download and set the model directory
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,               // <‑‑ enable auto download
    DirectoryModelPath = "YOUR_DIRECTORY"   // change to a writable folder
};
```

**可能會發生什麼問題？**  
如果 `DirectoryModelPath` 指向唯讀目錄，自動下載會失敗，並在 Console 中拋出例外。請確認資料夾已存在且應用程式具備寫入權限。

---

## 步驟 3：建立表格後處理器（如何校正表格）

OCR 取得的表格常常雜亂——合併儲存格、缺少框線或文字對齊錯誤。AsposeAI 的 `TableAIProcessor` 能自動清理這些問題。

```csharp
// Step 4: Create a table post‑processor that lets the engine decide when to run correction
TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);
```

**為什麼使用 AUTO 模式？**  
`AITableDetectionMode.AUTO` 讓引擎自行檢查 OCR 輸出，判斷是否需要校正。若想手動控制，也可以改用 `MANUAL`，自行呼叫 `RunCorrection()`。

---

## 步驟 4：掛載後處理器與其設定

現在把所有元件結合起來——logger、模型設定與表格處理器。

```csharp
// Step 5: Attach the post‑processor and its configuration to the AI engine
asposeAI.SetPostProcessor(tableProcessor, modelConfig);
```

此時 AI 引擎已知道 *模型存放位置*、*如何記錄* 以及 *要套用哪種後處理*。這樣的關注點分離讓未來的變更變得輕鬆。

---

## 步驟 5：對 OCR 結果執行後處理

假設你已經擁有來自 Aspose.OCR 的 `ocrResult`，只要把它交給引擎即可。

```csharp
// Step 6: Run the post‑processor on the OCR result returned by Aspose.OCR
asposeAI.RunPostprocessor(ocrResult);
```

**邊緣案例提醒：**  
如果 `ocrResult` 中根本沒有表格，處理器會靜默跳過校正。之後可以檢查 `tableProcessor.GetResult().Count` 以確認是否真的有處理到表格。

---

## 步驟 6：取得並 **顯示校正後的表格** 輸出

最後，將清理過的表格文字取出並印到 Console。

```csharp
// Step 7: Retrieve and display the corrected table text
Console.WriteLine("Corrected table output:");
Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
```

輸出範例（依來源影像而異）：

```
Corrected table output:
| Item   | Quantity | Price |
|--------|----------|-------|
| Apple  | 10       | $1.20 |
| Banana | 5        | $0.80 |
```

若看到空字串，請再次確認 OCR 是否偵測到表格，以及 `AllowAutoDownload` 是否成功執行。

---

## 步驟 7：釋放資源

完成工作後，記得釋放佔用較大資源的物件。

```csharp
// Step 8: Release resources used by the AI engine
asposeAI.Dispose();
```

若省略此步驟，可能會留下檔案句柄未關閉，尤其在 Windows 上模型檔案會被鎖定。

---

## 完整範例程式

以下提供可直接貼到新 Console 專案的完整程式碼。將 `"YOUR_DIRECTORY"` 替換為實際路徑，並確保在呼叫 `RunPostprocessor` 前已正確填入 `ocrResult`。

```csharp
using System;
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

namespace AsposeAITableCorrection
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a console logger
            ILogger consoleLogger = new ConsoleLogger();

            // 2️⃣ Initialise AsposeAI with the logger
            AsposeAI asposeAI = new AsposeAI(consoleLogger);

            // 3️⃣ Configure auto‑download (optional but recommended)
            AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
            {
                AllowAutoDownload = true,
                DirectoryModelPath = @"C:\AsposeModels" // <-- change this
            };

            // 4️⃣ Create the table processor (auto‑detect mode)
            TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);

            // 5️⃣ Attach processor and config
            asposeAI.SetPostProcessor(tableProcessor, modelConfig);

            // 6️⃣ Obtain OCR result (replace with your own OCR call)
            // Example placeholder – you should have this from Aspose.OCR already
            OcrResult ocrResult = GetOcrResultSomehow();

            // 7️⃣ Run post‑processor on the OCR output
            asposeAI.RunPostprocessor(ocrResult);

            // 8️⃣ Display corrected table
            Console.WriteLine("Corrected table output:");
            if (tableProcessor.GetResult().Count > 0)
            {
                Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
            }
            else
            {
                Console.WriteLine("No tables were detected or corrected.");
            }

            // 9️⃣ Clean up
            asposeAI.Dispose();
        }

        // Dummy method – replace with your actual OCR logic
        static OcrResult GetOcrResultSomehow()
        {
            // For illustration only
            OcrEngine engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample-table.png");
            return engine.Recognize();
        }
    }
}
```

**預期的 Console 輸出**（以簡易表格影像為例）：

```
Corrected table output:
| Name   | Age | City      |
|--------|-----|-----------|
| Alice  | 30  | New York  |
| Bob    | 25  | Seattle   |
```

---

## 常見問題與解答

- **自動下載需要網路連線嗎？**  
  需要。首次請求模型時，AsposeAI 會連到 CDN 下載。下載完成後存於 `DirectoryModelPath`，之後即可離線執行。

- **表格有合併儲存格怎麼辦？**  
  AI 模型會根據視覺線索嘗試拆分合併儲存格。若結果不理想，可在 OCR 前先對影像做前處理（提升對比、校正旋轉）。

- **可以一次處理多張表格嗎？**  
  可以。`tableProcessor.GetResult()` 會回傳列表，遍歷即可印出每張表格。

- **`ConsoleLogger` 是執行緒安全的嗎？**  
  它直接寫入 `System.Console`，對於簡單寫入而言是執行緒安全的。若在大量多執行緒情境下，建議自行實作具同步機制的 logger。

---

## 後續步驟與相關主題

了解 **如何校正表格** 後，你可能想進一步：

- 為其他 AsposeAI 模型（例如語言翻譯） **啟用自動下載**。
- 使用不同的日誌等級（Info、Warning、Error） **設定 Console Logger**，取得更細緻的控制。
- 在 GUI（WinForms 或 WPF）中 **顯示校正後的表格**，取代 Console。
- 結合表格校正與 **資料抽取**，直接寫入資料庫。

上述主題皆以本教學的基礎為出發點，歡迎自行實驗。

---

## 結論

我們完整示範了 **建立 Console Logger**、啟用自動下載，並使用 AsposeAI **校正表格** 的全流程，最後以乾淨的方式 **顯示校正後的表格**。現在，你已掌握這套工具鏈的核心操作，接下來可以自由擴展與應用。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}