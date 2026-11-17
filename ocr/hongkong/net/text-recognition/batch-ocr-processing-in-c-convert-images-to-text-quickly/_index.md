---
category: general
date: 2026-06-25
description: 批次 OCR 處理教學示範如何使用 Aspose.OCR 於 C# 將圖像轉換為文字並從圖像中擷取文字。學習一步一步的實作。
draft: false
keywords:
- batch ocr processing
- convert images to text
- how to extract text from images
language: zh-hant
og_description: 在 C# 中的批次 OCR 處理可讓您快速將圖像轉換為文字。請參考本指南，了解如何使用 Aspose.OCR 從圖像中提取文字。
og_title: C# 批次 OCR 處理 – 將圖像轉換為文字
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  headline: Batch OCR Processing in C# – Convert Images to Text Quickly
  type: TechArticle
- description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  name: Batch OCR Processing in C# – Convert Images to Text Quickly
  steps:
  - name: Expected Output
    text: 'When you run `dotnet run`, you’ll see something like:'
  - name: What image formats are supported?
    text: Aspose.OCR handles JPEG, PNG, TIFF, BMP, and GIF out of the box. If you
      encounter a format like WebP, convert it first or use a third‑party decoder.
  - name: Can I limit the OCR language to English only?
    text: 'Yes. Set the `Language` property on the `BatchRecognizer` before calling
      `Recognize`:'
  - name: How do I process thousands of files without blowing up memory?
    text: Break the list into smaller batches (e.g., 500 files each) and run the above
      routine in a loop. This keeps the in‑memory dictionary manageable and lets you
      log progress per batch.
  - name: What if I need the OCR results in a database instead of files?
    text: 'Replace the `File.WriteAllText` call with your preferred data‑access code.
      For example, using Dapper:'
  type: HowTo
tags:
- OCR
- Aspose
- C#
title: C# 批次 OCR 處理 – 快速將圖像轉換為文字
url: /zh-hant/net/text-recognition/batch-ocr-processing-in-c-convert-images-to-text-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# 批次 OCR 處理 – 快速將圖像轉換為文字

有沒有想過如何在不為每個檔案寫個別迴圈的情況下，對整個資料夾的掃描檔案進行 **batch OCR processing**？你並不是唯一有此需求的人。在許多專案中——例如發票自動化、舊文件歸檔，甚至是簡單的個人相片轉文字工具——都需要大量 **convert images to text**。

好消息是？使用 Aspose.OCR 只需幾行程式碼就能完成。此指南將帶領你完成一個完整、可直接執行的範例，示範如何使用 batch OCR processing **how to extract text from images**，說明每個部分的意義，並提供避免常見陷阱的技巧。

## 你將學到什麼

- 設定 Aspose.OCR 以支援批次操作。
- 設定平行度以加速大型工作。
- 自動將 OCR 結果寫入個別的 `.txt` 檔案。
- 處理進度事件，讓你隨時了解執行狀態。
- 擴充程式碼以支援自訂錯誤處理或不同的輸出格式。

不需要事先使用 Aspose 的經驗；只要具備基本的 C# 背景並已安裝 .NET 6（或更新版本）即可。

---

## 第一步：為批次 OCR 處理準備專案

在開始編寫程式碼之前，請確保已安裝 Aspose.OCR NuGet 套件。於專案資料夾中開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

> **專業提示：** 使用最新的穩定版（截至 2026 年 6 月為 23.9）以獲得效能提升與最新的語言支援。

如果尚未有專案，請建立新的主控台應用程式：

```bash
dotnet new console -n BatchOcrApp
cd BatchOcrApp
```

現在你已準備好撰寫實際的批次 OCR 處理邏輯。

## 第二步：定義要轉換的影像檔案

**batch OCR processing** 的第一步就是告訴辨識器要處理哪些檔案。你可以硬編碼清單、從目錄讀取，或甚至從資料庫取得路徑。為了說明，我們將使用靜態清單：

```csharp
// Step 2: List of image files to be processed
var imageFiles = new List<string>
{
    @"C:\Images\invoice1.jpg",
    @"C:\Images\receipt2.png",
    @"C:\Images\scan3.tif"
};
```

> **為什麼重要：** 透過傳遞集合，`BatchRecognizer` 能在內部跨多執行緒排程工作，這是快速 **convert images to text** 操作的核心。

## 第三步：建立並設定 BatchRecognizer

現在進入本教學的核心。`BatchRecognizer` 類別為你抽象化執行緒細節。你可以調整 `Parallelism` 屬性，以符合 CPU 核心數或自訂值，讓部分核心保留給其他工作使用。

```csharp
// Step 3: Initialise the BatchRecognizer with optional settings
var ocrBatch = new BatchRecognizer
{
    // Number of concurrent threads (default = Environment.ProcessorCount)
    Parallelism = 4,

    // Optional: Hook into progress events for real‑time feedback
    ProgressChanged = (s, e) =>
        Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
};
```

> **說明：** 設定 `Parallelism = 4` 代表庫會同時執行四個 OCR 工作。對於一般四核心筆記型電腦而言，可獲得不錯的加速且不會飽和系統。若在多核心伺服器上執行，可將此數值調高。

> **邊緣情況：** 若處理極大尺寸的影像，可能會觸及記憶體上限。此時請降低 parallelism 或將檔案分成較小的批次處理。

## 第四步：執行 OCR 並取得結果

對 `BatchRecognizer` 呼叫 `Recognize` 會回傳一個字典，鍵為原始檔案路徑，值為包含擷取文字、信心分數等資訊的 `OcrResult`。

```csharp
// Step 4: Execute batch OCR – returns a map of file → OcrResult
IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);
```

> **取得內容：** 每張影像的 `OcrResult.Text` 包含純文字表示。這正是以程式方式 **how to extract text from images** 時所需要的。

## 第五步：將每個結果寫入 .txt 檔案

大多數實務情境需要將 OCR 輸出保存以供後續處理——可能是匯入搜尋索引或附加至資料庫記錄。以下迴圈會在每個來源影像旁邊寫入 `.txt` 檔案，保留原始檔名。

```csharp
// Step 5: Write each OCR result to a corresponding .txt file
foreach (var entry in ocrResults)
{
    string txtPath = Path.ChangeExtension(entry.Key, ".txt");
    File.WriteAllText(txtPath, entry.Value.Text);
    Console.WriteLine($"Saved OCR text to {txtPath}");
}
```

> **提示：** 若需要其他格式（JSON、CSV 等），只要自行序列化 `entry.Value` 即可。`OcrResult` 物件亦提供 `Confidence` 與 `PageCount`，若你需要這些指標可加以使用。

## 第六步：標示完成並優雅地處理錯誤

乾淨的結束會讓你的工具更顯專業。範例程式碼已會印出最後一行訊息，但我們可以加入 try‑catch 區塊，以捕捉任何意外例外，例如檔案遺失或不支援的影像格式。

```csharp
try
{
    // (All steps 2‑5 go here)
    Console.WriteLine("Batch OCR processing finished successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
}
```

> **為何要包住：** 當在大型資料夾執行程式時，單一損壞的影像可能會導致整個工作中止。透過適當的錯誤處理，你可以記錄問題並繼續處理剩餘檔案。

## 完整、可直接執行的範例

以下是完整程式碼，你可以直接複製貼上到 `Program.cs`。請確保影像路徑指向你機器上的實際檔案。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchExample
{
    static void Main()
    {
        try
        {
            // Step 2: Define the image files to be processed
            var imageFiles = new List<string>
            {
                @"C:\Images\invoice1.jpg",
                @"C:\Images\receipt2.png",
                @"C:\Images\scan3.tif"
            };

            // Step 3: Create a BatchRecognizer and configure optional settings
            var ocrBatch = new BatchRecognizer
            {
                // Set the degree of parallelism (default = Environment.ProcessorCount)
                Parallelism = 4,

                // Hook into progress events to monitor processing
                ProgressChanged = (s, e) =>
                    Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
            };

            // Step 4: Run OCR on the batch of images (returns file → OcrResult)
            IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);

            // Step 5: Write each OCR result to a corresponding .txt file
            foreach (var entry in ocrResults)
            {
                string txtPath = Path.ChangeExtension(entry.Key, ".txt");
                File.WriteAllText(txtPath, entry.Value.Text);
                Console.WriteLine($"Saved OCR text to {txtPath}");
            }

            // Step 6: Indicate that batch processing has completed
            Console.WriteLine("Batch OCR processing finished successfully.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
        }
    }
}
```

### 預期輸出

執行 `dotnet run` 後，你會看到類似以下的結果：

```
Processed 1/3 – C:\Images\invoice1.jpg
Saved OCR text to C:\Images\invoice1.txt
Processed 2/3 – C:\Images\receipt2.png
Saved OCR text to C:\Images\receipt2.txt
Processed 3/3 – C:\Images\scan3.tif
Saved OCR text to C:\Images\scan3.txt
Batch OCR processing finished successfully.
```

每個 `.txt` 檔案現在都包含對應影像的純文字版本——正是大規模 **convert images to text** 所需的。

---

## 常見問題與邊緣情況

### 支援哪些影像格式？

Aspose.OCR 內建支援 JPEG、PNG、TIFF、BMP 與 GIF。若遇到 WebP 等格式，請先轉換或使用第三方解碼器。

### 能否僅限制 OCR 語言為英文？

是的。於呼叫 `Recognize` 前設定 `BatchRecognizer` 的 `Language` 屬性：

```csharp
ocrBatch.Language = "en";
```

限制語言可以提升準確度與速度，特別是當你只關注單一語言的 **how to extract text from images** 時。

### 如何在不耗盡記憶體的情況下處理數千個檔案？

將清單分割成較小的批次（例如每批 500 個檔案），在迴圈中執行上述程序。這樣可讓記憶體中的字典保持可管理，並能於每批次記錄進度。

### 若需將 OCR 結果寫入資料庫而非檔案該怎麼做？

將 `File.WriteAllText` 呼叫換成你偏好的資料存取程式碼。例如使用 Dapper：

```csharp
connection.Execute(
    "INSERT INTO OcrResults (FilePath, Text) VALUES (@Path, @Text)",
    new { Path = entry.Key, Text = entry.Value.Text });
```

---

## 結論

你剛剛已掌握使用 Aspose.OCR 在 C# 中的 **batch OCR processing**，學會了乾淨的 **convert images to text** 方法，並發現了多項實用技巧，以高效的方式 **how to extract text from images**。整個工作流程——收集檔案路徑、設定 `BatchRecognizer`、執行 OCR、保存結果——皆可寫成單一、易讀的程式。

接下來可以嘗試在多核心伺服器上提升 `Parallelism`、實驗語言套件，或加入拼寫檢查等後處理。你亦可探索將擷取的文字輸入 Azure Cognitive Search，讓掃描文件在數秒內即可搜尋。

有任何想法想分享——例如 OCR PDF 或處理多頁 TIFF？歡迎在下方留言，讓我們持續討論。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在此處示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [從資料夾使用 OCR 操作提取影像文字](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [如何在 Aspose.OCR for .NET 中使用清單批次 OCR 影像](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [如何使用 Aspose.OCR for .NET 從 ZIP 壓縮檔提取文字](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}