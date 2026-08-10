---
category: general
date: 2026-06-06
description: 如何在 C# OCR 引擎中啟用 GPU，快速辨識圖像文字。學習如何執行 OCR、載入圖像進行 OCR，並在數分鐘內使用 C# OCR 引擎。
draft: false
keywords:
- how to enable gpu
- how to perform ocr
- recognize text from image
- load image for ocr
- use ocr engine c#
language: zh-hant
og_description: 如何在 C# OCR 引擎中啟用 GPU。本教學示範如何執行 OCR、載入影像以進行 OCR，並使用 C# OCR 引擎從影像中辨識文字。
og_title: 如何在 C# OCR 引擎中啟用 GPU – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to enable GPU in a C# OCR engine and quickly recognize text from
    image. Learn how to perform OCR, load image for OCR, and use OCR engine C# in
    minutes.
  headline: How to Enable GPU in C# OCR Engine – Complete Programming Guide
  type: TechArticle
tags:
- OCR
- C#
- GPU
title: 如何在 C# OCR 引擎中啟用 GPU – 完整程式設計指南
url: /zh-hant/net/ocr-optimization/how-to-enable-gpu-in-c-ocr-engine-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# OCR 引擎中啟用 GPU – 完整程式指南

有沒有想過在 C# 中執行 OCR 工作負載時 **如何啟用 GPU**？你並不是唯一遇到這個問題的人——開發者常常因為只有 CPU 的慢速處理而受阻，尤其是面對高解析度的掃描檔。  

好消息是？開啟 GPU 加速非常簡單，一旦啟動並運作，你就能在瞬間 **perform OCR**、**load image for OCR**、以及 **recognize text from image**。在本指南中，我們將逐步說明從安裝正確套件到列印最終文字的每個步驟，同時確保程式碼保持簡潔且可執行。  

我們也會討論幾個「如果…」情境：如果你有多張 GPU 呢？如果影像格式不受支援呢？完成後，你將擁有一段穩固、可投入生產環境的程式碼片段，完整示範 **how to enable GPU** 並取得可信賴的結果。

## 前置條件

- .NET 6.0 或更新版本（範例為簡潔起見使用 top‑level 陳述式）
- 支援 GPU 的 OCR 函式庫（例如 *MyOcrLib* – 請換成你的供應商命名空間）
- 至少一張已安裝驅動程式的 CUDA 相容 GPU
- 一張放在可參考資料夾中的範例影像（JPEG/PNG）

如果缺少上述任一項，請下載最新的 NVIDIA 驅動程式並加入 NuGet 套件：

```bash
dotnet add package MyOcrLib --version 2.3.1
```

現在，讓我們開始吧。

## 步驟 1：在你的 C# OCR 引擎中啟用 GPU

首先，你需要在引擎的設定物件上打開 GPU 開關。大多數現代 OCR SDK 皆提供 `Config` 屬性，你可以在其中設定 `GpuEnabled`、`GpuDeviceId`，以及可選的精度模式，以爭取額外的效能提升。

```csharp
// Create the OCR engine instance
var ocrEngine = new MyOcrLib.OcrEngine();

// Enable GPU acceleration
ocrEngine.Config.GpuEnabled = true;                     // Turn on GPU mode
ocrEngine.Config.GpuDeviceId = 0;                       // Choose the first GPU (0‑based index)
ocrEngine.Config.GpuPrecision = GpuPrecision.Float16; // Optional: lower precision for less memory usage
```

**為什麼這很重要：** GPU 加速會將繁重的矩陣運算從 CPU 移至圖形處理器，讓其平行處理成千上萬的像素。以中階 RTX 3060 為例，較 CPU 單獨模式可提升 3‑5 倍的速度。

> **專業提示：** 若你有多張 GPU，可嘗試設定 `GpuDeviceId = 1`（或更高）以在卡片之間平衡負載。

## 步驟 2：在 C# 中載入 OCR 影像

在引擎能讀取任何內容之前，你必須提供影像串流。SDK 通常提供類似 `ImageStream.FromFile` 的輔助方法。請確保路徑正確且檔案可存取。

```csharp
// Load the image you want to process
ocrEngine.Image = MyOcrLib.ImageStream.FromFile(@"C:\OCRSamples\sample1.jpg");

// Quick sanity check – ensure the image was loaded
if (ocrEngine.Image == null)
{
    Console.WriteLine("Failed to load image. Check the file path and format.");
    return;
}
```

**邊緣情況：** 某些函式庫無法處理 CMYK JPEG。若發生例外，請先使用 `System.Drawing` 或 `ImageSharp` 將影像轉換為 RGB。

## 步驟 3：設定語言並執行 OCR

大多數 OCR 引擎需要知道使用哪種語言模型。許多套件預設為英文，但只要更改一次 enum，即可切換至法文、西班牙文等。

```csharp
// Choose the language for recognition
ocrEngine.Language = OcrLanguage.English; // Change to OcrLanguage.Spanish for Spanish text
```

現在我們實際執行辨識流程。這就是 **how to perform OCR** 轉化為具體呼叫的時刻。

```csharp
// Run the OCR process – this will automatically use the GPU because we enabled it earlier
var ocrResult = ocrEngine.Recognize();
```

如果呼叫回傳 `null` 或拋出例外，請再次確認 GPU 驅動程式為最新，且模型檔案已放置於預期目錄。

## 步驟 4：從影像辨識文字並輸出結果

`Recognize` 方法會回傳一個物件，通常包含 `Text` 屬性以及每行的信心分數。讓我們把純文字印到主控台。

```csharp
// Output the recognized text
if (ocrResult?.Text != null)
{
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
else
{
    Console.WriteLine("OCR failed to produce any text.");
}
```

**你會看到的結果：** 若是清晰的掃描頁面，輸出應接近完美。若出現亂碼，請考慮提升影像 DPI（300 dpi 為最佳），或將 `GpuPrecision` 改回 `Float32` 以提升準確度。

### 預期的主控台輸出（範例）

```
=== OCR Output ===
The quick brown fox jumps over the lazy dog.
```

## 步驟 5：常見陷阱與效能調校

| 症狀 | 可能原因 | 解決方法 |
|---------|--------------|-----|
| **GPU 未被使用**（CPU 使用率飆升） | `GpuEnabled` 為 `false` 或缺少驅動程式 | 確認 `ocrEngine.Config.GpuEnabled` 為 `true`，並執行 `nvidia-smi` 以檢查程序 |
| **記憶體不足錯誤** | 在極大影像上使用 `Float16` | 改用 `GpuPrecision.Float32`，或在輸入前縮小影像 |
| **準確度低** | 語言模型錯誤或 DPI 太低 | 正確設定 `ocrEngine.Language`，並確保影像 DPI ≥300 |
| **多頁 PDF 崩潰** | 引擎只接受單一影像 | 對每一頁迴圈，於每次迭代建立新的 `ImageStream` |

**額外提示：** 若需保持 UI 響應，可將 OCR 呼叫包在 `Task.Run` 中。GPU 工作會在獨立執行緒上執行，但 .NET 執行緒池仍會阻塞，除非將其卸載。

```csharp
var ocrResult = await Task.Run(() => ocrEngine.Recognize());
```

## 步驟 6：完整可執行範例（可直接複製貼上）

以下是一個獨立的程式，你可以直接放入 Console 應用程式中。它包含 `using` 指令、錯誤處理，以及最後的 `Console.ReadKey()`，讓你在視窗關閉前看到輸出結果。

```csharp
using System;
using MyOcrLib;               // Replace with the actual namespace of your OCR library
using MyOcrLib.Enums;        // For GpuPrecision and OcrLanguage

// ------------------------------------------------------------
// How to Enable GPU, Load Image, Perform OCR, and Get Text
// ------------------------------------------------------------
var ocrEngine = new OcrEngine();

// 1️⃣ Enable GPU acceleration
ocrEngine.Config.GpuEnabled = true;
ocrEngine.Config.GpuDeviceId = 0;                 // First GPU
ocrEngine.Config.GpuPrecision = GpuPrecision.Float16;

// 2️⃣ Load the image for OCR
string imagePath = @"C:\OCRSamples\sample1.jpg";
ocrEngine.Image = ImageStream.FromFile(imagePath);

if (ocrEngine.Image == null)
{
    Console.WriteLine("❌ Unable to load image. Check the path.");
    return;
}

// 3️⃣ Set language (how to perform OCR)
ocrEngine.Language = OcrLanguage.English;

// 4️⃣ Run OCR – this uses the GPU because we enabled it
var ocrResult = ocrEngine.Recognize();

if (ocrResult?.Text != null)
{
    Console.WriteLine("\n=== Recognized Text ===");
    Console.WriteLine(ocrResult.Text);
}
else
{
    Console.WriteLine("\n⚠️ OCR returned no text.");
}

// Keep console open
Console.WriteLine("\nPress any key to exit...");
Console.ReadKey();
```

使用 `dotnet run` 執行程式，你應該會在主控台看到擷取的文字。若將 `imagePath` 換成其他檔案，同樣的流程仍可運作——只要在需要時調整語言即可。

## 結論

我們已說明如何在 C# OCR 引擎中 **how to enable GPU**，示範了 **load image for OCR** 的方法，解釋了 **how to perform OCR**，並展示了使用 `OCR engine C#` API 進行 **recognize text from image** 的最簡單方式。最後的完整範例將所有步驟串接起來，讓你可以直接複製貼上，立即看到 GPU 加速的文字擷取效果。

想更進一步嗎？試著將一批影像交給 `Parallel.ForEach` 迴圈處理，實驗不同的 `GpuPrecision` 設定，或切換至多語言模型，以擴充應用程式的功能。  

如果遇到任何問題或有改進想法，歡迎留言——祝程式開發愉快！  

![如何在 OCR 引擎中啟用 GPU](/images/ocr-gpu-setup.png "顯示 GPU 啟用 OCR 流程圖 – how to enable gpu")

---

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [如何 OCR 影像 – 在 OCR 影像辨識中執行 OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [如何使用 Aspose 從串流辨識影像於 OCR 影像辨識](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [如何設定閾值於 OCR 影像辨識](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}