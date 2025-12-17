---
date: 2025-12-17
description: 學習如何使用 Aspose.OCR for .NET 從 OCR 圖像中提取段落的矩形——這是關於如何提取矩形及段落座標的首選指南。
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: 如何在 OCR 圖像辨識中提取段落矩形框
url: /zh-hant/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 OCR 圖像辨識中提取段落矩形

## 簡介

歡迎閱讀我們關於 **如何提取矩形** 以取得段落的完整指南，適用於 Aspose.OCR for .NET 的 OCR 圖像辨識。如果您想提升文件處理流程、抽取段落邊界並自動化資料擷取，這裡就是您的起點。我們將逐步說明——從環境設定到列印矩形座標——讓您立即開始使用 OCR 結果。

## 快速解答
- **「提取矩形」是什麼意思？** 它會返回偵測到的文字區域的邊界框（x、y、寬度、高度）。  
- **哪個 API 方法提供矩形？** `AsposeOcr.GetRectangles` 搭配 `AreasType.PARAGRAPHS`。  
- **開發時需要授權嗎？** 免費試用可用於測試；正式環境需要商業授權。  
- **可以一次處理多張圖片嗎？** 可以——對圖片清單迴圈，對每個檔案呼叫 `GetRectangles`。  
- **支援哪些格式？** PNG、JPEG、TIFF、BMP 等多種格式。

## 什麼是 OCR 中的「提取矩形」？
在 OCR 專業術語中，提取矩形指的是辨識圖像中每個段落或文字行的幾何邊界。這些座標讓您能夠突出、裁切或進一步分析掃描文件的特定區段。

## 為什麼要提取段落座標？
- **精確的後處理** – 您可以將每個矩形輸入後續工作流程（例如翻譯、遮蔽）。  
- **提升 UI/UX** – 在原始圖像上疊加邊界框，讓使用者看到文字所在位置。  
- **批次自動化** – 快速定位並分離大型文件集中的段落。

## 先決條件

- 具備 C# 與 .NET 開發的基本知識。  
- 已安裝 Aspose.OCR for .NET 的開發環境 – 您可以在[此處](https://releases.aspose.com/ocr/net/)下載。  
- 熟悉影像處理概念，了解 OCR 為何在從掃描檔案提取文字時至關重要。

## 匯入命名空間

在您的 C# 檔案中匯入所需的命名空間，以便使用 OCR 類別：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 步驟 1：設定文件目錄

定義包含您要分析的圖像的資料夾：

```csharp
string dataDir = "Your Document Directory";
```

## 步驟 2：初始化 AsposeOcr 實例

建立一個 `AsposeOcr` 物件——這會讓您存取所有 OCR 功能：

```csharp
AsposeOcr api = new AsposeOcr();
```

## 步驟 3：指定圖像路徑

指向您想要處理的確切圖像檔案：

```csharp
string fullPath = dataDir + "sample.png";
```

## 步驟 4：辨識圖像並取得段落矩形

呼叫 `GetRectangles` 方法。將 `detect_areas` 設為 `true` 會告訴引擎返回 **段落** 矩形：

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## 步驟 5：列印結果

輸出座標，以便您看到偵測到的 **提取段落座標**：

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|------|------|----------|
| 未返回矩形 | 圖像品質太低或 `AreasType` 錯誤 | 確保圖像清晰，並使用 `AreasType.PARAGRAPHS`。 |
| 座標偏差一個像素 | DPI 縮放不匹配 | 載入圖像時設定正確的 DPI，或使用 `api.Config.Dpi`。 |
| 授權例外 | 在生產環境未使用有效授權 | 透過 `api.SetLicense` 套用臨時或永久授權。 |

## 常見問答

**Q: Aspose.OCR 是否相容於不同的圖像格式？**  
A: 是的，Aspose.OCR 支援 PNG、JPEG、TIFF、BMP 等多種常見格式。

**Q: 我可以使用 Aspose.OCR 進行多張圖像的批次處理嗎？**  
A: 當然可以！遍歷檔案路徑集合，對每張圖像呼叫 `GetRectangles`。

**Q: 是否有 Aspose.OCR for .NET 的免費試用？**  
A: 有，您可以在[此處](https://releases.aspose.com/)探索免費試用。

**Q: 如何取得 Aspose.OCR 的臨時授權？**  
A: 您可以在[此處](https://purchase.aspose.com/temporary-license/)取得臨時授權。

**Q: 哪裡可以找到與 Aspose.OCR 相關的其他支援與討論？**  
A: 前往[Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16)取得社群支援與討論。

## 結論

在本教學中，我們示範了 **如何提取矩形** 以取得段落，使用 Aspose.OCR for .NET，逐步說明每段程式碼，並解釋如何解讀返回的座標。將這些步驟整合到您的應用程式後，您即可可靠地抽取段落邊界、提升文件工作流程，並打造更智慧的 OCR 驅動解決方案。

---

**最後更新：** 2025-12-17  
**測試版本：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}