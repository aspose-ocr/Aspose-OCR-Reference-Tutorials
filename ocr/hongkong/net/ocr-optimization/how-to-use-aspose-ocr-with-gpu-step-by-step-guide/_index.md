---
category: general
date: 2026-02-09
description: 如何在 C# 中使用 Aspose OCR 進行 GPU 加速。學習從 jpg 識別文字、從圖像提取文字，並在短短幾分鐘內啟用 GPU。
draft: false
keywords:
- how to use aspose
- recognize text from jpg
- extract text from image
- how to enable gpu
- how to set gpu
language: zh-hant
og_description: 如何在 C# 中使用 Aspose OCR 搭配 GPU。本指南將示範如何從 JPG 辨識文字，並使用 GPU 加速從影像中提取文字。
og_title: 如何使用 Aspose OCR 搭配 GPU – 完整程式設計指南
tags:
- Aspose
- OCR
- C#
- GPU Acceleration
title: 如何使用 Aspose OCR 搭配 GPU – 步驟指南
url: /zh-hant/net/ocr-optimization/how-to-use-aspose-ocr-with-gpu-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR 搭配 GPU – 完整程式開發指南

有沒有遇過要在瞬間處理一堆掃描發票，卻被 CPU 卡住的情況？這正是大規模使用 **how to use aspose** 進行 OCR 時的常見痛點。在本教學中，我們會示範一個真實案例，說明 **how to use aspose** 如何從 jpg 檔案辨識文字、從影像中抽取文字，並將 GPU 的效能發揮到極致。

把它想成咖啡休息時間的快速導覽——沒有冗長說明，只有可以直接複製貼上到 Visual Studio 的程式碼，讓你立刻看到效果。完成後，你將擁有一個自包含的 C# 主控台應用程式，能在任何搭配 NVIDIA 或 AMD GPU 的現代 Windows 電腦上執行。

![how to use aspose OCR with GPU](/images/aspose-gpu-example.png)

## 你需要的環境

- **.NET 6.0**（或更新）——程式碼以 .NET 6 為目標，但只要稍作調整，也能在 .NET 5 與 .NET Framework 4.8 上執行。
- **Aspose.OCR for .NET** NuGet 套件——使用 `dotnet add package Aspose.OCR` 安裝。
- 一台 **支援 GPU** 的機器——本教學會說明 **how to enable gpu** 與 **how to set gpu** 記憶體上限的設定方式，若找不到相容的 GPU，程式會自動回退至 CPU。
- 一張如 `invoice_01.jpg` 的影像，放在可供參照的資料夾內。

都備妥了嗎？好，讓我們開始吧。

## How to Use Aspose OCR with GPU – 初始設定

首先要做的事是建立 OCR 引擎的實例，並告訴它使用 GPU。這一步相當關鍵，因為若未設定此旗標，Aspose 會預設使用 CPU 處理，失去效能提升的意義。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 1: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the core of **how to use aspose** with a graphics card
ocrEngine.Configuration.UseGpu = true;

// Optional: limit GPU memory to avoid OOM on low‑end cards
ocrEngine.Configuration.GpuMemoryLimit = 1024; // in MB
```

**為什麼這很重要：** 啟用 GPU 後，繁重的影像處理核心會搬到圖形處理器上執行，對於大型影像而言，速度可提升 10‑20 倍。`GpuMemoryLimit` 是安全閥；將其設為 1024 MB 在大多數中階顯卡上都能保持程式回應。

> **小技巧：** 若在沒有相容 GPU 的機器上執行，Aspose 會自動切換回 CPU 模式並寫入警告。程式不會當機，只是執行較慢。

## 從 JPG 辨識文字 – 載入影像

引擎已就緒，接下來要把影像餵給它。範例使用 JPEG，因為 **recognize text from jpg** 是發票、收據與護照等常見情境。

```csharp
// Step 2: Load the JPEG image you want to process
// Replace the path with the location of your own image
var inputImage = ImageStream.FromFile(@"C:\OCR\Samples\invoice_01.jpg");

// Verify that the file exists (helps avoid a FileNotFoundException)
if (!System.IO.File.Exists(@"C:\OCR\Samples\invoice_01.jpg"))
{
    Console.WriteLine("Image file not found. Check the path and try again.");
    return;
}
```

**為什麼要檢查檔案：** 缺少檔案是快速示範中最常見的執行時錯誤。提前處理可讓教學更友善初學者。

## 從影像抽取文字 – 執行 OCR 引擎

取得影像後，接下來就是真正執行 OCR 的步驟。Aspose 會在此完成繁重運算，並回傳一個 `OcrResult` 物件，內含純文字、信心分數，甚至在需要時的邊界框資訊。

```csharp
// Step 3: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Step 4: Output the extracted plain‑text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.PlainText);
```

**你會看到什麼：** 主控台會印出 Aspose 偵測到的原始字元。例如對於一張乾淨的發票，可能會得到：

```
=== Extracted Text ===
Invoice #: 2023‑00123
Date: 02/08/2023
Total: $1,245.67
...
```

如果輸出看起來雜亂，可能需要調整影像品質或啟用額外的前處理選項（例如去斜、二值化）。這些超出本快速指南範圍，但可在 Aspose API 參考文件中找到說明。

## 如何啟用 GPU – 設定引擎

如果你錯過了第一步，想知道 **how to enable gpu**，只要在引擎的設定物件上切換 `UseGpu` 旗標即可，如前述程式碼所示。以下是一段精簡片段，可直接放入任何既有專案：

```csharp
ocrEngine.Configuration.UseGpu = true;   // Enables GPU
```

在背後，Aspose 會載入與硬體相符的原生 CUDA/OpenCL 函式庫。若執行時找不到相應檔案，會寫入警告並回退至 CPU。大多數 Windows 環境不需要額外安裝步驟。

## 如何設定 GPU – 微調記憶體使用

在低階 GPU 上，有時會碰到「記憶體不足」的錯誤。這時 **how to set gpu** 記憶體上限的設定就派上用場。`GpuMemoryLimit` 屬性接受以 MB 為單位的整數。

```csharp
// Example: restrict GPU usage to 512 MB
ocrEngine.Configuration.GpuMemoryLimit = 512;
```

**何時調整：** 若同時處理多張影像，建議降低上限以避免顯卡飽和。相反地，若工作站配備 8 GB VRAM，則可安全提升至 4096 MB，以加速批次處理。

## 完整可執行範例

以下是可直接複製到新建主控台專案（`dotnet new console`）的完整程式碼，包含前述所有片段與少量錯誤處理，使其更具韌性。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Create the OCR engine and enable GPU
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.Configuration.UseGpu = true;            // how to enable gpu
        ocrEngine.Configuration.GpuMemoryLimit = 1024;   // how to set gpu

        // -------------------------------------------------
        // Step 2: Load the JPEG image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\OCR\Samples\invoice_01.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }

        var inputImage = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // Step 3: Run the OCR engine
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 4: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

**預期輸出：** 執行 `dotnet run` 後，主控台會印出從 `invoice_01.jpg` 抽取的原始文字。若影像內的文字清晰，結果應與原始文件幾乎相同。

## 常見陷阱與避免方式

| 問題 | 為何會發生 | 快速解決方案 |
|------|------------|--------------|
| **GPU 未偵測到** | 缺少 CUDA 驅動或 GPU 不支援 | 安裝最新的 NVIDIA/AMD 驅動；使用 `nvidia-smi` 或等效指令確認 |
| **記憶體不足錯誤** | `GpuMemoryLimit` 設定過高 | 降低上限至 512 MB 或更低 |
| **輸出雜訊** | JPG 解析度低或壓縮過度 | 使用較高品質的原始影像或啟用 `ocrEngine.Preprocessing.Deskew = true` |
| **`ocrResult` 為 null** | 影像串流載入失敗 | 再次確認檔案路徑，確保檔案未被鎖定 |

提前處理這些問題，可避免日後追蹤難懂的堆疊追蹤訊息。

## 往後的發展方向

掌握 **how to use aspose** 進行高速 OCR 後，你可以進一步探索：

- **批次處理** – 迴圈遍歷整個 JPG 目錄，將每個結果寫入 `.txt` 檔案。
- **結構化抽取** – 使用 `ocrResult.Regions` 取得邊界框，提取發票號碼等特定欄位。
- **混合 CPU/GPU 模式** – 小尺寸影像使用 CPU，僅對大型檔案切換至 GPU，以平衡速度與記憶體需求。

以上所有延伸功能皆建立在剛才設定的基礎上，是你下一篇教學的絕佳題材。

---

*祝開發順利！若遇到任何問題，歡迎在下方留言或前往 Aspose 社群論壇討論。GPU 已就緒——讓 OCR 變得閃電般快速。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}