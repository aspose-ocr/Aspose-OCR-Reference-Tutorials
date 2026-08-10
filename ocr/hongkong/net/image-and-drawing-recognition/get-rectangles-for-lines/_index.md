---
date: 2026-02-22
description: 學習如何使用 Aspose.OCR for .NET 進行版面分析 OCR，辨識影像中的文字行並擷取行的矩形區域。
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: 版面分析 OCR – 從圖像取得行矩形
url: /zh-hant/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 版面分析 OCR – 從圖像取得行矩形

## 簡介

在本教學中，您將了解如何使用 Aspose.OCR for .NET **取得 OCR 行矩形**。完成本指南後，您將能夠 **辨識圖像中的文字行**，並 **擷取每條偵測到的行座標**——非常適合用於後續處理，例如 **版面分析 OCR**、資料擷取或自訂渲染。

## 快速問答
- **「取得 OCR 行矩形」是什麼意思？** 它會回傳圖像中每條偵測到的文字行的邊界框。  
- **使用哪個 API 方法？** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`。  
- **需要授權嗎？** 免費試用版可用於開發；商業授權則需於正式環境使用。  
- **支援的影像格式？** PNG、JPEG、BMP、TIFF 等。  
- **可以在 .NET Core 上執行嗎？** 可以，Aspose.OCR 完全支援 .NET Core 以及 .NET 5/6。

## 先決條件

在開始本教學之前，請確保已具備以下先決條件：

- 具備 C# 與 .NET 開發的基本知識。  
- 使用如 Visual Studio 等整合開發環境 (IDE)。  
- 已安裝 Aspose.OCR for .NET 程式庫。您可於 [此處](https://releases.aspose.com/ocr/net/) 下載。  
- 一張含有文字的樣本影像，用於 OCR 辨識。

## 匯入命名空間

確保已在專案中匯入必要的命名空間。請在 C# 檔案的最上方加入以下程式碼：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

現在，讓我們將 OCR 影像辨識中取得行矩形的流程分解為易於遵循的步驟。

## 版面分析 OCR – 步驟說明

### 步驟 1：設定文件目錄

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

將 `"Your Document Directory"` 替換為實際存放樣本影像的資料夾路徑。

### 步驟 2：初始化 Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

建立 `AsposeOcr` 類別的實例，以存取 OCR 功能。

### 步驟 3：指定影像路徑

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

定義欲執行 OCR 的影像完整路徑。

### 步驟 4：辨識影像並取得矩形

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

`GetRectangles` 方法會回傳 `Rectangle` 物件的清單，每個物件代表偵測到的文字行座標。這是 **取得 OCR 行矩形** 的核心，同時也支援 **版面分析 OCR**。

### 步驟 5：列印結果

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

將偵測區域的座標列印至主控台。您將看到可於之後用於 **擷取行座標** 的數值，以供自訂處理使用。

## 為何使用 Aspose.OCR 取得行矩形？

- **高精度** – 先進演算法即使在噪點或傾斜的影像中亦能偵測行。  
- **跨平台** – 支援 .NET Framework、.NET Core 以及 .NET 5/6。  
- **無外部相依性** – 純 .NET 程式庫，無需攜帶原生 DLL。  
- **豐富輸出** – 除了行矩形外，還可取得單字、字元與信心分數。

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| **未返回矩形** | 確保影像包含清晰的水平文字，且已指定 `AreasType.LINES`。 |
| **座標不正確** | 檢查影像 DPI；低解析度影像可能導致邊界不準確。 |
| **大型影像的效能瓶頸** | 在呼叫 `GetRectangles` 前，將影像調整至合理的解析度。 |
| **授權例外** | 測試時使用試用授權；正式環境請套用完整授權，以避免評估限制。 |

## 常見問與答

**Q: 我可以擷取單獨的單字而非整行嗎？**  
A: 可以，使用 `AreasType.WORDS` 搭配相同的 `GetRectangles` 方法即可取得單字層級的邊界框。

**Q: API 支援多頁 PDF 嗎？**  
A: 先將每頁 PDF 轉為影像，然後對每張影像呼叫 `GetRectangles`。

**Q: 如何處理旋轉的文字？**  
A: 在 OCR 設定中啟用自動旋轉選項，或在處理前先將影像預先旋轉。

**Q: 有辦法取得每行的信心分數嗎？**  
A: 取得矩形後，呼叫 `api.RecognizeImage(...).Lines` 以存取包含信心值的行物件。

**Q: 相容的 .NET 版本有哪些？**  
A: 此程式庫支援 .NET Framework 4.5 以上、 .NET Core 3.1 以上，以及 .NET 5/6。

## 真實案例應用

- **文件版面分析 OCR** – 將行矩形輸入版面引擎，以重建欄位結構。  
- **自動化資料擷取** – 使用座標裁切單獨的行，供後續 NLP 流程使用。  
- **自訂渲染** – 在原始影像上疊加邊界框，以進行視覺驗證或 UI 疊層。

## 結論

恭喜！您已成功使用 Aspose.OCR for .NET 為影像 **取得 OCR 行矩形**。手握這些邊界框後，您現在可以將行座標輸入後續工作流程，例如自訂渲染、資料擷取或 **版面分析 OCR**。

---

**最後更新：** 2026-02-22  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}