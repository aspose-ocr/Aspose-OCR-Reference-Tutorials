---
category: general
date: 2026-03-13
description: 使用 Aspose OCR 從任何圖片建立可搜尋的 PDF。了解如何將圖片轉換為 EPUB、加入可搜尋文字，並在 C# 中產生可搜尋的 PDF。
draft: false
keywords:
- create searchable pdf
- convert image to epub
- ocr image to pdf
- add searchable text
- generate searchable pdf
language: zh-hant
og_description: 使用 Aspose OCR 從任何圖像建立可搜尋的 PDF。本指南示範如何將圖像轉換為 EPUB、加入可搜尋文字，並在 C# 中產生可搜尋的
  PDF。
og_title: 建立可搜尋 PDF – 將圖片轉換為 EPUB 並加入文字
tags:
- Aspose OCR
- C#
- PDF
- EPUB
title: 製作可搜尋的 PDF – 將圖片轉換成 EPUB 並加入文字
url: /zh-hant/net/text-recognition/create-searchable-pdf-convert-image-to-epub-add-text/
---

PDF，並檢視 **檔案 → 屬性 → 說明**，會在 **字型** 分頁下看到隱藏的文字串流，證實可搜尋層已存在。"

## Common Questions & Edge Cases

"Common Questions & Edge Cases" -> "常見問題與特殊情況"

**Q: Does this work with non‑English languages?** -> "**問：此方法能支援非英語語言嗎？**"

Then closing shortcodes.

Now ensure we keep all shortcodes unchanged.

Also ensure we keep code block placeholders.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立可搜尋 PDF – 將影像轉換為 EPUB 並加入文字

想要從掃描的收據或任何影像**建立可搜尋的 PDF**嗎？在本教學中，我們將示範如何使用 Aspose OCR 建立可搜尋的 PDF，同時**將影像轉換為 EPUB**以及**加入可搜尋文字**層——全部在一個 C# 專案中完成。  

如果你曾經為了無法搜尋的 PDF 而苦惱，你並不孤單。好消息是，隱藏的文字層可以將平面影像轉變為完整可搜尋的文件，而 Aspose 讓這個過程幾乎毫不費力。

## 你將學會

* 如何初始化 Aspose OCR 引擎並設定語言。  
* 將影像**轉換為 EPUB**以供電子書發行的完整步驟。  
* 如何設定 PDF 寫入器，使輸出包含隱藏且可搜尋的文字層。  
* 處理特殊情況的技巧，例如多頁收據或非英語語言。  

在此之前，你只需要一個 .NET 開發環境（Visual Studio 2022 或更新版本）以及 Aspose OCR NuGet 套件。無需外部服務，無需複雜的設定檔——只要純粹的 C# 程式碼，你可以直接複製貼上並執行。

## 前置條件

| 必要條件 | 為何重要 |
|-------------|----------------|
| .NET 6.0+   | Aspose OCR 目標為 .NET Standard 2.0+，因此 .NET 6 可提供最新的執行時改進。 |
| Aspose.OCR NuGet 套件 | 提供 `OcrEngine`、`EpubWriter` 與 `PdfWriter` 類別，供程式碼使用。 |
| 影像檔案（例如 `receipt.jpg`） | 你將對其執行 OCR 的來源。任何點陣圖（PNG、JPEG、BMP）皆可。 |
| 基本的 C# 知識 | 你只需要閱讀與微調程式碼片段，無需從頭學習語言。 |

你可以使用以下指令安裝套件：

```bash
dotnet add package Aspose.OCR
```

> **專業提示：**如果你使用 Visual Studio，NuGet 套件管理員 UI 也能完成相同的工作——只要搜尋「Aspose.OCR」。

## 步驟 1 – 使用 Aspose OCR 建立可搜尋 PDF

我們首先需要一個能辨識語言的 `OcrEngine` 實例。預設為英文，但你可以透過設定 `ocrEngine.Language` 來改為法文、德文等其他語言。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialise the OCR engine and set the language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English          // Change this if your document isn’t English
};
```

為什麼要先初始化引擎？引擎會在記憶體中保留辨識模型，若只建立一次並在多張影像間重複使用，可節省 CPU 與記憶體。在大型批次作業中，你會讓同一個實例持續運行整個流程。

## 步驟 2 – 載入影像並執行 OCR

接著我們將引擎指向要處理的檔案。`ImageStream.FromFile` 會將影像讀取成 OCR 引擎能理解的格式。

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Run the recognition engine – this populates the internal text buffer
ocrEngine.Recognize();
```

> **如果影像是多頁的呢？**  
> Aspose OCR 能直接處理多頁 TIFF。只要傳入 TIFF 檔案的路徑，引擎會自動逐頁迭代。

## 步驟 3 – 將影像轉換為 EPUB

如果你同時需要掃描文件的電子書版本，Aspose 只需一行程式碼即可完成。`EpubWriter` 使用相同的 `OcrEngine` 實例，表示 OCR 結果會被直接重複使用，無需額外處理。

```csharp
// Export the recognised content to an ePub file
EpubWriter epubWriter = new EpubWriter();
epubWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt.epub");
```

為什麼要匯出為 EPUB？EPUB 是可重排的格式——非常適合行動閱讀器。OCR 文字可被選取，而原始影像則作為背景保留，維持原始掃描的外觀。

## 步驟 4 – 為 PDF 加入可搜尋文字層

現在進入實際**建立可搜尋 PDF**的部分。啟用 `AddSearchableTextLayer` 後，PDF 寫入器會嵌入一個與 OCR 輸出相同的隱形文字層。使用者可以像原生 PDF 一樣搜尋、複製或標註文字。

```csharp
// Configure PDF writer to include a hidden searchable text layer
PdfWriter pdfWriter = new PdfWriter
{
    AddSearchableTextLayer = true   // Enables the hidden text layer for searchability
};

// Save the OCR result as a searchable PDF
pdfWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt_searchable.pdf");
```

> **常見陷阱：**若忘記設定 `AddSearchableTextLayer`，產生的 PDF 看起來相同卻沒有可搜尋的文字。需要可搜尋文件時，務必再次確認此旗標。

## 步驟 5 – 完整範例

將所有步驟整合起來，以下是一個獨立的 Console 應用程式範例，你可以直接放入新的 .NET 專案並立即執行。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace OcrToPdfAndEpub
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the source image
            string imagePath = "YOUR_DIRECTORY/receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            ocrEngine.Recognize();

            // 4️⃣ Convert to EPUB (optional but handy)
            EpubWriter epubWriter = new EpubWriter();
            string epubPath = "YOUR_DIRECTORY/receipt.epub";
            epubWriter.Save(ocrEngine, epubPath);
            Console.WriteLine($"EPUB saved to {epubPath}");

            // 5️⃣ Create searchable PDF
            PdfWriter pdfWriter = new PdfWriter
            {
                AddSearchableTextLayer = true
            };
            string pdfPath = "YOUR_DIRECTORY/receipt_searchable.pdf";
            pdfWriter.Save(ocrEngine, pdfPath);
            Console.WriteLine($"Searchable PDF saved to {pdfPath}");
        }
    }
}
```

### 預期輸出

* `receipt.epub` – 可在 Calibre、Apple Books 或任何電子閱讀器中開啟的 EPUB 檔案。  
* `receipt_searchable.pdf` – 這個 PDF 讓你按 **Ctrl + F** 即可搜尋原始影像中出現的任何文字。

如果你在 Adobe Acrobat 中開啟 PDF，並檢視 **檔案 → 屬性 → 說明**，會在 **字型** 分頁下看到隱藏的文字串流，證實可搜尋層已存在。

## 常見問題與特殊情況

**問：此方法能支援非英語語言嗎？**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}