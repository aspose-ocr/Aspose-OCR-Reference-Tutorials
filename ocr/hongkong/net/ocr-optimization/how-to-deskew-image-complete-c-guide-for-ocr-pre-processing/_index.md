---
category: general
date: 2026-03-20
description: 學習如何使用 Aspose OCR 進行圖像去斜與去除噪點。本分步指南亦說明如何為 OCR 預處理圖像並提升 OCR 準確度。
draft: false
keywords:
- how to deskew image
- remove image noise
- preprocess image for OCR
- recognize text from image
- improve OCR accuracy
language: zh-hant
og_description: 學習如何使用 Aspose OCR 校正圖像傾斜並清除噪點。只需數分鐘即可提升 OCR 準確度。
og_title: 如何去除圖像傾斜 – 完整的 C# OCR 前處理指南
tags:
- OCR
- C#
- Image Processing
title: 如何校正圖像傾斜 – 完整的 C# OCR 前處理指南
url: /zh-hant/net/ocr-optimization/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何校正影像傾斜 – 完整的 C# OCR 前處理指南

有沒有想過 **如何校正影像傾斜**，當掃描器掃出的檔案呈現奇怪的角度時？你並非唯一遇到這個問題的人；許多開發者在將照片輸入 OCR 引擎時都會卡關。好消息是，只要幾行 C# 程式碼加上 Aspose OCR，就能在同一條整潔的管線中校正、去噪、提升對比度——根本不需要 Photoshop。

在本教學中，我們將一步步說明您需要了解的所有內容：從載入傾斜的圖片、**去除影像噪點**、**為 OCR 前處理影像**，最後**辨識影像中的文字**，以獲得高 **提升 OCR 準確度** 的分數。完成後，您將擁有一個可直接執行的主控台應用程式，將雜亂的掃描檔轉換為乾淨且可搜尋的文字。

## 您需要的環境

- .NET 6 或更新版本（程式碼使用 `using var` 語法，支援自 C# 8 起）
- Aspose OCR NuGet 套件 (`Aspose.OCR`) – 透過 `dotnet add package Aspose.OCR` 安裝
- 一張同時有傾斜與噪點的範例影像（例如 `skewed_noisy.png`）
- 您偏好的 IDE 或編輯器（Visual Studio、VS Code、Rider… 隨您選）

> **專業提示：** 若沒有範例檔案，只要將清晰的螢幕截圖旋轉幾度，並使用影像編輯器加入一些「鹽與胡椒」噪點即可。管線的運作方式不會改變。

## 步驟 1：使用 Deskew Filter 校正影像傾斜

我們首先要校正旋轉角度。Aspose 提供的 `DeskewFilter` 能自動偵測至可設定的 `MaxAngle` 角度上限。將其設定為 **5°** 為大多數掃描文件提供安全的預設值。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image class

// Initialize the OCR engine – English is the most common language
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};

// Build the preprocessing pipeline
var preprocessPipeline = new PreprocessPipeline()
    .Add(new DeskewFilter { MaxAngle = 5 })          // This is where we answer “how to deskew image”
    .Add(new DespeckleFilter { Strength = 2 })      // Next we’ll remove image noise
    .Add(new ContrastFilter { Level = 1.5 });        // Finally we boost contrast for OCR
```

**為什麼這很重要：**  
如果文字傾斜，OCR 演算法可能會誤判字元——例如把「l」辨識成「i」。先進行 **校正**，即可為引擎提供一個直線的畫布。

## 步驟 2：使用 Despeckle 去除影像噪點

廉價手機或舊式掃描器的掃描結果常會出現類似隨機點狀的斑點，這些斑點會干擾字元辨識器。`DespeckleFilter` 能在保留邊緣的同時平滑影像。

```csharp
// The DespeckleFilter is already part of the pipeline (see Step 1)
// Strength = 2 is a balanced setting; increase for very noisy pics
```

若需要更積極地 **去除影像噪點**，可將 `Strength` 提升至 3 或 4——但要留意可能會損失細線條。

## 步驟 3：為 OCR 前處理影像 – 提升對比度

低對比度的掃描（白紙上淡灰色）可能導致 OCR 漏掉淡弱的字母。`ContrastFilter` 會擴展色調範圍，使暗像素更暗、亮像素更亮。

```csharp
// Contrast level of 1.5 is a good starting point.
// You can experiment with values between 1.0 (no change) and 2.0 (strong boost).
```

**邊緣情況：** 若原始影像已具高對比度，套用此濾鏡可能會洗掉細節。在此情況下，將 `Level` 設為 `1.0`（等同於停用）。

## 步驟 4：載入並清理來源影像

現在我們實際載入圖片，並將其送入剛才組合好的管線中。

```csharp
// Load the source image – replace the path with your own file location
var sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_noisy.png");

// Apply the entire preprocessing pipeline
var cleanedImage = preprocessPipeline.Apply(sourceImage);
```

> **注意：** `Apply` 方法會回傳一個新的 `Image` 物件；原始影像保持不變。若要除錯此流程，這讓您能輕鬆比較「前」與「後」的差異。

## 步驟 5：使用 Aspose OCR 辨識影像文字

手上已有一張校正、去噪且高對比度的圖片，我們最後將它交給 OCR 引擎。

```csharp
// Perform OCR on the cleaned image
var ocrResult = ocrEngine.Recognize(cleanedImage);

// Output the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**您應該會看到：** 主控台會印出原始掃描的文字內容，通常比直接輸入原始檔案時的誤辨率低很多。

## 步驟 6：驗證與提升 OCR 準確度

即使管線已相當完整，仍可能有部分字元辨識錯誤——特別是原始字型較為特殊時。以下提供幾個快速技巧以 **提升 OCR 準確度**：

| 問題 | 快速解決方案 |
|-------|-----------|
| 小標點遺失 | 在對比度步驟前加入 `BinaryThresholdFilter` |
| 混合語言（例如 English + Spanish） | 設定 `ocrEngine.Language = Language.English | Language.Spanish;` |
| 背景過暗 | 在校正前先反轉影像 (`new InvertFilter()`) |
| 大型文件 | 使用平行處理頁面 (`Parallel.ForEach`) 以加速 |

可嘗試調整濾鏡的順序；有時在低品質掃描上先套用 **對比度** 再 **去斑點** 會得到更佳效果。

## 完整可執行範例

以下是完整程式碼，您可以直接複製貼上到新的主控台專案中。它包含了我們討論的所有步驟，並加入了幾項安全檢查。

```csharp
// File: Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine (English language)
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // -------------------------------------------------
        // 2️⃣ Build preprocessing pipeline:
        //    Deskew → Despeckle → Contrast Boost
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
            .Add(new DeskewFilter { MaxAngle = 5 })          // how to deskew image
            .Add(new DespeckleFilter { Strength = 2 })      // remove image noise
            .Add(new ContrastFilter { Level = 1.5 });        // preprocess image for OCR

        // -------------------------------------------------
        // 3️⃣ Load the source image (adjust path as needed)
        // -------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/skewed_noisy.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ File not found: {imagePath}");
            return;
        }

        var sourceImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // 4️⃣ Apply the pipeline → cleaned image
        // -------------------------------------------------
        var cleanedImage = preprocessPipeline.Apply(sourceImage);

        // -------------------------------------------------
        // 5️⃣ Recognize text (this is the “recognize text from image” step)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(cleanedImage);

        // -------------------------------------------------
        // 6️⃣ Output the result
        // -------------------------------------------------
        Console.WriteLine("\n=== OCR Output ===\n");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**預期輸出**（假設範例影像包含 “Hello World!”）：

```
=== OCR Output ===

Hello World!
```

如果看到亂碼，請再次確認管線的順序，或提升 `DespeckleFilter.Strength`。

## 結論

我們已說明 **如何校正影像傾斜**、**去除影像噪點**、**為 OCR 前處理影像**，以及最終使用 Aspose OCR **辨識影像文字**——同時關注 **提升 OCR 準確度**。完整且可執行的範例展示了每個步驟的實際應用，您只要將它放入任何 .NET 專案，即可立即開始擷取文字。

準備好接受下一個挑戰了嗎？試著擴充管線以處理多頁 PDF，或為多語言文件測試語言套件。概念相同——只要更換 `Language` 旗標，或在頁面顛倒時加入 `RotateFilter` 即可。

有任何問題或遇到仍無法處理的影像嗎？在下方留言，我們會一起排除故障。祝開發愉快！

![如何校正影像傾斜範例](/images/deskew-example.png "使用 Aspose OCR 校正影像的示意圖")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}