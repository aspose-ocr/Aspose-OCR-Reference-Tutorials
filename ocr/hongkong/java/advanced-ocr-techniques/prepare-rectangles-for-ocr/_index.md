---
date: 2026-02-20
description: 學習如何使用 Aspose.OCR for Java 識別頁面矩形、提取文字圖像 Java 專案，並遵循此 Aspose OCR Java
  教學以實現精準 OCR。
linktitle: How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: 如何在 Aspose.OCR 中辨識頁面矩形以進行 OCR 文字辨識
url: /zh-hant/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Aspose.OCR 中辨識頁面矩形以進行 OCR 文字辨識

在現代文件自動化流程中，**recognize page rectangles** 是讓您告訴 OCR 引擎確切搜尋位置的關鍵技術。透過將 Aspose.OCR 限制於實際包含文字的區域，您可以提升速度、減少雜訊，並獲得更乾淨的結果。在本教學中，我們將逐步說明每個步驟——設定函式庫、授權、定義矩形，最後呼叫 OCR API——讓您能自信地從任何影像中擷取文字。

## 快速答覆
- **什麼函式庫負責 Java 中的 OCR 文字辨識？** Aspose.OCR for Java.  
- **在正式環境使用是否需要授權？** 是 – 有效的 Aspose.OCR 授權可解鎖完整功能。  
- **我可以將 OCR 限制在影像的特定部分嗎？** 當然可以；您可以定義界定目標區域的矩形。  
- **主要前置條件是什麼？** JDK 17+、Aspose.OCR for Java 以及 Java IDE。  
- **此方法適合從影像中擷取文字嗎？** 是的，這是 **extract text image java** 專案的高效方式。

## 什麼是「recognize page rectangles」？
此詞指的是向 OCR 引擎提供一系列 `java.awt.Rectangle` 物件，以便僅處理頁面上那些特定區域的做法。此聚焦方式可縮短處理時間並提升準確度，尤其在發票或表單等複雜文件上更為顯著。

## 為何要為 OCR 文字辨識準備矩形？
定義矩形可將引擎聚焦於實際包含文字的區域，從而：
* 縮短處理時間。  
* 透過忽略雜訊背景提升準確度。  
* 只擷取您需要的資料——非常適合表單、發票與收據。  

## 前置條件

在開始之前，請確保您已具備：

- **Java Development Kit (JDK)** – Aspose.OCR for Java 支援 JDK 17 或更新版本。請從 Oracle 官方網站下載。  
- **Aspose.OCR for Java library** – 從官方下載頁面 [here](https://releases.aspose.com/ocr/java/) 取得最新 JAR。安裝說明請參考 [here](https://reference.aspose.com/ocr/java/)。  
- **Development Environment** – 任意 Java IDE（如 IntelliJ IDEA、Eclipse、VS Code 等）皆可。

## 匯入套件

在您的 Java 原始檔中，匯入所需的 Aspose.OCR 類別與標準 Java 工具：

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *我們匯入 `java.awt.Rectangle`，因為 OCR API 需要用矩形來定義要掃描的區域。*

## 步驟 1：設定授權

```java
SetLicense.main(null);
```

呼叫 `SetLicense` 會啟用您的 Aspose.OCR 授權，移除評估限制並開啟完整功能的 OCR 文字辨識。

## 步驟 2：定義文件目錄與影像路徑

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

將 `"Your Document Directory"` 替換為放置影像 (`p.png`) 的絕對路徑。此影像即為待處理的檔案。

## 步驟 3：建立 Aspose.OCR 實例

```java
AsposeOCR api = new AsposeOCR();
```

實例化 `AsposeOCR` 後，即可使用 `RecognizePage` 方法執行實際的 OCR。

## 步驟 4：準備含文字的矩形

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

每個 `Rectangle(x, y, width, height)` 告訴 Aspose.OCR 正確的文字搜尋位置。請依來源影像的版面調整座標。

## 步驟 5：執行 OCR 辨識

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` 呼叫僅處理已定義的矩形，並回傳擷取的字串。主控台輸出可即時驗證 **ocr text recognition** 結果。

## 常見問題與技巧

| Issue | Cause | Solution |
|-------|-------|----------|
| **無輸出** | 矩形座標或影像路徑不正確 | 再次確認 `dataDir` 的值，並確保矩形實際覆蓋文字區域。 |
| **雜訊字元** | 低解析度影像或不支援的字型 | 使用較高解析度的來源，或進行影像前處理（例如二值化）。 |
| **授權未套用** | `SetLicense` 未於 OCR 前呼叫 | 確保在任何 API 呼叫前執行 `SetLicense.main(null);`。 |
| **效能延遲** | 矩形過多且尺寸過大 | 限制矩形數量，且盡可能緊貼文字區域。 |

## 常見問答

**Q:** *Aspose.OCR 是否相容其他程式語言？*  
**A:** 是，Aspose.OCR 亦支援 .NET、C++ 與 Python。請參閱官方文件取得各語言範例。

**Q:** *我可以在商業專案中使用 Aspose.OCR 嗎？*  
**A:** 當然可以。請透過 [Aspose store](https://purchase.aspose.com/buy) 購買商業授權。

**Q:** *是否提供免費試用？*  
**A:** 有，您可在 [here](https://releases.aspose.com/) 下載試用版。

**Q:** *如何取得評估用的臨時授權？*  
**A:** 臨時授權可透過 [Aspose temporary‑license portal](https://purchase.aspose.com/temporary-license/) 取得。

**Q:** *哪裡可以取得社群支援？*  
**A:** 請前往 Aspose.OCR [forum](https://forum.aspose.com/c/ocr/16) 提問、交流技巧與程式碼範例。

## 結論

您現在已學會如何使用 Aspose.OCR for Java **recognize page rectangles**、設定授權、定義影像路徑，且最重要的是，準備緊密的矩形以將 OCR 聚焦於影像中所需的精確區域。此技巧非常適合任何需要精確、高效文字擷取的 **aspose ocr java tutorial**。

---

**最後更新：** 2026-02-20  
**測試環境：** Aspose.OCR for Java 24.12  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}