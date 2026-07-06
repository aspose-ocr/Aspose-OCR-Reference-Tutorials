---
category: general
date: 2026-02-11
description: 在 C# 中從阿拉伯語影像建立可搜尋的 PDF。學習如何將影像轉換為 PDF、擷取阿拉伯文字，並使用 Aspose OCR 加入隱藏文字。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract arabic text
- pdf with hidden text
- ocr arabic image
language: zh-hant
og_description: 使用 Aspose OCR 於 C# 從阿拉伯語圖像建立可搜尋 PDF。請依照本指南將圖像轉換為 PDF、擷取阿拉伯文字，並嵌入隱藏文字。
og_title: 從阿拉伯文字圖像建立可搜尋 PDF – 步驟說明
tags:
- Aspose
- OCR
- PDF
- C#
- Arabic
title: 從阿拉伯文字圖像建立可搜尋 PDF – 完整指南
url: /zh-hant/net/text-recognition/create-searchable-pdf-from-arabic-image-complete-guide/
---

extract" appears truncated. Keep as is? The original ends with "extract". We'll keep same.

Then closing shortcodes.

Now produce final content.

Make sure to keep markdown formatting.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從阿拉伯語圖像建立可搜尋 PDF – 完整指南

是否曾需要 **建立可搜尋 PDF**，但不確定如何在保留原始外觀的同時讓文字可被選取？您並不孤單。在許多文件自動化專案中，挑戰不僅是將圖像轉成 PDF，還要保留視覺版面，並加入搜尋引擎可索引的隱藏文字層。

在本教學中，我們將完整說明整個流程：**將圖像轉成 PDF**、使用 Aspose OCR **擷取阿拉伯文字**，最後將文字嵌入成 **含隱藏文字的 PDF**，使產生的檔案完全可搜尋。完成後，您將擁有一段可直接放入任何 .NET 解決方案的 C# 程式碼片段。無需外部服務，只需您已擁有的 Aspose 套件。

## 您需要的條件

- .NET 6 或更新版本（此程式碼亦適用於 .NET Core）  
- **Aspose.OCR** 與 **Aspose.Pdf** NuGet 套件（截至 2026 年 2 月的最新版本）  
- 一個阿拉伯語圖像檔（例如 `arabic_invoice.jpg`），您想將其轉成可搜尋 PDF  
- 基本的 C# 知識 – 概念相當直接，我們會說明每行程式碼背後的「為什麼」。

> **Pro tip:** 若尚未加入 NuGet 套件，請在專案資料夾執行  
> `dotnet add package Aspose.OCR` 和  
> `dotnet add package Aspose.Pdf`。

現在前置作業已完成，讓我們深入一步步實作。

## Step 1 – 設定阿拉伯文字的 OCR 引擎

首先必須設定 Aspose OCR 以辨識阿拉伯字元。阿拉伯文屬右至左書寫系統，我們必須告訴引擎載入相應語言，並啟用自動資源下載，以防機器上尚未安裝語言資料。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Configure OCR for Arabic and let Aspose fetch the language pack if needed
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Arabic,
    AutomaticResourceDownload = true
};
```

**為何這很重要：**  
若省略 `Language = OcrLanguage.Arabic` 設定，引擎會預設使用英文，結果會出現亂碼。啟用 `AutomaticResourceDownload` 可免除手動放置語言檔案的步驟。

## Step 2 – 載入來源圖像

接著載入含有阿拉伯文字的圖像。使用 `Image.FromFile` 可將圖像讀入 GDI+ 的 `Image` 物件，這是 Aspose OCR 所期待的格式。

```csharp
using System.Drawing;          // For Image
using System.IO;                // For MemoryStream

// Replace with the actual path to your Arabic invoice
string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";

using (var inputImage = Image.FromFile(imagePath))
{
    // The rest of the workflow lives inside this using block
```

**Edge case（邊緣情況）：** 若圖像尺寸過大（例如掃描的 A3 頁），建議先縮小尺寸以提升效能。OCR 引擎雖能處理大型檔案，但記憶體使用會快速飆升。

## Step 3 – 辨識阿拉伯文字並取得結果

現在正式執行 OCR。`Recognize` 方法會回傳一個 `OcrResult` 物件，內含偵測到的文字、信心分數以及邊界框（若您需要進階版面分析時會用到）。

```csharp
    // Perform OCR on the loaded image
    OcrResult ocrResult = ocrEngine.Recognize(inputImage);
    string extractedText = ocrResult.Text;

    // Quick sanity check: print the first 200 characters to the console
    Console.WriteLine("Extracted Arabic text (preview):");
    Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**為何保留預覽？**  
先看一小段擷取出的文字，可確認語言包是否正確載入，避免在產生 PDF 前浪費時間。

## Step 4 – 建立新 PDF 文件並新增空白頁

取得文字後，我們即可開始組裝 PDF。Aspose PDF 提供 `Document` 物件代表整個檔案。新增頁面則提供一個畫布，讓我們同時放置原始圖像與隱藏文字層。

```csharp
    // Initialize a new PDF document
    var pdfDocument = new Aspose.Pdf.Document();

    // Add a blank page – this will become the background for our image
    var pdfPage = pdfDocument.Pages.Add();
```

**Note（註）：** 若處理多頁 TIFF 或 PDF，可加入多個頁面；但對於單一圖像的情境，一頁即可。

## Step 5 – 將原始圖像作為背景元素插入

我們希望最終的 PDF 與掃描的發票外觀完全相同，因此將圖像作為可見背景嵌入。Aspose PDF 的 `Image` 類別需要串流，因此先將檔案讀入 `MemoryStream`。

```csharp
    // Load the same image bytes for the PDF background
    var backgroundImage = new Aspose.Pdf.Image
    {
        ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
    };

    // Add the image to the page's paragraph collection
    pdfPage.Paragraphs.Add(backgroundImage);
```

**為何使用背景圖像？**  
直接將圖像放在頁面上，可保留原始版面、顏色以及任何印章或商標，這些資訊若只靠 OCR 會被忽略。

## Step 6 – 將 OCR 文字加入隱藏層

製作 **可搜尋 PDF** 的關鍵在於將文字層隱藏於圖像之上。將字型大小設為 `0`，即可讓文字對人眼不可見，同時仍可被選取與搜尋。

```csharp
    // Create a TextFragment with the extracted Arabic text
    var searchableText = new Aspose.Pdf.Text.TextFragment(extractedText)
    {
        // Hide the visible text; only the text layer remains searchable
        TextState = { FontSize = 0 }
    };

    // Add the hidden text fragment to the same page
    pdfPage.Paragraphs.Add(searchableText);
```

**Important nuance（重要細節）：**  
若需要文字與圖像完美對齊（例如 OCR 回傳座標時），可使用 `TextFragmentAbsorber` 手動定位每個文字片段。對大多數發票而言，整頁覆蓋的簡易做法已足夠。

## Step 7 – 儲存可搜尋的 PDF

最後將 PDF 寫入磁碟。輸出檔案同時包含視覺圖像與隱藏的阿拉伯文字，讓 Adobe Reader、Google Drive 或任何支援 OCR 的檢視器皆能完整搜尋。

```csharp
    // Define the output path
    string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";

    // Save the document
    pdfDocument.Save(outputPath);

    Console.WriteLine($"Searchable PDF created at: {outputPath}");
}
```

### 完整可執行範例

將所有步驟整合，以下是完整、可直接執行的程式碼：

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR for Arabic
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Arabic,
            AutomaticResourceDownload = true
        };

        // 2️⃣ Load the source image
        string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";
        using (var inputImage = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR and get the text
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);
            string extractedText = ocrResult.Text;

            // Optional preview
            Console.WriteLine("Extracted Arabic text (preview):");
            Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));

            // 4️⃣ Create PDF document
            var pdfDocument = new Document();
            var pdfPage = pdfDocument.Pages.Add();

            // 5️⃣ Add original image as background
            var backgroundImage = new Aspose.Pdf.Image
            {
                ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
            };
            pdfPage.Paragraphs.Add(backgroundImage);

            // 6️⃣ Add hidden searchable text
            var searchableText = new TextFragment(extractedText)
            {
                TextState = { FontSize = 0 }
            };
            pdfPage.Paragraphs.Add(searchableText);

            // 7️⃣ Save the searchable PDF
            string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";
            pdfDocument.Save(outputPath);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Expected result（預期結果）：** 開啟產生的 `arabic_invoice_searchable.pdf`，在任何 PDF 檢視器中按 **Ctrl + F**，輸入原始發票上出現的阿拉伯文字。即使看不到文字層，檢視器仍能定位該詞。

## 常見問題與注意事項

- **這能套用於其他語言嗎？**  
  當然可以。只要將 `Language = OcrLanguage.YourLanguage` 改成目標語言，並確保相應語言包已安裝。其餘流程保持不變。

- **如果 OCR 信心分數太低該怎麼辦？**  
  您可以檢查 `ocrResult.Confidence`（介於 0~1 之間）。若低於某個門檻（例如 0.75），建議先對圖像做前處理——校正傾斜、提升對比度或轉成灰階，再送入引擎。

- **可以在同一個 PDF 中加入多張圖像嗎？**  
  可以。遍歷圖像路徑集合，為每張圖像新增一頁，然後重複第 5‑6 步。記得為每張圖像保留 `using` 區塊，以釋放 GDI 資源。

- **隱藏文字真的完全看不見嗎？**  
  設定 `FontSize = 0` 在大多數檢視器中會讓文字不可見。若仍出現淡淡的字形，可再將文字顏色設為全透明 (`TextState.FillColor = Color.Transparent`)。

## 後續步驟

了解如何 **建立可搜尋 PDF** 後，您可以進一步探索：

- **批次處理** – 讀取資料夾內所有圖像，為每個檔案產生單一可搜尋 PDF。  
- **加入 OCR 座標** – 使用 `OcrResult.Regions` 精確定位每段文字，提升複雜版面的搜尋準確度。  
- **加密 PDF** – Aspose PDF 可為檔案設定密碼或數位簽章，提供額外安全性。  
- **整合 Azure Blob Storage** – 直接將產生的 PDF 存入雲端，供後續工作流程使用。

每個主題都自然牽涉到次要關鍵字 **convert image to pdf**, **extract

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}