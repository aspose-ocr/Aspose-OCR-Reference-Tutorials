---
category: general
date: 2025-12-30
description: 如何在 Aspose OCR 中啟用 GPU，以進行批量 OCR 處理和文字提取。了解如何設定 GPU 設備以及如何高效使用 Aspose。
draft: false
keywords:
- how to enable gpu
- batch ocr processing
- ocr text extraction
- set gpu device
- how to use aspose
language: zh-hant
og_description: 如何在 Aspose OCR 中啟用 GPU。請參考本指南進行批次 OCR 處理、OCR 文字提取、設定 GPU 裝置，並學習如何使用
  Aspose。
og_title: 如何為 Aspose OCR 啟用 GPU – 完整教學
tags:
- Aspose
- OCR
- GPU
- C#
title: 如何為 Aspose OCR 啟用 GPU – 逐步指南
url: /zh-hant/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何為 Aspose OCR 啟用 GPU – 完整教學

有沒有想過在使用 Aspose OCR 時 **如何啟用 GPU**？你並非唯一的開發者——面對大量文件時，常因 OCR 引擎只能使用 CPU 而遇到效能瓶頸。好消息是，開啟 GPU 加速相當簡單，且能為每頁節省數秒。本指南將帶你一步步了解 **如何啟用 GPU**、執行 **批次 OCR 處理**、擷取辨識文字，甚至挑選適當的 GPU 裝置。完成後，你將知道 **如何使用 Aspose** 進行閃電般快速的 OCR 文字擷取。

## 本教學涵蓋內容

我們將先設定 Aspose OCR 函式庫，接著啟用 GPU 支援，最後將一批 TIFF 圖片送入引擎處理。過程中會說明為何需要手動 **設定 GPU 裝置**、可能遇到的陷阱，以及如何驗證文字擷取是否成功。無需外部文件，只提供完整、可直接複製貼上的解決方案，讓你今天就能執行。

> **先決條件**  
> - .NET 6.0 或更新版本（程式碼使用現代 C# 語法）  
> - Aspose.OCR for .NET NuGet 套件（版本 23.10 或更新）  
> - 支援 CUDA 的 GPU 並已安裝相應驅動程式  
> - 一個資料夾內放置數個 `.tif` 範例檔案以供批次執行  

如果已滿足上述條件，讓我們開始吧。

## 如何在 Aspose OCR 中啟用 GPU

首先需要告訴 `OcrEngine` 使用 GPU。這透過兩個簡單屬性完成：`UseGpu` 與可選的 `GpuDeviceId`。將 `UseGpu` 設為 `true` 即可切換引擎至 GPU 模式，而 `GpuDeviceId` 則讓你選擇哪一顆 GPU（若有多顆）負責運算。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;
using System.Collections.Generic;

// Step 1: Create the OCR engine and enable GPU acceleration
var ocrEngine = new OcrEngine
{
    // Turn on GPU support – this is the core of “how to enable gpu”
    UseGpu = true,

    // (optional) Choose GPU index 0; change if you have multiple devices
    GpuDeviceId = 0
};
```

> **為何這很重要** – CPU 版會逐像素順序處理，對高解析度影像可能成為瓶頸。GPU 版則平行執行數千個執行緒，顯著縮短每頁的處理時間。

### 視覺概覽  

![圖示說明在設定「如何啟用 GPU」時，OCR 引擎如何將工作卸載至 GPU](/images/enable-gpu-diagram.png){: .center .responsive alt="如何啟用 GPU"}

*(如果看不到圖片，請想像一張流程圖，說明 OCR 引擎將影像緩衝區交給 CUDA 核心。)*

## 使用 Aspose 進行批次 OCR 處理

既然引擎已具備 GPU 能力，接下來將檔案清單傳入。批次處理只需要對包含影像路徑的 `List<string>` 進行迴圈。由於使用 GPU，引擎會自動將每張影像排入裝置佇列，保持管線運作。

```csharp
// Step 2: Define the image files you want to process
var imageFiles = new List<string>
{
    @"C:\OCRSamples\page1.tif",
    @"C:\OCRSamples\page2.tif",
    @"C:\OCRSamples\page3.tif"
};

// Step 3: Process each image and report the character count
foreach (var imagePath in imageFiles)
{
    // Recognize the image – the GPU does the heavy lifting behind the scenes
    var ocrResult = ocrEngine.Recognize(imagePath);

    // Show how many characters were extracted – a quick sanity check
    Console.WriteLine($"{imagePath}: {ocrResult.Text.Length} characters");
}
```

> **專業提示** – 若批次規模極大，建議結合 `Parallel.ForEach` 與 `ocrEngine.Clone()` 使用，以避免執行緒安全問題。`Clone` 方法會建立引擎的淺層副本，仍指向相同的 GPU 上下文。

### 預期輸出

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

如果數字看起來合理，代表你的 **批次 OCR 處理** 正常運作且已使用 GPU。

## OCR 文字擷取 – 取得結果

`Recognize` 方法會回傳一個 `OcrResult` 物件，內含原始文字、信心分數，若需要亦可取得邊界框。讓我們取出純文字並寫入檔案，以便驗證擷取結果。

```csharp
foreach (var imagePath in imageFiles)
{
    var ocrResult = ocrEngine.Recognize(imagePath);
    var extractedText = ocrResult.Text;

    // Save the text to a .txt file with the same base name
    var outputPath = System.IO.Path.ChangeExtension(imagePath, ".txt");
    System.IO.File.WriteAllText(outputPath, extractedText);

    Console.WriteLine($"Extracted text saved to {outputPath}");
}
```

> **為何要寫入檔案？** – 儲存 OCR 文字可供後續處理（搜尋索引、資料探勘等）使用，免除重新執行引擎，也提供除錯時的永久紀錄。

## 設定 GPU 裝置以獲得最佳效能

如果你的工作站配備多顆 GPU，例如專用的 RTX 用於機器學習，還有整合式顯示卡，你需要確保選擇正確的 GPU。`GpuDeviceId` 屬性接受一個整數，對應 `CudaDeviceInfo.GetDevices()` 回傳的裝置索引。

```csharp
using Aspose.OCR.Gpu;

// List all available GPU devices
var devices = CudaDeviceInfo.GetDevices();
for (int i = 0; i < devices.Length; i++)
{
    Console.WriteLine($"Device {i}: {devices[i].Name} (Compute Capability {devices[i].ComputeCapability})");
}

// Suppose you want to use the second GPU (index 1)
ocrEngine.GpuDeviceId = 1;
Console.WriteLine($"Switched to GPU device {ocrEngine.GpuDeviceId}");
```

> **特殊情況** – 某些舊版 GPU 不支援所需的 CUDA 版本。此時 `UseGpu = true` 會靜默回退至 CPU，因此在初始化後務必檢查 `ocrEngine.IsGpuEnabled`。

## 在實務專案中如何使用 Aspose OCR

將上述所有步驟整合起來，以下是一個精簡且可直接執行的主控台應用程式範例，示範 **如何啟用 GPU**、執行 **批次 OCR 處理**、擷取文字，並讓你選擇 GPU 裝置。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine with GPU support
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,
            GpuDeviceId = 0 // change if you have multiple GPUs
        };

        // -------------------------------------------------
        // 2️⃣ (Optional) Show available GPU devices
        // -------------------------------------------------
        var devices = CudaDeviceInfo.GetDevices();
        Console.WriteLine("Available GPU devices:");
        for (int i = 0; i < devices.Length; i++)
        {
            Console.WriteLine($"  [{i}] {devices[i].Name} – Compute {devices[i].ComputeCapability}");
        }

        // -------------------------------------------------
        // 3️⃣ Define the batch of images to process
        // -------------------------------------------------
        var imageFiles = new List<string>
        {
            @"C:\OCRSamples\page1.tif",
            @"C:\OCRSamples\page2.tif",
            @"C:\OCRSamples\page3.tif"
        };

        // -------------------------------------------------
        // 4️⃣ Process each image, extract text, and save it
        // -------------------------------------------------
        foreach (var imagePath in imageFiles)
        {
            var result = ocrEngine.Recognize(imagePath);
            var text = result.Text;

            var txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, text);

            Console.WriteLine($"{Path.GetFileName(imagePath)} → {Path.GetFileName(txtPath)} ({text.Length} chars)");
        }

        Console.WriteLine("All done! GPU‑accelerated OCR batch completed.");
    }
}
```

### 執行範例

1. 安裝 NuGet 套件：`dotnet add package Aspose.OCR --version 23.10.0`  
2. 將 `imageFiles` 中的路徑替換為你自己的 `.tif` 檔案所在位置。  
3. 建置並執行：`dotnet run`。  

執行後應會看到 GPU 列表，接著每張影像會顯示字元數量以及產生的 `.txt` 檔案路徑。

## 常見問題與注意事項

- **這能在只有 CPU 的機器上運作嗎？**  
  可以——若 `UseGpu` 為 `true` 但找不到相容的 GPU，Aspose 會回退至 CPU。你可以透過 `ocrEngine.IsGpuEnabled` 來驗證模式。

- **如果出現「CUDA 驅動版本不足」錯誤該怎麼辦？**  
  請將 NVIDIA 驅動程式更新至與 Aspose 捆綁的 CUDA 工具包相符的最新版本。此函式庫至少需要 CUDA 11.0 才能使用近期的 GPU 功能。

- **可以直接處理 PDF 嗎？**  
  Aspose OCR 只能處理點陣圖影像。請先將 PDF 頁面轉為影像（例如使用 Aspose.PDF），再送入 OCR 引擎。

- **如何提升噪點掃描的辨識準確度？**  
  可啟用前處理選項，如 `ocrEngine.Preprocess = true`，或使用更高解析度的影像（300 dpi 以上）。GPU 加速仍然適用。

## 結論

我們已說明 **如何為 Aspose OCR啟用 GPU**、示範 **批次 OCR 處理**、展示 **OCR 文字擷取**，並教你 **設定 GPU 裝置** 以獲得最佳效能。依照完整的程式碼範例，你現在可以將快速的 GPU 加速 OCR 整合至任何 .NET 專案，並自信地回答「如何使用 Aspose」的問題。

準備好進一步了嗎？可以嘗試加入語言偵測、將擷取的文字輸入搜尋索引，或測試多 GPU 擴展以處理海量文件。結合 Aspose 完備的 API 與現代 GPU 的強大算力，無所不能。

祝程式開發順利，願你的 OCR 工作跑得跟 GPU 一樣快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}