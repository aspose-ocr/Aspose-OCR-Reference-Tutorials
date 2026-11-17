---
category: general
date: 2026-03-15
description: 使用 Aspose OCR 於 C# 執行影像的 OCR。了解如何在 OCR 前對影像進行前處理，以提升 OCR 準確度，並有效辨識影像中的文字。
draft: false
keywords:
- perform OCR on image
- recognize text from image
- improve OCR accuracy
- preprocess image before OCR
language: zh-hant
og_description: 使用 Aspose OCR 於圖像執行文字辨識。本指南說明如何在 OCR 前對圖像進行預處理、提升 OCR 準確度，以及在 C# 中從圖像辨識文字。
og_title: 對圖像執行 OCR – 使用 Aspose OCR 提升準確度
tags:
- C#
- Aspose OCR
- Image Processing
title: 對圖片執行 OCR – 提升 Aspose OCR 的準確度
url: /zh-hant/net/ocr-optimization/perform-ocr-on-image-boost-accuracy-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在圖像上執行 OCR – 使用 Aspose OCR 提升準確度

曾經需要 **perform OCR on image** 檔案卻一直得到亂碼輸出嗎？你並不孤單。在許多實務專案中，噪點多、傾斜的掃描件甚至會讓最好的 OCR 引擎失靈，導致文字看起來像是貓在鍵盤上走過所打出的。

事實上，原始圖片只解決了一半的問題。透過 **preprocess image before OCR**，你可以大幅 **improve OCR accuracy**，最終可靠地 **recognize text from image**。在本教學中，我們將逐步說明一個完整、可直接執行的 C# 範例，展示如何使用 Aspose.OCR 完成這些步驟。

我們將涵蓋：

* 安裝 Aspose.OCR NuGet 套件。  
* 建立前處理管線（去斜、去噪、對比度提升、二值化）。  
* 執行 OCR 引擎並列印辨識出的文字。  

不會有冗長說明或「稍後再看文件」的捷徑——只提供一個可直接放入 Console 應用程式的完整解決方案。

---

## 需要的環境

在開始之前，請確保你已具備：

* **.NET 6+**（或 .NET Framework 4.6.2+）。  
* 最新的 **Aspose.OCR** NuGet 套件（v23.10 或更新版本）。  
* 一張稍嫌雜亂的影像檔——例如有傾斜、噪點、低對比度等情況。  
* Visual Studio、VS Code，或任何你慣用的 IDE。

就這樣。如果缺少 NuGet 套件，請執行：

```bash
dotnet add package Aspose.OCR
```

現在讓我們動手實作。

---

## ## 在圖像上執行 OCR – 設定引擎

第一步是建立 `OcrEngine` 實例。這個物件是 Aspose OCR 的核心，負責保存設定、管線以及實際的辨識邏輯。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System.Drawing;          // For Image class
using System;                  // For Console

// Step 1: Instantiate the OCR engine
var ocrEngine = new OcrEngine();
```

> **Why this matters:**  
> 建立引擎可讓你從乾淨的起點開始。之後若要更換設定（語言、辨識模式等），不必修改其他程式碼。

---

## ## 前處理影像 – 建立管線

原始掃描很少是完美的。完善的前處理管線可在某些情況下 **improve OCR accuracy** 高達 30 %。以下我們串接四個濾鏡：

| 濾鏡 | 功能說明 | 典型值 |
|--------|--------------|----------------|
| `DeskewFilter` | 偵測並校正旋轉 | `Angle = 0.0` (auto‑detect) |
| `DenoiseFilter` | 移除斑點與顆粒 | `Strength = 70` (out of 100) |
| `ContrastBoostFilter` | 讓深色文字更突出 | `Strength = 40` |
| `BinarizationFilter` | 將影像轉為純黑白 | `Threshold = 128` |

```csharp
// Step 2: Create a preprocessing pipeline
var preprocessingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { Angle = 0.0 })               // auto‑detect skew angle
    .Add(new DenoiseFilter { Strength = 70 })           // reduce noise
    .Add(new ContrastBoostFilter { Strength = 40 })     // enhance contrast
    .Add(new BinarizationFilter { Threshold = 128 });   // convert to B/W

// Attach the pipeline to the OCR engine
ocrEngine.Configuration.PreProcessing = preprocessingPipeline;
```

> **Pro tip:** 若來源影像已相當乾淨，可省略 `DenoiseFilter`，或降低其 `Strength`。過度濾鏡有時會抹除細微字元。

---

## ## 載入影像 – 檔案位置說明

現在把引擎指向要辨識的圖片。`Image.FromFile` 方法支援 System.Drawing 可處理的所有格式（JPEG、PNG、BMP 等）。

```csharp
// Step 3: Load the image you want to recognize
var inputImagePath = @"C:\Images\skewed_noisy.jpg";   // change to your path
var inputImage = Image.FromFile(inputImagePath);
```

> **Edge case:** 若檔案路徑包含空格或 Unicode 字元，請如上例使用逐字字串 (`@"..."`) 包住。另外，正式環境請務必捕捉 `FileNotFoundException`。

---

## ## 從影像辨識文字 – 執行 OCR 引擎

引擎設定完成且影像已載入後，實際辨識只需一行程式碼。結果會包含擷取的文字以及可供日後檢查的信心指標。

```csharp
// Step 4: Perform OCR and get the result
var ocrResult = ocrEngine.Recognize(inputImage);

// Display the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

執行程式時，你應該會看到類似以下的輸出：

```
=== OCR Output ===
Invoice #12345
Date: 03/12/2026
Total: $1,250.00
```

如果輸出看起來不正常，請調整管線的強度或嘗試不同的 `Threshold` 值。微調往往能帶來顯著差異。

---

## ## 常見問題與解決方式

1. **Result is empty or mostly gibberish**  
   *檢查管線。* 過度去噪可能會抹除細線條。降低 `Strength` 或暫時註解掉該濾鏡。

2. **Skew isn’t corrected**  
   `DeskewFilter` 最適用於文字基線大致水平的文件。若影像旋轉超過 15°，可能需要先使用 `RotateFlip` 手動旋轉。

3. **Non‑Latin characters aren’t recognized**  
   預設 Aspose OCR 使用英文語言模型。於呼叫 `Recognize` 前，將 `ocrEngine.Configuration.Language` 設為相應的 ISO 代碼（例如 `"fr"` 代表法文）。

```csharp
ocrEngine.Configuration.Language = "fr";   // for French text
```

4. **Performance feels slow**  
   若一次處理數百頁，請重複使用同一個 `OcrEngine` 實例，僅在每次迴圈中更換 `Image` 物件。每次重新建立引擎會增加不必要的開銷。

---

## ## 視覺結果 – 前處理後的影像長什麼樣

以下示意前後對比（實際輸出可能有所不同）。

![執行 OCR 圖像結果](https://example.com/ocr-before-after.png "執行 OCR 圖像 – 前處理前後比較")

*Alt text:* 「執行 OCR 圖像 – 原始噪點掃描與前處理後可供 OCR 使用的版本比較」。

---

## ## 完整範例：可直接執行的程式碼

將下方完整程式碼貼到新建的 Console 專案（`dotnet new console`）中，然後按 **F5**。它會編譯、執行，並將辨識出的文字印到主控台。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System.Drawing;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build a preprocessing pipeline (improve OCR accuracy)
        var preprocessingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { Angle = 0.0 })               // auto‑detect skew angle
            .Add(new DenoiseFilter { Strength = 70 })           // reduce noise
            .Add(new ContrastBoostFilter { Strength = 40 })     // enhance contrast
            .Add(new BinarizationFilter { Threshold = 128 });   // convert to B/W

        ocrEngine.Configuration.PreProcessing = preprocessingPipeline;

        // 3️⃣ Load the image you want to read
        var imagePath = @"YOUR_DIRECTORY\skewed_noisy.jpg";   // ← update this path
        var inputImage = Image.FromFile(imagePath);

        // 4️⃣ Run OCR – recognize text from image
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Show the result
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Expected output:** 主控台會印出圖片上文字的純文字版——無論是發票、護照掃描，或是手寫筆記。

---

## ## 往後的方向 – 深入探索

* **批次處理：** 在 `foreach` 迴圈中呼叫辨識，處理整個資料夾的影像。  
* **語言套件：** 從 Aspose 安裝額外語言資料，以 **recognize text from image** 支援西班牙文、德文、中文等。  
* **自訂後處理：** 使用正規表達式從 OCR 結果中抽取日期、金額或身分證號。  
* **其他函式庫比較：** 與 Tesseract 或 Microsoft Azure Computer Vision 比較，看看 **preprocess image before OCR** 在不同平台上的表現。

---

## ## 結論

我們剛剛示範了如何使用 Aspose OCR **perform OCR on image**，建構智慧的前處理管線，並證明 **preprocess image before OCR** 能顯著 **improve OCR accuracy**。依照上述步驟，你現在可以在任何 C# 應用程式中可靠地 **recognize text from image**——不再為亂碼輸出苦惱。

歡迎自行調整濾鏡強度、嘗試不同影像格式，或將此程式碼整合至更大型的文件處理服務。只要 OCR 管線穩固，未來的可能性無限。

有任何問題或酷炫的使用案例嗎？在下方留言，我們一起討論，祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}