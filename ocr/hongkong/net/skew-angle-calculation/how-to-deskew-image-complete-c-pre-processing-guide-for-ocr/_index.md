---
category: general
date: 2026-01-13
description: 如何在 C# 中校正影像傾斜並去除影像噪點 – 學習提升影像對比度、預處理影像 OCR，並套用多種影像濾鏡。
draft: false
keywords:
- how to deskew image
- remove image noise
- increase image contrast
- preprocess image ocr
- multiple image filters
language: zh-hant
og_description: 如何在 C# 中去斜影像並去除影像噪點 – 學習提升影像對比度、預處理影像 OCR 以及套用多種影像濾鏡。
og_title: 如何校正圖像傾斜 – 完整的 C# OCR 前處理指南
tags:
- OCR
- C#
- Image Processing
title: 如何校正影像傾斜 – 完整 C# OCR 前處理指南
url: /zh-hant/net/skew-angle-calculation/how-to-deskew-image-complete-c-pre-processing-guide-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何校正影像傾斜 – 完整的 C# 前置處理指南（OCR）

有沒有想過 **如何校正影像傾斜** 後再送入 OCR 引擎？你並不孤單。在許多實務情境──掃描合約、收據或舊的影印件──文字往往呈現輕微斜角，畫面顆粒感強，對比度參差不齊。好消息是，只要幾行 C# 程式碼就能把斜角校正、去除雜訊、提升對比度，為你的 OCR 打下堅實基礎。

在本教學中，我們將示範一個 **完整、可執行的範例**，說明如何校正影像傾斜、去除影像雜訊、提升影像對比度，然後使用 Aspose.OCR 進行 OCR。完成後，你將擁有一條可重複使用的管線，能在單一流暢呼叫中套用 **多個影像濾鏡**，不再需要猜測。

## 需求

- **.NET 6+**（或任何近期的 .NET 版本；API 使用方式相同）
- **Aspose.OCR for .NET** NuGet 套件（`Aspose.OCR` 與 `Aspose.OCR.Filters`）
- 一張示範用的掃描影像（例如 `skewed_noisy.png`），具備傾斜、雜訊與低對比度
- 你慣用的 IDE（Visual Studio、Rider、VS Code──隨你喜好）

如果已經有專案，只要加入 NuGet 參考即可：

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Filters
```

> **小技巧：** Aspose 提供免費試用版，頁數有限──非常適合先試跑以下程式碼。

## 步驟 1：建立 OCR 引擎實例

首先，我們建立一個 `OcrEngine`。把它想像成稍後會閱讀文字的大腦。雖然很簡單，但它是後續所有操作的基礎。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

> **為什麼重要：** 只要初始化一次引擎，然後在多張影像間重複使用，就能避免每次載入語言資料的額外開銷。

## 步驟 2：載入原始掃描影像

接著，我們從磁碟讀取影像。`OcrImage.FromFile` 會把檔案讀入 Aspose 可操作的格式。

```csharp
        // Step 2: Load the raw scanned image (skewed, noisy, low‑contrast)
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");
```

> **邊緣情況：** 若影像是非標準格式（TIFF、BMP），Aspose 仍能處理，但為了一致性，建議先轉成 PNG。

## 步驟 3：建構前置處理管線（校正 → 去雜訊 → 提升對比）

這裡就是回答核心問題 **如何校正影像傾斜**，同時 **去除影像雜訊** 與 **提升影像對比度** 的地方。Aspose 的流暢 API 允許我們將濾鏡串接起來，程式碼讀起來就像一句話。

```csharp
        // Step 3: Apply Deskew, Denoise, and Contrast filters in one pipeline
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())      // Corrects rotation
            .ApplyFilter(new DenoiseFilter())     // Reduces grainy artifacts
            .ApplyFilter(new ContrastFilter());   // Boosts foreground/background separation
```

### 各濾鏡功能說明

| 濾鏡 | 目的 | 常見影響 |
|------|------|----------|
| **DeskewFilter** | 偵測文字行的角度並旋轉影像，使其水平。 | 移除讓 OCR 困惑的斜角，錯誤率通常降低 30‑50 %。 |
| **DenoiseFilter** | 套用保留邊緣的平滑演算法，同時去除隨機像素雜訊。 | 清理掃描收據或低光照片，使字元更清晰。 |
| **ContrastFilter** | 拉伸直方圖，使暗部更暗、亮部更亮。 | 提升文字與背景的區分度，特別適合褪色文件。 |

> **為什麼要串接？** 先校正傾斜可確保去雜訊在正確方向的影像上執行；最後提升對比度則讓清理過的文字在 OCR 引擎面前更突出。

## 步驟 4：對處理後的影像執行 OCR

影像已經校正、清理且高對比，我們把它交給 OCR 引擎。這裡使用英文語言資料，Aspose 支援超過 150 種語言。

```csharp
        // Step 4: Recognize text using the English language pack
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);
```

若需其他語言，只要把 `OcrLanguage.English` 換成相應的列舉值（例如 `OcrLanguage.Spanish`）。

## 步驟 5：輸出辨識結果

最後，我們把結果印到主控台。實際應用中，你可能會寫入檔案、資料庫，或將文字送入下游的 NLP 管線。

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### 預期輸出

在一張典型的傾斜收據上執行完整程式，會得到類似以下的結果：

```
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
Thank you for your business!
```

如果輸出雜亂，請再次檢查原始影像──過度模糊或過暗可能需要額外的前置處理（例如 `SharpenFilter`）。

![如何校正影像傾斜範例](images/deskewed_example.png "如何校正影像傾斜 – 前後處理比較")

*上圖左側為原始傾斜掃描，右側為校正、去雜訊、提升對比度後的結果。*

## 其他技巧與常見陷阱

### 1. 當傾斜角度過大時

若文件傾斜超過 30°，`DeskewFilter` 可能無法正確校正。此時可先手動旋轉影像：

```csharp
var manuallyRotated = rawImage.Rotate(45); // rotates 45 degrees clockwise
var processed = manuallyRotated.ApplyFilter(new DeskewFilter());
```

### 2. 處理彩色影像

濾鏡在內部會轉成灰階，但你也可以強制轉換：

```csharp
var grayImage = rawImage.ConvertToGrayscale();
var processed = grayImage.ApplyFilter(new DeskewFilter());
```

### 3. 調整去雜訊強度

`DenoiseFilter` 接受可選的 `strength` 參數（0‑100）。數值越高去除的雜訊越多，但可能會模糊細節。

```csharp
.ApplyFilter(new DenoiseFilter(strength: 70))
```

### 4. 使用更多影像濾鏡

Aspose 內建許多其他濾鏡：`SharpenFilter`、`BinarizeFilter`、`ResizeFilter` 等。你可以自由組合，打造符合特定文件類型的自訂管線。

```csharp
var processed = rawImage
    .ApplyFilter(new DeskewFilter())
    .ApplyFilter(new DenoiseFilter())
    .ApplyFilter(new BinarizeFilter())
    .ApplyFilter(new SharpenFilter());
```

## 完整可執行範例（直接複製貼上）

以下是整個程式碼，直接放入 Console 專案即可使用。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Load the original scanned image
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // Build preprocessing pipeline: Deskew → Denoise → Contrast
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())
            .ApplyFilter(new DenoiseFilter())
            .ApplyFilter(new ContrastFilter());

        // Run OCR using English language
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);

        // Output recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

使用 `dotnet run` 執行。若環境設定正確，主控台會顯示從原本傾斜、雜訊多的影像中擷取出的乾淨、可讀文字。

## 結論

我們剛剛示範了 **如何校正影像傾斜** 同時 **去除影像雜訊**、**提升影像對比度**，並以 **多個影像濾鏡** 的鏈結方式完成 OCR 前置處理。關鍵在於，良好排序的前置處理管線能顯著提升 OCR 準確度──往往能把幾乎無法辨識的掃描件變成清晰可讀的文字。

想更進一步嗎？試著把 `ContrastFilter` 換成 `BinarizeFilter`，觀察二值化（黑白）轉換對結果的影響；或是加入 `ResizeFilter`，將更高解析度的影像送入引擎。無論選擇哪種濾鏡，模式皆相同，讓你在未來的 OCR 專案中擁有彈性且可擴充的基礎。

對於 PDF 處理、多語言 OCR，或是將此功能整合到 ASP.NET API 有任何疑問，歡迎在下方留言。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}