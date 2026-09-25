---
category: general
date: 2025-12-29
description: 使用 Aspose OCR 批次處理，將掃描圖像製作成可搜尋的 PDF。學習將圖像轉換為 PDF、為 OCR 進行圖像前處理，以及校正掃描文件的傾斜。
draft: false
keywords:
- create searchable pdf
- batch ocr processing
- convert images to pdf
- preprocess images for ocr
- deskew scanned documents
language: zh-hant
og_description: 使用 Aspose OCR 批次處理，將掃描圖像製作可搜尋的 PDF。學習如何將圖像轉換為 PDF、為 OCR 進行圖像前處理，以及校正掃描文件的傾斜。
og_title: 使用批次 OCR 建立可搜尋的 PDF – C# 指南
tags:
- OCR
- C#
- PDF/A
- Aspose
title: 使用批次 OCR 建立可搜尋的 PDF – C# 指南
url: /zh-hant/net/ocr-optimization/create-searchable-pdf-with-batch-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立可搜尋 PDF（批次 OCR） – C# 教學

曾經需要 **建立可搜尋的 PDF** 檔案，卻因為大量掃描圖像而卡在第一步嗎？你並不孤單——大多數開發者在面對雜亂的掃描、頁面傾斜或大量轉換時，都會遇到同樣的障礙。  

好消息是？使用 Aspose OCR，你可以建立一個 **批次 OCR 處理** 流程，不僅 **將影像轉換為 PDF**，還能 **為 OCR 前置處理影像**，甚至自動 **校正掃描文件的傾斜**。在本教學中，我們將一步步說明，從設定引擎到優化輸出，讓你只需對一個資料夾執行，即可產出可搜尋的 PDF/A‑2b 檔案。

> **你將得到：** 一個完整、可執行的 C# 主控台應用程式，接受一個影像（或 PDF）資料夾，清理每一頁、執行 OCR，並在原始檔旁產生可搜尋的 PDF/A‑2b 檔案。沒有零散的程式碼片段，只有一個完整的解決方案。

---

## 前置條件

- .NET 6 SDK 或更新版本（程式碼同樣可在 .NET Core 上編譯）。  
- Aspose OCR NuGet 套件（`Aspose.OCR`）。  
- 一個包含掃描影像（TIFF、JPEG、PNG）或 PDF 的資料夾，準備轉換成可搜尋的 PDF。  
- （可選）正式授權金鑰——若未提供，試用模式會加上浮水印，但仍可用於測試。

如果你已備妥上述項目，讓我們開始吧。

---

## 概觀 – 整個流程如何產生可搜尋 PDF

1. **啟用試用模式**（或載入授權）。  
2. **設定 `OcrBatchProcessor`** – 指定讀取來源、輸出 PDF 的位置、使用的格式，以及平行執行的執行緒數量。  
3. **前置處理每張影像** – 校正傾斜、去除雜訊、去背，使 OCR 引擎看到乾淨的頁面。  
4. **執行批次** – Aspose 會處理每個檔案、執行 OCR，並寫入可搜尋的 PDF/A‑2b。  
5. **通知完成** – 簡單的主控台訊息，你也可以接上 logger 或 webhook。

以上即為高階流程。下方程式碼實作了每一步，並附有詳細註解，讓你可以自行調整而不會破壞整體。

---

## 步驟 1 – 啟用試用模式（或載入授權）

在呼叫任何 Aspose 類別之前，需要先讓程式庫知道你已取得授權。對於快速實驗，試用模式已足夠。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

// Activate trial mode – replace with OcrEngine.SetLicense("YourLicenseFile.lic") for production
OcrEngine.EnableTrialMode();
```

> **小技巧：** 請將授權啟用程式碼放在 `Program.cs` 最上方。若忘記，第一次呼叫 `Process()` 時引擎會拋出例外。

---

## 步驟 2 – 設定批次 OCR 處理引擎

以下是建立 **批次 OCR 處理** 物件的程式碼。請注意，此範例中 `InputFolder` 與 `OutputFolder` 為同一資料夾，實際使用時可自行分開。

```csharp
// Define where your source images live and where the searchable PDFs should be saved
var ocrBatch = new OcrBatchProcessor
{
    // Folder that contains the images or PDFs to be processed
    InputFolder = @"C:\Scans\Incoming",

    // Folder where searchable PDF/A‑2b files will be saved
    OutputFolder = @"C:\Scans\Processed",

    // Choose the output format – searchable PDF/A‑2b (perfect for archiving)
    OutputFormat = SaveFormat.SearchablePdf,

    // Limit the number of concurrent OCR operations to avoid CPU spikes
    MaxDegreeOfParallelism = 3,

    // Pre‑process each image: deskew, denoise, and remove background
    Preprocess = img => ImageFilters
                            .Deskew(img)          // fixes rotated pages
                            .Denoise()            // reduces speckles
                            .RemoveBackground()   // clears colored backgrounds
};
```

### 為何這些設定很重要

- **`MaxDegreeOfParallelism`**：過多的 OCR 執行緒會飽和 CPU，尤其在一般工作站上。三個執行緒對大多數四核心筆記型電腦而言是較佳的平衡點。  
- **`Preprocess` 管線**：三個過濾器共同顯著提升 OCR 正確率。校正傾斜解決常見的「掃描傾斜」問題，去噪除去隨機雜訊，去背則確保引擎只看到黑白文字。  
- **`SaveFormat.SearchablePdf`**：此設定會產生符合 PDF/A‑2b 標準的檔案，既適合長期保存，也具備搜尋功能，符合多數合規需求。

---

## 步驟 3 – 執行批次並觀察魔法

執行批次只需要呼叫 `Process()`。此方法會阻塞直至所有檔案處理完畢，然後返回。若需要進度回報，可掛接 `ProgressChanged` 事件（此處未示範）。

```csharp
// Start processing – this will walk through every file in InputFolder
ocrBatch.Process();

// Let the user (or calling script) know we’re finished
Console.WriteLine("All files processed. Searchable PDFs are ready.");
```

當主控台印出最後一行訊息時，你會在 `C:\Scans\Processed` 中找到每個輸入影像對應的可搜尋 PDF。用 Adobe Reader 開啟任一檔案，按 **Ctrl+F**，即可搜尋剛才從掃描中抽出的文字。

---

## 步驟 4 – 完整可執行程式（直接複製貼上）

以下是 **完整、獨立** 的程式碼，你可以直接放入新建的主控台專案（`dotnet new console`）。先確定已加入 Aspose.OCR NuGet 套件（`dotnet add package Aspose.OCR`）。

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

namespace CreateSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Activate trial mode (replace with real license for production)
            OcrEngine.EnableTrialMode();

            // 2️⃣ Configure batch OCR processing
            var ocrBatch = new OcrBatchProcessor
            {
                InputFolder = @"C:\Scans\Incoming",   // 👉 change to your source folder
                OutputFolder = @"C:\Scans\Processed", // 👉 change to your target folder
                OutputFormat = SaveFormat.SearchablePdf,
                MaxDegreeOfParallelism = 3,
                Preprocess = img => ImageFilters
                                        .Deskew(img)          // fixes rotated pages
                                        .Denoise()            // cleans up noise
                                        .RemoveBackground()   // strips colored backgrounds
            };

            // 3️⃣ Run the batch
            ocrBatch.Process();

            // 4️⃣ Notify completion
            Console.WriteLine("All files processed. Searchable PDFs are ready.");
        }
    }
}
```

### 預期輸出

```
All files processed. Searchable PDFs are ready.
```

執行完畢後，前往 `C:\Scans\Processed` 會看到一組 `.pdf` 檔案——每個都是可搜尋且符合 PDF/A‑2b 標準。打開任一檔案，輸入原始掃描中確實出現的字詞，即可看到文字被高亮顯示。

---

## 常見問題與邊緣案例處理

### 若來源資料夾已經有 PDF 呢？

Aspose OCR 能直接接受 PDF；它會將每頁光柵化，套用相同的 **前置處理** 過濾器，並嵌入 OCR 層。無需額外程式碼。

### 如何改成輸出普通 PDF（非可搜尋）？

將 `SaveFormat.SearchablePdf` 改為 `SaveFormat.Pdf`。如此會失去文字搜尋層，但視覺保真度不變。

### 我的掃描是彩色的——去背會不會影響顏色？

`RemoveBackground()` 只會移除非白色背景，同時保留主要文字。若需保留彩色圖形，可省略此過濾器：

```csharp
.Preprocess = img => ImageFilters.Deskew(img).Denoise()
```

### 伺服器記憶體有限——可以降低執行緒數量嗎？

當然可以。將 `MaxDegreeOfParallelism` 設為 `1` 或 `2`。批次處理時間會變長，但記憶體使用量會降低。

---

## 視覺摘要（可選）

如果你喜歡快速的圖示，想像以下流程圖：

![建立可搜尋 PDF 工作流程 – 顯示輸入資料夾 → 前置處理 → OCR → 可搜尋 PDF 輸出](/images/ocr-workflow.png)

*圖片替代文字：* **建立可搜尋 PDF 工作流程圖** – 示意批次 OCR 處理、轉換與校正傾斜步驟。

---

## 結論

現在你擁有一個 **完整、可投入生產環境** 的解決方案，能夠 **建立可搜尋 PDF** 檔案，無論是批次掃描影像還是 PDF。透過 **批次 OCR 處理**，你可以 **將影像轉換為 PDF**、**為 OCR 前置處理影像**，並自動 **校正掃描文件的傾斜**——只需幾行 C# 程式碼。

接下來的步驟是什麼？試著加入自訂命名規則、接上日誌框架以捕捉 OCR 信心分數，或是實驗其他 `ImageFilters`（如 `Sharpen()`）以提升淡文字的辨識度。Aspose OCR API 足夠彈性，能隨你的需求成長。

祝開發順利，願你的 PDF 永遠可搜尋！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}