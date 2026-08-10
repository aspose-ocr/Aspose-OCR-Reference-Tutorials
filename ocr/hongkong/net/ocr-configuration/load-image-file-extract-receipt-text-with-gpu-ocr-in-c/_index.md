---
category: general
date: 2026-02-14
description: 載入圖像檔案並使用 Aspose OCR GPU 引擎從收據中擷取文字。了解如何設定最大 GPU 記憶體、配置 GPU 記憶體，並高效執行圖像
  OCR。
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: zh-hant
og_description: 載入圖像檔案並使用 Aspose OCR GPU 引擎從收據中提取文字。本指南說明如何設定最大 GPU 記憶體以及在 C# 中對圖像執行
  OCR。
og_title: 載入圖像檔案並使用 GPU OCR 在 C# 中提取收據文字
tags:
- C#
- OCR
- Aspose
- GPU
title: 載入圖像檔案並於 C# 中使用 GPU OCR 提取收據文字
url: /zh-hant/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 載入影像檔案並使用 GPU OCR 於 C# 中擷取收據文字

曾經需要 **load image file** 並從收據中取得精確文字，但在 OCR 步驟卡住了嗎？你並非唯一遇到這情況的人。在許多實務應用中——如費用追蹤、庫存系統，甚至簡單的收據掃描機器人——能快速讀取收據影像往往是關鍵。  

好消息是？使用 Aspose.OCR 的 GPU 加速引擎，你只需幾行簡潔的 C# 程式碼即可 **load image file**、**set max GPU memory**，以及 **run OCR on image**。以下我們將一步步說明整個流程，從 GPU 設定到列印擷取出的純文字。

## 您將學會

* **Load image file** 從磁碟載入，使用 Aspose 的 `ImageStream`。
* **Configure GPU memory** 讓引擎不會佔用超過您設定的記憶體。
* **Run OCR on image** 並擷取收據上的每個字元。
* 處理常見問題——例如記憶體不足錯誤或模糊掃描。
* 驗證輸出並調整設定以提升準確度。

不需要外部服務，也不需要隱晦的技巧——純粹的 C# 程式碼，可直接放入任何 .NET 6+ 專案。

---

## 前置條件

在開始之前，請確保您已具備：

* .NET 6 SDK 或更新版本已安裝。
* 有效的 Aspose.OCR 授權（或使用免費評估模式）。
* 已在專案中加入 `Aspose.OCR` 與 `Aspose.OCR.Gpu` NuGet 套件。
* 磁碟上已有範例收據影像（`receipt.png`）。

如果上述項目您不熟悉，請先暫停並安裝套件：

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

就這樣——不需要額外的原生函式庫，因為 GPU 支援已內建於 NuGet 套件中。

---

## 載入影像檔案並準備 GPU 引擎

第一件事是 **load image file** 到 `ImageStream`。此物件抽象化檔案系統細節，為 OCR 引擎提供乾淨的記憶體內表示。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**為何重要**：  
*Loading the image file* 透過 `ImageStream.FromFile` 可確保引擎看到完整的像素資料，保留 DPI 與色深。跳過此步驟或傳入損毀的串流會導致 OCR 漏字或拋出例外。

> **專業提示**：若處理使用者上傳的檔案，請將 `FromFile` 呼叫包在 try‑catch 區塊中，並先驗證檔案大小。大型影像若未正確 **configure GPU memory**，可能會耗盡 GPU 記憶體。

---

## 設定最大 GPU 記憶體以獲得最佳效能

GPU 資源相當寶貴，特別是在共享伺服器或 VRAM 有限的筆記型電腦上。`MaxDeviceMemory` 屬性告訴 Aspose 可安全分配多少 GPU 記憶體。

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

當你 **set max GPU memory** 時，若無法滿足需求，引擎會自動回退至 CPU 處理，避免當機。這是 **configure GPU memory** 時最安全的做法，無需硬編碼裝置特定上限。

**何時調整**：  
* 若在大量批次處理時看到 `OutOfMemoryException`，請降低上限。  
* 若收據為高解析度（300 DPI 以上），可將上限提升至 2 GB 以維持高速。

---

## 在影像上執行 OCR 以擷取收據文字

現在進入有趣的部分——實際 **run OCR on image** 並擷取收據文字。`Recognize` 方法會回傳一個 `OcrResult` 物件，其 `Text` 屬性即為純文字輸出。

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

主控台會顯示類似以下內容：

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**為何有效**：  
GPU 引擎執行的深度學習模型已在各種文件版面上進行訓練。只要提供乾淨且正確載入的影像，就能讓模型有最佳機會 **extract text from receipt**，達到高準確度。

---

## 驗證輸出與常見問題

即使使用強大的引擎，OCR 仍非魔法。以下是需要留意的幾點：

| 問題 | 原因 | 解決方式 |
|------|------|----------|
| 字元亂碼 | 對比度低或影像模糊 | 使用 Aspose 的 `ImageProcessor` 前處理以提升對比度 |
| 遺失行列 | 影像裁切過緊 | 確保收據完整位於影像範圍內 |
| 記憶體不足錯誤 | `MaxDeviceMemory` 對於影像大小過低 | 提升 `MaxDeviceMemory` 或先將影像縮小 |
| 語言錯誤 | 收據包含非英文文字 | 設定 `gpuEngine.Language = OcrLanguage.Spanish;`（或相應語言） |

若遇到上述情況，快速的解法是將影像最長邊縮小至 2000 px 以下——這可大幅減輕 GPU 壓力，同時對大多數收據的可讀性影響不大。

---

## 完整範例（可直接複製貼上）

以下是完整程式碼，直接編譯即可。請將檔案路徑替換為您自己的收據位置。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**預期的主控台輸出**（您的收據會有所不同）：

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

使用 `dotnet run` 執行程式。若看到文字被列印，恭喜您已成功 **load image file**、**set max GPU memory**，並 **run OCR on image** 以 **extract text from receipt**。

---

## 常見問題

**Q: 此功能能在沒有專屬 GPU 的機器上運作嗎？**  
A: 能。若未偵測到相容的 GPU，Aspose.OCR 會優雅地回退至 CPU 模式。您仍可 **load image file** 並 **run OCR on image**，只是速度會稍慢。

**Q: 我可以一次批次處理多張收據嗎？**  
A: 當然可以。將辨識程式碼包在 `foreach` 迴圈中，但請記得重複使用同一個 `GpuEngine` 實例——這樣可避免每個檔案都重新初始化 GPU 資源。

**Q: 若我的收據不是英文，該怎麼辦？**  
A: 在呼叫 `Recognize` 前先設定語言：

```csharp
gpuEngine.Language = OcrLanguage.French;
```

引擎將套用相應的字元集。

---

## 後續步驟與相關主題

既然已掌握基礎，建議進一步探索：

* **Fine‑tuning OCR accuracy** – 嘗試調整 `gpuEngine.RecognitionOptions`，例如 `EnableDeskew` 或 `ContrastEnhancement`。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}