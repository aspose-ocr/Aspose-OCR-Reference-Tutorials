---
category: general
date: 2026-01-10
description: 使用 Aspose OCR 於 C# 從圖像提取文字。了解如何使用批次處理轉換掃描文件的文字並儲存結果。
draft: false
keywords:
- extract text from image
- convert scanned document text
- batch OCR processing
- Aspose OCR
- C# OCR tutorial
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中從圖像提取文字。本教學示範如何透過批次處理將掃描文件的文字轉換。
og_title: 從圖像中提取文字（C#）– 完整 Aspose OCR 指南
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 在 C# 中從圖像提取文字 – 完整的 Aspose OCR 指南
url: /zh-hant/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從影像中擷取文字 – 完整 Aspose OCR 教學

是否曾需要 **從影像中擷取文字**，卻不知從何下手？你並不孤單；許多開發者在處理掃描 PDF、多頁 TIFF 或以相片形式的收據時，都會碰到這個問題。好消息是，使用 Aspose OCR，你只需幾行 C# 程式碼，就能 **將掃描文件的文字轉換** 出來。

在本教學中，我們將示範一個真實情境：取得多頁 TIFF，對每一頁執行批次 OCR，並寫入一個包含所有頁面內容的文字檔。完成後，你將擁有一個可直接執行的主控台應用程式，了解每個步驟的意義，並知道如何針對密碼保護的影像或自訂語言套件等邊緣案例進行調整。

## 前置條件

- .NET 6.0 SDK 或更新版本（此程式碼同樣適用於 .NET Core 與 .NET Framework）  
- Visual Studio 2022（或任何你慣用的編輯器）  
- Aspose OCR 授權檔（或使用免費評估模式）  
- 一個多頁影像檔（例如 `multipage.tif`），放在可參考的資料夾中  

除了 `Aspose.OCR` 之外，無需其他 NuGet 套件，我們會在第一步安裝它。

## 第一步 – 安裝 Aspose OCR 並建立專案

首先，建立一個新的主控台專案，並加入 Aspose OCR 函式庫。

```bash
dotnet new console -n ImageTextExtractor
cd ImageTextExtractor
dotnet add package Aspose.OCR
```

> **專業提示：** 若你有授權檔 (`Aspose.OCR.lic`)，請將它複製到專案根目錄。函式庫會在執行時自動載入。

為什麼要這麼做？安裝套件後，你即可使用 `BatchProcessor`、`OcrEngine` 等便利類別，免除低階影像處理的麻煩；同時也確保使用 Aspose 最新的 OCR 演算法。

## 第二步 – 使用 BatchProcessor 載入多頁影像

`BatchProcessor` 正是為此情境設計：在不必手動切割檔案的情況下，逐頁遍歷多頁影像。

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System.Text;

// Step 2: Initialize the batch processor with the path to your TIFF
var batchProcessor = new BatchProcessor(@"YOUR_DIRECTORY\multipage.tif");

// Verify that pages were loaded
if (batchProcessor.Pages.Count == 0)
{
    Console.WriteLine("No pages found – double‑check the file path.");
    return;
}
```

`BatchProcessor` 會將所有頁面讀入記憶體，透過 `batchProcessor.Pages` 取得。每個頁面物件都有其編號 (`ocrPage.Number`)，稍後會用來產生清晰的標題。

## 第三步 – 建立 StringBuilder 以累積結果

我們希望產生一個包含所有頁面 OCR 輸出的單一文字檔，並以標題分隔。`StringBuilder` 是在迴圈中串接字串的最佳效能選擇。

```csharp
// Step 3: Create a StringBuilder to collect OCR results
var extractedText = new StringBuilder();
```

為什麼使用 `StringBuilder`？在迴圈內使用 `+` 直接串接字串會在每次迭代時產生新字串，造成大量記憶體分配，對大型文件的效能影響尤為明顯。

## 第四步 – 逐頁執行 OCR 並加入結果

現在進入教學的核心：遍歷每一頁、辨識文字，並以頁碼標記儲存。

```csharp
// Step 4: Process each page individually
foreach (var ocrPage in batchProcessor.Pages)
{
    // Create a fresh OcrEngine for every page – this isolates settings
    var ocrEngine = new OcrEngine
    {
        Image = ocrPage
    };

    // Perform recognition
    ocrEngine.Recognize();

    // Append a clear header and the recognized text
    extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
    extractedText.AppendLine(ocrEngine.Text);
}
```

**為什麼每頁都要建立新的 `OcrEngine`？** 有些開發者會重複使用同一個引擎並更改其 `Image` 屬性，但這樣可能會保留先前的語言設定或結果，導致細微錯誤。每次重新實例化可確保環境乾淨。

### 處理常見邊緣案例

- **空白頁面：** 若頁面無可辨識文字，`ocrEngine.Text` 會是空字串。你可以插入佔位文字，例如 “(未偵測到文字)”。
- **語言選擇：** 預設 Aspose OCR 使用英文。若要處理德文或法文，可在呼叫 `Recognize()` 前設定 `ocrEngine.Language = Language.German;`。
- **效能小技巧：** 對於巨大的 TIFF，可啟用 `ocrEngine.UseParallelProcessing = true;` 以利用多核心。

## 第五步 – 將合併結果寫入文字檔

最後，將累積的字串寫入磁碟。

```csharp
// Step 5: Save the result to a .txt file
string outputPath = @"YOUR_DIRECTORY\multipage_result.txt";
File.WriteAllText(outputPath, extractedText.ToString());

Console.WriteLine($"OCR complete! Results saved to {outputPath}");
```

產生的 `multipage_result.txt` 會類似以下內容：

```
--- Page 1 ---
This is the first page of the scanned document.
It contains a title and some introductory text.

--- Page 2 ---
Continuation of the report.
Data tables and figures follow.
```

現在你已 **從影像中擷取文字**，並成功 **將掃描文件的文字轉換** 為可搜尋、可編輯的格式。

## 加分 – 視覺概覽（圖片替代文字）

以下是一張簡易流程圖，說明整個處理過程。  
*替代文字：*「圖示說明如何使用 Aspose OCR 批次處理在 C# 中從影像擷取文字的流程」。

![OCR Flow Diagram](placeholder-image-url.png)

*（若你在靜態網站上發佈本教學，請將佔位圖換成實際的 SVG 或 PNG。）*

## 常見問題

**這能處理 PDF 檔嗎？**  
可以，Aspose OCR 能將 PDF 頁面當作影像讀取。你只需要先將 PDF 轉成影像，或使用 `Aspose.PDF` 的 `PdfDocument`，將每頁的光柵化影像傳給 `OcrEngine`。

**如果我的 TIFF 有密碼保護怎麼辦？**  
`BatchProcessor` 本身不支援加密。請先使用如 `Aspose.Imaging` 等函式庫解密，然後再交給 OCR 流程。

**可以輸出 JSON 而非純文字嗎？**  
完全可以。只要把 `StringBuilder` 的邏輯換成 JSON 序列化（例如 `System.Text.Json`），將每頁文字存入 `pageNumber` 鍵即可。

## 完整範例程式

以下是可直接貼到 `Program.cs` 的完整程式碼，包含所有 using 指令、錯誤處理與註解。

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Text;

namespace ImageTextExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            string inputImagePath = @"YOUR_DIRECTORY\multipage.tif";
            string outputTextPath = @"YOUR_DIRECTORY\multipage_result.txt";

            // 1️⃣ Load the multi‑page image
            var batchProcessor = new BatchProcessor(inputImagePath);
            if (batchProcessor.Pages.Count == 0)
            {
                Console.WriteLine("No pages detected – verify the file path.");
                return;
            }

            // 2️⃣ Prepare a StringBuilder for the final output
            var extractedText = new StringBuilder();

            // 3️⃣ Process each page
            foreach (var ocrPage in batchProcessor.Pages)
            {
                var ocrEngine = new OcrEngine
                {
                    Image = ocrPage,
                    // Uncomment to change language:
                    // Language = Language.German,
                    // UseParallelProcessing = true
                };

                // Run OCR
                ocrEngine.Recognize();

                // Append header and text
                extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
                // Guard against empty results
                string pageText = string.IsNullOrWhiteSpace(ocrEngine.Text)
                    ? "(No text detected on this page)"
                    : ocrEngine.Text;
                extractedText.AppendLine(pageText);
            }

            // 4️⃣ Write to file
            File.WriteAllText(outputTextPath, extractedText.ToString());

            Console.WriteLine($"✅ Extraction complete. File saved at: {outputTextPath}");
        }
    }
}
```

執行程式：

```bash
dotnet run
```

你應該會在主控台看到成功訊息，且輸出檔案會包含合併後的 OCR 結果。

## 結論

我們剛剛示範了如何使用 Aspose OCR **從影像中擷取文字**，將任何多頁掃描檔轉換為純文字、可搜尋的內容。透過 `BatchProcessor` 與每頁獨立的 `OcrEngine` 設定，你可以可靠地 **將掃描文件的文字轉換**，同時保持程式碼簡潔易維護。

歡迎自行嘗試：更換語言、改為 JSON 輸出，或將此邏輯整合到即時處理上傳檔案的 Web API。核心模式不變——載入、辨識、累積、持久化。

對 OCR、Aspose 授權或大量文件批次處理有更多疑問嗎？歡迎在下方留言，或參考 Aspose 官方文件深入了解。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}