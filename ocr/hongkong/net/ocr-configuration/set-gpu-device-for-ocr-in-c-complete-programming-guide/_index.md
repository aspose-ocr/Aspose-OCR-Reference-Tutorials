---
category: general
date: 2026-03-18
description: 在 Aspose OCR 中設定 GPU 裝置，以快速從圖像中提取文字。學習如何載入圖像進行 OCR，辨識收據圖像並獲得準確結果。
draft: false
keywords:
- set GPU device
- extract text from image
- how to extract text
- load image for OCR
- recognize receipt image
language: zh-hant
og_description: 在 Aspose OCR 中設定 GPU 裝置，以快速從圖像提取文字。請依照此步驟指南載入圖像進行 OCR，並辨識收據圖像。
og_title: 在 C# 中設定 OCR 的 GPU 裝置 – 完整程式設計指南
tags:
- OCR
- C#
- GPU
- Aspose
title: 在 C# 中設定 OCR 的 GPU 裝置 – 完整程式設計指南
url: /zh-hant/net/ocr-configuration/set-gpu-device-for-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 設定 GPU 裝置以進行 C# OCR – 完整程式開發指南

需要 **設定 GPU 裝置** 以加速 OCR 處理嗎？本指南將一步步說明如何使用 Aspose OCR 設定 GPU 裝置，然後只用幾行程式碼即可從收據影像中擷取文字。

如果你曾經為 **載入影像以進行 OCR** 而苦惱，或想知道 *如何從高解析度掃描檔中擷取文字*，這裡正是你的最佳去處。完成後，你將擁有一個可執行的程式，能辨識收據影像、印出純文字，且在沒有 GPU 時會優雅地回退至 CPU。

## 本教學涵蓋內容

我們將說明你需要知道的一切：

* 安裝 Aspose OCR NuGet 套件（唯一的外部相依性）。  
* 設定 GPU 裝置（`set GPU device`）並可選擇不同的 GPU 索引。  
* 載入影像檔以進行 OCR —— 是的，這包括讓許多新手卡關的「載入影像以進行 OCR」步驟。  
* 執行辨識引擎以 **辨識收據影像** 內容。  
* 取得結果字串，讓你可以 **從影像中擷取文字** 並在應用程式中使用。  

沒有魔法，沒有隱藏的文件連結 —— 只是一個完整、獨立的解決方案，你可以直接複製貼上到 Visual Studio 並立即執行。

## 前置條件

* .NET 6.0 或更新版本（此程式碼同樣適用於 .NET Core 與 .NET Framework）。  
* 具備 GPU 且已安裝相應驅動程式的機器 —— 否則函式庫會自動切換至 CPU 模式。  
* 一張範例收據影像（例如 `receipt_highres.png`），放在可使用完整路徑參照的位置。  

就這些。如果缺少 NuGet 套件，請在專案資料夾執行 `dotnet add package Aspose.OCR`。

---

## 步驟 1 – 在 Aspose OCR 中設定 GPU 裝置

首先必須在 OCR 引擎上 **設定 GPU 裝置**。這會告訴 Aspose 將繁重的運算交給顯示卡，而非 CPU。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        var ocrEngine = new OcrEngine();

        // Enable GPU processing – this is where we set the GPU device
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu;

        // (Optional) Choose a specific GPU if you have more than one.
        // The default is device 0, but you can set it to 1, 2, etc.
        ocrEngine.Settings.GpuDeviceId = 0;
```

**為什麼這很重要：**  
當引擎以 `ProcessingMode.Gpu` 執行時，底層的 CUDA 核心會大幅加速字元分割與神經網路推論。在現代 RTX 3080 上，你會看到 OCR 時間從數秒下降到次秒等級，尤其是高解析度的收據。

> **小技巧：** 若不確定要使用哪個 GPU 索引，可呼叫 `OcrEngine.GetAvailableGpuDevices()`（較新版本提供）並挑選記憶體最充足的那一個。

---

## 步驟 2 – 載入影像以進行 OCR

引擎設定完成後，我們需要 **載入影像以進行 OCR**。Aspose 提供便利的 `ImageStream` 包裝類別，可抽象化檔案 I/O，並支援來自記憶體、網路或磁碟的串流。

```csharp
        // Load the receipt image you want to recognize
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        var imageStream = ImageStream.FromFile(imagePath);
```

**可能會發生什麼問題？**  
如果檔案路徑錯誤或影像損毀，`FromFile` 會拋出 `FileNotFoundException`。在建立串流前先執行 `File.Exists(imagePath)` 檢查，可避免程式當機。

---

## 步驟 3 – 辨識收據影像

取得影像後，我們呼叫 `Recognize`。這一步會 **辨識收據影像** 內容，使用先前設定好的 GPU 加速管線。

```csharp
        // Perform OCR – this returns an OcrResult object
        var ocrResult = ocrEngine.Recognize(imageStream);
```

**背後運作原理：**  
引擎先將影像轉換為正規化的灰階位圖，接著執行深度學習模型以預測字元機率。因為在 GPU 上執行，模型會平行處理整張位圖，這就是大型收據能快速完成的原因。

---

## 步驟 4 – 從影像中擷取文字並驗證輸出

最後，我們從 `OcrResult` 取出純文字結果，寫入主控台。此時你已 **從影像中擷取文字**，可將其傳遞給後續的邏輯（例如解析項目明細）。

```csharp
        // Output the recognized plain text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

**預期輸出：**  

```
=== OCR Result ===
Store Name
Date: 03/15/2026
Item A   $12.99
Item B   $5.49
Total    $18.48
==================
```

如果文字看起來亂碼，請再次確認影像為高解析度且 GPU 驅動程式已更新。你也可以切換 `ocrEngine.Settings.PreprocessMode` 以提升暗光收據的對比度。

---

## 步驟 5 – 回退至 CPU（邊緣案例處理）

如果目標機器沒有相容的 GPU，該怎麼辦？不要讓程式崩潰，你可以偵測此情況並切換至 CPU 處理。

```csharp
        // Detect GPU availability – fallback if needed
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, falling back to CPU mode.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }
```

**為什麼要加入這段？**  
在 CI 流程或雲端容器中，常常只有無頭伺服器而沒有 GPU。優雅的降級機制確保相同程式碼在任何環境都能執行。

---

## 常見問題與實用技巧

| 常見問題 | 避免方式 |
|---------|----------|
| 忘記在載入影像前設定 `ProcessingMode`。 | 永遠先在 Step 1 完成引擎設定。 |
| 使用錯誤的 GPU 索引 (`GpuDeviceId`)。 | 查詢可用裝置或直接使用預設 `0`。 |
| 載入低解析度影像，導致 OCR 準確度下降。 | 收據建議至少 300 DPI。 |
| 未釋放 `ImageStream`，造成檔案被鎖定。 | 使用 `using` 區塊或手動呼叫 `Dispose()`。 |
| 忽略 `IsGpuAvailable` 標誌，導致在沒有 CUDA 的機器上失敗。 | 加入 Step 5 的回退邏輯。 |

---

## 完整可執行範例（直接複製貼上）

以下是完整程式碼，已備妥可編譯。存為 `Program.cs`，加入 Aspose OCR NuGet 套件後執行。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // ---------- Step 1: Set GPU device ----------
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu; // set GPU device
        ocrEngine.Settings.GpuDeviceId = 0; // use the first GPU (change if needed)

        // Optional: fallback if GPU isn't present
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, switching to CPU.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }

        // ---------- Step 2: Load image for OCR ----------
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }
        var imageStream = ImageStream.FromFile(imagePath);

        // ---------- Step 3: Recognize receipt image ----------
        var ocrResult = ocrEngine.Recognize(imageStream);

        // ---------- Step 4: Extract text from image ----------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

執行程式後，會在主控台印出先前示範的收據文字。接著你可以把這段字串傳給解析器、資料庫，或任何其他商業邏輯。

---

## 結論

我們示範了如何在 Aspose OCR 中 **設定 GPU 裝置**、**載入影像以進行 OCR**，以及 **辨識收據影像**，讓你能以閃電般的速度 **從影像中擷取文字**。完整、可執行的範例同時說明了「如何做」與「為什麼這樣做」，為任何需要 GPU 加速的 C# OCR 專案奠定堅實基礎。

準備好進一步探索了嗎？可以嘗試以下方向：

* 使用 `Parallel.ForEach` 同時處理多張影像。  
* 微調 `ocrEngine.Settings.PreprocessMode` 以改善低對比度掃描的結果。  
* 將 OCR 輸出匯出為 JSON，供下游分析使用。  

如有任何問題，歡迎留言討論，祝開發順利！

![顯示如何為 OCR 處理設定 GPU 裝置的圖示](set-gpu-device.png "設定 GPU 裝置")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}