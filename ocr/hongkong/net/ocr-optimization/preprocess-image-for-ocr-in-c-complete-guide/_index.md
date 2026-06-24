---
category: general
date: 2026-06-16
description: 使用 C# 及 Aspose OCR 進行影像前處理。學習增強圖像對比度與去除掃描圖像雜訊，以確保文字提取的準確性。
draft: false
keywords:
- preprocess image for OCR
- enhance image contrast
- remove noise from scanned image
language: zh-hant
og_description: 使用 Aspose OCR 進行影像前處理以供 OCR。透過增強影像對比度與去除掃描影像噪點，提高準確度。
og_title: C# 圖像預處理（OCR）完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Preprocess image for OCR using Aspose OCR in C#. Learn to enhance image
    contrast and remove noise from scanned image for accurate text extraction.
  headline: Preprocess Image for OCR in C# – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR using Aspose OCR in C#. Learn to enhance image
    contrast and remove noise from scanned image for accurate text extraction.
  name: Preprocess Image for OCR in C# – Complete Guide
  steps:
  - name: '**Heavy Salt‑and‑Pepper Noise** – Increase the aggressiveness of `DenoiseFilter`
      by passing a custom `DenoiseOptions` object (e.g., `new DenoiseFilter(new DenoiseOptions
      { Strength = 2 })`).'
    text: '**Heavy Salt‑and‑Pepper Noise** – Increase the aggressiveness of `DenoiseFilter`
      by passing a custom `DenoiseOptions` object (e.g., `new DenoiseFilter(new DenoiseOptions
      { Strength = 2 })`).'
  - name: '**Faded Ink on Yellow Paper** – Pair `ContrastEnhanceFilter` with a `BrightnessAdjustFilter`
      to lift the background tone before boosting contrast.'
    text: '**Faded Ink on Yellow Paper** – Pair `ContrastEnhanceFilter` with a `BrightnessAdjustFilter`
      to lift the background tone before boosting contrast.'
  - name: '**Colored Text** – Convert the image to grayscale first (`new GrayscaleFilter()`)
      because most OCR engines, including Aspose, work best on single‑channel data.'
    text: '**Colored Text** – Convert the image to grayscale first (`new GrayscaleFilter()`)
      because most OCR engines, including Aspose, work best on single‑channel data.'
  - name: '**Build** the console project (`dotnet build`).'
    text: '**Build** the console project (`dotnet build`).'
  - name: '**Run** (`dotnet run`). You should see something like:'
    text: '**Run** (`dotnet run`). You should see something like:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
title: 在 C# 中對圖像進行 OCR 前處理 – 完整指南
url: /zh-hant/net/ocr-optimization/preprocess-image-for-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中預處理 OCR 圖像 – 完整指南

有沒有想過為什麼即使原始相片相當清晰，OCR 結果卻像是一團亂碼？事實上，大多數 OCR 引擎（包括 Aspose OCR）都需要乾淨、對齊良好的圖像。**Preprocess image for OCR** 是將模糊、低對比度的掃描圖像轉換為清晰、機器可讀文字的第一步。

在本教學中，我們將逐步示範一個實用的端到端範例，不僅 **preprocess image for OCR**，還會示範如何使用 Aspose 內建的濾鏡 **enhance image contrast** 以及 **remove noise from scanned image**。完成後，你將擁有一個可直接執行的 C# 主控台應用程式，提供更可靠的辨識結果。

---

## 所需條件

- **.NET 6.0 或更新版本**（此程式碼亦可於 .NET Framework 4.6+ 執行）  
- **Aspose.OCR for .NET** – 你可以取得 NuGet 套件 `Aspose.OCR`  
- 一張受噪點、傾斜或低對比度影響的範例圖像（示範中將使用 `skewed-photo.jpg`）  
- 任何你喜歡的 IDE – Visual Studio、Rider 或 VS Code 都可使用  

不需要額外的原生函式庫或複雜的安裝；所有功能皆內建於 Aspose 套件中。

---

## ## Preprocess Image for OCR – 步驟實作

以下是你將編譯的完整原始檔案。隨意將它複製貼上到新的主控台專案中，然後按 **F5**。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2: Add preprocessing filters to improve recognition.
        // 2a – Remove noise from scanned image.
        ocrEngine.Settings.Filters.Add(new DenoiseFilter()); // Reduces random speckles.
        // 2b – Correct skew (deskew) that often appears in photographed documents.
        ocrEngine.Settings.Filters.Add(new DeskewFilter()); // Straightens the baseline.
        // 2c – Enhance image contrast for better character separation.
        ocrEngine.Settings.Filters.Add(new ContrastEnhanceFilter()); // Boosts contrast.

        // Step 3: (Optional) Rotate the image if it was captured at an angle.
        // Negative values rotate clockwise, positive counter‑clockwise.
        ocrEngine.Settings.Filters.Add(new RotateFilter(-3)); // Small correction.

        // Step 4: Perform OCR on the image file.
        // Replace the path with the actual location of your test image.
        string extractedText = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed-photo.jpg");

        // Step 5: Display the recognized text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

### 為何每個濾鏡都很重要

| 濾鏡 | 功能說明 | 為何有助於 OCR |
|--------|--------------|-----------------|
| **DenoiseFilter** | 去除低光掃描中常見的隨機像素噪點。 | 噪點可能被誤認為字形碎片，破壞字元形狀。 |
| **DeskewFilter** | 偵測主要文字行的角度，並將圖像旋轉至 0°。 | 傾斜的基線會讓 OCR 引擎認為字元斜向，導致辨識錯誤。 |
| **ContrastEnhanceFilter** | 擴大深色文字與淺色背景之間的差異。 | 較高的對比度可提升大多數 OCR 流程中的二值化閾值步驟。 |
| **RotateFilter** (optional) | 套用你指定的手動旋轉。 | 當自動去斜不足時很實用，例如照片以輕微角度拍攝。 |

> **Pro tip:** 如果你的來源是掃描的 PDF，請先將頁面匯出為圖像（例如使用 `PdfRenderer`），再將其送入相同的濾鏡鏈。相同的預處理邏輯仍然適用。

---

## ## Enhance Image Contrast Before OCR – 視覺確認

加入濾鏡是一回事，看到效果則是另一回事。以下是一個簡單的前後對照示意圖（測試時請自行替換為你的螢幕截圖）。

![Diagram of preprocess image for OCR pipeline](image.png){alt="OCR 圖像預處理流程圖"}

左側顯示原始、雜訊較多的掃描圖，右側則是經過 **enhance image contrast**、**remove noise from scanned image** 以及去斜處理後的同一圖像。請留意字元變得清晰且獨立——正是 OCR 引擎所需要的。

---

## ## Remove Noise from Scanned Image – 邊緣案例與技巧

並非每份文件都會遭遇相同類型的噪點。以下列出幾種可能的情況，以及如何調整流程。

1. **Heavy Salt‑and‑Pepper Noise** – 透過傳入自訂的 `DenoiseOptions` 物件（例如 `new DenoiseFilter(new DenoiseOptions { Strength = 2 })`）來提升 `DenoiseFilter` 的強度。  
2. **Faded Ink on Yellow Paper** – 結合 `ContrastEnhanceFilter` 與 `BrightnessAdjustFilter`，先提升背景色調再增強對比度。  
3. **Colored Text** – 先將圖像轉為灰階 (`new GrayscaleFilter()`) ，因為包括 Aspose 在內的大多數 OCR 引擎在單通道資料上表現最佳。  

濾鏡的順序也會影響結果。實務上，我會將 `DenoiseFilter` **放在** `DeskewFilter` **之前**，因為較乾淨的圖像能提供去斜演算法更可靠的邊緣資料。

---

## ## Running the Demo & 驗證輸出

1. **Build** 主控台專案（`dotnet build`）。  
2. **Run**（`dotnet run`）。你應該會看到類似以下的輸出：

```
=== OCR RESULT ===
The quick brown fox jumps over the lazy dog.
```

如果輸出仍出現亂碼，請再次確認圖像路徑是否正確，且來源檔案的解析度是否過低（大多數 OCR 任務建議最低 300 dpi）。

---

## 結論

你現在已擁有一套穩固、可投入生產環境的 **preprocess image for OCR** C# 範例。透過串接 Aspose 的 `DenoiseFilter`、`DeskewFilter`、`ContrastEnhanceFilter`，以及可選的 `RotateFilter`，即可 **enhance image contrast**、**remove noise from scanned image**，大幅提升後續文字擷取的準確度。

接下來要做什麼？可以將清理過的圖像輸入其他後處理步驟，例如拼寫檢查、語言偵測，或將原始文字送入自然語言處理管線。你亦可探索 Aspose 的 `BinarizationFilter` 用於僅二值化的工作流程，或改用其他 OCR 引擎（Tesseract、Microsoft OCR），同時重用相同的預處理鏈。

遇到仍無法辨識的棘手圖像嗎？留下評論，我們一起排除問題。祝編程愉快，願你的 OCR 結果永遠清晰如晶！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在此處示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何使用 AspOCR：.NET 的圖像 OCR 預處理濾鏡](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [從圖像提取文字 – 使用 Aspose.OCR for .NET 進行 OCR 優化](/ocr/english/net/ocr-optimization/)
- [如何使用 Aspose.OCR for .NET 從圖像提取文字](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}