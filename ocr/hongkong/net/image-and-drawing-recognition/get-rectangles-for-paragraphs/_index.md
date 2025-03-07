---
title: 在 OCR 影像辨識中取得段落的矩形
linktitle: 在 OCR 影像辨識中取得段落的矩形
second_title: Aspose.OCR .NET API
description: 使用 Aspose.OCR for .NET 解鎖進階 OCR 功能。輕鬆提取段落矩形。
weight: 11
url: /zh-hant/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 OCR 影像辨識中取得段落的矩形

## 介紹

歡迎閱讀我們關於利用 Aspose.OCR for .NET 在 OCR 影像辨識中提取段落矩形的綜合指南。如果您希望增強文件處理能力並在 .NET 應用程式中利用光學字元辨識 (OCR) 的強大功能，那麼您來對地方了。

## 先決條件

在我們深入學習本教程之前，請確保您具備以下先決條件：

- C# 和 .NET 開發的基礎知識。
- 使用 Aspose.OCR for .NET 設定的開發環境。如果您還沒有，您可以下載[這裡](https://releases.aspose.com/ocr/net/).
- 了解圖像處理概念以及 OCR 在從圖像中提取文字的重要性。

## 導入命名空間

在您的 C# 程式碼中，請確保匯入了有效使用 Aspose.OCR 所需的命名空間。在文件頂部包含以下內容：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 第 1 步：設定您的文件目錄

首先初始化儲存用於 OCR 處理的影像的文檔目錄的路徑：

```csharp
string dataDir = "Your Document Directory";
```

## 步驟2：初始化AsposeOcr實例

建立 AsposeOcr 類別的實例以存取 OCR 功能：

```csharp
AsposeOcr api = new AsposeOcr();
```

## 第三步：指定影像路徑

定義要處理的影像的完整路徑：

```csharp
string fullPath = dataDir + "sample.png";
```

## 第四步：辨識影像並取得段落矩形

呼叫`GetRectangles`方法取得 OCR 影像中段落的矩形。放`detect_areas`到`true`如果你想提取段落：

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## 第 5 步：列印結果

列印所識別區域的座標：

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## 第六步：結論

恭喜！您已成功執行 OCR 影像辨識過程，以使用 Aspose.OCR for .NET 取得段落的矩形。

## 結論

在本教程中，我們探索了將 Aspose.OCR for .NET 整合到您的應用程式中的基本步驟，讓您可以從 OCR 處理的圖像中提取段落矩形。 Aspose.OCR 簡化了 OCR 的實施，使其成為文件處理和文字擷取的寶貴工具。

## 常見問題解答

### Q1：Aspose.OCR 是否相容於不同的影像格式？

A1：是的，Aspose.OCR 支援各種影像格式，包括 PNG、JPEG 和 TIFF。

### Q2：我可以使用Aspose.OCR批次處理多張影像嗎？

A2：當然！ Aspose.OCR 有助於批次以無縫處理多個影像。

### 問題 3：Aspose.OCR for .NET 有沒有免費試用版？

 A3：是的，您可以探索免費試用[這裡](https://releases.aspose.com/).

### Q4：如何取得Aspose.OCR的臨時許可證？

A4：您可以獲得臨時許可證[這裡](https://purchase.aspose.com/temporary-license/).

### Q5：在哪裡可以找到與 Aspose.OCR 相關的其他支援和討論？

 A5：前往[Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16)以獲得社區支持和討論。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
