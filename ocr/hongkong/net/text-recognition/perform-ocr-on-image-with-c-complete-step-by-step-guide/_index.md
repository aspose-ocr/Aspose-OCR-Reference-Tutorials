---
category: general
date: 2026-05-21
description: 使用 C# 對圖像執行 OCR。了解如何載入圖像以進行 OCR、從 PNG 中擷取文字，以及使用簡短程式碼範例辨識圖像中的文字。
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: zh-hant
og_description: 在 C# 中快速執行影像 OCR。本指南示範如何載入影像進行 OCR、從 PNG 提取文字，以及以版面感知的 HTML 輸出辨識影像文字。
og_title: 使用 C# 於圖片執行 OCR – 完整程式教學
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: 使用 C# 對圖像執行 OCR – 完整逐步指南
url: /zh-hant/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中對圖像執行 OCR – 完整逐步指南

有沒有想過如何在不使用笨重 GUI 的情況下 **對圖像執行 OCR**？你並不是唯一有此需求的人。無論是數位化收據、從掃描表單中提取資料，或只是需要將 PNG 轉換為可搜尋的文字，幾行 C# 程式碼就能完成工作。

在本教學中，我們將逐步說明如何載入圖像以進行 OCR、從圖像辨識文字，最後將 PNG 中的文字提取為乾淨的 HTML。完成後，你將擁有一個可直接執行的主控台應用程式，能 **對圖像執行 OCR** 並保留原始版面配置。

## 你將建立的內容

- 一個最小化的主控台程式，讀取 PNG（或任何支援的圖像）  
- 使用 OCR 引擎 **從圖像辨識文字**  
- 將結果儲存為具版面感知的 HTML，並嵌入原始圖片  
- 示範如何 **載入圖像以進行 OCR**、**從 PNG 提取文字**，以及處理常見的邊緣案例  

> **先決條件**  
> - .NET 6.0 SDK 或更新版本（亦可目標 .NET Framework 4.7+）  
> - 相容於 NuGet 的 OCR 函式庫 – 範例使用 *Aspose.OCR*，但任何具類似 API 的函式庫皆可使用  
> - 基本的 C# 知識（不需高階技巧）  

都有了嗎？太好了——讓我們開始吧。

## 執行圖像 OCR – 完整程式碼說明

以下是 **完整、可執行** 的程式。將它複製貼上到新建的主控台專案 (`dotnet new console`) 並按 **F5**。

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **預期輸出**  
> ```
> HTML with layout saved.
> ```  
> 執行完畢後，你會在 PNG 同目錄下找到 `form.html`。在瀏覽器開啟它，你會看到相同的版面配置，但文字現在可以選取與搜尋。

### 載入圖像以進行 OCR

程式碼 `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` 就是我們 **載入圖像以進行 OCR** 的地方。`ImageStream` 輔助類別抽象化了檔案格式細節，讓你可以直接使用 JPEG、BMP 或 TIFF 而不需更改程式碼。  

**為什麼不直接傳入 `Bitmap`？**  
因為許多 OCR SDK 期待一個同時包含 DPI 中繼資料的串流。使用函式庫內建的載入器可確保引擎看到的圖像與螢幕上顯示的完全相同，從而提升辨識準確度。

#### 專業提示  
如果你在處理一批檔案，請將載入步驟包在 `try/catch` 中，並記錄任何 `FileNotFoundException`。這樣可避免因單一遺失檔案導致整批作業崩潰。

### 從 PNG 提取文字

當 `engine.Recognize()` 完成後，OCR 引擎會在內部保存已辨識的文字。若只需要原始文字，可將其取出為字串：

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

這是 **從 PNG 提取文字** 的最快方法，當你不在乎版面時。對於大多數資料輸入工作，純文字已足夠——若要匯入 CSV，請記得去除換行符號。

### 從圖像辨識文字

`Recognize()` 呼叫負責所有繁重工作。引擎在底層會：

1. 正規化圖像（校正傾斜、去除雜訊）  
2. 將圖像切割成行與字  
3. 執行訓練自數百萬字形的神經網路分類器  

因為我們設定 `Language = OcrLanguage.English`，引擎會套用英語專屬的字典，顯著降低誤判。若需要多語言支援，只需傳入語言陣列：

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### 處理具版面感知的 HTML 輸出

大多數開發者只停留在純文字，但我們使用的 `HtmlSaveOptions` 讓你 **對圖像執行 OCR** 並保留視覺結構。兩個旗標很重要：

- `PreserveLayout = true` – 保留欄位、表格與間距。  
- `EmbedImages = true` – 以 Base64 編碼的 `<img>` 元素插入原始 PNG，使 HTML 自包含。

如果你想要較輕量的檔案，將 `EmbedImages = false`，HTML 會改為參照磁碟上的原始 PNG。

#### 邊緣案例：大型檔案  
對於大於 5 MB 的圖像，嵌入會使 HTML 大幅膨脹。此時請改用外部圖像參照，並考慮先使用 `ImageProcessor.Compress` 壓縮 PNG。

## 常見陷阱與專業提示

| 症狀 | 可能原因 | 解決方式 |
|--------|--------------|-----|
| 文字亂碼 | 語言設定錯誤或缺少語言套件 | 安裝相應的語言資料檔案，並正確設定 `engine.Language` |
| 輸出無文字 | 圖像過暗或解析度過低 | 使用 `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` 進行前處理 |
| HTML 版面錯亂 | `PreserveLayout` 保持預設的 `false` | 在 `HtmlSaveOptions` 中設定 `PreserveLayout = true` |
| 大量頁面處理緩慢 | 每個檔案都重新初始化引擎 | 重複使用同一個 `OcrEngine` 實例，僅在每次迴圈中更換 `engine.Image` |

### 擴展至多檔案處理

如果你需要在資料夾中 **對圖像執行 OCR**，可將核心邏輯包在簡單的迴圈中：

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

請注意，我們在迴圈內 **載入圖像以進行 OCR**，但保留相同的 `engine` 與 `htmlOptions` 物件。這樣可減少記憶體開銷並加速批次作業。

## 更進一步：匯出為 PDF 或 DOCX

相同的 `engine` 也能儲存為其他格式：

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

如果下游系統需要可搜尋的 PDF，這只需要一行程式碼即可完成——不必另寫轉換管線。

## 結論

我們剛剛示範了如何使用 C# **對圖像執行 OCR**，從載入圖片到 **從 PNG 提取文字**，最後 **從圖像辨識文字** 成為具版面感知的 HTML 檔案。完整範例已可直接執行，現在你了解每個步驟的意義、如何針對不同語言微調，以及需要留意的陷阱。

接下來，試著將英語語系換成其他語系，或將 `PreserveLayout = false` 以產生更精簡的 HTML，甚至把純文字輸出導入資料庫以建立可搜尋的檔案庫。只要結合穩定的 OCR 引擎與幾行 C# 程式碼，可能性無限。

對於多頁 TIFF 的處理有疑問，或想了解如何將此功能整合到 ASP.NET Core API 中？在下方留言，我們一起討論，祝開發愉快！

## 相關教學

- [使用 Aspose.OCR 進行語言選擇的 C# 圖像文字提取](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [透過在 OCR 中準備矩形來提取圖像文字的方法](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [提取圖像文字 – 使用 Aspose.OCR 辨識行](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}