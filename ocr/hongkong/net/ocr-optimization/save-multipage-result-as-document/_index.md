---
date: 2026-04-29
description: 學習如何使用 Aspose.OCR 於 C# 將圖像轉換為 PDF、將多頁 OCR 結果儲存為文件，以及從圖像中提取文字（C#）。
keywords:
- convert images to pdf
- extract text from images
- c# ocr library
- convert images to xlsx
- generate pdf from tiff
linktitle: 將圖像轉換為 PDF C# – 儲存多頁 OCR 結果
second_title: Aspose.OCR .NET API
title: 將圖像轉換為 PDF（C#）– 保存多頁 OCR 結果
url: /zh-hant/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將圖像轉換為 PDF C# – 儲存多頁 OCR 結果

## 簡介

在本教學中，您將學習如何使用功能強大的 **Aspose.OCR** .NET 函式庫 **將圖像轉換為 PDF C#**。無論您需要 **將掃描的 TIFF 檔案轉換為可搜尋的 PDF**、從圖像中擷取文字以進行資料挖掘，或是從一批圖片產生 Excel 活頁簿，本指南都會以清晰的說明、實務技巧與最佳實踐建議，逐步帶領您完成。

## 快速解答
- **本教學涵蓋什麼內容？** 使用 Aspose.OCR 於 C# 中將多張圖像轉換為 PDF、Docx、Text 與 Xlsx，並將 OCR 結果儲存為多頁文件。  
- **支援哪些輸出格式？** Docx、Text、Pdf 與 Xlsx（亦可直接輸出 PDF）。  
- **我需要授權嗎？** 免費試用可用於評估；正式上線需購買永久授權。  
- **相容的 .NET 版本為何？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。  
- **轉換時能否擷取文字？** 可以——在儲存前使用 OCR 結果提取可搜尋的文字。  

## 什麼是「將圖像轉換為 PDF C#」？

在 C# 中將圖像轉換為 PDF，指的是以程式方式取得一或多個位圖檔案（PNG、JPEG、TIFF 等），產生保留視覺版面的 PDF 文件，同時可選擇透過 OCR 嵌入可搜尋的文字。Aspose.OCR 提供 **c# ocr library**，可端對端處理此工作，包括多頁支援與直接儲存為常見辦公格式。

## 為何在此任務中使用 Aspose.OCR？

- **高精度 OCR**，支援數十種語言。  
- **多頁處理** – 輸入整個資料夾的圖像，即可產生單一可搜尋的 PDF。  
- **直接匯出** 為 Docx、Text、Pdf 與 Xlsx，無需二次轉換。  
- **純 .NET** – 無原生相依性，可於 Windows、Linux 及雲端執行環境運行。  

## 先決條件

1. 安裝 Aspose.OCR for .NET。您可以下載它 [here](https://releases.aspose.com/ocr/net/)。  
2. 取得免費試用或購買授權 – 可在[此處](https://releases.aspose.com/)取得試用版，或在[此處](https://purchase.aspose.com/buy)購買。  
3. 閱讀官方[文件](https://reference.aspose.com/ocr/net/)，熟悉 API 介面。  
4. 加入[支援論壇](https://forum.aspose.com/c/ocr/16)社群，取得問題協助。  

現在一切就緒，讓我們開始編寫程式碼。

## 匯入命名空間

首先在 C# 檔案中加入所需的命名空間：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

這些匯入讓您可以使用集合、檔案處理、LINQ 以及 Aspose OCR 類別。

## 步驟 1：設定文件目錄

將 `"Your Document Directory"` 替換為來源圖像所在的絕對或相對路徑，以及您希望儲存輸出檔案的目錄。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

## 步驟 2：初始化 Aspose.OCR

建立 `AsposeOcr` 物件即可使用所有 OCR 功能，包括 **convert images to PDF C#** 工作流程。

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 步驟 3：辨識圖像

`RecognizeMultipleImages` 方法會處理清單中的每個檔案，並回傳 `RecognitionResult` 集合。您可以提供任意數量的圖像，非常適合 **convert scanned images to PDF** 的情境。

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

## 步驟 4：以偏好格式儲存結果

選擇最符合後續工作流程的格式：

- **Docx** – 可編輯的 Word 文件，內含可搜尋的文字。  
- **Text** – 純文字抽取，適合快速資料挖掘（**extract text from images**）。  
- **Pdf** – 經典的 PDF 輸出，適合保存。  
- **Xlsx** – 表格資料的試算表表示（**convert images to xlsx**）。

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

## 如何將圖像轉換為 PDF C# – 步驟回顧

1. **準備資料夾**，放入您要轉換的圖像。  
2. **建立 `AsposeOcr` 實例** 以使用 OCR 功能。  
3. **呼叫 `RecognizeMultipleImages`** 取得每個檔案的 OCR 結果。  
4. **使用 `SaveMultipageDocument`** 以您需要的格式儲存多頁結果。  

## 常見使用案例

- **數位保存：** 將掃描的紙本合約轉換為可搜尋的 PDF。  
- **資料輸入自動化：** 從收據或發票擷取文字，並寫入資料庫。  
- **批次處理：** 以最少程式碼在單一作業中處理數千張圖像。  
- **從 TIFF 產生 PDF：** 適用於需保留原始高解析度掃描文件的情況。  

## 故障排除與提示

- **大量圖像集：** 將圖像分成較小批次處理，以避免記憶體激增。  
- **圖像品質：** 確保圖像解析度至少為 300 dpi，以獲得最佳 OCR 準確度。  
- **授權錯誤：** 在呼叫 OCR 方法前，確認授權檔案已正確載入。  
- **空結果：** 若圖像無法讀取，對應的 `RecognitionResult` 之 `Text` 屬性會為空——儲存前請檢查是否為 null 或空字串。  

## 常見問題

**Q: 可以在不使用 OCR 的情況下將圖像轉換為 PDF C# 嗎？**  
A: 可以，您可以使用 Aspose.PDF 或其他函式庫進行純粹的圖像轉 PDF 轉換，但 OCR 會加入可搜尋的文字，使 PDF 更具實用性。

**Q: 轉換後，如何在 C# 中從圖像擷取文字？**  
A: `RecognizeMultipleImages` 回傳的 `result` 清單每頁都有 `Text` 屬性。您可以將這些字串寫入 `.txt` 檔案，或直接在應用程式中處理。

**Q: 能否設定自訂頁邊距或方向？**  
A: 儲存為 PDF 或 Docx 時，您可在呼叫 `SaveMultipageDocument` 前，透過 Aspose.Words 或 Aspose.PDF API 調整文件版面配置。

**Q: 若圖像無法讀取會發生什麼？**  
A: OCR 引擎會為該頁回傳空的 `RecognitionResult`；您可以偵測到後跳過或記錄該問題檔案。

**Q: 此 API 支援雲端部署嗎？**  
A: 可以，該函式庫可在任何 .NET 執行環境上運作，包括 Azure Functions 與 AWS Lambda，只要符合版本需求即可。

## 結論

您現在擁有完整且可投入生產的工作流程，可 **將圖像轉換為 PDF C#**、擷取可搜尋的文字，甚至從一批圖片產生 Word、純文字或 Excel 檔案。歡迎嘗試不同的輸出格式、調整特定語言的 OCR 設定，或將程式碼整合至更大的文件處理管線中。

---

**最後更新:** 2026-04-29  
**測試環境:** Aspose.OCR 24.11 for .NET  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}