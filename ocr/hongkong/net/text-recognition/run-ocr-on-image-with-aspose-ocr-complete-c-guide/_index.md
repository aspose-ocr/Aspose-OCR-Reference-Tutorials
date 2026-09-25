---
category: general
date: 2026-02-17
description: 使用 Aspose OCR 於 C# 執行圖像的光學字符辨識（OCR）。了解如何從 jpg 提取文字、為 OCR 進行圖像前處理，以及使用一步一步的程式碼載入圖像進行
  OCR。
draft: false
keywords:
- run OCR on image
- extract text from jpg
- preprocess image for OCR
- load image for OCR
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中對圖像執行 OCR。本指南將示範如何從 jpg 提取文字、預處理圖片，以及載入圖像以進行 OCR。
og_title: 使用 Aspose OCR 於圖像執行 OCR – 完整 C# 指南
tags:
- Aspose OCR
- C#
- Image Processing
title: 使用 Aspose OCR 於圖片執行 OCR – 完整 C# 指南
url: /zh-hant/net/text-recognition/run-ocr-on-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 在圖像上執行 OCR – 完整 C# 指南

曾經需要 **run OCR on image** 檔案，但不知從何開始嗎？在許多實際應用中——例如發票掃描器或收據追蹤器——第一個障礙是從 JPEG 中取得可靠的文字。好消息是？使用 Aspose OCR，你只需幾行 C# 程式碼就能 **run OCR on image** 檔案，並且還能學會如何 **extract text from jpg**、**preprocess image for OCR** 以及 **load image for OCR**，無需在零散的文件中搜尋。

在本教學中，我們將逐步演示一個完整、可直接複製貼上的範例，說明如何設定引擎、加入實用的前處理過濾器、將圖片送入辨識器，並將結果印到主控台。完成後，你將擁有一個可自行運作的程式，能直接放入任何 .NET 專案，即時從圖像中擷取文字。

## 需要的環境

- .NET 6.0 或更新版本（此程式碼亦可於 .NET Core 上執行）  
- Aspose.OCR NuGet 套件（`Install-Package Aspose.OCR`）  
- 放置於可參考資料夾中的範例 JPEG（`input.jpg`）  
- 基本的 C# 語法了解（不需高階知識）

如果你已經備妥上述項目，太好了——讓我們直接開始。若尚未準備，請先取得 NuGet 套件與測試圖片；本指南的後續內容皆假設你已完成這些步驟。

## 步驟 1：建立 OCR 引擎 – 執行 OCR on Image 的核心

要 **run OCR on image** 資料，首先必須實例化 `OcrEngine`。此物件保存了辨識所需的所有設定與狀態。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // Step 1 – create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **為何重要：** `OcrEngine` 是通往 Aspose 辨識流程的入口。沒有它，你將無法使用過濾器、語言套件或 `Recognize` 方法。

## 步驟 2：加入前處理過濾器 – 在 **extract text from jpg** 時提升準確度

直接從相機拍攝的影像很少是完美的。傾斜角度或隨機雜訊甚至會讓最好的 OCR 演算法也失靈。在 **extract text from jpg** 之前加入幾個過濾器，能顯著提升結果。

```csharp
        // Step 2 – add preprocessing filters
        // Deskew corrects rotation; DenoiseGaussian reduces visual noise
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });
```

> **專業提示：** 若來源影像已相當乾淨，可省略 `DenoiseGaussianFilter`。過度平滑可能會抹除微弱的字元。

## 步驟 3：載入影像以供 OCR – 將 JPEG 提供給引擎

接下來是 **load image for OCR** 的步驟。Aspose 提供了便利的 `ImageStream.FromFile` 輔助方法，將檔案路徑包裝成引擎可理解的串流。

```csharp
        // Step 3 – specify the path to the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        // Load the image and run OCR in one call
        var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));
```

> **邊緣情況：** 若檔案不存在，`FromFile` 會拋出 `FileNotFoundException`。如果在執行時可能缺少檔案，請將呼叫包在 try/catch 中。

## 步驟 4：取得並顯示辨識文字

最後，當引擎完成後，你可以透過 `Text` 屬性取得純文字結果。將其印到主控台足以作為快速示範，但亦可寫入資料庫或文字檔案。

```csharp
        // Step 4 – output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**預期輸出**

```
=== OCR Result ===
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
```

實際內容會依你輸入的圖像而異，但你應該會看到一段格式良好的文字，而非亂碼。

![顯示 OCR 流程圖 – 執行 OCR on Image、前處理、載入、辨識](/images/ocr-pipeline.png "run OCR on image 流程圖")

### 為何每個步驟都重要

| Step | Purpose | What Happens If Skipped |
|------|---------|--------------------------|
| **Create engine** | 初始化內部結構 | 沒有可用的辨識器 – 會拋出 `NullReferenceException`。 |
| **Add filters** | 透過校正旋轉與雜訊提升準確度 | 傾斜或雜訊的影像會產生亂碼輸出。 |
| **Load image** | 為引擎提供原始位圖 | 引擎無資料可處理，導致 `Text` 欄位為空。 |
| **Read result** | 取得純文字字串以供後續使用 | 雖然已執行 OCR，卻看不到結果 – 沒什麼用。 |

## 常見變化與流程調整方式

### 更換語言套件

Aspose OCR 內建支援多種語言。如果需要 **run OCR on image** 檔案中包含例如法文或德文文字，請在呼叫 `Recognize` 前設定 `Language` 屬性。

```csharp
ocrEngine.Language = OcrLanguage.French;
```

### 處理多頁 PDF

如果來源是多頁 PDF 而非單一 JPEG，你可以先將每頁轉換為影像（使用 Aspose.PDF），再將每張影像送入相同的流程。對頁面進行迴圈相當簡單：

```csharp
foreach (var pageImage in pdfPagesAsImages)
{
    var result = ocrEngine.Recognize(ImageStream.FromMemory(pageImage));
    Console.WriteLine(result.Text);
}
```

### 處理大型檔案

處理高解析度圖片時，記憶體使用量可能會激增。請考慮在 **load image for OCR** 前先對影像進行降採樣：

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

var loadOptions = new JpegLoadOptions { Width = 1024, Height = 768 };
using (var img = (Image)Image.Load(imagePath, loadOptions))
{
    var stream = new MemoryStream();
    img.Save(stream, new JpegOptions());
    var ocrResult = ocrEngine.Recognize(ImageStream.FromMemory(stream.ToArray()));
}
```

## 完整、可直接執行的範例

以下是結合所有前述內容的完整程式。將其複製貼上至新的主控台專案，將 `YOUR_DIRECTORY` 替換為存放 `input.jpg` 的資料夾，然後按下 **F5**。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Add useful preprocessing filters
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });

        // 3️⃣ Load the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        try
        {
            // Recognize text – this is where we actually run OCR on image
            var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));

            // 4️⃣ Print the extracted text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

### 驗證結果

1. 執行程式。  
2. 檢查主控台 – 你應該會看到 `input.jpg` 上的文字。  
3. 若輸出看起來亂碼，請嘗試調整 `DenoiseGaussianFilter` 的 `Sigma` 值，或加入額外的過濾器，例如 `ContrastEnhancementFilter`。

## 重點回顧與後續步驟

我們剛剛介紹了如何使用 Aspose OCR **run OCR on image** 檔案，從設定引擎到產出乾淨、可讀的文字。主要重點如下：

- 建立 `OcrEngine` 實例。  
- 使用 `DeskewFilter` 與 `DenoiseGaussianFilter` 等過濾器 **preprocess image for OCR**。  
- 使用 `ImageStream.FromFile` **load image for OCR**。  
- 呼叫 `Recognize` 並讀取 `ocrResult.Text` 以 **extract text from jpg**。

想更進一步？試試以下想法：

- **批次處理** – 讀取資料夾中的 JPEG，將每個結果輸出為單獨的 `.txt` 檔案。  
- **整合 Azure Blob Storage** – 從雲端取得影像，執行 OCR，然後將文字儲存回去。  
- **結合 NLP** – 將擷取的文字輸入語言理解模型，自動分類發票。  

隨意嘗試不同的過濾器組合、語言套件，甚至切換至 PNG 或 TIFF——只要正確 **load image for OCR**，相同的流程皆可運作。

---

如果遇到任何問題，請在下方留言或查閱 Aspose OCR 文件以取得進階設定。祝開發愉快，盡情將圖片轉換為可搜尋的文字！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}