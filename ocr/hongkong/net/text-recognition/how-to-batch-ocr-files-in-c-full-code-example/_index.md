---
category: general
date: 2026-02-17
description: 如何在 C# 中使用 Aspose OCR 批次對多個 PDF 和圖片進行 OCR。學習從 PDF 提取文字、將 PDF 轉換為文字，以及辨識圖片中的文字。
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: zh-hant
og_description: 如何在 C# 中使用 Aspose OCR 批次 OCR 多個文件。取得逐步程式碼，以從 PDF 提取文字、將 PDF 轉換為文字，並從圖像辨識文字。
og_title: 如何在 C# 中批次 OCR 檔案 – 完整指南
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: 如何在 C# 中批次 OCR 檔案 – 完整程式碼範例
url: /zh-hant/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中批次 OCR 檔案 – 完整指南

有沒有想過 **如何批次 OCR** 一堆 PDF 與影像掃描檔，而不必為每個檔案寫一個獨立的迴圈？你並不孤單。大多數開發者在一次需要從數十頁中擷取文字時，都會碰到這個障礙。好消息是？使用 Aspose OCR，你只要把檔案集合傳給單一引擎，就能讓它自行處理繁重的工作。

在本教學中，我們將示範一個實用的解決方案，讓你 **從 pdf 擷取文字**、**將 pdf 轉換為文字**，以及 **從影像辨識文字**，全部在一次批次執行。完成後，你將擁有一個可直接執行的 console 應用程式，會為每一頁印出 OCR 結果，並且了解每一步背後的原理，方便你自行套用到其他專案。

## 前置條件 – 開始前需要的項目

- **.NET 6.0 或更新版本**（程式碼在 .NET Framework 也可執行，但建議使用 .NET 6+）
- **Aspose.OCR NuGet 套件** – 使用 `dotnet add package Aspose.OCR` 安裝
- 兩個範例檔案：多頁 PDF（`doc1.pdf`）與掃描的 TIFF（`doc2.tif`）。請將它們放在可參照的資料夾，例如 `C:\OCRSamples`。
- 基本的 C# 知識 – 需要熟悉 `using` 陳述式與集合。

> 小技巧：如果沒有授權，Aspose 提供免費的臨時金鑰，可在開發期間移除 100 頁的限制。

## 步驟 1：建立專案並匯入命名空間

首先，建立一個新的 console 專案（或在現有專案中加入），然後匯入所需的命名空間。

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **為什麼重要：** 匯入 `Aspose.OCR.Image` 後，你可以使用便利的 `ImageStream.FromFile` 方法，該方法會自動將 PDF 頁面切割成獨立的影像串流。這就是讓批次處理變得輕鬆的祕密醬。

## 步驟 2：初始化 OCR 引擎

引擎是與底層 OCR 核心溝通的工作馬。整個批次只需要一個實例即可。

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **說明：** 重複使用同一個 `OcrEngine` 可以減少記憶體的頻繁分配，並加速處理，因為原生函式庫在頁面之間保持已載入狀態。

## 步驟 3：建立影像串流清單

在這裡我們收集所有要處理的文件。`ImageStream.FromFile` 足夠聰明，會把 PDF 拆成單頁影像串流，因此三頁的 PDF 會在背後變成三個獨立的串流。

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **邊緣案例：** 若同時有 PDF、TIFF、JPEG 或 PNG，只要把它們全部加入同一個清單，Aspose 會自動偵測格式。

## 步驟 4：執行批次 OCR 作業

現在把清單交給引擎。`RecognizeBatch` 會回傳 `OcrResult` 物件的集合，每個頁面對應一個結果。

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **為什麼使用批次？** 逐頁手動迴圈執行 OCR 會讓引擎每次都重新初始化，處理時間可能會加倍。`RecognizeBatch` 讓引擎保持熱態，並在結果可用時即時回傳。

## 步驟 5：輸出辨識文字

最後，我們遍歷結果，將每頁的文字寫入 console。此處你可以把 `Console.WriteLine` 換成寫檔、寫入資料庫或其他下游動作。

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### 預期的 Console 輸出

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

若使用範例檔案執行程式，你應該會看到每一頁都有一段文字，證明你已成功 **一次性擷取掃描 pdf 文字**。

## 常見問題處理

| 問題 | 為什麼會發生 | 快速解決方案 |
|------|--------------|--------------|
| **記憶體不足錯誤** | 大型 PDF 會產生大量高解析度影像。 | 載入 PDF 時限制 DPI：`ocrEngine.Settings.ImageDpi = 200;` |
| **出現雜訊字元** | 原始掃描品質低或使用了不支援的語言。 | 明確設定語言：`ocrEngine.Language = Language.English;` |
| **結果不完整** | 批次清單中有損毀的檔案。 | 在 `RecognizeBatch` 外層加上 try/catch，並記錄 `e.Message` 以找出問題檔案。 |
| **效能瓶頸** | 在多核心機器上只使用單一執行緒。 | 使用 `Parallel.ForEach`，為每個執行緒建立獨立的 `OcrEngine` 實例（進階）。 |

## 加分技巧：將 OCR 結果存成文字檔

如果想為每頁產生單獨的 `.txt` 檔，只要在迴圈內加入一小段寫檔程式碼：

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

現在你已把 **將 pdf 轉換為文字** 變成一個整齊的純文字檔資料夾——非常適合後續的索引或搜尋。

## 完整範例程式

以下是可直接複製貼上的完整程式碼，沒有隱藏的相依或外部腳本。

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

在專案資料夾執行 `dotnet run`，即可看到 console 被擷取的文字填滿。這就是 **如何批次 OCR** 一系列文件，只需要幾行 C# 程式碼。

## 我們學到了什麼 – 快速回顧

- 建立 .NET console 應用並安裝 Aspose.OCR。  
- 建立單一 `OcrEngine` 實例以提升效能。  
- 建立會自動將 PDF 拆頁的 `ImageStream` 清單。  
- 使用 `RecognizeBatch` **一次性從 pdf 擷取文字** 以及其他影像格式。  
- 印出結果，並可選擇將其儲存為個別的 `.txt` 檔，完成 **將 pdf 轉換為文字** 的工作流程。  

## 後續步驟與相關主題

- **規模化**：使用 `Parallel.ForEach` 搭配 `OcrEngine` 物件池，同時處理數百個檔案。  
- **語言套件**：將 `Language.English` 換成 `Language.French`，或在需要 **從影像辨識文字** 的其他語言時載入自訂字典。  
- **後處理**：將 OCR 輸出導入拼寫檢查或自然語言解析器，以提升掃描合約的準確度。  
- **其他函式庫**：若想找開源方案，可比較 Aspose OCR 與 Tesseract.NET——兩者都能 **擷取掃描 pdf 文字**，但授權與即時準確度有所不同。

---

![如何批次 OCR 示例](alt="how to batch OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}