---
category: general
date: 2026-03-13
description: 如何快速且可靠地批次 OCR，同時學習使用 Aspose.OCR 從 tiff 檔案提取文字。請跟隨此逐步教學。
draft: false
keywords:
- how to batch OCR
- extract text from tiff
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: zh-hant
og_description: 學習如何在 C# 中批量執行 OCR，並使用 Aspose.OCR 從 TIFF 檔案提取文字。本指南涵蓋設定、程式碼及最佳實踐技巧。
og_title: 如何在 C# 中批次執行 OCR – 完整程式設計指南
tags:
- OCR
- C#
- Aspose
- Batch processing
title: 如何在 C# 中批次 OCR – 完整程式設計指南
url: /zh-hant/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批次 OCR – 完整程式指南

有沒有想過 **如何批次 OCR** 大量掃描的發票，而不必為每個檔案寫一個單獨的腳本？你並不是唯一有此需求的人。在許多實務專案中，痛點不是 OCR 的準確度，而是需要轉換成可搜尋文字的影像數量——通常是 TIFF——之龐大規模。  

本教學將示範如何使用 Aspose.OCR 的 `BatchProcessor` **批次 OCR**，同時教你如何在一次乾淨的執行中 **extract text from tiff**。完成後，你將擁有一個可直接執行的 Console 應用程式，能處理整個資料夾、利用可選的 GPU 加速，並在任意位置產生純文字結果。

## 您需要的條件

- **.NET 6+**（或若你偏好傳統執行環境則使用 .NET Framework 4.7.2）  
- **Aspose.OCR for .NET** – 可使用 `dotnet add package Aspose.OCR` 取得 NuGet 套件。  
- 一個存放欲讀取的 **TIFF** 影像的資料夾（教學範例使用 `Invoices`）。  
- 可選：支援 DirectX 11 或 CUDA 的 GPU，以提升處理速度。  

不需要額外服務、雲端金鑰——只要本機的 C# 專案與 Aspose 函式庫即可。

## 步驟 1：設定專案並安裝 Aspose.OCR

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** 若你在 Windows 上且計畫使用 GPU 加速，請確保已安裝最新的顯示卡驅動程式。否則 `UseGpu = true` 旗標會自動回退至 CPU。

## 步驟 2：建立 BatchProcessor 設定

現在我們要設定 `BatchProcessor`。這是 **如何批次 OCR** 的核心——你告訴 Aspose 期待的語言、要套用的前處理濾鏡，以及是否使用 GPU。

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 2: Configure the batch processor
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                // Primary language – English works for most invoices
                Language = Language.English,

                // Set to true if you have a compatible GPU; otherwise false
                UseGpu = true,

                // Optional pre‑processing to improve OCR accuracy
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),   // straightens tilted scans
                    new DespeckleFilter() // removes speckles and noise
                }
            };
```

**為什麼要這樣設定？**  
- `Language = Language.English` 告訴引擎使用英文語言模型，較通用模型更為精確。  
- `UseGpu` 在配備不錯的 GPU 上可將處理時間減半，但若是沒有 GPU 的筆記型電腦，保留 `false` 亦安全。  
- 濾鏡管線模擬人工操作：先校正頁面傾斜，再去除雜點，最後交給 OCR 引擎。

## 步驟 3：將處理器指向您的 TIFF 資料夾

接下來的 **如何批次 OCR** 步驟是告訴函式庫來源檔案的位置。支援萬用字元，可一次抓取所有 `.tif` 檔案。

```csharp
            // -------------------------------------------------
            // Step 3: Add the folder containing TIFF images
            // -------------------------------------------------
            // Replace YOUR_DIRECTORY with the actual path on your machine
            batchProcessor.AddFolder(@"C:\Data\Invoices", "*.tif");
```

> **Edge case:** 若影像同時有 `.tiff`、`.tif`、`.png` 等副檔名，可多次呼叫 `AddFolder`，或使用 `*.*` 後在程式碼中自行過濾。

## 步驟 4：選擇 OCR 結果的輸出位置

你可能會問，「擷取的文字會放在哪裡？」這是 **如何批次 OCR** 的第三個要點——定義輸出位置與格式。我們會把純文字檔與原始檔案並排存放。

```csharp
            // -------------------------------------------------
            // Step 4: Define output folder and format
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;
```

如果需要 JSON 或 XML 而非純文字，只要將 `OutputFormat.PlainText` 換成 `OutputFormat.Json` 或 `OutputFormat.Xml`。函式庫會自動完成轉換。

## 步驟 5：執行批次工作並回報結果

最後，啟動工作。`Execute` 方法會阻塞直到所有檔案處理完畢，之後即可檢查 `ProcessedCount` 以確認成功。

```csharp
            // -------------------------------------------------
            // Step 5: Execute the batch job
            // -------------------------------------------------
            batchProcessor.Execute();

            // Simple verification output
            Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
            Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
        }
    }
}
```

### 預期輸出

執行程式時，主控台會印出類似以下的訊息：

```
Batch completed. Processed files: 42
Check C:\Data\Output for .txt files containing extracted text.
```

在 `Output` 資料夾中，你會找到每個來源 TIFF 對應的 `.txt` 檔案，檔名與原始影像相同（例如 `Invoice_001.txt`）。打開任一檔案，即可看到原始 OCR 文字——非常適合匯入搜尋索引或後續資料抽取流程。

## 處理常見問題

### 1. GPU 不可用

若 `UseGpu = true` 但找不到相容裝置，Aspose 會靜默回退至 CPU。若想明確捕捉，可處理 `DeviceNotFoundException`：

```csharp
try
{
    batchProcessor.Execute();
}
catch (DeviceNotFoundException)
{
    Console.WriteLine("GPU not detected – switching to CPU mode.");
    batchProcessor.UseGpu = false;
    batchProcessor.Execute();
}
```

### 2. 同一資料夾中的非 TIFF 檔案

當資料夾內混雜其他類型檔案時，可在程式中自行過濾：

```csharp
var tiffFiles = Directory.GetFiles(@"C:\Data\Invoices", "*.*")
                         .Where(f => f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase) ||
                                     f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));

foreach (var file in tiffFiles)
    batchProcessor.AddFile(file);
```

### 3. 超過記憶體的巨型檔案

對於超大多頁 TIFF，請啟用串流模式：

```csharp
batchProcessor.EnableMemoryManagement = true; // reduces RAM footprint
```

## 提升精確度的專業技巧（當您 **extract text from tiff**）

- **解析度很重要** – 建議 300 dpi 以上。低於此值 OCR 引擎可能遺漏字元。  
- **彩色 vs. 灰階** – 在 OCR 前將彩色掃描轉為灰階；`DeskewFilter` 已在底層完成此步驟，若需更快可額外加入 `ColorDepthReductionFilter`。  
- **後處理** – 取得純文字後，可執行拼寫檢查或正規表達式清理，以修正常見 OCR 錯誤（例如 “0” 與 “O” 的混淆）。

## 完整可執行範例（直接複製貼上）

以下是完整程式碼，你只要把佔位路徑換成自己的目錄即可編譯執行。

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Configure the batch processor (how to batch OCR)
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                Language = Language.English,
                UseGpu = true, // set false if no GPU
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),
                    new DespeckleFilter()
                },
                EnableMemoryManagement = true // helps with huge TIFFs
            };

            // -------------------------------------------------
            // Add source TIFF files
            // -------------------------------------------------
            string sourceFolder = @"C:\Data\Invoices";
            batchProcessor.AddFolder(sourceFolder, "*.tif");

            // -------------------------------------------------
            // Optional: add only TIFFs if folder contains other images
            // -------------------------------------------------
            var extraTiffs = Directory.GetFiles(sourceFolder, "*.*")
                                      .Where(f => f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));
            foreach (var file in extraTiffs)
                batchProcessor.AddFile(file);

            // -------------------------------------------------
            // Define where results go
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;

            // -------------------------------------------------
            // Execute the batch job
            // -------------------------------------------------
            try
            {
                batchProcessor.Execute();
                Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
                Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
            }
            catch (DeviceNotFoundException)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
                batchProcessor.UseGpu = false;
                batchProcessor.Execute();
                Console.WriteLine($"Batch completed (CPU). Processed files: {batchProcessor.ProcessedCount}");
            }
        }
    }
}
```

編譯並執行：

```bash
dotnet run
```

現在你應該會得到一組整齊的 `.txt` 檔案——每個檔案都是透過全自動批次流程 **extracting text from tiff** 的結果。

## 結論

我們已從頭到尾示範了在 C# 中 **如何批次 OCR**，並有效率地 **extract text from tiff**。關鍵要點如下：

1. 使用 Aspose.OCR 的 `BatchProcessor`，免除自行撰寫重複迴圈。  
2. 利用前處理濾鏡（校正、去雜點）提升準確度。  
3. 有條件時啟用 GPU 加速，並保留 CPU 後備方案。  
4. 將結果存放於可預測的資料夾結構，方便下游工作自動取得。

接下來你可以探索：

- 將純文字匯入 **search index**（例如 Elasticsearch）以實現發票可搜尋。  
- 將輸出轉為 **JSON**，再餵給機器學習模型以抽取明細項目。  
- 為損毀的 TIFF 或權限問題加入 **error handling**。

試試看吧，

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}