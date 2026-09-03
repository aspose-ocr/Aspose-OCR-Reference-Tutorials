---
date: 2026-03-05
description: 學習如何在 .NET 應用程式中使用 Aspose.OCR 偵測區域模式提升 OCR 準確度，從圖像中提取表格文字。
linktitle: OCR Detect Areas Mode in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Improve OCR Accuracy – Detect Areas Mode in OCR
url: /zh-hant/net/text-recognition/ocr-detect-areas-mode/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr 文件模式 – OCR 圖像辨識中的偵測區域模式

## 介紹

在現代 .NET 開發中，**ocr 文件模式** 是在需要精確控制圖像內文字偵測方式時提升 **OCR 準確度** 的首選方案。Aspose.OCR for .NET 讓您輕鬆切換不同的偵測策略，從收據、發票或多欄文件等複雜版面中 **提取表格文字圖像**。本 **aspose ocr tutorial c#** 將帶您深入了解 Detect Areas Mode 功能、說明何時使用各模式，並提供一段可直接執行的程式碼範例。

## 快速回答
- **什麼是 ocr 文件模式？** 一組偵測策略（PHOTO、DOCUMENT、COMBINE），告訴 Aspose.OCR 如何定位文字區域。
- **哪種模式最適合表格？** `PHOTO` 模式在提取表格文字圖像與小文字區塊方面表現最佳。
- **開發時需要授權嗎？** 測試可使用免費試用授權，正式上線則需商業授權。
- **支援哪些 .NET 版本？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6 及更高版本。
- **設定需要多久？** 通常在 10 分鐘內完成整合與執行範例程式碼。

## 如何透過 Detect Areas Mode 提升 OCR 準確度？

選擇正確的 **Detect Areas Mode** 是提升結構化圖像（如表格、收據、多欄版面）OCR 準確度的關鍵。透過告訴引擎圖像是照片、印刷文件或兩者混合，可減少誤偵測、加快處理速度，並取得更乾淨的文字輸出。

## 什麼是 ocr 文件模式？

`ocr 文件模式` 指的是在執行文字辨識前，告訴 Aspose.OCR 如何切割圖像的設定。內建的三種模式如下：

- **PHOTO** – 為照片、收據、發票及小文字區塊最佳化（適合提取表格文字圖像）。
- **DOCUMENT** – 適用於多欄印刷頁面與含有內嵌圖形的文件。
- **COMBINE** – 結合 PHOTO 與 DOCUMENT 的結果，提供最完整的覆蓋範圍。

## 為什麼要使用 Detect Areas Mode？

選擇合適的偵測模式可降低偽陽性、加快處理速度，並提升準確度——這在處理表格等結構化資料時尤為重要。依圖像類型調整模式，可免除大量後處理工作。

## 常見使用情境

| 情境 | 推薦模式 | 為什麼有幫助 |
|----------|------------------|--------------|
| 含有密集表格的收據或發票 | **PHOTO** | 專注於小文字區塊，保留表格版面 |
| 多欄雜誌或報告 | **DOCUMENT** | 處理欄位分割與內嵌圖形 |
| 同時包含照片與文字的掃描文件 | **COMBINE** | 結合 PHOTO 與 DOCUMENT 的優勢 |

## 前置需求

在開始之前，請確保您已具備：

- **Aspose.OCR for .NET** – 從 [Aspose.OCR for .NET documentation](https://reference.aspose.com/ocr/net/) 下載並安裝套件。
- **文件目錄** – 您機器上存放欲處理圖像的資料夾（例如 `table.png`）。

## 匯入命名空間

首先，匯入在 C# 專案中使用 Aspose.OCR 所需的命名空間。

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## 步驟 1：初始化 Aspose.OCR

建立 OCR 引擎實例，並指向您的資料夾。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 步驟 2：載入圖像並選擇 Detect Areas Mode

載入目標圖像，並指定符合情境的偵測策略。

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "table.png", new RecognitionSettings
{
    // Choose the Detect Areas Mode
    DetectAreasMode = DetectAreasMode.PHOTO
    // Other options: NONE, DOCUMENT, COMBINE
});
```

## 步驟 3：取得並顯示辨識結果文字

OCR 完成後，您即可取得抽取的文字，方便進一步處理或存入資料庫。

```csharp
// Display the recognized text
Console.WriteLine(result.RecognitionText);

Console.WriteLine("OCRDetectAreasMode executed successfully");
```

## 常見問題與解決方案

| 問題 | 原因 | 解決方式 |
|-------|--------|-----|
| **輸出為空白** | 圖像類型使用了錯誤的 `DetectAreasMode` | 依版面切換為 `DOCUMENT` 或 `COMBINE` |
| **出現雜訊字元** | 解析度過低的圖像 | 提供更高解析度的來源或先行進行影像增強 |
| **大型檔案逾時** | 記憶體不足 | 使用 `RecognitionSettings` 限制區域大小，或分批處理頁面 |

## 常見問答

**Q: Aspose.OCR for .NET 是否適用於大規模應用程式？**  
A: 是的，該套件設計能處理高容量的 OCR 工作負載，效能已最佳化。

**Q: 我可以用 Aspose.OCR for .NET 辨識手寫文字嗎？**  
A: 此函式庫主要針對印刷文字，手寫辨識可能需要專門的引擎。

**Q: 支援哪些影像格式？**  
A: 完全支援 PNG、JPEG、BMP、TIFF 等常見格式。

**Q: 如何取得技術支援？**  
A: 前往 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 提問並與社群互動。

**Q: 有免費試用版嗎？**  
A: 有，您可透過 [free trial license](https://releases.aspose.com/) 進行功能體驗。

## 結論

掌握 **ocr 文件模式** 與 Detect Areas Mode 的各種選項後，您即可為 Aspose.OCR for .NET 進行精細調校，從而在提取表格文字圖像與其他結構化資料時 **提升 OCR 準確度**。將此方法整合至您的應用程式，可自動化資料輸入、發票處理或任何需要將圖像轉換為可搜尋文字的情境。

---

**最後更新：** 2026-03-05  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}