---
title: 在 OCR 影像辨識中準備矩形
linktitle: 在 OCR 影像辨識中準備矩形
second_title: Aspose.OCR .NET API
description: 透過我們的綜合指南釋放 Aspose.OCR for .NET 的潛力。逐步學習如何準備用於影像辨識的矩形。透過無縫 OCR 整合提升您的 .NET 應用程式。
weight: 11
url: /zh-hant/net/ocr-optimization/prepare-rectangles/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 OCR 影像辨識中準備矩形

## 介紹

在不斷發展的技術領域，光學字元辨識 (OCR) 在將影像轉換為機器可讀文字方面發揮關鍵作用。對於尋求將 OCR 功能無縫整合到 .NET 應用程式中的開發人員來說，Aspose.OCR for .NET 是一個強大的解決方案。在本綜合指南中，我們將探索使用 Aspose.OCR for .NET 在 OCR 影像辨識中準備矩形的過程。

## 先決條件

在深入學習本教程之前，請確保您具備以下先決條件：

- .NET 開發的實用知識。
- 安裝了 Aspose.OCR for .NET 函式庫。你可以下載它[這裡](https://releases.aspose.com/ocr/net/).
- 對影像辨識概念的基本了解。

## 導入命名空間

讓我們先導入必要的命名空間來啟動我們的 OCR 之旅：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 第 1 步：設定您的文件目錄

首先指定儲存文檔的目錄。代替`"Your Document Directory"`與您的文件的實際路徑。

```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";

//初始化 AsposeOcr 實例
AsposeOcr api = new AsposeOcr();
```

## 步驟 2：辨識具有多個矩形的影像

在此步驟中，我們將示範如何使用多個矩形從圖像中識別文字。請依照以下子步驟操作：

### 2.1 定義矩形

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### 2.2 進行OCR識別

```csharp
//第一個案例
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

//顯示識別的文字
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## 步驟3：使用辨識設定辨識影像

在此步驟中，我們將展示使用 RecognitionSettings 進行影像辨識的替代方法：

### 3.1 定義識別設定

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 3.2 顯示識別的文本

```csharp
//顯示識別的文字
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## 結論

恭喜！您已成功完成使用 Aspose.OCR for .NET 在 OCR 影像辨識中準備矩形的過程。本指南使您能夠將 OCR 無縫整合到 .NET 應用程式中，從而增強其文字辨識功能。

### 常見問題解答

### Q1：我可以將 Aspose.OCR for .NET 與其他 .NET 框架一起使用嗎？

A1：是的，Aspose.OCR for .NET 與各種.NET 框架相容。

### 問題 2：Aspose.OCR for .NET 有沒有免費試用版？

 A2：當然！您可以存取免費試用版[這裡](https://releases.aspose.com/).

### 問題 3：如何獲得 Aspose.OCR for .NET 支援？

 A3：訪問[Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16)以獲得專門的支援。

### Q4：我可以獲得臨時許可證用於測試目的嗎？

 A4：是的，您可以獲得臨時許可證[這裡](https://purchase.aspose.com/temporary-license/).

### Q5：在哪裡可以找到 Aspose.OCR for .NET 的文件？

 A5：文件可用[這裡](https://reference.aspose.com/ocr/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
