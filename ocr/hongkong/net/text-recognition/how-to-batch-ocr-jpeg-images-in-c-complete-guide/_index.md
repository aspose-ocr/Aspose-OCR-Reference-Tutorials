---
category: general
date: 2026-02-22
description: 如何在 C# 中使用 Aspose.OCR 批次 OCR JPEG 圖像。學習從 jpg 提取文字、將 jpg 轉換為 txt，並高效批量處理圖像。
draft: false
keywords:
- how to batch ocr
- extract text from jpg
- convert jpg to txt
- batch process images
- c# ocr example
language: zh-hant
og_description: 如何在 C# 中使用 Aspose.OCR 批次 OCR JPEG 圖像。本教程示範如何從 jpg 提取文字、將 jpg 轉換為 txt，並在數分鐘內批次處理圖像。
og_title: 如何在 C# 中批次 OCR JPEG 圖片 – 完整指南
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中批量 OCR JPEG 圖像 – 完整指南
url: /zh-hant/net/text-recognition/how-to-batch-ocr-jpeg-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR JPEG 圖像 – 完整指南

有沒有想過 **如何批量 OCR** 一個充滿圖片的資料夾，而不必為每個檔案寫一個單獨的程式？在本指南中，我們將示範如何使用 Aspose.OCR **批量 OCR** JPEG 檔案，讓您只需幾行程式碼即可 **從 jpg 提取文字** 並 **將 jpg 轉換為 txt**。  

如果您曾經盯著一個掃描發票的目錄，心想「一定有更快的方法」的話，您來對地方了。我們會逐步說明每個步驟，解釋每個環節的重要性，並提供一些處理大批量的專業小技巧。

## 您將建立的內容

到本教學結束時，您將擁有一個小型主控台應用程式，能夠：

* 掃描指定目錄中的 `*.jpg` 檔案。  
* 將每張圖片送入 Aspose OCR 引擎（若有相容的顯示卡則使用 GPU 加速）。  
* 將辨識出的文字寫入與原圖相同目錄下的 `.txt` 檔案。  

不需要外部服務，也不需要手動複製貼上——只需純粹的 C# 與可靠的 OCR 函式庫。

### 前置條件

* .NET 6.0 或更新版本（程式碼亦可在 .NET Framework 4.8 上執行）。  
* Visual Studio 2022 或任何支援 C# 的編輯器。  
* Aspose.OCR NuGet 套件（免費試用版可用於測試）。  

如果缺少上述任一項，請先暫停並安裝；本指南的其餘部分假設它們已就緒。

![How to batch OCR example](/images/how-to-batch-ocr.png "how to batch ocr diagram")

## 第一步：安裝 Aspose.OCR NuGet 套件

首先，您的專案需要 OCR 函式庫。於解決方案資料夾開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

或在 Visual Studio 中使用 NuGet 套件管理員 UI。這會下載所有必要的檔案，包括若機器支援則的 GPU 加速二進位檔。

> **專業提示：** 若您打算在沒有 GPU 的伺服器上執行，之後將 `UseGpu = false`；引擎會自動回退至 CPU。

## 第二步：設定 OCR 引擎

建立並設定 `OcrEngine` 即是魔法開始的地方。您需要告訴引擎預期的語言、是否使用 GPU，以及輸出格式。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 2: Initialize and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most documents; change if you need another language.
    Language = Language.English,

    // Enable GPU for faster processing on supported hardware.
    UseGpu = true,

    // We only need plain text for our .txt files.
    OutputFormat = OutputFormat.Text
};
```

**為什麼這很重要：** 設定 `Language` 可提升準確度，因為引擎能縮小字元集範圍。啟用 `UseGpu` 在現代顯示卡上可將處理時間減半，對於 **批量處理圖像** 來說是極大的優勢。

## 第三步：辨識資料夾中的所有 JPEG 檔案

現在讓 Aspose 承擔繁重工作。靜態的 `BatchProcessor.RecognizeFolder` 方法會遍歷目錄，對每個符合的檔案執行 OCR，並回傳結果集合。

```csharp
using System.Collections.Generic;

// ...

// Step 3: Run OCR on every *.jpg in the target directory
IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
    ocrEngine,
    @"C:\Images\Invoices",   // <-- replace with your folder path
    searchPattern: "*.jpg"); // Only JPEG files are processed
```

**邊緣案例處理：** 若資料夾內含子資料夾，可加入 `SearchOption.AllDirectories` 的重載（或自行遞迴），以確保不遺漏任何檔案。

## 第四步：將每個結果寫入對應的 `.txt` 檔案

`OcrResult` 物件包含原始檔案路徑與辨識文字。遍歷它們，變更副檔名，並寫入輸出。

```csharp
using System.IO;

// ...

// Step 4: Persist OCR results as .txt files next to the source images
foreach (var result in ocrResults)
{
    // Change "image.jpg" → "image.txt"
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");

    // Save the extracted text
    File.WriteAllText(txtFilePath, result.Text);
}
```

就這樣——每個 JPEG 現在都有一個同名的文字檔，您可以將其輸入後續流程、搜尋索引，或僅作為存檔使用。

## 第五步：執行應用程式並驗證輸出

編譯並執行程式：

```bash
dotnet run
```

假設資料夾內有 `invoice1.jpg` 與 `receipt2.jpg`，您應該會看到 `invoice1.txt` 與 `receipt2.txt` 伴隨在旁。開啟任一 `.txt` 檔案，即可看到原始 OCR 輸出，例如：

```
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

若文字顯示為亂碼，請再次確認來源影像具高對比度，且 `Language` 屬性與文件語言相符。

## 第六步：進階調整（可選）

### a) 處理低品質掃描

有時 JPEG 會有噪點。您可以使用 Aspose.Imaging 或其他函式庫先行前處理影像：

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

// Example: increase contrast before OCR
using (var image = Image.Load(result.SourceFilePath))
{
    image.Contrast = 30; // boost contrast
    image.Save(result.SourceFilePath); // overwrite or save to temp file
}
```

### b) 批次平行化

若檔案眾多且具多核心 CPU，可將迴圈包在 `Parallel.ForEach` 中：

```csharp
Parallel.ForEach(ocrResults, result =>
{
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
    File.WriteAllText(txtFilePath, result.Text);
});
```

請注意 Aspose OCR 引擎本身不是執行緒安全的；您需要為每個執行緒建立獨立的 `OcrEngine` 實例，或使用併發佇列。

### c) 日誌與錯誤處理

健全的解決方案會記錄失敗，以便稍後重試：

```csharp
try
{
    // OCR and write logic here
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {result.SourceFilePath}: {ex.Message}");
    // Optionally write to a log file
}
```

## 完整範例程式

將所有部份整合起來，以下是您可以直接複製貼上至新 Console App 的完整程式：

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create and configure the OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = Language.English,
            UseGpu = true,
            OutputFormat = OutputFormat.Text
        };

        // 2️⃣ Recognize all JPEG images in the target folder
        IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
            ocrEngine,
            @"C:\Images\Invoices",   // <-- change to your directory
            searchPattern: "*.jpg");

        // 3️⃣ Write each OCR result to a matching .txt file
        foreach (var result in ocrResults)
        {
            string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
            File.WriteAllText(txtFilePath, result.Text);
        }

        Console.WriteLine("Batch OCR complete. Check the folder for .txt files.");
    }
}
```

執行它，觀察主控台輸出，然後開啟幾個 `.txt` 檔案，以確認 **從 jpg 提取文字** 步驟已成功。  

---

## 結論

我們剛剛說明了如何在 C# 中使用 Aspose.OCR **批量 OCR** JPEG 圖像，將每張圖片轉換為可搜尋的 `.txt` 檔案。此解決方案簡潔、支援 GPU，且易於擴充以加入錯誤處理、影像前處理或平行執行。  

如果您想更進一步，可考慮以下下一步：

* **批量處理其他格式** 的影像（如 `*.png`、`*.tif`），只需調整 `searchPattern`。  
* 將輸出結合 Lucene.NET 等全文搜尋引擎，以即時文件查找。  
* 探索 Aspose 的 PDF 轉換功能，直接從 OCR 結果產生可搜尋的 PDF。  

盡情實驗吧——更換語言、關閉 GPU，或將文字導入資料庫。核心模式保持不變，現在您已擁有堅實的基礎可供構建。祝程式開發順利，願您的 OCR 流程始終快速且精確！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}