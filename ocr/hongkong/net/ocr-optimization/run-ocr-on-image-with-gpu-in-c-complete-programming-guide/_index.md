---
category: general
date: 2026-03-26
description: 使用 Aspose OCR GPU 支援於 C# 進行影像文字辨識。學習如何載入影像進行 OCR、設定 GPU 裝置 ID，並快速從影像中擷取文字。
draft: false
keywords:
- run OCR on image
- extract text from image
- load image for OCR
- recognize text from document
- set GPU device ID
language: zh-hant
og_description: 使用 Aspose OCR GPU 於 C# 執行影像光學字符辨識（OCR）。本指南說明如何載入影像進行 OCR、設定 GPU 裝置
  ID，並高效擷取影像中的文字。
og_title: 在 C# 中使用 GPU 執行圖像 OCR – 完整指南
tags:
- C#
- OCR
- GPU
- Aspose
title: 在 C# 中使用 GPU 執行影像 OCR – 完整程式設計指南
url: /zh-hant/net/ocr-optimization/run-ocr-on-image-with-gpu-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中使用 GPU 執行影像 OCR – 完整程式指南

有沒有曾經需要 **run OCR on image** 檔案，但發現 CPU 版慢得令人痛苦？你並不孤單。在許多實務應用中——例如發票掃描器或大規模文件檔案庫——瓶頸往往就在 OCR 引擎本身。  

在本教學中，我們將逐步示範一個 **完整且可執行的範例**，說明如何 **載入影像以進行 OCR**、可選地 **設定 GPU 裝置 ID**，最後使用 Aspose OCR 的 GPU 加速 API **從影像擷取文字**。完成後，你將能在純 CPU 方法所需時間的一小部分內 **辨識文件中的文字** 影像。

## 你將學到什麼

- 如何安裝與參考 Aspose.OCR 與 Aspose.OCR.Gpu 套件。  
- 使用 GPU 加速的 **執行影像 OCR** 的完整步驟。  
- 為何在多 GPU 機器上選擇正確的 **GPU device ID** 如此重要。  
- 處理大型檔案、備援策略與常見陷阱的技巧。  

### 前置條件

| 需求 | 原因 |
|-------------|--------|
| .NET 6.0 or later | 現代語言功能與更佳效能 |
| Visual Studio 2022 (or any C# IDE) | 便於建立專案 |
| NVIDIA GPU with CUDA support (optional) | 僅在需要 GPU 加速時才必須 |
| Aspose.OCR & Aspose.OCR.Gpu NuGet packages | 提供 `GpuOcrEngine` 類別 |

如果沒有 GPU，也別慌——程式碼會優雅地回退至 CPU 引擎，我們稍後會說明。

---

## 步驟 1：安裝 Aspose OCR 套件

在能 **run OCR on image** 之前，你需要先安裝這些函式庫。打開終端機（或套件管理員主控台）並執行：

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

這兩個套件會加入核心 OCR 引擎與 GPU 專屬擴充功能。安裝完成後，你會在 `.csproj` 中看到以下參考：

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
  <PackageReference Include="Aspose.OCR.Gpu" Version="23.10.0" />
</ItemGroup>
```

> **Pro tip:** 保持套件版本同步；版本不匹配可能導致執行時錯誤。

---

## 步驟 2：建立 GPU 加速的 OCR 引擎

現在函式庫已就緒，讓我們使用 GPU **執行影像 OCR**。`GpuOcrEngine` 類別是加速處理的入口點。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Instantiate the GPU OCR engine
        var gpuEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Choose which GPU to use – 0 = first GPU
        // This is where the "set GPU device ID" keyword comes into play.
        gpuEngine.DeviceId = 0;

        // The rest of the workflow continues in the following steps...
```

**為何使用 GPU？**  
GPU 核心擅長平行像素運算，這正是 OCR 在掃描高解析度影像時所需的。透過設定 `DeviceId`，你可以告訴函式庫使用哪張實體卡片——在多 GPU 工作站上相當方便。

---

## 步驟 3：載入影像以進行 OCR

在辨識之前，你必須 **載入影像以進行 OCR**。Aspose 提供便利的靜態工廠方法，支援多種格式（JPEG、PNG、TIFF 等）。

```csharp
        // Step 3: Load the image you want to recognize
        // Replace the path with your actual file location.
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");

        // Quick sanity check – ensure the image was loaded.
        if (ocrImage == null)
        {
            Console.WriteLine("Failed to load image. Check the file path.");
            return;
        }
```

> **Edge case:** 若影像大於 10 MB，建議先縮小尺寸以避免 GPU 記憶體耗盡。可在辨識前使用 `ocrImage.Resize(width, height)` 進行縮放。

---

## 步驟 4：從文件辨識文字

引擎已就緒且影像已載入，現在可以 **辨識文件中的文字**。`Recognize` 方法會回傳 `OcrResult` 物件，內含純文字輸出與其他中繼資料。

```csharp
        // Step 4: Run the OCR process on the image
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);

        // Verify that OCR succeeded
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR failed or returned empty result.");
            return;
        }
```

**底層發生了什麼？**  
GPU 引擎將像素資料傳送至 CUDA 核心，執行二值化、字元分割與神經網路推論——全部平行處理。這就是為何你可以 **執行影像 OCR** 檔案，而在 CPU 上則需要數秒。

---

## 步驟 5：從影像擷取文字並輸出

最後，我們 **擷取影像文字** 並顯示。你也可以將結果寫入檔案、資料庫，或傳入後續的 NLP 流程。

```csharp
        // Step 5: Output the recognized plain‑text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // Optional: Save to a .txt file for later processing
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }
}
```

**預期輸出**（為簡潔起見已截斷）：

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

如果執行程式後看到類似的區塊，恭喜你——已成功 **執行影像 OCR** 並使用 GPU 加速！

---

## 處理沒有 GPU 的情況（備援）

如果部署的機器沒有相容的 GPU 會怎樣？`GpuOcrEngine` 建構子會拋出 `GpuNotSupportedException`。將初始化包在 try‑catch 中，並回退至 `OcrEngine`（CPU），如下所示：

```csharp
        try
        {
            var gpuEngine = new GpuOcrEngine { DeviceId = 0 };
            // Continue with GPU workflow...
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not available – switching to CPU OCR.");
            var cpuEngine = new OcrEngine();
            OcrResult result = cpuEngine.Recognize(ocrImage);
            Console.WriteLine(result.Text);
        }
```

此模式可確保應用程式不論硬體如何皆能正常運作，這對雲端部署尤為重要。

---

## 完整可執行範例（可直接複製貼上）

以下是 **完整程式**——完整無遺，只需將檔案路徑換成自己的即可。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Create a GPU‑enabled OCR engine
        GpuOcrEngine gpuEngine;
        try
        {
            gpuEngine = new GpuOcrEngine { DeviceId = 0 }; // set GPU device ID
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not detected. Falling back to CPU engine.");
            var cpuEngine = new OcrEngine();
            RunCpuOcr(cpuEngine);
            return;
        }

        // 2️⃣ Load image for OCR
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        if (ocrImage == null)
        {
            Console.WriteLine("Unable to load image – check the path.");
            return;
        }

        // 3️⃣ Recognize text from document
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR returned no text.");
            return;
        }

        // 4️⃣ Extract text from image and output
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }

    // Helper for CPU fallback
    static void RunCpuOcr(OcrEngine cpuEngine)
    {
        var img = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        var result = cpuEngine.Recognize(img);
        Console.WriteLine("=== CPU OCR Result ===");
        Console.WriteLine(result.Text);
    }
}
```

> **Note:** 上述程式碼會自動 **擷取影像文字** 並寫入 `ocr_result.txt`。請依需求調整路徑。

---

## 常見問題與技巧

| 問題 | 答案 |
|----------|--------|
| *我需要特定的 NVIDIA 驅動程式嗎？* | 是——建議使用 CUDA 11.x 或更新版本。請查閱 Aspose 的發行說明以取得確切相容性資訊。 |
| *我可以同時處理多張影像嗎？* | 當然可以。將 OCR 呼叫包在 `Parallel.ForEach` 迴圈中，但需留意 GPU 記憶體限制。 |
| *如果 OCR 結果出現亂碼該怎麼辦？* | 可嘗試調整影像前處理：在辨識前使用 `ocrImage.Binarize()` 或 `ocrImage.Deskew()`。 |
| *有沒有方法限制語言模型？* | 若僅需英文，可設定 `gpuEngine.Language = OcrLanguage.English;` 以加速處理。 |

---

## 結論

你現在擁有一個 **完整、端到端的解決方案** 以 **執行影像 OCR**。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}