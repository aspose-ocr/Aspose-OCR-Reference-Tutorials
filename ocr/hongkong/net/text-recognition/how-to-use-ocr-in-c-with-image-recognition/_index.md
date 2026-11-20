---
category: general
date: 2026-11-20
description: 如何在 C# 中使用 OCR 從圖片識別文字。學習載入圖片 OCR、設定 OCR 語言，並從 JPEG 檔案提取文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text image
- load image OCR
- recognize text JPEG
- set OCR language
language: zh-hant
lastmod: 2026-11-20
og_description: 如何在 C# 中使用 OCR 從圖像提取文字。本指南展示了載入圖像、設定 OCR 語言，以及從 JPEG 檔案辨識文字。
og_image_alt: Screenshot of C# code demonstrating how to use OCR to recognize text
  from an image
og_title: 如何在 C# 中使用 OCR – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to use OCR in C# to recognize text from an image. Learn to load
    image OCR, set OCR language, and extract text from JPEG files.
  headline: How to use OCR in C# with image recognition
  type: TechArticle
tags:
- OCR
- C#
- Image processing
- Text extraction
title: 如何在 C# 中使用 OCR 進行圖像辨識
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-with-image-recognition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR 進行圖像辨識

如果您需要在 C# 應用程式中 **how to use OCR**，本指南將帶您完成整個流程。無論是將掃描合約數位化，或是從照片中提取資訊，您都將學會快速且可靠地 **recognize text image** 檔案。

本教學涵蓋載入圖像、設定 OCR 引擎，以及從 JPEG 檔案取得辨識文字。完成後，您將擁有一個自包含、可執行的範例，能直接放入任何 .NET 專案中使用。

## 前置條件

* 已安裝 .NET 6.0（或更新版本）。
* 取得提供 `OcrEngine`、`ImageStream` 與語言模組的 OCR 函式庫（例如 **Leadtools**、**Aspose.OCR**，或任何相容套件）。
* 在已知目錄中有一個名為 `sample.jpg` 的範例圖像。

不需要額外的外部服務——OCR 引擎會自動下載缺少的語言套件。

## 步驟 1：載入 OCR 圖像

載入圖像是任何 OCR 工作流程的第一步。以下程式碼會從磁碟上的 JPEG 檔案建立 `ImageStream`。

```csharp
// Step 1: Load the image to be recognized
var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
var image = ImageStream.FromFile(imagePath);
```

*為什麼這很重要：* `ImageStream` 物件抽象化檔案處理，並提供 OCR 引擎所需的像素資料。若找不到檔案，`FromFile` 會拋出明確的例外，使除錯變得直接。

## 步驟 2：建立 OCR 引擎實例（自動釋放）

使用 `using` 區塊可確保在 OCR 工作完成後立即釋放非受控資源。

```csharp
// Step 2: Create an OCR engine instance (automatically disposes when done)
using var ocrEngine = new OcrEngine();
```

*專業提示：* 相較於手動呼叫 `Dispose()`，建議使用 `using` 陳述式，因為它可避免遺忘釋放原生記憶體的風險，從而防止長時間服務的記憶體泄漏。

## 步驟 3：設定 OCR 語言（可選但建議）

若您知道來源文件的語言，設定語言可提升辨識精度並加快處理速度。範例將語言設定為西里爾文；您可以改為任何支援的語言列舉值。

```csharp
// Step 3 (optional): Specify the language module, e.g., Cyrillic
// The required language pack will be downloaded automatically if missing
ocrEngine.Language = OcrLanguage.Cyrillic;
```

*為什麼要設定語言？* OCR 引擎內含特定語言的字元模型。選擇正確的模型可減少偽陽性，避免不必要的字元替換。

## 步驟 4：對已載入的圖像執行 OCR

現在引擎會處理位圖，並以字串形式回傳辨識出的文字。

```csharp
// Step 4: Perform OCR on the loaded image
string recognizedText = ocrEngine.Recognize(image);
```

*特殊情況：* 若圖像解析度低或壓縮過度，引擎可能只回傳部分結果。建議先進行前處理（例如二值化）以獲得更佳效果。

## 步驟 5：輸出辨識文字

最後，將擷取的文字顯示於主控台，或傳遞給其他元件。

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

**預期輸出**

```
=== Recognized Text ===
Пример текста, полученного из изображения.
```

具體內容取決於來源圖像，但主控台會顯示 OCR 引擎偵測到的完整字串。

## 完整、可執行的範例

將所有步驟整合即可得到一個緊湊的程式，您可以立即編譯並執行。

```csharp
using System;
using System.IO;

// Ensure you reference the OCR library that provides these types
// e.g., using Leadtools.OCR;

class Program
{
    static void Main()
    {
        // Load the image to be recognized
        var imagePath = Path.Combine("YOUR_DIRECTORY", "sample.jpg");
        var image = ImageStream.FromFile(imagePath);

        // Create an OCR engine instance (auto‑dispose)
        using var ocrEngine = new OcrEngine();

        // Optional: set the language (Cyrillic in this case)
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // Perform OCR
        string recognizedText = ocrEngine.Recognize(image);

        // Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

將程式碼複製到新的 Console 專案中，將 `YOUR_DIRECTORY` 替換為圖像所在路徑，然後執行 `dotnet run`。程式會將辨識文字印出至主控台。

## 常見問題與疑難排解

| Question | Answer |
|----------|--------|
| **如果語言套件未下載該怎麼辦？** | OCR 函式庫會自動嘗試下載。請確保機器具備網路連線，或依照函式庫文件事先安裝語言套件。 |
| **我可以辨識 PNG 或 BMP 檔案的文字嗎？** | 可以。`ImageStream.FromFile` 可支援底層影像函式庫所支援的任何格式，只需更改檔案副檔名即可。 |
| **如何提升噪點掃描的辨識精度？** | 在傳遞給 `Recognize` 前先對圖像進行前處理（對比度調整、除噪），許多函式庫提供 `ImageProcessor` 類別可用於此目的。 |
| **在使用者上傳的檔案上執行 OCR 安全嗎？** | 請驗證檔案大小與類型，並在沙箱環境中執行 OCR，以避免惡意載荷。 |

## 結論

您現在已了解如何在 C# 中 **how to use OCR** 以可靠地 **recognize text image** 檔案、**load image OCR**、**set OCR language**，以及 **recognize text JPEG** 內容。完整範例展示了一個簡潔、可釋放的工作流程，您可進一步加入前處理、多語言支援，或整合至更大型的文件處理管線中。

### 後續步驟

* 透過迴圈處理 JPEG 目錄，探索批次處理。  
* 將 OCR 與自然語言處理 (NLP) 結合，以抽取結構化資料。  
* 嘗試其他語言模組，例如 `OcrLanguage.English` 或 `OcrLanguage.Arabic`。  

歡迎依您的實際需求調整程式碼，祝開發順利！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通額外的 API 功能，並在自己的專案中探索替代實作方式。

- [在 C# 中使用 Windows.Media.Ocr 辨識文字圖像 – 完整 OCR 指南](/ocr/english/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/)
- [如何在 C# 中使用 OCR – 非同步擷取圖像文字](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-asynchronously/)
- [如何在 C# 中使用 OCR – 使用 Aspose OCR 擷取圖像文字](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}