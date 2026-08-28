---
date: 2026-02-25
description: 學習如何使用 Aspose.OCR for .NET 將圖像轉換為文字，並以精確的 OCR 識別設定從圖像中提取文字。
linktitle: convert image to text – Perform OCR on Image from URL
second_title: Aspose.OCR .NET API
title: 將圖像轉換為文字 – 從 URL 執行 OCR
url: /zh-hant/net/ocr-optimization/perform-ocr-on-image-from-url/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 轉換圖像為文字 – 從 URL 執行 OCR

## 介紹

如果您需要在 .NET 應用程式中**將圖像轉換為文字**，Aspose.OCR for .NET 提供可靠的方式，從網路上任何位置的圖片中擷取文字。透過本教學，您將學會如何從公開 URL 的圖像辨識文字、設定 OCR 識別參數，並處理結果——全部只需幾分鐘即可完成。

## 快速回答
- **本教學涵蓋什麼內容？** 使用 Aspose.OCR for .NET 從公開 URL 轉換圖像為文字。  
- **目標的主要關鍵字是？** *convert image to text*  
- **我需要授權嗎？** 提供試用版，但正式上線需購買商業授權。  
- **支援哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6+。  
- **實作需要多長時間？** 基本設定通常在 10 分鐘以內完成。

## 什麼是「convert image to text」？
將圖像中的字符視覺表示轉換為可編輯、可搜尋的字串。此過程亦稱為**從圖像擷取文字**，可用於文件數位化、資料輸入自動化與無障礙解決方案。

## 為什麼使用 Aspose.OCR for .NET 來轉換圖像為文字？
- **高準確度**，內建語言支援，並可選用 **OCR language pack** 擴充。  
- **細緻的 OCR 識別設定**，如自動校正傾斜、區域偵測與多行處理。  
- **簡易 API**，同時支援 .NET Framework 與 .NET Core，無需外部相依。  
- **直接支援 URL** —— 可**從 URL 辨識文字**而無需先下載圖像，亦可選擇**下載圖像以供 OCR**。

## 前置條件

在開始之前，請確保您已具備：

- 已安裝 Aspose.OCR for .NET。從[發佈頁面](https://releases.aspose.com/ocr/net/)取得最新程式庫。  
- .NET 開發環境（Visual Studio、VS Code 或您偏好的 IDE）。  
- 具備網際網路連線以下載要處理的圖像。

## 匯入命名空間

加入必要的命名空間，以便使用 Aspose.OCR 類別：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## 從 URL 轉換圖像為文字的逐步指南

### 步驟 1：設定文件目錄
定義暫存檔案或結果的存放位置。

```csharp
string dataDir = "Your Document Directory";
```

### 步驟 2：提供圖像 URL
提供可公開存取的 URL。若圖像需要驗證，您需要先**下載圖像以供 OCR**，然後改用串流。

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

### 步驟 3：初始化 AsposeOcr 引擎
建立 OCR 引擎的實例。

```csharp
AsposeOcr api = new AsposeOcr();
```

### 步驟 4：設定 OCR 識別設定
微調引擎處理圖像的方式。此處我們啟用區域偵測、自動傾斜，並示範以兩個自訂矩形作為 **ocr recognition settings** 的範例。

```csharp
RecognitionResult result = api.RecognizeImageFromUri(uri, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    RecognitionAreas = new List<Rectangle>()
    {
        new Rectangle(1,3,390,70),
        new Rectangle(1,72,390,70)
    }
});
```

> **小技巧：** 若不需要自訂區域，將 `DetectAreas = false`，讓引擎自動定位文字區塊。

### 步驟 5：輸出 OCR 結果
列印辨識出的文字、偵測到的區域、任何警告，以及完整的 JSON 資料以供除錯。

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

### 步驟 6：確認執行成功
簡單的確認訊息可讓您知道流程已順利完成，且未拋出例外。

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## 常見問題與解決方案

- **圖像未公開存取** – 請確認該 URL 能在瀏覽器開啟。對於受保護的圖像，請先下載後呼叫 `RecognizeImageFromStream`。  
- **偵測區域不正確** – 調整 `Rectangle` 參數或停用 `DetectAreas`，讓引擎自動偵測。  
- **語言未被辨識** – 安裝相應的 **OCR language pack**，並在 `RecognitionSettings` 中設定 `Language = "eng"`（或其他 ISO 代碼）。

## 常見問答

### Q1：Aspose.OCR 是否適合處理多語言？
**A：** 是的。透過加入相關的 **ocr language pack**，即可辨識數十種語言的文字。

### Q2：我可以使用 Aspose.OCR 進行單行與多行文字擷取嗎？
**A：** 當然可以。可在 `RecognitionSettings` 中切換 `RecognizeSingleLine` 以符合您的需求。

### Q3：商業專案有授權方案嗎？
**A：** 有，您可在 [Aspose 商店](https://purchase.aspose.com/buy) 探索授權方案並購買完整授權。

### Q4：是否提供免費試用？
**A：** 有，試用版可從 [發佈頁面](https://releases.aspose.com/) 下載。

### Q5：在哪裡可以取得社群支援？
**A：** 請前往專屬的 [Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16) 取得協助與討論。

## 結論

使用 Aspose.OCR for .NET，從遠端 URL 轉換圖像為文字既簡單又高度可客製化。依照上述步驟，您即可在任何 .NET 應用程式中整合強大的 OCR 功能，無論是需要簡易的 **extract text from image** 功能，或是針對複雜文件的進階 **ocr recognition settings**。

---

**最後更新：** 2026-02-25  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}