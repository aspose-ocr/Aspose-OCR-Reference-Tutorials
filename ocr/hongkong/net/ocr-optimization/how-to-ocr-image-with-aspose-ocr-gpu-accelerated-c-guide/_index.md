---
category: general
date: 2026-02-17
description: 學習如何在 GPU 上使用 Aspose OCR 進行影像文字辨識。提供逐步程式碼示範，從影像中辨識文字、載入高解析度影像、設定 GPU
  裝置 ID，並使用 Aspose 抽取文字。
draft: false
keywords:
- how to ocr image
- recognize text from image
- load high resolution image
- set gpu device id
- extract text using aspose
language: zh-hant
og_description: 如何在 GPU 上使用 Aspose OCR 進行圖像文字辨識。跟隨完整的 C# 教程，從圖像中識別文字、載入高解析度圖像、設定 GPU
  裝置 ID，並使用 Aspose 提取文字。
og_title: 如何使用 Aspose OCR 進行圖像文字辨識 – GPU 加速 C# 指南
tags:
- Aspose OCR
- C#
- GPU acceleration
title: 使用 Aspose OCR 進行圖像光學字符辨識 – GPU 加速 C# 指南
url: /zh-hant/net/ocr-optimization/how-to-ocr-image-with-aspose-ocr-gpu-accelerated-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR 進行圖像 OCR – GPU 加速 C# 指南

有沒有想過 **如何 OCR 圖像**，當檔案是巨大的 300 DPI 掃描且需要在數秒內得到結果？你並不孤單——開發者常常與僅使用 CPU 的緩慢 OCR 引擎搏鬥，尤其是面對高解析度圖片。好消息是？Aspose OCR 讓你利用 GPU，大幅縮短處理時間，同時保持高準確度。

在本教學中，我們將逐步示範一個完整、可執行的範例，**從圖像辨識文字**、**載入高解析度圖像**、**設定 GPU 裝置 ID**，最後 **使用 Aspose 抽取文字**。完成後，你將擁有一個可直接放入任何 .NET 專案的自包含程式。

## 您需要的環境

- **.NET 6.0** 或更新版本（此程式碼亦支援 .NET Framework 4.7+）
- **Aspose.OCR for .NET** NuGet 套件（版本 23.11 或更新）
- 具備 CUDA 11+ 的 GPU 機器（可選，但建議使用）
- 一張你想要 OCR 的高解析度 JPEG/PNG（例如 `highres_scan.jpg`）

如果缺少上述任一項，請使用以下指令取得 NuGet 套件：

```bash
dotnet add package Aspose.OCR
```

不需要額外的原生函式庫；Aspose 已為你捆綁 CUDA 執行時。

![如何 OCR 圖像示意圖](image-placeholder.png "說明 GPU 加速 OCR 流程的圖示 – 如何 OCR 圖像")

## 步驟 1：建立 OCR 引擎並設定 GPU 裝置 ID  

首先必須告訴 Aspose 在 GPU 上執行。這就是 **設定 GPU 裝置 ID** 的用處——若你有多顆 GPU，可選擇最適合工作負載的那一顆。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine with GPU processing mode
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    ProcessingMode = ProcessingMode.Gpu, // Enable GPU acceleration
    GpuDeviceId = 0                     // Choose GPU #0 (change if you have several)
});
```

> **為什麼重要：** GPU 處理會將繁重的影像分析工作交給平行核心，使典型掃描的速度提升 3‑5 倍。若未設定 `GpuDeviceId`，Aspose 會預設使用第一顆裝置，對單 GPU 環境而言已足夠。

## 步驟 2：載入高解析度圖像  

接著，我們 **載入高解析度圖像** 資料，使 OCR 引擎能正確讀取。Aspose 提供 `ImageStream.FromFile`，可直接將檔案讀入記憶體，避免不必要的轉換。

```csharp
// Path to your high‑resolution scan (300 DPI or more)
string imagePath = @"YOUR_DIRECTORY/highres_scan.jpg";

// Load the image; ImageStream handles large files efficiently
var image = ImageStream.FromFile(imagePath);
```

> **小技巧：** 若圖像存放於雲端儲存桶，也可以直接傳入 `Stream`——只需將 `FromFile` 改為 `FromStream(yourStream)`。引擎仍會將其視為高解析度來源。

## 步驟 3：從圖像辨識文字  

現在引擎已就緒且圖片已載入，我們可以 **從圖像辨識文字**。`Recognize` 方法會回傳 `OcrResult` 物件，內含純文字、信心分數，甚至如果需要還有邊界框資訊。

```csharp
// Perform OCR; this call is where the GPU does its magic
OcrResult recognitionResult = ocrEngine.Recognize(image);

// For debugging, you can also inspect recognitionResult.Regions
```

> **邊緣情況：** 若圖像過暗或噪點過多，建議在呼叫 `Recognize` 前先進行前處理（例如提升對比度）。Aspose 提供 `Preprocess` API，但對大多數乾淨掃描而言預設設定已足夠。

## 步驟 4：使用 Aspose 抽取文字並顯示  

最後，我們 **使用 Aspose 抽取文字**，只要讀取結果的 `Text` 屬性即可。以下範例將文字印到主控台，你也可以寫入檔案或資料庫。

```csharp
// Output the plain‑text result
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(recognitionResult.Text);
```

**預期輸出**（以掃描發票為例）：

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,254.00
Thank you for your business!
```

若出現亂碼，請再次確認圖像確實為高解析度，且在 `OcrEngineSettings` 中正確設定語言（例如 `Language = Language.English`）。

## 完整範例程式  

將所有步驟整合起來，以下是可直接貼到新 Console 專案的完整程式碼：

```csharp
// ------------------------------------------------------------
// Full OCR example – Aspose OCR with GPU acceleration
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine for GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            ProcessingMode = ProcessingMode.Gpu, // GPU acceleration
            GpuDeviceId = 0                      // Change if you have multiple GPUs
        });

        // 2️⃣ Load a high‑resolution image
        string imagePath = @"YOUR_DIRECTORY/highres_scan.jpg";
        var image = ImageStream.FromFile(imagePath);

        // 3️⃣ Recognize text from the image
        OcrResult result = ocrEngine.Recognize(image);

        // 4️⃣ Extract and display the plain text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

使用 `dotnet run` 執行。若 GPU 表現良好，即使是 5 MB、300 DPI 的掃描，也能在一秒內取得 OCR 結果。

## 常見問題與專業技巧  

### 若沒有 GPU 該怎麼辦？  
仍可在 CPU 上使用 Aspose OCR，只需設定 `ProcessingMode = ProcessingMode.Cpu`。API 完全相同，唯一差別是效能。

### 如何處理多語言？  
在 `OcrEngineSettings` 中加入 `Language = Language.Multilingual`（或指定如 `Language.French`）即可。Aspose 會自動載入相應的語言套件。

### 能直接處理 PDF 嗎？  
可以——Aspose OCR 先從 PDF 中抽取圖像，再對每頁執行 OCR。將 `Aspose.PDF` 與相同的 `OcrEngine` 結合，即可打造無縫流水線。

### 什麼時候需要調整 `GpuDeviceId`？  
若伺服器同時執行影像處理與機器學習工作，建議將 GPU 1 指派給 OCR（`GpuDeviceId = 1`），保留 GPU 0 給推論任務使用。

### 如何提升噪點掃描的準確度？  
前處理圖像：  
```csharp
image = image.AdjustContrast(1.2f).ApplyThreshold(0.5f);
```
這些方法屬於 Aspose 的影像處理工具。

## 結論  

現在你已掌握 **如何 OCR 圖像**，使用 Aspose OCR 搭配 GPU 加速，了解 **從圖像辨識文字**、**載入高解析度圖像**、**設定 GPU 裝置 ID**，以及 **使用 Aspose 抽取文字** 的完整流程，並能在乾淨、可投入生產的 C# 程式中實作。

試著在不同檔案上跑跑看——模糊的收據、光亮的傳單，甚至手寫筆記。調整語言設定與前處理步驟，觀察準確度的變化。

接下來，你可以探索 **批次處理**（遍歷資料夾中的多張掃描）或將 OCR 結果整合至 **搜尋索引**，以實現快速文件檢索。這兩個主題自然延伸自本教學，亦是絕佳的後續專案。

祝開發順利，願你的 OCR 流程快速且完美！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}