---
category: general
date: 2026-01-04
description: 快速將掃描 PDF 轉換為可搜尋的 PDF。了解如何在 C# 中使用 Aspose OCR 轉換掃描 PDF、為 PDF 加入 OCR，並調整圖像品質。
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- add ocr to pdf
- adjust image quality
- how to use ocr
language: zh-hant
og_description: 快速將掃描 PDF 轉換為可搜尋的 PDF。跟隨此一步一步指南，將掃描 PDF 轉為可搜尋 PDF、為 PDF 加上 OCR，並調整影像品質。
og_title: 使用 Aspose OCR 從掃描檔案建立可搜尋的 PDF
tags:
- Aspose OCR
- C#
- PDF processing
title: 使用 Aspose OCR 從掃描檔案建立可搜尋的 PDF
url: /zh-hant/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 從掃描檔案建立可搜尋的 PDF

是否曾需要 **建立可搜尋的 PDF**，卻不知道從哪裡開始？你並不孤單——許多開發者在建構文件管理流程時都會碰到這個問題。好消息是，使用 Aspose OCR 只要幾行 C# 程式碼，就能 **轉換掃描的 PDF**、加入 OCR，並微調影像品質。

在本教學中，我們會一步步說明完整流程，從載入掃描的 PDF 到儲存完整可搜尋的版本。完成後，你將清楚 **如何使用 OCR** 搭配 Aspose、每個設定的意義，以及當事情不如預期時該如何調整。沒有模糊的參考，只有可直接放入專案的完整可執行範例。

## 前置條件

在開始之前，請確保你已具備：

- .NET 6.0 或更新版本（程式碼同樣支援 .NET Core 與 .NET Framework）
- 有效的 Aspose OCR 授權（免費試用版可用於測試）
- 名為 `input.pdf` 的輸入 PDF，放在你可控制的資料夾中
- Visual Studio 2022 或任意你慣用的 C# 編輯器

就這些。如果有任何項目不熟悉，請先安裝缺少的部份——不需要其他前置作業。

## 步驟 1：初始化 OCR 引擎並載入掃描的 PDF  
**（這是第一次 **將 OCR 加入 PDF** 的地方。）**

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Load the scanned PDF from disk
ocrEngine.LoadPdf(@"C:\Docs\input.pdf");
```

*為什麼需要這一步？*  
`OcrEngine` 是 Aspose OCR 的核心。載入 PDF 讓引擎知道要從哪裡取得之後要分析的點陣圖影像。如果省略此步，將沒有可轉換的內容，後續步驟會拋出例外。

> **小技巧：** 若你的 PDF 有密碼保護，請使用 `ocrEngine.LoadPdf(path, password)` 以避免執行時錯誤。

## 步驟 2：設定主要語言與額外語言  
**（我們將 **轉換掃描的 PDF** 為英文、法文與德文。）**

```csharp
// Primary language – the most common language in the document
ocrEngine.Config.Language = Language.English;

// Add extra languages if the document contains multilingual text
ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };
```

*語言為何重要？*  
OCR 的準確度取決於它預期的字元集。將英文設為主要語言，並加入法文/德文，引擎即可正確辨識重音字元與特殊符號。忘記設定語言常會導致文字雜亂。

## 步驟 3：調整影像品質 – 微調 PDF 輸出  
**（在此 **調整影像品質** 以在檔案大小與可讀性之間取得平衡。）**

```csharp
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    ImageQuality = 90,          // JPEG quality for embedded images (0‑100)
    Compress = true,            // Enable PDF compression to shrink file size
    PreserveOriginalLayout = true // Keep the scanned layout intact
};
```

*為什麼要調整 `ImageQuality`？*  
較高的數值（90‑100）能保留銳利度，對 OCR 準確度相當重要，但同時會使檔案變大。如果要保存數百萬頁，將其降至 70‑80 可在不犧牲太多可讀性的前提下減少檔案體積。

## 步驟 4：將結果儲存為可搜尋的 PDF  
**（最後我們 **建立可搜尋的 PDF**，以便後續索引。）**

```csharp
// Export the OCR result as a searchable PDF
ocrEngine.SaveAsSearchablePdf(@"C:\Docs\output.pdf", pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created at C:\\Docs\\output.pdf");
```

*實際會發生什麼事？*  
Aspose OCR 從每一頁擷取文字層，並將其嵌入原始影像之後。PDF 的外觀保持不變，但現在可以選取、複製與搜尋文字，對後續工作流程是極大的加分。

## 步驟 5：驗證輸出（可選，但建議執行）  
雖然看起來一切正常，但快速的檢查可以避免日後的頭痛。

```csharp
using System.Diagnostics;

// Open the generated PDF automatically (Windows only)
Process.Start(new ProcessStartInfo
{
    FileName = @"C:\Docs\output.pdf",
    UseShellExecute = true
});
```

開啟檔案，嘗試選取一個單字，或按 `Ctrl+F` 並輸入原始掃描中確定存在的片語。若文字可被選取，即表示你已成功 **建立可搜尋的 PDF**。

## 常見邊緣案例與處理方式  

| 情況 | 為何會發生 | 快速解決方案 |
|-----------|----------------|-----------|
| **解析度不一致的頁面**（部分 150 dpi，部分 300 dpi） | OCR 品質因頁面而異，導致搜尋性不均。 | 在載入前設定 `ocrEngine.Config.Dpi = 300;` 以強制升頻，或使用 `ImageProcessor` 先行正規化 DPI。 |
| **加密的 PDF** | 未提供密碼時 Aspose OCR 無法讀取。 | 如前所示將密碼傳入 `LoadPdf`。 |
| **大型 PDF（>500 MB）** | 記憶體使用激增，導致 `OutOfMemoryException`。 | 將文件分段處理：`ocrEngine.SplitPdfIntoPages();` 逐頁 OCR 後再合併結果。 |
| **非拉丁字元**（例如西里爾文） | 未加入相應語言，字元會變成 “?”。 | 將 `Language.Russian`（或其他需要的語言）加入 `AdditionalLanguages`。 |
| **影像品質過低** | 文字模糊，OCR 失敗。 | 提升 `ImageQuality` 或使用 `pdfOptions.Dpi = 300;` 以嵌入較高解析度的影像。 |

## 完整、可直接執行的範例  

以下程式碼可直接貼到新的 Console 應用程式中。它包含所有步驟、錯誤處理與說明註解。

```csharp
using System;
using System.Diagnostics;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\Docs\input.pdf";
            string outputPath = @"C:\Docs\output.pdf";

            try
            {
                // 1️⃣ Initialize OCR engine and load scanned PDF
                OcrEngine ocrEngine = new OcrEngine();
                ocrEngine.LoadPdf(inputPath);

                // 2️⃣ Configure languages (primary + additional)
                ocrEngine.Config.Language = Language.English;
                ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };

                // 3️⃣ Set PDF save options – adjust image quality as needed
                PdfSaveOptions pdfOptions = new PdfSaveOptions
                {
                    ImageQuality = 90,
                    Compress = true,
                    PreserveOriginalLayout = true
                };

                // 4️⃣ Save as searchable PDF
                ocrEngine.SaveAsSearchablePdf(outputPath, pdfOptions);
                Console.WriteLine($"✅ Searchable PDF created at {outputPath}");

                // 5️⃣ Optional: open the file to verify
                Process.Start(new ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            catch (Exception ex)
            {
                // Friendly error message – helps during debugging
                Console.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
                // For real‑world apps, consider logging the stack trace
            }
        }
    }
}
```

**預期輸出：**  
```
✅ Searchable PDF created at C:\Docs\output.pdf
```

開啟 `output.pdf` 後，你應該能選取並搜尋原始掃描中出現的任何文字。

---

## 常見問答 (FAQs)

**Q: 這能處理同時包含掃描影像與原生文字的 PDF 嗎？**  
A: 當然可以。Aspose OCR 只會在需要的地方加入隱藏文字層，既有的文字保持不變。

**Q: 可以批次處理整個資料夾的 PDF 嗎？**  
A: 可以。將上述程式碼包在 `foreach (var file in Directory.GetFiles(folder, "*.pdf"))` 迴圈中，並相應調整輸出路徑即可。

**Q: 如何進一步縮小最終 PDF 的大小？**  
A: 降低 `ImageQuality` 至 70‑80，啟用 `Compress`，或將 `pdfOptions.Dpi = 150` 以在嵌入前下採樣影像。

**Q: 有沒有辦法在不產生 PDF 的情況下直接取得 OCR 文字？**  
A: 載入 PDF 後呼叫 `ocrEngine.ExtractText();` 即可取得純文字字串，供儲存或索引使用。

---

## 結語  

我們剛剛說明了 **如何使用 OCR** 搭配 Aspose **建立可搜尋的 PDF**，展示了 **轉換掃描的 PDF**、**將 OCR 加入 PDF**、以及 **調整影像品質** 以取得最佳結果。完整程式碼已備妥，故障排除表格也能在意外發生時協助你快速前進。

接下來可以嘗試：

- 為多語言檔案庫加入不同語言包
- 透過 `ImageProcessor` 進行自訂影像前處理（去斜、除噪點）
- 將可搜尋的 PDF 整合至 SharePoint 或 ElasticSearch 流程中

如有任何問題或發現巧妙的調整方式，歡迎留言討論。祝開發順利，享受即時可搜尋的 PDF 吧！

![Create searchable PDF flowchart showing OCR engine → language config → PDF save options → searchable PDF output](create-searchable-pdf-flow.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}