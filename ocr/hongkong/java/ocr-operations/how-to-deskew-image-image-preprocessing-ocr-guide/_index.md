---
category: general
date: 2026-06-22
description: 如何校正影像傾斜以進行 OCR：學習影像前處理的 OCR 步驟、去除鹽與胡椒雜訊，提升辨識準確度。
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: zh-hant
og_description: 如何在完整的 Java 範例中對圖像進行去斜校正、去除鹽胡椒噪聲，並套用圖像前處理 OCR 技術。
og_title: 如何校正圖像傾斜 – 圖像前處理 OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: 如何校正圖像傾斜 – 圖像前處理 OCR 指南
url: /zh-hant/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何校正圖像傾斜 – 圖像前處理 OCR 指南

有沒有想過 **如何校正圖像傾斜**，讓你的 OCR 引擎真的能讀取文字？你並不是唯一遇到這個問題的人。傾斜的掃描會把完美的文件變成一團亂碼，而且大多數開發者至少會遇到一次這種情況。

在本教學中，我們將逐步說明完整的 **image preprocessing OCR** 工作流程，不僅校正旋轉，還會 **remove[s] salt pepper** 雜訊並提升對比度——基本上涵蓋了在將圖像送入引擎前 **preprocess images OCR**‑風格所需的全部前處理。完成後，你將擁有一段可直接執行的 Java 程式碼片段，以及對每個步驟重要性的清晰概念。

## 如何校正圖像傾斜 – 建立前處理管線

任何 OCR 友好工作流程的核心是一個 **preprocess options** 物件，用於串接一系列過濾器。把它想像成傳送帶：每個過濾器執行單一任務，然後將圖像傳遞給下一個。以下是一個最小但完整的範例，使用假想的 OCR 函式庫，內含 `DeskewFilter`、`DenoiseFilter` 與 `ContrastBoostFilter`。

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### 為什麼這樣有效

* **DeskewFilter** 會分析圖像中主要的文字行，估算傾斜角度，並將位圖旋轉回水平。大多數函式庫將校正範圍限制在 ±15°，因為更大的角度通常代表掃描品質差，需要手動處理。
* **DenoiseFilter** 針對經典的 *salt‑and‑pepper* 模式——那些孤立的黑白像素，像電視的雜訊。移除它們可防止 OCR 引擎將噪點誤認為字元。
* **ContrastBoostFilter** 拉伸直方圖，使淡弱的筆畫更突出。`1.5f` 的倍率是一個安全的預設值；如果你的掃描圖像特別暗淡，可以適度提升。

> **專業提示：** 若你知道文件的傾斜角度永遠不會超過 10°，可將此較小的上限傳給 `DeskewFilter`——演算法執行更快，且較不會過度校正。

## Image Preprocessing OCR：正確排序加入過濾器

順序很重要。想像在校正傾斜之前先去噪聲；噪點可能會干擾角度偵測，導致校正結果錯位。相反地，在校正傾斜之後再提升對比度，則可確保旋轉不會產生新的雜訊。

以下是一個快速檢查清單，你可以直接複製貼上到任何專案中：

| 步驟 | 過濾器 | 原因 |
|------|--------|--------|
| 1 | `DeskewFilter` | 對齊文字基線 |
| 2 | `DenoiseFilter` | 移除孤立像素噪點 |
| 3 | `ContrastBoostFilter` | 提升 OCR 可讀性 |

如果需要插入其他步驟——例如，用於二值化 OCR 的 **binarization** 過濾器——應該將它放在對比度提升 **之後**，因為乾淨且高對比度的圖像能更精確地進行二值化。

## 使用 DenoiseFilter 移除鹽與胡椒雜訊

鹽與胡椒雜訊在低品質掃描中相當常見，尤其是來自廉價手機相機的圖像。我們函式庫中的 `DenoiseFilter` 採用中值濾波核，將每個像素替換為其鄰域的中位數。效果是？這些斑點會消失，同時不會模糊真正的字元。

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*何時需要增大核大小？* 若你的來源圖像充斥著較大的斑點，較大的核可以將它們清除，但要小心：核太大可能會抹掉細小字體的細筆畫。

## Preprocess Images OCR – 套用管線

組好過濾器鏈後，將它附加到引擎只需一行程式碼 (`engine.setPreprocessOptions`)。從此之後，每次呼叫 `recognizeText` 都會自動通過管線。無需手動逐一呼叫過濾器——程式碼保持簡潔，未來的變更（新增過濾器、調整參數）也集中管理。

以下是一個成功執行的範例，使用原本有 12° 傾斜且明顯鹽與胡椒雜訊的掃描圖像：

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

請注意，文字已變得乾淨、方向正確，且不會出現原本會變成 “I n v o i c e” 或 “$‑‑‑” 的雜散字元。

## 邊緣情況與常見陷阱

| 情況 | 需留意的事項 | 建議解決方案 |
|-----------|-------------------|---------------|
| Rotation > 15° | DeskewFilter 可能會放棄校正 | 手動先旋轉或使用更大範圍的過濾器 |
| Extremely low resolution ( < 100 dpi ) | 對比度提升無法恢復細節 | 先重新取樣圖像（例如 `ResampleFilter`） |
| Mixed noise (Gaussian + salt‑pepper) | `DenoiseFilter` 單獨不足 | 在 `DenoiseFilter` 前加入 `GaussianBlurFilter` |
| Color scans with colored text | 需要灰階轉換 | 在對比度提升前插入 `GrayscaleFilter` |

預先考慮這些情況，可為你節省大量日後除錯的時間。

## 完整可執行範例（全功能）

以下是一個獨立的 Java 類別，你可以將它放入任何包含 `com.example.ocr` 相依性的 Maven 或 Gradle 專案中。它示範了 **how to deskew image**、**remove salt pepper** 雜訊，以及 **preprocess images OCR**‑風格的前處理。

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**預期輸出**（假設 `scanned-document.png` 為清晰的發票圖像）：

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

如果你換成已經完美對齊的圖像，你會發現管線仍會執行——不會出錯，且 OCR 準確度仍保持在高水平。

## 結論

你現在已經對 **how to deskew image** 有了扎實的了解，並明白每個前處理步驟——**image preprocessing OCR**、**remove salt pepper**、以及 **preprocess images OCR**——在產出乾淨、可搜尋的文字時扮演關鍵角色。上述範例是一個完整的，

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在此處示範的技巧之上。每個資源都提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Calculate Skew Angle for OCR Image Preprocessing](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}