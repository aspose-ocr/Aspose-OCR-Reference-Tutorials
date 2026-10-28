---
category: general
date: 2026-10-27
description: C# 範例 OCR 西里爾文字指南說明如何使用 C# OCR 函式庫，透過正確的 OCR 設定，從圖像中擷取西里爾文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- c# example ocr cyrillic
- c# ocr library
- cyrillic language module
- image text extraction
- ocr settings
- recognition language
language: zh-hant
lastmod: 2026-10-27
og_description: c# 範例 OCR 西里爾文字示範如何設定 C# OCR 函式庫、載入影像，並輸出辨識出的西里爾文字，附完整程式碼。
og_image_alt: Diagram of c# example ocr cyrillic workflow showing image loading, OCR
  settings, and text output
og_title: C# 範例 OCR 西里爾文字 – 提取西里爾文字的逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-27'
  description: c# example ocr cyrillic guide shows how to use a C# OCR library to
    extract Cyrillic text from images with proper OCR settings.
  headline: c# example ocr cyrillic – perform OCR on Cyrillic text
  type: TechArticle
tags:
- C#
- OCR
- Cyrillic
- Image Processing
- Example
title: C# 範例 OCR 西里爾文 – 對西里爾文字執行 OCR
url: /zh-hant/net/ocr-settings/c-example-ocr-cyrillic-perform-ocr-on-cyrillic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# 範例 OCR 西里爾文 – 執行西里爾文字的 OCR

如果你需要 **c# example ocr cyrillic**，本教學將帶你完成整個流程。你將學習如何設定 C# OCR 函式庫、載入含有西里爾字元的影像，並從辨識引擎取得純文字。

OCR（光學字符辨識）能處理多種字母表，但西里爾文需要專屬的語言模組。本指南涵蓋所有必備步驟——從安裝函式庫到驗證輸出——讓你能將西里爾文字擷取整合到任何 .NET 專案中。

## 前置條件

* .NET 6.0 或更新版本已安裝  
* 支援語言模組的 C# OCR 函式庫（例如 **IronOCR**, **Tesseract .NET**, 或商業 SDK）  
* 包含西里爾文字的影像檔（範例使用 `cyrillic_sample.jpg`）  

你不需要額外的 OCR 引擎二進位檔；函式庫會在你請求時自動下載 **cyrillic language module**。

## 步驟 1：載入包含西里爾文字的影像

第一步是將來源影像讀入記憶體。`Image.FromFile` 方法會建立一個 `System.Drawing.Image` 物件，供 OCR 引擎處理。

```csharp
// Load the image file that holds Cyrillic characters
var sourceImage = Image.FromFile("YOUR_DIRECTORY/cyrillic_sample.jpg");

// Verify that the image was loaded successfully
if (sourceImage == null)
{
    throw new InvalidOperationException("Failed to load the image file.");
}
```

*Why this matters*：將影像載入為 `System.Drawing.Image` 可讓 OCR 引擎直接存取像素資料，提升對西里爾等複雜文字的辨識準確度。

## 步驟 2：設定 OCR 參數以請求西里爾語言模組

OCR 引擎會提供設定物件讓你指定目標語言。將 `Language` 設為 `RecognitionLanguage.Cyrillic`，若尚未安裝，會觸發下載 **cyrillic language module**。

```csharp
// Create OCR settings and request the Cyrillic language pack
var ocrSettings = new RecognitionSettings
{
    Language = RecognitionLanguage.Cyrillic   // activates the Cyrillic module
};

// Optional: adjust additional parameters for better accuracy
ocrSettings.Dpi = 300;               // higher DPI improves character detail
ocrSettings.EnableNoiseReduction = true;
```

*Why this matters*：若未使用正確的語言模組，引擎會將西里爾字元視為未知字形，導致輸出雜亂。`RecognitionLanguage` 列舉確保引擎使用正確的字元集。

## 步驟 3：使用指定設定執行 OCR 引擎於影像上

現在呼叫 OCR 引擎，傳入影像與先前設定。`Recognize` 方法會回傳包含擷取文字的結果物件。

```csharp
// Perform OCR using the image and the prepared settings
var ocrResult = OcrEngine.Recognize(sourceImage, ocrSettings);

// Verify that the OCR process succeeded
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    throw new InvalidOperationException("OCR did not return any text.");
}
```

*Why this matters*：`OcrEngine.Recognize` 結合 **image text extraction** 與特定語言模型，產生保留西里爾字元的 Unicode 文字。

## 步驟 4：將辨識出的純文字輸出至主控台

最後，顯示擷取的文字。在實際應用中，你可能會將結果寫入資料庫或傳遞給其他服務，但 `Console.WriteLine` 已足以示範核心輸出。

```csharp
// Write the recognized Cyrillic text to the console
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

**預期輸出**（範例）：

```
Recognized text:
Пример текста на кириллице
```

如果輸出與原始影像內容相符，代表你的 **c# example ocr cyrillic** 正常運作。

## 完整、可執行範例

以下是完整程式碼，你可以在加入相應的 OCR 函式庫參考後，直接複製、貼上並執行。

```csharp
using System;
using System.Drawing;
using YourOcrLibrary;          // Replace with the actual namespace of your OCR SDK

class Program
{
    static void Main()
    {
        // Step 1: Load the image that contains Cyrillic text
        var sourceImage = Image.FromFile("YOUR_DIRECTORY/cyrillic_sample.jpg");
        if (sourceImage == null)
        {
            Console.Error.WriteLine("Unable to load image.");
            return;
        }

        // Step 2: Configure OCR settings to request the Cyrillic language module
        var ocrSettings = new RecognitionSettings
        {
            Language = RecognitionLanguage.Cyrillic,
            Dpi = 300,
            EnableNoiseReduction = true
        };

        // Step 3: Run the OCR engine on the image with the specified settings
        var ocrResult = OcrEngine.Recognize(sourceImage, ocrSettings);
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.Error.WriteLine("OCR failed to extract text.");
            return;
        }

        // Step 4: Output the recognized plain text to the console
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **專業提示**：批次處理影像時，重複使用同一個 `OcrEngine` 實例以降低開銷。同時，可針對低對比或有背景圖樣的影像，調整 `Dpi` 與 `EnableNoiseReduction` 參數以取得更佳效果。

## 常見問題與邊緣案例

| Question | Answer |
|----------|--------|
| *如果西里爾模組未自動下載怎麼辦？* | 請確認應用程式具備網路連線，且 OCR 函式庫的授權允許即時下載模組。你也可以自行從供應商網站下載該模組，並將 SDK 指向本機資料夾。 |
| *我可以辨識混合語言的文件嗎（例如 Latin + Cyrillic）？* | 將 `Language = RecognitionLanguage.Multilingual`，或在 SDK 支援的情況下提供語言陣列。引擎會依需求在不同字元集之間切換。 |
| *如何處理大型影像而不耗盡記憶體？* | 在傳入 `Recognize` 前，先將影像長邊縮小至最高 2000 px。可使用 `Image.GetThumbnailImage` 建立記憶體效能較佳的副本。 |
| *輸出永遠是 Unicode 嗎？* | 現代 OCR 函式庫會回傳 UTF‑8 字串，能保留西里爾字元。如需其他編碼，可使用 `Encoding.GetEncoding("windows-1251")` 進行轉換。 |

## 結論

現在你已擁有一個 **c# example ocr cyrillic**，它會載入影像、設定 **cyrillic language module**、執行 OCR 引擎，並印出辨識文字。這個端對端流程示範了使用 C# OCR 函式庫進行 **image text extraction** 的關鍵步驟。

從這裡你可以：

* 將程式碼整合至接受上傳影像的 Web API 中。  
* 將範例擴充為先將 PDF 每頁轉為影像再處理。  
* 探索其他 **ocr settings**，如自訂字典或信心門檻。  

嘗試不同的影像品質與語言套件，以微調特定使用情境的辨識準確度。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以示範的技術為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [How to Perform OCR in C# – Recognize Cyrillic Text with Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [read text from png – extract Cyrillic text with Aspose OCR](/ocr/english/net/ocr-configuration/read-text-from-png-extract-cyrillic-text-with-aspose-ocr/)
- [Extract Text from Image in C# – Complete Aspose OCR Example](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-example/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}