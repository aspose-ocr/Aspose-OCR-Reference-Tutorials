---
date: 2025-12-22
description: 學習如何使用 Aspose.OCR for .NET 從圖像中辨識文字，並以精確的 OCR 辨識設定將圖像轉換為文字。
linktitle: recognize text from image – Perform OCR on Image from URL
second_title: Aspose.OCR .NET API
title: 從圖像辨識文字 – 從 URL 執行 OCR
url: /zh-hant/net/ocr-optimization/perform-ocr-on-image-from-url/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 URL 圖片上執行 OCR 影像辨識

## 介紹

在光學字元辨識（OCR）領域，Aspose.OCR for .NET 讓您 **從影像中辨識文字**，精準度高，協助開發者輕鬆從圖片中擷取內容。若您想在 .NET 應用程式中整合 OCR 功能，並從遠端來源執行文字辨識，本步驟指南將帶您完成從 URL 取得影像並執行 OCR 的全過程。

## 快速回答
- **本教學涵蓋什麼內容？** 使用 Aspose.OCR for .NET 從公開 URL 的影像中辨識文字。  
- **主要關鍵字是什麼？** *recognize text from image*  
- **需要授權嗎？** 提供試用版，但正式環境需購買商業授權。  
- **支援哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6+。  
- **實作需要多久？** 基本設定通常在 10 分鐘內完成。

## 什麼是「recognize text from image」？
從影像辨識文字即將字元的視覺表現轉換為可編輯、可搜尋的文字。此過程常稱為 **convert image to text** 或 **extract text from image**，可應用於文件數位化、資料輸入自動化及無障礙功能等情境。

## 為什麼使用 Aspose.OCR for .NET？
- **高準確度**，內建多語言支援。  
- **細緻的 OCR 設定**（例如自動去斜、區域偵測）。  
- **簡易 API**，同時支援 .NET Framework 與 .NET Core。  
- **無外部相依**——全部在本機執行。

## 前置條件

在開始教學前，請確保已具備以下條件：

- Aspose.OCR for .NET：確定已將 Aspose.OCR 套件整合至您的 .NET 專案，可從 [release page](https://releases.aspose.com/ocr/net/) 下載。  
- 開發環境：您的機器上已安裝可運作的 .NET 開發環境。

## 匯入命名空間

在 .NET 專案中，加入必要的命名空間以使用 Aspose.OCR 功能。將以下程式碼片段加入您的專案：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## 如何使用 URL 進行「recognize text from image」？

### 步驟 1：設定文件目錄

先指定存放文件的目錄路徑。將 `"Your Document Directory"` 替換為實際的文件路徑。

```csharp
string dataDir = "Your Document Directory";
```

### 步驟 2：取得要辨識的影像

提供欲執行 OCR 的影像 URL，確保該影像可公開存取。

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

### 步驟 3：初始化 AsposeOcr

建立 AsposeOcr 類別的實例，以存取 OCR 功能。

```csharp
AsposeOcr api = new AsposeOcr();
```

### 步驟 4：辨識影像

使用 Aspose.OCR 套件對指定的影像 URL 進行文字辨識，並依需求調整辨識設定。

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

### 步驟 5：輸出結果

顯示辨識結果，包括辨識出的文字、區域資訊以及任何警告訊息。

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

### 步驟 6：執行與驗證

執行您的應用程式，若設定正確，您將看到 OCR 成功執行的結果。

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## 常見問題與解決方案

- **影像無法公開存取** – 請確認 URL 在瀏覽器中能正常開啟。若影像需要驗證，請先下載後使用 `RecognizeImageFromStream`。  
- **辨識區域不正確** – 調整 `Rectangle` 參數，或將 `DetectAreas = false` 交由引擎自動偵測。  
- **語言未被辨識** – 確認已安裝相應語言包，或在 `RecognitionSettings` 中設定 `Language = "eng"`（或其他 ISO 代碼）。

## 常見問答

### Q1：Aspose.OCR 能處理多種語言嗎？

A1：可以，Aspose.OCR 支援多語言文字辨識，適用於國際化應用。

### Q2：是否同時支援單行與多行文字辨識？

A2：當然！Aspose.OCR 可彈性辨識單行或多行文字，依需求調整即可。

### Q3：Aspose.OCR 有哪些授權方案？

A3：您可在 [Aspose store](https://purchase.aspose.com/buy) 查看並購買授權。

### Q4：是否提供免費試用？

A4：有，請前往 [releases page](https://releases.aspose.com/) 下載試用版。

### Q5：哪裡可以取得支援或社群討論？

A5：請造訪 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 取得支援並與社群互動。

## 結論

使用 Aspose.OCR for .NET，將 OCR 功能整合至 .NET 應用變得相當順暢。本教學說明了如何透過 URL **recognize text from image**，為您在專案中運用文字擷取奠定堅實基礎。

---

**最後更新：** 2025-12-22  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}