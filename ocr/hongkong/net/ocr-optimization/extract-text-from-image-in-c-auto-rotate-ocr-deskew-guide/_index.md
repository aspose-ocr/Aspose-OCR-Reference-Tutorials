---
category: general
date: 2026-03-29
description: 使用 Aspose OCR 在 C# 中從圖像提取文字。學習自動旋轉 OCR 以及如何校正掃描圖像的傾斜，以獲得完美結果。
draft: false
keywords:
- extract text from image
- auto rotate ocr
- how to deskew scanned image
- Aspose OCR C#
- image preprocessing OCR
language: zh-hant
og_description: 使用 Aspose OCR 從圖像中提取文字。本指南展示自動旋轉 OCR 以及如何在 C# 中校正掃描圖像的傾斜。
og_title: 在 C# 中從圖像提取文字 – 自動旋轉 OCR 與去斜
tags:
- C#
- OCR
- Aspose
- Image Processing
title: 在 C# 中從圖像提取文字 – 自動旋轉 OCR 與去斜指南
url: /zh-hant/net/ocr-optimization/extract-text-from-image-in-c-auto-rotate-ocr-deskew-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字（C#） – 自動旋轉 OCR 與去斜指南

是否曾需要**從圖像中提取文字**，但檔案卻以奇怪的角度出現？這是常見的困擾——尤其在處理掃描發票、拍攝收據或歪斜的 PDF 時。好消息是，你不必自行編寫旋轉演算法。透過使用 Aspose OCR 內建的 *auto rotate OCR* 功能，你可以讓引擎自行校正圖片，然後在同一步驟中**從圖像中提取文字**。

在本教學中，我們將逐步說明一個完整、可直接執行的 C# 程式，該程式會：

* 初始化 OCR 引擎，啟用自動方向校正與去斜功能，
* 識別旋轉或傾斜的圖片，
* 回傳偵測到的旋轉角度以及提取出的文字。

不需要外部服務，也不需要繁雜的數學計算——只要幾行程式碼，並提供在需要時*如何去斜掃描圖像*的清晰說明。

## 需要的條件

| Prerequisite | Why it matters |
|--------------|----------------|
| .NET 6.0 or later (or .NET Framework 4.6+) | Aspose OCR 以 NuGet 套件形式提供，支援上述執行環境。 |
| Visual Studio 2022 (or any C# editor) | 方便加入 NuGet 套件並執行主控台應用程式。 |
| A sample image (`rotated_document.jpg`) | 檔案需為 JPEG、PNG、BMP 或 TIFF，且不是完全正立的。 |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | 提供 `OcrEngine`、`PreprocessingFilters` 以及相關型別。 |

如果已勾選以上項目，即可開始。否則，請從 NuGet 取得最新的 Aspose OCR——只需一次點擊安裝。

---

## 步驟 1 – 初始化 OCR 引擎（主要關鍵字實作）

我們首先建立一個 `OcrEngine` 實例，並告訴它 **auto rotate OCR** 與 **deskew** 任何輸入的圖片。這兩個旗標以位元 OR (`|`) 結合，因為 `PreprocessingFilters` 是具備 `[Flags]` 屬性的列舉型別。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine with English language and preprocessing options
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Enable both auto‑rotate and auto‑deskew
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };
```

> **為什麼重要：**  
> *Auto‑rotate OCR* 會檢查圖像的文字基線，推測正確的方向，並在辨識前於內部自動旋轉。*Auto‑deskew* 則針對掃描文件常見的輕微斜角執行相同處理。啟用兩者即可在不需手動編輯圖像的情況下，確保 **extract text from image** 的最佳結果。

---

## 步驟 2 – 識別圖像並取得結果

現在將檔案路徑交給引擎。`RecognizeImage` 方法會回傳一個 `OcrResult` 物件，內含偵測到的旋轉角度、信心分數以及純文字輸出。

```csharp
        // Recognise the image file and obtain the OCR result
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/rotated_document.jpg");
```

> **提示：** 若使用串流（例如上傳的檔案），請改用 `ocrEngine.RecognizeImage(Stream)`。前處理旗標仍然適用，仍可獲得 **auto rotate OCR** 的好處。

---

## 步驟 3 – 顯示旋轉角度與提取的文字

最後，我們在主控台印出兩項資訊：引擎認為圖片需要旋轉的角度，以及實際提取出的文字。

```csharp
        // Show the detected rotation and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**預期輸出**（數值會因輸入圖像而異）：

```
Detected rotation: 12.3°
----- Extracted Text -----
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

如果圖像本身已正立，旋轉角度會是 `0°`，且仍能得到乾淨的文字，這要歸功於 *auto‑deskew* 演算法。

---

## 步驟 4 – 了解如何去斜掃描圖像（次要關鍵字深入探討）

當 OCR 引擎回傳非零旋轉時，你可能會想知道 *how to deskew scanned image*。在底層，Aspose OCR 會使用 **Hough transform** 來偵測主要文字行的方向，然後以該角度的相反方向旋轉位圖，從而校正文字。

**何時重要？**  
* 掃描器以稍微傾斜的方式送紙（辦公環境常見）。  
* 手持手機拍攝的照片——水平線很少完美。

**邊緣案例處理：**  
若結果的 `RotationAngle` 異常大（例如 > 45°），引擎可能誤判圖像（可能是標誌或非文字圖形）。此時可：

1. 使用 `System.Drawing` 手動旋轉圖像後再交給引擎，或  
2. 停用 `AutoRotate`，僅保留 `AutoDeskew`，前提是文件已正立。

```csharp
// Example: manually rotate 90° clockwise before OCR
using (var img = Aspose.OCR.Image.Load("rotated_document.jpg"))
{
    img.Rotate(90);
    OcrResult result = ocrEngine.RecognizeImage(img);
    Console.WriteLine(result.Text);
}
```

---

## 步驟 5 – 常見陷阱與專業技巧（E‑E‑A‑T 實作）

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| **Blurry or low‑resolution images** | OCR 準確度會大幅下降，旋轉偵測可能失敗。 | 使用至少 300 dpi 的掃描；在 OCR 前套用銳化濾鏡。 |
| **Mixed languages** | 引擎預設為英文，外語字元會變成亂碼。 | 設定 `Language = Language.English | Language.Spanish`（或其他適當組合）。 |
| **Large files (> 10 MB)** | 記憶體壓力可能導致 `OutOfMemoryException`。 | 先縮小圖像，或使用 `OcrEngine.RecognizeRegion` 以區塊方式處理。 |
| **Incorrect file path** | `FileNotFoundException` 會中斷程式。 | 使用 `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")` 提升穩定性。 |

> **專業技巧：** 永遠記錄 `ocrResult.RotationAngle` 與 `ocrResult.Confidence`（若有提供）。這些指標可協助判斷是否需要以不同前處理設定重新嘗試。

---

## 步驟 6 – 擴充範例（接下來做什麼？）

現在你已能透過自動旋轉與去斜功能 **extract text from image**，可以考慮以下進階應用：

* **批次處理** – 迴圈遍歷資料夾內的圖像，將每筆結果寫入資料庫，並將 `RotationAngle > 5°` 的項目標記為需人工審核。  
* **PDF 轉換** – 使用 Aspose.PDF 將提取的文字與原始圖像合併，產生可搜尋的 PDF。  
* **語言偵測** – 使用 Aspose.OCR 的 `AutoDetectLanguage` 旗標，讓引擎自動選擇最佳語言。

這些皆建立在相同的核心原則上：讓函式庫處理方向校正，你只需專注於業務邏輯。

---

## 完整可執行範例（直接複製貼上）

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine with auto‑rotate and auto‑deskew
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };

        // 2️⃣ Recognise the image – replace the path with your own file
        string imagePath = "YOUR_DIRECTORY/rotated_document.jpg";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 3️⃣ Output the rotation angle and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

將檔案儲存為 `Program.cs`，執行 `dotnet add package Aspose.OCR`，再執行 `dotnet run`。你應該會在主控台看到旋轉角度與乾淨的文字。

---

## 結論

我們剛剛示範了如何在 C# 中 **extract text from image**，同時讓 Aspose OCR 處理 *auto rotate OCR* 與那個棘手的 *how to deskew scanned image* 問題。啟用這兩個前處理旗標後，引擎會自動校正歪斜的圖片、偵測正確方向，並輸出精確文字——不需要手動編輯圖像。

歡迎嘗試更大的批次、不同語言，甚至將輸出整合至可搜尋的 PDF。只要 OCR 引擎負責繁重的工作，你的文件流程就能升級到新高度。

**準備好提升文件處理效能了嗎？** 把程式碼抓下來，指向自己的掃描檔，觀察旋轉角度消失的過程。若有任何問題，歡迎在下方留言——祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}