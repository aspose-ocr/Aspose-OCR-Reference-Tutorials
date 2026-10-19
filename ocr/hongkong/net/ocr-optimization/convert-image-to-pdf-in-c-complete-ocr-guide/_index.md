---
category: general
date: 2026-09-13
description: 了解如何在 C# 中使用 Aspose OCR 將掃描頁面轉換為 PDF。本指南展示影像前處理、韓文文字辨識以及建立可搜尋的 PDF。
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: 了解如何在 C# 中使用 Aspose OCR 將掃描頁面轉換為 PDF。教學涵蓋影像前處理、GPU 加速的韓文 OCR 以及在數分鐘內產生可搜尋的
  PDF。
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: 如何在 C# 中使用 OCR 將掃描頁面轉換為 PDF
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: 如何在 C# 中使用 OCR 將掃描頁面轉換為 PDF
url: /zh-hant/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR 將掃描頁面轉換為 PDF

如果您需要在保持文字可搜尋的情況下**將掃描頁面轉換為 PDF**，您來對地方了。本教學將帶您使用 Aspose OCR 來**preprocess image for OCR**、**recognize Korean text image**，最後**create searchable PDF image**——全部透過一個簡單的 C# 主控台應用程式。

## 快速回答
- **什麼函式庫負責 OCR？** Aspose.OCR for .NET  
- **我可以使用 GPU 嗎？** Yes – enable GPU acceleration for up to 2× faster processing  
- **我需要韓文語言套件嗎？** It downloads automatically on first use  
- **輸出會是可搜尋的嗎？** The generated PDF contains an invisible text layer  
- **支援哪些 .NET 版本？** .NET 6.0 and later (including .NET Core and .NET Framework)

## 系統需求

- **.NET 6.0 或更新版本** – 可在 .NET Core、.NET Framework 以及 .NET 5/6+ 上運行  
- **Aspose.OCR for .NET** NuGet 套件 (`Aspose.OCR`) – trial keys are free on the Aspose site  
- 一張包含韓文字符的範例圖片，例如 `korean_book_page.jpg`  
- 您喜愛的 IDE（Visual Studio 2022、VS Code、Rider 等）

> **Pro tip:** 將圖片存放於 `Resources/` 資料夾，以確保路徑在不同機器間保持一致。

## 流程概覽

1. 使用 GPU 支援初始化 OCR 引擎。  
2. 新增 **preprocess image for OCR** 濾鏡，如校正傾斜 (deskew) 與去噪 (denoise)。  
3. 下載並載入韓文語言模型（自動處理）。  
4. 在圖片上執行 OCR。  
5. 使用 **SearchablePdfExporter** 匯出結果，以 **create searchable PDF image**。  
6. （可選）將 OCR 輸出序列化為 JSON，以供下游管線使用。

以下我們將展開每個步驟，說明*為何*它重要，並提供您可以直接複製貼上的完整程式碼。

## 掃描頁面轉 PDF 的轉換原理是什麼？

`OcrEngine` 是 Aspose.OCR 中執行影像光學字符辨識的主要類別。  
`SearchablePdfExporter` 會建立一個 PDF，內含原始影像與供搜尋的隱形文字層。  
`RecognitionResult` 保存 OCR 引擎回傳的文字與信賴度資料。

使用 `new OcrEngine()` 載入您的影像，然後呼叫 `engine.Recognize("korean_book_page.jpg")`，接著將 `RecognitionResult` 傳遞給 `SearchablePdfExporter.Export`。此兩步流程會讀取位圖、擷取 Unicode 文字，並將兩者嵌入同一個 PDF，文字層為隱形但可搜尋。GPU 加速可將辨識時間縮短約一半，而校正傾斜與去噪濾鏡可在噪點掃描上提升最高 15 % 的準確度。

## 轉換影像為 PDF – 完整工作流程

以下程式碼片段是*完整*的程式。建立一個新的主控台專案 (`dotnet new console -n OcrPdfDemo`) 並將自動產生的 `Program.cs` 替換為占位符中顯示的程式碼。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### 為什麼這樣有效

- **GPU acceleration** 可將辨識時間縮短約一半，相較於僅使用 CPU 的模式。  
- **Deskew** 與 **Denoise** 為經典的 *preprocess image for OCR* 技術；它們可校正常見的掃描缺陷，否則會導致引擎遺漏字符。  
- **Language model loading** 對於 **recognize Korean text image** 至關重要——若未載入韓文模型，引擎將退回使用通用的拉丁字母，產生無意義的結果。  
- **SearchablePdfExporter** 會將原始位圖與隱形文字覆蓋層打包，為您提供 **create searchable pdf image** 的結果，您可在任何 PDF 閱讀器中進行索引。

## 為什麼這樣有效

- **GPU acceleration** 可將辨識時間縮短約一半，相較於僅使用 CPU 的模式。  
- **Deskew** 與 **Denoise** 為經典的 *preprocess image for OCR* 技術；它們可校正常見的掃描缺陷，否則會導致引擎遺漏字符。  
- **Language model loading** 對於 **recognize Korean text image** 至關重要——若未載入韓文模型，引擎將退回使用通用的拉丁字母，產生無意義的結果。  
- **SearchablePdfExporter** 會將原始位圖與隱形文字覆蓋層打包，為您提供 **create searchable pdf image** 的結果，您可在任何 PDF 閱讀器中進行索引。

## OCR 前處理影像 – 提示與技巧

`DeskewFilter` 校正掃描頁面的旋轉。  
`ContrastFilter` 調整影像對比度以提升 OCR 準確度。  
`BinarizationFilter` 依據閾值將影像轉為黑白，減少背景雜訊。  
`OrientationFilter` 偵測並校正混合的直式/橫式頁面。

| 問題 | 額外濾鏡 | 如何新增 |
|-------|-------------------|------------|
| 低對比度 | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| 大量背景噪聲 | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| 混合方向（直式與橫式） | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Note:** 添加過多濾鏡會降低處理速度。請在單頁上測試每項變更，再進行規模擴展。

## 辨識韓文影像 – 常見陷阱

韓文文字包含視覺上密集的 Hangul 音節。如果您發現輸出雜亂：

1. **確保語言模型已完整下載** – 在主控台檢查類似 “Downloading Korean model…” 的訊息。  
2. **在 `DeskewFilter` 中提升 `MaxAngle`**，若您的掃描旋轉角度超過 12°。  
3. **提升 GPU 記憶體**，設定 `ocrEngine.GpuMemoryLimit = 2048;`（單位為 MB）。

`LanguageModel.Korean` 載入韓文語言資料以供 OCR 使用，實現精確的 Hangul 辨識。  

這些調整直接影響 **recognize Korean text image** 的成功率。

## 建立可搜尋 PDF 影像 – 驗證結果

程式執行完畢後，於任何 PDF 閱讀器（Adobe Acrobat Reader、Foxit，甚至 Chrome）開啟 `korean_page.pdf`。您應該能夠：

- **Select text** 以滑鼠選取文字，就像原生 PDF 一樣。  
- **Search** 使用內建搜尋框搜尋韓文字詞。

如果文字層顯示為空白，請再次確認 `Export` 方法收到正確的影像路徑，且 OCR 結果的 `RecognitionResult.Text` 非空。

## 完整 JSON 輸出 – 期待的結果

主控台會印出格式化良好的 JSON 負載。以下是一個裁剪過的範例：

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## 疑難排解與常見問題

**Q: 我的 PDF 相較於原始影像過大。**  
A: 匯出器會以原始解析度嵌入位圖。如果檔案大小是考量因素，請在辨識前先縮小影像：

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: OCR 回傳空字串。**  
A: 請確認影像路徑正確且檔案未損壞。同時，確保 GPU 驅動程式為最新版本；舊版驅動可能導致靜默失敗。

**Q: 我可以在迴圈中處理多頁嗎？**  
A: 當然可以。將第 4‑6 步驟包在 `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` 迴圈中，並相應調整輸出 PDF 的路徑。

## 結論

我們剛剛**將影像轉換為 PDF**，同時保留可搜尋的文字，這全賴 Aspose OCR 強大的管線。透過 **preprocess image for OCR** 提升準確度；透過 **recognize Korean text image** 處理複雜文字；再透過 **create searchable pdf image** 獲得可攜帶、可索引的文件。

取得程式碼，指向您自己的掃描檔，並嘗試額外的濾鏡或語言模型。相同的模式亦適用於中文、日文或任何拉丁語系語言——只需將 `LanguageModel.Korean` 替換為相應的列舉值。

還有其他問題嗎？留下評論，祝開發愉快！

---

**最後更新：** 2026-09-13  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose

## 相關教學

- [使用 Aspose Ocr 從掃描檔建立可搜尋 PDF](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [OCR 前處理管線：如何從影像辨識文字](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [使用 Aspose Ocr 完整 C 指南：從影像辨識文字](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}