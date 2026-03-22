---
category: general
date: 2026-03-21
description: c# OCR 教學：學習如何從圖片中提取文字、掃描發票，並在 c# 中使用 Aspose OCR 及 GPU 加速載入圖片。
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- ocr invoice scanning
- how to ocr image
- load image in c#
language: zh-hant
og_description: C# OCR 教學：逐步指南，從圖像提取文字、執行 OCR 發票掃描，並學習如何在 C# 中使用 GPU 加速進行圖像 OCR。
og_title: c# OCR 教學 – 使用 Aspose OCR 從圖像提取文字
tags:
- OCR
- C#
- Image Processing
title: C# OCR 教學 – 使用 Aspose OCR 從圖像提取文字
url: /zh-hant/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教學 – 使用 Aspose OCR 從影像中擷取文字

有沒有想過如何以 **c# OCR 教學** 的方式解決像是將掃描發票轉換成可編輯文字的實際問題？你並不孤單。許多開發者在需要 *從影像中擷取文字* 時會卡住，最終寫出脆弱的解析器，一遇到有雜訊的掃描檔就會失效。

事實上——Aspose.OCR 讓整個流程變得輕而易舉，尤其在啟用 GPU 加速時更是如此。在本指南中，你將會看到如何在 C# 中 **如何對影像進行 OCR**、正確地在 C# 中載入影像，甚至在不抓狂的情況下處理常見的發票掃描怪癖。

完成本教學後，你將擁有一個可執行的主控台應用程式，能讀取 TIFF 發票、在 GPU 上執行 OCR，並輸出乾淨的純文字。沒有魔法，只有你可以直接複製貼上並調整的實用程式碼。

---

## 需要的環境

- **.NET 6.0**（或更新版本）– 目前的 LTS 版，確保未來相容。
- **Aspose.OCR for .NET** NuGet 套件 – 版本 23.10（撰寫時的最新版本）。
- **支援 GPU 的機器**（可選，但建議使用）– 若未偵測到相容的 GPU，程式會自動回退至 CPU。
- 範例影像，例如 `large_invoice.tif`。任何支援的格式（PNG、JPEG、TIFF、PDF）皆可使用。

如果尚未安裝 NuGet 套件，請執行：

```bash
dotnet add package Aspose.OCR
```

既然已完成前置作業，讓我們深入實作步驟。

## 步驟 1：建立新的主控台專案並加入 Aspose.OCR

首先，建立一個全新的主控台應用程式，以保持教學的獨立性。

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
dotnet add package Aspose.OCR
```

> **小技巧：** 使用 `-n` 參數為專案命名，使其具備意義；當你之後加入更多模組時，解決方案會保持整潔。

`Program.cs` 檔案是 Visual Studio 產生的，我們將把它當作練習場。開啟後，移除預設的 `Console.WriteLine` 行——我們會以 OCR 邏輯取代它。

## 步驟 2：在 C# 中載入影像 – 正確做法

載入影像看似簡單，但若處理不當會導致記憶體泄漏或檔案被鎖定。`System.Drawing.Image` 類別在大多數情況下都能正常使用，但必須將其包在 `using` 區塊中以確保釋放。

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 2: Load the image you want to OCR.
            // Replace the path with the actual location of your invoice file.
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // The using statement ensures the image gets disposed automatically.
            using var inputImage = Image.FromFile(imagePath);
            
            // Continue to the OCR engine setup…
        }
    }
}
```

留意註解 `// 👉 Step 2:` —— 它對應本教學的步驟編號，方便日後閱讀程式碼的人快速定位。

## 步驟 3：使用 GPU 加速初始化 OCR 引擎

Aspose.OCR 允許你在建構時選擇處理模式。`OcrEngineMode.Gpu` 會在偵測到顯示卡時使用 GPU；若未偵測到，則會靜默回退至 CPU，無需自行撰寫額外的回退邏輯。

```csharp
// 👉 Step 3: Create the OCR engine.
// The constructor argument selects GPU mode; it's the fastest option for large invoices.
var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);
```

> **為什麼使用 GPU？**  
> 高解析度發票的 OCR 會消耗大量 CPU。將運算交給 GPU 可將執行時間從數秒縮短至毫秒級，特別是在批次處理時更為顯著。

## 步驟 4：執行 OCR 並從影像擷取文字

現在魔法發生了。呼叫 `Recognize` 取得純文字。Aspose 會回傳一個 `OcrResult` 物件，內含原始文字、信心分數，甚至每個字元的邊界框，若之後需要可自行使用。

```csharp
// 👉 Step 4: Perform the OCR operation.
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Display the extracted text.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

執行程式後，你應該會看到類似以下的輸出：

```
=== OCR Output ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

若輸出呈現雜亂，請再次確認影像具備高對比度，且 OCR 語言設定正確（預設為英文）。你也可以微調 `ocrEngine.Settings` 以提升準確度，但預設設定已足以應付大多數列印發票。

## 步驟 5：處理 OCR 發票掃描的邊緣案例

發票形態多樣——有些是多頁的，有些包含表格或手寫備註。以下提供幾個快速調整方式，讓你不必重寫整個流程。

### 5.1 多頁 PDF 或 TIFF

若來源檔案包含多頁，需遍歷每一頁並將結果串接起來。

```csharp
using var multiPageImage = Image.FromFile(@"C:\Invoices\multi_page_invoice.tif");

// Aspose can split multi‑page TIFFs into separate images.
for (int i = 0; i < multiPageImage.GetFrameCount(FrameDimension.Page); i++)
{
    multiPageImage.SelectActiveFrame(FrameDimension.Page, i);
    using var page = (Image)multiPageImage.Clone();
    var pageResult = ocrEngine.Recognize(page);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

### 5.2 低解析度掃描

若 DPI 低於 150，請在送入引擎前先將影像放大。這會顯著提升字元辨識率。

```csharp
// Simple nearest‑neighbor scaling – replace with a better algorithm if needed.
var highRes = new Bitmap(inputImage, new Size(inputImage.Width * 2, inputImage.Height * 2));
var highResResult = ocrEngine.Recognize(highRes);
Console.WriteLine(highResResult.Text);
```

### 5.3 自訂語言套件

預設情況下 Aspose 使用英文。若需其他語言，請從 Aspose 官方網站下載相應的語言套件並註冊：

```csharp
ocrEngine.Settings.Language = OcrLanguage.Spanish; // example for Spanish invoices
```

這些調整讓你的 **ocr invoice scanning** 解決方案足以應付正式環境的工作負載。

## 完整範例程式

以下是結合上述所有步驟的完整可執行程式。將其複製到 `Program.cs`，調整檔案路徑，然後按 **F5** 執行。

```csharp
// ---------------------------------------------------------------
// Complete c# OCR tutorial – Aspose OCR with GPU acceleration
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialize the OCR engine (GPU mode)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);

            // -----------------------------------------------------------------
            // Step 2: Load the image you want to process
            // -----------------------------------------------------------------
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // Using ensures the image is disposed properly.
            using var inputImage = Image.FromFile(imagePath);

            // -----------------------------------------------------------------
            // Step 3: Run OCR and extract plain text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);

            // -----------------------------------------------------------------
            // Step 4: Output the result
            // -----------------------------------------------------------------
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);

            // -----------------------------------------------------------------
            // Optional: Demonstrate handling a multi‑page TIFF (comment out if not needed)
            // -----------------------------------------------------------------
            // HandleMultiPageTiff(@"C:\Invoices\multi_page_invoice.tif", ocrEngine);
        }

        // ---------------------------------------------------------------
        // Helper for multi‑page TIFFs – shows how to iterate pages
        // ---------------------------------------------------------------
        static void HandleMultiPageTiff(string path, OcrEngine engine)
        {
            using var multiPage = Image.FromFile(path);
            int pageCount = multiPage.GetFrameCount(FrameDimension.Page);

            for (int i = 0; i < pageCount; i++)
            {
                multiPage.SelectActiveFrame(FrameDimension.Page, i);
                using var page = (Image)multiPage.Clone();
                var result = engine.Recognize(page);
                Console.WriteLine($"\n--- Page {i + 1} ---");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

**預期輸出**（為簡潔起見已截斷）：

```
=== OCR Output ===
Invoice #98765
Date: 02/28/2026
Bill To: Acme Corp.
Subtotal: $2,500.00
Tax (8%): $200.00
Total: $2,700.00
...
```

執行程式並確認主控台印出發票上的文字。若得到空字串，請再次確認影像路徑正確且檔案未損毀。

## 常見問題 (FAQ)

**Q: 這在 Linux 上能運作嗎？**  
A: 能。Aspose.OCR 為跨平台套件。只要在 Linux 上安裝 .NET 執行環境，即可使用相同的 NuGet 套件。GPU 加速則需要相容 CUDA 的顯示卡與相應驅動程式。

**Q: 若沒有 GPU 該怎麼辦？**  
A: `OcrEngineMode.Gpu` 建構子會在未偵測到相容 GPU 時自動回退至 CPU。仍能取得準確結果，只是會稍微慢一些。

**Q: 能否對手寫筆記進行 OCR？**  
A: Aspose 的預設模型針對印刷文字。若要辨識手寫，需要專門的模型或其他服務（例如 Azure Form Recognizer）。不過，你仍可使用相同程式碼，只是信心分數可能較低。

## 結論

你剛剛完成了一個 **c# OCR 教學**，示範了如何 *從影像中擷取文字*、執行 **ocr invoice scanning**，以及了解 **how to o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}