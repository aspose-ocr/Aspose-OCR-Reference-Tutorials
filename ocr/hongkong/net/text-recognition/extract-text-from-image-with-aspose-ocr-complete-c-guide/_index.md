---
category: general
date: 2026-01-07
description: 使用 Aspose OCR 於 C# 從圖像擷取文字。了解如何從相片辨識文字、提升 OCR 準確度、載入圖像進行 OCR 以及設定 OCR
  語言。
draft: false
keywords:
- extract text from image
- recognize text from photo
- improve ocr accuracy
- load image for ocr
- set ocr language
language: zh-hant
og_description: 使用 Aspose OCR 從圖像中提取文字。本指南展示如何從相片中辨識文字、提升 OCR 準確度、載入圖像進行 OCR 以及設定
  OCR 語言。
og_title: 使用 Aspose OCR 從圖像提取文字 – C# 教程
tags:
- Aspose OCR
- C#
- Image Processing
title: 使用 Aspose OCR 從圖像擷取文字 – 完整 C# 指南
url: /zh-hant/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖片擷取文字 – 完整 C# 實作搭配 Aspose OCR

是否曾需要 **從圖片擷取文字**，卻不確定哪個函式庫能提供可靠的結果？你並不孤單。在許多實務應用中——收據掃描、身分證驗證，或只是快速筆記工具——**從相片辨識文字** 是必備功能。

在本教學中，我們將一步步說明完整、可直接執行的範例，示範如何 **載入圖片供 OCR 使用**、設定引擎的 **OCR 語言**，以及運用幾個前處理技巧 **提升 OCR 準確度**。完成後，你將擁有一個單一的 C# 檔案，能將擷取的文字印出至主控台，並了解每個設定的意義。

> **提示：** 此程式碼相容於 Aspose.OCR ≥ 23.5、.NET 6+，以及任何能執行 .NET Core 的 Windows、Linux 或 macOS 環境。

## 前置條件

- 已安裝 .NET 6 SDK（或更新版本）  
- Visual Studio 2022、VS Code，或任意你慣用的編輯器  
- NuGet 套件 `Aspose.OCR`（可透過 `dotnet add package Aspose.OCR` 安裝）  
- 一張包含清晰印刷或打字文字的影像檔（JPEG/PNG）  

如果以上都已備妥，讓我們開始吧。

![從圖片擷取文字範例](/images/ocr-example.png "從圖片擷取文字 – Aspose OCR 輸出")

## 步驟 1：建立並釋放 OCR 引擎 – 「從圖片擷取文字」核心

首先需要取得 `OcrEngine` 的實例。將它包在 `using` 區塊中，可確保原生資源得到正確釋放。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

/// <summary>
/// Demonstrates how to extract text from image using Aspose OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // Step 1 – Initialize the OCR engine (the heart of the process)
        using (var ocrEngine = new OcrEngine())
        {
            // The rest of the workflow lives inside this block.
```

**為何這很重要：** `OcrEngine` 會為原生 OCR DLL 保留非受控記憶體。及時釋放可避免記憶體泄漏，尤其在批次處理大量圖片時更是關鍵。

## 步驟 2：定義辨識設定 – 提升 OCR 準確度

接著建立 `RecognitionSettings` 物件。此處可 **設定 OCR 語言**，並加入前處理濾鏡，往往能決定輸出是雜亂字串還是乾淨結果。

```csharp
            // Step 2 – Configure recognition settings
            var recognitionSettings = new RecognitionSettings
            {
                // Set the language to English; other languages are available via Language enum.
                Language = Language.English,

                // PreprocessFilters help the engine deal with real‑world photo issues.
                PreprocessFilters = new[]
                {
                    PreprocessFilter.Deskew,          // Corrects slight rotation
                    PreprocessFilter.Denoise,         // Reduces grainy noise
                    PreprocessFilter.ContrastEnhance // Boosts text visibility
                }
            };
```

**為何使用這些濾鏡？**  
- **Deskew** 修正手機拍照時常見的角度偏差。  
- **Denoise** 移除可能被誤認為字元的雜訊點。  
- **ContrastEnhance** 讓淡淡的墨跡更突出，對 **提升 OCR 準確度** 至關重要。

## 步驟 3：載入圖片 – 高效載入 OCR 圖片

Aspose 提供 `ImageStream.FromFile` 以快速載入。若圖片來源是 Web 請求或資料庫，也可以傳入 `MemoryStream`。

```csharp
            // Step 3 – Load the image you want to analyze
            var imagePath = @"YOUR_DIRECTORY/phone_photo.jpg";
            var imageStream = ImageStream.FromFile(imagePath);
```

**常見陷阱：** 在 Windows 上使用正斜線路徑仍可運作，但使用 `Path.Combine` 會讓跨平台專案更安全。

## 步驟 4：執行辨識 – 從相片辨識文字

現在呼叫 `Recognize`，同時傳入圖片串流與設定。此方法會回傳包含擷取文字的純字串。

```csharp
            // Step 4 – Run OCR and capture the result
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

若圖片內有多個文字區塊，Aspose 會以換行符號串接，盡可能保留原始版面配置。

## 步驟 5：輸出結果 – 驗證擷取

最後將結果寫入主控台。實際應用中，你可能會將它存入資料庫、傳送至其他服務，或在 UI 中顯示。

```csharp
            // Step 5 – Show the extracted text
            Console.WriteLine("=== Extracted Text Start ===");
            Console.WriteLine(recognizedText);
            Console.WriteLine("=== Extracted Text End ===");
        } // End of using block – OcrEngine disposed
    }
}
```

### 預期的主控台輸出

```
=== Extracted Text Start ===
This is a sample receipt.
Total: $23.45
Thank you for shopping!
=== Extracted Text End ===
```

如果看到雜亂的字元，請再次確認圖片是否清晰、語言是否正確，以及前處理濾鏡是否適當。

## 步驟 6：可選調整 – 為特殊情況微調

### a. 切換語言

```csharp
recognitionSettings.Language = Language.Spanish; // For Spanish receipts
```

### b. 加入自訂濾鏡

Aspose 亦提供 `PreprocessFilter.Sharpen` 或 `PreprocessFilter.Binarize`。當預設三項濾鏡不足以應付時，可自行實驗。

### c. 處理大型圖片

對於超高解析度的相片，可先縮小尺寸以降低記憶體使用：

```csharp
var resizedStream = ImageProcessor.Resize(imageStream, 1024, 768);
string text = ocrEngine.Recognize(resizedStream, recognitionSettings);
```

## 常見問答

**Q: 這能辨識手寫筆記嗎？**  
A: Aspose OCR 主要針對印刷文字進行優化。手寫辨識需要其他引擎（例如 Aspose.OCR for Handwriting 或機器學習模型）。

**Q: 可以在迴圈中處理多張圖片嗎？**  
A: 當然可以。只要將 `using (var ocrEngine = new OcrEngine())` 區塊移到迴圈外，重複使用同一個引擎即可提升效能。

**Q: 若圖片是 PDF 頁面該怎麼辦？**  
A: 先將 PDF 頁面轉為影像（可使用 Aspose.PDF 將頁面渲染為 PNG/JPEG），再交給 OCR 引擎處理。

## 重點回顧 – 我們完成了什麼

- 使用單一、獨立的 C# 程式 **從圖片擷取文字**。  
- 示範如何透過前處理 **提升 OCR 準確度**，從而 **從相片辨識文字**。  
- 展示正確的 **載入圖片供 OCR** 與 **設定 OCR 語言** 方式，支援多語系情境。  

## 後續步驟與相關主題

- **批次處理：** 結合 `Directory.GetFiles`，一次 OCR 整個資料夾。  
- **後處理：** 使用正規表達式清理日期、金額或身分證號等資訊。  
- **整合應用：** 將擷取的文字送入 Azure Cognitive Search 或 Elastic，建立可搜尋的文件。  

歡迎嘗試不同的濾鏡組合、語言與影像來源。核心流程不變：建立引擎、設定參數、載入影像、辨識、輸出。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}