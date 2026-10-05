---
category: general
date: 2026-01-01
description: 如何在 C# 中使用 Aspose OCR 引擎批量執行 OCR。學習如何從圖像辨識文字，並利用 GPU 加速從 TIFF 檔案提取文字。
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from TIFF
language: zh-hant
og_description: 如何在 C# 中使用 Aspose OCR 引擎批量 OCR。本指南將向您展示如何從圖像識別文字，並高效地從 TIFF 檔案中提取文字。
og_title: 如何在 C# 中批量 OCR – 完整 Aspose 指南
tags:
- OCR
- C#
- Aspose
- GPU
title: 如何在 C# 中使用 Aspose OCR 引擎批量執行 OCR
url: /zh-hant/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose OCR 引擎批量 OCR

有沒有想過 **如何批量 OCR**，當你有數十份掃描文件放在資料夾中時？你並不孤單——許多開發者在從單張影像辨識轉向處理整個集合時會卡在這裡。好消息是 Aspose OCR 讓這變得輕而易舉，無論你是使用 CPU 還是利用 GPU 加速。

在本教學中，我們將逐步說明一個完整且可執行的範例，該範例 **從影像辨識文字**，甚至 **批量從 TIFF 檔案提取文字**。不會有模糊的「請參閱文件」捷徑——只提供一個可自行複製貼上並立即執行的完整解決方案。

## 前置條件

* 已安裝 .NET 6.0 或更新版本（程式碼以 .NET 6 為目標，但 .NET 5 亦可運作）。
* Aspose.OCR for .NET NuGet 套件（提供 CPU 與 GPU 版本；請安裝與硬體相符的版本）。
* 一個資料夾，內含幾個想要處理的範例 TIFF 或 PNG 檔案。
* Visual Studio 2022 或任何你偏好的 IDE。

> **專業提示：** 若你打算使用 GPU 版，請確認顯示卡驅動程式已更新至最新，且已安裝 CUDA 11 以上。若找不到相容的 GPU，引擎會自動回退至 CPU。

## 第一步 – 設定專案並安裝 Aspose.OCR

### H2: 建立新 Console 應用程式並加入 Aspose.OCR

在終端機（或 Visual Studio 的套件管理員主控台）中開啟並執行：

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

如果你擁有 GPU 授權，請改為加入 GPU 套件：

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

就這樣——你的專案現在已參考我們將用於 **批量 OCR** 的 OCR 函式庫。

## 第二步 – 初始化 OCR 引擎（CPU 或 GPU）

### H2: 如何批量 OCR – 引擎初始化

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**為何重要：** 透過切換 `UseGpu`，讓 Aspose 決定最快的路徑。若 GPU 不可用，引擎會靜默切換回 CPU，避免因硬體缺失而導致批次作業崩潰。

## 第三步 – 收集要處理的檔案

### H2: 從影像辨識文字 – 建立檔案清單

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**邊緣情況說明：** 若有混合格式，請將搜尋模式改為 `"*.*"`，並在迴圈內依副檔名過濾。這樣可保持批次的彈性。

## 第四步 – 處理每張影像並顯示預覽

### H2: 從 TIFF 提取文字 – 逐檔迴圈

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**你會看到的結果：** 每個 TIFF，主控台會印出類似以下內容：

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```

此預覽可確認批次成功執行，且無需手動開啟每個檔案。

## 第五步 – 儲存結果（可選但實用）

### H3: 將 OCR 輸出持久化為文字檔

若需要完整文字供後續處理，請在 `foreach` 迴圈內加入以下程式碼：

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

現在每個 TIFF 會產生相對應的 `.txt` 檔，內含完整的 OCR 輸出——非常適合索引、搜尋或餵入語言模型。

## 第六步 – 執行示範並驗證

1. 建置專案：`dotnet build`。
2. 執行：`dotnet run --project GpuBatchDemo.csproj`。

你應該會在主控台看到預覽行，且（若已加入可選步驟）會在來源影像旁產生一系列 `.txt` 檔案。

### H3: 常見問題與解決方法

| 症狀 | 可能原因 | 解決方式 |
|---------|--------------|-----|
| **`ocrResult.Text` 為空** | 影像過暗或 DPI 太低 | 預先處理影像（提升對比、放大）或設定 `ocrEngine.Settings.PreprocessImage = true`。 |
| **GPU 錯誤「CUDA driver version is insufficient」** | 驅動程式過舊 | 更新 GPU 驅動程式，或設定 `UseGpu = false` 強制使用 CPU。 |
| **例外「File not found」** | Linux/macOS 上的路徑分隔符錯誤 | 使用 `Path.Combine` 或正斜線 (`/`)。 |

## 第七步 – 擴展規模（超過少量檔案）

當你從少量 TIFF 擴展到數千個時，請考慮：

* **平行處理：** 將 `foreach` 包裝在 `Parallel.ForEach` 中（確保引擎實例是執行緒安全的；否則每個執行緒建立一個實例）。
* **分塊 I/O：** 分批讀取影像，以免耗盡記憶體。
* **記錄日誌：** 將進度寫入日誌檔案；有助於在崩潰後恢復。

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **請記住：** GPU 記憶體是共享的，過多平行 GPU 工作會實際降低效能。請先以少量執行緒測試。

## 完整可執行範例（可直接複製貼上）

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

執行此程式將 **從影像辨識文字**、**從 TIFF 提取文字**，並有效示範 **如何批量 OCR**。

---

## 結論

現在你已擁有一個完整、端對端的 **如何在 C# 中使用 Aspose OCR 引擎批量 OCR** 範例。教學涵蓋了從設定專案、切換 GPU 加速、建立檔案清單、處理每張影像，到持久化結果的全部步驟。無論是從 TIFF 檔案或其他影像格式提取文字，都可套用相同模式——只需更換檔案副檔名。

準備好進一步了嗎？試著將 OCR 輸出整合至搜尋索引、餵入大型語言模型，或透過平行處理縮短大量批次的處理時間。沒有任何限制，而你已具備了構建的基礎。

有任何問題或想分享自己的批量 OCR 技巧嗎？在下方留言吧——祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}