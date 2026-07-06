---
category: general
date: 2026-04-17
description: 如何使用 Aspose.OCR 快速去斜圖像 – 學習載入圖像 OCR、預處理圖像 OCR，以及以高精準度辨識文字圖像。
draft: false
keywords:
- how to deskew image
- recognize text image
- improve ocr accuracy
- load image ocr
- preprocess image ocr
language: zh-hant
og_description: 如何在 C# 中校正圖像傾斜並提升 OCR 準確度。學習載入圖像進行 OCR、預處理圖像，以及使用 Aspose.OCR 進行文字辨識。
og_title: 如何校正圖像傾斜 – 完整 C# OCR 教學
tags:
- Aspose.OCR
- C#
- Image Processing
title: 如何校正圖像傾斜並提升 C# OCR 準確率 – 步驟指南
url: /zh-hant/net/ocr-optimization/how-to-deskew-image-and-boost-ocr-accuracy-in-c-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中校正影像傾斜並提升 OCR 準確度

**如何校正影像傾斜** 是在需要從未完全對齊的照片中擷取文字時常見的障礙。本指南將逐步說明載入影像、前置處理，最後使用 Aspose.OCR 強大的濾鏡鏈 **辨識文字影像**。

如果你曾用手機相機對著收據、招牌或掃描表單拍照，結果卻得到歪斜、難以辨認的字元，你一定深有體會。好消息是，只要幾行 C# 程式碼就能將圖片校正、去除雜訊，並取得可直接使用的乾淨字串。我們也會簡要說明如何透過調整前置處理步驟 **提升 OCR 準確度**。

## 需求

- .NET 6.0 或更新版本（亦支援 .NET Core）  
- **Aspose.OCR** 的授權或評估版（可透過 NuGet 取得）  
- 一張稍微旋轉或有雜訊的影像檔（例如 `skewed_photo.png`）  

不需要額外的第三方工具——只要 Aspose.OCR 函式庫與一點 C# 基礎即可。

![如何校正影像示例](/images/deskew-demo.png "如何校正影像 – 原始 vs 校正後")

---

## 步驟 1 – 載入影像 OCR：準備來源檔案

在校正之前，我們必須先將圖片載入記憶體。`OcrImage.FromFile` 方法正是用來完成此動作。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the image you want to process
var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");
```

> **為什麼重要：** 將影像載為 `OcrImage` 讓 OCR 引擎直接存取像素資料，這對後續的 **前置處理影像 OCR** 步驟至關重要。若檔案路徑錯誤，會拋出 `FileNotFoundException`，請務必確認路徑正確。

## 步驟 2 – 前置處理影像 OCR：建立校正濾鏡鏈

接下來就是 **如何校正影像傾斜** 的核心。Aspose.OCR 內建多種濾鏡，可依任意順序堆疊。對於大多數實際照片，我們建議：

1. **Deskew** – 校正旋轉角度  
2. **Denoise** – 去除鹽與胡椒雜訊  
3. **ContrastEnhance** – 提升淡弱字元的可見度

```csharp
// Create a chain of preprocessing filters
var filterChain = new ImageFilterCollection
{
    new DeskewFilter(),          // Detects and corrects rotation
    new DenoiseFilter(),        // Reduces noise
    new ContrastEnhanceFilter() // Boosts contrast for faint text
};

// Apply the filter chain to obtain a cleaned image
var filteredImage = filterChain.Apply(ocrImage);
```

> **小技巧：** 若影像已經曝光良好，可省略 `ContrastEnhanceFilter`。減少處理步驟即可提升執行速度。

### 邊緣情況

- **極端旋轉 (>45°)：** `DeskewFilter` 最佳效果約在 30° 以內。若角度更大，建議先手動旋轉影像 (`filteredImage.Rotate(…)`)。  
- **彩色背景：** 在去雜訊前先轉為灰階，可獲得更佳結果 (`filteredImage = filteredImage.ToGrayscale();`)。

## 步驟 3 – 辨識文字影像：執行 OCR 引擎

取得乾淨且已校正的位圖後，就可以開始擷取文字了。

```csharp
// Create an OCR engine instance
using var ocrEngine = new OcrEngine();

// Recognize text from the filtered image
var ocrResult = ocrEngine.Recognize(filteredImage);

// Display the recognized text
Console.WriteLine(ocrResult.Text);
```

> **底層發生了什麼？** `OcrEngine` 會使用神經網路辨識器，該辨識器需要近乎直立且高對比度的影像。因此先前的 **前置處理影像 OCR** 步驟對 **提升 OCR 準確度** 至關重要。

### 預期輸出

若原始照片的文字為「Invoice #12345 – Total $89.99」，控制台大概會印出：

```
Invoice #12345 – Total $89.99
```

如果出現亂碼，請重新檢查濾鏡鏈——或許需要額外的銳化 (`new SharpenFilter()`)。

## 步驟 4 – 微調以提升 OCR 準確度

即使已校正，OCR 仍可能在特定字型或低解析度掃描件上失誤。以下提供幾個快速調整方式：

| 問題 | 解決方案 |
|------|----------|
| 字型太小 (<10 pt) | 放大影像 (`filteredImage = filteredImage.Resize(2.0);`) |
| 淺灰色文字在白底上 | 再次提升對比度 (`new ContrastEnhanceFilter(1.5)`) |
| 混合語言文字 | 設定 `ocrEngine.Language = OcrLanguage.Multilingual;` |

這些調整可直接 **提升 OCR 準確度**，且不需改變程式的核心結構。

## 完整範例

以下是結合上述所有步驟的完整可執行程式。將它複製到新的 Console 專案，然後按 **F5** 執行。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 1: Load the image you want to process
        var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");

        // Step 2: Build a chain of preprocessing filters
        var filterChain = new ImageFilterCollection
        {
            new DeskewFilter(),          // Detects and corrects rotation
            new DenoiseFilter(),        // Reduces salt‑and‑pepper noise
            new ContrastEnhanceFilter() // Improves faint characters
        };

        // Step 3: Apply the filter chain to obtain a cleaned image
        var filteredImage = filterChain.Apply(ocrImage);

        // Step 4: Create an OCR engine instance
        using var ocrEngine = new OcrEngine();

        // Optional: set language or other engine options here
        // ocrEngine.Language = OcrLanguage.English;

        // Step 5: Recognize text from the filtered image
        var ocrResult = ocrEngine.Recognize(filteredImage);

        // Step 6: Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

執行程式後，您應該會在控制台看到已清理、校正的文字。

## 常見問題與解答

**Q: 這能用在 PDF 上嗎？**  
A: 能。先將每一頁 PDF 轉為影像（例如使用 `Aspose.PDF`），再將產生的位圖送入相同的濾鏡鏈。

**Q: 若我的影像已經完全對齊，該怎麼辦？**  
A: `DeskewFilter` 會偵測到接近零度的角度，並保持影像不變——不會造成任何損害。

**Q: 可以一次批次處理多張影像嗎？**  
A: 當然可以。將程式碼包在 `foreach (var path in Directory.GetFiles(...))` 迴圈中，並將每個 `ocrResult.Text` 存入清單或檔案即可。

---

## 結論

我們示範了 **如何程式化校正影像傾斜**，說明了 **載入影像 OCR** 步驟、建立穩健的 **前置處理影像 OCR** 流程，最後使用 Aspose.OCR **辨識文字影像**。透過調整濾鏡、適度放大或銳化，即可 **提升 OCR 準確度**，應對各種實務情境。

準備好接受下一個挑戰了嗎？試著將此流程整合到 Web API，或在校正前加入 `new BinarizationFilter()` 以實驗手寫筆記辨識。可能性無限——祝開發順利！

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}