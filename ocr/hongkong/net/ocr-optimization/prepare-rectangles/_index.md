---
date: 2026-07-23
description: 了解如何使用 Aspose.OCR for .NET 從圖像提取文字，透過設定矩形提升 OCR 準確度，並高效將圖像轉換為文字。
keywords:
- extract text from image
- convert image to text
- improve ocr accuracy
lastmod: 2026-07-23
linktitle: 在 OCR 圖像辨識中設定矩形
og_description: 使用 Aspose.OCR for .NET 從圖像提取文字。了解如何設定矩形、提升 OCR 準確度，並高效將圖像轉換為文字。
og_image_alt: Guide to extract text from image using rectangles with Aspose.OCR for
  .NET
og_title: 使用矩形提取圖像文字 – OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from image using Aspose.OCR for .NET, preparing
    rectangles to improve OCR accuracy and convert image to text efficiently.
  headline: Extract Text from Image with Rectangles – OCR Guide
  type: TechArticle
- questions:
  - answer: It converts visual characters in a picture into machine‑readable strings.
    question: What does “extract text from image” mean?
  - answer: Aspose.OCR for .NET provides a full‑featured OCR engine.
    question: Which library handles this in .NET?
  - answer: A free trial works for development; a commercial license is required for
      deployment.
    question: Do I need a license for production?
  - answer: Yes—define rectangles to target only the areas that contain useful text.
    question: Can I limit OCR to specific zones?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: What .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr
- Aspire.OCR
- .NET image processing
- extract text from image
title: 使用矩形提取圖像文字 – OCR 指南
url: /zh-hant/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用矩形從圖像提取文字 – OCR 指南

## 介紹

光學字符識別（OCR）讓您 **從圖像提取文字** 檔案，使其可搜尋且可編輯。在本教學中，我們將示範如何透過自訂矩形來提升 OCR 準確度，將引擎聚焦於您需要的精確區域。使用 Aspose.OCR for .NET，您將看到完整的工作流程——從專案設定到取得辨識字串——讓您能在任何 .NET 應用程式中嵌入可靠的圖像轉文字功能。

## 快速解答
- **什麼是「從圖像提取文字」？** 它將圖片中的視覺字符轉換為機器可讀的字串。  
- **哪個函式庫在 .NET 中處理此功能？** Aspose.OCR for .NET 提供完整功能的 OCR 引擎。  
- **生產環境需要授權嗎？** 免費試用可用於開發；部署時需購買商業授權。  
- **我可以將 OCR 限制在特定區域嗎？** 可以——定義矩形以僅針對包含有用文字的區域。  
- **支援哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。

## 什麼是使用矩形的「從圖像提取文字」？
`extract text from image` 流程會讀取定義的矩形區域內的字符，忽略其他部分。將 OCR 限制於這些區域可提升準確度、加快處理速度，並減少後處理工作。此方法可將您關注的文字孤立，同時剔除背景圖形、裝飾元素及其他可能干擾 OCR 引擎的視覺雜訊。

## 為什麼在 OCR 前先準備矩形？
準備矩形可讓 OCR 引擎聚焦於圖像中最相關的部分，從而提升速度與精確度。透過縮小分析區域，可減少引擎需檢查的資料量，進而得到更快速的結果，並降低因多餘視覺雜訊導致的誤辨識。

- **聚焦於相關內容：** 跳過會干擾引擎的標頭、頁腳或裝飾圖形。  
- **提升效能：** 較小的區域需要較少計算，可在大型掃描上將執行時間縮短最高 40%。  
- **提高準確度：** 減少視覺雜訊可將噪聲文件的字符辨識率從約 85% 提升至超過 95%。

## 為何此在實務專案中重要
許多商業文件——收據、發票、身分證——文字與標誌或條碼混雜。透過在實際需要的欄位周圍繪製矩形，您僅提取有價值的資料，減少後續清理工作，提升自動化工作流程的可靠性。此目標式提取降低後處理工作量，並有助於遵守資料處理標準。

## 常見使用情境
- **資料輸入自動化：** 從掃描表單或費用收據中提取特定欄位。  
- **合規性檢查：** 隔離法律條款或規範聲明以進行驗證。  
- **內容索引：** 僅索引圖像的標題或說明文字，以提升搜尋引擎可見度。

## 前置條件

- 具備 C# 與 .NET 開發的基本知識。  
- 已安裝 Aspose.OCR for .NET 函式庫 – 於 **[此處](https://releases.aspose.com/ocr/net/)** 下載，或於 **[此處](https://releases.aspose.com/)** 瀏覽所有版本。  
- 一張包含您想提取文字的示例圖像（例如 `sample.png`）。

## 匯入命名空間

`using` 陳述式將 OCR 引擎與幾何類別引入作用域。

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 步驟 1：設定文件目錄

指定保存圖像的資料夾，並建立 OCR 引擎的實例。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 如何使用多個矩形從圖像提取文字

先載入圖像一次，然後將矩形清單傳遞給 OCR 引擎。每個矩形定義一個感興趣的區域，引擎會為每個區域返回獨立的字串，讓您能個別處理欄位並根據需要合併結果。

### 定義矩形

`Rectangle` 物件描述您想掃描的每個區域的 X‑Y 座標與大小。  

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### 執行 OCR 辨識

`RecognizeImage` 方法使用提供的矩形清單處理圖像，並返回每個區域的辨識文字。  

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## 如何使用 RecognitionSettings 從圖像提取文字（替代方法）

如果您偏好基於設定的呼叫，可使用 `RecognitionSettings` 取得相同結果。此物件允許您將矩形定義與語言、DPI 及其他 OCR 選項一起打包，提供簡潔的單參數 API 呼叫。

### 定義辨識設定

`RecognitionSettings` 讓您將矩形清單與其他選項（例如語言、DPI）打包成單一物件。  

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 顯示辨識文字

遍歷返回的字串，輸出每個區域的文字。  

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## 常見問題與技巧

- **矩形座標不正確：** 請確認 `X`、`Y`、`Width` 與 `Height` 對應到預期區域。  
- **影像品質：** 低解析度或高度壓縮的圖像會降低 OCR 結果，建議進行二值化等前處理。  
- **結果為空：** 確認矩形內實際包含可讀文字，否則引擎會返回空字串。

## 疑難排解與最佳實踐

| 症狀 | 可能原因 | 解決方法 |
|------|----------|----------|
| 無輸出或空字串 | 矩形超出圖像範圍 | 再次檢查圖像尺寸與矩形座標 |
| 文字亂碼 | 對比度差或有雜訊 | 在 OCR 前先轉為灰階並進行閾值化 |
| 大檔案執行緩慢 | 矩形過多或圖像過大 | 如可能，將圖像分割或減少矩形數量 |

## 結論

您現在已了解如何透過使用 Aspose.OCR for .NET 準備自訂矩形來 **從圖像提取文字**。此方法讓您精確控制 OCR 處理，為任何 .NET 解決方案提供更快速、更準確的文字提取功能。

## 常見問答

**Q:** 我可以將 Aspose.OCR for .NET 與其他 .NET 框架一起使用嗎？  
**A:** 可以，Aspose.OCR for .NET 支援 .NET Framework 4.5+、.NET Core 3.1+ 以及 .NET 5/6/7。

**Q:** 是否提供免費試用？  
**A:** 當然！請於 **[此處](https://releases.aspose.com/)** 下載試用版。

**Q:** 在哪裡可以取得 Aspose.OCR for .NET 的支援？  
**A:** 前往 **[Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16)** 獲得專業協助。

**Q:** 我可以取得測試用的臨時授權嗎？  
**A:** 可以，臨時授權可於 **[此處](https://purchase.aspose.com/temporary-license/)** 取得。

**Q:** 官方文件在哪裡？  
**A:** 完整的 API 參考位於 **[此處](https://reference.aspose.com/ocr/net/)** 。

---

**最後更新：** 2026-07-23  
**測試版本：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< blocks/products/products-backtop-button >}}

## 相關教學

- [如何在 OCR 圖像辨識中提取段落的矩形](/ocr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/)
- [如何 OCR 圖像 – 在 OCR 圖像辨識中執行圖像 OCR](/ocr/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [如何使用 Aspose.OCR for .NET 從圖像提取文字](/ocr/net/text-recognition/get-recognition-result/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}