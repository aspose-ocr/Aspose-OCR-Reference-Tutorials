---
date: 2026-04-23
description: 學習如何使用 Aspose.OCR 於 C# 將圖像轉換為 PDF、將多頁 OCR 結果儲存為文件，並從圖像中提取文字。
keywords:
- extract text from images
- batch image to pdf
- convert scanned images pdf
linktitle: 將圖片轉換為 PDF C# – 儲存多頁 OCR 結果
second_title: Aspose.OCR .NET API
title: 從圖像提取文字 – 將圖像轉換為 PDF C#
url: /zh-hant/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像提取文字 – 將圖像轉換為 PDF C#

## 簡介

在本教學中，您將學習如何 **extract text from images** 同時 **convert images to PDF C#**，使用 Aspose.OCR for .NET，並將多頁 OCR 結果儲存為文件。無論您是需要 **batch image to pdf** 以進行歸檔、 **convert scanned images pdf** 以符合合規要求，或僅僅從圖片中提取可搜尋的文字，我們都會逐步說明，提供清晰的解釋、實務技巧與最佳實踐建議。

## 快速解答
- **本教學涵蓋什麼內容？** 將多張圖像轉換為 PDF/Docx/Txt/Xlsx，並使用 Aspose.OCR 在 C# 中 **extract text from images**。  
- **支援哪些輸出格式？** Docx、Text、Pdf 和 Xlsx（您也可以直接輸出 PDF）。  
- **需要授權嗎？** 免費試用可用於評估；正式環境需購買永久授權。  
- **相容的 .NET 版本為何？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。  
- **轉換時可以同時提取文字嗎？** 可以 — 在儲存前使用 OCR 結果提取文字。

## 什麼是「extract text from images」以及為何要將其與 PDF 轉換結合？

從圖像提取文字是指使用 OCR（光學字符識別）將視覺字符轉換為可搜尋、可編輯的字串。當您 **convert images to PDF C#** 時，會將這些字串嵌入 PDF，使文件可搜尋且可索引——非常適合數位歸檔與資料挖掘。

## 為何在此任務中使用 Aspose.OCR？

- **高精度** 支援數十種語言。  
- **多頁支援** – 一次呼叫即可處理批次圖像（適用於 **batch image to pdf** 情境）。  
- **直接儲存** 至常用辦公格式，無需額外轉換步驟。  
- **完整 .NET 整合** – 無原生相依，支援 Windows、Linux 以及雲端執行環境。

## 先決條件

在開始之前，請確保您已具備以下條件：

1. 已安裝 Aspose.OCR for .NET。您可於 [here](https://releases.aspose.com/ocr/net/) 下載。  
2. 取得免費試用或購買授權 – 可在 [here](https://releases.aspose.com/) 取得試用，或在 [here](https://purchase.aspose.com/buy) 購買。  
3. 閱讀官方 [documentation](https://reference.aspose.com/ocr/net/) 以熟悉 API。  
4. 加入 [support forums](https://forum.aspose.com/c/ocr/16) 社群，以獲得問題協助。  

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

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

將 `"Your Document Directory"` 替換為來源圖像所在的絕對或相對路徑，以及您希望儲存輸出檔案的路徑。

## 步驟 2：初始化 Aspose.OCR

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

建立 `AsposeOcr` 物件即可使用所有 OCR 操作，包括 **convert images to PDF C#** 工作流程。

## 步驟 3：辨識圖像

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

`RecognizeMultipleImages` 方法會處理清單中的每個檔案，並回傳 `RecognitionResult` 集合。您可以提供任意數量的圖像，非常適合 **convert scanned images pdf** 情境。

## 步驟 4：以偏好的格式儲存結果

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

選擇最符合後續工作流程的格式：

- **Docx** – 可搜尋文字的可編輯 Word 文件。  
- **Text** – 用於快速資料挖掘的純文字提取（**extract text from images**）。  
- **Pdf** – 經典的 PDF 輸出，適合歸檔。  
- **Xlsx** – 用於表格資料的試算表表示。

## 常見使用情境

- **Digital archiving:** 將掃描的紙本合約轉換為可搜尋的 PDF。  
- **Data entry automation:** 從收據或發票中提取文字，並寫入資料庫。  
- **Batch processing:** 在單一作業中處理數千張圖像，程式碼極少—非常適合 **batch image to pdf** 需求。

## 故障排除與技巧

- **Large image sets:** 將圖像分成較小批次處理，以避免記憶體激增。  
- **Image quality:** 確保圖像解析度至少為 300 dpi，以獲得最佳 OCR 精度。  
- **License errors:** 在呼叫 OCR 方法前，確認授權檔案已正確載入。  
- **Empty results:** OCR 引擎對無法辨識的頁面會回傳空的 `RecognitionResult`；請檢查 `result[i].Text` 是否為 null 或空字串，並作相應處理。

## 常見問題

**Q: 可以在不使用 OCR 的情況下將圖像轉換為 PDF C# 嗎？**  
A: 可以，您可以使用 Aspose.PDF 或其他函式庫進行純粹的圖像轉 PDF 轉換，但 OCR 會加入可搜尋的文字。

**Q: 轉換後如何在 C# 中提取圖像文字？**  
A: `RecognizeMultipleImages` 回傳的 `result` 清單包含 `Text` 屬性，您可以將其寫入 `.txt` 檔案或直接處理。

**Q: 可以設定自訂頁邊距或方向嗎？**  
A: 在儲存為 PDF 或 Docx 時，您可以在呼叫 `SaveMultipageDocument` 之前，透過 Aspose.Words 或 Aspose.PDF API 修改文件版面配置。

**Q: 若圖像無法讀取會發生什麼？**  
A: OCR 引擎會對該頁回傳空的 `RecognitionResult`；您可以檢查 `result[i].Text` 是否為 null 或空字串，並作相應處理。

**Q: 此 API 支援雲端部署嗎？**  
A: 可以，該函式庫可在任何 .NET 執行環境上運作，包括 Azure Functions 與 AWS Lambda，只要執行環境符合版本需求。

---

**最後更新：** 2026-04-23  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}