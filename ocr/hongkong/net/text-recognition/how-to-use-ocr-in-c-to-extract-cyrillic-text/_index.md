---
category: general
date: 2026-09-10
description: 如何在 C# 中使用 OCR 提取西里爾文字、預處理圖像，並在單一可執行範例中將其轉換為 PDF 或 HTML 檔案。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- preprocess image for OCR
- convert image to PDF
- convert image to HTML
- extract Cyrillic text
language: zh-hant
lastmod: 2026-09-10
og_description: 如何在 C# 中使用 OCR 提取西里爾文字、預處理圖像，並將結果匯出為 PDF 或 HTML。請依照此逐步指南操作。
og_image_alt: Diagram illustrating how to use OCR to extract Cyrillic text and convert
  images
og_title: 如何在 C# 中使用 OCR – 提取西里爾文字並轉換圖像
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: How to use OCR in C# to extract Cyrillic text, preprocess images, and
    convert them to PDF or HTML files in a single, runnable example.
  headline: How to use OCR in C# to extract Cyrillic text
  type: TechArticle
tags:
- OCR
- C#
- Cyrillic
- Image processing
- PDF conversion
title: 如何在 C# 中使用 OCR 提取西里爾文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-to-extract-cyrillic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR 提取西里爾文字

如果你需要在 C# 中 **使用 OCR** 來從掃描文件中提取西里爾文字，本指南將為你展示一個完整、可直接執行的解決方案。你還會學習如何 **預處理影像以供 OCR 使用**，以及在文字辨識完成後，如何 **將影像轉換為 PDF** 或 **將影像轉換為 HTML**。

文件數位化專案常會遇到兩個問題：掃描品質低以及需要以多種格式儲存結果。本教學透過使用 Aspose.OCR 函式庫解決這兩個問題，該函式庫會自動下載缺少的語言套件，提供內建的影像處理輔助功能，且只需一次呼叫即可將 OCR 結果匯出為 PDF 或 HTML。

## 前置條件

* .NET 6.0 SDK 或更新版本（程式碼亦可在 .NET Framework 4.7+ 上執行）。
* Visual Studio 2022 或任何支援 C# 專案的編輯器。
* **Aspose.OCR** NuGet 套件。使用以下指令安裝：

```bash
dotnet add package Aspose.OCR
```

* 包含西里爾字元的影像檔（例如 `sample_cyrillic.jpg`）。  
  將檔案放置於可以 `YOUR_DIRECTORY` 參照的資料夾中。

函式庫會在你第一次設定 `ocrEngine.Language = Language.Cyrillic;` 時自動下載西里爾語言套件，因此不需要手動下載。

## 第一步 – 初始化 OCR 引擎（使用 OCR）

建立 `OcrEngine` 實例可為之後的所有操作做好準備。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine – the first step in how to use OCR with Aspose
        var ocrEngine = new OcrEngine();
```

**為什麼這很重要：** 引擎會保存語言、影像處理設定以及輸出選項等配置。只初始化一次即可讓其餘程式碼保持簡潔且具執行緒安全性。

## 第二步 – 選擇西里爾語言（提取西里爾文字）

```csharp
        // Select Cyrillic language; the pack is fetched automatically if missing
        ocrEngine.Language = Language.Cyrillic;
```

**為什麼這很重要：** OCR 的準確度高度依賴正確的語言模型。透過明確選取 `Language.Cyrillic`，引擎會套用適用於俄文、烏克蘭文、保加利亞文等的字元頻率表。

## 第三步 – 為 OCR 預處理影像

低品質的掃描可能有傾斜、斑點或光線不均等問題。內建的 `ImageProcessor` 只需兩次呼叫即可提升辨識率。

```csharp
        // Optional but strongly recommended: deskew and despeckle the image
        ocrEngine.ImageProcessor.Deskew();      // Aligns rotated text
        ocrEngine.ImageProcessor.Despeckle();  // Removes isolated noise pixels
```

**為什麼這很重要：** 預處理可減少錯誤字元並提升信心分數。傾斜的文字常會產生亂碼；校正傾斜可將其矯正。去除斑點則能消除微小雜訊，避免 OCR 引擎誤將其辨識為字母。

> **小技巧：** 若來源影像已相當乾淨，可省略這些呼叫。對於嚴重退化的掃描，建議加入額外步驟，例如 `Binarize()` 或 `ContrastStretch()`。

## 第四步 – 對輸入影像執行 OCR

```csharp
        // The image path can be absolute or relative to the executable
        string inputPath = Path.Combine("YOUR_DIRECTORY", "sample_cyrillic.jpg");
        ocrEngine.Process(inputPath);
```

**為什麼這很重要：** `Process` 會在提供的 bitmap 上執行辨識流程。它不回傳值（`void`），辨識後的文字可透過 `Text` 屬性取得。

## 第五步 – 取得辨識文字並儲存至檔案

```csharp
        // Access the recognized string
        string recognizedText = ocrEngine.Text;

        // Save the plain‑text result
        string txtOutput = Path.Combine("YOUR_DIRECTORY", "result.txt");
        File.WriteAllText(txtOutput, recognizedText);
        Console.WriteLine("Text saved to: " + txtOutput);
```

**為什麼這很重要：** 儲存原始文字可供後續處理，例如搜尋、索引或輸入至翻譯服務。

## 第六步 – 匯出 OCR 結果至其他格式（將影像轉換為 PDF 及將影像轉換為 HTML）

```csharp
        // Export as PDF – useful for archival or sharing with non‑technical users
        string pdfOutput = Path.Combine("YOUR_DIRECTORY", "result.pdf");
        ocrEngine.SaveResultAsPdf(pdfOutput);
        Console.WriteLine("PDF saved to: " + pdfOutput);

        // Export as HTML – retains basic layout and can be displayed in browsers
        string htmlOutput = Path.Combine("YOUR_DIRECTORY", "result.html");
        ocrEngine.SaveResultAsHtml(htmlOutput);
        Console.WriteLine("HTML saved to: " + htmlOutput);
    }
}
```

**為什麼這很重要：** 將 OCR 結果轉換為 PDF 或 HTML 可保留原始影像的視覺情境，同時提供可搜尋的文字。這在法律或檔案保存流程中特別有價值。

### 預期輸出

執行程式並使用清晰的西里爾掃描圖像時，會產生三個檔案：

* `result.txt` – 純 Unicode 文字，例如 `Пример текста на кириллице`。
* `result.pdf` – 包含影像且具隱藏文字層以供搜尋的 PDF。
* `result.html` – 顯示影像與可選取文字的 HTML 頁面。

開啟任一檔案，即可驗證西里爾字元已正確提取。

## 常見問題與邊緣案例

| 問題 | 答案 |
|----------|--------|
| **如果語言套件下載失敗怎麼辦？** | 確保機器具備網路連線。也可以先從 Aspose 官方網站下載語言套件，並放置於 `bin` 資料夾中。 |
| **我可以在同一次執行中辨識其他字母表嗎？** | 可以。於 `Process` 之前呼叫 `ocrEngine.Language = Language.English;`（或任何支援的列舉值）。若影像混合多種文字，可能需要針對每種語言分別執行 `Process`。 |
| **我的影像是多頁 TIFF – 能使用嗎？** | `OcrEngine` 每次只處理一個 bitmap。將每一頁載入為 `Bitmap`，於迴圈中呼叫 `Process`，再將結果串接起來。 |
| **如何提升大量批次的效能？** | 重複使用同一個 `OcrEngine` 實例，並設定 `ocrEngine.OptimizeMemory = true;`。此外，也可考慮在每個執行緒使用獨立的引擎實例以進行平行處理。 |

## 結論

現在你已了解如何在 C# 中 **使用 OCR** 來 **提取西里爾文字**、**預處理影像以供 OCR**，以及 **將影像轉換為 PDF** 或 **將影像轉換為 HTML**，只需幾個簡潔步驟。完整範例展示了生產環境的‑

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [如何使用 AspOCR：為 .NET 預處理影像 OCR 濾鏡](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [如何在 C# 中提取 OCR 文字 – 完整步驟指南](/ocr/english/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/)
- [如何在影像辨識中使用 Aspose OCR 取得 JSON 結果](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}