---
category: general
date: 2026-01-13
description: 學習如何使用 Aspose OCR 從圖像中辨識文字，並快速從收據中提取文字。包括載入圖像進行 OCR 以及設定 GPU 裝置 ID 的步驟。
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for ocr
- set gpu device id
language: zh-hant
og_description: 使用 Aspose OCR 即時辨識圖像文字。請依照本步驟指南載入圖像進行 OCR、設定 GPU 裝置 ID，並從收據中擷取文字。
og_title: 從圖像辨識文字 – 完整 GPU 加速 C# 指南
tags:
- Aspose OCR
- C#
- GPU computing
title: 使用 Aspose OCR 從圖像辨識文字 – GPU 加速的 C# 教程
url: /zh-hant/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像辨識文字 – 完整 GPU 加速 C# 指南

Ever needed to **recognize text from image** but found the CPU version painfully slow? Maybe you’re trying to **extract text from receipt** files and the latency is killing your user experience. The good news is you don’t have to settle for sluggish performance—Aspose OCR’s GPU package can turbo‑charge the process, and the code is only a few lines long.

In this tutorial we’ll walk through a full, runnable example that shows how to **load image for OCR**, configure the GPU with **set GPU device ID**, and finally retrieve the plain‑text result. By the end you’ll have a ready‑to‑drop snippet that works on any modern Windows or Linux machine with a supported NVIDIA card.

---

## 您需要的環境

- **.NET 6+**（或 .NET Framework 4.7.2+）– 兩者皆支援此 API。  
- **Aspose.OCR** NuGet 套件 **加上** **Aspose.OCR.Gpu** 附加元件。  
- 具備至少 2 GB VRAM 的 NVIDIA GPU（示範限制使用 1 GB）。  
- 範例影像，例如掃描的收據 (`receipt.jpg`)。

如果您已有專案，只需執行 `dotnet add package Aspose.OCR` 與 `dotnet add package Aspose.OCR.Gpu`。不需要額外的原生函式庫；SDK 已內建所需的 CUDA 二進位檔。

---

## Step‑by‑Step Implementation

### ## 如何使用 Aspose OCR 與 GPU 進行圖像文字辨識

以下是 **完整、獨立的程式**。直接貼到新的 Console 專案中，然後按 `Ctrl+F5` 執行。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑accelerated namespace

class GpuOcrDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize a GPU‑enabled OCR engine
        // -------------------------------------------------
        var ocrEngine = new GpuOcrEngine();

        // -------------------------------------------------
        // Step 2: (Optional) Select the GPU device and limit memory usage
        // -------------------------------------------------
        ocrEngine.DeviceId = 0;        // set GPU device ID – first GPU in the system
        ocrEngine.MaxMemoryMb = 1024;  // cap at 1 GB to avoid OOM on shared machines

        // -------------------------------------------------
        // Step 3: Load the image you want to recognize
        // -------------------------------------------------
        var receiptImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

        // -------------------------------------------------
        // Step 4: Perform OCR – here we extract text from receipt (English)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);

        // -------------------------------------------------
        // Step 5: Output the recognized plain text
        // -------------------------------------------------
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **Pro tip:** If your machine has multiple GPUs, change `DeviceId` to `1`, `2`, etc., to pick the less‑busy card. The SDK will throw a clear `GpuDeviceNotFoundException` if the ID is out of range.

### ### 步驟 1：Load image for OCR

The `OcrImage.FromFile` call does more than just read a bitmap—it pre‑processes the image (deskew, binarization) based on internal heuristics. This is why **load image for OCR** is a separate step: you can swap in a `MemoryStream` if your image lives in a database.

```csharp
var receiptImage = OcrImage.FromFile(@"C:\Invoices\receipt.jpg");
```

If you need to **recognize text from image** that’s already in memory:

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes(@"receipt.jpg")))
{
    var receiptImage = OcrImage.FromStream(ms);
}
```

### ### 步驟 2：Set GPU device ID and memory limits

GPU resources are finite. By exposing `DeviceId` and `MaxMemoryMb`, Aspose lets you **set GPU device ID** safely, preventing one process from hogging the entire card.

```csharp
ocrEngine.DeviceId = 0;        // first GPU
ocrEngine.MaxMemoryMb = 1024; // 1 GB ceiling
```

If you exceed the memory cap, the engine will automatically spill to system RAM, which is slower but prevents crashes.

### ### 步驟 3：Extract text from receipt (recognize text from image)

The `Recognize` method does the heavy lifting. You can pass any language supported by Aspose OCR; for receipts, English works most of the time, but you can also add `OcrLanguage.Spanish` or a custom language pack.

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);
Console.WriteLine(ocrResult.Text);
```

**Expected output** (sample):

```
Store: QuickMart
Date: 2025-12-01
Total: $23.45
Thank you for shopping!
```

---

## 常見變化與邊緣案例

| 情境 | 需要變更的地方 | 原因 |
|-----------|----------------|-----|
| **同一張圖像中有多張收據** | 呼叫 `ocrEngine.Recognize` 於每個裁切區域（使用 `OcrImage.Crop`） | 因為引擎只看到較小、較乾淨的區域，可提升辨識準確度。 |
| **低解析度掃描（<150 dpi）** | 在辨識前使用 `receiptImage.Resize(2.0)` 進行放大 | 更高的像素密度讓 GPU 有更多資料可處理。 |
| **非英文收據** | 傳入 `OcrLanguage.French`（或自訂的 `.traineddata`） | 語言專屬模型可減少誤判。 |
| **GPU 不可用** | 在 try‑catch 區塊內回退至 `OcrEngine`（CPU） | 確保應用在無頭伺服器上仍能正常運作。 |

```csharp
try
{
    var gpuEngine = new GpuOcrEngine();
    // configure GPU as shown earlier …
    var result = gpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
catch (GpuDeviceNotFoundException)
{
    // Graceful fallback
    var cpuEngine = new OcrEngine();
    var result = cpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
```

---

## 產線級 OCR 小技巧

- **批次處理：** 將辨識迴圈包在 `Parallel.ForEach` 中，但將平行度限制在可分配的 GPU 串流數量（通常每張卡 1‑2 個）。  
- **記憶體管理：** 及時釋放 `OcrImage` 物件（`receiptImage.Dispose()`），尤其在處理數千張收據時。  
- **日誌記錄：** 捕捉 `ocrResult.Confidence`，對低信心的行列觸發人工審核流程。  
- **安全性：** 處理敏感收據時，確保影像檔案儲存在加密的暫存資料夾，並在處理完畢後即時清除。

---

## 結論

You now have a **complete, runnable example** that shows how to **recognize text from image** with Aspose OCR’s GPU acceleration, **load image for OCR**, **set GPU device ID**, and finally **extract text from receipt** in a few concise steps. The code is ready for copy‑paste, and the explanations give you enough context to adapt it to multi‑language, multi‑GPU, or high‑throughput scenarios.

Ready for the next challenge? Try feeding a live video stream into `GpuOcrEngine` for real‑time receipt scanning, or integrate the result into a bookkeeping API. The sky’s the limit when you combine fast GPU OCR with clean C# design.

*祝編程快樂，願你的 OCR 永遠快速！* 

![recognize text from image demo screenshot](placeholder-image.png "recognize text from image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}