---
date: 2026-02-25
description: 學習如何使用 Aspose.OCR for .NET 從圖像中提取文字。本指南將帶領您完成 OCR 圖像辨識的矩形準備，以及提升辨識準確度。
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: 如何在 OCR 中設定矩形以從圖像提取文字
url: /zh-hant/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 OCR 圖像辨識中準備矩形區域

## 介紹

光學字元辨識（OCR）是將視覺內容轉換為可搜尋、可編輯文字的關鍵技術。在本教學中，您將透過 **從圖像中擷取文字**，藉由自訂矩形區域讓 OCR 引擎只聚焦於特定區段。使用 Aspose.OCR for .NET，我們將逐步說明從專案設定到取得辨識文字的每個步驟，讓您能在 .NET 應用程式中整合強大的圖像轉文字功能。

## 快速答覆
- **「從圖像中擷取文字」是什麼意思？** 即將圖片中的視覺字元轉換為機器可讀的字串。  
- **哪個 .NET 函式庫可以協助完成？** Aspose.OCR for .NET。  
- **開發階段需要授權嗎？** 免費試用可用於測試；正式上線需購買授權。  
- **可以只針對特定區域嗎？** 可以，透過定義矩形來限制 OCR 範圍。  
- **支援哪些 .NET 版本？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6/7。

## 什麼是「使用矩形從圖像中擷取文字」？
當您在圖像上定義矩形區域時，OCR 引擎僅會處理這些區域。這樣可提升辨識準確度、縮短處理時間，並且讓您忽略雜訊背景或不相關的部分。

## 為何在 OCR 前先準備矩形？
- **聚焦於相關內容：** 跳過標頭、頁腳或裝飾圖形。  
- **提升效能：** 較小的區域意味更快的辨識速度。  
- **改善準確度：** 減少視覺雜訊可得到更乾淨的結果。

## 為什麼這對實務專案很重要
許多商業文件（如收據、發票、身分證）都有混合版面，只有特定部位含有關鍵文字。使用矩形即可只擷取所需欄位，顯著減少後續處理工作，提升自動化流程的可靠性。

## 常見使用情境
- **資料輸入自動化：** 從掃描表單中抽取特定欄位。  
- **合規性檢查：** 分離並驗證法律文字區塊。  
- **內容索引：** 只為圖像的標題或說明文字建立索引，以供搜尋引擎使用。  

## 前置條件

- 熟悉 C# 與 .NET 開發。  
- 已安裝 Aspose.OCR for .NET 函式庫 – 可在 **[此處](https://releases.aspose.com/ocr/net/)** 下載。  
- 準備一張包含欲擷取文字的樣本圖像（例如 `sample.png`）。

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

### 步驟 2：使用多個矩形辨識圖像

#### 2.1 定義矩形

建立 `Rectangle` 物件清單，列出您希望 OCR 引擎掃描的區域。

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

### 步驟 3：使用辨識設定 (Alternative Approach)

若您偏好使用 `RecognitionSettings`，也能以稍微不同的 API 呼叫達成相同結果。

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

- **矩形座標不正確：** 請確認 `X`、`Y`、`Width`、`Height` 的數值正確對應欲擷取的區域。  
- **圖像品質：** 低解析度圖像可能導致 OCR 效果不佳，建議先進行前處理（例如二值化）。  
- **結果為空：** 請確認矩形內確實包含文字，否則引擎會回傳空字串。

## 疑難排解與最佳實踐

| 症狀 | 可能原因 | 解決方式 |
|------|----------|----------|
| 沒有輸出或回傳空字串 | 矩形超出圖像範圍 | 再次檢查圖像尺寸與矩形座標 |
| 文字亂碼 | 對比度低或雜訊過多 | 在 OCR 前先做圖像清理（灰階、閾值化） |
| 大檔案處理緩慢 | 矩形過多或圖像過大 | 將圖像切分或減少矩形數量 |

## 結論

您現在已掌握如何透過 Aspose.OCR for .NET，**從圖像中擷取文字**，並以自訂矩形控制 OCR 處理範圍。此技巧讓您在應用程式中建立更快速、精確的文字擷取功能。

## 常見問答

**Q:** 可以在其他 .NET 框架上使用 Aspose.OCR for .NET 嗎？  
**A:** 可以，Aspose.OCR for .NET 相容於多種 .NET 框架。

**Q:** 有提供免費試用嗎？  
**A:** 當然！您可在 **[此處](https://releases.aspose.com/)** 取得免費試用。

**Q:** 如何取得 Aspose.OCR for .NET 的支援？  
**A:** 請前往 **[Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16)** 獲取專屬支援。

**Q:** 可以取得測試用的臨時授權嗎？  
**A:** 可以，請至 **[此處](https://purchase.aspose.com/temporary-license/)** 取得臨時授權。

**Q:** 哪裡可以找到 Aspose.OCR for .NET 的文件？  
**A:** 文件位於 **[此處](https://reference.aspose.com/ocr/net/)**。

---

**最後更新：** 2026-02-25  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}