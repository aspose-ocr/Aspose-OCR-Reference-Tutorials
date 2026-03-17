---
category: general
date: 2026-03-17
description: 使用 Aspose OCR 在 C# 中從 PNG 提取文字。學習如何從圖像讀取文字、處理收據 OCR，並建立具 GPU 加速的 OCR
  引擎。
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: zh-hant
og_description: 使用 Aspose OCR 從 PNG 提取文字。本指南展示如何從圖像讀取文字、處理收據 OCR，以及高效建立 OCR 引擎。
og_title: 從 PNG 中提取文字 – 使用 OCR 讀取圖像文字
tags:
- OCR
- CSharp
- Aspose
title: 從 PNG 擷取文字 – 使用 OCR 讀取圖片文字
url: /zh-hant/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 PNG 提取文字 – 使用 OCR 從圖像讀取文字

是否曾需要 **從 PNG 提取文字**，卻不確定哪個函式庫能提供可靠的結果？你並不孤單——開發者常問：「如何在不自行開發神經網路的情況下，讀取收據等圖像檔案中的文字？」好消息是 Aspose OCR 已為你處理好繁重的工作，甚至可以啟用 GPU 以提升速度。

在本教學中，我們將一步步說明如何 **處理收據 OCR**，從安裝 NuGet 套件到建立能辨識 PNG 檔案的 OCR 引擎。完成後，你將擁有一個獨立的 Console 應用程式，能讀取收據圖像、印出辨識出的文字，並示範如何針對不同情境微調引擎。全程只有程式碼與清晰說明，無需外部文件。

## 前置條件

- .NET 6.0 SDK（或任何較新版本的 .NET）  
- Visual Studio 2022 或配備 C# 擴充功能的 VS Code  
- 支援的 NVIDIA GPU 以及最新驅動程式（可選，但建議使用 GPU 模式）  
- **Aspose.OCR** NuGet 套件（`dotnet add package Aspose.OCR`）  

如果沒有 GPU，也可以在 CPU 模式下執行範例——只要略過 GPU 設定的程式碼行即可。

## 步驟 1：安裝 Aspose.OCR 並建立專案

首先，建立一個新的 Console 專案，並加入 Aspose OCR 函式庫。

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

為什麼要這麼做：`Aspose.OCR` 套件內含 OCR 引擎、影像載入器，以及可選的 GPU 支援。透過 NuGet 加入可確保取得最新穩定版（截至 2026 年 3 月為 23.10）。

## 步驟 2：匯入命名空間並建立 OCR 引擎

接著開啟 **Program.cs**，加入必要的 `using` 指示詞，然後實例化引擎。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**小技巧：** 若在沒有 GPU 的機器上遇到 `System.DllNotFoundException`，只要將設定 `EngineMode` 與 `GpuDeviceId` 的兩行程式碼註解掉，引擎會自動回退至 CPU。

## 步驟 3：載入要提取文字的 PNG 影像

Aspose OCR 可以直接從檔案路徑、串流或位元組陣列讀取影像。此示範將載入本機的收據圖檔。

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

請注意我們已加入檔案不存在的防護機制。實務上，你可能會改為顯示友善的 UI 訊息，而非直接結束程式。

## 步驟 4：執行 OCR 辨識

文字提取只需一次方法呼叫。引擎會回傳 `OcrResult` 物件，內含原始字串、信心分數與版面資訊。

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

為什麼要檢查 `ocrResult.Text`：有時品質不佳的 PNG 會回傳空字串，這時比起什麼都不顯示，主動告知使用者較好。

## 步驟 5：輸出辨識結果

最後，將提取出的字串印到 Console。你也可以寫入檔案、資料庫，或傳給其他服務。

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

執行程式 (`dotnet run`) 後，預期會看到類似以下的輸出：

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

這就是 **使用 Aspose OCR 從 PNG 檔案提取文字** 的完整解決方案，同時也示範了如何 **從圖像讀取文字**，即使圖檔看起來像收據。

## 可選：微調 OCR 引擎（進階）

若需要針對特定字型或雜訊背景提升準確度，可調整以下設定：

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

這些調整在批次處理 **收據 OCR** 時特別有用，因為掃描品質常常參差不齊。

## 常見問題與避免方式

| 問題 | 為何會發生 | 解決方式 |
|------|------------|----------|
| **缺少 GPU 驅動程式** | 引擎嘗試載入 CUDA 但找不到 DLL。 | 安裝最新的 NVIDIA 驅動程式，或移除 `EngineMode.Gpu` 行改用 CPU 模式。 |
| **影像路徑錯誤** | `ImageStream.FromFile` 在找不到檔案時會拋出例外。 | 如步驟 3 所示，先驗證路徑，或使用 `Path.Combine` 確保跨平台安全。 |
| **模糊收據信心低** | OCR 引擎無法辨識字元。 | 開啟 `EnableImagePreprocessing`，必要時提升影像 DPI 後再送入引擎。 |
| **長時間服務記憶體泄漏** | 每個 `OcrEngine` 會持有非受控資源。 | 使用 `using var ocrEngine = new OcrEngine();` 在使用完畢後即釋放。 |

## 完整範例（直接複製貼上）

以下是可以直接貼到 `Program.cs` 的 **完整程式碼**，其中所有可選的微調都已以註解方式保留，方便隨時啟用。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

儲存後執行 `dotnet run`，即可在 Console 中看到收據內容。

![extract text from png example](receipt.png "extract text from png example")

*上圖示範一張可供程式處理的收據 PNG 範例。*

## 重點回顧

我們說明了如何使用 Aspose OCR **從 PNG 檔案提取文字**，展示了 **從圖像讀取文字** 的方法，並完成了一條包含可選 GPU 加速的 **收據 OCR** 流程。自行 **建立 OCR 引擎** 能讓你全面掌控設定、效能與錯誤處理。

## 接下來可以探索什麼？

- **批次處理**：遍歷 PNG 收據資料夾，將每筆結果寫入 CSV 檔。  
- **結合 Azure Functions**：將此 Console 應用轉為無伺服器端點，接受圖像上傳。  
- **多語言支援**：將 `Language.English` 換成 `Language.Spanish`，或加入自訂字典。  
- **後處理**：使用正規表達式從原始 OCR 文字中抽取總金額、日期或稅號等欄位。

盡情實驗吧——只要掌握正確的調整點，OCR 就是一個相當彈性的工具。若遇到問題，歡迎在下方留言或參考 Aspose OCR API 文件深入了解。

祝開發順利，玩得開心，將那些頑固的 PNG 收據轉換成可搜尋的文字吧！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}