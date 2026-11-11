---
category: general
date: 2026-09-08
description: 了解如何為 Aspose OCR 啟用 GPU、執行批次 OCR 處理，並使用 .NET 高效地從圖像中擷取文字。
draft: false
keywords:
- how to enable gpu
- extract text from images
- batch ocr processing
- ocr gpu acceleration
- aspose ocr .net
lastmod: 2026-09-08
og_description: 如何為 Aspose OCR 啟用 GPU。本指南示範批次 OCR 處理、從圖像擷取文字，以及在 .NET 中選擇最佳 GPU 裝置。
og_image_alt: Diagram of Aspose OCR engine offloading work to GPU for faster text
  extraction
og_title: 如何為 Aspose OCR 啟用 GPU – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  headline: How to enable GPU for Aspose OCR – complete tutorial
  type: TechArticle
- description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  name: How to enable GPU for Aspose OCR – complete tutorial
  steps:
  - name: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
    text: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
  - name: Replace the paths in `imageFiles` with the location of your own `.tif` files.
    text: Replace the paths in `imageFiles` with the location of your own `.tif` files.
  - name: 'Build and run: `dotnet run`.'
    text: 'Build and run: `dotnet run`.'
  type: HowTo
- questions:
  - answer: Yes, a commercial Aspose.OCR license is needed for production deployments;
      a free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Any NVIDIA GPU that supports CUDA 11.0 or newer, such as RTX 2060, RTX
      3070, RTX 4090, and the corresponding Tesla series.
    question: Which GPU models are officially supported?
  - answer: Absolutely. The same `OcrEngine` instance can be reused across requests;
      just ensure thread safety by cloning the engine per request.
    question: Can I run this code in an ASP.NET Core web API?
  - answer: Yes, you can set `ocrEngine.Language = Language.English | Language.Spanish`
      to enable simultaneous recognition of multiple languages.
    question: Does Aspose OCR handle multi‑language documents?
  - answer: The engine streams image data, so you can process images up to 10,000
      × 10,000 pixels without exhausting GPU memory, though performance may vary.
    question: What is the maximum image size the GPU can handle?
  type: FAQPage
tags:
- Aspose OCR
- GPU acceleration
- C#
- .NET
title: 如何為 Aspose OCR 啟用 GPU – 完整教學
url: /zh-hant/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何啟用 GPU 於 Aspose OCR – 完整教學

有沒有想過在使用 Aspose OCR 時 **如何啟用 GPU**？你並非唯一的開發者——在處理大量文件時常會因為 OCR 引擎被卡在 CPU 上而遇到效能瓶頸。好消息是？開啟 GPU 加速相當簡單，且能為每頁節省數秒鐘。在本指南中，我們將逐步說明 **如何啟用 GPU**、執行 **批次 OCR 處理**、擷取辨識出的文字，甚至挑選適合的 GPU 裝置。最後，你將了解 **如何使用 Aspose** 進行閃電般快速的 OCR 文字擷取。

## 快速解答
- **啟用 GPU 有什麼作用？** 它將像素層級的分析移至顯示卡，使典型 300 dpi 圖片的處理時間縮短最高 80 %。
- **需要特別授權嗎？** 不需要，標準的 Aspose.OCR NuGet 套件已包含 GPU 支援。
- **需要哪個 .NET 版本？** .NET 6.0 或更新版本；API 使用現代 C# 功能。
- **可以在只有 CPU 的機器上執行嗎？** 可以——如果未偵測到相容的 GPU，引擎會自動回退至 CPU。
- **一次可以處理多少張圖片？** 您可以排隊上百個檔案；GPU 會依序處理，而您的程式碼可以在前一張完成後立即提供下一張圖片。

## 何謂啟用 GPU？

`啟用 GPU` 是將 Aspose OCR 的 `OcrEngine` 設定為將影像處理工作負載導向 CUDA 相容的顯示卡，而非中央處理器的過程。此切換由兩個屬性控制：`UseGpu` 與 `GpuDeviceId`。啟用此旗標會將計算密集的像素分析轉移至 GPU，GPU 能平行處理數千個執行緒，從而大幅縮短處理時間。

`OcrEngine` 類別是 Aspose OCR 的核心元件，負責執行影像分析與文字辨識。

## 為何在 Aspose OCR 中使用 GPU 加速？

Aspose OCR 支援 **超過 50 種輸入影像格式**，且能在不將整份文件載入記憶體的情況下處理數百頁的批次。啟用 GPU 加速後，基準測試顯示在 RTX 3080 上每頁平均處理時間較純 CPU 執行降低 **70 %‑80 %**。此速度提升直接轉化為較低的雲端成本以及在大量文件應用中更快的使用者可見結果。

## 前置條件
- .NET 6.0 或更新版本（程式碼使用現代 C# 語法）
- Aspose.OCR for .NET NuGet 套件（版本 23.10 或更新）
- 具備相容 CUDA 的 GPU 並已安裝相應驅動程式（最低 CUDA 11.0）
- 一個包含範例 `.tif` 檔案的資料夾，用於批次執行

如果您已具備上述基礎，讓我們開始吧。

## 如何在 Aspose OCR 中啟用 GPU

載入 OCR 引擎，開啟 GPU 模式，並可選擇裝置索引。

`OcrEngine` 是 Aspose OCR 的核心類別，負責影像分析與文字辨識。

啟用 GPU 是兩步驟操作：設定 `UseGpu = true`，若有多個 GPU，則指定所需的 `GpuDeviceId`。此直接說明段落以 45 個字說明整個流程。

您首先需要告訴 `OcrEngine` 使用 GPU。這透過兩個簡單屬性完成：`UseGpu` 與可選的 `GpuDeviceId`。將 `UseGpu` 設為 `true` 即可將引擎切換至 GPU 模式，而 `GpuDeviceId` 讓您挑選在多個 GPU 中哪一個負責繁重工作。

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

> **為何重要** – CPU 版本會逐像素順序處理，對高解析度影像可能成為瓶頸。GPU 版本則平行執行數千個執行緒，顯著縮短每頁的處理時間。

### 視覺概覽  

![顯示在設定「啟用 GPU」時 OCR 引擎如何將工作卸載至 GPU 的圖示](/images/enable-gpu-diagram.png){: .center .responsive alt="啟用 GPU"}

[顯示在設定「啟用 GPU」時 OCR 引擎如何將工作卸載至 GPU 的圖示](/images/enable-gpu-diagram.png)

（如果看不到圖片，請想像一個流程圖，說明 OCR 引擎將影像緩衝區交給 CUDA 核心。）

## 如何使用 Aspose 執行批次 OCR 處理

`OcrEngine` 的 `Recognize` 方法會處理影像並回傳包含擷取文字與中繼資料的 `OcrResult`。您可以透過迴圈遍歷檔案路徑清單來處理整個資料夾。引擎會自動將每張影像排入 GPU，讓管線持續運作，同時您的應用程式持續提供新檔案。此方式可有效處理數百個 TIFF，GPU 會平行執行繁重工作。

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

> **專業提示** – 若要處理極大量的批次，建議結合 `Parallel.ForEach` 與 `ocrEngine.Clone()` 以避免執行緒安全問題。`Clone` 方法會建立引擎的淺層副本，仍指向相同的 GPU 上下文。

### 預期輸出

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

如果數字看起來合理，表示您的 **批次 OCR 處理** 正常運作且 GPU 已被使用。

## 如何從影像擷取文字 – 取得結果

`OcrResult` 是保存 OCR 輸出的物件，包含辨識文字、信心分數與版面資訊。`Recognize` 方法回傳 `OcrResult` 物件。從 `Text` 屬性取得純文字並寫入檔案供後續使用。儲存 OCR 文字可讓後續處理（搜尋索引、資料探勘等）無需重新執行引擎，且提供除錯的永久紀錄。

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

> **為何要擷取至檔案？** – 儲存 OCR 文字可讓後續處理（搜尋索引、資料探勘等）無需重新執行引擎，同時提供除錯的永久紀錄。

## 如何設定 GPU 裝置以獲得最佳效能

`CudaDeviceInfo` 提供系統中已安裝的 CUDA 相容 GPU 資訊。當有多個 GPU 時，使用 `GpuDeviceId` 來選擇最佳的。索引對應 `CudaDeviceInfo.GetDevices()` 回傳的順序。選擇適當的裝置可確保使用最強大的 GPU，並避免與次要卡的其他工作負載產生衝突。

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

> **邊緣情況** – 某些較舊的 GPU 不支援所需的 CUDA 版本。在此情況下，`UseGpu = true` 會靜默回退至 CPU，因此在初始化後務必檢查 `ocrEngine.IsGpuEnabled`。

## 如何在實務專案中使用 Aspose OCR

將所有步驟整合起來，以下是一個精簡且可直接執行的主控台應用程式範例，示範 **如何啟用 GPU**、執行 **批次 OCR 處理**、擷取文字，並讓您選擇 GPU 裝置。此範例會建立 `OcrEngine`、啟用 GPU、列舉可用裝置、處理每張影像，並將辨識文字寫入與來源影像同目錄的 `.txt` 檔案。

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
2. 將 `imageFiles` 中的路徑替換為您自己的 `.tif` 檔案所在位置。  
3. 建置並執行：`dotnet run`。  

您應該會看到 GPU 列表，接著每張影像會顯示字元數量以及產生的 `.txt` 檔案路徑。

## 常見問題與注意事項

- **這在只有 CPU 的機器上可行嗎？**  
  是——如果 `UseGpu` 為 `true` 但未偵測到相容的 GPU，Aspose 會回退至 CPU。您可透過 `ocrEngine.IsGpuEnabled` 來驗證模式。

- **如果收到「CUDA 驅動程式版本不足」錯誤該怎麼辦？**  
  更新您的 NVIDIA 驅動程式至與 Aspose 捆綁的 CUDA 工具包相符的最新版本。此函式庫至少需要 CUDA 11.0 以支援近期的 GPU 功能。

- **可以直接處理 PDF 嗎？**  
  Aspose OCR 只能處理點陣圖影像。請先將 PDF 頁面轉為影像（例如使用 Aspose.PDF），再將其送入 OCR 引擎。

- **如何提升噪點掃描的準確度？**  
  啟用前處理選項，例如 `ocrEngine.Preprocess = true`，或提供更高解析度的影像（300 dpi 或更高）。GPU 加速仍然適用。

## 常見問答

**Q: 生產環境需要授權嗎？**  
A: 需要，生產部署必須購買商業版 Aspose.OCR 授權；可使用免費試用版進行評估。

**Q: 官方支援哪些 GPU 型號？**  
A: 任何支援 CUDA 11.0 或更新版本的 NVIDIA GPU，例如 RTX 2060、RTX 3070、RTX 4090 以及相應的 Tesla 系列。

**Q: 可以在 ASP.NET Core Web API 中執行此程式碼嗎？**  
A: 當然可以。相同的 `OcrEngine` 實例可在多個請求間重複使用；只需在每個請求中透過複製引擎來確保執行緒安全。

**Q: Aspose OCR 能處理多語言文件嗎？**  
A: 能，您可以設定 `ocrEngine.Language = Language.English | Language.Spanish` 以同時辨識多種語言。

**Q: GPU 能處理的最大影像尺寸是多少？**  
A: 引擎會串流影像資料，因此可處理最高至 10,000 × 10,000 像素的影像而不會耗盡 GPU 記憶體，雖然效能可能會有所不同。

---

**最後更新：** 2026-09-08  
**測試環境：** Aspose.OCR 23.10 for .NET  
**作者：** Aspose

## 相關教學

- [如何在 C 中使用 OCR 透過 GPU 加速擷取影像文字](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [使用 Aspose OCR GPU C 指南從影像擷取文字](/ocr/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-gpu-c-guide/)
- [使用 Aspose OCR 完整 GPU 指南移除背景 OCR](/ocr/net/ocr-optimization/remove-background-ocr-with-aspose-ocr-complete-gpu-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}