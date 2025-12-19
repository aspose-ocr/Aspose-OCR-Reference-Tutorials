---
date: 2025-12-06
description: 學習如何使用 Aspose.OCR for Java 進行 OCR 文字辨識、從圖像中提取文字，並準備矩形以進行目標辨識。
linktitle: Preparing Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: 在 Aspose.OCR 中為文字識別準備矩形
url: /zh-hant/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 為 Aspose.OCR 準備 OCR 文字辨識用的矩形區域

## 介紹

在當今資料驅動的世界，**OCR 文字辨識** 是將掃描文件、螢幕截圖與相片轉換為可搜尋、可編輯內容的基礎。Aspose.OCR for Java 讓這個過程快速且可靠，特別是當您需要聚焦於影像的特定區域時。本教學將逐步說明如何準備矩形，以限制 OCR 只在您關心的區域執行，從而提供精確的控制與更佳的效能。

## 快速回答
- **哪個函式庫在 Java 中處理 OCR 文字辨識？** Aspose.OCR for Java。  
- **正式環境需要授權嗎？** 需要 – 有效的 Aspose.OCR 授權可解鎖完整功能。  
- **可以將 OCR 限制在影像的某些部分嗎？** 當然可以；只要定義矩形即可框住目標區域。  
- **主要前置條件是什麼？** JDK 17+、Aspose.OCR for Java，以及 Java IDE。  
- **此方法適合從影像中擷取文字嗎？** 是的，這是 **extract text image java** 專案的高效方式。

## 什麼是 OCR 文字辨識？
OCR（光學字符辨識）將像素圖像轉換為機器可讀的文字。它讓您能搜尋、編輯與分析原本僅以圖片形式存在的內容。

## 為什麼要為 OCR 文字辨識準備矩形？
定義矩形可讓引擎聚焦於實際包含文字的區域，從而：
* 減少處理時間。  
* 透過忽略雜訊背景提升準確度。  
* 只擷取您需要的資料——非常適合表單、發票與收據。

## 前置條件

開始之前，請確保您已具備：

- **Java Development Kit (JDK)** – Aspose.OCR for Java 支援 JDK 17 或更新版本。請從 Oracle 官方網站下載。  
- **Aspose.OCR for Java 函式庫** – 從官方下載頁面取得最新 JAR 檔案 [此處](https://releases.aspose.com/ocr/java/)。安裝說明請參考 [此處](https://reference.aspose.com/ocr/java/)。  
- **開發環境** – 任意 Java IDE（IntelliJ IDEA、Eclipse、VS Code 等）皆可。

## 匯入套件

在 Java 原始檔中匯入必要的 Aspose.OCR 類別與標準 Java 工具：

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *我們匯入 `java.awt.Rectangle`，因為 OCR API 需要矩形來定義要掃描的區域。*

## 步驟 1：設定授權

```java
SetLicense.main(null);
```

呼叫 `SetLicense` 會啟用您的 Aspose.OCR 授權，移除評估限制並開啟完整的 OCR 文字辨識功能。

## 步驟 2：定義文件目錄與影像路徑

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

將 `"Your Document Directory"` 替換為放置影像 (`p.png`) 的絕對路徑。此影像即為待處理的檔案。

## 步驟 3：建立 Aspose.OCR 物件

```java
AsposeOCR api = new AsposeOCR();
```

實例化 `AsposeOCR` 後，即可使用 `RecognizePage` 方法執行實際的 OCR。

## 步驟 4：準備帶文字的矩形

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

每個 `Rectangle(x, y, width, height)` 都告訴 Aspose.OCR 要在何處尋找文字。請依照來源影像的版面配置調整座標。

## 步驟 5：執行 OCR 辨識

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` 只會處理先前定義的矩形，並回傳擷取的字串。主控台輸出可即時驗證 **OCR 文字辨識** 結果。

## 常見問題與技巧

| 問題 | 原因 | 解決方案 |
|------|------|----------|
| **沒有輸出** | 矩形座標或影像路徑不正確 | 再次確認 `dataDir` 的值，並確保矩形實際覆蓋文字區域。 |
| **出現雜訊字元** | 影像解析度過低或字型不支援 | 使用較高解析度的來源，或先行做影像前處理（例如二值化）。 |
| **授權未生效** | `SetLicense` 未於 OCR 前呼叫 | 確保在任何 API 呼叫前執行 `SetLicense.main(null);`。 |
| **效能延遲** | 矩形過多且尺寸過大 | 減少矩形數量，並盡可能緊貼文字範圍。 |

## 結論

您現在已學會如何整合 Aspose.OCR for Java、設定授權、定義影像路徑，最重要的是，如何準備矩形以將 **OCR 文字辨識** 聚焦於影像的特定部位。此技巧非常適合任何需要精準、高效文字擷取的 **java ocr tutorial**。

## 常見問答

**Q: Aspose.OCR 是否支援其他程式語言？**  
A: 支援，此外還有 .NET、C++ 與 Python。請參閱官方文件取得各語言範例。

**Q: 可以在商業專案中使用 Aspose.OCR 嗎？**  
A: 當然可以。可於 [Aspose 商店](https://purchase.aspose.com/buy) 購買商業授權。

**Q: 有提供免費試用嗎？**  
A: 有，您可在此下載試用版 [此處](https://releases.aspose.com/)。  

**Q: 如何取得暫時授權以進行評估？**  
A: 暫時授權可透過 [Aspose 暫時授權入口](https://purchase.aspose.com/temporary-license/) 取得。

**Q: 哪裡可以獲得社群支援？**  
A: 請前往 Aspose.OCR [論壇](https://forum.aspose.com/c/ocr/16) 交流問題、技巧與程式碼範例。

---

**最後更新：** 2025-12-06  
**測試環境：** Aspose.OCR for Java 24.12  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
