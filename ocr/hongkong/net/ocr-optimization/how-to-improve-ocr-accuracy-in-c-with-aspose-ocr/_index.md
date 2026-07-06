---
category: general
date: 2026-04-11
description: 學習如何在 C# 中使用 Aspose OCR 識別 JPG 文字、校正圖像傾斜及去除噪點，以提升 OCR 效能。
draft: false
keywords:
- how to improve OCR
- recognize text from jpg
- extract text from image
- how to deskew image
- how to remove noise
language: zh-hant
og_description: 探索如何透過辨識 JPG 文字、校正影像傾斜與去除噪點來提升 OCR 效能——完整 C# 教學。
og_title: 如何在 C# 中使用 Aspose OCR 提升文字辨識準確度
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中使用 Aspose OCR 提升 OCR 準確度
url: /zh-hant/net/ocr-optimization/how-to-improve-ocr-accuracy-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose OCR 提升 OCR 準確度

有沒有想過 **如何提升 OCR** 的結果，當你的掃描檔看起來更像抽象藝術而不是可讀文字時？你並不是唯一的困擾者。在許多實務專案——例如發票、收據或手寫筆記——中，來源影像常常是傾斜的、顆粒感的，或是雜訊太多。好消息是？Aspose OCR 提供了一系列前處理參數，能把這些雜亂的影像變成乾淨、機器可讀的字元。在本教學中，我們將示範一個完整、可執行的範例，說明 **如何提升 OCR**，包括 **從 JPG 辨識文字**、校正圖片傾斜，以及去除不必要的雜訊。

> *小技巧：* 若跳過前處理，你很可能會得到像密碼填字遊戲般的亂碼輸出。讓我們避免這種情況。

![如何透過 Aspose OCR 前處理提升 OCR 效能](https://example.com/ocr-preprocess.png "如何透過 Aspose OCR 前處理提升 OCR 效能")

## 你將學到什麼

在接下來的幾分鐘內，你會看到：

1. 如何為取得最佳準確度而設定 Aspose OCR 引擎。  
2. **從 JPG 辨識文字** 所需的完整程式碼。  
3. 為什麼啟用 *AutoDeskew*（自動校正傾斜）與 *RemoveNoise*（去除雜訊）很重要，以及如何微調它們。  
4. 如何 **從影像檔案中擷取文字**，而不必自行撰寫過濾器。  
5. 常見陷阱（檔案遺失、不支援的格式）以及快速解決方法。

完成後，你將擁有一個單一的 C# 主控台應用程式，能接受任何 JPG、清理影像，並輸出擷取的字串——可直接供後續處理或儲存使用。

## 前置條件

- .NET 6.0 SDK 或更新版本（範例使用頂層語句以簡化程式碼）。  
- Aspose.OCR NuGet 套件（`dotnet add package Aspose.OCR`）。  
- 一張範例 JPG 影像（檔名為 `input.jpg`），放在可執行檔同一資料夾內。  
- 基本的 C# 語法認識——不需要進階概念。

如果你已經有專案，只要把程式碼貼上即可；若沒有，請建立新的主控台應用程式：

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

現在讓我們深入程式碼。

## 如何提升 OCR：前處理設定概覽

**如何提升 OCR** 的核心在於 `PreprocessSettings` 物件。它就像在實際字元辨識引擎啟動前執行的迷你影像編輯器。以下快速說明最具影響力的旗標：

| 設定                     | 功能說明                                                | 常見使用情境 |
|--------------------------|--------------------------------------------------------|--------------|
| `AutoDeskew`             | 套用深度學習去傾斜演算法。                              | 輕微傾斜的掃描頁面。 |
| `AdaptiveThreshold`      | 提升低光或褪色影像的對比度。                            | 墨水淡化的舊收據。 |
| `RemoveNoise`            | 使用高斯模糊濾鏡抑制斑點。                              | 手機閃光拍攝的照片。 |
| `NoiseRemovalStrength`   | 控制去噪力度（1 = 低，3 = 高）。                        | 依來源顆粒程度微調。 |

啟用這些選項基本上就是 **如何提升 OCR** 在不完美輸入上的「祕密醬料」。

## 使用 Aspose OCR 從 JPG 辨識文字

以下是完整、可直接執行的程式。每一行都有註解，讓你了解 *為什麼* 需要這段程式碼，而不只是 *它做什麼*。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class PreprocessDemo
{
    static void Main()
    {
        // ------------------------------------------------------------
        // Step 1: Create an OCR engine instance.
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ------------------------------------------------------------
        // Step 2: Fine‑tune preprocessing to improve accuracy.
        // ------------------------------------------------------------
        ocrEngine.Settings.Preprocess = new PreprocessSettings
        {
            AutoDeskew = true,               // How to deskew image automatically.
            AdaptiveThreshold = true,        // Improves contrast for better recognition.
            RemoveNoise = true,              // How to remove noise before OCR.
            NoiseRemovalStrength = 2         // Medium strength; adjust 1‑3 as needed.
        };

        // ------------------------------------------------------------
        // Step 3: Load the JPG image you want to process.
        // ------------------------------------------------------------
        // If the file is missing, Aspose will throw a FileNotFoundException.
        // Wrap it in a try/catch if you need graceful fallback.
        ImageStream image;
        try
        {
            image = ImageStream.FromFile("input.jpg");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading image: {ex.Message}");
            return;
        }

        // ------------------------------------------------------------
        // Step 4: Run the OCR engine on the preprocessed image.
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ------------------------------------------------------------
        // Step 5: Display the extracted text.
        // ------------------------------------------------------------
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### 預期輸出

若 `input.jpg` 內含文字「Invoice #12345 – Total: $256.78」，主控台會印出：

```
=== Extracted Text ===
Invoice #12345 – Total: $256.78
```

可以看到輸出乾淨，保留了破折號與美元符號——正是 **從影像檔案中擷取文字** 時所期待的結果。

## 使用前處理設定校正影像傾斜

為什麼校正傾斜很重要？即使只有 2 度的傾斜，也會干擾字元分割階段，導致字母辨識錯誤。`AutoDeskew` 旗標在底層使用卷積神經網路偵測主導角度，並將影像旋轉回基線。

如果需要更細部的控制，你也可以手動設定角度：

```csharp
ocrEngine.Settings.Preprocess = new PreprocessSettings
{
    AutoDeskew = false,          // Turn off automatic detection.
    // Manually specify a rotation angle (in degrees):
    DeskewAngle = -1.8           // Positive = clockwise, negative = counter‑clockwise.
};
```

> **何時使用手動校正傾斜：** 若你知道相機或掃描器固定以相同角度傾斜影像（例如固定式掃描器），硬編碼角度可以省下一點處理時間。

## 去除雜訊以取得更乾淨的擷取結果

雜訊通常以隨機斑點或顆粒形式出現在低光照片中。`RemoveNoise` 旗標會套用雙邊濾鏡，平滑背景同時保留邊緣（即實際字元）。`NoiseRemovalStrength` 屬性讓你調整去噪力度：

| 強度 | 效果說明 |
|------|----------|
| 1    | 輕度平滑——適合略帶顆粒的圖片。 |
| 2    | 中等平衡——適用大多數手機拍攝。 |
| 3    | 重度平滑——當影像極度雜訊時使用，但要留意會模糊細小筆畫。 |

若在使用高強度平滑後，細小字體變得難以辨識，只需降低強度或直接關閉此濾鏡。

## 從影像擷取文字：不只限於 JPG

雖然示範以 JPG 為例，Aspose OCR 同時支援 PNG、BMP、TIFF，甚至 PDF 頁面。若要 **從影像檔案中擷取文字**（非 JPG），只要在 `ImageStream.FromFile` 中更改副檔名即可。對於多頁 TIFF，你可以遍歷每一頁：

```csharp
for (int i = 0; i < tiffPageCount; i++)
{
    ImageStream page = ImageStream.FromFile($"input_{i}.tiff");
    OcrResult result = ocrEngine.Recognize(page);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(result.Text);
}
```

上述程式碼展示了如何將相同的 **如何提升 OCR** 工作流程擴展至批次處理整批掃描文件。

## 常見陷阱與解決方法

| 症狀 | 可能原因 | 快速解決方案 |
|------|----------|--------------|
| 輸出空白 | 前處理過度導致影像全白（門檻過高） | 降低 `NoiseRemovalStrength` 或將 `AdaptiveThreshold = false`。 |
| 文字雜亂 | 語言模型錯誤（預設為英文） | 設定 `ocrEngine.Settings.Language = Language.English;` 或載入自訂語言套件。 |
| 大檔案當機 | 高解析度影像導致記憶體不足 | 在辨識前使用 `ocrEngine.Settings.ImageResizeFactor = 0.5;` 縮小影像。 |
| 旋轉掃描無輸出 | 不小心關閉 `AutoDeskew` | 開啟 `AutoDeskew = true` 或提供正確的 `DeskewAngle`。 |

記住這些要點，能在生產環境中節省大量除錯時間，讓你更快達成 **如何提升 OCR** 的目標。

## 加速 vs. 準確度的調整技巧

如果每天要處理上千張收據，可能會優先考慮速度。關閉 `AdaptiveThreshold` 並將 `NoiseRemovalStrength = 1`。相反地，若是法律文件，錯過一個字元可能代價高昂，則全部開啟，甚至把 `NoiseRemovalStrength` 提升至 3。

## 結語

我們已完整說明在 C# 中使用 Aspose OCR **如何提升 OCR** 的全流程：從建立引擎、設定前處理（即 *如何校正影像傾斜* 與 *如何去除雜訊* 的核心）、載入 JPG、辨識文字、以及處理各種邊緣情況。程式碼自包含、即拿即用，示範了 **從 jpg 辨識文字** 以及 **從影像檔案中擷取文字** 的每一步。

### 接下來可以做什麼？

- 嘗試其他影像格式（PNG、TIFF），觀察相同設定的表現差異。  
- 將 OCR 輸出整合至資料庫或

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}