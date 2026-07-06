---
category: general
date: 2026-06-19
description: 如何在 C# 中使用 Aspose OCR 從圖像提取文字、對圖像執行 OCR 以及從掃描件識別文字——一步一步的指南。
draft: false
keywords:
- how to use aspose
- extract text from images
- run ocr on images
- recognize text from scans
language: zh-hant
og_description: 如何在 C# 中使用 Aspose OCR 從圖像提取文字、對圖像執行 OCR 以及從掃描件識別文字——完整指南。
og_title: 如何在 C# 中使用 Aspose OCR – 從影像中提取文字
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to use Aspose OCR in C# to extract text from images, run OCR on
    images, and recognize text from scans – step‑by‑step guide.
  headline: How to Use Aspose OCR in C# – Extract Text from Images
  type: TechArticle
tags:
- Aspose
- OCR
- C#
- Image Processing
title: 如何在 C# 中使用 Aspose OCR – 從圖片中提取文字
url: /zh-hant/net/text-recognition/how-to-use-aspose-ocr-in-c-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose OCR – 從圖像提取文字

Ever wondered **how to use Aspose** to pull words out of a photo of a document? You're not the first one scratching their head over that. In this tutorial we’ll walk through a practical, end‑to‑end example that shows you exactly how to extract text from images, run OCR on images in a batch, and even recognize text from scans with just a few lines of C#.

我們將先設定 Aspose OCR 引擎，然後提供一系列 JPEG 檔案，最後把每個結果印到主控台。完成後，你將擁有一段可直接放入任何 .NET 專案的可重用程式碼——沒有神祕步驟，也沒有遺漏的參考。

## 你需要什麼

在開始之前，請確保你已具備：

* .NET 6.0 SDK 或更新版本（此程式碼同時支援 .NET Core 與 .NET Framework）  
* 有效的 **Aspose.OCR** NuGet 套件（可從 Aspose 官網取得免費試用金鑰）  
* 包含數張掃描圖像或文字照片的資料夾（支援 JPEG 或 PNG）  
* 你慣用的 IDE——Visual Studio、Rider，或甚至 VS Code 都行。

就這樣。沒有龐大的 OCR 函式庫，沒有外部指令列工具。只要 Aspose 加上幾行程式碼即可。

## 第一步：安裝 Aspose.OCR NuGet 套件

在專案資料夾的終端機中執行：

```bash
dotnet add package Aspose.OCR
```

此指令會取得最新版本（截至 2026 年 6 月為 22.9）並將參考加入你的 `.csproj`。如果你偏好使用 Visual Studio UI，請右鍵點選 **Dependencies → Manage NuGet Packages**，搜尋 “Aspose.OCR”。

> **專業提示：** 留意授權到期日；免費試用可使用 30 天，之後需換成正式金鑰。

## 第二步：設定 OCR 引擎 – “How to Use Aspose” 從此開始

套件安裝完成後，讓我們建立 OCR 引擎並指定要辨識的語言。大多數情況下英文已足夠，但 Aspose 支援超過 70 種語言。

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;
using System.Collections.Generic;

// Configure the OCR engine to use English language
var ocrConfig = new OcrEngineConfig { Language = Language.English };
using var ocrEngine = new OcrEngine(ocrConfig);
```

為什麼要把 `OcrEngine` 包在 `using` 陳述式裡？因為它實作了 `IDisposable`。釋放會釋放 OCR 引擎在內部配置的原生資源（例如未受管理的記憶體）——這在每分鐘處理數十個檔案的生產服務中是必須的。

## 第三步：建立圖像路徑清單 – 為 **Run OCR on Images** 做好準備

接下來只要建立一個簡單的 `List<string>`，指向所有要處理的圖片。你可以像下方手動建立，或使用 `Directory.GetFiles` 動態產生。

```csharp
// Prepare a list of image file paths to be processed
var imagePaths = new List<string>
{
    @"C:\Scans\page1.jpg",
    @"C:\Scans\page2.jpg",
    @"C:\Scans\page3.jpg"
};
```

如果圖像位於執行檔相對的子資料夾，只要在那裡加入 `Path.Combine` 即可。關鍵是清單的順序會被保留——Aspose 會以相同的序列回傳結果，讓輸入與輸出對應變得非常簡單。

## 第四步：在單一批次 **Run OCR on Images**

當需要一次處理大量檔案時，Aspose OCR 的表現尤為突出。`ProcessBatch` 方法接受剛才建立的清單，回傳 `IList<OcrResult>`，其中每個元素都包含辨識文字、信心分數，甚至還有需要時的邊界框資訊。

```csharp
// Run OCR on the entire batch and obtain results in the same order
IList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imagePaths);
```

在底層，Aspose 會產生原生執行緒以加速處理，因此可隨 CPU 核心數接近線性擴展。若工作負載極大，你可以調整 `OcrEngineConfig.ThreadCount` 屬性，但預設的自動偵測在大多數桌面情境下已足夠。

## 第五步：顯示 **Recognized Text from Scans** – 驗證輸出

最後，我們遍歷結果並印出每段文字。同時回顯原始檔名，讓你一目了然哪段輸出屬於哪張掃描。

```csharp
// Iterate through the results and display the recognized text for each image
for (int i = 0; i < ocrResults.Count; i++)
{
    System.Console.WriteLine($"--- Result for {imagePaths[i]} ---");
    System.Console.WriteLine(ocrResults[i].Text);
}
```

執行程式時，主控台會顯示類似以下內容：

```
--- Result for C:\Scans\page1.jpg ---
Invoice #12345
Date: 06/15/2026
Total: $1,250.00

--- Result for C:\Scans\page2.jpg ---
Terms and Conditions
...
```

這就是 **how to use Aspose** 把一堆掃描的 PDF 或 JPEG 轉成可搜尋、可編輯文字的最佳範例。

![How to Use Aspose OCR example output](image-placeholder.png "How to Use Aspose OCR example output")

*Image alt text: “How to use Aspose OCR example output showing recognized text from scans.”*

## 可選：微調準確度 – 當 **Extract Text from Images** 需要加強時

如果發現缺字或文字亂碼，請嘗試以下調整：

| Setting | 功能說明 | 何時使用 |
|---------|----------|----------|
| `ocrConfig.DetectOrientation = true` | 自動旋轉側向的圖像 | 掃描書籍常為直式模式 |
| `ocrConfig.Preprocess = true` | 進行對比度增強與降噪 | 手機拍攝的低畫質照片 |
| `ocrConfig.CharacterWhitelist = "0123456789"` | 只辨識數字 | 抽取發票金額或序號 |
| `ocrEngine.SetPageSegmentationMode(PageSegMode.SingleBlock)` | 把整頁視為單一文字區塊 | 版面簡單且想要提升速度時 |

持續調整這些旗標，直到信心分數（可透過 `ocrResults[i].Confidence` 取得）超過 0.9。記得，來源圖像越清晰，OCR 結果就越好——在 Photoshop 或 ImageMagick 先做點前處理，能為你省下大量除錯時間。

## 完整範例 – 直接複製貼上

以下是可直接編譯執行的完整程式碼。只要把檔案路徑換成自己的資料夾即可。

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure the OCR engine (how to use Aspose OCR)
        var ocrConfig = new OcrEngineConfig
        {
            Language = Language.English,
            DetectOrientation = true,          // optional: auto‑rotate
            Preprocess = true                  // optional: improve low‑quality scans
        };
        using var ocrEngine = new OcrEngine(ocrConfig);

        // 2️⃣ List of image files (run OCR on images)
        var imagePaths = new List<string>
        {
            @"C:\Scans\page1.jpg",
            @"C:\Scans\page2.jpg",
            @"C:\Scans\page3.jpg"
        };

        // 3️⃣ Process the batch (extract text from images)
        IList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imagePaths);

        // 4️⃣ Show the results (recognize text from scans)
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Result for {imagePaths[i]} ---");
            Console.WriteLine(ocrResults[i].Text);
            Console.WriteLine($"Confidence: {ocrResults[i].Confidence:P2}");
            Console.WriteLine(); // blank line for readability
        }
    }
}
```

使用 `dotnet run` 編譯並執行，主控台會充滿乾淨、可搜尋的文字。這就是在 50 行程式碼內完成 **how to use aspose** 工作流程的全部內容。

## 常見問題與解決方式

* **NullReferenceException 於 `ocrResults[i]`** – 通常代表引擎無法開啟檔案（路徑錯誤、格式不支援）。請再次確認檔案副檔名與權限。  
* **出現雜訊字元** – 若看到 “�” 符號，可能是圖像使用非 UTF‑8 編碼。先將圖像轉成無損 PNG，或啟用 `ocrConfig.Preprocess`。  
* **效能瓶頸** – 若批次超過 100 張圖，考慮使用 `Parallel.ForEach` 並為每個執行緒建立獨立的 `OcrEngine` 實例。只要每個執行緒擁有自己的引擎，Aspose 即為執行緒安全。

## 往下走 – 深入探索

掌握了 **how to use Aspose** 進行 OCR 基礎後，你可能想進一步：

* **匯出為可搜尋 PDF** – 使用 `Aspose.Pdf` 把辨識文字嵌入 PDF，將掃描文件變成真正可搜尋的檔案。  
* **結合 Azure Functions** – 當新圖像上傳至 Azure Blob 時自動觸發 OCR。  
* **與 AI 語言模型結合** – 把抽出的文字送給 ChatGPT 或 Claude 進行摘要、實體抽取或翻譯。

上述主題皆自然包含我們的次要關鍵字——**extract text from images**、**run OCR on images**、**recognize text from scans**——讓你在擴展技能的同時，持續強化這些核心概念。

## 結論

我們已完整示範一個可投入生產環境的範例，回答了 **how to use Aspose** 以從圖像抽取文字、批次執行 OCR、以及辨識掃描文字的問題。只要設定引擎、建立檔案路徑清單、批次處理，並印出結果，你就擁有任何文件自動化專案的堅實基礎。

快試試看，微調設定旗標，讓你能把成山的紙本資料轉換成可搜尋的數位內容。


## 接下來該學什麼？

以下教學與本指南的技巧緊密相關，能幫助你進一步掌握 API 功能並探索其他實作方式：

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}