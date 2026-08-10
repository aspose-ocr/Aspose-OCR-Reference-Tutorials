---
category: general
date: 2026-02-14
description: 如何在 C# 中使用 OCR 快速提取 PNG 檔案的文字。學習批量 OCR 圖像、處理多張圖片，並在同一指南中使用 Aspose OCR
  C#。
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: zh-hant
og_description: 如何在 C# 中使用 Aspose OCR C# 進行 OCR。本教學示範如何從 PNG 檔案擷取文字、批量 OCR 圖像，以及高效處理多張圖像。
og_title: 如何在 C# 中使用 OCR – 批量 PNG 文字提取
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中使用 OCR – 使用 Aspose OCR 批次處理 PNG 圖像
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

Also there is a bullet list in prerequisites, we need to keep list format with hyphens.

Also bullet list in Pro Tips.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 批次處理 PNG 圖片與 Aspose OCR

有沒有想過 **如何使用 OCR** 從一堆 PNG 檔案中提取文字，而不必為每個檔案寫一個獨立的程式？你並不孤單。許多開發者在需要大規模 **extract text PNG** 資產時會卡住，尤其是當圖片放在資料夾中，必須為每個檔案啟動 OCR 引擎時。

在本指南中，我們將逐步說明一個完整、即時可執行的解決方案，該方案能 **batch OCR images**、在平行執行 **process multiple images**，並利用強大的 **Aspose OCR C#** 函式庫。完成後，你將擁有一個可讀取任意數量 PNG、提取文字並將結果輸出至主控台的單一執行檔——只需幾行程式碼。

## 前置條件

- .NET 6.0 或更新版本（此程式碼同樣適用於 .NET Core 與 .NET Framework）  
- 有效的 Aspose.OCR for .NET 授權（或免費試用版）— 可從 Aspose 官方網站取得。  
- 包含欲讀取 PNG 檔案的資料夾。  
- Visual Studio 2022（或任何相容 C# 的 IDE）。  

- 除了 `Aspose.OCR` 之外，無需其他 NuGet 套件。

## 步驟 1：如何使用 OCR – 初始化 Aspose OCR 引擎

首先，你需要建立 `Engine` 類別的實例。此物件抽象化底層的 OCR 技術，且可根據硬體與授權在 CPU 或 GPU 上執行。

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*為何重要：* 只初始化一次引擎並在多執行緒間重複使用，可節省記憶體並避免重複載入 OCR 模型的開銷，同時確保所有圖片使用一致的設定。

## 步驟 2：Extract Text PNG – 收集圖片路徑

接下來，我們需要一組檔案路徑。在實際專案中，你可能會動態讀取目錄，但為了說明清楚，我們將列出幾個範例檔案。

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*提示：* 將 `YOUR_DIRECTORY` 替換為圖片的絕對或相對路徑。若檔案數量眾多，可將手動清單改為 `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`。

## 步驟 3：Batch OCR Images – 平行執行辨識

逐一處理圖片雖然簡單卻速度緩慢。透過使用 `Parallel.ForEach`，我們可以同時 **process multiple images**，利用多核心 CPU 的效能。

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*為何使用平行？* 每次 OCR 呼叫都相當耗費 CPU，但彼此獨立，於是同時執行可大幅縮短總執行時間，特別是在四核心或更高的機器上。

## 步驟 4：Process Multiple Images – 顯示提取的文字

現在我們已擁有 `OcrResult` 物件的集合，可以遍歷它們並印出辨識出的文字。通常你會將輸出儲存至資料庫或寫入檔案，但使用主控台輸出可讓範例保持簡潔。

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**預期的主控台輸出（範例）：**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

若有任何圖片載入失敗，Aspose 會拋出例外；你可以將 `engine.Recognize` 呼叫包在 try/catch 區塊中，以記錄錯誤而不會中止整個批次。

## 步驟 5：Full Working Example – 完整範例整合

以下是完整程式碼，你可以直接複製貼上至新的 C# 主控台專案。它包含從 `using` 陳述式到最終輸出迴圈的全部內容。

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### 執行範例

1. 在 Visual Studio 中建立新的 **Console App** 專案。  
2. 加入 **Aspose.OCR** NuGet 套件 (`Install-Package Aspose.OCR`)。  
3. 將 `YOUR_DIRECTORY` 替換為存放 PNG 檔案的路徑。  
4. 建置並執行——你應該會在主控台看到提取的文字。

## 專業提示與邊緣情況

- **GPU acceleration:** 如果你有相容的 GPU 且已取得 Aspose OCR 授權，可在建立引擎前透過 `EngineSettings` 啟用。這可為每張圖片節省數秒。  
- **Large files:** 若圖片大於 10 MB，建議先縮小尺寸以減少記憶體壓力。  
- **Language support:** 預設情況下引擎使用英文。可設定 `engine.Language = Language.French;`（或任何支援的語言）以提升非英文文字的辨識準確度。  
- **Error handling:** 平行迴圈內的 `try/catch` 可確保損壞的檔案不會中止整個批次。你也可以將失敗記錄至檔案以供日後檢查。  
- **Result storage:** 若不想印出，可使用 `File.WriteAllText(Path.ChangeExtension(path, ".txt"))` 將 `result.Text` 寫入 `.txt` 檔案。

## 結論

現在你已了解如何在 C# 中 **how to use OCR** 來 **extract text PNG** 檔案、**batch OCR images**，以及使用 Aspose OCR C# 高效地 **process multiple images**。此解決方案完整自足、支援平行執行，且可輕易擴充以處理數百甚至數千個檔案，只需極少的修改。

準備好進一步了嗎？試著將主控台輸出改為 CSV 報表、實驗 GPU 加速，或將 OCR 文字輸入搜尋索引。可能性無窮，而核心模式——一次初始化、平行執行、優雅處理錯誤——將在任何影像處理流程中為你帶來效益。

祝程式開發順利，願你的 OCR 任務快速且零錯！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}