---
category: general
date: 2026-04-01
description: 學習如何透過設定 GPU 裝置 ID 並啟用 GPU 加速，在 Aspose OCR 中快速辨識 PNG 檔案的文字。一步一步的 C# 指南。
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: zh-hant
og_description: 透過設定 GPU 裝置 ID，快速辨識 PNG 檔案中的文字。請參考此完整的 C# 指南，啟用 Aspose OCR 的 GPU 加速功能。
og_title: 從 PNG 識別文字 – GPU 加速的 Aspose OCR 教程
tags:
- C#
- OCR
- GPU
- Aspose
title: 使用 Aspose OCR 從 PNG 辨識文字 – GPU 加速批次示範
url: /zh-hant/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 PNG 識別文字 – 完整 C# GPU 加速批次教學

有沒有曾經需要 **recognize text from png** 圖片，但發現過程非常慢？你並不孤單。大多數開發者會先使用簡單的 OCR 呼叫，然後在資料夾裡有數十張截圖時，看到控制台的執行速度像蝸牛般緩慢。  

好消息是？Aspose OCR 可以將繁重的工作交給顯示卡處理，只需幾行程式碼就能 **set gpu device id** 以選擇你想要的 GPU。在本指南中，我們將逐步示範一個完整且可執行的範例，從資料夾中抓取所有 PNG，啟用 GPU 加速，選擇第一個 GPU，並列印每個檔案的字元數。  

完成後，你將擁有一個可自行運行的程式，能直接放入任何 .NET 專案，並且了解為何啟用 GPU 很重要、如何處理邊緣案例，以及如何調整以獲得更佳效能。

## 需要的環境

- **.NET 6.0** 或更新版本（程式碼亦可在 .NET Core 上編譯）。  
- **Aspose.OCR** NuGet 套件 – 使用 `dotnet add package Aspose.OCR` 安裝。  
- 一台具備 CUDA 相容 GPU（通常為 NVIDIA）且已安裝相應驅動程式的機器。  
- 一個包含欲處理的 **PNG** 圖片的資料夾。  

如果上述任一項目聽起來陌生，別慌。以下步驟提供你所需的完整指令，我們也會說明在沒有 GPU 時該怎麼辦。

## 步驟 1：初始化 OCR 引擎並啟用 GPU 加速  

首先，你需要建立一個 `OcrEngine` 實例，並開啟 GPU 支援。此旗標會告訴 Aspose 在底層使用原生 CUDA 函式庫。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**為何重要：** 若未設定 `UseGpuAcceleration`，每張圖片都會在 CPU 上處理，速度會慢上數個等級，尤其是高解析度的 PNG。啟用此旗標同時讓引擎能在之後接受特定的 GPU 裝置。

## 步驟 2：設定 GPU 裝置 ID（可選但建議）  

如果你的工作站有多於一張 GPU，你可以自行決定使用哪一張。裝置 ID 從 **0** 開始，因此 `0` 代表第一張 GPU，`1` 代表第二張，以此類推。

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**小技巧：** 在共享伺服器上執行時，明確設定 GPU 裝置 ID 可避免你的工作搶佔其他程序的資源。若省略此行，Aspose 會自動選擇預設裝置，對於單一 GPU 的環境通常已足夠。

## 步驟 3：從批次資料夾收集所有 PNG 檔案  

接下來，我們需要找出所有要進行 OCR 的 PNG。`Directory.GetFiles` 方法會完成這項繁重工作。

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**邊緣案例：** 若資料夾為空，`imageFiles` 會是一個空陣列。我們稍後會以友善訊息處理此情況。

## 步驟 4：處理每張圖片並輸出辨識出的字元數  

現在進入核心迴圈。對每張 PNG 呼叫 `Recognize`，然後列印檔名與擷取文字的長度。

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**你會看到的結果：**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

如果圖片中沒有文字，計數會是 `0`。對於純圖形的截圖而言，這是完全正常的。

## 步驟 5：執行程式並驗證 GPU 使用情況  

編譯檔案（`dotnet build`）並執行（`dotnet run`）。當控制台滾動時，你可以開啟 GPU 監控工具（例如 NVIDIA Smi）查看每張圖片時 GPU 使用率的短暫峰值。若未看到任何活動，請再次確認以下項目：

1. 已安裝 CUDA 驅動程式。  
2. `UseGpuAcceleration` 已設定為 `true`。  
3. 正確的 `GpuDeviceId` 對應到實體 GPU。  

若 GPU 不可用，Aspose 會自動回退至 CPU，但你將失去速度上的優勢。

## 常見變化與技巧  

| Situation | What to Change |
|-----------|----------------|
| **不同的影像格式**（例如 JPEG） | 將搜尋模式改為 `*.jpg` 或 `*.*`，Aspose 仍會辨識文字。 |
| **批次規模龐大**（數千檔案） | 分批處理以避免記憶體壓力：將 `imageFiles` 分割成較小的陣列。 |
| **需要實際文字，而非僅字元長度** | 在 `WriteLine` 中將 `ocrResult.Text.Length` 替換為 `ocrResult.Text`。 |
| **在無頭伺服器上執行** | 確保伺服器已安裝 GPU 驅動程式；否則將 `UseGpuAcceleration = false`，以避免不必要的錯誤。 |
| **多張 GPU，想要平衡負載** | 在 `foreach` 內使用 `ocrEngine.GpuDeviceId = i % gpuCount` 迴圈，以輪替裝置。 |

## 預期輸出與驗證  

當一切正常時，控制台會列印每個檔名及其字元數，如前所示。若要再次確認實際的 OCR 輸出，你可以暫時將文字輸出：

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

請記得在大量批次時移除或註解掉該行；印出上千行會淹沒你的終端機。

## 完整可執行範例（直接複製貼上）

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

將此檔案儲存為 `GpuBatchDemo.cs`，執行 `dotnet add package Aspose.OCR`，再執行 `dotnet run`。得益於 GPU 加速，你應該會看到每個 PNG 的字元數幾乎即時顯示。

## 結論  

現在你已了解如何透過啟用 GPU 加速並在 Aspose OCR 中明確 **set gpu device id**，有效地 **recognize text from png** 檔案。這個完整的複製貼上程式會處理資料夾搜尋、邊緣案例檢查，並即時回饋 OCR 效能。  

下一步？若需要非阻塞處理，可將 `Recognize` 呼叫改為 `ocrEngine.RecognizeAsync`，或嘗試 Aspose 提供的不同影像前處理選項（例如二值化）。你也可以將 OCR 結果導入資料庫或搜尋索引，建構全文搜尋解決方案。  

對於處理多頁 PDF 有疑問，或想比較 Aspose OCR 與 Tesseract 的差異嗎？歡迎留言或探索我們其他的教學，如 **batch OCR C#**、**OCR performance tips** 與 **GPU‑driven image processing**。祝開發愉快！  

![顯示 PNG 檔案辨識字元數的主控台輸出 – 使用 GPU 加速辨識文字](image-placeholder.png "recognize text from png 輸出範例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}