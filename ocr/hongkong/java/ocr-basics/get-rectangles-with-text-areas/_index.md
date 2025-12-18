---
date: 2025-12-10
description: 學習如何使用 Aspose.OCR for Java 從圖像中識別文字並提取段落。一步一步的指南，附有程式碼範例。
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: 從圖片辨識文字並取得文字區域矩形
url: /zh-hant/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像識別文字並取得文字區域矩形

## 介紹

如果您需要在 Java 應用程式中 **從圖像識別文字**，Aspose.OCR for Java 提供快速且高精度的解決方案。本教學將逐步說明如何從圖像中擷取段落、取得每個文字區域的邊界矩形，並將座標輸出至主控台。完成後，您將了解此方法的原理、如何整合此函式庫，以及可以在哪裡延伸以符合自己的使用情境。

## 快速答覆
- **「從圖像識別文字」是什麼意思？** 代表將圖片中的視覺字符轉換為可編輯的字串資料。  
- **哪個 Java 函式庫負責此功能？** Aspose.OCR for Java。  
- **開發階段需要授權嗎？** 可使用測試授權；正式上線需購買正式授權。  
- **可以擷取段落而非單字嗎？** 可以 – 使用 `AreasType.PARAGRAPHS` 取得段落層級的矩形。  
- **程式碼是否相容於 Java 11 以上？** 完全相容，API 支援 Java 11 及更高版本。

## Aspose.OCR 中的「從圖像識別文字」是什麼？
Aspose.OCR 的 `RecognizePage` 方法會分析位圖、套用 OCR 演算法，並回傳辨識後的字串。當您要求文字區域時，函式庫同時會計算每個文字區塊的精確 `Rectangle` 座標，讓您日後能輕鬆標示或處理特定區段。

## 為什麼選擇 Aspose.OCR for Java？
- **高精度** – 支援多種語言與複雜字型。  
- **易於整合** – 單一 JAR 即可加入完整 OCR 功能。  
- **彈性輸出** – 可取得原始文字、格式化 HTML，或精確的文字區域矩形。  
- **執行緒安全** – 適用於高吞吐量的伺服器環境。

## 前置條件

- 已在電腦上安裝 **Java Development Kit**（JDK 11 或更新版本）。  
- 取得 **Aspose.OCR for Java** 函式庫 – 可從官方網站[此處](https://releases.aspose.com/ocr/java/)下載。  
- 具備 IDE 或建置工具（Maven/Gradle）以管理 JAR 相依性。

## 匯入套件

在您的 Java 專案中匯入必要的類別：

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## 步驟說明

### 步驟 1：設定專案
建立新的 Java 專案（或在既有專案中加入），並將 Aspose.OCR JAR 放入 classpath。若使用 Maven，請依下載套件內說明加入相依性。

### 步驟 2：定義文件目錄與圖像路徑
指定範例圖像所在位置：

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### 步驟 3：建立 Aspose.OCR 實例
建立 OCR 引擎：

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### 步驟 4：在圖像中辨識文字
呼叫 `RecognizePage` 將圖片轉換為純文字。此步驟示範核心的 **從圖像識別文字** 功能：

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### 步驟 5：取得文字區域的矩形
現在取得每個段落（或其他區域類型）的邊界矩形。這就是 **從圖像擷取段落** 並取得其座標的地方：

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## 常見問題與除錯

| 症狀 | 可能原因 | 解決方式 |
|------|----------|----------|
| `IOException` 發生於 `RecognizePage` | 檔案路徑錯誤或缺少讀取權限 | 確認 `imagePath` 指向已存在的 PNG/JPG，且應用程式具備檔案系統存取權限。 |
| 結果字串為空 | 圖像品質低或語言不支援 | 前處理圖像（提升對比、二值化）或使用 `api.setLanguage("eng")` 指定正確語言。 |
| 未返回矩形 | 使用了錯誤的 `AreasType`（例如 `WORDS` 而期待段落） | 改為 `AreasType.PARAGRAPHS` 或視需求改用 `AreasType.LINES`。 |

## 常見問答

**Q: Aspose.OCR 是否相容於 Java 11？**  
A: 是的，Aspose.OCR 可在 Java 11 及之後的版本執行。

**Q: 可以在個人與商業專案中使用 Aspose.OCR 嗎？**  
A: 可以，任何類型的專案皆可使用。授權細節請參閱[此處](https://purchase.aspose.com/buy)。

**Q: 如何取得評估用的臨時授權？**  
A: 可於[此處](https://purchase.aspose.com/temporary-license/)取得臨時授權。

**Q: 哪裡可以找到社群支援或官方協助？**  
A: 請前往 [Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16) 參與討論與支援。

**Q: Aspose.OCR 支援多執行緒嗎？**  
A: 支援，函式庫為執行緒安全，可在並行環境中使用以提升效能。

## 結論

本教學說明了如何使用 Aspose.OCR for Java **從圖像識別文字**、擷取段落，並取得每個文字區塊的精確矩形。這些功能可協助您建立可搜尋的 PDF、在 UI 之上高亮文字，或將結構化資料傳遞至後續流程。建議進一步探索 API，以自訂語言設定、處理不同圖像格式，或整合雲端儲存服務。

---

**最後更新：** 2025-12-10  
**測試環境：** Aspose.OCR 23.10 for Java  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}