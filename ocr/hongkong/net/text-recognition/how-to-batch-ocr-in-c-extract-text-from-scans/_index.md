---
category: general
date: 2026-05-06
description: 學習如何在 C# 中批次執行 OCR，並使用 Aspose OCR Batch 快速從掃描檔案提取文字。跟隨完整的逐步指南，內含程式碼、技巧與邊緣案例處理。
draft: false
keywords:
- how to batch OCR
- extract text from scans
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: zh-hant
og_description: 如何在 C# 中批量 OCR？本指南將向您展示如何使用 Aspose OCR、GPU 支援及平行處理，高效地從掃描檔案中提取文字。
og_title: 如何在 C# 中批量執行 OCR – 從掃描檔提取文字
tags:
- C#
- OCR
- Aspose
title: 如何在 C# 中批次執行 OCR – 從掃描檔提取文字
url: /zh-hant/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批次 OCR – 從掃描檔提取文字

有沒有想過 **如何批次 OCR**，當你面前是一個塞滿掃描 PDF 或 JPEG 的資料夾？你並不是唯一一個盯著一堆影像，心想「一定有更快的方式把文字抽出來」的人。在本教學中，我們將一步步示範一個實用的解決方案，不僅能 **從掃描檔提取文字**，還能透過 GPU 加速與平行處理提升效能。

事實上，一次只處理一個檔案的 OCR 會耗費大量時間，尤其當你面對數十或數百頁時。閱讀完本指南後，你將擁有一個可直接執行的 C# 主控台應用程式，只要一個指令就能處理整個目錄，產生乾淨的文字檔，方便後續索引、搜尋或其他用途。

## 前置條件

在開始之前，請確認你已具備：

- **.NET 6.0 或更新版本**（程式碼使用了現代 C# 語法）。
- **Aspose.OCR 授權**（免費試用版可用於測試）。
- 若想啟用 `UseGpu`，需要 **支援 GPU 的機器**；否則程式庫會自動回退至 CPU。
- 基本的 **C# 主控台應用程式** 使用經驗。

不需要外部服務，也不需要隱藏的設定檔——只要 SDK 與一個影像資料夾即可。

## 第一步：安裝 Aspose.OCR NuGet 套件

首先，將 Aspose OCR 函式庫加入你的專案。於解決方案資料夾開啟終端機，執行：

```bash
dotnet add package Aspose.OCR
```

這會把 `Aspose.OCR` 以及其 batch 命名空間拉進來，稍後我們會用它來 **批次 OCR**。

> **小技巧：** 若你使用 Visual Studio，也可以透過 NuGet 套件管理員 UI 加入套件。

## 第二步：建立主控台應用程式骨架

先建立一個最小的主控台程式，作為批次處理器的容器。新增 `Program.cs`，貼上以下骨架程式碼：

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll configure and run the OCR batch processor here.
        }
    }
}
```

為什麼把邏輯寫在 `Main` 裡？因為主控台應用程式可以即時透過 `Console.WriteLine` 顯示訊息，方便快速驗證 **批次 OCR** 工作是否順利完成。

## 第三步：設定 OcrBatchProcessor

現在進入解決方案的核心。我們會實例化 `OcrBatchProcessor`，指向輸入資料夾、設定輸出位置，並調整幾個效能參數。

```csharp
// Step 3: Configure the OCR batch processor
var batch = new OcrBatchProcessor
{
    // Folder that contains the source images to be processed
    InputFolder = @"YOUR_DIRECTORY/Scans",

    // Folder where the OCR results will be saved
    OutputFolder = @"YOUR_DIRECTORY/OcrResults",

    // Specify the language of the documents (Spanish in this example)
    Language = OcrLanguage.Spanish,

    // Enable GPU acceleration for faster processing (if available)
    UseGpu = true,

    // Limit the number of concurrent OCR operations
    MaxDegreeOfParallelism = 4
};
```

### 為什麼這些設定很重要

| 設定 | 功能說明 | 何時可能需要調整 |
|------|----------|-------------------|
| `InputFolder` | 要處理的掃描檔所在路徑。 | 為了可移植性，可使用相對路徑。 |
| `OutputFolder` | 每張影像抽出的文字會以 `.txt` 檔儲存於此。 | 若需集中存放，可指向網路共享資料夾。 |
| `Language` | OCR 語言模型；此處以西班牙文示範多語言支援。 | 改成 `OcrLanguage.English` 或其他支援語言。 |
| `UseGpu` | 將大量矩陣計算交給 GPU 處理。 | 在沒有 GPU 的無頭伺服器上設為 `false`。 |
| `MaxDegreeOfParallelism` | 同時處理的影像數量上限。 | 在 CPU 較弱的機器上降低，以免過度佔用資源。 |

## 第四步：執行批次作業並加入錯誤處理

執行批次只要呼叫 `Execute()`，但我們會把它包在 try‑catch 區塊，讓程式在發生錯誤（例如資料夾遺失、影像格式不支援）時提供友善訊息。

```csharp
try
{
    // Step 4: Run the batch OCR operation
    batch.Execute();

    // Step 5: Inform the user that processing has finished
    Console.WriteLine("Batch completed.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
}
```

當處理器完成時，主控台會顯示 **Batch completed.**，而每個來源影像都會在 `OcrResults` 中產生對應的 `.txt` 檔。檔名與原始影像相同，方便對照。

## 第五步：驗證輸出 – 會看到什麼

程式執行完畢後，打開 `YOUR_DIRECTORY/OcrResults` 內的任意檔案，你應該會看到從對應影像抽出的純文字內容，例如：

```
Este es un documento de prueba.
Contiene varias líneas de texto.
```

如果輸出看起來亂碼，請再次確認 `Language` 是否與掃描檔的語言相符。Aspose OCR 支援超過 100 種語言，你可以把 `OcrLanguage.Spanish` 換成任何需要的語言。

## 處理邊緣案例與常見陷阱

### 1. GPU 不可用

若機器沒有相容的 GPU，`UseGpu = true` 會自動回退至 CPU 模式，但會失去加速效益。若想明確檢測 GPU 能力，可這樣寫：

```csharp
if (!OcrBatchProcessor.IsGpuSupported)
{
    batch.UseGpu = false;
    Console.WriteLine("GPU not detected – falling back to CPU processing.");
}
```

### 2. 大檔案超出記憶體

處理巨大的 TIFF 或 PDF 時，建議先將檔案切割成較小的影像。Aspose OCR 能處理多頁 PDF，但記憶體使用量會隨頁數上升。可使用 `Aspose.Imaging` 先將文件切片成可管理的區塊。

### 3. 輸入資料夾內有非影像檔案

批次處理器會自動忽略無法解析的檔案，但保持資料夾整潔仍是好習慣。你可以依副檔名過濾：

```csharp
batch.InputFolder = @"YOUR_DIRECTORY/Scans";
batch.FileFilter = file => file.EndsWith(".png", StringComparison.OrdinalIgnoreCase)
                         || file.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase);
```

*(註：`FileFilter` 為假想屬性；若實際 API 有提供，請改用正確的屬性名稱。)*

## 完整可執行範例

以下是完整、可直接複製貼上的程式碼。將 `YOUR_DIRECTORY` 替換成你機器上的絕對路徑。

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Configure the batch processor
            var batch = new OcrBatchProcessor
            {
                InputFolder = @"C:\MyScans",          // <-- change this
                OutputFolder = @"C:\OcrResults",     // <-- change this
                Language = OcrLanguage.Spanish,
                UseGpu = true,
                MaxDegreeOfParallelism = 4
            };

            // Optional: fall back to CPU if no GPU is found
            if (!OcrBatchProcessor.IsGpuSupported)
            {
                batch.UseGpu = false;
                Console.WriteLine("GPU not detected – using CPU.");
            }

            try
            {
                // Run the batch job
                batch.Execute();

                Console.WriteLine("Batch completed.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### 預期的主控台輸出

```
Batch completed.
```

在 `C:\OcrResults` 中，你會找到每張 `C:\MyScans` 影像對應的 `.txt` 檔。

## 結論

現在你已掌握在 C# 中 **批次 OCR** 以及 **從掃描檔提取文字** 的完整、可投入生產的作法，無需手動開啟每個檔案。透過 Aspose 的 batch API、GPU 加速與可調整的平行度，這個解決方案可以從少量頁面擴展到數千頁。

接下來可以嘗試以下想法：

- **整合搜尋索引**（例如 Elasticsearch），讓抽出的文字可被搜尋。
- **加入後處理**，如拼字檢查或語言偵測。
- **將主控台程式包裝成 Windows Service**，持續監控指定的投遞資料夾。

盡情實驗、調整平行度或更換語言模型吧。如果遇到任何問題，歡迎在下方留言——祝你 OCR 順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}