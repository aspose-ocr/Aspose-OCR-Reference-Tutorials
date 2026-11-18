---
category: general
date: 2026-07-05
description: 使用 Aspose.OCR 於 C# 進行影像 OCR。了解如何載入影像以執行 OCR、在 OCR 前對影像進行前處理，以及從收據中擷取文字，同時提升
  OCR 準確度。
draft: false
keywords:
- perform OCR on image
- extract text from receipt
- improve OCR accuracy
- load image for OCR
- preprocess image before OCR
language: zh-hant
og_description: 使用 Aspose.OCR 在 C# 中對圖像執行 OCR。本教學示範如何載入圖像進行 OCR、在 OCR 前對圖像進行前處理，以及從收據中提取文字，以提升
  OCR 準確度。
og_title: 使用 Aspose 於圖像執行 OCR – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Aspose.OCR in C#. Learn how to load image
    for OCR, preprocess image before OCR, and extract text from receipt while improving
    OCR accuracy.
  headline: Perform OCR on Image with Aspose – Complete C# Guide
  type: TechArticle
- description: Perform OCR on image using Aspose.OCR in C#. Learn how to load image
    for OCR, preprocess image before OCR, and extract text from receipt while improving
    OCR accuracy.
  name: Perform OCR on Image with Aspose – Complete C# Guide
  steps:
  - name: '**Load** the picture file into memory.'
    text: '**Load** the picture file into memory.'
  - name: '**Preprocess** it: deskew, denoise, and boost contrast.'
    text: '**Preprocess** it: deskew, denoise, and boost contrast.'
  - name: '**Run** the OCR engine.'
    text: '**Run** the OCR engine.'
  - name: '**Read** the resulting text.'
    text: '**Read** the resulting text.'
  type: HowTo
- questions:
  - answer: Aspose.OCR works best with printed text. For cursive or mixed fonts you
      may need a specialized handwriting model or a different library.
    question: What if the receipt is handwritten?
  - answer: Yes—convert each PDF page to an image (`Aspose.PDF` can help) and feed
      those images into the same pipeline.
    question: Can I process PDFs directly?
  - answer: Wrap the core logic inside a `foreach` loop that iterates over a folder
      of images. Remember to dispose of the `OcrEngine` after each file to free memory.
    question: Is there a way to batch‑process many receipts?
  - answer: Aspose offers a free evaluation with a watermark. For production use,
      purchase a license to remove the watermark and unlock full performance.
    question: Do I need a license?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- Image Processing
title: 使用 Aspose 於圖像執行 OCR – 完整 C# 指南
url: /zh-hant/net/ocr-optimization/perform-ocr-on-image-with-aspose-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose 執行圖像 OCR – 完整 C# 指南

有沒有曾經需要 **在圖像上執行 OCR**，但結果模糊、缺字或完全錯誤？你並不孤單——掃描收據、發票或手寫筆記常常變成猜測遊戲。在本指南中，我們將實作一個實用的方法，**載入圖像以供 OCR**、清理圖像，最後 **從收據中擷取文字**，並明顯 **提升 OCR 準確度**。

說明一下：Aspose.OCR 函式庫提供一套整潔的 API，讓你可以依需求堆疊前處理濾鏡。完成本教學後，你將擁有一個可直接執行的 C# 主控台應用程式，能讀取傾斜的收據、校正傾斜、去除背景雜訊、提升對比度，並將乾淨的文字印到主控台。沒有神祕，只要一步一步的程式碼，直接複製貼上即可。

## 您將學習

- 如何使用 Aspose 的 `ImageStream` **載入圖像以供 OCR**。
- 哪些 **在 OCR 前處理圖像** 的濾鏡對收據最有效。
- 在不購買昂貴第三方服務的情況下 **提升 OCR 準確度** 的技巧。
- 精確的 **從收據中擷取文字** 指令以及驗證輸出的方法。
- 一個完整、可執行的範例，現在就能放入 Visual Studio 使用。

### 前置條件

- .NET 6.0 SDK 或更新版本（程式碼同樣適用於 .NET Core）。
- 有效的 Aspose.OCR NuGet 套件（`Aspose.OCR` 23.9 或更新）。
- 一張範例收據圖像（例如 `skewed_receipt.jpg`），放在可參照的資料夾中。
- 基本的 C# 主控台應用程式開發經驗。

如果你已具備上述條件，讓我們直接進入主題——不囉嗦，只說重點。

---

## 執行圖像 OCR – 步驟概覽

在開始寫程式碼之前，先想像整個流程：

1. **載入** 圖片檔案至記憶體。  
2. **前處理**：校正傾斜、去除雜訊、提升對比度。  
3. **執行** OCR 引擎。  
4. **讀取** 產生的文字。

每個階段都是拼圖的一小塊，合起來就能 **在圖像上執行 OCR**，即使原始檔案本來難以辨識。以下各節會逐一說明每個步驟。

---

## 載入圖像以供 OCR

任何 OCR 工作流程的第一件事就是取得可供處理的位圖。Aspose 透過 `ImageStream` 抽象化檔案處理，讓你不必直接操作 `System.Drawing`，除非你真的需要。

```csharp
using Aspose.OCR;
using System;

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Step 2: Load the image you want to recognize
// Replace the path with the actual location of your receipt image
ocrEngine.Image = ImageStream.FromFile(@"C:\OCRDemo\skewed_receipt.jpg");

// Quick sanity check – make sure the image was loaded
if (ocrEngine.Image == null)
{
    Console.WriteLine("Failed to load image. Verify the file path.");
    return;
}
```

> **為什麼這很重要：** 正確載入圖像是基礎。如果路徑錯誤，之後的每個濾鏡都會在 null 參考上靜默執行，最終只會得到空結果。上面的檢查可以避免這種情況。

## 在 OCR 前處理圖像

收據照片常見三大問題：旋轉、隨機斑點、對比度低。Aspose 內建三種濾鏡，直接針對這些問題。順序很重要——先校正傾斜，再去雜訊，最後提升對比度。

```csharp
// Step 3: Add preprocessing filters in the desired order
ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Deskew);          // Corrects image rotation
ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Denoise);        // Reduces noise
ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.ContrastBoost); // Enhances contrast
```

> **小技巧：** 如果你一次處理的收據都是 300 dpi 掃描的，可以省略 `ContrastBoost`，因為掃描器已提供足夠的對比度。針對你的資料集進行實驗，是 **提升 OCR 準確度** 的關鍵。

## 使用濾鏡提升 OCR 準確度

現在圖像已完成前處理，OCR 引擎就能發揮魔法。`Recognize()` 會在清理過的位圖上執行基於神經網路的辨識器。

```csharp
// Step 4: Perform OCR recognition
ocrEngine.Recognize();
```

在背後，Aspose 會套用語言特定模型、字元分割與後處理啟發式演算法。把校正傾斜、去雜訊、高對比度的圖像餵給它，就等於給它一本教科書品質的頁面——因此你會看到期待的 **提升 OCR 準確度**。

## 從收據中擷取文字

最後，從引擎取得辨識後的字串。`Text` 屬性包含原始 Unicode 結果，你可以將它寫入主控台、檔案或資料庫。

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== Recognized Receipt Text ===");
Console.WriteLine(ocrEngine.Text);
```

典型的收據輸出會長這樣：

```
=== Recognized Receipt Text ===
Store: QuickMart
Date: 2024-06-15
Item 1  $2.99
Item 2  $5.49
Total   $8.48
Thank you!
```

如果發現缺少數字或出現亂碼，請回到前處理步驟——或許需要更強的 `Denoise` 等級或自訂濾鏡。好消息是，你可以在需要時堆疊多個相同的濾鏡實例。

## 完整可執行範例

以下是完整程式碼，直接複製貼上即可。將檔案存為 `Program.cs`、還原 NuGet 套件，然後執行。主控台會顯示擷取出的收據文字。

```csharp
using Aspose.OCR;
using System;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create the OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣  Load the image you want to process
            // -------------------------------------------------
            // Change the path to point at your own receipt file
            string imagePath = @"C:\OCRDemo\skewed_receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image from '{imagePath}'. Check the path and try again.");
                return;
            }

            // -------------------------------------------------
            // 3️⃣  Preprocess the image – this is where we
            //     actually **improve OCR accuracy**
            // -------------------------------------------------
            ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Deskew);
            ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Denoise);
            ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.ContrastBoost);

            // -------------------------------------------------
            // 4️⃣  Run the OCR engine – **perform OCR on image**
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // 5️⃣  Extract and display the text – **extract text from receipt**
            // -------------------------------------------------
            Console.WriteLine("\n=== Recognized Receipt Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### 預期輸出

對清晰、已校正傾斜的收據執行程式，應會印出與前面示例相似的文字。如果得到空字串，請再次檢查前處理順序，或嘗試提升來源圖像的 DPI。

---

## 常見問題與注意事項

- **如果收據是手寫的怎麼辦？**  
  Aspose.OCR 最適合辨識印刷文字。對於草寫或混合字型，可能需要專門的手寫模型或改用其他函式庫。

- **可以直接處理 PDF 嗎？**  
  可以——先將每頁 PDF 轉成圖像（`Aspose.PDF` 可協助），再將圖像送入相同的流程。

- **有沒有方法批次處理大量收據？**  
  把核心邏輯包在 `foreach` 迴圈中，遍歷資料夾內的圖像。記得在每個檔案處理完後釋放 `OcrEngine`，以釋放記憶體。

- **需要授權嗎？**  
  Aspose 提供帶浮水印的免費評估版。正式上線時，請購買授權以移除浮水印並解鎖完整效能。

## 結論

我們剛剛示範了如何使用 Aspose.OCR **在圖像上執行 OCR**，從 **載入圖像以供 OCR**、**在 OCR 前處理圖像**，最後 **從收據中擷取文字**。依序使用校正傾斜、去雜訊、對比度提升的濾鏡，通常能顯著 **提升 OCR 準確度**，尤其是低品質的收據掃描。

接下來可以嘗試加入語言提示 (`ocrEngine.Language = Language.English;`) 或實驗自訂的顏色反轉濾鏡。你也可以把擷取出的文字導入簡易的解析器，自動抽取項目明細與總金額。

如果本教學幫助你突破了常見的 OCR 障礙，歡迎在 GitHub 上給予星標或在下方留言。祝開發順利，願你的收據永遠可讀！

![說明協助您在圖像上執行 OCR 的前處理流程圖] 

---


## 接下來該學什麼？

以下教學與本指南所示技術密切相關，能幫助你進一步掌握 API 功能，並在自己的專案中探索其他實作方式。每個資源都提供完整可執行的程式碼範例與逐步說明。

- [從圖像擷取文字 – 使用 Aspose.OCR 進行 .NET OCR 優化](/ocr/english/net/ocr-optimization/)
- [如何使用 AspOCR：.NET 圖像 OCR 前處理濾鏡](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [使用 Aspose.OCR 以語言選擇擷取圖像文字 C#](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}