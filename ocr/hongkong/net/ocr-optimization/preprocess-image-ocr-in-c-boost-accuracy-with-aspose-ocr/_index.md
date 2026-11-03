---
category: general
date: 2026-01-01
description: 預處理圖像 OCR 以提升準確度。了解如何辨識文字圖像、提升 OCR 準確度、載入圖像 OCR 並使用 Aspose OCR 顯示 OCR
  文字。
draft: false
keywords:
- preprocess image ocr
- recognize text image
- improve ocr accuracy
- display ocr text
- load image ocr
language: zh-hant
og_description: 預處理圖像 OCR 以提升準確度。本指南展示如何辨識文字圖像、載入圖像 OCR、套用濾鏡，以及顯示 OCR 文字。
og_title: 預處理圖像 OCR（C#）– 使用 Aspose OCR 提升準確度
tags:
- Aspose OCR
- C#
- Image preprocessing
title: 在 C# 中預處理圖像 OCR – 使用 Aspose OCR 提升準確度
url: /zh-hant/net/ocr-optimization/preprocess-image-ocr-in-c-boost-accuracy-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# preprocess image ocr in C# – 使用 Aspose OCR 提升準確度

有沒有想過如何 **preprocess image ocr**，讓引擎真的能讀取頁面上的內容？你並不孤單——大多數開發者在面對雜訊多、傾斜的掃描圖時都會卡住。好消息是，只要採取幾個聰明的前處理步驟，就能把災難級的影像變成乾淨、可讀的文字。

在本教學中，我們將逐步示範一個完整、可直接執行的範例，能 **recognize text image** 檔案、**improve OCR accuracy**，最後在主控台 **display OCR text**。完成後，你將了解如何 **load image OCR** 資源、套用如傾斜校正與去噪的過濾器，並取得可靠的結果——全部使用 Aspose.OCR for .NET。

## 你將學會

- 如何建立 `OcrEngine` 實例並設定前處理過濾器。
- 為何傾斜校正與去噪過濾器對 **improve OCR accuracy** 如此重要。
- 取得 **load image ocr** 檔案並執行辨識的完整程式碼。
- 如何以使用者友善的方式 **display OCR text**。
- 在實務專案中可套用的技巧、常見陷阱與可選的微調。

### 前置條件

- 在機器上安裝 .NET 6+（或 .NET Framework 4.7+）。
- Aspose.OCR 授權（免費試用版即可執行此示範）。
- 基本的 C# 知識——不需要進階技巧。

如果上述項目有不熟悉的，請先暫停並安裝缺少的部分；其餘指南假設這些已就緒。

---

## preprocess image ocr – 設定過濾器

首先你需要了解 **why preprocessing matters**。OCR 引擎擅長讀取清晰、正面的文字，但實際掃描常會出現旋轉、模糊或背景雜訊。將清理過的影像提供給引擎，能大幅提升正確辨識的機率。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters.
        //    • SkewCorrectionFilter: straightens tilted text.
        //    • DenoiseFilter: removes speckles and grain.
        ocrEngine.Settings.PreprocessingFilters.Add(new SkewCorrectionFilter());
        ocrEngine.Settings.PreprocessingFilters.Add(new DenoiseFilter());

        // 3️⃣ (Optional) Fine‑tune filter parameters.
        // ((SkewCorrectionFilter)ocrEngine.Settings.PreprocessingFilters[0]).MaxAngle = 25;

        // 4️⃣ Load the image you want to run OCR on.
        OcrImage inputImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition.
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // 6️⃣ Show the recognized text.
        Console.WriteLine("Corrected text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**這段程式碼在做什麼？**  
- **Step 1** 建立引擎——Aspose OCR 函式庫的核心。  
- **Step 2** 加入兩個過濾器。`SkewCorrectionFilter` 會將影像旋轉回水平，`DenoiseFilter` 則平滑像素層級的雜訊。  
- **Step 3** 為可選但實用的設定；你可以限制引擎嘗試校正的最大角度，避免對已經水平的頁面過度旋轉。  
- **Step 4** 為 **load image OCR** 資料的步驟。請將 `YOUR_DIRECTORY/skewed_noisy.jpg` 替換為測試檔案的路徑。  
- **Step 5** 真正執行 OCR，產生 `OcrResult`。  
- **Step 6** 在主控台 **display OCR text**，即時取得回饋。

> **專業提示：** 若發現輸出仍有亂碼，請嘗試提高 `MaxAngle`，或在去噪步驟前加入 `ContrastFilter`。

## recognize text image – 正確載入檔案

常見的絆腳石是以錯誤的格式或 DPI **load image ocr**。Aspose.OCR 支援 PNG、JPEG、TIFF、BMP，甚至 PDF 形式的影像。然而，對於列印文件，300 DPI 或更高的解析度效果最佳。

```csharp
// Example: loading a high‑resolution PNG
string imagePath = @"C:\Images\invoice_300dpi.png";
OcrImage highRes = OcrImage.FromFile(imagePath);
```

若處理多頁 TIFF，可迴圈遍歷每個影格：

```csharp
var tiff = Aspose.OCR.ImageProcessing.TiffImage.FromFile(@"multi_page.tif");
foreach (var frame in tiff.Frames)
{
    OcrResult pageResult = ocrEngine.Recognize(frame);
    Console.WriteLine(pageResult.Text);
}
```

**為何這對 improve OCR accuracy 很重要？** 較高的解析度保留每個字元的形狀，提供辨識器更多資料點。低 DPI 影像常會導致字形合併或斷裂，讓引擎誤判。

## improve OCR accuracy – 微調過濾器參數

預設的過濾器設定已相當不錯，但仍可進一步優化效能。

| 過濾器 | 關鍵屬性 | 典型值 | 調整時機 |
|--------|----------|--------|----------|
| `SkewCorrectionFilter` | `MaxAngle` | `15` (degrees) | 影像傾斜嚴重（最高可達 30°）的情況。 |
| `DenoiseFilter` | `Strength` | `0.5` (0‑1) | 噪點非常多的掃描；可提升至 `0.8`。 |
| `ContrastFilter` (optional) | `Level` | `1.2` | 對比度低的螢幕截圖。 |

以下為同時自訂兩者的範例：

```csharp
var skew = new SkewCorrectionFilter { MaxAngle = 25 };
var denoise = new DenoiseFilter { Strength = 0.8 };
ocrEngine.Settings.PreprocessingFilters.Clear(); // start fresh
ocrEngine.Settings.PreprocessingFilters.Add(skew);
ocrEngine.Settings.PreprocessingFilters.Add(denoise);
```

**邊緣情況：** 若影像同時包含手寫筆記與印刷文字，建議在去噪前加入 `BinarizationFilter`，以將前景與背景分離。

## display OCR text – 格式化輸出

純文字主控台輸出適合示範，但正式程式碼通常需要清理過的字串、換行，甚至 JSON。

```csharp
// Remove extra whitespace and line breaks
string cleaned = System.Text.RegularExpressions.Regex
    .Replace(ocrResult.Text, @"\s+", " ")
    .Trim();

Console.WriteLine("📝 Recognized Text:");
Console.WriteLine(cleaned);
```

若 API 回應需要 JSON：

```csharp
var payload = new {
    source = imagePath,
    text = cleaned,
    confidence = ocrResult.Confidence // overall confidence score
};
string json = System.Text.Json.JsonSerializer.Serialize(payload, new JsonSerializerOptions { WriteIndented = true });
Console.WriteLine(json);
```

現在你已以可供下游服務使用的格式 **display OCR text**。

## 完整範例 – 整合所有步驟

以下是最終的完整程式，你可以直接複製貼上到新的主控台專案中。它包含可選過濾器、高解析度影像載入，以及乾淨的輸出。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Text.Json;
using System.Text.RegularExpressions;

class PreprocessDemo
{
    static void Main()
    {
        // ---------- 1️⃣ Initialize OCR engine ----------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------- 2️⃣ Configure preprocessing ----------
        // Skew correction (up to 25°) + strong denoise
        var skew = new SkewCorrectionFilter { MaxAngle = 25 };
        var denoise = new DenoiseFilter { Strength = 0.8 };
        ocrEngine.Settings.PreprocessingFilters.Add(skew);
        ocrEngine.Settings.PreprocessingFilters.Add(denoise);

        // Optional: increase contrast for low‑visibility scans
        // ocrEngine.Settings.PreprocessingFilters.Add(new ContrastFilter { Level = 1.3 });

        // ---------- 3️⃣ Load the image ----------
        string imagePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // ---------- 4️⃣ Run OCR ----------
        OcrResult result = ocrEngine.Recognize(inputImage);

        // ---------- 5️⃣ Clean & display ----------
        string cleaned = Regex.Replace(result.Text, @"\s+", " ").Trim();
        Console.WriteLine("✅ Corrected text:");
        Console.WriteLine(cleaned);

        // ---------- 6️⃣ JSON payload (if needed) ----------
        var payload = new {
            source = imagePath,
            text = cleaned,
            confidence = result.Confidence
        };
        string json = JsonSerializer.Serialize(payload, new JsonSerializerOptions { WriteIndented = true });
        Console.WriteLine("\n📦 JSON output:");
        Console.WriteLine(json);
    }
}
```

**預期的主控台輸出（範例）：**

```
✅ Corrected text:
Invoice #12345 Date: 01/15/2026 Total: $1,250.00

📦 JSON output:
{
  "source": "YOUR_DIRECTORY/skewed_noisy.jpg",
  "text": "Invoice #12345 Date: 01/15/2026 Total: $1,250.00",
  "confidence": 0.97
}
```

若使用不同檔案執行程式，文字與信心指標會相應變化。

## 常見問答

**問：如果我的影像已經是水平的呢？**  
**答：** 傾斜過濾器會偵測到接近零度的角度，實際上不會執行任何操作，因此可以安全保留此過濾器。

**問：Aspose.OCR 是否支援英語以外的語言？**  
**答：** 支援——只要在呼叫 `Recognize` 前設定 `ocrEngine.Settings.Language = OcrLanguage.Spanish;`（或任何支援的語言）。

**問：如何處理多頁 PDF？**  
**答：** 先將每頁轉為影像（可使用 Aspose.PDF），再逐一送入同一個 `OcrEngine` 實例。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}