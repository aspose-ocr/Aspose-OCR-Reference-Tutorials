---
category: general
date: 2026-03-04
description: 學習如何校正圖像傾斜，並透過調整對比度來辨識圖像中的文字，以提升 OCR 準確度並增強圖像的 OCR 效果。
draft: false
keywords:
- how to deskew image
- recognize text from image
- how to apply contrast
- improve OCR accuracy
- enhance image for OCR
language: zh-hant
og_description: 如何校正圖像傾斜並提升 OCR 效果。學習調整對比度、提高 OCR 準確率，並使用可重複使用的流程管線從圖像中辨識文字。
og_title: 如何校正影像傾斜 – 完整 C# OCR 教程
tags:
- OCR
- C#
- image‑processing
title: 如何為 OCR 去除圖像傾斜 – C# 逐步指南
url: /zh-hant/net/ocr-optimization/how-to-deskew-image-for-ocr-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何校正影像傾斜 – 完整 C# OCR 教學

有沒有想過 **how to deskew image**，讓你的 OCR 引擎真的能讀出文字？你並不是唯一有這個疑問的人。在許多實務專案中——掃描的收據、拍攝的合約，或是手機相機拍出的模糊收據——圖片往往不是完全正立的。頁面傾斜會干擾字元辨識器，最終只會得到一堆亂碼。

好消息是？只要先校正影像 **and** 再調整對比度，就能顯著 **improve OCR accuracy**。本教學將一步步示範完整的 C# 範例，說明在套用校正濾鏡與對比度提升後，如何 **recognize text from image**。我們也會說明 **how to apply contrast** 的正確方式、討論邊緣情況，並提供一個可重複使用的管線，讓你可以直接套用到任何專案中。

## 本指南你將學到什麼

- 為何校正影像與調整對比度對 OCR 如此重要的清晰說明。  
- 一個可直接執行的 C# 程式碼範例，建立濾鏡管線、將其附加至 OCR 引擎，並讀取多張圖片。  
- 如何在多個檔案間重複使用同一管線、處理失敗情況，以及測量準確度提升的技巧。  
- 相關主題的連結，例如影像二值化、雜訊移除與多語言 OCR（全部在同一頁面內完成）。

**Prerequisites** – 需要 .NET 6+ 環境、支援濾鏡管線的 OCR 函式庫（例如 Tesseract‑.NET、IronOCR，或任何商業 SDK），以及幾張範例 PNG。無需外部服務。

---

## Step 1 – 為何校正影像是第一件該做的事

當掃描的頁面即使只旋轉幾度，OCR 引擎看到的每行基線也會呈角度。大多數辨識器假設文字是水平的；任何偏差都會降低信心分數，並產生替換錯誤。

> **Pro tip:** 若有條件，請使用平坦的表面與良好的光線拍攝影像；軟體修正無法完全取代良好的原始資料。

在程式碼層面上，「how to deskew image」通常指偵測主要文字行的方向，並將位圖旋轉回 0°。大多數 OCR SDK 都提供 `DeskewFilter`，可自動完成此動作。

```csharp
// Create a deskew filter – it analyses the image and rotates it back.
var deskew = new DeskewFilter();
```

此濾鏡的前提是假設頁面上文字比背景多，這在大多數文件中皆成立。若你的照片中有大量留白，可能需要備援演算法——但對於大多數掃描的 PDF，預設設定已足夠。

---

## Step 2 – 提升對比度讓字元更突出

對比度是最暗與最亮像素之間的差異。低對比度的掃描看起來像是被洗掉，OCR 引擎無法分辨字元的起始與結束。透過提升對比度，我們「銳化」了視覺上的分離，從而 **improve OCR accuracy**。

```csharp
// Set the contrast level – 1.0 is neutral, >1.0 brightens the darks and whites.
var contrast = new ContrastFilter { Level = 1.2 };
```

為什麼是 1.2？實務上，適度提升（10‑30 %）已足夠。若提升過度，會失去細微的細節，尤其是細體字。歡迎自行實驗；稍後建立的管線允許你在不重新編譯整個應用程式的情況下調整此參數。

---

## Step 3 – 建立可重複使用的濾鏡管線

現在把兩個濾鏡合併成單一管線。這樣你每次都會 **recognize text from image**，使用完全相同的前處理，確保結果一致。

```csharp
using YourOcrLibrary;          // Replace with the actual namespace of your OCR SDK
using YourOcrLibrary.Filters; // Namespace where DeskewFilter & ContrastFilter live

// Step 3: Build a filter pipeline that deskews the image and enhances contrast
var filterPipeline = new FilterBuilder()
    .Add(new DeskewFilter())                 // First: straighten the page
    .Add(new ContrastFilter { Level = 1.2 }) // Then: make the text pop
    .Build();
```

**Why a pipeline?**  
- **Modularity:** 可在不觸及 OCR 呼叫的情況下新增或移除濾鏡。  
- **Performance:** 函式庫可以批次處理操作，減少記憶體抖動。  
- **Reusability:** 同一管線可附加至多個 `engine.Recognize` 呼叫。

---

## Step 4 – 把管線附加到 OCR 引擎

大多數 OCR 引擎提供 `Filters` 屬性或 `SetFilters` 方法。只要在此處指派我們的管線，之後的每張影像都會先經過校正 + 對比度的前處理，才開始真正的字元分析。

```csharp
// Step 4: Attach the pipeline to the OCR engine so it processes images using these filters
var engine = new OcrEngine(); // Instantiate your OCR engine (configure language, etc.)
engine.Filters = filterPipeline;
```

如果需要變更語言模型（例如 English → Spanish），可以在附加濾鏡之前完成；前處理階段的順序並不影響語言設定。

---

## Step 5 – 從第一張影像辨識文字

讓管線上線運作。我們載入 PNG、執行 OCR，並印出結果。注意我們使用同一個 `engine` 實例——不需要每次都重建濾鏡。

```csharp
// Step 5: Recognize text from the first image using the configured engine
var firstImagePath = @"C:\Images\doc1.png";
var firstResult = engine.Recognize(ImageInfo.Load(firstImagePath));

Console.WriteLine("=== First Document ===");
Console.WriteLine(firstResult.Text);
```

**What you should see:** 乾淨、正確方向的文字，遠比未經處理的掃描圖來得少很多亂碼。若仍有錯誤，可考慮在對比度步驟之後加入 `BinarizeFilter`（轉為純黑白）。

---

## Step 6 – 在其他檔案上重複使用同一管線

濾鏡管線最大的優勢之一，就是可以在數十個檔案間重複使用，且不會產生額外負擔。

```csharp
// Step 6: Recognize text from a second image to demonstrate reuse of the same pipeline
var secondImagePath = @"C:\Images\doc2.png";
var secondResult = engine.Recognize(ImageInfo.Load(secondImagePath));

Console.WriteLine("\n=== Second Document ===");
Console.WriteLine(secondResult.Text);
```

如果你有一個資料夾裡放滿了掃描的 PDF，只要對 `Directory.GetFiles(...)` 迴圈呼叫 `engine.Recognize` 即可。校正與對比度步驟保持一致，這正是 **enhance image for OCR** 在批次工作中的關鍵。

---

## Full Working Example – 完整範例整合

以下是完整、可自行執行的程式。直接複製貼上到新的 Console 專案，加入對應的 NuGet 套件（你的 OCR SDK），然後執行。程式會輸出兩張範例圖片的辨識文字。

```csharp
// ------------------------------------------------------------
// Complete C# OCR Example – Deskew + Contrast Pipeline
// ------------------------------------------------------------
using System;
using System.IO;
using YourOcrLibrary;          // e.g., IronOcr, Tesseract.NET, etc.
using YourOcrLibrary.Filters; // Filters live here

class Program
{
    static void Main()
    {
        // 1️⃣ Build the filter pipeline (deskew + contrast)
        var filterPipeline = new FilterBuilder()
            .Add(new DeskewFilter())                 // Straighten the page
            .Add(new ContrastFilter { Level = 1.2 }) // Boost contrast a bit
            .Build();

        // 2️⃣ Create and configure the OCR engine
        var engine = new OcrEngine
        {
            // Example: set language to English (adjust as needed)
            Language = OcrLanguage.English,
            Filters = filterPipeline
        };

        // 3️⃣ Define image paths (replace with your own)
        string[] imagePaths = {
            @"C:\Images\doc1.png",
            @"C:\Images\doc2.png"
        };

        // 4️⃣ Process each image
        foreach (var path in imagePaths)
        {
            if (!File.Exists(path))
            {
                Console.WriteLine($"⚠️ File not found: {path}");
                continue;
            }

            var result = engine.Recognize(ImageInfo.Load(path));

            Console.WriteLine($"\n=== {Path.GetFileName(path)} ===");
            Console.WriteLine(result.Text);
        }

        Console.WriteLine("\n✅ All done – you have successfully deskewed and enhanced contrast for OCR!");
    }
}
```

### Expected Output

```
=== doc1.png ===
Invoice #12345
Date: 2024‑02‑15
Total: $1,250.00
...

=== doc2.png ===
Meeting Minutes
1. Project kickoff...
2. Budget approval...
...
```

如果將此輸出與 **without** 濾鏡管線的執行結果比較，你會發現缺字、錯位的數字，或是整行亂碼的情況大幅減少。這正是正確掌握 **how to deskew image** 與 **how to apply contrast** 所帶來的可量化影響。

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *如果影像已經是正立的呢？* | `DeskewFilter` 會偵測到 0° 旋轉，直接回傳原始位圖，幾乎不會產生額外負擔。 |
| *可以用在 PDF 上嗎？* | 可以。大多數 OCR SDK 都允許你將 PDF 頁面載入為 `ImageInfo`。同一管線仍然適用，因為底層位圖的處理方式相同。 |
| *我的文件有彩色文字——對比度會破壞顏色嗎？* | 對比度濾鏡作用於亮度，顏色會被保留但變得更易辨識。若需要純黑白，請在對比度步驟之後加入 `BinarizeFilter`。 |
| *如何測量準確度提升？* | 在測試集上分別執行管線前後的 OCR，計算字元錯誤率 (CER) 或詞彙錯誤率 (WER)。通常會看到 10‑30 % 的錯誤下降。 |
| *會不會影響效能？* | 校正會增加少量 CPU 開銷（通常 < 100 ms/頁），對比度則是簡單的像素運算，整體影響相較於 OCR 本身可忽略不計。 |

---

## Next Steps – 讓你的 OCR 更上一層樓

現在你已經了解 **how to deskew image**、**how to apply contrast**，以及如何使用可重複使用的管線 **recognize text from image**，不妨進一步探索以下相關主題：

- **Noise reduction** – 在校正之前加入 `MedianFilter`，清除雜點。  
- **Binarization** – 轉為純黑白，對於結構複雜的語系特別有效。  
- **Multi‑page processing** – 迴圈處理 PDF 頁面，並將結果存入可搜尋的索引。  
- **Language models** – 隨時在 `OcrLanguage.English` 與 `OcrLanguage.French` 之間切換。  
- **Post‑processing** – 使用拼字檢查或正規表達式修正常見的 OCR 錯讀（例如 “0” 與 “O” 的混淆）。

以上每項都可以直接插入同一個 `FilterBuilder` 鏈中，讓你在任何生產環境中都有一個模組化、易於維護的解決方案，**enhances image for OCR**。

---

## Conclusion

我們已完整說明 **how to deskew image** 在 OCR 中的重要性、為何調整對比度是一個既便宜又強大的 **improve OCR accuracy** 手段，以及如何使用乾淨、可重複使用的方式 **recognize text from image**。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}