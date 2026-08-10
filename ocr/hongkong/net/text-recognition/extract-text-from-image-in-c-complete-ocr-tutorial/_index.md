---
category: general
date: 2026-05-06
description: 使用支援 GPU 的 Aspose OCR 從圖像提取文字。了解如何在 C# OCR 教學中快速提取文字，內容涵蓋設定、程式碼與最佳實踐。
draft: false
keywords:
- extract text from image
- how to extract text
- c# ocr tutorial
- Aspose OCR GPU
- C# image processing
language: zh-hant
og_description: 使用 Aspose OCR 於 C# 從圖像提取文字。本指南展示如何利用 GPU 加速快速提取文字，並一步步說明提取文字的方法。
og_title: 在 C# 中從圖像提取文字 – 完整 OCR 教學
tags:
- OCR
- C#
- Aspose
title: 在 C# 中從圖片提取文字 – 完整 OCR 教學
url: /zh-hant/net/text-recognition/extract-text-from-image-in-c-complete-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字 (C#) – 完整 OCR 教程

曾經需要 **從圖像中提取文字**，卻不確定哪個函式庫能同時兼顧速度與準確度嗎？你並不孤單——許多開發者在建構文件數位化流程時都會碰到這道牆。好消息是：使用 Aspose OCR，你幾乎可以從任何點陣圖中抽取文字，且只需幾行程式碼，即可在背景啟用 GPU 加速。

在本 **C# OCR 教程** 中，我們將一步步說明所有必備知識：從安裝 NuGet 套件、設定 GPU 模式，到處理多頁 TIFF。完成後，你將能自信地回答「如何提取文字」的問題，並擁有一個可直接放入任何 .NET 專案的完整範例。

## 你將學到

- 使用 Aspose OCR **如何從圖像檔案提取文字** 的完整步驟。  
- 如何啟用 GPU 加速以獲得巨大的效能提升。  
- 常見陷阱（例如缺少 CUDA 驅動程式）與快速解決方法。  
- 如何將解決方案擴充為批次處理或支援不同圖像格式。

> **專業提示：** 若開發機沒有專屬 GPU，仍可在 CPU 模式下執行程式碼——只要將 `UseGpu = false` 即可。其餘教學內容保持不變。

## 前置條件

在開始之前，請確保你具備以下條件：

| 前置條件 | 為什麼重要 |
|----------|------------|
| .NET 6.0 或更新版本（或 .NET Framework 4.7.2 以上） | Aspose OCR 針對現代執行環境設計。 |
| Visual Studio 2022（或你慣用的任何 IDE） | 方便除錯與 NuGet 整合。 |
| NVIDIA GPU 並支援 CUDA 11+（可選，但建議） | `UseGpu = true` 設定所需。 |
| Aspose.OCR NuGet 套件（`Aspose.OCR` 與 `Aspose.OCR.Gpu`） | 提供 OCR 引擎與 GPU 支援。 |

若缺少上述任一項目，編譯或執行時會出現錯誤或例外——別慌，教學會說明如何補救。

## 步驟 1：安裝 Aspose OCR 套件

在終端機中切換到專案資料夾，執行：

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

這兩個套件提供核心 OCR 功能以及可選的 GPU 加速層。安裝完成後，你會在 `.csproj` 中看到相應的組件參考。

## 步驟 2：設定 OCR GPU 參數

接著建立 `OcrEngineSettings` 物件，告訴引擎使用 GPU。這就是 **從圖像中提取文字** 能獲得效能提升的關鍵所在。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Required for GPU acceleration

// Configure OCR to run on the first available GPU (device ID 0)
var ocrSettings = new OcrEngineSettings
{
    UseGpu = true,          // Turn on GPU acceleration
    GpuDeviceId = 0         // Optional: specify which GPU to use
};
```

> **為什麼重要：** 啟用 GPU 後，繁重的工作（像素前處理、神經網路推論）會從 CPU 轉移到顯示卡，處理時間常能從秒級縮減至毫秒級。

若沒有相容的 GPU，只需將 `UseGpu = false`，引擎會自動回退到 CPU 模式，程式碼不需其他變更。

## 步驟 3：初始化 OCR 引擎

設定完成後，實例化 `OcrEngine`。此物件會保存設定，並可在處理多張圖像時重複使用。

```csharp
// Create the OCR engine with the previously defined settings
var ocrEngine = new OcrEngine(ocrSettings);
```

你可能會好奇為什麼要把設定與引擎分開。答案在於彈性——只要替換 `ocrSettings`，就能在同一個 `ocrEngine` 實例中即時切換 GPU 與 CPU，適用於多檔案處理。

## 步驟 4：辨識圖像中的文字

以下是 **如何提取文字** 的核心流程。我們呼叫 `RecognizeImage`，並傳入欲分析的檔案路徑。此方法會回傳包含抽取字串與信心分數的 `OcrResult`。

```csharp
// Replace with the actual path to your image file
string imagePath = @"C:\Images\sample_multi_page.tif";

// Perform OCR – this will extract text from the image
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);
```

> **邊緣情況：** 若圖像為多頁 TIFF，Aspose OCR 會自動逐頁處理並將結果串接。若需要每頁的輸出，可檢查 `ocrResult.PageResults`。

## 步驟 5：顯示或儲存抽取的文字

最後，將結果輸出到主控台、寫入檔案，或傳給其他系統。本教學僅示範直接印出。

```csharp
// Show the extracted text in the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

執行程式後，你應該會看到類似以下的輸出：

```
=== OCR Output ===
Invoice #12345
Date: 04/30/2026
Total: $1,250.00
...
```

這就是成功使用 Aspose OCR **從圖像中提取文字** 的時刻。

## 完整範例程式

以下是一個完整、可直接執行的主控台應用程式，將所有步驟整合在一起。將它貼到新的 `Program.cs`，然後按 **F5** 執行。

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Required for GPU acceleration

namespace ExtractTextFromImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure OCR settings (GPU enabled)
            var ocrSettings = new OcrEngineSettings
            {
                UseGpu = true,          // Turn on GPU acceleration
                GpuDeviceId = 0         // Optional: specify which GPU to use
            };

            // 2️⃣ Initialize the OCR engine with those settings
            var ocrEngine = new OcrEngine(ocrSettings);

            // 3️⃣ Path to the image you want to process
            string imagePath = @"YOUR_DIRECTORY\sample_multi_page.tif";

            // 4️⃣ Perform OCR – this extracts the text
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Output the result
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### 預期輸出

對清晰的列印發票執行時，程式會產生發票欄位的純文字表示。若圖像模糊或語言不受支援，`ocrResult.Text` 可能會出現亂碼——此時可調整圖像前處理（例如二值化）或改用其他語言模型以提升準確度。

## 常見問題與除錯

**Q: 我的應用程式拋出 “CUDA driver not found”。**  
A: 確認已安裝 CUDA 11+，且 GPU 驅動版本與 CUDA 相符。也可以在命令提示字元執行 `nvidia-smi` 以確認驅動是否被偵測到。

**Q: 如何一次處理整個資料夾的圖像？**  
A: 將 `RecognizeImage` 包在 `foreach (var file in Directory.GetFiles(folder, "*.tif"))` 迴圈中。記得重複使用同一個 `ocrEngine` 實例以提升效能。

**Q: 能否直接從 PDF 提取文字？**  
A: Aspose OCR 本身不支援 PDF，但可以先使用 Aspose.PDF（或其他函式庫）將 PDF 頁面轉為圖像，再交給 OCR 處理。

**Q: 若要提取非英文語言的文字該怎麼做？**  
A: 在呼叫 `RecognizeImage` 前設定 `ocrEngine.Language = OcrLanguage.Spanish`（或任何支援的語言）。

## 教程延伸

- **批次處理：** 結合 `Parallel.ForEach`，在沒有 GPU 時利用多核心平行處理。  
- **後處理：** 使用正規表達式清理電話號碼、日期或金額等資訊。  
- **整合應用：** 將抽取的字串寫入資料庫或 Azure Cognitive Search 索引，實現可搜尋的文件。

## 結論

現在你已掌握一套完整的 **C# OCR 教程**，清楚說明 **如何從圖像中提取文字**、如何利用 GPU 加速，以及如何優雅地處理多頁檔案。依照上述步驟，你可以將 Aspose OCR 輕鬆整合至任何 .NET 專案，快速將圖片轉換為可搜尋、可編輯的文字。

準備好迎接下一個挑戰了嗎？試著關閉 GPU 旗標，觀察效能差異，或改用 PNG、JPEG 等不同圖像格式。可能性無限——祝程式開發愉快！

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}