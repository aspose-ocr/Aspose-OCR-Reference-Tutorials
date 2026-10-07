---
category: general
date: 2026-03-02
description: 如何在 C# 中使用 Aspose OCR 執行光學字符辨識 – 學習預處理影像以供 OCR、去除噪點、自動校正傾斜及提升對比度。
draft: false
keywords:
- how to perform OCR
- preprocess image for OCR
- remove noise from image
- auto deskew image
- boost image contrast
language: zh-hant
og_description: 如何在 C# 中使用完整的前處理流程執行 OCR。學習去除雜訊、自動校正傾斜以及提升對比度，以獲得最佳效果。
og_title: 如何在 C# 中執行 OCR – 逐步指南
tags:
- OCR
- C#
- Image Processing
title: 如何在 C# 中執行 OCR – 包含預處理的完整指南
url: /zh-hant/net/ocr-optimization/how-to-perform-ocr-in-c-complete-guide-with-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 完整指南與前處理

有沒有想過 **如何執行 OCR** 在模糊、傾斜的掃描檔上，而不需要花上數小時調整設定？你並不孤單。在許多實務專案中，來源影像往往雜訊多、傾斜，或是對比度低，直接送入 OCR 引擎通常會得到一堆垃圾。  

好消息是？只要加入幾個聰明的前處理步驟——**preprocess image for OCR**、**remove noise from image**、**auto deskew image** 與 **boost image contrast**——就能在數秒內把雜亂的影像變成可讀的文字。以下提供一個即時可執行的 C# 範例，完整示範這些步驟，並說明每個濾鏡的原理。

![如何執行 OCR 範例](ocr-example.png "如何執行 OCR 範例")

## 您將學會

- 在 .NET 專案中安裝並引用 Aspose.OCR。  
- 載入 bitmap 並建立前處理管線，以處理傾斜、雜訊與暗淡問題。  
- 執行 OCR 引擎並輸出辨識出的字串。  
- 提供調整濾鏡、處理例外情況與擴充解決方案的技巧。  

不需要外部文件，也沒有模糊的「請參考 API」連結——只有一份可自行複製貼上、立即執行的完整指南。

---

## 如何執行 OCR – 設定專案

### 1️⃣ 安裝 Aspose.OCR NuGet 套件

在解決方案資料夾中開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

> **專業提示：** 使用最新的穩定版（截至 2026 年 3 月，v23.10）。較新版會加入雜訊移除的效能優化。

### 2️⃣ 新增必要的 `using` 指令

```csharp
using Aspose.OCR;
using System.Drawing;
using System;
```

這些指令會將 OCR 引擎、bitmap 處理與主控台工具納入作用範圍。

---

## 前處理影像以供 OCR – 濾鏡說明

收據的原始照片很少看起來像教科書頁面。以下三個濾鏡可解決最常見的問題。

### 3️⃣ 載入輸入影像

```csharp
// Step 3: Load the image you want to read
Bitmap inputImage = new Bitmap(@"YOUR_DIRECTORY/skewed_noisy.jpg");
```

將 `YOUR_DIRECTORY` 替換為放置測試影像的資料夾。檔案 `skewed_noisy.jpg` 應為真實範例——有傾斜、顆粒感且稍微偏暗。

### 4️⃣ 建立前處理管線

```csharp
// Step 4: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Step 5: Attach filters – this is where we *preprocess image for OCR*
ocrEngine.PreprocessFilters
    .Add(new AutoDeskewFilter())                     // auto deskew image
    .Add(new NoiseRemovalFilter())                   // remove noise from image
    .Add(new ContrastBoostFilter { Level = 1.5 });   // boost image contrast
```

#### 為何每個濾鏡重要

| 濾鏡 | 功能說明 | 何時需要 |
|--------|--------------|------------------|
| **AutoDeskewFilter** | 偵測主要文字角度，並旋轉 bitmap 使文字水平。 | 掃描圖像傾斜（手機拍照常見）。 |
| **NoiseRemovalFilter** | 使用基於中位數的去雜訊演算法，平滑斑點而不模糊字元。 | 影像有顆粒、鹽與胡椒雜訊或壓縮產生的雜訊。 |
| **ContrastBoostFilter** | 乘算像素強度差異；`Level = 1.5` 為安全預設值。 | 文字在淡色背景上顯得暗淡。 |

如果你處理的是完全平整、乾淨的掃描檔，可以直接省略整個管線，但額外負擔微乎其微——因此我們通常仍保留它。

---

## 辨識文字並取得結果

### 5️⃣ 執行 OCR 引擎

```csharp
// Step 6: Recognize text from the preprocessed image
string recognizedText = ocrEngine.Recognize(inputImage);
```

在底層，Aspose.OCR 會先自行進行影像增強，然後再將 bitmap 送入辨識模型。我們的外部濾鏡僅是提供更乾淨的起始影像。

### 6️⃣ 顯示擷取的文字

```csharp
// Step 7: Output the result to the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

執行程式後，你應該會看到一段可讀的文字，與原始文件相符。對於範例 `skewed_noisy.jpg`，輸出大致如下：

```
=== OCR Result ===
Invoice #12345
Date: 02/01/2026
Total: $1,245.67
Thank you for your business!
```

若結果仍出現亂碼，請考慮將 `ContrastBoostFilter.Level` 提升至 `2.0`，或在辨識前加入 `BinarizationFilter`（另一個 Aspose 類別）。

---

## 邊緣情況與常見變化

| 情況 | 建議調整 |
|-----------|-----------------|
| **Very dark background** | 在對比度提升前加入 `BrightnessAdjustmentFilter { Level = 0.3 }`。 |
| **Colored text** | 在去雜訊前使用 `GrayscaleFilter` 將影像轉為灰階。 |
| **Multiple languages** | 建立引擎後設定 `ocrEngine.Language = Language.English | Language.Spanish;`。 |
| **Large PDFs** | 將每一頁作為獨立的 bitmap 處理，以降低記憶體使用。 |

請記住，前處理是 *反覆* 的過程。執行 OCR、檢視輸出，然後調整濾鏡參數，直到滿意為止。

---

## 完整可執行範例（即貼即用）

```csharp
// ------------------------------------------------------------
// Complete OCR example with preprocessing (Aspose.OCR)
// ------------------------------------------------------------
using Aspose.OCR;
using System.Drawing;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the image – replace path with your own file
        Bitmap inputImage = new Bitmap(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 2️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Add preprocessing filters
        ocrEngine.PreprocessFilters
            .Add(new AutoDeskewFilter())                     // auto deskew image
            .Add(new NoiseRemovalFilter())                   // remove noise from image
            .Add(new ContrastBoostFilter { Level = 1.5 });   // boost image contrast

        // 4️⃣ Perform recognition
        string recognizedText = ocrEngine.Recognize(inputImage);

        // 5️⃣ Show the result
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

將此檔案存為 `Program.cs`，執行 `dotnet run`，即可在主控台看到擷取的文字。這就是完整的 **how to perform OCR** 工作流程，程式碼不到 30 行。

---

## 常見問與答 (FAQ)

**Q: 這在 .NET Core 與 .NET Framework 上能運作嗎？**  
A: 可以。Aspose.OCR 以 .NET Standard 2.0 為目標，因此可在 .NET 5、6、7，或傳統的 Framework 4.8 上執行。

**Q: 如果我的影像是 PDF 頁面呢？**  
A: 先將每一頁 PDF 轉為 bitmap（例如使用 `Aspose.PDF`），再將 bitmap 送入相同的管線。

**Q: 我可以在 Linux 上執行嗎？**  
A: 完全可以。此函式庫跨平台；只要確保已安裝 `System.Drawing.Common` 所需的原生相依性（在 Ubuntu 上安裝 `libgdiplus`）。

**Q: 如何處理非常大的文件？**  
A: 每次處理單一頁面，並在每次 OCR 呼叫後釋放 bitmap（`bitmap.Dispose()`），以降低記憶體佔用。

---

## 結論

現在你已掌握在 C# 中執行 **how to perform OCR** 的方法，透過完整的前處理鏈結 **preprocesses image for OCR**、**removes noise from image**、**auto deskews image** 與 **boosts image contrast**。依照上述步驟，即可將雜亂的掃描檔轉換為乾淨、可搜尋的文字，只需幾行程式碼。

準備好迎接下一個挑戰了嗎？試著調整不同的濾鏡等級、加入二值化步驟，或整合語言偵測以處理多語言收據。同樣的模式也適用於身分證、護照，甚至手寫筆記——只要依實際視覺特性替換相應的濾鏡即可。

如果你覺得本指南有幫助，請在 GitHub 上給予星標，與同事分享，或在下方留下評論。祝編程愉快，願你的 OCR 永遠清晰！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}