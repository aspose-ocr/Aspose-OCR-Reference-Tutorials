---
category: general
date: 2026-03-07
description: 了解如何使用 Aspose OCR 校正影像傾斜、增強對比度，並從掃描檔中擷取文字。提供完整的 C# 範例，輕鬆載入影像並執行 OCR。
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: zh-hant
og_description: 學習如何使用 Aspose OCR 於 C# 進行圖像去斜、提升對比度，並從掃描檔提取文字。提供逐步程式碼執行影像 OCR。
og_title: 如何在 C# 中校正影像傾斜並執行 OCR – 完整指南
tags:
- C#
- OCR
- Image Processing
title: 如何校正影像傾斜並在 C# 中執行 OCR – 完整指南
url: /zh-hant/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何校正影像傾斜並在 C# 中執行 OCR – 完整指南

如果你曾經想過在執行 OCR 前 **如何校正影像傾斜**，你來對地方了。在本教學中，我們將帶你一步步提升對比度、載入影像以供 OCR，最後使用 Aspose OCR **從掃描中擷取文字**。  

無論你是要數位化舊收據、清理掃描的合約，或只是需要一個可靠的方法從斜斜的相片讀取文字，以下步驟涵蓋你所需的一切。沒有多餘說明——只提供一個可直接複製貼上至 Visual Studio 的可執行範例。  

## 你將達成的目標

* 校正至多 30° 的傾斜（這就是 **如何校正影像傾斜** 的部分）。  
* 提升影像對比度，使字元邊緣更銳利（**如何提升對比度**）。  
* 將你的圖片載入 OCR 引擎（**載入影像以供 OCR**）。  
* 執行辨識程序並 **從掃描中擷取文字**。  

以上全部皆可使用最新的 Aspose.OCR .NET NuGet 套件（撰寫時為 v23.11）運作。  

---

![校正影像傾斜範例](/images/deskew-example.png "如何校正影像傾斜")

*上圖顯示了掃描文件在校正前後的樣子。*

## 前置條件

* .NET 6.0 或更新版本（程式碼亦可在 .NET Framework 4.7+ 上執行）。  
* Visual Studio 2022（或任何你喜歡的 C# IDE）。  
* Aspose.OCR NuGet 套件 – 透過 `dotnet add package Aspose.OCR` 安裝。  

就這樣。無需外部服務，亦不需要 API 金鑰。

---

## 使用 Aspose OCR 校正影像傾斜

我們首先建立一個 **ImageProcessingPipeline**，並加入 `DeskewFilter`。此過濾器會自動偵測主要文字行的角度，並將影像旋轉回水平。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**為什麼這很重要：**  
傾斜的掃描會讓 OCR 引擎困惑，因為字元不再與基線對齊。`DeskewFilter` 會分析影像直方圖，找出角度並旋轉影像，顯著提升辨識準確度。

> **專業提示：** 若你知道文件的傾斜角度永不超過 15°，可將 `MaxAngle = 15` 設定，以加快處理速度。

---

## 提升對比度以獲得更佳辨識效果

校正完畢後，下一步是讓文字更突出。`ContrastBoostFilter` 會拉伸像素強度範圍，對於褪色的印刷特別有幫助。

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**為什麼這有幫助：**  
低對比度的掃描會產生灰色的字元，二值化器可能會將其誤判為背景。提升對比度會使暗像素更暗、亮像素更亮，為後續的 `BinarizationFilter` 提供更乾淨的畫布。

---

## 在影像上執行 OCR – 載入檔案

現在影像已完成前置處理，我們需要 **載入影像以供 OCR**。Aspose 提供便利的 `ImageStream.FromFile` 輔助方法。

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

如果你的影像位於串流中（例如透過 Web API 上傳），也可以改用 `ImageStream.FromStream(yourStream)`。引擎支援 BMP、JPEG、PNG、TIFF 等多種格式。

---

## 執行辨識程序並從掃描中擷取文字

所有設定完成後，呼叫 `Recognize()` 即可執行繁重的工作。呼叫結束後，可透過 `ocrEngine.Text` 取得辨識後的文字。

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**預期輸出**（簡易發票範例）：

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

如果輸出看起來亂碼，請再次確認管線順序——先校正傾斜，接著去噪、提升對比度，最後二值化。調換順序可能會降低結果品質。

---

## 常見陷阱與邊緣案例

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **結果為空** | 影像過暗或過亮，導致預設二值化方法無法正常運作。 | 提升 `ContrastBoostFilter.Strength` 或改用 `BinarizationMethod.Otsu`。 |
| **部分文字缺失** | 去噪後仍有雜訊殘留。 | 對較輕微的影像使用 `DenoiseLevel.Medium`，或加入第二個 `DenoiseFilter`。 |
| **旋轉方向錯誤** | 文件的方向混雜（例如拍攝了已旋轉頁面的照片）。 | 手動將 `DeskewFilter.MaxAngle` 設為較低值，並使用 `ImageProcessor.Rotate` 先行旋轉影像。 |
| **效能下降** | 大量高解析度影像的批次處理。 | 在管線前先縮小影像 (`ImageProcessor.Resize`)，或使用平行處理 (`Parallel.ForEach`)。 |

---

## 完整可執行範例（即貼即用）

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

將此存為 `Program.cs`，執行 `dotnet run`，即可在主控台看到 **從掃描中擷取文字** 的結果。  

---

## 後續步驟與相關主題

* **批次處理** – 將上述邏輯包在迴圈中，以處理數十個檔案。  
* **自訂語言套件** – 若需讀取非拉丁文字，可透過 `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;` 載入語言模型。  
* **PDF 輸出** – 結合 Aspose.PDF 與 OCR，將可搜尋文字直接嵌入 PDF 檔案。  
* **效能調校** – 嘗試調整 `ImageProcessingPipeline` 的順序；在噪點較多的照片中，先去噪再校正傾斜有時能更快得到結果。  

所有這些皆建立在我們先前討論的核心概念之上：**如何校正影像傾斜**、**如何提升對比度**、**載入影像以供 OCR**、**在影像上執行 OCR**，以及最後的 **從掃描中擷取文字**。

---

## 結語

我們剛剛示範了一套完整、可投入生產環境的 **如何校正影像傾斜** 並在 C# 中執行 OCR 的方法。透過串接校正過濾器、去噪步驟、對比度提升與二值化，你即可得到乾淨的輸入，讓 Aspose OCR 能可靠地 **從掃描中擷取文字**。  

試著執行這段程式碼，依你的文件調整過濾器參數，你會看到辨識準確度迅速提升。有任何問題，歡迎留言，祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}