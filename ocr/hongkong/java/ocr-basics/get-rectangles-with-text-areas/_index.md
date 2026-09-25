---
date: 2026-02-09
description: 學習如何使用 Aspose OCR Java 函式庫將圖像轉換為文字，並擷取文字區域矩形。一步一步的指南，附有程式碼範例。
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: 將圖像轉換為文字 – 從圖像辨識文字並取得文字區域矩形
url: /zh-hant/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 轉換圖像為文字 – 從圖像辨識文字並取得文字區域矩形

## 介紹

如果您需要在 Java 應用程式中 **convert image to text** 與 **recognize text from image**，Aspose.OCR for Java 提供快速且高精度的解決方案。本教學將逐步說明如何從圖像中擷取段落、取得每個文字區域的邊界矩形，並將座標輸出至主控台。完成後，您將了解此方法的原理、如何整合此函式庫，以及可自行擴充的應用情境。

## 快速答覆
- **「recognize text from image」是什麼意思？** 代表將圖片中的視覺字元轉換成可編輯的字串資料。  
- **哪個函式庫在 Java 中負責此功能？** Aspose.OCR for Java。  
- **開發時需要授權嗎？** 可取得暫時授權供測試使用；正式上線則需購買完整授權。  
- **可以擷取段落而非單字嗎？** 可以 – 使用 `AreasType.PARAGRAPHS` 取得段落層級的矩形。  
- **程式碼是否相容於 Java 11 以上？** 完全相容，API 支援 Java 11 及更新版本。

## Aspose.OCR 中的「convert image to text」是什麼？

Aspose.OCR 的 `RecognizePage` 方法會分析位圖、套用 OCR 演算法，並回傳辨識出的字串。當您要求取得文字區域時，函式庫同時會計算每個文字區塊的精確 `Rectangle` 座標，方便日後高亮或進一步處理特定區段。

## 為何選擇這個 **java ocr library**？

- **高精度** – 支援多種語言與複雜字型。  
- **易於整合** – 單一 JAR 即可加入完整 OCR 功能。  
- **彈性輸出** – 可取得原始文字、格式化 HTML，或精確的文字區域矩形。  
- **執行緒安全** – 適用於高吞吐量的伺服器環境。

## 前置條件

- 已在電腦上安裝 **Java Development Kit**（JDK 11 或更新版本）。  
- 下載 **Aspose.OCR for Java** 函式庫，請至官方網站 [here](https://releases.aspose.com/ocr/java/) 取得。  
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
建立新的 Java 專案（或在既有專案中加入），將 Aspose.OCR JAR 放入 classpath。若使用 Maven，請依下載套件中的說明加入相依性。

### 步驟 2：定義文件目錄與圖像路徑
指定範例圖像所在的位置：

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### 步驟 3：建立 Aspose.OCR 實例
建立 OCR 引擎物件：

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### 步驟 4：辨識圖像中的文字
呼叫 `RecognizePage` 將圖片轉換為純文字。此步驟示範核心的 **recognize text image java** 功能：

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
現在取得每個段落（或其他區域類型）的邊界矩形。這就是 **extract paragraphs from image** 並取得其座標的地方：

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
| `IOException` on `RecognizePage` | 檔案路徑錯誤或缺少讀取權限 | 確認 `imagePath` 指向已存在的 PNG/JPG，且應用程式具備檔案系統存取權限。 |
| 結果字串為空 | 圖像品質低或語言不支援 | 前處理圖像（提升對比、二值化）或使用 `api.setLanguage("eng")` 指定正確語言。 |
| 未返回矩形 | 使用錯誤的 `AreasType`（例如使用 `WORDS` 卻期待段落） | 改為 `AreasType.PARAGRAPHS` 或視需求改用 `AreasType.LINES`。 |

## 常見問答

**Q: Aspose.OCR 是否相容於 Java 11？**  
A: 是的，Aspose.OCR 可在 Java 11 及更新版本上執行。

**Q: 我可以在個人與商業專案中使用 Aspose.OCR 嗎？**  
A: 可以，任何類型的專案皆可使用。授權細節請參閱 [here](https://purchase.aspose.com/buy)。

**Q: 如何取得評估用的暫時授權？**  
A: 可於此取得暫時授權 [here](https://purchase.aspose.com/temporary-license/)。

**Q: 哪裡可以找到社群支援或官方協助？**  
A: 請前往 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 參與討論與求助。

**Q: Aspose.OCR 支援多執行緒嗎？**  
A: 支援，函式庫為執行緒安全，可在並行環境下提升效能。

## 結論

在本 **aspose ocr java tutorial** 中，您學會了如何使用 Aspose.OCR for Java **convert image to text**、擷取段落，並取得每個文字區塊的精確矩形。這些功能可協助您建立可搜尋的 PDF、在 UI 上高亮文字，或將結構化資料輸入後續流程。建議進一步探索 API，客製化語言設定、處理不同圖像格式，或整合雲端儲存服務。

---

**Last Updated:** 2026-02-09  
**Tested With:** Aspose.OCR 23.10 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}