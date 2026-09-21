---
category: general
date: 2026-02-09
description: 使用 C# 設定批次 OCR 的最大平行度，快速擷取圖像文字——學習如何轉換掃描頁面、處理多圖像 OCR 以及高效讀取 PNG 文字。
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: zh-hant
og_description: 在 C# 中設定最大平行度以提取圖像文字。本教學示範如何轉換掃描頁面、執行多圖像 OCR 以及使用 Aspose OCR 讀取 PNG
  文字。
og_title: 使用 C# 從 PNG 中提取文字圖像 – 完整批次 OCR 指南
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: 使用 C# 從 PNG 中提取文字圖像 – 使用 Aspose OCR 進行批次 OCR
url: /zh-hant/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 PNG 中提取文字圖像（C#） – 使用 Aspose OCR 進行批次 OCR

有沒有需要從一個掃描 PNG 資料夾中 **提取文字圖像**，卻卡在「如何加快速度？」的問題上？你並不孤單。在許多實務專案中，開發者必須 **設定最大平行度**，才能在數秒內處理數十頁，而非數分鐘。  

本指南將逐步說明一個完整、可執行的範例，**轉換掃描頁面**、執行 **多圖像 OCR**，最後 **讀取 PNG 文字**，讓你輕鬆上手。沒有模糊的「請參考文件」連結——只有可直接複製貼上的程式碼、每行程式碼重要性的說明，以及避免常見陷阱的技巧。

> **專業提示：**如果你已在其他地方使用 Aspose OCR，你會發現相同的 `OcrEngine` 類別在此出現，但我們會調整其設定以實現真正的平行處理。

---

## 需要的環境

- **.NET 6+**（或 .NET Framework 4.6+）。API 的使用方式相同，但較新的執行環境提供更佳的執行緒處理。  
- **Aspose.OCR for .NET** – 透過 NuGet 安裝：`Install-Package Aspose.OCR`。  
- 一個包含數個 PNG 掃描檔的資料夾（`page1.png`、`page2.png`，…）。  
- 你熟悉的 IDE 或編輯器（Visual Studio、Rider、VS Code …）。

就這樣。無需額外服務、無需雲端金鑰，純粹在本機處理。

---

## 提取文字圖像 – 設定批次 OCR 的最大平行度

當你對多個檔案啟動 OCR 時，引擎預設只使用單一執行緒。這樣雖安全卻非常慢。透過設定 `MaxDegreeOfParallelism`，你可以告訴引擎同時可啟動多少執行緒。

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**為什麼是 4？**  
在大多數現代筆記型電腦上，4 核心是一個理想的平衡點——足以讓 CPU 保持忙碌，同時不會過度佔用資源而影響其他程序。若在擁有 16 核心的伺服器上執行，可將數值提升至 12 或 14，以獲得明顯的加速效果。

---

## 轉換掃描頁面 – 建立 Image Stream 集合

Aspose 需要每張圖片為 `ImageStream`。`FromFile` 輔助方法會讀取檔案、將其保留於記憶體，並傳遞給 OCR 引擎。若圖片來源於資料庫或 HTTP 回應，你也可以傳入 `MemoryStream`。

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**邊緣情況：**如果任何檔案遺失或損壞，`FromFile` 會拋出 `FileNotFoundException`。若預期輸入不穩定，請將建構包在 `try/catch` 中。

---

## 多圖像 OCR – 執行批次 OCR

現在開始大量運算。`RecognizeBatch` 會根據先前設定的執行緒數量啟動相應的執行緒，處理每張圖片，並回傳 `OcrResult` 物件的清單。

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

在背後，每個執行緒會載入其圖片、執行神經網路，並擷取純文字。結果的順序與輸入清單的順序相同，因而可以安全地將第 1 頁對應到 result 0，依此類推。

---

## 讀取 PNG 文字 – 顯示擷取的內容

最後，我們遍歷結果並將純文字輸出至主控台。你也可以將輸出導入檔案、資料庫，甚至下游的 NLP 服務。

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### 預期的主控台輸出

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

如果看到空白區段，請再次確認 PNG 不是純白圖像——OCR 需要一定的對比度。

---

## 實用技巧與常見陷阱

| Situation | What to Do |
|-----------|------------|
| **大量批次的記憶體壓力** | 將圖片分批處理（每批 10‑20 個檔案），若發現記憶體尖峰則呼叫 `GC.Collect()`。 |
| **語言偵測不正確** | 在呼叫 `RecognizeBatch` 前，設定 `ocrEngine.Configuration.Language = OcrLanguage.English;`（或你的目標語言）。 |
| **即使平行化仍效能緩慢** | 確認 SSD 沒有限制 I/O；先將所有檔案讀入記憶體（如同使用 `ImageStream.FromFile`）。 |
| **缺字** | 將 `ocrEngine.Configuration.DPI = 300;` 提高，以進行更高解析度的處理。 |

---

## 擴充範例 – 從 PNG 轉為 PDF 或 DOCX

如果最終需要將 **掃描頁面** 轉換為可搜尋的 PDF，只需將相同的 `ocrResults[i].PlainText` 傳入 PDF 函式庫（例如 Aspose.PDF），並以隱形圖層覆蓋文字。相同的平行化技巧同樣適用於此。

---

## 完整原始碼（可直接複製貼上）

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

將此檔案另存為 `BatchExample.cs`，執行 `dotnet run`，即可看到主控台顯示先前隱藏在 PNG 掃描檔中的文字。

---

## 視覺摘要

![提取文字圖像範例](images/ocr-batch.png){alt="提取文字圖像範例"}

圖示說明流程：**PNG 檔案 → ImageStream 集合 → OcrEngine（最大平行度） → OCR 結果 → 主控台 / 下游儲存**。

---

## 結論

現在你已掌握一套完整、端到端的作法，能在 C# 中 **提取文字圖像**，同時 **設定最大平行度**、**轉換掃描頁面**、處理 **多圖像 OCR**，以及 **讀取 PNG 文字**，且效率高。程式碼自成一體，說明同時涵蓋「如何」與「為何」，而技巧則可避免常見的麻煩。

接下來可以怎麼做？嘗試將 PNG 清單改為動態的 `Directory.GetFiles` 迴圈、實驗不同的執行緒數量，或將輸出導入可搜尋的 PDF。相同的模式可輕鬆擴展至數百頁，幾乎不需額外程式碼。

有任何問題或特殊邊緣案例嗎？在下方留言，我們會回覆。祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}