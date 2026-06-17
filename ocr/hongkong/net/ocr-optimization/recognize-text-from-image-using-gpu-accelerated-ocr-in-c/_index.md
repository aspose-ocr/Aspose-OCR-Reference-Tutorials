---
category: general
date: 2026-02-25
description: 使用 GPU 加速的 OCR 快速辨識影像文字。學習設定 GPU 模式、載入影像進行 OCR，並從 TIFF 中提取文字。
draft: false
keywords:
- recognize text from image
- set gpu mode
- gpu accelerated ocr
- load image for ocr
- extract text from tiff
language: zh-hant
og_description: 使用 GPU 加速的 OCR 即時辨識圖像文字。逐步 C# 教學，涵蓋設定 GPU 模式、載入 OCR 圖像，以及從 TIFF 提取文字。
og_title: 使用 GPU 加速 OCR 從圖像辨識文字 – C# 指南
tags:
- Aspose OCR
- C#
- GPU computing
title: 使用 GPU 加速的 OCR 在 C# 中辨識圖像文字
url: /zh-hant/net/ocr-optimization/recognize-text-from-image-using-gpu-accelerated-ocr-in-c/
---

and hand the heavy lifting to your GPU, turning a sluggish operation into a near‑instant one."

Translate.

Proceed similarly.

Make sure to keep **bold** formatting.

Proceed step by step.

Also code block placeholders remain.

Let's craft final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 GPU 加速 OCR 在 C# 中辨識影像文字

有沒有曾經需要 **辨識影像文字**，卻因為 CPU 在高解析度掃描上卡頓？你並不孤單。在許多實務專案中——例如發票數位化或舊報紙的保存——單一 TIFF 檔案就可能讓整條流水線停滯數分鐘。好消息是？Aspose.OCR 只要切換一下開關，就能把繁重的運算交給 GPU，將緩慢的處理變成近乎即時的速度。

在本教學中，我們將完整示範：如何 **設定 GPU 模式**、如何 **載入影像供 OCR 使用**，以及如何 **從 TIFF 檔案擷取文字**。完成後，你將擁有一個可直接放入任何 .NET 6+ 專案的完整、可投入生產的範例。

## 前置條件

在開始之前，請確保你已具備：

- 已安裝 .NET 6 SDK（或更新版本）。
- Visual Studio 2022 或你慣用的編輯器。
- 已於專案中加入 Aspose.OCR NuGet 套件（`Aspose.OCR`）。
- 支援 DirectX 11 或更新版本的 GPU（大多數現代顯示卡皆符合）。  
  *若沒有 GPU，也可以使用 `GpuMode.Auto` 執行程式碼——函式庫會自動回退至 CPU。*

> **專業提示：** 請確認你的 GPU 驅動程式為最新版本；過時的驅動程式可能會導致難以追蹤的初始化錯誤。

## 第一步 – 建立 OCR 引擎並設定 GPU 模式

首先需要建立 `OcrEngine` 的實例。此物件負責所有設定，包括是否使用 GPU。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Enable GPU acceleration.
            // Use GpuMode.Auto if you want the library to pick CPU when a GPU isn’t available.
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled);

            // The rest of the workflow continues below…
        }
    }
}
```

**為什麼重要：** 啟用 GPU 模式會將計算密集的影像前處理（二值化、除噪等）搬到顯示卡上。以中階 RTX 3060 為例，可獲得 **3‑5 倍** 的速度提升，較純 CPU 處理快許多。

## 第二步 – 載入影像供 OCR 使用（TIFF 範例）

Aspose.OCR 支援多種格式，但 TIFF 常用於掃描文件，因為它能保留無損品質。使用 `ImageStream.FromFile` 讀取檔案至記憶體。

```csharp
// Step 2: Load the high‑resolution TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"C:\Data\high_res_scan.tif");

// Optional: If you need to work with a stream (e.g., from a web API), use:
// ocrEngine.Image = ImageStream.FromStream(yourInputStream);
```

**邊緣情況：** 某些 TIFF 檔案包含多頁。`ImageStream.FromFile` 只會讀取第一頁。若需處理每一頁，請遍歷 `ImageInfo.Pages`，並將每頁分別送入引擎。

## 第三步 – 執行辨識

現在引擎已設定完成且影像已載入，呼叫 `Recognize()`。此方法會回傳 `OcrResult` 物件，內含純文字輸出與其他中繼資料。

```csharp
// Step 3: Run OCR
OcrResult result = ocrEngine.Recognize();

// The result may include confidence scores per line, if you enable them in the config.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

**如果文字呈現亂碼該怎麼辦？**  
- 確認影像方向正確（必要時旋轉）。  
- 調整前處理選項，例如 `ocrEngine.Config.DeskewEnabled = true;`。  
- 若文件為多語言，設定 `ocrEngine.Config.Language = Language.English;` 或相應的列舉值。

## 第四步 – 驗證輸出並處理錯誤

穩健的實作會檢查結果是否為 null，並捕捉可能的例外（例如缺少 GPU 驅動程式）。

```csharp
try
{
    OcrResult result = ocrEngine.Recognize();

    if (result?.Text == null)
    {
        Console.WriteLine("No text detected – double‑check the image quality.");
    }
    else
    {
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
catch (Exception ex)
{
    Console.WriteLine($"OCR failed: {ex.Message}");
    // You might want to fallback to CPU mode here:
    // ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
}
```

**為什麼要這樣包起來？** GPU 初始化若找不到必要的原生函式庫，會拋出 `DllNotFoundException`。此 catch 區塊提供了優雅的降級機制。

## 完整、可執行的範例

將上述步驟整合起來，以下是一個可直接編譯執行的完整程式。請將檔案路徑替換為你機器上的實際 TIFF 檔案。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // 1️⃣ Create OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled); // or GpuMode.Auto for fallback

            // 2️⃣ Load the image you want to process
            string imagePath = @"C:\Data\high_res_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Optional: tweak preprocessing (helps with noisy scans)
            ocrEngine.Config.DeskewEnabled = true;
            ocrEngine.Config.RemoveNoiseEnabled = true;

            // 4️⃣ Run recognition and handle the result
            try
            {
                OcrResult result = ocrEngine.Recognize();

                if (string.IsNullOrWhiteSpace(result?.Text))
                {
                    Console.WriteLine("No text found – consider improving image quality.");
                }
                else
                {
                    Console.WriteLine("=== Recognized Text ===");
                    Console.WriteLine(result.Text);
                }
            }
            catch (Exception e)
            {
                Console.WriteLine($"Error during OCR: {e.Message}");
                // Fallback to CPU if GPU failed
                ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
                // You could retry here…
            }
        }
    }
}
```

**預期輸出**

若 TIFF 含有可辨識的英文文字，會看到類似以下的結果：

```
=== Recognized Text ===
Invoice #12345
Date: 2024‑11‑08
Total Amount: $1,235.00
...
```

若影像為空白或無法辨識，主控台會提示你檢查來源檔案。

## 常見問題與變化

| 問題 | 答案 |
|----------|--------|
| **可以處理 JPEG 或 PNG 而不是 TIFF 嗎？** | 當然可以。`ImageStream.FromFile` 支援所有 Aspose.OCR 可處理的格式（PNG、JPEG、BMP 等）。 |
| **如果一個 TIFF 包含多頁該怎麼辦？** | 迭代 `ImageInfo.Pages`，在呼叫 `Recognize()` 前將每頁指派給 `ocrEngine.Image`。 |
| **使用 Aspose.OCR 需要授權嗎？** | 免費評估版可處理最多 100 頁。正式上線時請購買授權，以移除評估浮水印。 |
| **如何變更語言模型？** | 設定 `ocrEngine.Config.Language = Language.Spanish;`（或任何支援的列舉值）。 |
| **有辦法取得信心分數嗎？** | 開啟 `ocrEngine.Config.EnableConfidence = true;`，然後檢查 `result.Confidence`（每行的分數）。 |

## 結論

現在你已掌握如何在 C# 中使用 **GPU 加速的 OCR** 來 **辨識影像文字**。只要 **設定 GPU 模式**、**載入影像**，以及 **從 TIFF 檔案擷取文字**，就能建構一套快速、可擴充的解決方案，適用於真實工作負載。

接下來的步驟是什麼？可以將此程式碼與 PDF 產生器結合，製作可搜尋的 PDF，或將擷取的字串送入自然語言處理管線。亦可嘗試 `GpuMode.Auto`，讓你的應用在沒有 GPU 的環境下自動切換。

祝開發順利，願你的 OCR 執行如閃電般快速！

![辨識影像文字範例](https://example.com/ocr-demo.png "使用 GPU 加速 OCR 辨識影像文字")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}