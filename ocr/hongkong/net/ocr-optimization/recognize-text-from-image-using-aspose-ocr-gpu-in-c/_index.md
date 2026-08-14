---
category: general
date: 2026-02-20
description: 使用 Aspose OCR 的 GPU 加速快速辨識圖像文字。學習如何在 C# 中從掃描檔提取文字，並提供完整可執行的範例。
draft: false
keywords:
- recognize text from image
- extract text from scan
- Aspose OCR GPU
- C# OCR tutorial
- image to text conversion
language: zh-hant
og_description: 使用 GPU 加速從圖片辨識文字。本教學示範如何在 C# 中使用 Aspose OCR 從掃描檔提取文字，並提供完整程式碼與技巧。
og_title: 使用 Aspose OCR GPU 從圖像辨識文字 – C# 指南
tags:
- Aspose
- OCR
- C#
- GPU
title: 在 C# 中使用 Aspose OCR GPU 從圖像辨識文字
url: /zh-hant/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu-in-c/
---

於 C# 進行影像文字辨識". Keep capitalisation? We'll translate natural.

Now paragraph.

We'll translate each paragraph.

Let's craft translation.

Be careful with code placeholders.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR GPU 於 C# 進行影像文字辨識

是否曾經需要 **從影像中辨識文字**，但檔案太大導致 CPU 卡頓？或是你嘗試過傳統的 OCR 函式庫，結果耗時過久、辨識結果斷斷續續。好消息是：透過 Aspose OCR 的 GPU 加速，你可以在數秒內將巨大的掃描 TIFF 轉換成乾淨、可搜尋的文字。

本指南將一步步示範一個完整、可直接複製貼上的範例，教你如何在支援 GPU 的機器上 **從掃描檔案中擷取文字**。不會有模糊的說明，只有你需要的程式碼、每行程式碼的意義說明，以及避免踩雷的小技巧。

## 你需要的環境

- **.NET 6+**（或 .NET Framework 4.7+ – API 使用方式相同）
- **Aspose.OCR for .NET** NuGet 套件（版本 23.12 或更新）
- 支援 CUDA 的 **GPU**（非必要，但可大幅提升速度）
- 高解析度的掃描影像（例如 `large_doc.tif`）

如果沒有 GPU，引擎會自動回退至 CPU——仍可執行範例，只是速度較慢。

## 步驟 1 – 安裝 Aspose.OCR 套件

在終端機或 Package Manager Console 中執行：

```bash
dotnet add package Aspose.OCR
```

或是在 Visual Studio 的 NuGet UI 中搜尋 **Aspose.OCR**，然後點選 *Install*。這會同時安裝核心 OCR 程式庫以及可選的 GPU 加速組件。

> **小技巧：** 安裝完成後，請檢查 `packages` 資料夾內是否有 `Aspose.OCR.Acceleration.dll`。此檔案是 GPU 支援所必需的；若你在無圖形介面的伺服器上執行，可省略它，程式仍能編譯。

## 步驟 2 – 初始化 GPU 加速的 OCR 引擎

`GpuOcrEngine` 類別會自動偵測相容的 GPU。若有多張裝置，你可以指定特定的 GPU，但大多數開發者只需要讓它自行選擇。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration;   // <-- enables GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Create the OCR engine. It will look for a CUDA‑compatible GPU.
        GpuOcrEngine ocrEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Force a particular GPU device.
        // Uncomment the line below if you know the device ID you want to use.
        // ocrEngine.Device = GpuDevice.GetById(0);
```

**為什麼這很重要：** 只在程式啟動時初始化一次 GPU 引擎，可降低額外開銷。如果在迴圈內不斷建立與銷毀引擎，將失去效能優勢。

## 步驟 3 – 載入高解析度的掃描影像

Aspose OCR 使用 `System.Drawing.Image`。請確保檔案路徑指向真實的影像，否則會拋出 `FileNotFoundException`。

```csharp
        // Step 3: Load the image you want to process.
        // Replace YOUR_DIRECTORY with the actual folder on your machine.
        var scannedImage = Image.FromFile(@"YOUR_DIRECTORY/large_doc.tif");
```

> **例外情況：** 若影像尺寸超過 10 000 × 10 000 px，建議先做降採樣。GPU 記憶體有限，直接載入過大的位圖可能導致 `OutOfMemoryException`。

## 步驟 4 – 使用預設（Latin）語言設定執行 OCR

`Recognize` 方法會回傳純文字字串。若需要其他語言或自訂前處理，可傳入 `OcrOptions` 物件。

```csharp
        // Step 4: Run OCR. By default it assumes Latin script.
        string recognizedText = ocrEngine.Recognize(scannedImage);
```

**為什麼預設即可運作：** 大多數掃描文件（合約、發票、報告）皆使用拉丁字母系統。若需辨識西里爾、阿拉伯或中文等語系，請在呼叫 `Recognize` 前設定 `ocrEngine.Language = "ru"`（或相對應的 ISO 代碼）。

## 步驟 5 – 顯示或儲存擷取出的文字

為了快速驗證，我們僅將結果寫入主控台。實際應用中，你可能會將文字寫入資料庫、`.txt` 檔，或送入搜尋索引。

```csharp
        // Step 5: Output the OCR result.
        Console.WriteLine(recognizedText);

        // Optional: Save to a file.
        // File.WriteAllText(@"output.txt", recognizedText);
    }
}
```

### 預期輸出

若 `large_doc.tif` 只包含簡單段落「Hello, world!」，主控台會顯示：

```
Hello, world!
```

對於多頁掃描，引擎會依閱讀順序串接文字。若需要分頁資訊，可之後依換行符號（`\n`）切割。

## 常見問題處理

| 問題 | 徵象 | 解決方式 |
|------|------|----------|
| **未偵測到 GPU** | `ocrEngine.Device` 為 `null`，處理速度緩慢。 | 安裝最新的 NVIDIA 驅動程式與 CUDA Toolkit（v11 以上），並以 `nvidia-smi` 確認裝置。 |
| **垃圾回收延遲** | 處理大量影像後記憶體急升。 | 在 OCR 完成後呼叫 `scannedImage.Dispose()`，或將影像包在 `using` 區塊中。 |
| **語言設定錯誤** | 非拉丁文字出現亂碼。 | 在 `Recognize` 前設定正確的 ISO 639‑1 語言代碼，例如 `ocrEngine.Language = "zh"`。 |
| **檔案過大** | `OutOfMemoryException`。 | 使用 `Image.GetThumbnailImage` 降採樣，或將掃描切割成多塊處理。 |

## 完整、可直接執行的範例

以下程式碼包含 `using` 指示、錯誤處理，以及使用 `using` 區塊確保影像釋放：

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration; // GPU support

class GpuOcrDemo
{
    static void Main()
    {
        try
        {
            // Initialize the GPU‑accelerated OCR engine.
            GpuOcrEngine ocrEngine = new GpuOcrEngine();

            // OPTIONAL: Choose a specific GPU device.
            // ocrEngine.Device = GpuDevice.GetById(0);

            // Load the high‑resolution scanned image.
            string imagePath = @"YOUR_DIRECTORY/large_doc.tif";
            if (!File.Exists(imagePath))
                throw new FileNotFoundException($"Image not found: {imagePath}");

            using (Image scannedImage = Image.FromFile(imagePath))
            {
                // Perform OCR (defaults to Latin script).
                string text = ocrEngine.Recognize(scannedImage);

                // Output the extracted text.
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(text);

                // Save to a text file (optional).
                string outputPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(outputPath, text);
                Console.WriteLine($"Text saved to {outputPath}");
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### 程式碼說明

1. **建立** `GpuOcrEngine`，自動挑選最佳 GPU。  
2. **載入** 目標 TIFF，放在 `using` 區塊內以保證釋放。  
3. **呼叫** `Recognize`，將位圖轉換為字串。  
4. **寫入** 結果至主控台與來源影像同目錄下的 `.txt` 檔。  
5. **捕捉** 任何例外並顯示友善的錯誤訊息。

## 更進一步 – 從「影像文字辨識」到完整文件流水線

既然已能 **從掃描檔案中擷取文字**，可以考慮以下延伸：

- **批次處理：** 迴圈掃描整個 TIFF 資料夾，將結果彙整至單一可搜尋索引。  
- **語言偵測：** 使用 `ocrEngine.DetectLanguage()`（若支援）自動切換語系。  
- **後處理：** 透過拼字檢查或正規表達式過濾 OCR 產生的雜訊。  
- **與 Azure Cognitive Search 整合：** 將擷取的文字推送至雲端搜尋索引，實現即時查詢。

上述每一步都遵循相同的核心模式：一次初始化，引擎持續接收影像，收集文字。

## 結論

你已學會如何在 C# 中使用 Aspose OCR 的 GPU 加速引擎 **辨識影像文字**。完整、可執行的範例示範了如何設定引擎、載入高解析度掃描、執行 OCR，並處理輸出。依照上述技巧與例外處理，你可以避免常見陷阱，無論在開發筆記本或正式伺服器上，都能取得可靠的結果。

準備好將更多掃描檔轉換為可搜尋資料了嗎？試著批次處理整個資料夾、實驗非拉丁語系，或將結果匯入全文搜尋引擎。未來的可能性無限，而你剛寫好的程式碼正是堅實的基礎。

祝開發順利！ 🚀

![辨識影像文字範例](/images/ocr-gpu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}