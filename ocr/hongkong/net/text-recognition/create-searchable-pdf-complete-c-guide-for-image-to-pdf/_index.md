---
category: general
date: 2026-04-08
description: 快速建立可搜尋的 PDF，並學習如何壓縮 PDF 圖片、嵌入字型以及在 C# 中使用 Aspose.OCR 進行文字影像辨識。
draft: false
keywords:
- create searchable pdf
- compress pdf images
- embed fonts pdf
- image to searchable pdf
- recognize text image
language: zh-hant
og_description: 使用 Aspose.OCR 快速建立可搜尋 PDF，於單一教學中學習壓縮 PDF 圖像、嵌入字型至 PDF 以及辨識文字圖像。
og_title: 建立可搜尋的 PDF – 完整 C# 指南
tags:
- Aspose.OCR
- C#
- PDF Generation
title: 製作可搜尋 PDF – 完整 C# 圖片轉 PDF 指南
url: /zh-hant/net/text-recognition/create-searchable-pdf-complete-c-guide-for-image-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立可搜尋的 PDF – 完整 C# 指南

需要從掃描圖像**建立可搜尋的 PDF**嗎？你並不是唯一一個盯著巨大的 PNG 想把它變成輕量、可文字搜尋文件的人。好消息是，使用 Aspose.OCR 只需幾行程式碼即可完成，同時你還會學會如何**壓縮 PDF 圖像**、**嵌入 PDF 字型**以及**辨識文字圖像**，毫不費力。

在本教學中，我們將逐步說明整個流程：從載入圖像、執行 OCR、調整 PDF 儲存選項，到最終將可搜尋的 PDF 寫入磁碟。完成後，你將擁有一個可直接套用於任何 .NET 專案的方法，並附上一些針對未來可能遇到的特殊情況的專業技巧。

## 需要的條件

- **.NET 6+**（此程式碼同樣適用於 .NET Framework 4.7，但我們將以 .NET 6 為目標以使用現代語法）。
- **Aspose.OCR for .NET** – 透過 NuGet 安裝：`Install-Package Aspose.OCR`。
- 一個包含欲轉為可搜尋文字之內容的圖像檔（PNG、JPEG、TIFF）。
- 適度的好奇心——其餘內容在下方說明。

> **專業提示：** 若你計畫處理數十頁圖像，建議重複使用同一個 `OcrEngine` 實例，以避免重複載入語言資料所產生的額外負擔。

## 步驟 1：設定 OCR 引擎 – 辨識文字圖像

我們首先需要一個能從來源位圖讀取字元的 OCR 引擎。Aspose.OCR 允許你指定語言（英語、法語等），並回傳包含原始文字與圖像資料的 `OcrResult` 物件。

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

public static OcrResult LoadAndRecognize(string imagePath)
{
    // Initialize the OCR engine – “en” is the ISO code for English.
    var ocrEngine = new OcrEngine { Language = "en" };

    // Recognize the image and get the result.
    OcrResult result = ocrEngine.RecognizeImage(imagePath);

    // Quick sanity check – throw if nothing was detected.
    if (string.IsNullOrWhiteSpace(result.Text))
        throw new InvalidOperationException("No text was recognized in the image.");

    return result;
}
```

**為什麼這很重要：**
- 設定語言可大幅提升辨識準確度；引擎會在背景載入特定語言的字典。
- `OcrResult` 不僅保存擷取的字串，還包含底層位圖，我們稍後會將其嵌入 PDF，使文件在視覺上與原始掃描保持一致。

## 步驟 2：設定 PDF 儲存選項 – 壓縮 PDF 圖像與嵌入字型

可搜尋的 PDF 本質上是普通 PDF，於掃描圖像上方疊加一層隱形文字層。若忽略壓縮，最終檔案可能會非常龐大。`PdfSaveOptions` 類別提供對圖像品質、字型嵌入以及是否子集化字型的精細控制。

```csharp
public static PdfSaveOptions GetPdfSaveOptions()
{
    return new PdfSaveOptions
    {
        // Reduce file size by compressing the raster image.
        CompressImages = true,

        // ImageQuality ranges from 0 (worst) to 100 (best). 75 is a good balance.
        ImageQuality = 75,

        // Embedding fonts ensures the text layer looks the same on any machine.
        EmbedFonts = true,

        // Subsetting keeps only the glyphs we actually use – another size saver.
        FontSubset = true
    };
}
```

**為什麼要嵌入 PDF 字型：**
當 PDF 在缺少 OCR 層所使用的精確字型的系統上開啟時，文字可能會顯示為亂碼。嵌入字型可確保跨平台的視覺一致性，這對於法律或檔案保存的文件尤為重要。

## 步驟 3：將結果儲存為可搜尋的 PDF – 圖像轉可搜尋 PDF

現在把所有步驟結合起來：取得 `OcrResult`、套用我們的 `PdfSaveOptions`，然後寫入檔案。`SaveAsSearchablePdf` 方法負責主要工作——建立一個隱形文字覆蓋層，與 OCR 輸出相對應，同時保留原始圖像。

```csharp
public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
{
    // Step 1: Recognize the image.
    OcrResult ocrResult = LoadAndRecognize(inputImage);

    // Step 2: Prepare PDF options.
    PdfSaveOptions pdfOptions = GetPdfSaveOptions();

    // Step 3: Write the searchable PDF.
    ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);

    Console.WriteLine($"Searchable PDF created at: {outputPdf}");
}
```

### 完整範例程式

以下是一個獨立的主控台程式範例，你可以直接複製貼上到新的 .NET 主控台專案中。程式假設圖像位於相對於執行檔的 `YOUR_DIRECTORY` 資料夾內。

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

class Program
{
    static void Main()
    {
        string inputPath = "YOUR_DIRECTORY/input.png";
        string outputPath = "YOUR_DIRECTORY/output.pdf";

        try
        {
            CreateCompressedSearchablePdf(inputPath, outputPath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // --- Methods from the previous steps -------------------------------------------------
    public static OcrResult LoadAndRecognize(string imagePath)
    {
        var ocrEngine = new OcrEngine { Language = "en" };
        OcrResult result = ocrEngine.RecognizeImage(imagePath);
        if (string.IsNullOrWhiteSpace(result.Text))
            throw new InvalidOperationException("OCR did not detect any text.");
        return result;
    }

    public static PdfSaveOptions GetPdfSaveOptions()
    {
        return new PdfSaveOptions
        {
            CompressImages = true,
            ImageQuality = 75,
            EmbedFonts = true,
            FontSubset = true
        };
    }

    public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
    {
        OcrResult ocrResult = LoadAndRecognize(inputImage);
        PdfSaveOptions pdfOptions = GetPdfSaveOptions();
        ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);
        Console.WriteLine("Searchable PDF created.");
    }
}
```

執行程式後會產生 `output.pdf`，你可以在 Adobe Reader、Foxit 或任何 PDF 檢視器中開啟，並立即搜尋原本僅存在於圖像中的文字。

## 步驟 4：驗證輸出 – 搜尋功能是否正常？

檔案產生後，開啟它並使用內建搜尋功能（Ctrl + F）。若能找到如「invoice」、「date」或「total」等詞彙，即表示你已成功建立**可搜尋的 PDF**。

如果搜尋沒有結果：

1. **檢查 OCR 準確度**——可能來源圖像解析度過低。考慮在 OCR 前提升 DPI（Aspose 可在引擎上設定 `Resolution`）。
2. **確認字型已嵌入**——開啟 PDF 屬性，檢查 *Fonts* 項目，應能看到已嵌入的字型。
3. **檢查圖像壓縮**——過低的 `ImageQuality` 可能導致視覺層無法辨識，進而影響後續工具的處理。

## 常見變化與邊緣情況

| Scenario | What to Adjust | Why |
|----------|----------------|-----|
| **多頁 TIFF** | 對每個影格迴圈，對每頁呼叫 `RecognizeImage`，然後使用 `PdfSaveOptions` 並設定 `AppendMode = true`。 | 確保每個掃描頁面皆為獨立的可搜尋頁面。 |
| **非英語語系** | 將 `Language = "fr"`（或其他適當的 ISO 代碼）改為目標語言，並可選擇提供自訂字典。 | 提升對帶重音字元與語系特有字形的辨識率。 |
| **非常大的圖像** | 在 OCR 前縮小位圖（`ocrEngine.Image = Image.FromFile(...).GetThumbnailImage(...)`）。 | 降低記憶體使用量並加速 OCR，且不會大幅犧牲準確度。 |
| **需要 OCR 信心分數** | 存取 `ocrResult.RecognizedWords` 並檢查 `Confidence` 屬性。 | 讓你能標記信心分數低的字詞以供人工審核。 |

## 效能技巧

- **重複使用 `OcrEngine`** 於批次處理檔案時——它會快取語言資料。
- **平行化** 辨識步驟（使用 `Parallel.ForEach`），若在多核心機器上執行，但 PDF 寫入需保持順序，以避免檔案存取衝突。
- **調整 `ImageQuality`**：85‑90 可提供近乎無損的圖像，60‑70 則通常足以應付文字密集的文件。

## 結論

我們已說明如何使用 Aspose.OCR 從圖像**建立可搜尋的 PDF**檔案，同時學會**壓縮 PDF 圖像**、**嵌入 PDF 字型**以及高效**辨識文字圖像**。完整程式碼範例已可直接套用於任何 C# 專案，額外的技巧則有助於你將此解決方案擴展至更大工作負載或不同語言。

準備好進一步了嗎？試著加入浮水印、合併多個可搜尋的 PDF，或將此流程整合至 Web API，讓使用者上傳掃描檔後即時取得可搜尋的 PDF。可能性無窮，只要掌握了基礎，你就能輕鬆擴充工作流程。

祝程式開發順利，願你的 PDF 保持小巧、可搜尋且完美呈現！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}