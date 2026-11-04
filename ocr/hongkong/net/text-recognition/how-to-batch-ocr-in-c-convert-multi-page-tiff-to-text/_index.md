---
category: general
date: 2026-03-28
description: 學習如何在 C# 中批次執行 OCR，輕鬆將 TIFF 轉換為文字。本一步一步的指南示範如何使用 Aspose OCR 從 TIFF 檔案提取文字。
draft: false
keywords:
- how to batch ocr
- convert tiff to text
- extract text from tiff
- c# ocr tutorial
language: zh-hant
og_description: 如何在 C# 中批次執行 OCR？請參考本完整教學，使用 Aspose OCR 將多頁 TIFF 檔案轉換為可搜尋的文字。
og_title: 如何在 C# 中批次 OCR – 將多頁 TIFF 轉換為文字
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中批次 OCR – 將多頁 TIFF 轉換為文字
url: /zh-hant/net/text-recognition/how-to-batch-ocr-in-c-convert-multi-page-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批量 OCR – 將多頁 TIFF 轉換為文字

有沒有想過 **如何批量 OCR** 一堆掃描頁面，而不必為每張圖片寫一個迴圈？你並不是唯一有此需求的人。在許多專案中——例如發票處理或檔案數位化——每天都會需要 **將 TIFF 轉換為文字**，而一次只處理一頁很快就會變成噩夢。

好消息是什麼？只要幾行 C# 程式碼加上 Aspose OCR，你就可以將整個多頁 TIFF 輸入引擎，並得到一個將頁碼對應到擷取文字的字典。在本教學中，我們將逐步示範完整且可執行的範例，說明 **如何批量 OCR**、**如何從 TIFF 擷取文字**，以及為什麼此方法優於手動方式。

## 您將學會

- 在 .NET 專案中設定 Aspose OCR 函式庫。  
- 使用 `Image.FromMultiPageFile` 載入多頁 TIFF 檔案。  
- 執行 `RecognizeBatch` 取得每頁結果的 `Dictionary<int,string>`。  
- 以整潔、易讀的格式列印輸出。  

完成後，你將擁有一個可直接執行的主控台應用程式，能將任何多頁 TIFF 轉換為純文字——不需要額外工具。  

### 前置條件

- .NET 6.0 SDK（或任何較新版本的 .NET）。  
- Visual Studio 2022 或 VS Code——你喜歡的 IDE 都可以。  
- 有效的 Aspose OCR 授權或免費評估金鑰（API 在未授權時仍可使用，但會加上浮水印）。  
- 一個名為 `multipage.tif` 的範例多頁 TIFF，放置於可參考的資料夾中。

> **小技巧：** 若你使用 Windows，預設的專案資料夾是放置 TIFF 的便利位置；在 Linux/macOS 上只需相應調整路徑即可。

## 步驟 1：安裝 Aspose OCR NuGet 套件

在撰寫任何程式碼之前，我們需要先取得 OCR 函式庫。於專案資料夾開啟終端機並執行以下指令：

```bash
dotnet add package Aspose.OCR
```

## 步驟 2：建立主控台應用程式骨架

讓我們快速搭建一個最小化的程式，引用 OCR 引擎。`using` 指示詞相當重要——若缺少它們，編譯器會抱怨找不到類型。

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Required for Image class
```

> **為什麼這很重要：** `Image` 類別位於子命名空間，若忘記匯入 `ImageProcessing`，會出現「找不到類型或命名空間」的錯誤，可能浪費一小時的除錯時間。

現在加入 `Main` 方法，並加上一段簡短的註解說明其目的：

```csharp
/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        // Implementation will go here
    }
}
```

## 步驟 3：初始化 OCR 引擎

`OcrEngine` 是核心工作馬。只建立一次並在所有頁面重複使用，既省記憶體又快速。

```csharp
// Step 3: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **底層在做什麼？** 引擎會載入語言模型並預先設定預設值（例如英文、自動旋轉）。你之後可以調整這些設定，但預設對大多數文件已相當適用。

## 步驟 4：載入多頁 TIFF

Aspose 讓載入多影格影像變得毫不費力。提供完整路徑或相對於執行檔工作目錄的路徑即可。

```csharp
// Step 4: Load a multi‑page TIFF image
string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // ← replace with your actual path
var multiPageImage = Image.FromMultiPageFile(tiffPath);
```

若找不到檔案，`FromMultiPageFile` 會拋出 `FileNotFoundException`。如果需要優雅的錯誤處理，可將其包在 `try/catch` 中——我們會在下一步示範。

## 步驟 5：執行批量 OCR

現在登場的是本教學的主角：`RecognizeBatch`。它會回傳一個 `Dictionary<int,string>`，鍵為頁面索引（從 0 開始），值則是辨識出的文字。

```csharp
// Step 5: Perform batch OCR on all pages
Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);
```

> **邊緣情況：** 有些 TIFF 可能包含空白頁面。Aspose 會為這些頁面回傳空字串，你可以在之後過濾掉，以免輸出雜亂。

## 步驟 6：顯示結果

最後，遍歷字典並印出每頁的文字。使用插值字串可讓程式碼保持整潔。

```csharp
// Step 6: Output the recognized text for each page
foreach (var pageResult in ocrResults)
{
    Console.WriteLine($"--- Page {pageResult.Key + 1} ---"); // +1 for human‑friendly numbering
    Console.WriteLine(pageResult.Value);
    Console.WriteLine(); // Blank line for readability
}
```

執行程式後應會產生類似以下的輸出：

```
--- Page 1 ---
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
...

--- Page 2 ---
Terms and Conditions
...
```

如果看到亂碼，請再次確認來源 TIFF 未損毀，且文字語言與引擎的預設語言（英文）相符。對於非英文文件，你也可以設定 `ocrEngine.Language = OcrLanguage.Spanish;`。

## 完整可執行範例

將所有部件組合起來，以下是完整程式碼，你可以直接複製貼上到 `Program.cs` 並執行：

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Needed for Image class

/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        try
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Load a multi‑page TIFF image
            string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // Change to your actual file location
            var multiPageImage = Image.FromMultiPageFile(tiffPath);

            // Step 3: Perform batch OCR on all pages
            Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);

            // Step 4: Output the recognized text for each page
            foreach (var pageResult in ocrResults)
            {
                Console.WriteLine($"--- Page {pageResult.Key + 1} ---");
                Console.WriteLine(pageResult.Value);
                Console.WriteLine(); // Extra line for visual separation
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

儲存、建置並執行：

```bash
dotnet run
```

你應該會在主控台看到每頁擷取的內容。這就是你所需求的完整 **c# ocr 教學**。

## 常見問題與邊緣情況

### 如果我的 TIFF 包含數十頁怎麼辦？

`RecognizeBatch` 會在一次呼叫中處理所有影格，但記憶體使用量會隨頁數線性增加。對於非常大的文件（數百頁），建議分批處理：

```csharp
for (int i = 0; i < multiPageImage.PageCount; i += 50)
{
    var subImage = multiPageImage.GetPages(i, Math.Min(50, multiPageImage.PageCount - i));
    var partialResults = ocrEngine.RecognizeBatch(subImage);
    // Merge partialResults into the main dictionary...
}
```

### 我可以將擷取的文字儲存為檔案而不是印出嗎？

當然可以。將 `Console.WriteLine` 區塊改為檔案 I/O：

```csharp
string outputFolder = "ExtractedText";
Directory.CreateDirectory(outputFolder);

foreach (var pageResult in ocrResults)
{
    string filePath = Path.Combine(outputFolder, $"Page_{pageResult.Key + 1}.txt");
    File.WriteAllText(filePath, pageResult.Value);
}
```

現在每頁都會產生自己的 `.txt` 檔案——非常適合後續索引。

### 如何變更輸出語言或啟用自動旋轉？

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
ocrEngine.AutoRotate = true;             // Detects rotated text automatically
```

這些設定必須在呼叫 `RecognizeBatch` **之前** 套用。

## 結論

我們已說明如何在 C# 中使用 Aspose OCR **批量 OCR** 多頁 TIFF。只要載入影像一次、呼叫 `RecognizeBatch`，再遍歷回傳的字典，即可在數秒內 **將 TIFF 轉換為文字**。此範例同時示範了 **從 TIFF 擷取文字**、錯誤處理，以及可選的將結果寫入檔案——全部在一個乾淨、獨立的主控台應用程式中完成。

準備好進一步了嗎？可以將此方法與 PDF 產生函式庫結合，產出可搜尋的 PDF，或將輸出接入資料庫以建立可搜尋的檔案庫。你也可以嘗試其他影像格式（PNG、JPEG），只需將 `Image.FromMultiPageFile` 改為 `Image.FromFile` 即可。

對 OCR、授權或效能調校還有其他問題嗎？在下方留言，我們會回覆。祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}