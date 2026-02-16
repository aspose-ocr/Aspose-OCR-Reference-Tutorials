---
category: general
date: 2026-02-16
description: 學習如何在 C# 中使用 Aspose.OCR 進行 OCR——從相片辨識文字、從掃描件讀取文字，並以高準確度從收據中提取文字。
draft: false
keywords:
- how to perform OCR
- recognize text from photo
- read text from scan
- extract text from receipt
- improve OCR accuracy
language: zh-hant
og_description: 學習如何在 C# 中使用 Aspose.OCR 執行 OCR。此指南將向您展示如何從照片中辨識文字、從掃描件中讀取文字，以及從收據中提取文字。
og_title: 如何在 C# 中執行 OCR – 完整 Aspose 指南
tags:
- C#
- Aspose.OCR
- Image Processing
title: 如何在 C# 中執行 OCR – 完整 Aspose 指南
url: /zh-hant/net/text-recognition/how-to-perform-ocr-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 完整 Aspose 指南

有沒有想過 **如何在模糊的收據**或手機隨手拍的照片上 **執行 OCR**？你並不是唯一有此需求的人。在許多實際應用中，我們需要 **recognize text from photo** 檔案、**read text from scan** 文件，或 **extract text from receipt** 圖片，而不必將資料傳送至雲端服務。  

在本教學中，我們將逐步說明一個完整的範例，展示如何使用 Aspose.OCR **how to perform OCR**，同時穿插提升 **improve OCR accuracy** 的技巧。完成後，你將擁有一個可直接執行的 C# 主控台程式，能從任何指向的圖像中擷取純文字。

> **你需要的條件**  
> * .NET 6 SDK（或任何較新的 .NET 版本）  
> * Aspose.OCR NuGet 套件（`Install-Package Aspose.OCR`）  
> * 範例圖片 – 例如名為 `photo_receipt.jpg` 的收據照片  

![how to perform OCR example](image.png){alt="如何執行 OCR 範例"}

## 使用 Aspose.OCR 在 C# 中執行 OCR 的方法

第一步是設定 OCR 引擎並載入英文語言模型。這是 **how to perform OCR** 的核心，若未載入語言模型，引擎將無法辨識要尋找的字元。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the English language model – change this if you need another language
ocrEngine.LoadLanguage(LanguageModel.English);
```

*為什麼這很重要*：載入正確的語言模型會直接影響辨識速度與準確度。英文是最常見的情況，但 Aspose 也提供數十種其他語言模型，若你需要在法文、德文等 **read text from scan** 文件中使用時，可加以利用。

## 從照片辨識文字

手機拍攝的照片常會出現旋轉、雜訊或低對比度等問題。在請求引擎 **recognize text from photo** 之前，我們先設定一些前置處理選項，以清理圖像。

```csharp
// Configure preprocessing to boost OCR results
PreprocessingOptions preprocessingOptions = new PreprocessingOptions
{
    Deskew = true,                     // Auto‑correct rotation (helps with tilted receipts)
    Denoise = DenoiseLevel.Medium,    // Reduce graininess
    Binarize = BinarizeMethod.Otsu,   // Convert to black‑and‑white for sharper edges
    ContrastEnhancement = true        // Boost contrast for faint characters
};

// Apply the preprocessing configuration
ocrEngine.Preprocessing = preprocessingOptions;
```

*小技巧*：如果發現缺字，試著將 `DenoiseLevel` 改為 `High`，或使用 `BinarizeMethod.Sauvola`。這些調整屬於 **improve OCR accuracy** 的策略之一。

## 從掃描檔讀取文字

現在引擎已就緒，我們載入圖像。無論是以 JPEG 形式保存的掃描 PDF 頁面，或是印刷表單的照片，程式碼皆相同。

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/photo_receipt.jpg");
```

如果你有 `Stream` 而非檔案路徑，只需將 `FromFile` 換成 `FromStream`。此彈性在處理來自網路上傳的 **read text from scan** 圖片時相當便利。

## 從收據擷取文字

所有設定完成後，實際的 OCR 呼叫只需一行程式碼。此方法會回傳擷取出的純文字字串，我們可以將其顯示、儲存，或傳入其他系統。

```csharp
// Perform OCR and capture the result
string extractedText = ocrEngine.Recognize();

// Output the text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(extractedText);
```

**預期輸出**（簡易收據範例）：

```
=== OCR RESULT ===
Store: CoffeeShop
Date: 2024-02-15
Item      Qty   Price
Latte      2    4.50
Bagel      1    2.75
Total            7.25
```

如果輸出呈現亂碼，請重新檢查前置處理部分——這是最常需要 **improve OCR accuracy** 的地方。

## 提升 OCR 準確度 – 進階調整

雖然預設設定適用於多數情況，但在生產等級的流程中常需要額外調整：

| 情況 | 調整 | 原因 |
|-----------|------------|--------|
| 背景極暗 | `ContrastEnhancement = true` + `Binarize = BinarizeMethod.Sauvola` | 提升文字與背景的分離度 |
| 手寫筆記 | `ocrEngine.LoadLanguage(LanguageModel.EnglishHandwritten)` | 針對手寫筆畫的專屬模型 |
| 多頁掃描 | Loop over each page image and call `Recognize()` per iteration | 降低記憶體佔用 |
| 大型圖像（> 2000 px） | Resize before feeding to OCR (`Image.Resize(width, height)`) | 加快處理速度，減少記憶體波動 |

請記住，**how to perform OCR** 並非萬用配方——你往往需要不斷調整這些參數，直至輸出符合你的品質標準。

## 完整可執行範例

以下是完整、可直接複製貼上的程式碼。它包含了前述所有部份，並加入一個小型輔助函式，用於在讀取前檢查檔案是否存在。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine and load language
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 2️⃣ Set up preprocessing to improve OCR accuracy
        ocrEngine.Preprocessing = new PreprocessingOptions
        {
            Deskew = true,
            Denoise = DenoiseLevel.Medium,
            Binarize = BinarizeMethod.Otsu,
            ContrastEnhancement = true
        };

        // 3️⃣ Path to the image – change this to your own file
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo_receipt.jpg");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"⚠️  Image not found: {imagePath}");
            return;
        }

        // 4️⃣ Load the image (recognize text from photo / read text from scan)
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 5️⃣ Perform OCR – this is the core of how to perform OCR
        string extractedText = ocrEngine.Recognize();

        // 6️⃣ Show the result – you can now extract text from receipt, invoice, etc.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

使用 `dotnet run` 執行程式。若一切設定正確，將會在主控台上看到擷取出的文字。

## 常見問題與特殊情況

**Q: 如果圖片是 PDF 會怎樣？**  
A: 先將每一頁 PDF 轉換為圖像（例如使用 `Aspose.Pdf` 或 `PdfSharp`），再將產生的 bitmap 傳入 `ocrEngine.Image`。

**Q: 我可以平行處理圖像嗎？**  
A: 可以，但每個執行緒需要建立獨立的 `OcrEngine`。此引擎非執行緒安全，若共用同一個實例可能會導致競爭條件。

**Q: 這在 Linux 上能運作嗎？**  
A: 完全可以。Aspose.OCR 為跨平台套件，只需確保已安裝原生相依性（Linux 上 .NET Core 需要 `libgdiplus`）。

**Q: 如何處理多語言收據？**  
A: 在辨識前載入多個語言模型：  
```csharp
ocrEngine.LoadLanguage(LanguageModel.English);
ocrEngine.LoadLanguage(LanguageModel.Spanish);
```  
引擎會依序嘗試每個模型。

## 結論

現在你已掌握使用 Aspose.OCR 在 C# 中 **how to perform OCR** 的完整端對端解決方案。本教學涵蓋了從初始化引擎、**recognize text from photo**、**read text from scan** 到 **extract text from receipt** 的所有步驟，並提供了實用的 **improve OCR accuracy** 方法。  

接下來的步驟？可以嘗試將英文模型換成手寫模型、實驗不同的 `BinarizeMethod` 參數，或將 OCR 呼叫整合至即時處理上傳的 ASP.NET API 中。可能性與你提供的圖像一樣廣闊。  

對 OCR、圖像前置處理或 Aspose 函式庫有更多疑問嗎？歡迎留言或深入閱讀官方 Aspose.OCR 文件。祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}