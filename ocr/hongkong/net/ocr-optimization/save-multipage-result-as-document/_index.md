---
date: 2025-12-30
description: 學習如何使用 Aspose.OCR 以 C# 將圖像轉換為 PDF、將多頁 OCR 結果儲存為文件，以及以 C# 從圖像中提取文字。
linktitle: Convert Images to PDF C# – Save Multipage OCR Result
second_title: Aspose.OCR .NET API
title: 將圖像轉換為 PDF C# – 保存多頁 OCR 結果
url: /zh-hant/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將影像轉換為 PDF C# – 儲存多頁 OCR 結果

## 介紹

在本教學中，您將學會如何使用 Aspose.OCR for .NET **將影像轉換為 PDF C#**，並將產生的多頁 OCR 輸出儲存為文件。無論您是需要 **將掃描影像轉換為 PDF** 以作存檔，或是 **從影像中提取文字 C#** 以進行資料處理，本指南都會一步步帶領您完成，並提供實務範例與最佳實踐建議。

## 快速回答
- **本教學涵蓋什麼內容？** 使用 Aspose.OCR 在 C# 中將多張影像轉換為 PDF/Docx/Txt/Pdf/Xlsx。
- **支援哪些格式？** Docx、Text、Pdf 與 Xlsx（亦可直接輸出 PDF）。
- **需要授權嗎？** 評估可使用免費試用版；正式上線需購買永久授權。
- **相容的 .NET 版本？** .NET Framework 4.5 以上、 .NET Core 3.1 以上、 .NET 5/6/7。
- **轉換時能同時提取文字嗎？** 可以——使用 OCR 結果在儲存前取得文字。

## 什麼是「convert images to PDF C#」？

在 C# 中將影像轉換為 PDF，指的是以程式方式將一或多張位圖檔（PNG、JPEG、TIFF 等）產生 PDF 文件，保留原始視覺版面，同時可選擇透過 OCR 嵌入可搜尋的文字。Aspose.OCR 讓此流程簡單且高度客製化。

## 為何選擇 Aspose.OCR 來完成此任務？

- **高準確度** 的 OCR 引擎，支援多種語言。
- **多頁支援** – 可一次處理多張影像。
- **直接儲存** 為常用辦公格式，無需額外轉換步驟。
- **完整 .NET 整合** – 無本機相依或外部工具。

## 前置條件

在開始之前，請確保您已具備以下項目：

1. 安裝 Aspose.OCR for .NET。您可於 [此處](https://releases.aspose.com/ocr/net/) 下載。  
2. 取得免費試用或購買授權 – 試用版請點 [此處](https://releases.aspose.com/)，購買請至 [此處](https://purchase.aspose.com/buy)。  
3. 閱讀官方 [文件](https://reference.aspose.com/ocr/net/)，熟悉 API。  
4. 加入 [支援論壇](https://forum.aspose.com/c/ocr/16) 社群，取得問題協助。

一切就緒後，讓我們開始撰寫程式碼。

## 匯入命名空間

在 C# 檔案中加入必要的命名空間：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

這些匯入讓您可以使用集合、檔案處理、LINQ 以及 Aspose OCR 類別。

## 步驟 1：設定文件目錄

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

將 `"Your Document Directory"` 替換為來源影像所在的絕對或相對路徑，以及您希望儲存輸出檔案的目錄。

## 步驟 2：初始化 Aspose.OCR

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

建立 `AsposeOcr` 物件，即可使用所有 OCR 操作，包括 **convert images to PDF C#** 工作流程。

## 步驟 3：辨識影像

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

`RecognizeMultipleImages` 方法會處理清單中的每個檔案，並回傳 `RecognitionResult` 集合。您可以一次提供任意數量的影像，非常適合 **convert scanned images to PDF** 的情境。

## 步驟 4：以偏好格式儲存結果

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

依您的後續流程選擇最合適的格式：

- **Docx** – 可編輯的 Word 文件，內含可搜尋文字。  
- **Text** – 純文字抽取，適合快速資料挖掘（**extract text from images C#**）。  
- **Pdf** – 經典 PDF 輸出，適合存檔。  
- **Xlsx** – 表格化的試算表，適用於結構化資料。

## 常見使用情境

- **數位存檔：** 將掃描的紙本合約轉換為可搜尋的 PDF。  
- **資料輸入自動化：** 從收據或發票中提取文字，寫入資料庫。  
- **批次處理：** 以最少程式碼一次處理數千張影像。

## 疑難排解與技巧

- **大量影像集合：** 將影像分批處理，以避免記憶體激增。  
- **影像品質：** 確保影像解析度至少 300 dpi，以獲得最佳 OCR 準確度。  
- **授權錯誤：** 呼叫 OCR 方法前，先確認授權檔案已正確載入。

## 其他常見問題

**Q: 能否在不使用 OCR 的情況下將影像轉換為 PDF C#？**  
A: 可以，您可以使用 Aspose.PDF 或其他函式庫進行純影像轉 PDF，但 OCR 會額外提供可搜尋文字。

**Q: 轉換完成後，如何在 C# 中從影像提取文字？**  
A: `RecognizeMultipleImages` 回傳的 `result` 清單中，每個 `RecognitionResult` 皆有 `Text` 屬性，您可將其寫入 `.txt` 檔或直接處理。

**Q: 能否自訂頁邊距或方向？**  
A: 在儲存為 PDF 或 Docx 前，您可透過 Aspose.Words 或 Aspose.PDF API 調整文件版面，然後呼叫 `SaveMultipageDocument`。

**Q: 若影像無法讀取會發生什麼？**  
A: OCR 引擎會為該頁回傳空的 `RecognitionResult`；您可檢查 `result[i].Text` 是否為 null 或空字串，並自行處理。

**Q: API 是否支援雲端部署？**  
A: 支援，該函式庫可在任何 .NET 執行環境上運行，包括 Azure Functions 與 AWS Lambda，只要符合版本需求即可。

---

**最後更新：** 2025-12-30  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}