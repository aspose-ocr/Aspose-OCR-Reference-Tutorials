---
category: general
date: 2026-05-06
description: 學習如何在 C# 中使用 Aspose OCR 對 PDF 檔案執行光學字符辨識（OCR）。本教學亦示範如何從 PDF 提取文字以及載入
  PDF 進行 OCR。
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF
- how to extract text from scanned PDF
- load PDF for OCR
language: zh-hant
og_description: 了解如何在 C# 中使用 Aspose OCR 對 PDF 進行 OCR。提供逐步程式碼、說明與技巧，讓您高效擷取 PDF 文字。
og_title: 使用 Aspose OCR 於 PDF 進行光學字符辨識 – 完整指南
tags:
- Aspose OCR
- C#
- PDF processing
title: 使用 Aspose OCR 在 PDF 上執行 OCR – 完整指南
url: /zh-hant/net/text-recognition/perform-ocr-on-pdf-with-aspose-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 上執行 OCR（使用 Aspose OCR） – 完整指南

是否曾經需要 **在 PDF 上執行 OCR**，卻不知從何開始？你並不孤單。在許多實務專案中——例如自動化發票處理或數位化保存的報告——能夠從掃描的 PDF 中擷取文字是必備的。  

在本教學中，我們將一步步示範一個實作解決方案，不僅 **在 PDF 上執行 OCR**（使用 Aspose OCR 函式庫），還會說明如何 **從 PDF 擷取文字**、**載入 PDF 以進行 OCR**，甚至處理多語言文件。完成後，你將擁有一個可直接執行的 C# 程式，能把任何掃描的 PDF 轉換成可搜尋、可編輯的文字。

## 你將學會

- 如何在 .NET 專案中設定 Aspose OCR。  
- **載入 PDF 以進行 OCR** 的完整步驟，並將檔案送入引擎。  
- 如何將不同語言對應到各個頁面——當 PDF 同時包含英文、法文與德文時非常有用。  
- 驗證輸出結果與排除常見問題的方法。  

> **專業小技巧：** 若處理大型 PDF，考慮以平行方式處理頁面，可縮短數分鐘的執行時間。我們稍後會提及。

## 前置條件

- .NET 6.0 或更新版本（此程式碼同樣適用於 .NET Core 與 .NET Framework）。  
- 有效的 Aspose OCR 授權或暫時的評估金鑰。  
- 一個名為 `multilang.pdf` 的掃描 PDF，放置於程式碼可參考的資料夾中。  

不需要其他第三方套件。

---

## Step 1 – 安裝 Aspose OCR 並建立引擎

首先，將 Aspose.OCR NuGet 套件加入你的專案：

```bash
dotnet add package Aspose.OCR
```

套件安裝完成後，即可實例化 OCR 引擎。此物件是整個作業的核心，負責讀取影像、PDF，並將它們轉換成文字。

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Create an OCR engine instance – this is where we’ll perform OCR on PDF
var ocrEngine = new OcrEngine();
```

> **為什麼重要：** 只初始化一次引擎並在多頁間重複使用，可降低記憶體開銷並提升處理速度。

---

## Step 2 – 載入 PDF 文件以進行 OCR

引擎可以直接開啟 PDF，但必須告訴它要處理哪一個檔案。這就是許多開發者常忽略的 **載入 PDF 以進行 OCR** 步驟。

```csharp
// Load the multi‑language PDF document from disk
ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");
```

將 `YOUR_DIRECTORY` 替換為你機器上的實際路徑。若檔案是以資源方式嵌入，也可以從串流載入。

> **特殊情況：** 若 PDF 受密碼保護，請呼叫 `ocrEngine.LoadPdf(path, password)` 提供解密密碼。

---

## Step 3 – 將語言對應到頁面（可選但功能強大）

掃描的 PDF 常會包含不同語言的頁面。預設情況下 Aspose OCR 會假設英文，導致法文或德文頁面的辨識效果不佳。我們將建立一個簡易字典，告訴引擎每頁應使用哪種語言。

```csharp
// Define a language map: page index → OcrLanguage enum
var languageMap = new Dictionary<int, OcrLanguage>
{
    { 0, OcrLanguage.English }, // Page 1
    { 1, OcrLanguage.French },  // Page 2
    { 2, OcrLanguage.German }   // Page 3
};

// Provide the mapping via a lambda expression
ocrEngine.PageLanguageProvider = pageIndex =>
    languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;
```

> **為什麼要這樣做：** 提供正確的語言可大幅提升辨識準確度，尤其是對於帶重音符號的字元與語言特有的標點符號。

---

## Step 4 – 執行 OCR 並取得結果

現在開始進行重點工作。呼叫 `Recognize()` 會依照剛才設定的語言對應，處理 *所有* 頁面。

```csharp
// Run OCR on every page and collect the result
var recognitionResult = ocrEngine.Recognize();
```

`recognitionResult` 物件包含一個 `Text` 屬性，會彙總每一頁的辨識文字。

---

## Step 5 – 輸出擷取的文字

最後，我們只需要把合併後的文字寫入主控台——當然，你也可以寫入檔案、資料庫或其他下游系統。

```csharp
// Display the combined OCR output
Console.WriteLine(recognitionResult.Text);
```

如果想寫入檔案：

```csharp
System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
```

> **驗證小技巧：** 開啟產生的 `extracted_text.txt`，搜尋每種語言的已知詞彙。若法文重音顯示異常，請再次確認語言對應設定。

---

## 完整範例程式

以下提供一個完整、可直接執行的程式範例。將它貼到新的 Console 專案中，按 **F5** 即可執行。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑language PDF document
        // Make sure the path points to your actual file
        ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");

        // Step 3: Define which language should be used for each page
        var languageMap = new Dictionary<int, OcrLanguage>
        {
            { 0, OcrLanguage.English },
            { 1, OcrLanguage.French },
            { 2, OcrLanguage.German }
        };

        // Step 4: Provide the language mapping to the engine
        ocrEngine.PageLanguageProvider = pageIndex =>
            languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;

        // Step 5: Run OCR on all pages
        var recognitionResult = ocrEngine.Recognize();

        // Step 6: Output the combined text from the document
        Console.WriteLine("=== OCR Output Start ===");
        Console.WriteLine(recognitionResult.Text);
        Console.WriteLine("=== OCR Output End ===");

        // Optional: Save to a file for later use
        System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
        Console.WriteLine("Text saved to extracted_text.txt");
    }
}
```

**預期輸出**（為簡潔起見已截斷）：

```
=== OCR Output Start ===
Page 1 (English):
Invoice #12345
Date: 2024‑04‑30
...

Page 2 (French):
Facture #12345
Date : 30/04/2024
...

Page 3 (German):
Rechnung #12345
Datum: 30.04.2024
...
=== OCR Output End ===
Text saved to extracted_text.txt
```

---

## 處理大型 PDF 與效能調校

若你的 PDF 包含數百頁，建議採取以下調整：

1. **分段處理** – 每次處理 50 頁，然後將中間結果寫入磁碟。  
2. **平行處理** – 使用 `Parallel.ForEach` 搭配獨立的 `OcrEngine` 實例（每個引擎在初始化後皆為執行緒安全）。  
3. **記憶體管理** – 每處理完一個分段後呼叫 `ocrEngine.Dispose()`，釋放原生資源。

```csharp
Parallel.ForEach(pageIndices, pageIdx =>
{
    var localEngine = new OcrEngine();
    localEngine.LoadPdf("multilang.pdf", pageIdx, 1); // Load a single page
    // Apply language mapping as before …
    var result = localEngine.Recognize();
    // Append result.Text to a thread‑safe collection
    localEngine.Dispose();
});
```

---

## 常見問題與解決方式

| 症狀 | 可能原因 | 解決方式 |
|------|----------|----------|
| 法文頁面出現亂碼 | 語言設定錯誤 | 確認 `PageLanguageProvider` 為該頁返回 `OcrLanguage.French`。 |
| 輸出檔案為空 | PDF 未正確載入（路徑錯誤） | 檢查路徑是否正確，且檔案未被其他程序鎖定。 |
| 大型 PDF 發生記憶體不足例外 | 引擎一次載入整份 PDF | 改用 `LoadPdf` 的單頁重載或分段處理。 |
| 處理緩慢（> 5 分鐘處理 100 頁） | 單執行緒執行 | 如上所示啟用平行處理。 |

---

## 往下走 – 超越基礎 OCR

既然已能 **在 PDF 上執行 OCR** 並 **從 PDF 擷取文字**，你可能想進一步：

- **可搜尋 PDF 建立** – 使用 Aspose.PDF 將 OCR 文字嵌回原始 PDF，使其可搜尋。  
- **資料抽取** – 以正規表達式抓取發票號碼、日期或金額等資訊。  
- **與 AI 整合** – 將 OCR 輸出送入語言模型（例如 Azure OpenAI）進行摘要或分類。  

所有這些延伸功能仍仰賴 **載入 PDF 以進行 OCR** 的核心能力，你已具備基礎。

---

## 結論

我們已完整說明如何在 C# 中使用 Aspose OCR **在 PDF 上執行 OCR**。從安裝函式庫、載入 PDF、為每頁指定語言、執行辨識引擎，到最終 **從 PDF 擷取文字** 並儲存，整個教學提供一套自給自足、可投入生產環境的解決方案。  

歡迎自行嘗試平行處理、不同語言組合，或將 OCR 文字與其他文件處理函式庫結合。若遇到問題，請參考上方的故障排除表，或留下評論——祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}