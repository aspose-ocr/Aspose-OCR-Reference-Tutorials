---
category: general
date: 2026-10-21
description: 學習如何對 JPG 進行 OCR、從圖像中擷取文字，並使用 Aspose.OCR 在 C# 中載入圖像進行 OCR。完整的逐步教學指南。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from jpg
- load image for OCR
- perform OCR on image
language: zh-hant
lastmod: 2026-10-21
og_description: 如何在 C# 中使用 Aspose.OCR 進行圖像 OCR。請參考本指南載入圖像以執行 OCR，從 JPG 識別文字並從圖像中提取文字。
og_image_alt: Screenshot showing how to perform OCR on a Cyrillic image in C#
og_title: 如何在 C# 中對圖像執行 OCR – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to perform OCR on a JPG, extract text from image and load
    image for OCR using Aspose.OCR in C#. Complete step‑by‑step guide.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
- Image processing
- Text extraction
title: 如何在 C# 中使用 Aspose.OCR 對圖像執行 OCR
url: /zh-hant/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.OCR 對圖像執行 OCR

如果您需要 **how to perform OCR** 在圖片上執行 OCR，這篇教學會向您展示一個完整、可直接執行的解決方案。您將學習如何載入 OCR 圖像、從 JPG 檔案辨識文字，以及使用 Aspose.OCR 函式庫從圖像中擷取文字。

本指南涵蓋從安裝 NuGet 套件、處理語言模型到列印辨識結果的全部步驟。完成後，您即可將 OCR 整合至任何 .NET 專案，並在不離開 IDE 的情況下處理西里爾文或其他語言文字。

## 您需要的環境

- .NET 6.0 或更新版本（此程式碼亦可於 .NET Framework 4.7+ 執行）
- Visual Studio 2022（或任何 C# 編輯器）
- 首次執行時需要網路連線（Aspose.OCR 會自動下載語言模型）
- 範例圖像，例如 `cyrillic_sample.jpg`，放置於可於程式碼中參照的資料夾

## 第一步：安裝 Aspose.OCR

在 NuGet 套件管理員中開啟，並將 **Aspose.OCR** 加入您的專案：

```bash
dotnet add package Aspose.OCR
```

此套件包含 OCR 引擎、語言模型以及影像處理所需的輔助類別。無需額外的 DLL。

## 第二步：建立 OCR 引擎 – how to perform OCR

在 **how to perform OCR** 中的第一個實作任務是實例化引擎。此物件負責整個辨識流程。

```csharp
using Aspose.OCR;

// Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

`OcrEngine` 輕量且可重複使用，同一個實例可處理多張影像，提升批次處理的效能。

## 第三步：載入 OCR 圖像

在辨識之前必須提供影像資料。**load image for OCR** 步驟支援多種格式，但本範例以 JPEG 檔案為例。

```csharp
// Load the image you want to process
engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

`OcrImage.FromFile` 會將檔案讀入記憶體並為引擎做好準備。若檔案路徑無效，會拋出 `ArgumentException`，請確保路徑正確。

## 第四步：選擇適當的語言（可選，但建議）

若影像中包含西里爾字元，請將語言設定為 `Cyrillic`。所需模型會在首次執行時自動下載。

```csharp
// Choose the language model
engine.Language = OcrLanguage.Cyrillic;
```

您也可以透過變更此屬性切換至其他語言（例如 `OcrLanguage.English`）。此函式庫支援超過 60 種語言。

## 第五步：從 JPG 辨識文字 – how to perform OCR on a JPEG

現在呼叫 `Recognize` 方法。這是 **how to perform OCR** 的核心，會將位圖轉換為 Unicode 文字。

```csharp
// Perform the recognition
engine.Recognize();
```

此方法會阻塞直至 OCR 處理完成。對於大型影像，建議在背景執行緒上執行，以保持 UI 的回應性。

## 第六步：從影像擷取文字

辨識完成後，引擎會將結果存於 `Text` 屬性。此即完成 **extract text from image** 步驟。

```csharp
// Retrieve the extracted text
string extractedText = engine.Text;

// Output the recognized text to the console
Console.WriteLine(extractedText);
```

輸出將包含圖中找到的精確字元，保留換行與標點符號。

## 完整、可執行範例

將所有步驟整合後，即得到一個可直接複製、貼上並執行的程式：

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image for OCR
        engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");

        // Step 3: Choose the language model (Cyrillic in this case)
        engine.Language = OcrLanguage.Cyrillic;

        // Step 4: Perform OCR on the image
        engine.Recognize();

        // Step 5: Extract text from image
        string extractedText = engine.Text;

        // Step 6: Output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

### 預期輸出

若 `cyrillic_sample.jpg` 包含短語 “Привет мир”（Hello world），控制台將顯示：

```
=== OCR Result ===
Привет мир
```

不同的字型或影像品質可能影響準確度，但 Aspose.OCR 在清晰列印的情況下通常可達 >95 % 的辨識率。

## 常見陷阱與實用技巧

- **Image quality matters** – 低解析度或雜訊較多的 JPEG 會降低準確度。如有需要，可使用 `engine.Image.AdjustContrast()` 進行影像前處理（例如提升對比度）。
- **Language model download** – 第一次執行時會將模型下載至 `%USERPROFILE%\.Aspose\OCR`。請確保執行程序具有寫入權限。
- **Batch processing** – 重複使用同一個 `OcrEngine` 實例，僅在檔案之間變更 `engine.Image`。可避免重複載入模型。
- **Memory usage** – 大尺寸影像會佔用較多記憶體。若在迴圈中處理大量檔案，請在每次辨識後呼叫 `engine.Image.Dispose()` 釋放資源。
- **Thread safety** – `OcrEngine` 並非執行緒安全。平行處理時，請為每個執行緒建立獨立的實例。

## 結論

現在您已了解如何在 JPEG 上 **how to perform OCR**、**load image for OCR**，以及使用 Aspose.OCR 在 C# 中 **extract text from image**。完整的解決方案示範了語言設定、從 JPG 辨識文字以及列印結果，為任何文字擷取專案奠定堅實基礎。

接下來，您可以探索相關主題，例如 **perform OCR on image** 批次處理、將 OCR 與 ASP.NET Core API 整合，或將擷取的文字轉換為可搜尋的 PDF。嘗試不同語言與影像前處理，以提升辨識品質。

## 接下來您可以學習什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [如何在 C# 中執行 OCR – 使用 Aspose OCR 將影像轉換為文字](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-text-with-aspose-oc/)
- [如何在 C# 中執行 OCR – 從影像辨識文字](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/)
- [如何使用 Aspose.OCR for .NET 從影像擷取文字](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}