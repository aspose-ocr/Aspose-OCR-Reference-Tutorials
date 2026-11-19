---
category: general
date: 2026-05-25
description: 使用 Aspose.OCR 於 C# 將 TIFF 轉換為文字。學習批次圖像轉文字的轉換方法，並高效提取 TIFF 檔案中的文字。
draft: false
keywords:
- convert tiff to text
- extract text from tiff
- batch image to text conversion
- convert scanned images txt
language: zh-hant
og_description: 使用 Aspose.OCR 將 TIFF 轉換為文字。本指南示範批次影像轉文字的轉換方式，以及如何在幾行 C# 程式碼中從 TIFF
  檔案提取文字。
og_title: 將 TIFF 轉換為文字（C#）– 完整批次 OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  headline: Convert TIFF to Text in C# – Complete Batch OCR Guide
  type: TechArticle
- description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  name: Convert TIFF to Text in C# – Complete Batch OCR Guide
  steps:
  - name: '**Create** an OCR engine set for English.'
    text: '**Create** an OCR engine set for English.'
  - name: '**Collect** every TIFF file from the target folder.'
    text: '**Collect** every TIFF file from the target folder.'
  - name: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
    text: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
  - name: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
    text: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
  type: HowTo
tags:
- C#
- OCR
- Aspose
- TIFF
title: 在 C# 中將 TIFF 轉換為文字 – 完整批次 OCR 指南
url: /zh-hant/net/text-recognition/convert-tiff-to-text-in-c-complete-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中將 TIFF 轉換為文字 – 完整批次 OCR 指南

是否曾需要 **將 TIFF 轉換為文字**，卻不知從何下手？你並不孤單——許多開發者在處理掃描文件時，都會卡在批次 OCR 上。本文將手把手示範一個 **從 TIFF 檔案擷取文字** 的解決方案，使用 Aspose.OCR，並以平行方式執行，讓大型資料夾在數秒內完成。

我們同時也會談到 **批次影像轉文字** 的最佳實踐，最終你將擁有一段可重複使用的程式碼，能將整個目錄的掃描影像一次性轉成整齊的 *.txt* 檔案——非常適合建立索引、搜尋，或供下游分析使用。

## 需要的環境

- **.NET 6.0** 或更新版本（程式碼亦可在 .NET Framework 上編譯）  
- **Aspose.OCR for .NET** NuGet 套件（`Install-Package Aspose.OCR`）  
- 一個包含一個或多個 *.tif* 檔案的資料夾（經典的 TIFF 掃描格式）  
- 你慣用的 IDE（Visual Studio、VS Code、Rider——隨你喜好）

就這些。無需外部服務、API 金鑰，只要純粹的 C# 與 Aspose。

![處理中的 TIFF 檔案及其產生的文字檔案之螢幕截圖](/images/ocr-result.png "OCR 結果顯示已轉換的 TIFF 為文字輸出")

*(Alt text: 螢幕截圖顯示已將 TIFF 轉換為文字的輸出結果)*

## 步驟 1：設定 OCR 引擎 – 將 TIFF 轉換為文字

首先，我們需要一個 `OcrEngine` 實例，並告訴它要讀取英文字符。引擎是轉換的核心；正確設定可確保結果可靠。

```csharp
using Aspose.OCR;
using System.IO;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Create an OCR engine configured for English – this is the core of convert TIFF to text
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };
```

*為什麼這很重要：*  
Aspose.OCR 支援數十種語言。如果你的掃描文件是多語言，只要將 `OcrLanguage.English` 改成對應的列舉值即可。若未指定語言，引擎會進入自動偵測模式，速度較慢且準確度可能下降。

## 步驟 2：收集所有 TIFF 檔案 – 高效提取 TIFF 文字

接著，我們從你指定的資料夾中抓取每一個 *.tif* 檔案。使用 `Directory.GetFiles` 可取得乾淨的陣列，方便後續批次處理。

```csharp
        // Locate every TIFF in the input folder – adjust the path to your own directory
        string inputFolder = @"C:\Scans\Batch";
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif", SearchOption.TopDirectoryOnly);

        if (tiffFiles.Length == 0)
        {
            System.Console.WriteLine("No TIFF files found. Check the folder path.");
            return;
        }
```

*小技巧：* 若掃描檔案散布於子資料夾，可使用 `SearchOption.AllDirectories` 旗標。但請注意，遞迴層級過深可能會在批次階段增加記憶體使用量。

## 步驟 3：執行平行 OCR – 批次影像轉文字

現在進入有趣的部分。Aspose.OCR 內建靜態輔助工具 `BatchOcr.RecognizeAll`，接受檔案路徑陣列、引擎以及 `parallelism` 提示。我們將啟動四條執行緒，在現代四核心筆記型電腦上可獲得近線性加速。

```csharp
        // Run OCR on all files in parallel (4 threads by default)
        // The result is a dictionary where Key = file path, Value = extracted text
        Dictionary<string, string> ocrResults = BatchOcr.RecognizeAll(tiffFiles, ocrEngine, parallelism: 4);
```

*為什麼要使用平行處理？*  
一次處理大量高解析度 TIFF 會非常耗費 CPU。將工作分散到多條執行緒，可讓所有核心保持忙碌，顯著縮短總執行時間。若在核心更多的伺服器上執行，只要相應提升 `parallelism` 數值即可。

## 步驟 4：寫入輸出 – 將掃描影像轉為 TXT 檔案

最後，我們遍歷字典，將每段文字寫入與原始檔名相同但副檔名為 *.txt* 的檔案。這就是 **將掃描影像轉為 txt** 成真的時刻。

```csharp
        // Save each recognized text to a .txt file with the same base name as the source TIFF
        foreach (var kvp in ocrResults)
        {
            string sourcePath = kvp.Key;
            string extractedText = kvp.Value;

            // Change extension from .tif to .txt
            string txtPath = Path.ChangeExtension(sourcePath, ".txt");

            // Write the text – UTF‑8 ensures all characters are preserved
            File.WriteAllText(txtPath, extractedText);
            System.Console.WriteLine($"Saved: {txtPath}");
        }

        System.Console.WriteLine("Batch conversion complete!");
    }
}
```

### 程式碼功能說明（簡易說明）

1. **建立** 一個設定為英文的 OCR 引擎。  
2. **收集** 目標資料夾內的所有 TIFF 檔案。  
3. **執行** `BatchOcr.RecognizeAll`，使用四條執行緒，將每張影像轉成字串。  
4. **遍歷** 結果，將 `.tif` 副檔名換成 `.txt`，並寫入磁碟。

以上就是在不到 50 行程式碼內完成 **將 TIFF 轉換為文字** 工作流程的全部內容。

## 處理例外情況 – 當流程不順時

- **遺失或損毀的 TIFF** – `BatchOcr` 會拋出 `OcrException`。如需優雅降級，請將呼叫包在 `try / catch` 中。  
- **非英文文件** – 將 `OcrLanguage.English` 改成 `OcrLanguage.Spanish`、`OcrLanguage.French` 等，或使用 `OcrLanguage.AutoDetect`。  
- **極大尺寸的影像** – 考慮在 OCR 前降低 DPI（`ocrEngine.ImagePreprocessing.Dpi = 200`），以節省記憶體，但可能會犧牲部分準確度。  
- **輸出編碼** – 若需特定代碼頁（例如 Windows‑1252），可使用 `File.WriteAllText(txtPath, extractedText, Encoding.GetEncoding(1252))`。

## 專業提示：打造穩健的批次轉換

- **記錄失敗**：建立 `List<string> failedFiles`，將拋例的檔案加入清單，最後寫入日誌。  
- **重複使用引擎**：同一個 `OcrEngine` 實例可在多個檔案間重複使用，切勿在迴圈內重新實例化。  
- **驗證結果**：簡單的 `if (string.IsNullOrWhiteSpace(extractedText))` 可偵測空白或無法辨識的掃描。  
- **結合 PDF**：若來源是多頁 PDF，可先使用 Aspose.PDF 逐頁轉成 TIFF，再套用本批次流程。

## 後續步驟 – 超越簡單轉換

現在你已能 **批次擷取 TIFF 文字**，接下來或許想：

- 將 *.txt* 檔案匯入搜尋索引（Elasticsearch、Azure Cognitive Search）。  
- 為每個結果執行語言偵測，將文件導向特定語系的處理管線。  
- 透過將 OCR 文字覆蓋回原始影像，產生可搜尋的 PDF（再次使用 Aspose.PDF）。  

所有這些情境皆建立在同一核心概念上：**批次影像轉文字** 是更大文件處理系統的基礎模組。

---

### 結論

你剛剛學會如何使用 Aspose.OCR **將 TIFF 轉換為文字**，以平行方式處理整個資料夾，並將每個結果儲存為乾淨的 *.txt* 檔案。此解決方案輕量、可完全自訂，且已具備上線條件——無論是數位化舊發票、歸檔掃描合約，或是為文字搜尋引擎供稿，都能輕鬆應對。

快試試看，調整平行度，開始把新產生的文字檔案投入你的工作流程吧。祝 OCR 順利！

---


## 相關教學

- [使用 OCR 操作於資料夾中擷取影像文字](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [影像文字擷取 – 使用 Aspose.OCR for .NET 進行 OCR 最佳化](/ocr/english/net/ocr-optimization/)
- [C# 以語言選擇擷取影像文字 – Aspose.OCR 範例](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}