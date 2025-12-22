---
date: 2025-12-22
description: 學習如何使用 Aspose.OCR for .NET 從圖片中提取文字。本指南將帶領您完成為 OCR 圖片識別準備矩形以及提升準確度的步驟。
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: 如何在 OCR 中設定矩形以從圖像擷取文字
url: /zh-hant/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 準備 OCR 圖像識別的矩形

## 介紹

光學字符識別（OCR）是將視覺內容轉換為可搜尋、可編輯文字的關鍵技術。在本教學中，您將透過 **從圖像中擷取文字**，先建立自訂矩形，讓 OCR 引擎只聚焦於特定區域。使用 Aspose.OCR for .NET，我們將一步步說明——從專案設定到取得辨識文字——讓您能在 .NET 應用程式中整合強大的圖像轉文字功能。

## 快速答覆
- **「從圖像中擷取文字」是什麼意思？** 代表將圖片中的視覺字符轉換為機器可讀的字串。  
- **哪個 .NET 函式庫可以協助完成？** Aspose.OCR for .NET。  
- **開發階段需要授權嗎？** 可使用免費試用版進行測試；正式上線需購買授權。  
- **可以只針對特定區域嗎？** 可以，透過定義矩形來限制 OCR 範圍。  
- **支援哪些 .NET 版本？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6/7。

## 什麼是「使用矩形從圖像中擷取文字」？
當您在圖像上定義矩形區域時，OCR 引擎僅會處理這些區域。這樣可提升辨識精確度、縮短處理時間，並讓您忽略雜訊背景或不相關的部分。

## 為什麼在 OCR 前先準備矩形？
- **聚焦於相關內容：** 跳過標頭、頁腳或裝飾圖形。  
- **提升效能：** 處理較小的區域可加快辨識速度。  
- **改善準確度：** 減少視覺雜訊，得到更乾淨的結果。

## 前置條件

- 熟悉 C# 與 .NET 開發。  
- 已安裝 Aspose.OCR for .NET 函式庫——可在 **[此處](https://releases.aspose.com/ocr/net/)** 下載。  
- 準備一張範例圖像（例如 `sample.png`），內含您想擷取的文字。

## 匯入命名空間

首先，將所需的命名空間引入程式碼：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 步驟 1：設定文件目錄

指定圖像檔案所在位置，並建立 OCR 引擎實例。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## 如何使用多個矩形從圖像中擷取文字

### 步驟 2：以多個矩形辨識圖像

#### 2.1 定義矩形

建立 `Rectangle` 物件的清單，標示您希望 OCR 引擎掃描的區域。

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 執行 OCR 辨識

將圖像路徑與矩形清單傳入 `RecognizeImage`。此方法會回傳字串集合——每個條目對應一個矩形。

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### 步驟 3：使用辨識設定辨識圖像（替代方式）

如果您偏好使用 `RecognitionSettings`，也能以稍有不同的 API 呼叫達成相同結果。

#### 3.1 定義辨識設定

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 顯示辨識文字

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## 常見問題與技巧

- **矩形座標不正確：** 請確認 `X`、`Y`、`Width`、`Height` 的數值正確對應到目標區域。  
- **圖像品質：** 低解析度圖像可能導致 OCR 效果不佳；建議先行前處理（例如二值化）。  
- **結果為空：** 請確認矩形內確實包含文字，否則引擎會回傳空字串。

## 結論

現在您已學會如何透過 Aspose.OCR for .NET，**以自訂矩形從圖像中擷取文字**。此技巧讓您對 OCR 處理擁有精細的控制，助您在應用程式中打造更快速、準確的文字擷取功能。

## 常見問答

**Q:** 我可以在其他 .NET 框架上使用 Aspose.OCR for .NET 嗎？  
**A:** 可以，Aspose.OCR for .NET 相容於多種 .NET 框架。

**Q:** 是否提供 Aspose.OCR for .NET 的免費試用？  
**A:** 當然！您可在 **[此處](https://releases.aspose.com/)** 取得免費試用。

**Q:** 如何取得 Aspose.OCR for .NET 的支援？  
**A:** 請前往 **[Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16)** 尋求專業協助。

**Q:** 我可以取得暫時授權以進行測試嗎？  
**A:** 可以，請至 **[此處](https://purchase.aspose.com/temporary-license/)** 申請暫時授權。

**Q:** 哪裡可以找到 Aspose.OCR for .NET 的文件？  
**A:** 文件位於 **[此處](https://reference.aspose.com/ocr/net/)**。

---

**最後更新：** 2025-12-22  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}