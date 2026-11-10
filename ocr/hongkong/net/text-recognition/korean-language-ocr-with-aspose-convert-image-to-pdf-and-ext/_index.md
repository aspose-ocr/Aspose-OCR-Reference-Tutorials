---
category: general
date: 2026-05-28
description: 使用 Aspose 於 C# 的韓文 OCR 教學。學習如何從串流載入影像、提取純文字、將影像轉換為 PDF 以及匯出可搜尋的 PDF。
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: zh-hant
og_description: 使用 Aspose 在 C# 中進行韓文 OCR。逐步指南：從串流載入影像、提取純文字、將影像轉換為 PDF 並匯出可搜尋的 PDF。
og_title: 韓文 OCR – 圖像轉 PDF 並提取文字 (C# 指南)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 使用 Aspose 的韓文 OCR：將圖像轉換為 PDF 並在 C# 中提取文字
url: /zh-hant/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose 進行韓文 OCR：將影像轉換為 PDF 並在 C# 中擷取文字

有沒有想過在不將資料上傳至雲端的情況下執行 **Korean Language OCR**？你並不是唯一有此需求的人。無論是數位化街道招牌、處理收據，或是建構多語言搜尋索引，能在本機辨識韓文字元都能為你節省時間、成本與隱私上的麻煩。

在本教學中，我們將一步步示範完整且可執行的範例，說明如何 **load image from stream**、**extract plain text**、**convert image to PDF**，最後 **export searchable PDF**——全部使用 Aspose.OCR 以及少量 C# 程式碼。無需外部服務、無隱藏魔法——只要純 .NET 程式碼即可直接放入任何 Console 應用程式。

## 你將學會什麼

- 一個可執行的 Console 程式，透過檔案串流讀取 JPEG 檔案。  
- 以 Unicode 字串形式擷取的韓文文字。  
- 詳細的 JSON 報告，可用於除錯或分析 OCR 執行結果。  
- 可搜尋的 PDF，能在任何 PDF 閱讀器中選取韓文字。

**Prerequisites**  
- .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.7 以上）。  
- 已安裝 Aspose.OCR for .NET NuGet 套件（`Install-Package Aspose.OCR`）。  
- 一個資料夾內含 `korean_sign.jpg`，以及可寫入的輸出位置。

如果上述條件皆已就緒，太好了——讓我們動手實作。

## Step 1: Initialize the OCR Engine for Korean Language OCR

第一步需要建立 `OcrEngine` 實例。若有 GPU 可用，啟用 GPU 會大幅提升辨識速度；同時關閉自動資源下載，可強制使用離線語言套件，確保在無網路環境下仍能正常運作。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **為什麼這很重要：**  
> *GPU 加速* 能將大型批次的處理時間從秒級縮短至毫秒級。將 `AutomaticResourceDownload` 設為 `false`，確保範例在離線環境下執行——這是許多企業環境的關鍵需求。

## Step 2: Load Image from Stream

透過串流讀取影像可提供彈性：你可以從磁碟、網路共享，甚至是記憶體快取的 Blob 中取得檔案。此處示範開啟本機 JPEG 檔案，其他 `Stream` 亦同理。

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **專業提示：** 若需處理 Web API 上傳的影像，只要將 `File.OpenRead` 改成 `IFormFile.OpenReadStream()`，其餘程式碼保持不變。

## Step 3: Choose Korean Language and Apply Pre‑Processing Filters

Aspose.OCR 支援多種前置處理步驟，可在辨識前清理影像。對於韓文招牌而言，校正傾斜與去噪聲通常已足夠。

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **背後發生了什麼？**  
> `Deskew` 濾鏡會將傾斜的文字校正為水平，`Denoise` 則移除可能干擾字元分類器的雜訊。若省略這些步驟，低解析度照片常會產生亂碼輸出。

## Step 4: Extract Plain Text Asynchronously

現在到了關鍵時刻——讓引擎辨識字元並回傳乾淨的字串。使用 `RecognizeAsync` 可在桌面或 Web 應用程式中保持 UI 響應。

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

執行程式後，你應該會看到類似以下的輸出：

```
OCR complete. Extracted text:
서울시청
```

> **為什麼使用 async？**  
> OCR 可能相當耗費 CPU。非同步執行可避免執行緒被阻塞，對於 ASP.NET Core 等需要避免執行緒飢餓的環境特別有用。

## Step 5: Get a Detailed Recognition Result and Save as JSON

有時候僅有原始字串不足以滿足需求——例如需要信心分數、邊界框或原始影像資料。`RecognizeDetailed` 方法會回傳 `RecognitionResult` 物件，便於序列化為 JSON 供日後分析。

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

開啟 `korean_ocr.json` 後會看到類似以下的結構：

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **何時使用此功能？**  
> 若你在建構搜尋索引，信心值可協助過濾低品質結果。若需在 UI 中高亮文字，邊界框則是你的座標圖。

## Step 6: Convert Image to PDF and Export Searchable PDF

Aspose 讓從點陣圖到向量圖的轉換變得輕鬆。將 `OutputFormat` 設為 `SearchablePdf`，函式庫會嵌入原始影像並在其上覆蓋一層隱形文字層，包含 OCR 輸出。產生的 PDF 可被搜尋、複製與索引，與一般 PDF 無異。

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

在 Adobe Reader 或任何 PDF 檢視器中開啟 `korean_searchable.pdf`，按 **Ctrl+F**，輸入韓文字，即可直接跳至該頁面的正確位置。這就是可搜尋 PDF 的威力。

> **額外小技巧：** 若只需要純視覺的 PDF（不含隱藏文字層），只要將 `OutputFormat` 改成 `Pdf` 即可。

## Full Working Example

以下為完整程式碼——直接複製、貼上，將 `YOUR_DIRECTORY` 替換成實際路徑，然後按 **F5** 執行。

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Expected Console Output

```
OCR complete. Extracted text:
서울시청
```

執行後，你會在原始影像旁看到三個新檔案：

- `korean_ocr.json` – 完整的辨識資料。  
- `korean_searchable.pdf` – 可搜尋的 PDF。  
- （可選）任何你自行加入的中間日誌。

## Common Questions & Edge Cases

**如果我沒有 GPU 該怎麼辦？**  
將 `EnableGpu = false`；CPU 後備在小批次處理時已足夠。

**可以一次處理多張影像嗎？**  
當然可以。將核心邏輯包在 `foreach (var file in Directory.GetFiles(...))` 迴圈中，並在每次迭代重新指派 `ocrEngine.Image` 即可。

**如何同時處理韓文以外的其他語言？**  
Aspose.OCR 允許設定 `Language = Language.AutoDetect`，或使用位元 OR 方式結合語言，例如 `Language.Korean | Language.English`。

**如果 OCR 信心值太低該怎麼辦？**  
檢查 `detailedResult.Pages[0].Words`，過濾 `Confidence < 0.7` 的項目。也可以調整前置處理濾鏡——試著加入 `PreprocessFilter.ContrastEnhancement`。

## Wrapping Up

你已完整了解如何以 **Korean Language OCR** 從 **loading image from stream**、**extract plain text**、**convert image to PDF**，最終 **export searchable PDF** 的全流程。此方法具備模組化特性，未來可自由替換影像來源、變更輸出格式，或將 JSON 輸出接入任何下游管線。

What’s next

## Related Tutorials

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}