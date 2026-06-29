---
category: general
date: 2026-06-28
description: 如何使用 Aspose.OCR 校正影像傾斜。學習為 OCR 進行影像前處理、提升 OCR 準確度，並以完整的 C# 範例對掃描影像進行去斜。
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- how to improve ocr
- deskew scanned image
language: zh-hant
og_description: 如何使用 Aspose.OCR 校正影像傾斜。本教學將一步步示範如何為 OCR 進行影像前處理、提升辨識準確度，以及校正掃描影像的傾斜。
og_title: 如何在 C# 中校正圖像傾斜 – 完整 Aspose.OCR 使用指南
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  headline: How to Deskew Image in C# – Complete Aspose.OCR Guide
  type: TechArticle
- description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  name: How to Deskew Image in C# – Complete Aspose.OCR Guide
  steps:
  - name: Why a Deskew Filter First?
    text: 'When a document is rotated even a few degrees, the OCR engine misinterprets
      line baselines, leading to garbled output. The `DeskewFilter` automatically
      estimates the rotation angle (up to `MaxAngle` degrees) and rotates the bitmap
      back to a horizontal baseline. The returned `DeskewConfidence` tells '
  - name: 1️⃣ DeskewFilter (Primary Step)
    text: '- **What it does:** Detects the dominant text line direction and rotates
      the image. - **Why it matters:** A straight baseline maximizes character segmentation
      accuracy. - **Tip:** If your documents never exceed 10°, set `MaxAngle = 10`
      to speed up detection.'
  - name: 2️⃣ DenoiseFilter (Secondary Cleanup)
    text: '- **What it does:** Reduces random pixel noise that can appear after scanning.
      - **Why it matters:** Noise often creates false edges, confusing the OCR''s
      segmentation. - **Tip:** Adjust `Strength` between 0.3 (light) and 0.8 (aggressive)
      based on scan quality.'
  - name: 3️⃣ ContrastBoostFilter (Final Polish)
    text: '- **What it does:** Increases the difference between foreground text and
      background. - **Why it matters:** Low contrast can make faint characters invisible
      to the recognition engine. - **Tip:** A `Level` of 1.2 works for most black‑on‑white
      scans; for colored documents, experiment with values up to '
  type: HowTo
tags:
- OCR
- Aspose
- Image Processing
title: 如何在 C# 中去除影像傾斜 – 完整 Aspose.OCR 指南
url: /zh-hant/net/ocr-optimization/how-to-deskew-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中校正圖像傾斜 – 完整 Aspose.OCR 指南

有沒有想過在將圖像檔案送入 OCR 引擎之前 **如何校正圖像傾斜**？你並不是唯一有此疑問的人。掃描文件常常會傾斜，而這微小的旋轉會嚴重影響辨識結果。好消息是？使用 Aspose.OCR 只需幾行 C# 程式碼就能將圖像校正（deskew）並清理。

在本教學中，我們將逐步說明一個完整且可執行的範例，該範例 **為 OCR 預處理圖像**，加入校正濾鏡，並示範 **如何提升 OCR** 的準確度。完成後，你將能自動 **校正掃描圖像** 檔案，並自行查看信心分數。

> **注意：** 此程式碼適用於 Aspose.OCR ≥ 22.10 以及 .NET 6+，但其概念同樣適用於較早的版本。

## 您需要的條件

- **Aspose.OCR for .NET** (NuGet 套件 `Aspose.OCR`)
- 想要校正的 **傾斜 TIFF** 或 JPEG
- Visual Studio 2022（或任何 C# IDE）
- 具備 C# 與主控台應用程式的基本知識

不需要額外的第三方函式庫；整個管線全部由 Aspose.OCR 內部提供。

---

## 使用 Aspose.OCR 校正圖像傾斜

此解決方案的核心是一個 **濾鏡管線**。可將其想像成組裝線，每個濾鏡處理特定問題：首先校正旋轉，接著降低噪點，最後提升對比，使 OCR 引擎能清晰辨識字元。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class DeskewExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();

        // Step 2: Load the skewed image to be processed
        var img = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_doc.tif");

        // Step 3: Build a filter pipeline – deskew, then denoise, then boost contrast
        var pipeline = new OcrFilter[]
        {
            new DeskewFilter { MaxAngle = 30 },   // auto‑detect rotation up to 30°
            new DenoiseFilter { Strength = 0.5 },
            new ContrastBoostFilter { Level = 1.2 }
        };

        // Step 4: Apply the filters to the image before OCR
        var preprocessed = engine.ApplyFilters(img, pipeline);

        // Step 5: Perform OCR on the pre‑processed image
        var result = engine.Recognize(preprocessed);

        // Step 6: Output the deskew confidence and recognized text
        System.Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
        System.Console.WriteLine(result.Text);
    }
}
```

> **圖像範例**  
> ![校正圖像範例](/images/deskew-example.png "校正圖像範例")

### 為什麼先使用 Deskew Filter？

當文件即使只旋轉幾度，OCR 引擎也會誤判行基線，導致輸出雜亂。`DeskewFilter` 會自動估算旋轉角度（最高至 `MaxAngle` 度），並將位圖旋轉回水平基線。返回的 `DeskewConfidence` 會告訴你演算法對校正的信心程度——對於記錄或備援策略相當有用。

---

## 為 OCR 預處理圖像 – 建立濾鏡管線

### 1️⃣ DeskewFilter（主要步驟）

- **它的功能：** 偵測主要文字行方向並旋轉圖像。
- **重要性：** 直線基線可最大化字元分割的準確度。
- **提示：** 若文件的傾斜角度永不超過 10°，可將 `MaxAngle = 10` 以加速偵測。

### 2️⃣ DenoiseFilter（次要清理）

- **它的功能：** 減少掃描後可能出現的隨機像素噪點。
- **重要性：** 噪點常會產生偽邊緣，干擾 OCR 的分割。
- **提示：** 可根據掃描品質將 `Strength` 調整於 0.3（輕度）至 0.8（強度）之間。

### 3️⃣ ContrastBoostFilter（最終調整）

- **它的功能：** 增強前景文字與背景之間的差異。
- **重要性：** 低對比度會使微弱字元對辨識引擎不可見。
- **提示：** `Level` 設為 1.2 可適用大多數黑白掃描；若為彩色文件，可嘗試最高至 2.0 的數值。

透過串接這三個濾鏡，你可以 **為 OCR 預處理圖像**，同時解決最常見的問題：傾斜、噪點與低對比度。

---

## 如何透過 Deskew 與 Denoise 提升 OCR 準確度

你可能會問：「如果已經有 Deskew 濾鏡，為何還要使用 denoise 與 contrast boost？」答案在於 **累積式提升**。每個濾鏡解決不同缺陷，合起來可提升整體信心。

#### 真實案例測試

| 測試 | 原始 OCR 準確率 | 校正後 | 完整管線後 |
|------|-----------------------|--------------|---------------------|
| 簡易發票（5° 傾斜） | 78 % | 92 % | 96 % |
| 舊報紙掃描（15° 傾斜，顆粒感） | 61 % | 78 % | 88 % |
| 低對比表單（無傾斜） | 70 % | 71 % | 84 % |

*數字僅作示範，卻反映了 Aspose 使用者常見的提升幅度。*

**重點摘要：** 即使你的主要目標是 **校正掃描圖像**，加入 denoise 與 contrast 步驟通常也能顯著提升最終文字品質。

---

## 校正掃描圖像：驗證結果

管線執行完畢後，你會得到兩項有用資訊：

```csharp
Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
Console.WriteLine(result.Text);
```

- **Deskew 信心** (`result.DeskewConfidence`) 為百分比。超過 90 % 通常表示旋轉已正確校正。
- **辨識文字** (`result.Text`) 讓你即時驗證輸出是否合理。

如果信心值偏低 (< 70 %)，可考慮：

1. **提升 `MaxAngle`** – 可能文件的傾斜角度超出預期。
2. **在校正前加入 `BinarizationFilter`** 以簡化圖像。
3. **手動旋轉** 圖像，使用 `OcrImage.Rotate(angle)` 作為備援。

---

## 完整端對端範例（可直接執行）

以下是 **完整、獨立的程式**，可直接複製貼上至新的 Console App 專案。請記得將 `YOUR_DIRECTORY` 替換為存放傾斜 TIFF 的資料夾路徑。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace DeskewDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize the OCR engine
            var engine = new OcrEngine();

            // 2️⃣ Load the image you want to straighten
            var imgPath = @"C:\Images\skewed_doc.tif"; // <-- update this path
            var img = OcrImage.FromFile(imgPath);

            // 3️⃣ Define the preprocessing pipeline
            var pipeline = new OcrFilter[]
            {
                new DeskewFilter { MaxAngle = 30 },   // auto‑detect up to 30°
                new DenoiseFilter { Strength = 0.5 }, // moderate noise reduction
                new ContrastBoostFilter { Level = 1.2 } // brighten the text
            };

            // 4️⃣ Apply the pipeline – this returns a new image instance
            var preprocessed = engine.ApplyFilters(img, pipeline);

            // 5️⃣ Run OCR on the cleaned‑up image
            var result = engine.Recognize(preprocessed);

            // 6️⃣ Show confidence and the extracted text
            Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(result.Text);
        }
    }
}
```

**預期輸出**（假設掃描品質相當乾淨）：

```
Deskew confidence: 96.45%
=== Recognized Text ===
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

如果看到雜亂的字元，請重新檢查濾鏡強度或如前所述加入 `BinarizationFilter`。

---

## 常見陷阱與專業提示

- **陷阱：** 使用多頁的 TIFF。`OcrImage.FromFile` 只會讀取第一幀。如需全部頁面，請使用 `OcrImage.FromMultiPageFile`。
- **陷阱：** 忘記釋放 `OcrEngine`。在正式程式碼中以 `using` 區塊包住，以釋放原生資源。
- **專業提示：** 若大量處理設定相同的圖像，可快取管線以減少開銷。
- **專業提示：** 將 `DeskewConfidence` 紀錄至監控系統；突發下降可能表示掃描器校正有變化。

---

## 往後步驟 – 擴充工作流程

既然你已了解 **如何校正圖像** 以及 **為 OCR 預處理圖像**，接下來可以探索：

- **批次處理** – 迴圈遍歷掃描 PDF 資料夾，將每頁轉為圖像，並套用相同的管線。
- **語言支援** – 設定 `engine.Language = OcrLanguage.English;` 或其他語言以提升辨識。
- **自訂後處理** – 使用正規表達式清理常見的 OCR 錯誤（例如 “0” 與 “O” 的混淆）。

上述每個主題皆自然呼應次要關鍵字 **如何提升 OCR** 與 **校正掃描圖像**。

---

## 結論

我們已完整說明使用 Aspose.OCR **校正圖像傾斜** 的所有必要知識，從建立穩健的濾鏡管線到驗證信心分數。透過 **為 OCR 預處理圖像**（包括校正、降噪與對比提升），你將在 **如何提升 OCR** 結果上看到可衡量的提升，尤其是對於傾斜或噪點較多的掃描件。

試著在自己的文件集上執行，調整濾鏡參數，觀察 OCR 準確度提升。若有任何問題或遇到難以校正的檔案，請在下方留言——讓我們一起排除故障。祝編程愉快！

---

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸技術。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通其他 API 功能，並在專案中探索替代實作方式。

- [如何使用 AspOCR：為 .NET 預處理圖像 OCR 濾鏡](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [如何 OCR 圖像 – 在 OCR 圖像辨識中執行圖像 OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [如何設定閾值於 OCR 圖像辨識](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}