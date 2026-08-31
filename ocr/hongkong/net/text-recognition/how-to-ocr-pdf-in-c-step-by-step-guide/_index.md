---
category: general
date: 2025-12-29
description: 學習如何在 C# 中對 PDF 檔案進行 OCR，並從 PDF 頁面擷取文字。本教學亦涵蓋將 PDF 轉換為文字以及在 C# 中讀取 PDF
  頁面的技巧。
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- extract pdf text c#
- read pdf page c#
language: zh-hant
og_description: 如何在 C# 中 OCR PDF 的簡明指南。獲取完整程式碼以從 PDF 提取文字、將 PDF 轉換為文字，以及在 C# 中讀取 PDF
  頁面。
og_title: 如何在 C# 中對 PDF 進行 OCR – 完整程式設計指南
tags:
- OCR
- C#
- PDF processing
title: 如何在 C# 中對 PDF 進行 OCR – 步驟指南
url: /zh-hant/net/text-recognition/how-to-ocr-pdf-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中 OCR PDF – 步驟說明指南

有沒有想過 **如何在 C# 應用程式中 OCR PDF** 檔案？或許你手頭有一堆掃描過的發票，需要在不手動複製貼上的情況下擷取文字。這是常見的痛點，尤其是當 PDF 為影像型且傳統文字擷取失效時。

在本教學中，我們將一步步示範完整、可直接執行的解決方案，不僅告訴你 **如何 OCR PDF**，同時示範 *從 PDF 中擷取文字*、*將 PDF 轉換為文字*，以及 *在 C# 中讀取 PDF 頁面*，全部使用 Aspose.OCR 函式庫。沒有模糊的參考——只有你可以直接貼到 Visual Studio 並開始實驗的程式碼。

## 你需要的環境

- **.NET 6.0** 或更新版本（此程式碼亦可在 .NET Framework 4.7+ 上執行）  
- **Aspose.OCR** NuGet 套件 – 使用 `dotnet add package Aspose.OCR` 安裝  
- 一個掃描過的 PDF（例如 `invoice.pdf`），放在可參考的資料夾中  
- 基本的 C# 主控台應用程式知識  

就這樣。如果你已經有專案，只要加入套件即可開始。

## 步驟 1：建立專案並加入 Aspose.OCR

首先，建立一個新的主控台專案（或使用既有的），然後將 OCR 函式庫加入專案。

```csharp
// Create a new console app (run this in a terminal)
// > dotnet new console -n OcrPdfDemo
// > cd OcrPdfDemo
// > dotnet add package Aspose.OCR
```

此步驟的重要性：Aspose.OCR 負責影像分析、版面偵測與字元辨識的繁重工作。若沒有它，你必須自行拼湊光柵化、Tesseract 引擎以及大量的黏合程式碼。

## 步驟 2：匯入命名空間並建立 OCR 引擎

現在開啟 `Program.cs`（或任何你偏好的 .cs 檔），加入必要的 `using` 指令。

```csharp
using System;
using Aspose.OCR;   // Core OCR classes
```

建立引擎相當簡單，我們同時會設定幾個選項，以提升對常見發票掃描的辨識準確度。

```csharp
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // Enable automatic language detection (optional but handy)
    Language = Language.English,
    // Turn on deskew to correct rotated pages
    ImagePreprocessingOptions = new ImagePreprocessingOptions
    {
        Deskew = true,
        Binarization = true
    }
};
```

**小技巧：** 若事先知道語言，請明確設定 `Language`；這會加快辨識速度。

## 步驟 3：指向你的 PDF 檔案

指定要處理的 PDF 的絕對或相對路徑。以下範例假設檔案位於名為 `Samples` 的資料夾內。

```csharp
// Path to the PDF you want to OCR
string pdfFilePath = @"Samples/invoice.pdf";

// Verify the file exists early to avoid runtime surprises
if (!System.IO.File.Exists(pdfFilePath))
{
    Console.WriteLine($"File not found: {pdfFilePath}");
    return;
}
```

檢查檔案是否存在是一個小步驟，但能避免之後出現難以理解的例外。

## 步驟 4：選擇要讀取的頁面

PDF 可能有數十頁，但通常只需要特定的一頁——例如發票的第二頁，總金額所在之處。`RecognizePdf` 方法允許你針對單一頁面或整份文件。

```csharp
// Extract text from page 2 (page numbers are 1‑based)
int pageNumber = 2;

// The method returns an OcrResult containing the recognized text
OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);
```

如果想要 *將 PDF 轉換為文字*（整份文件），只要省略 `pageNumber` 參數：

```csharp
// OcrResult fullResult = ocrEngine.RecognizePdf(pdfFilePath);
```

## 步驟 5：顯示或儲存擷取的文字

OCR 引擎完成工作後，你可以將文字印到主控台、寫入 `.txt` 檔，或傳入其他系統（例如資料庫）。

```csharp
// Show the recognized text in the console
Console.WriteLine("=== OCR Result (Page {0}) ===", pageNumber);
Console.WriteLine(ocrResult.Text);

// Optionally, save to a .txt file
string outputPath = $"output_page{pageNumber}.txt";
System.IO.File.WriteAllText(outputPath, ocrResult.Text);
Console.WriteLine($"Text saved to {outputPath}");
```

**為什麼這很重要：** 透過持久化輸出，你可以產生可重複使用的成果——非常適合後續的分析或搜尋索引。

## 完整範例程式

將所有步驟整合，以下是一個可直接貼到 `Program.cs` 並立即執行的自包含程式。

```csharp
using System;
using Aspose.OCR;

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine with helpful options
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                ImagePreprocessingOptions = new ImagePreprocessingOptions
                {
                    Deskew = true,
                    Binarization = true
                }
            };

            // 2️⃣ Define the PDF path
            string pdfFilePath = @"Samples/invoice.pdf";
            if (!System.IO.File.Exists(pdfFilePath))
            {
                Console.WriteLine($"Error: File not found -> {pdfFilePath}");
                return;
            }

            // 3️⃣ Choose which page to OCR (change as needed)
            int pageNumber = 2; // read PDF page C# example

            // 4️⃣ Perform OCR on the selected page
            OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);

            // 5️⃣ Output the result
            Console.WriteLine($"--- OCR Result for page {pageNumber} ---");
            Console.WriteLine(ocrResult.Text);

            // 6️⃣ Save to a text file for later use
            string outputPath = $"output_page{pageNumber}.txt";
            System.IO.File.WriteAllText(outputPath, ocrResult.Text);
            Console.WriteLine($"Extracted text saved to: {outputPath}");
        }
    }
}
```

### 預期輸出

```
--- OCR Result for page 2 ---
Invoice #12345
Date: 2024‑11‑30
Total: $1,250.00
...
Extracted text saved to: output_page2.txt
```

如果 PDF 內的掃描圖像清晰且高解析度，輸出將近乎完美。較低品質的影像可能需要額外前處理（例如提升 DPI 或套用濾鏡）；可調整 Aspose.OCR 的 `ImagePreprocessingOptions` 以因應這類情況。

## 常見問題與邊緣案例

### 1️⃣ PDF 若有密碼保護該怎麼辦？
Aspose.OCR 的 `RecognizePdf` 多載接受 `PdfLoadOptions` 物件，你可以在其中設定密碼：

```csharp
var loadOptions = new PdfLoadOptions { Password = "mySecret" };
OcrResult result = ocrEngine.RecognizePdf(pdfFilePath, pageNumber, loadOptions);
```

### 2️⃣ 能一次 OCR 整份文件嗎？
可以——只要呼叫 `RecognizePdf(pdfFilePath)`，不指定頁碼。此方法會回傳單一 `OcrResult`，其中包含所有頁面的合併文字。

### 3️⃣ 與使用文字型函式庫「從 PDF 中擷取文字」有何不同？
純文字擷取（例如使用 iTextSharp）僅適用於已包含可選取文字的 PDF。**如何 OCR PDF** 則在 PDF 本質上是影像（如掃描發票）時必須使用。此時 OCR 引擎會執行光學字符辨識，將圖片轉換為可搜尋的文字。

### 4️⃣ 大型 PDF 的效能如何？
處理時間大致與頁數與影像解析度呈線性關係。若需大量批次作業，可考慮：
- 使用平行處理 (`Parallel.ForEach`)  
- 在 OCR 前降低影像 DPI (`Resolution = 150`)  
- 將 `OcrEngine` 實例快取起來，而非每個檔案重新建立

### 5️⃣ 如何取得每個字的邊界框？
`OcrResult` 會暴露 `OcrRegion` 物件集合，每個物件都包含座標。你可以遍歷它們，以建立可搜尋的 PDF 或在 UI 中高亮顯示結果。

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} – ({region.Bounds.X}, {region.Bounds.Y}, {region.Bounds.Width}, {region.Bounds.Height})");
}
```

## 產品環境實作小技巧

- **錯誤處理：** 將 OCR 呼叫包在 try/catch 中，以捕捉函式庫特有的例外。  
- **日誌記錄：** 記錄頁碼與處理時間，有助於發現問題掃描。  
- **記憶體管理：** 若手動將 PDF 頁面轉為影像再 OCR，請釋放大型 `Bitmap` 物件。  
- **安全性：** 切勿將原始 PDF 存放在不安全的磁碟上；考慮直接將檔案串流至 OCR 引擎。

## 結論

現在你已掌握使用 C# **如何 OCR PDF** 的完整端對端解決方案。教學涵蓋了從安裝 Aspose.OCR、選取特定頁面、擷取文字，到處理常見邊緣案例的所有步驟。憑藉這個基礎，你可以 *從 PDF 中擷取文字*、*將 PDF 轉換為文字*，以及 *在 C# 中讀取 PDF 頁面*，以建構任何文件處理管線。

準備好下一步了嗎？試著將 OCR 輸出送入全文搜尋引擎（如 Lucene.NET），或透過在原始影像上覆蓋辨識文字來產生可搜尋的 PDF。未來的可能性無限，而你已擁有實現它的工具。

---

![如何 OCR PDF 範例](image-placeholder.png "PDF 頁面 OCR 處理示意圖")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}