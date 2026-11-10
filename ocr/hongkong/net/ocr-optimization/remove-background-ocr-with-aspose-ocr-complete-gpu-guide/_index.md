---
category: general
date: 2026-01-07
description: 移除背景 OCR 使用 Aspose OCR 在 GPU 上。學習提取文字圖像、選擇 GPU 設備，以及在 C# 中預處理圖像 OCR。
draft: false
keywords:
- remove background ocr
- extract text image
- select gpu device
- preprocess image ocr
language: zh-hant
og_description: 移除背景 OCR 使用 Aspose OCR 在 GPU 上。取得逐步 C# 程式碼以提取文字圖像、選擇 GPU 裝置，並預處理圖像
  OCR。
og_title: 使用 Aspose OCR 去除背景 OCR – 完整 GPU 指南
tags:
- Aspose OCR
- C#
- GPU acceleration
title: 使用 Aspose OCR 去除背景 – 完整 GPU 指南
url: /zh-hant/net/ocr-optimization/remove-background-ocr-with-aspose-ocr-complete-gpu-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# remove background ocr with Aspose OCR – 完整 GPU 指南

有沒有想過在需要從雜訊掃描中提取文字時，如何**remove background ocr**？你並不孤單。在許多實務專案中，背景雜訊會讓 OCR 結果幾乎無法閱讀，而僅使用 CPU 的流程速度緩慢。此指南將向你展示一種快速、GPU 加速的方式來*remove background ocr*，並從影像中取得乾淨的文字。

我們將逐步說明你所需的一切：從選擇正確的 GPU 裝置、設定 **preprocess image ocr** 流程，到最終提取文字影像。完成後，你將擁有一個可直接執行的 C# 程式，能自動完成所有步驟。

## 你將學會

- 如何為 Aspose OCR **select gpu device** 以及其重要性。
- 哪些 **preprocess image ocr** 濾鏡能真正去除背景雜訊。
- 使用 Aspose 的 `GpuOcrEngine` 完整實作 **remove background ocr**。
- 如何可靠地 **extract text image**，即使是低對比度文件。
- 技巧、邊緣案例處理，以及擴展此解決方案的後續想法。

> **先決條件** – .NET 6+（或 .NET Core 3.1+）、Visual Studio 2022（或任何 IDE）、具備 CUDA 支援的 NVIDIA GPU，以及 Aspose.OCR for .NET 授權。若尚未取得授權，可向 Aspose 申請免費暫時金鑰。

![remove background ocr 範例](remove-background-ocr.png "remove background ocr"){: .align-center alt="remove background ocr"}

## 第一步：Remove Background OCR – 初始化 GPU 引擎

首先，你需要建立一個支援 GPU 的 OCR 引擎。此引擎會在顯示卡上執行所有繁重的運算，速度遠快於純 CPU 處理。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Gpu;

// Create a GPU‑enabled OCR engine inside a using block so resources are freed automatically.
using (var ocrEngine = new GpuOcrEngine())
{
    // ... further configuration goes here ...
}
```

**為什麼這很重要：** `GpuOcrEngine` 類別會在內部載入 CUDA 核心，加速影像前處理與字元辨識。若跳過此步驟而使用預設的 `OcrEngine`，將失去使 **remove background ocr** 在大批次中實用的效能提升。

## 第二步：選擇最佳效能的 GPU 裝置

如果你的機器有多張 GPU（工作站常見），必須告訴 Aspose 使用哪一張。`DeviceId` 屬性接受從 0 開始的索引，`0` 代表偵測到的第一張 GPU。

```csharp
// Select the first GPU (DeviceId = 0). Change this value if you have more than one GPU.
ocrEngine.DeviceId = 0;
```

**專業提示：** 在終端機執行 `nvidia-smi` 以查看 GPU 清單及其 ID。選擇最強大的 GPU（通常是記憶體最大的那張）可將處理時間減半。

## 第三步：Preprocess Image OCR – 去除背景

現在我們設定 **preprocess image ocr** 流程。目標是 *remove background ocr* 各種雜訊，如斑點、不均勻光照與殘留陰影。

```csharp
var recognitionSettings = new RecognitionSettings
{
    Language = Language.ChineseSimplified, // Change to your target language
    PreprocessFilters = new[]
    {
        PreprocessFilter.Deskew,           // Aligns rotated text
        PreprocessFilter.ContrastEnhance, // Boosts contrast for faint characters
        PreprocessFilter.RemoveBackground // <-- This is the key for remove background ocr
    }
};
```

- **Deskew** – 自動旋轉影像，使文字行水平。  
- **ContrastEnhance** – 讓淡色文字在深色背景上更突出。  
- **RemoveBackground** – 本流程的關鍵；它會分析影像直方圖並去除低頻背景模式，正是取得乾淨 **remove background ocr** 結果所需。

> **邊緣案例：** 若來源影像已是均勻白色背景，可省略 `RemoveBackground`，避免過度處理。

## 第四步：載入要處理的影像

Aspose 能讀取多種格式（TIFF、PNG、JPEG、PDF）。此處我們載入一個包含中文合約的 TIFF 檔案——非常適合測試背景去除。

```csharp
// Replace the path with the location of your image file.
var imageStream = ImageStream.FromFile(@"YOUR_DIRECTORY/chinese_contract.tif");
```

> **提示：** 若處理大規模工作，可考慮使用 `ImageStream.FromUrl` 從雲端儲存桶（Azure Blob、AWS S3）串流影像。相同的 `ocrEngine.Recognize` 呼叫不需更改程式碼即可使用。

## 第五步：執行 OCR – Extract Text Image

在設定好引擎、裝置與前處理後，我們最終呼叫 `Recognize`。此方法會回傳包含 OCR 結果的純文字字串。

```csharp
// Execute OCR using the configured engine and settings.
string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);

// Display the extracted text in the console.
Console.WriteLine(recognizedText);
```

**預期結果：** 主控台會印出合約中的中文文字，且無背景雜訊。若仍看到雜散符號，請再次確認已啟用 `RemoveBackground`，且影像未過度壓縮。

## 完整範例

將上述所有步驟整合，以下是一個可直接複製貼上至新 Console 專案的完整程式。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Gpu;

namespace RemoveBackgroundOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a GPU‑enabled OCR engine.
            using (var ocrEngine = new GpuOcrEngine())
            {
                // Step 2: Select the GPU device (0 = first GPU).
                ocrEngine.DeviceId = 0;

                // Step 3: Configure preprocessing – this is the core of remove background ocr.
                var recognitionSettings = new RecognitionSettings
                {
                    Language = Language.ChineseSimplified, // Change as needed.
                    PreprocessFilters = new[]
                    {
                        PreprocessFilter.Deskew,
                        PreprocessFilter.ContrastEnhance,
                        PreprocessFilter.RemoveBackground // Crucial for background removal.
                    }
                };

                // Step 4: Load the image you want to process.
                var imageStream = ImageStream.FromFile(@"YOUR_DIRECTORY/chinese_contract.tif");

                // Step 5: Perform OCR and get the extracted text.
                string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);

                // Step 6: Output the result.
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(recognizedText);
            }
        }
    }
}
```

將檔案儲存為 `Program.cs`，還原 NuGet 套件（`dotnet add package Aspose.OCR`），然後執行 `dotnet run`。你應該會在終端機看到已清理的 OCR 輸出。

## 常見問題與解答

### 這能用於中文以外的語言嗎？

當然可以。將 `Language.ChineseSimplified` 改為任何支援的語言，例如 `Language.English` 或 `Language.French`。相同的 **remove background ocr** 流程同樣適用。

### 如果有多張影像要處理該怎麼辦？

將 OCR 呼叫包在 `foreach` 迴圈中，重複使用同一個 `GpuOcrEngine` 實例。引擎會持續駐留在 GPU 上，避免每個檔案重新初始化的開銷。

```csharp
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY", "*.tif"))
{
    var stream = ImageStream.FromFile(file);
    string text = ocrEngine.Recognize(stream, recognitionSettings);
    // Save or log `text` as needed.
}
```

### 我的 GPU 較舊且不支援 CUDA 11+，還能執行嗎？

Aspose OCR 需要相容 CUDA 的 GPU。若使用舊版顯示卡，可改用 CPU 引擎（`OcrEngine`），但會失去速度提升。**remove background ocr** 濾鏡仍可使用，只是較慢。

### 如何驗證背景真的已被移除？

使用 `ocrEngine.SavePreprocessedImage(imageStream, "preprocessed.png")` 將前處理後的影像儲存至磁碟。開啟 PNG 後，你會看到只有字元保留的純白畫布——證明 **remove background ocr** 步驟已成功。

## 提示與最佳實踐

- **批次大小很重要：** 若處理上千頁，請將其分成 50–100 頁的批次，以控制 GPU 記憶體使用。  
- **監控 GPU 使用率：** 使用 `nvidia-smi` 等工具即時觀察記憶體消耗；若出現尖峰，可調整 `DeviceId` 或批次大小。  
- **微調濾鏡：** 有時僅 `ContrastEnhance` 即可；若文件已對齊，可嘗試關閉 `Deskew`。  
- **記錄日誌：** 捕捉 OCR 信心分數（`ocrEngine.LastResult.Confidence`），以標記低品質頁面供人工審核。

## 結論

你剛剛已掌握使用 Aspose OCR 在 GPU 上的 **remove background ocr**。透過選擇適當的 GPU 裝置、設定針對性的 **preprocess image ocr** 流程，並執行辨識步驟，即可可靠地從雜訊掃描中 **extract text image** 資料。上方完整且可執行的範例為你建立更大型文件處理管線奠定堅實基礎，無論是合約、發票或檔案照片皆適用。

準備好接受下一個挑戰了嗎？可將此方法與 Aspose 的 PDF 轉換工具結合，對整個 PDF 文件集執行 OCR，或嘗試平行 GPU 串流以達到大規模吞吐量。沒有極限—祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}