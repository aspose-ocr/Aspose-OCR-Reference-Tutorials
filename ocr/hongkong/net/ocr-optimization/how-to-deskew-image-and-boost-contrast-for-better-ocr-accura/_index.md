---
category: general
date: 2025-12-30
description: 如何快速校正圖像傾斜，並學習在提取圖像文字時提升對比度，以提高 OCR 準確度。
draft: false
keywords:
- how to deskew image
- how to boost contrast
- extract text from image
- recognize text image
- improve ocr accuracy
language: zh-hant
og_description: 快速校正圖像傾斜，並學習在提取圖像文字時提升對比度，以提高 OCR 準確度。
og_title: 如何校正影像傾斜並提升對比度以提高 OCR 準確度
tags:
- OCR
- C#
- Image Processing
title: 如何校正圖像傾斜並提升對比度以提高 OCR 準確度
url: /zh-hant/net/ocr-optimization/how-to-deskew-image-and-boost-contrast-for-better-ocr-accura/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何校正圖像傾斜並提升對比度以提高 OCR 準確度

有沒有想過 **how to deskew image** 從掃描器或手機取得的圖檔？  
你並不孤單——大多數開發者在來源圖片稍微傾斜或雜訊較多時都會卡關，導致 OCR 輸出變成一團亂碼。  

好消息是，只要幾行 C# 程式碼，你就能把圖片校正、清理背景，甚至提升對比度，讓引擎像專業人士一樣讀取文字。本文亦會示範如何 **extract text from image** 檔案以及使用 Aspose.OCR 進行 **recognize text image** 內容，同時將 **improve OCR accuracy** 放在首位。

## 需要的環境

- **.NET 6.0** 或更新版本（此程式碼亦可在 .NET Framework 4.7+ 上編譯）  
- **Aspose.OCR** NuGet 套件（版本 23.12 或更新）— 透過 `dotnet add package Aspose.OCR` 安裝  
- 一張同時有旋轉與雜訊的範例圖（例如 `noisy_rotated.jpg`）  
- Visual Studio、VS Code，或任何你慣用的 IDE  

就這樣——不需要額外的原生函式庫，也不需要龐大的 OpenCV 綁定。純粹使用受管理的程式碼。

---

## 步驟 1：設定專案並匯入命名空間

首先，建立一個新的 console 應用程式，並將所需的命名空間引入作用域。此步驟是後續所有操作的基礎。

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later
        }
    }
}
```

**為何重要：**  
`Aspose.OCR` 提供 `OcrEngine` 類別，而 `Aspose.OCR.Filters` 則提供方便的前置處理過濾器，如 `DeskewFilter` 與 `ContrastBoostFilter`。提前匯入可讓程式碼保持整潔，並告訴編譯器我們的使用意圖。

---

## 步驟 2：初始化 OCR 引擎並加入 Deskew Filter

現在我們真正開始 **how to deskew image**。`DeskewFilter` 會自動偵測旋轉角度（上限由你設定），並將位圖旋轉回水平。

```csharp
// Inside Main()
var ocrEngine = new OcrEngine();

// Deskew: correct up to 15 degrees of rotation
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
```

**背後的運作原理是什麼？**  
過濾器會掃描圖像中最長的水平文字行，估算傾斜角度，並套用相反的旋轉。將 `MaxAngle` 限制在 15°，可避免對已經筆直的圖像過度校正。

> **專業提示：** 若來源圖像可能顛倒，將 `MaxAngle` 提升至 180°——過濾器仍會找出正確的方向。

---

## 步驟 3：使用 Denoise Filter 降低雜訊

雜訊掃描甚至會欺騙最聰明的 OCR 引擎。加入 `DenoiseFilter` 可平滑斑點，同時保留細節。

```csharp
// Denoise: strength ranges from 0 (off) to 1 (max)
ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });
```

**為何需要它：**  
雜訊會產生偽邊緣，讓 OCR 演算法誤判為字元。`0.7` 的強度對大多數掃描文件而言是最佳平衡；對於極乾淨或極髒的輸入，可自行調整。

---

## 步驟 4：提升對比度 – 「How to Boost Contrast」實作

這裡回應次要關鍵字 **how to boost contrast**。`ContrastBoostFilter` 會放大深色文字與亮色背景之間的差異，使字母更突出。

```csharp
// Contrast boost: level > 1 increases contrast
ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });
```

**背後的考量：**  
較高的對比度可降低細微筆畫被遺漏的機會。`1.3` 的等級對一般黑白文件效果良好；若是彩色相片，可能需要 `1.5` 或更高。

---

## 步驟 5：執行 OCR 並擷取文字

經過圖像前置處理後，我們最終使用 `Recognize` 方法 **extract text from image**。此方法會回傳包含原始字串與信心分數的 `OcrResult` 物件。

```csharp
// Perform OCR on the prepared image
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/noisy_rotated.jpg");

// Output the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**你會得到什麼：**  
`ocrResult.Text` 包含引擎能讀取的純文字表示。若需要字級別的信心度，可檢視 `ocrResult.Regions`——每個區域都有 `Confidence` 屬性。

---

## 完整範例（可直接複製貼上）

以下是完整程式碼，可直接貼入 `Program.cs`。請確保圖像路徑指向您機器上的實際檔案。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Deskew – correct up to 15° rotation
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

            // 3️⃣ Denoise – smooth out speckles (strength 0.7)
            ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });

            // 4️⃣ Contrast boost – make text pop (level 1.3)
            ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });

            // 5️⃣ Recognize the image
            var imagePath = @"YOUR_DIRECTORY\noisy_rotated.jpg";
            var ocrResult = ocrEngine.Recognize(imagePath);

            // 6️⃣ Show the result
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**預期輸出（範例）：**

```
=== OCR Output ===
Invoice #12345
Date: 2024-09-30
Total Amount: $1,250.00
Thank you for your business!
```

如果結果看起來亂碼，請再次檢查圖像品質、調整 `Strength` 或 `Level`，或提升 `MaxAngle` 以加強校正力度。

---

## 常見問題與邊緣案例

### 如果圖像是顛倒的？

在 `DeskewFilter` 中設定 `MaxAngle = 180`。過濾器會偵測到 180° 旋轉並正確翻轉。

### 我的文件是彩色的（例如帶有藍色標記的掃描表單）。

可嘗試在提升對比度前加入 `ColorFilter`，或手動將圖像轉為灰階：

```csharp
ocrEngine.Filters.Add(new GrayscaleFilter());
```

### 我需要批次處理大量檔案。

將 OCR 邏輯包在遍歷目錄的 `foreach` 迴圈中：

```csharp
foreach (var file in Directory.GetFiles(@"C:\Scans", "*.jpg"))
{
    var result = ocrEngine.Recognize(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

### 我要如何得知 OCR 的信心度？

檢視 `ocrResult.Regions`：

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"Text: {region.Text} – Confidence: {region.Confidence:P2}");
}
```

較高的信心值（接近 100%）通常代表前置處理步驟成功。

---

## 提升 OCR 準確度的技巧

| 小技巧 | 為何有助 |
|-----|--------------|
| **使用無損影像格式**（PNG、TIFF） | JPEG 壓縮會模糊邊緣，降低辨識率。 |
| **保持 DPI 在 300 以上** | 每個字元的像素越多，引擎可利用的資訊越豐富。 |
| **裁切掉不相關的邊緣** | 減少雜訊並加快處理速度。 |
| **在提升對比度後套用二值化閾值**（黑白）於純文字文件 | 將影像簡化為兩色，大多數 OCR 引擎都偏好此格式。 |
| **先以小樣本測試** | 讓你在大規模執行前微調 `Strength` 與 `Level`。 |

---

## 結論

我們已說明 **how to deskew image** 檔案、**how to boost contrast**，以及使用 Aspose.OCR 完整的 **extract text from image** 流程。於呼叫 `Recognize` 前串接 `DeskewFilter`、`DenoiseFilter` 與 `ContrastBoostFilter`，即可在大多數實務掃描中明顯提升 **improve OCR accuracy**。

執行程式碼、微調過濾器參數以符合你的文件特性，你將能快速從最雜亂的照片中擷取乾淨文字。想更進一步？可加入語言特定的字典，或將輸出送入拼寫檢查器進行後處理。

祝開發順利，願你的 OCR 結果永遠清晰如水晶！

--- 

![how to deskew image example](deskew_example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}