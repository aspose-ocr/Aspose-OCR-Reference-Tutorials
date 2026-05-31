---
category: general
date: 2026-05-31
description: 如何在 C# 中使用 Aspose OCR 進行批次 OCR。學習將圖像轉換為文字、從圖像中提取文字，並高效處理多個檔案。
draft: false
keywords:
- how to batch OCR
- convert images to text
- extract text from images
- OCR multiple files
- batch OCR processing
language: zh-hant
og_description: 如何在 C# 中使用 Aspose OCR 批量執行 OCR。將圖像轉換為文字，從圖像提取文字，輕鬆處理多個檔案的 OCR。
og_title: 如何在 C# 中批次 OCR – 完整程式設計指南
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  headline: How to Batch OCR in C# – Complete Programming Guide
  type: TechArticle
- description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  name: How to Batch OCR in C# – Complete Programming Guide
  steps:
  - name: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
    text: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
  - name: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
    text: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
  - name: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
    text: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- batch-processing
title: 如何在 C# 中批次執行 OCR – 完整程式設計指南
url: /zh-hant/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批次 OCR – 完整程式指南

有沒有想過 **如何批次 OCR** 整個資料夾的掃描圖片，而不必手動開啟每個檔案？你並不是唯一有此需求的人。在許多實務專案中——例如發票自動化或歷史照片的檔案保存——你需要 **大量將影像轉換為文字**，而逐一處理會耗費大量時間。

在本教學中，我們將一步步說明一個可直接執行的 C# 主控台應用程式，該程式會讀取來源目錄下的每個 PNG、JPG 或 TIFF，對每張圖片執行 Aspose OCR，並在輸出資料夾中產生相對應的 *.txt* 檔案。完成後，你將能熟練 **從影像擷取文字**、處理 **OCR 多檔案**，並擁有一個穩固的 **批次 OCR 處理** 基礎，供日後使用。

## 你將學到什麼

- 使用 Aspose OCR NuGet 套件建立 .NET 專案。  
- 為 **批次 OCR** 設定來源與目的資料夾。  
- 列舉支援的影像類型並將它們送入 OCR 引擎。  
- 將辨識出的文字寫入各自的 *.txt* 檔案，實際 **將影像轉換為文字**。  
- 解決常見問題，如資料夾不存在、格式不支援以及效能調校。

不需要事先具備 Aspose 的使用經驗，只要對 C# 與 Visual Studio 有基本了解即可上手。

---

![Diagram showing the flow of batch OCR processing from image folder to text output – how to batch OCR](/images/batch-ocr-flow.png){alt="批次 OCR 流程圖"}

## 如何批次 OCR – 建立專案

在開始撰寫程式碼之前，請先確保你已具備以下環境：

1. 已安裝 **.NET 6 SDK**（或更新版本）——較新的執行環境提供更佳效能與非同步 I/O 原生支援。  
2. **Visual Studio 2022**（Community 版亦可）或任意你喜歡的編輯器。  
3. **Aspose.OCR** NuGet 套件。於套件管理員主控台執行以下指令安裝：

   ```powershell
   Install-Package Aspose.OCR
   ```

完成以上步驟後，教學的後續內容皆假設套件已正確引用。

## 第 2 步：準備來源與目的資料夾（將影像轉換為文字）

首先，我們需要兩個資料夾：一個存放原始圖片，另一個放置產生的 *.txt* 檔案。以下程式碼會在目的資料夾不存在時自動建立——不需要手動操作。

```csharp
// Define where the images live and where the text files will go
string sourceFolder = @"C:\OCR\Batch";
string outputFolder = @"C:\OCR\BatchTxt";

// Ensure the output directory exists; CreateDirectory is idempotent
Directory.CreateDirectory(outputFolder);
```

> **為什麼重要：** 若省略 `CreateDirectory` 呼叫，程式在嘗試寫入第一個文字檔時會拋出 `DirectoryNotFoundException`。提前處理可讓批次 OCR 流程更穩定。

## 第 3 步：列舉要進行 OCR 多檔案的影像檔案

接著，我們取得所有符合支援格式的檔案。使用 LINQ 可讓程式碼簡潔且易讀。

```csharp
// Grab all PNG, JPG, and TIFF files from the source folder (non‑recursive)
var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
    .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));
```

> **小技巧：** 若日後需要支援 PDF 或 BMP，只要在 `Where` 子句中加入相應的副檔名即可。將過濾條件集中管理，可讓未來的調整更輕鬆。

## 第 4 步：對每張影像執行 OCR 引擎（如何批次 OCR）

現在進入核心：將每張影像送入 Aspose OCR，並取得辨識結果。以下迴圈會為每個檔案建立全新的 `OcrEngine` 實例——確保前一張影像佔用的記憶體在處理下一張之前已釋放。

```csharp
foreach (var imagePath in imageFiles)
{
    // Initialize the OCR engine with the current image
    OcrEngine ocrEngine = new OcrEngine
    {
        Image = ImageStream.FromFile(imagePath)
    };

    // Perform recognition; Recognize() returns an OcrResult object
    OcrResult ocrResult = ocrEngine.Recognize();

    // Build the output .txt file path (same base name, .txt extension)
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    // Persist the extracted text
    File.WriteAllText(textFilePath, ocrResult.Text);

    Console.WriteLine($"Processed {Path.GetFileName(imagePath)} → {Path.GetFileName(textFilePath)}");
}
```

**發生了什麼？**  

- `ImageStream.FromFile` 會將影像載入 Aspose 可讀取的串流。  
- `ocrEngine.Recognize()` 執行實際的 OCR 演算法，結果以 `ocrResult.Text` 形式回傳字串。  
- `File.WriteAllText` 把字串寫入磁碟，實際上 **從影像擷取文字**。

### 處理例外情況

- **損毀的影像** – 在辨識呼叫外層加上 `try/catch`，記錄失敗原因後繼續處理下一個檔案。  
- **大量批次** – 若使用多核心機器，可考慮以 `Parallel.ForEach` 以非同步方式處理檔案。  
- **不同語言** – 在呼叫 `Recognize()` 前設定 `ocrEngine.Language = Language.English;` 或其他支援的語言。

## 第 5 步：儲存擷取的文字（從影像擷取文字）

前面的程式碼已經將 OCR 輸出寫入檔案，現在把這段邏輯抽成一個輔助方法，讓主迴圈更簡潔，也方便重複使用。

```csharp
static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
{
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    File.WriteAllText(textFilePath, recognizedText);
}
```

接著把內嵌的 `File.WriteAllText` 呼叫換成：

```csharp
SaveOcrResult(outputFolder, imagePath, ocrResult.Text);
```

> **為什麼要抽成方法？** 這樣可以將「辨識」與「持久化」的職責分離，並提供一個單一位置來加入後處理（例如去除多餘空白或加入時間戳記）。

## 完整範例 – C# 批次 OCR 處理

將以下程式碼全部貼到新建的 Console App 專案中，即可直接執行。

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Define source & destination folders
            string sourceFolder = @"C:\OCR\Batch";
            string outputFolder = @"C:\OCR\BatchTxt";

            // 2️⃣ Make sure the output folder exists
            Directory.CreateDirectory(outputFolder);

            // 3️⃣ Get all supported image files (convert images to text)
            var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
                .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));

            // 4️⃣ Process each image (how to batch OCR)
            foreach (var imagePath in imageFiles)
            {
                try
                {
                    // Initialise OCR engine for the current file
                    OcrEngine ocrEngine = new OcrEngine
                    {
                        Image = ImageStream.FromFile(imagePath)
                    };

                    // Run OCR – this extracts text from images
                    OcrResult result = ocrEngine.Recognize();

                    // 5️⃣ Save the result (extract text from images)
                    SaveOcrResult(outputFolder, imagePath, result.Text);

                    Console.WriteLine($"✅ {Path.GetFileName(imagePath)} processed.");
                }
                catch (Exception ex)
                {
                    // Gracefully handle problematic files
                    Console.WriteLine($"⚠️ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }

            Console.WriteLine("🎉 Batch OCR processing complete!");
        }

        // Helper to write the OCR output to a .txt file
        static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
        {
            string textFilePath = Path.Combine(outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, recognizedText);
        }
    }
}
```

### 預期輸出

執行程式後，主控台會顯示類似以下的訊息：

```
✅ invoice001.png processed.
✅ receipt123.jpg processed.
✅ map.tif processed.
🎉 Batch OCR processing complete!
```

同時，`C:\OCR\BatchTxt` 資料夾會出現：

- `invoice001.txt`
- `receipt123.txt`
- `map.txt`

每個檔案皆為其來源影像的純文字表示，可供索引、搜尋或後續分析使用。

## 專業技巧與常見陷阱（批次 OCR 處理）

- **記憶體管理：** Aspose OCR 會在每次 `Recognize()` 後釋放影像緩衝區，但若處理上千檔案，建議適度呼叫 `GC.Collect()` 以降低記憶體佔用。  
- **效能提升：** 在 .NET 6 以上版本使用 `OcrEngine.RecognizeAsync()`，並搭配 `Task` 併發執行多個辨識任務。

## 接下來該學什麼？

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Perform OCR on Archive Images with Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}