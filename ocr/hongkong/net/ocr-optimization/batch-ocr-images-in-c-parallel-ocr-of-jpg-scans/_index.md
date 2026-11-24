---
category: general
date: 2026-04-29
description: 使用 Aspose OCR 於 C# 快速批次 OCR 圖像。了解如何從 jpg 檔案提取文字、從掃描件讀取文字，並平行處理圖像清單。
draft: false
keywords:
- batch OCR images
- extract text from jpg
- read text from scans
- parallel OCR processing
- process image list
language: zh-hant
og_description: 使用 Aspose OCR 快速批次文字辨識圖像。本指南示範如何從 jpg 提取文字、從掃描件讀取文字，以及平行處理圖像清單。
og_title: 在 C# 中批量 OCR 圖片 – JPG 掃描的並行 OCR
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 在 C# 中批次 OCR 圖像 – JPG 掃描的並行 OCR
url: /zh-hant/net/ocr-optimization/batch-ocr-images-in-c-parallel-ocr-of-jpg-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 批次 OCR 圖像（C#） – JPG 掃描的平行 OCR

有沒有需要 **批次 OCR 圖像**，卻不知該如何在多個檔案間擴展工作？你並不孤單——開發者在逐一讀取掃描檔文字時常會卡住。好消息是，使用 Aspose OCR 只要幾行 C# 程式碼，就能 **從 jpg 檔提取文字**、**從掃描件讀取文字**，以及 **平行處理影像清單**。

本教學將逐步說明一個完整、可直接執行的範例，展示如何做到這點。完成後，你將擁有一個自包含的主控台應用程式，能辨識資料夾內的 JPEG 掃描檔、印出每頁文字，並告訴你每個操作花了多久。無需外部文件、無半成品程式碼——只要把完整解決方案貼到 Visual Studio 即可執行。

## 需要的環境

- **.NET 6.0** 或更新版本（程式碼亦可在 .NET Framework 4.6+ 上編譯）
- **Aspose.OCR** NuGet 套件（`Install-Package Aspose.OCR`）
- 幾張想要處理的 JPG 或掃描影像檔
- 任意你喜歡的 IDE；我使用 Visual Studio 2022，VS Code 也同樣適用

就這麼簡單。只要已安裝 NuGet 套件，即可開始。

## 第一步 – 初始化 OCR 引擎（Batch OCR Images Setup）

首先建立 `OcrEngine` 實例，並告訴它要辨識的語言。大多數情況下英文已足夠，你也可以把 `OcrLanguage.English` 換成任何支援的語言。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine and set the language to English
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };
```

*為什麼這很重要：* 只初始化一次引擎並在所有影像間重複使用，遠比每個檔案都建立新實例來得有效率。這也讓 Aspose 能共享內部資源，對 **平行 OCR 處理** 至關重要。

## 第二步 – 建立影像清單（Process Image List）

接著定義要送入批次辨識的檔案路徑集合。你可以使用 `Directory.GetFiles` 動態產生清單，但為了說明清晰，我們直接硬寫幾筆路徑。

```csharp
        // Step 2: Define the image files that will be processed
        var imagePaths = new List<string>
        {
            @"YOUR_DIRECTORY/page1.jpg",
            @"YOUR_DIRECTORY/page2.jpg",
            @"YOUR_DIRECTORY/page3.jpg"
        };
```

*小技巧：* 若有成千上萬的掃描檔，建議改用 `Directory.EnumerateFiles` 搭配 `*.jpg` 篩選，避免一次將全部清單載入記憶體。

## 第三步 – 執行批次辨識（Parallel OCR Processing）

現在進入核心：呼叫 `BatchRecognize`。此方法接受 `maxDegreeOfParallelism` 參數，決定 Aspose 會啟動多少執行緒。預設使用四條執行緒，若 CPU 核心更多，可自行提升。

```csharp
        // Step 3: Run batch recognition (4 parallel threads by default)
        var recognitionResults = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);
```

*底層在做什麼？* Aspose 會把 `imagePaths` 集合切割成多個區塊，分別交給不同執行緒處理，最後再彙總結果。這是 **從 jpg 檔提取文字** 時，對 **process image list** 進行同時處理的最佳方式。

## 第四步 – 顯示結果（Read Text from Scans）

最後，我們遍歷 `recognitionResults` 集合，印出每個檔案的文字與處理時間。`OcrResult` 物件同時提供來源檔名，方便你記錄或儲存輸出。

```csharp
        // Step 4: Output the results for each image
        foreach (var result in recognitionResults)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

**預期輸出（範例）：**

```
File: C:\Scans\page1.jpg
Time: 1.34s
The quick brown fox jumps over the lazy dog.
----------------------------------------
File: C:\Scans\page2.jpg
Time: 1.27s
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----------------------------------------
File: C:\Scans\page3.jpg
Time: 1.41s
Invoice #12345
Total: $1,250.00
----------------------------------------
```

可以看到每個區塊都會顯示檔名、OCR 所花時間，以及擷取出的文字。這正是 **從掃描件讀取文字** 時在生產流程中所需的全部資訊。

## 常見邊緣情況處理

| 情境 | 需注意的地方 | 快速解決方案 |
|-----------|-------------------|-----------|
| **檔案遺失** | `BatchRecognize` 內拋出 `FileNotFoundException` | 在加入 `imagePaths` 前先以 `File.Exists` 驗證路徑。 |
| **不支援的格式** | Aspose 只處理點陣圖（JPG、PNG、BMP、TIFF）。 | 先將 PDF 轉成影像（使用 Aspose.PDF）或直接跳過這些檔案。 |
| **記憶體壓力** | 大尺寸影像在多執行緒下會耗盡 RAM。 | 降低 `maxDegreeOfParallelism`，或在 OCR 前先縮小影像。 |
| **非英文文字** | 語言設定為英文會遺漏其他文字。 | 改為 `Language = OcrLanguage.French`（或多語言組合）。 |

以上技巧可讓你的批次作業更穩健，特別是當 **processing an image list** 來源為使用者上傳或掃描檔案庫時。

## 專業小技巧 – 調校平行度

在 8 核心機器上執行時，可將平行度提升至 6 或 8，速度會顯著提升。但請記得，每條執行緒也會為位圖佔用記憶體。以下是一個簡易的參考原則：

```csharp
int cores = Environment.ProcessorCount;
int maxThreads = Math.Max(1, cores - 1); // leave one core free for UI/OS
```

將 `maxThreads` 帶入 `BatchRecognize`，即可實現依機器自動調整的配置。

## 完整可執行範例（直接複製貼上）

以下程式碼即為完整程式，直接編譯即可。只要把 `YOUR_DIRECTORY` 替換成存放 JPG 掃描檔的路徑即可。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine – English language
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };

        // 2️⃣ Build the list of image files to process
        var imagePaths = new List<string>();
        string folder = @"C:\Scans"; // <-- change this
        foreach (var file in Directory.EnumerateFiles(folder, "*.jpg"))
        {
            imagePaths.Add(file);
        }

        if (imagePaths.Count == 0)
        {
            Console.WriteLine("No JPG files found in the specified folder.");
            return;
        }

        // 3️⃣ Run batch OCR – let the library use 4 threads (adjust as needed)
        var results = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);

        // 4️⃣ Output each result
        foreach (var result in results)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

> **注意：** `using System.IO;` 這一行是必須的，因為要使用 `Directory` 輔助工具。若未找到 JPG，程式會印出友善提示，避免靜默失敗。

## 結論

我們剛剛示範了一個簡潔的 **batch OCR images** 工作流程，能 **從 jpg 檔提取文字**、**從掃描件讀取文字**，並以 **parallel OCR processing** 高效 **process an image list**。完整、可執行的範例說明了如何初始化引擎、提供檔案集合、以及處理結果，同時控制記憶體使用與執行緒數量。

準備好進一步嘗試了嗎？可以改成法文、加入 PDF 轉影像的步驟，或把 OCR 結果寫入資料庫。模式不變：一次初始化、一次提供清單，讓 Aspose 平行完成繁重工作。

有任何問題或想分享自己的調整嗎？歡迎在下方留言，祝開發順利！

![Batch OCR images processing flow](https://example.com/placeholder.png "Diagram illustrating batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}