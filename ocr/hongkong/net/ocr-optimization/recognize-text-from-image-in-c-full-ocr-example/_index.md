---
category: general
date: 2026-06-22
description: 使用 Aspose OCR 於 C# 進行圖像文字辨識。了解如何自動去斜圖像、為 OCR 預處理圖像，以及在簡潔的 C# OCR 範例中啟用自動去斜功能。
draft: false
keywords:
- recognize text from image
- auto deskew image
- preprocess image for ocr
- c# ocr example
- enable auto deskew
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中辨識圖像文字。本指南說明如何自動校正圖像傾斜、為 OCR 前置處理圖像，以及在實用的 C#
  OCR 範例中啟用自動校正。
og_title: 在 C# 中從圖像辨識文字 – 完整 OCR 範例
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  headline: Recognize Text from Image in C# – Full OCR Example
  type: TechArticle
- description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  name: Recognize Text from Image in C# – Full OCR Example
  steps:
  - name: 1. Low Contrast or Dark Backgrounds
    text: 'Aspose.OCR offers an extra flag `PreprocessingOptions.ContrastEnhancement`.
      Add it to the `Preprocessing` line:'
  - name: 2. Non‑English Documents
    text: Swap `OcrLanguage.English` for `OcrLanguage.Spanish`, `OcrLanguage.French`,
      etc. The engine auto‑loads the appropriate language model.
  - name: 3. Large Images
    text: 'Processing a 5 MP photo can be memory‑hungry. Scale it down first:'
  - name: 4. Getting Bounding Boxes
    text: 'If you need the exact location of each word (e.g., for a UI overlay), iterate
      over `result.Regions`:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 在 C# 中從圖片辨識文字 – 完整 OCR 範例
url: /zh-hant/net/ocr-optimization/recognize-text-from-image-in-c-full-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像辨識文字（C#）– 完整 OCR 範例

有沒有想過如何在 C# 應用程式中 **從圖像辨識文字**，而不必因模糊的掃描而抓狂？你並不孤單。無論是數位化收據、從表單提取資料，或只是玩 AI 驅動的圖像技巧，取得乾淨的 OCR 結果關鍵在於適當的前處理——例如自動校正圖像傾斜與降噪。

在本教學中，我們將逐步說明一個使用 Aspose.OCR 函式庫的 **c# ocr 範例**，它能 **啟用自動校正**，自動將傾斜的照片校正為水平，並 **為 OCR 前處理圖像**，只需幾行程式碼。完成後，你將擁有一個可執行的程式，直接在主控台印出辨識出的文字。

## 你將學到什麼

- 如何安裝與參考 Aspose.OCR NuGet 套件。  
- 設定具備英文語言支援的 `OcrEngine`。  
- 在單一步驟中啟用 **auto deskew image** 與其他前處理選項。  
- 對真實情境的照片執行引擎並處理輸出。  
- 處理邊緣情況的技巧，例如高度旋轉的圖像或低對比度掃描。

> **先決條件** – 需要 .NET 6（或更新版本）以及對 C# 的基本了解。無需先前的 OCR 經驗。

---

## ## 從圖像辨識文字 – 安裝 Aspose.OCR 套件

在撰寫任何程式碼之前，必須先將函式庫加入專案。於解決方案資料夾中開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

此指令會下載最新的穩定版 Aspose.OCR，內含 OCR 引擎、語言套件以及我們所需的前處理工具。

*小技巧：* 若目標是 .NET Framework 而非 .NET Core，請使用 Visual Studio NuGet 套件管理員 UI——搜尋 “Aspose.OCR” 並點選 **Install**。

## ## 從圖像辨識文字 – 初始化 OCR 引擎

套件安裝完成後，我們即可建立引擎。第一步是告訴引擎預期使用哪種語言。大多數情況下英文已足夠，但此函式庫內建支援數十種語言。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine and set the language to English
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,

            // Step 2: Enable preprocessing to automatically deskew and denoise the image
            Preprocessing = PreprocessingOptions.AutoDeskew | PreprocessingOptions.Denoise
        };
```

**為什麼這很重要：**  
- `Language = OcrLanguage.English` 告訴引擎使用哪套字元集，能大幅提升準確度。  
- `Preprocessing` 屬性結合了兩個旗標——`AutoDeskew` 與 `Denoise`。此 **auto deskew image** 步驟會將圖片旋轉回水平基線，而 `Denoise` 則移除顆粒雜訊，避免干擾 OCR 引擎。  

如果省略前處理，掃描收據或斜拍的照片常會得到雜亂的輸出。

## ## 從圖像辨識文字 – 將圖像提供給引擎

引擎已就緒後，接下來要將圖像檔案交給它。Aspose.OCR 接受路徑或 `Stream`，因此你可以使用本機檔案、內嵌資源，甚至是從網路下載的圖像。

```csharp
        // Step 3: Recognize text from the input image
        var result = engine.RecognizeImage(@"YOUR_DIRECTORY/skewed_photo.jpg");
```

**邊緣情況說明：**  
- 若圖像 **高度旋轉**（> 45°），`AutoDeskew` 仍會盡力校正，但你可能需要先使用 `System.Drawing` 或 `ImageSharp` 手動旋轉後再傳給引擎。  
- 若是 **多頁 PDF**，請改用 `engine.RecognizePdf`；相同的前處理旗標仍然適用。

## ## 從圖像辨識文字 – 輸出結果

最後，我們顯示擷取出的文字。`result` 物件不只包含純文字，還提供信心分數、邊界框以及帶有高亮區域的原始圖像。簡易示範只需印出 `result.Text` 即可。

```csharp
        // Step 4: Output the recognized text to the console
        System.Console.WriteLine(result.Text);
    }
}
```

執行程式時，應會看到類似以下的輸出：

```
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!
```

如果輸出看起來雜亂，請再次確認來源圖像清晰、光線充足，且 **preprocess image for OCR** 確實已啟用（上述的 `Preprocessing` 旗標）。

## ## 從圖像辨識文字 – 處理常見陷阱

### 1. 低對比或深色背景
Aspose.OCR 提供額外的旗標 `PreprocessingOptions.ContrastEnhancement`。將其加入 `Preprocessing` 行中：

```csharp
Preprocessing = PreprocessingOptions.AutoDeskew |
                PreprocessingOptions.Denoise |
                PreprocessingOptions.ContrastEnhancement
```

### 2. 非英文文件
將 `OcrLanguage.English` 換成 `OcrLanguage.Spanish`、`OcrLanguage.French` 等。引擎會自動載入相應的語言模型。

### 3. 大尺寸圖像
處理 5 MP 的照片可能會佔用大量記憶體。請先將其縮小：

```csharp
engine.Image = ImageProcessor.Resize(@"YOUR_DIRECTORY/skewed_photo.jpg", 1024, 768);
```

### 4. 取得邊界框
若需要每個單詞的精確位置（例如在 UI 上疊加），可遍歷 `result.Regions`：

```csharp
foreach (var region in result.Regions)
{
    System.Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

## ## 從圖像辨識文字 – 完整可執行範例

以下是 **完整、可直接複製貼上的** 程式碼，已整合上述所有技巧。將其存為 `Program.cs`，將 `YOUR_DIRECTORY` 替換為放置測試圖像的資料夾路徑，然後執行 `dotnet run`。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,
            // Enable auto deskew, denoise, and contrast enhancement
            Preprocessing = PreprocessingOptions.AutoDeskew |
                            PreprocessingOptions.Denoise |
                            PreprocessingOptions.ContrastEnhancement
        };

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/skewed_photo.jpg";

        // Recognize the image
        var result = engine.RecognizeImage(imagePath);

        // Output plain text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // Optional: print bounding boxes for each detected region
        Console.WriteLine("=== Detected Regions ===");
        foreach (var region in result.Regions)
        {
            Console.WriteLine($"{region.Text}  -->  {region.Bounds}");
        }
    }
}
```

**預期的主控台輸出**（假設圖像是一張簡單的收據）：

```
=== Recognized Text ===
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!

=== Detected Regions ===
Invoice #12345  -->  {X=12,Y=34,Width=250,Height=20}
Date: 2026-06-01  -->  {X=12,Y=60,Width=200,Height=18}
Total: $256.78  -->  {X=12,Y=86,Width=180,Height=18}
Thank you for your business!  -->  {X=12,Y=112,Width=300,Height=22}
```

如果看到文字乾淨地印出，恭喜你——已成功 **recognize text from image**，並具備自動校正與前處理功能！

## ## 從圖像辨識文字 – 後續步驟與相關主題

- **批次處理：** 在 `foreach` 迴圈中包裹引擎呼叫，以一次處理數十張照片。  
- **PDF 轉換：** 使用 `engine.RecognizePdf` 處理多頁文件，然後合併結果。  
- **自訂字典：** 將詞彙清單提供給 `engine.CustomWords`，提升領域特定術語（例如醫療代碼）的辨識精度。  
- **效能調校：** 若大量處理圖像，請快取 `OcrEngine` 實例；建立引擎是最耗時的步驟。  

這些延伸功能自然仍使用相同概念——**preprocess image for OCR**、**enable auto deskew**、以及 **recognize text from image**——因此你可以重複使用剛學到的程式碼模式。

## 結論

我們剛剛示範了一個 **c# ocr 範例**，說明如何使用 Aspose.OCR **recognize text from image**，同時自動校正與降噪。啟用 `AutoDeskew`（即 **auto deskew image** 功能）並加入少數前處理旗標，即可大幅提升 OCR 的可靠性，且不需自行撰寫任何圖像處理程式碼。

現在你可以拿這個骨架程式，套入自己的圖像，開始為發票、身分證或任何紙本文件抽取資料。遇到難處理的掃描？試試我們提到的額外前處理選項，或實驗自訂語言套件。沒有極限。

如果本指南幫助你解決問題，歡迎留下評論、分享成果，或在 GitHub 上私訊我——祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在所示技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [如何使用 AspOCR：為 .NET 前處理圖像 OCR 濾鏡](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [從圖像提取文字 – 使用 Aspose.OCR 於 .NET 的 OCR 最佳化](/ocr/english/net/ocr-optimization/)
- [如何使用 Aspose.OCR for .NET 提取圖像文字](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}