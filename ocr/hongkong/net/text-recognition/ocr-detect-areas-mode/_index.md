---
date: 2026-01-02
description: 使用 Aspose.OCR 的 OCR 文件模式，提升您的 .NET 應用程式的高效圖像文字識別。學習如何透過此 Aspose OCR 教學（C#）提取表格文字圖像。
linktitle: OCR Detect Areas Mode in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: OCR 文件模式 – OCR 圖像辨識中的偵測區域模式
url: /zh-hant/net/text-recognition/ocr-detect-areas-mode/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr 文檔模式 – OCR 圖像識別中的偵測區域模式

## 簡介

在現代 .NET 開發中，**ocr 文檔模式** 是在需要精確控制圖像內文字偵測方式時的首選方法。Aspose.OCR for .NET 讓您輕鬆在不同偵測策略之間切換，從收據、發票或多欄文件等複雜版面中**提取表格文字圖像**。本 **aspose ocr tutorial c#** 將帶您深入了解 Detect Areas Mode 功能，說明何時使用各模式，並提供可直接執行的程式碼範例。

## 快速回答
- **什麼是 ocr 文檔模式？** 一組偵測策略（PHOTO、DOCUMENT、COMBINE），告訴 Aspose.OCR 如何定位文字區域。
- **哪種模式最適合表格？** `PHOTO` 模式在提取表格文字圖像和小文字區塊方面表現卓越。
- **開發時需要授權嗎？** 測試時免費試用授權已足夠；正式環境需商業授權。
- **.NET 支援哪些版本？** .NET Framework 4.5 以上、 .NET Core 3.1 以上、 .NET 5/6 及更高版本。
- **設定需要多久？** 通常在 10 分鐘內完成整合並執行範例程式碼。

## 什麼是 ocr 文檔模式？
`ocr document mode` 指告訴 Aspose.OCR 在執行文字辨識前如何分割影像的設定。內建的三種模式如下：

- **PHOTO** – 為相片、收據、發票及小文字區域優化（適合提取表格文字圖像）。
- **DOCUMENT** – 適用於多欄列印頁面及含嵌入圖形的文件。
- **COMBINE** – 合併 PHOTO 與 DOCUMENT 的結果，以取得最完整的覆蓋。

## 為什麼使用偵測區域模式？
選擇正確的偵測模式可減少誤判、加快處理速度，並提升準確度——尤其在處理表格等結構化資料時更為顯著。依影像類型調整模式，即可在不需後處理的情況下取得可靠的 OCR 結果。

## 先決條件

在開始之前，請確保您已具備：

- **Aspose.OCR for .NET** – 從 [Aspose.OCR for .NET 文件](https://reference.aspose.com/ocr/net/) 下載並安裝此函式庫。
- **Document Directory** – 您機器上存放欲處理影像的資料夾（例如 `table.png`）。

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

## 步驟 2：載入影像並選擇偵測區域模式

載入目標影像，並指定符合情境的偵測策略。

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "table.png", new RecognitionSettings
{
    // Choose the Detect Areas Mode
    DetectAreasMode = DetectAreasMode.PHOTO
    // Other options: NONE, DOCUMENT, COMBINE
});
```

## 步驟 3：取得並顯示辨識文字

OCR 完成後，您即可取得擷取的文字——非常適合進一步處理或存入資料庫。

```csharp
// Display the recognized text
Console.WriteLine(result.RecognitionText);

Console.WriteLine("OCRDetectAreasMode executed successfully");
```

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|------|------|----------|
| **空白輸出** | 影像類型使用了錯誤的 `DetectAreasMode` | 根據版面切換至 `DOCUMENT` 或 `COMBINE` |
| **雜訊字元** | 低解析度影像 | 提供更高解析度的來源或使用影像增強前處理 |
| **大型檔案逾時** | 記憶體不足 | 使用 `RecognitionSettings` 限制區域大小或分批處理頁面 |

## 常見問答

**Q: Aspose.OCR for .NET 是否適用於大規模應用程式？**  
A: 是的，該套件設計用於處理高量 OCR 工作負載，具備最佳化效能。

**Q: 我可以使用 Aspose.OCR for .NET 來辨識手寫文字嗎？**  
A: 此函式庫主要針對印刷文字；手寫辨識可能需要專門的引擎。

**Q: 支援哪些影像格式？**  
A: 常見的 PNG、JPEG、BMP 與 TIFF 格式皆完整支援。

**Q: 如何取得技術支援？**  
A: 前往 [Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16) 提問並與社群互動。

**Q: 是否提供免費試用？**  
A: 有的，您可使用 [免費試用授權](https://releases.aspose.com/) 來體驗功能。

## 結論

透過精通 **ocr 文檔模式** 與 Detect Areas Mode 選項，您可以微調 Aspose.OCR for .NET，以高精度提取表格文字圖像及其他結構化資料。將此方法整合至您的應用程式，可自動化資料輸入、發票處理或任何需要將影像轉換為可搜尋文字的情境。

---

**最後更新：** 2026-01-02  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}