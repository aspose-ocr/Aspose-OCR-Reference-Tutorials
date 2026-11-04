---
category: general
date: 2026-03-26
description: 如何在 C# 中批次 OCR，使從 PNG 檔案提取文字變得簡單。跟隨這個一步一步的 C# OCR 教學，使用 Aspose OCR 進行批次文字提取。
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: zh-hant
og_description: 如何在 C# 中批次 OCR，讓您快速從 PNG 檔案提取文字。本指南將帶您完成完整的 C# OCR 教學，實現批次文字提取。
og_title: 在 C# 中批次執行 OCR – 從 PNG 提取文字
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中批次執行 OCR – 從 PNG 提取文字
url: /zh-hant/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批次 OCR – 從 PNG 提取文字

有沒有想過 **如何批次 OCR** 一堆螢幕截圖，而不必為每個檔案寫一個獨立程式？你並不孤單。在許多專案中，我們最終會有數十個 PNG 需要擷取文字，逐一處理實在很麻煩。  

好消息是？使用 Aspose OCR，你可以快速建立一個小型 C# 主控台應用程式，平行處理所有影像，實現快速的 **批次文字擷取** 並產生整潔的結果集合。本指南將逐步說明完整的 **c# ocr tutorial**，解釋每個部份的意義，並展示最終的輸出樣貌。

閱讀完本文後，你將能夠：

* 一次載入多個 PNG（或任何支援的影像）檔案清單。  
* 設定共用的 `OcrEngine`，讓設定在整個批次中保持一致。  
* 使用最多四個平行工作者執行辨識佇列。  
* 取得每頁的辨識文字並印出到主控台。

沒有魔法，只有可直接套用到你解決方案中的實用程式碼。

## 需要的環境

在開始之前，請確保你已具備：

* .NET 6 SDK（或任何較新的 .NET 版本）。  
* 有效的 Aspose OCR 授權或暫時的評估金鑰。  
* 放置欲處理 PNG 檔案的資料夾。  
* Visual Studio 2022 或你慣用的編輯器。

就這樣——除了 `Aspose.OCR` 與標準的 `System.Collections.Generic`，不需要額外的 NuGet 套件。

## 如何批次 OCR – 建立專案

首先，建立一個新的主控台專案，並加入 Aspose OCR 套件。

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

還原完成後，開啟 **Program.cs**（或建立新檔案），加入一般的 `using` 指示詞：

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

這個簡易骨架讓我們可以使用 `OcrEngine`、`RecognitionQueue` 以及稍後會用到的輔助類別。

## 從 PNG 提取文字 – 準備影像清單

接下來必須告訴程式 **要處理哪些 PNG**。最直接的方式是建立一個 `List<string>`，內含絕對或相對路徑。

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

將 `YOUR_DIRECTORY` 替換成實際的資料夾路徑。如果你的檔案集合是動態的，也可以使用 `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")`，再把結果填入清單。重點是 **extract text from PNG** 只要把正確的檔名送入佇列即可。

![How to batch OCR workflow](https://example.com/placeholder.png "Diagram illustrating how to batch OCR a collection of PNG files")

*Image alt text: how to batch OCR workflow diagram*

## C# OCR tutorial – 設定辨識佇列

批次作業的核心是 `RecognitionQueue`。把它想像成傳送帶，將每張影像交給共用的 `OcrEngine`。透過共用引擎，我們可以降低記憶體使用，且保證每頁使用相同設定。

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

為什麼要把 `MaxDegreeOfParallelism` 設為 4？在一般的四核心筆記型電腦上，這樣可以取得最佳吞吐量，同時不會讓作業系統資源枯竭。如果在核心數更多的伺服器上執行，只要相應調高數值即可。

### 小技巧

如果需要自訂語言套件、DPI 設定或感興趣區域裁切，請在將任何影像加入佇列前 **一次** 在共用的 `Engine` 上完成。例如：

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

之後的所有辨識都會自動繼承這些選項——這正是 **how to create OCR** 流程保持一致的關鍵。

## 批次文字擷取 – 將影像加入佇列並執行

佇列準備好後，接下來要把每張影像推入佇列。`Enqueue` 方法接受一個 `OcrImage` 例項，我們可以從檔案路徑建立它。

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

所有檔案都加入佇列後，啟動處理：

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` 會阻塞直到每張影像完成，然後回傳一個清單，清單中的每個元素對應於輸入的順序。這保證第 1 頁的結果在索引 0，第 2 頁在索引 1，以此類推——在需要將結果映射回來源檔案時非常方便。

## How to create OCR – 顯示結果

最後，將辨識文字印到主控台。這就是實際看到 **batch text extraction** 效果的時刻。

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

執行程式 (`dotnet run`) 後，你應該會看到類似以下的輸出：

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

如果某張影像失敗（例如檔案損毀），對應的 `OcrResult` 會有空的 `Text` 屬性，你可以檢查 `ocrResults[i].Exception` 取得診斷資訊。

## How to create OCR – 小技巧、邊緣案例與最佳實踐

### 處理大型批次

若一次處理上百張 PNG，仍可能因保留所有 `OcrResult` 物件而耗盡記憶體。此時可在每筆結果產生後立即將輸出寫入檔案或資料庫：

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### 支援非 PNG 格式

Aspose OCR 也原生支援 JPEG、BMP 與 TIFF。只要在清單中更改副檔名或使用萬用字元搜尋即可。相同的 **c# ocr tutorial** 步驟仍然適用——不需要修改程式碼。

### 跳過空白頁

如果處理的 PDF 有時會出現空白頁，可以過濾結果：

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### 授權考量

評估版會在每頁加上浮水印。正式上線時，請在 `Main` 開頭載入授權檔案：

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### 平行度調校

`MaxDegreeOfParallelism` 預設為 `Environment.ProcessorCount`。如果發現 CPU 使用率過高或記憶體壓力大，可降低此值。相反地，在多核心的雲端 VM 上，將其提升以充分利用硬體。

## 小結

現在你已擁有完整的 **how to batch OCR** 解決方案，能在 C# 中 **extract text from PNG** 檔案、平行執行，並取得整潔且有序的結果。透過共用單一 `OcrEngine`，你已學會 **how to create OCR** 流程的記憶體效能與維護性。這個 **c# ocr tutorial** 也示範了如何將 **batch text extraction** 擴展至數百張影像，只需少量額外程式碼。

---

### 接下來可以做什麼？

* 嘗試加入語言偵測 (`Engine.Language = Language.AutoDetect`)。  
* 實驗不同的輸出格式——將結果寫成 JSON 或 CSV，供後續分析使用。  
* 結合 PDF 轉影像的步驟，處理整份掃描文件。

隨意調整平行度、換成自己的影像來源，或把結果匯入搜尋索引。掌握 **how to batch OCR** 在 C# 後，天地任你闊步。

祝開發順利，願你的 OCR 執行快速且零錯誤！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}