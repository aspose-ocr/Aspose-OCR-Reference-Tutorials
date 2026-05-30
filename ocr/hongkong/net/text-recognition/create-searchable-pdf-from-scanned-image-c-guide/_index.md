---
category: general
date: 2026-04-26
description: 使用 Aspose OCR 於 C# 中將掃描圖像轉換為可搜尋的 PDF。了解如何快速將掃描圖像轉換、提取文字，並產生可搜尋的 PDF。
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: zh-hant
og_description: 使用 Aspose OCR 從掃描圖像建立可搜尋的 PDF。逐步 C# 程式碼示範如何轉換、擷取文字，並產生可搜尋的 PDF。
og_title: 從掃描圖像建立可搜尋 PDF – C# 指南
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: 從掃描圖像建立可搜尋的 PDF – C# 指南
url: /zh-hant/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從掃描圖像建立可搜尋 PDF – C# 教學

有沒有需要 **建立可搜尋 PDF** 檔案的時候，面對紙本合約、收據或舊檔案？你並不孤單——大多數開發者在客戶交付一堆 TIFF 掃描檔，卻要求交付可搜尋 PDF 時，都會卡關。

在本教學中，我們將示範 **如何對文件進行 OCR**，並使用 Aspose OCR for .NET 將掃描圖像轉換成 **可搜尋 PDF**。完成後，你將能 **轉換掃描圖像** 檔案、 **從圖像中擷取文字**，甚至處理多頁 TIFF，毫不費力。

## 需要的環境

在開始之前，請確保你已具備：

* .NET 6.0 或更新版本（API 同時支援 .NET Core、.NET Framework 與 .NET 5+）。  
* 有效的 Aspose OCR 授權，或接受評估版的浮水印。  
* 已安裝 `Aspose.OCR` NuGet 套件（`dotnet add package Aspose.OCR`）。  
* 一個範例 TIFF 檔（例如 `contract_scan.tif`），你想將它轉成可搜尋 PDF。

就這些——不需要額外函式庫，也不需要複雜設定。準備好了嗎？開始吧。

![建立可搜尋 PDF 範例](create-searchable-pdf.png "建立可搜尋 PDF 範例")

## 步驟 1 – 初始化 OCR 引擎（Create Searchable PDF）

首先，你需要一個 `OcrEngine` 實例。這個物件負責讀取位圖、辨識字元，並回傳文字給你。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**為什麼要設定語言？**  
如果保留預設，Aspose 會嘗試所有語言包，會降低速度。指定 `Language.Latin` 可讓引擎只聚焦於拉丁字母，提升速度並在英文合約上取得更準確的結果。

## 步驟 2 – 載入掃描圖像（Convert Scanned Image）

現在把要處理的圖像提供給引擎。Aspose 可以接受檔案路徑、串流，甚至 `byte[]`。為了簡化，我們使用 `ImageStream.FromFile`。

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

如果之後需要 **將 TIFF 轉成 PDF**，請記得多頁 TIFF 會自動處理——每個影格會變成 PDF 的單獨頁面。

## 步驟 3 – 執行 OCR 並取得文字（Extract Text From Image）

執行 OCR 只要呼叫 `Recognize` 即可。引擎會回傳 `RecognitionResult`，其中包含純文字、信心分數與版面資訊。

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**小技巧：** 若你只需要文字（不需要 PDF），此時即可將 `extractedText` 寫入 `.txt` 檔。但大多數情況下，我們的目標是可搜尋 PDF，所以會繼續往下走。

## 步驟 4 – 儲存為可搜尋 PDF（Create Searchable PDF）

Aspose 讓最後一步變得非常簡單：只要使用 `Save` 並指定 `SaveFormat.PdfSearchable`。在背後，函式庫會將擷取的文字以隱形圖層嵌入，同時保留原始圖像外觀。

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

當你在任何 PDF 閱讀器中開啟 `contract_searchable.pdf`，即可選取、複製與搜尋文字——這正是客戶對「可搜尋 PDF」的期待。

## 處理多頁 TIFF（Convert Tiff to PDF）

若來源檔案包含多頁，Aspose 會自動將每個影格視為獨立頁面，無需額外迴圈。但你可能想為每頁調整 DPI 或圖像品質：

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

設定完這些選項後，對每個影格重複 **步驟 2**，或直接將 `ImageStream.FromFile` 指向多頁 TIFF，讓 Aspose 完成繁重工作。

## 常見問題與解決方式

| 症狀 | 可能原因 | 解決方法 |
|------|----------|----------|
| 文字亂碼或缺失 | 語言設定錯誤 | 將 `ocrEngine.Language` 設為正確的語言包（例如 `Language.German`）。 |
| PDF 檔案過大（單頁掃描就 10 MB） | 預設圖像壓縮率低 | 將 `ocrEngine.ImageProcessingOptions.Compression` 調整為 `Jpeg`，並設定合理的 `Quality`（0‑100）。 |
| OCR 執行非常慢 | 使用預設的 `Auto` 語言偵測 | 明確設定預期的語言。 |
| 沒有可搜尋圖層 | 使用 `SaveFormat.Pdf` 而非 `PdfSearchable` 儲存 | 改用 `PdfSearchable`。 |

## 完整端對端範例

以下是一個可直接貼到 Visual Studio 的完整主控台應用程式範例：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**執行結果會顯示：**  
* 主控台視窗印出 OCR 文字的片段。  
* `contract_searchable.pdf` 檔案會與原始 TIFF 同目錄。開啟後，按 **Ctrl + F**，搜尋原始掃描中出現的任意字詞——完成！

## 後續步驟與相關主題

* **如何批次 OCR 文件** – 將上述程式碼包在 `foreach` 迴圈中，處理整個資料夾。  
* **轉換其他掃描圖像格式**（PNG、JPEG） – 同樣的 API 只要換檔案副檔名即可。  
* **從圖像中擷取文字** 以進行後續分析 – 把 `result.Text` 送入自然語言處理管線。  
* **優化 PDF 大小** – 探索 `PdfSaveOptions` 以進一步壓縮圖像或僅在需要時嵌入字型。  

試試這些想法，你很快就會成為「把掃描檔轉成可搜尋 PDF」的首選專家。

---

### TL;DR

現在你已掌握使用 Aspose OCR 在 C# 中 **建立可搜尋 PDF** 檔案的完整流程：初始化引擎、載入圖像、執行 OCR，最後以 `PdfSearchable` 儲存。調整語言、DPI 與壓縮設定即可因應各種情境，讓你能 **轉換掃描圖像**、 **從圖像中擷取文字**，甚至 **將 TIFF 轉成 PDF**，規模化處理。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}