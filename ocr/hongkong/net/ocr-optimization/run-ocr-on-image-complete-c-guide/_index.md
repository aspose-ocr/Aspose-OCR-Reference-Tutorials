---
category: general
date: 2026-05-28
description: 使用 C# 在圖像上執行 OCR，快速讀取圖像文字並提取收據內容。了解 GPU 選項與載入技術。
draft: false
keywords:
- run ocr on image
- read text from image
- extract text from receipt
- load image for ocr
language: zh-hant
og_description: 使用 C# 於圖像執行 OCR。本教學示範如何從圖像讀取文字、從收據提取文字，並優化 GPU 使用。
og_title: 在圖像上執行 OCR – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  headline: Run OCR on Image – Complete C# Guide
  type: TechArticle
- description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  name: Run OCR on Image – Complete C# Guide
  steps:
  - name: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
    text: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
  - name: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
    text: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
  - name: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
    text: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
  - name: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
    text: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Computer Vision
title: 在圖像上執行 OCR – 完整 C# 指南
url: /zh-hant/net/ocr-optimization/run-ocr-on-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在圖像上執行 OCR – 完整 C# 指南

有沒有曾經需要 **在圖像上執行 OCR** 檔案，但不知從何開始？你並不孤單；許多開發者在首次嘗試從圖像資料讀取文字時都會碰到這個障礙。好消息是，只要幾行 C# 程式碼，你就能從收據掃描、PDF 或任何圖片中提取文字。在本指南中，我們將逐步示範一個完整、可直接執行的範例，並說明如何 **load image for OCR**、使用 GPU 加速，以及安全地限制記憶體使用量。

在本教學結束時，你將能夠：

* 在 C# 中初始化 OCR 引擎  
* **Load image for OCR** 從磁碟或串流載入  
* **Read text from image** 使用可選的 GPU 支援  
* **Extract text from receipt** 並將結果輸出至主控台  

不需要外部服務——只需本機函式庫與一張範例收據圖片。

## 需要的條件

| Prerequisite | Reason |
|--------------|--------|
| .NET 6.0 SDK or later | 現代執行環境，支援最新語言功能 |
| An OCR library that exposes an `OcrEngine` class (e.g., IronOCR, Tesseract .NET wrapper) | 提供下方使用的 `Configuration` 與 `Recognize` 方法 |
| A CUDA‑enabled GPU (optional) | 啟用 `EnableGpu` 旗標以加快處理速度 |
| A sample receipt image (`receipt.jpg`) | 示範 **extract text from receipt** 步驟 |
| Any C# IDE (Visual Studio, Rider, VS Code) | 方便快速編譯與除錯 |

如果沒有 GPU，程式碼會自動回退至 CPU 模式——不必擔心。

![在圖像上執行 OCR 範例輸出，顯示已辨識的收據文字](https://example.com/ocr-output.png "在圖像上執行 OCR – 範例主控台輸出")

## 步驟 1：在圖像上�行 OCR – 設定引擎

首先：建立 OCR 引擎的實例。此物件是整個流程的核心；它保存所有設定細節並執行繁重的運算。

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

*為何重要:* `OcrEngine` 類別封裝了原生 OCR 引擎（Tesseract、IronOCR 等）。只建立一次並在多張圖像間重複使用，可減少開銷，且讓你有唯一的地方調整設定。

## 步驟 2：Load Image for OCR

在引擎能讀取任何內容之前，你必須提供一張圖像。函式庫的 `Image` 屬性會根據實作方式接受串流或檔案路徑。

```csharp
// Step 2: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

*提示:* 如果你處理使用者上傳的檔案，請將此段包在 `try/catch` 中，並先驗證檔案類型。不支援的格式會拋出例外，可妥善處理。

## 步驟 3：Enable GPU Acceleration（可選）

如果你的機器具備相容的 CUDA 或 OpenCL 執行環境，開啟 GPU 模式可為每次辨識減少數秒時間。

```csharp
// Step 3: Enable GPU acceleration (requires CUDA/OpenCL runtime)
ocrEngine.Configuration.EnableGpu = true;
```

*專業提示:* 並非所有 GPU 效能相同。舊款顯卡可能因驅動程式開銷而稍微變慢。請同時測試兩種設定 (`EnableGpu = true/false`) 以找出最適合你硬體的方案。

## 步驟 4：Limit GPU Memory Usage（可選）

有時你不希望 OCR 程序佔用全部 GPU 記憶體，特別是當你與其他工作負載（如深度學習推論）共用 GPU 時。

```csharp
// Step 4: (Optional) Limit the amount of GPU memory the engine can use (in MB)
ocrEngine.Configuration.GpuMemoryLimit = 1024; // 1 GB limit
```

*使用時機:* 如果你在執行同時處理大量圖像的 Web 服務，限制記憶體可防止記憶體不足而當機。

## 步驟 5：Recognize Text and Read Text from Image

現在引擎已準備好執行工作。呼叫 `Recognize()` 會執行 OCR 流程並回傳提取出的字串。

```csharp
// Step 5: Perform OCR and retrieve the recognized text
string recognizedText = ocrEngine.Recognize();
```

*核心原因:* 這一行隱含了多層前處理（二值化、去斜）以及實際的字元分類。回傳的 `recognizedText` 為純 Unicode 字串，可直接進行後續處理。

## 步驟 6：Extract Text from Receipt – 輸出

最後，將結果寫入主控台或儲存到任意位置。對於收據，你之後可能會解析項目、總金額或日期。

```csharp
// Step 6: Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

**預期的主控台輸出（為簡潔起見已截斷）：**

```
=== OCR Result ===
Store Name
123 Main St.
Date: 04/27/2026
Item   Qty   Price
Apple   2    1.20
Bread   1    2.50
Total          3.70
Thank you!
```

如果 OCR 在特定收據版面上表現不佳，請考慮調整前處理選項（例如 `ocrEngine.Configuration.Deskew = true`）或提供更高解析度的圖像。

## 常見邊緣案例與處理方式

| Situation | Suggested Fix |
|-----------|----------------|
| **Null image** – `ocrEngine.Image` is `null` | 在指派前驗證檔案路徑；若缺少則拋出明確的 `ArgumentException`。 |
| **GPU not available** – `EnableGpu = true` throws `PlatformNotSupportedException` | 將 GPU 啟用呼叫包在 `try/catch` 中，並回退至 CPU 模式。 |
| **Large receipts ( > 10 MB )** cause memory pressure | 使用 `GpuMemoryLimit`，或將圖像分割成多塊處理（`ocrEngine.Configuration.TileSize`）。 |
| **Incorrect language detection** – output contains gibberish | 設定 `ocrEngine.Configuration.Language = "eng"`（或相應的 ISO 代碼）以強制使用英文。 |

## 生產環境 OCR 的專業提示

1. **Batch processing:** 重複使用單一 `OcrEngine` 實例處理一批圖像；它會快取語言模型並降低延遲。  
2. **Pre‑filtering:** 在將圖像交給引擎前，先執行簡單的灰階轉換與對比度提升——許多函式庫提供 `Preprocess` 方法。  
3. **Error logging:** 在每次呼叫 `Recognize()` 後捕獲 `ocrEngine.LastError`（若有），以診斷失敗而不會使服務當機。  
4. **Thread safety:** 大多數 OCR 引擎 **不** 支援執行緒安全。若需平行處理，請為每個執行緒建立獨立的引擎或使用佇列機制。  

## 結論

我們剛剛完整示範了在 C# 中 **run OCR on image** 的工作流程。從建立引擎、**loading image for OCR**、切換 GPU 加速，到最後 **extracting text from receipt**，你現在已具備堅實的基礎，可建構更複雜的文件處理管線。

接下來的步驟可以包括：

* 將收據文字解析成結構化的 JSON（使用正規表達式或自然語言函式庫）——非常適合 **read text from image** 自動化。  
* 將 OCR 步驟整合至 ASP .NET Core API，讓使用者可透過 HTTP 上傳收據。  
* 嘗試不同的 OCR 後端（Tesseract 與商業 SDK）以比較準確度。  

試著使用不同的收據版面，調整設定，你會發現將模糊照片轉換為可用資料的速度有多快。祝開發愉快，願你的圖像永遠清晰！

## 相關教學

- [使用 Aspose.OCR 進行語言選擇的 C# 圖像文字提取](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [從圖像提取文字 – 使用 Aspose.OCR for .NET 進行 OCR 優化](/ocr/english/net/ocr-optimization/)
- [如何透過在 OCR 中準備矩形來提取圖像文字](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}