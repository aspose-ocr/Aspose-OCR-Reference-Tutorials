---
category: general
date: 2026-04-08
description: 使用 Aspose OCR 於 C# 從圖像提取文字。了解如何對圖像進行預處理以供 OCR 使用，以及如何預處理圖像以提升準確度。
draft: false
keywords:
- extract text from image
- preprocess image for ocr
- how to preprocess image
- Aspose OCR C#
- image preprocessing techniques
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中從圖像提取文字。本指南說明如何為 OCR 預處理圖像，以及如何預處理圖像以獲得最佳效果。
og_title: 使用 Aspose OCR 從圖像擷取文字 – 完整 C# 指南
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 使用 Aspose OCR 從圖像提取文字 – 完整 C# 教學
url: /zh-hant/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 從圖像提取文字 – 完整 C# 指南

是否曾需要 **從圖像提取文字**，但結果充滿錯誤？你並不孤單——大多數開發人員在來源圖片傾斜、雜訊多或對比度低時都會遇到這個問題。好消息是，簡短的前處理流程可以把模糊的快照變成 OCR 的乾淨來源，而 Aspose OCR 讓整個過程變得輕而易舉。

在本教學中，我們將逐步示範一個實務範例，說明如何使用 Aspose OCR 內建濾鏡 **前處理圖像以供 OCR**，然後僅用幾行 C# 代碼 **從圖像提取文字**。完成後，你將擁有可直接執行的程式，了解每個濾鏡的重要性，並知道如何為自己的特殊情況微調流程。

## 需要的環境

- .NET 6.0 或更新版本（此程式碼亦可在 .NET Framework 4.7+ 上執行）
- Aspose.OCR NuGet 套件 (`Install-Package Aspose.OCR`)
- 一張傾斜、雜訊或低對比度的範例圖像（例如 `skewed_noisy.jpg`）
- 任意你喜歡的 IDE——Visual Studio、Rider 或 VS Code 都可

不需要額外的原生函式庫、亦不需 Web 服務，僅使用純 C#。

## 步驟 1：設定 OCR 引擎 – 提取文字的起點

首先，建立一個 `OcrEngine` 實例，並告訴它要辨識的語言。英語最常用，但你可以將 `"en"` 換成 `"fr"`、`"de"` 等語言代碼。

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void PreprocessAndOcr()
    {
        // 1️⃣ Initialize the OCR engine – this is where we define the language.
        var ocrEngine = new OcrEngine { Language = "en" };
```

**為何重要：** 引擎內部保存字典與語言特定的啟發式演算法。如果省略語言設定，Aspose 會預設為英語，但明確指定可避免日後切換語系時產生意外。

## 步驟 2：建立前處理管線 – 如何前處理圖像以獲得最佳結果

現在我們加入濾鏡。把它們想像成在 OCR 步驟之前自動執行的迷你影像編輯套件。以下三個濾鏡涵蓋最常見的問題：

| Filter | 修正內容 | 使用時機 |
|--------|---------------|----------------|
| `DeskewFilter` | 將圖像旋轉回水平 | 角度拍攝的圖片 |
| `DenoiseFilter` | 減少隨機斑點與顆粒 | 低光照片或掃描文件 |
| `ContrastStretchFilter` | 提升對比，使深色文字更突出 | 褪色的列印品或顏色淡化的螢幕截圖 |

```csharp
        // 2️⃣ Add preprocessing steps – this is the core of “how to preprocess image”.
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast
```

**小技巧：** 順序很重要。先去傾斜（Deskew），再去雜訊（Denoise），最後拉伸對比（ContrastStretch）。若顛倒順序，可能會放大雜訊而非消除。

## 步驟 3：執行 OCR – 最終從圖像提取文字

管線就緒後，將圖片路徑交給引擎。Aspose 會自動套用濾鏡，然後執行辨識演算法。

```csharp
        // 3️⃣ Recognize text from the pre‑processed image.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");
```

若找不到檔案，會拋出明確的 `FileNotFoundException`。因此我們建議在開發階段使用絕對路徑，之後在正式環境改用相對路徑或設定值。

## 步驟 4：顯示結果 – 看看得到什麼

`OcrResult` 物件包含原始文字、信心分數，甚至每個字的邊界框。為了快速示範，我們只會把文字印到主控台。

```csharp
        // 4️⃣ Output the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

執行程式後，你應該會看到類似以下的輸出：

```
=== OCR Output ===
Invoice Number: 2023-0456
Date: 03/15/2024
Total: $1,234.56
```

若輸出雜亂，請再次檢查圖像品質，或嘗試加入其他濾鏡（例如針對二值圖的 `BinarizationFilter`）。

## 完整範例 – 複製貼上即可執行

以下是完整、獨立的程式。只需將 `YOUR_DIRECTORY/skewed_noisy.jpg` 替換為實際測試圖像的路徑即可。

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void Main()
    {
        PreprocessAndOcr();
    }

    public static void PreprocessAndOcr()
    {
        // Step 1: Create OCR engine and set language
        var ocrEngine = new OcrEngine { Language = "en" };

        // Step 2: Build preprocessing pipeline
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast

        // Step 3: Recognize text from the pre‑processed image
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // Step 4: Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**預期輸出** – 主控台會印出圖像中文字的純文字表示。若圖像是一個寫著 “OpenAI” 的簡單標誌，則會只看到該字，沒有額外符號。

## 邊緣案例與管線微調方法

### 1️⃣ 超暗圖像

若對比濾鏡仍不足，可在前面加入 `BrightnessCorrectionFilter`：

```csharp
ocrEngine.Preprocess.Add(new BrightnessCorrectionFilter(30)); // increase brightness by 30%
```

### 2️⃣ 多語言文件

設定 `Language = "en+fr"`（Aspose 支援以逗號分隔的語言代碼），若希望引擎自動偵測，可加入 `LanguageDetectionFilter`。

### 3️⃣ 大型 PDF 轉圖像

一次處理千頁 PDF 的每頁圖像會很慢。可使用 `Parallel.ForEach` 同時對多張圖像執行 OCR，但請記得 `OcrEngine` 並非執行緒安全——每個執行緒需建立獨立的實例。

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine { Language = "en" };
    // add same filters...
    var result = engine.RecognizeImage(path);
    // store result...
});
```

### 4️⃣ 取得邊界框

若需要每個字的座標（例如做高亮顯示），可檢查 `ocrResult.Regions`。每個區域都包含 `Rectangle` 座標，可用於 UI 疊加層。

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

## 常見陷阱（以及如何避免）

- **省略 Deskew 步驟** – 即使是 2 度的傾斜也會使信心下降約 20 %。當來源未完全對齊時，務必加入 `DeskewFilter`。
- **使用高壓縮率的 JPEG** – 壓縮雜訊會被當成噪點；改用 PNG 或 TIFF 可提升 OCR 效果。
- **硬編碼路徑** – 相對路徑在本機可行，但在 CI/CD 流程中應從設定或環境變數讀取圖像位置。

## 測試你的設定

1. 使用乾淨、高對比度的圖像執行程式，應能取得近乎完美的文字。
2. 換成雜訊多、傾斜的照片，確認加入三個濾鏡後輸出是否改善。
3. 逐一移除濾鏡進行實驗，觀察其影響——這有助於了解每個步驟 *為何* 重要。

## 結論

我們剛剛示範了如何使用 Aspose OCR **從圖像提取文字**，同時展示了一種在大多數實務情境下有效的 **前處理圖像以供 OCR** 方法。透過串接 `DeskewFilter`、`DenoiseFilter` 與 `ContrastStretchFilter`，為引擎提供乾淨的畫布，顯著提升辨識準確度。

接下來，你可以探索更進階的濾鏡、處理多頁文件，或將 OCR 結果整合至搜尋索引。無論選擇何種方式，核心流程——初始化、前處理、辨識、消費——皆保持不變。

想更上一層樓嗎？可嘗試加入 `BinarizationFilter` 以處理黑白掃描，或將輸出接入資料庫以產生可搜尋的 PDF。祝開發順利，願每張送入 Aspose 的圖像都能返回清晰可讀的文字！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}