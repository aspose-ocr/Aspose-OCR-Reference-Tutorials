---
category: general
date: 2026-05-06
description: 使用 Aspose OCR 於 C# 建立可搜尋的 PDF。學習將 png 轉換為 pdf、從圖片提取文字並產生可搜尋的 PDF。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- convert png to pdf
- ocr image to pdf
language: zh-hant
og_description: 使用 Aspose OCR 於 C# 從圖像建立可搜尋的 PDF。本逐步教學示範如何將 PNG 轉換為 PDF、從圖像提取文字，並產生可搜尋的
  PDF。
og_title: 從圖像建立可搜尋的 PDF – C# Aspose OCR 指南
tags:
- Aspose
- C#
- OCR
- PDF
title: 從圖像建立可搜尋 PDF – C# Aspose OCR 指南
url: /zh-hant/net/text-recognition/create-searchable-pdf-from-image-c-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像建立可搜尋的 PDF – C# Aspose OCR 指南

是否曾需要從掃描的圖片 **建立可搜尋的 PDF**，卻不知從何著手？也許你有 PNG 格式的收據、合約的 JPEG，或任何想要轉換成可搜尋 PDF 的點陣圖。這是常見的痛點，尤其是當你面對放在資料夾中閒置的舊掃描檔時。

好消息是，使用 Aspose OCR 你可以 **convert image to PDF**，提取隱藏的文字，最終得到完整可搜尋的文件——只需幾行 C# 程式碼。本指南還會示範如何 **convert png to PDF**、**extract text from image**，甚至說明處理多頁 TIFF 的特殊情況。完成後，你將擁有一個可直接放入任何 .NET 專案的完整解決方案。

## 需要的環境

- **.NET 6+**（此程式碼亦可於 .NET Framework 4.6+ 上執行）
- **Visual Studio 2022** 或任何你偏好的 IDE
- **Aspose.OCR** NuGet 套件（會自動帶入 Aspose.PDF）
- 一個影像檔案（PNG、JPEG、BMP、TIFF），用於轉換成可搜尋的 PDF

不需要額外的授權技巧，也不需外部服務——只要一個 NuGet 參考，花上幾分鐘寫程式即可。

## 步驟 1：安裝 Aspose.OCR NuGet 套件

首先，將函式庫加入你的專案。開啟套件管理員主控台並執行以下指令：

```powershell
Install-Package Aspose.OCR
```

這條指令會同時下載 **Aspose.OCR** 與其相依的 **Aspose.Pdf** 組件，讓你同時能讀取影像與寫入 PDF。

> **小技巧：** 若使用 .NET CLI，等效指令為 `dotnet add package Aspose.OCR`。

## 步驟 2：初始化 OCR 引擎

建立 `OcrEngine` 的實例是所有 OCR 作業的入口。可以把它想像成會檢視圖片並「閱讀」文字的腦部。

```csharp
using Aspose.OCR;
using Aspose.Pdf;   // pulled in by the OCR package

// Create an OCR engine instance – this object holds configuration and state
var ocrEngine = new OcrEngine();
```

你可能會想，*為什麼不直接呼叫靜態方法？* 物件導向的方式讓你之後可以調整設定（語言、解析度等），而不必改變整體流程。

## 步驟 3：載入要轉換的影像

這裡就是以精神上 **convert image to PDF** 的方式——將位圖送入 OCR 引擎。將 `"YOUR_DIRECTORY/input.png"` 替換成實際檔案路徑。

```csharp
// Load the source image (PNG, JPEG, BMP, or multi‑page TIFF)
ocrEngine.SetImage("YOUR_DIRECTORY/input.png");
```

若是 **convert png to pdf** 的情況，只需指向 PNG 即可。對於多頁 TIFF，Aspose.OCR 會自動將每個影格視為獨立頁面。

## 步驟 4：執行 OCR 並選擇性取得文字

呼叫 `Recognize()` 會完成繁重的工作：分析圖片、偵測字元，並回傳結構化結果。你可以保留文字用於記錄、搜尋索引或顯示。

```csharp
// Perform OCR – this extracts the textual content from the image
var ocrResult = ocrEngine.Recognize();

// Optional: show the extracted text in the console
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

> **為什麼要提取文字？** 雖然最終會將文字嵌入 PDF，但保留原始字串對於驗證或分析仍很有用。

## 步驟 5：設定 PDF 選項以產生可搜尋文件

Aspose.PDF 提供一個特殊的 `PdfSaveOptions` 模式 **CreateSearchablePdf**。它指示函式庫將 OCR 文字以隱形圖層嵌入影像之後，使 PDF 可被搜尋。

```csharp
// Prepare PDF save options – this tells Aspose to embed OCR text
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();
```

若需要純影像 PDF（無隱藏文字），可以改用 `PdfSaveOptions.CreatePdf()`。但為了達成 **create searchable PDF** 的目標，可搜尋模式才是關鍵。

## 步驟 6：將可搜尋的 PDF 儲存至磁碟

現在把所有步驟串起來。`SavePdf` 方法會將影像與隱藏文字寫入同一個檔案。

```csharp
// Save the searchable PDF file
ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created successfully.");
```

此時你已擁有一個 **searchable PDF**，可在 Adobe Reader 中開啟，於搜尋框輸入關鍵字，即可立即跳至對應位置——即使可見頁面仍是原始影像。

## 完整範例程式

將所有片段組合起來，以下是一個可直接執行的主控台應用程式。將程式碼貼到新的 C# 專案，調整檔案路徑，然後按 **F5**。

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf; // included automatically with Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image that contains the scanned document
        // Replace with your actual image path
        ocrEngine.SetImage("YOUR_DIRECTORY/input.png");

        // Step 3: Run the OCR process to extract text (optional but useful)
        var ocrResult = ocrEngine.Recognize();

        // Show extracted text – helpful for debugging
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("======================");

        // Step 4: Prepare to export the recognized content as a searchable PDF
        var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

        // Step 5: Save the searchable PDF to disk
        // Replace with your desired output path
        ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created successfully.");
    }
}
```

### 預期輸出

執行程式時，主控台會顯示類似以下內容：

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑04‑30
Total: $1,250.00
...
======================
Searchable PDF created successfully.
```

在 `YOUR_DIRECTORY` 中會看到 `output.pdf`。開啟後，按 **Ctrl F**，輸入「Invoice」即可直接跳至該詞——即使頁面看起來只是平面掃描。

## 處理常見變化

### 同時轉換多張影像

若資料夾內有大量 PNG 且想產生單一可搜尋 PDF，可遍歷檔案並將每張加入為獨立頁面：

```csharp
var allImages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
var ocrEngine = new OcrEngine();
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

foreach (var imgPath in allImages)
{
    ocrEngine.SetImage(imgPath);
    ocrEngine.Recognize(); // extracts text for the current page
    ocrEngine.SavePdf("temp_page.pdf", pdfOptions);

    // Merge temp_page.pdf into the final document (omitted for brevity)
}
```

也可以使用 Aspose.PDF 的 `PdfFileEditor` 將暫存的 PDF 合併成最終檔案。

### 處理低解析度掃描

當影像 DPI 低於 150 時，OCR 的準確度會下降。可在送入影像前先將其放大：

```csharp
ocrEngine.ImageProcessingOptions.Dpi = 300; // forces 300 DPI for better recognition
```

### 指定特定語言

若文件不是英文，請在 `Recognize()` 前設定語言：

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, etc.
```

這些調整可確保 **extract text from image** 在各種情境下皆能可靠運作。

## 視覺結果

![Searchable PDF created with Aspose OCR – create searchable PDF](https://example.com/images/searchable-pdf.png)

*上圖顯示 PDF 中影像可見，但文字圖層可被搜尋。*

## 結論

現在你已擁有完整、可投入生產的食譜，能使用 Aspose OCR 與 C# 從任何影像 **create searchable PDF**。我們說明了如何 **convert image to PDF**、**extract text from image**，甚至涉及 **convert png to pdf** 與 **ocr image to pdf** 的特殊情況。程式碼完全自足，可在任何 .NET 執行環境上執行，亦可擴充為批次處理或自訂語言支援。

接下來可以嘗試加入浮水印、加密 PDF，或將提取的文字輸入搜尋索引（如 Elasticsearch）。可能性無窮，而相同的流程——載入 → 辨識 → 儲存——適用於任何 OCR 工作流程。

如果遇到任何問題或有有趣的使用案例想分享，歡迎在下方留言。祝開發順利，盡情將那些頑固的掃描檔變成可搜尋的寶藏！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}