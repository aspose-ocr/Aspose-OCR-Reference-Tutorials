---
date: 2026-06-19
description: 了解如何在 Java 中將影像轉換為文字、從影像中擷取段落，並使用 Aspose OCR Java 函式庫取得文字區域矩形。
keywords:
- image to text java
- convert scanned image text
- extract paragraphs from image
- aspose ocr java tutorial
linktitle: Image to Text Java – 從影像辨識文字並取得文字區域矩形
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  headline: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  type: TechArticle
- description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  name: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  steps:
  - name: Set Up Your Project
    text: Create a new Java project (or add to an existing one) and place the Aspose.OCR
      JAR on the classpath. If you use Maven, add the dependency as described in the
      download package.
  - name: Define Document Directory and Image Path
    text: 'Specify where your sample image resides:'
  - name: Create AsposeOCR Instance
    text: '`AsposeOCR` is the main class that provides OCR functionality. Instantiate
      the OCR engine:'
  - name: Recognize Text in the Image
    text: Load your image and call `RecognizePage` to convert the picture into plain
      text. This single method call performs image preprocessing, character segmentation,
      and language‑specific recognition in one step.
  - name: Get Rectangles with Text Areas
    text: Retrieve the bounding rectangles for each paragraph (or other area types).
      This step returns a collection of `Rectangle` objects that precisely enclose
      the detected text blocks, enabling you to highlight or further process individual
      sections. CODE_BLOCK_PLACEHOLDER_5_END
  type: HowTo
- questions:
  - answer: Yes, Aspose.OCR works with Java 11 and later versions.
    question: Is Aspose.OCR compatible with Java 11?
  - answer: Yes, you can use it in any type of project. For licensing details, visit
      [here](https://purchase.aspose.com/buy).
    question: Can I use Aspose.OCR for both personal and commercial projects?
  - answer: You can obtain a temporary license [here](https://purchase.aspose.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: For support and discussions, visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).
    question: Where can I find community support or official assistance?
  - answer: Yes, the library is thread‑safe and can be used in concurrent environments
      for better performance.
    question: Does Aspose.OCR support multithreading?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Image to Text Java – 轉換影像為文字並取得文字區域矩形
url: /zh-hant/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java 圖像文字轉換 – 將圖像轉為文字並取得文字區域矩形

## 介紹

如果您需要在 Java 應用程式中 **convert image to text**，Aspose.OCR for Java 提供快速且高精度的解決方案。在本教學中，我們將逐步說明如何從圖像中擷取段落、取得每個文字區域的邊界矩形，並將這些座標輸出至主控台。完成後，您將了解此方法的原理、如何整合此函式庫，以及在哪裡可以為自己的使用情境擴充功能。

## 快速答覆
`AreasType` 是一個列舉，指定文字分割的層級（字詞、行、段落）。

- **What does “recognize text from image” mean?** 它表示將圖片中的視覺字符轉換為可編輯的字串資料。  
- **Which library handles this in Java?** 哪個函式庫在 Java 中處理此功能？ Aspose.OCR for Java。  
- **Do I need a license for development?** 開發時需要授權嗎？ 提供臨時授權供測試使用；正式環境需購買完整授權。  
- **Can I extract paragraphs instead of single words?** 我可以提取段落而不是單字嗎？ 是的 – 使用 `AreasType.PARAGRAPHS` 取得段落層級的矩形。  
- **Is the code compatible with Java 11+?** 此程式碼是否相容於 Java 11 以上？ 絕對相容，API 支援 Java 11 及更高版本。

## 什麼是 Aspose.OCR 中的「convert image to text」？

`convert image to text` 指的是分析位圖、套用 OCR 演算法，並將辨識出的字符以字串回傳的過程。Aspose.OCR 的 `RecognizePage` 方法執行此轉換，同時可選擇提供每個偵測到的文字區塊的精確 `Rectangle` 座標。

## 為什麼使用此 **java ocr library**？

Aspose.OCR 支援 **30+ 種語言**，且可處理高達 **50 MB** 的圖像而無需將整個檔案載入記憶體，在一般伺服器硬體上提供次秒級的回應時間。此函式庫具備執行緒安全性，只需單一 JAR，即可提供彈性的輸出格式——包括原始文字、HTML 以及精確的文字區域矩形——非常適合高吞吐量的企業情境。

## 先決條件

- **Java Development Kit** (JDK 11 或更新版本) 已安裝於您的機器上。  
- **Aspose.OCR for Java** 函式庫 – 從官方網站 [here](https://releases.aspose.com/ocr/java/) 下載。  
- 用於管理 JAR 依賴的 IDE 或建置工具 (Maven/Gradle)。

## 匯入套件

在您的 Java 專案中，匯入必要的類別：

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

## 逐步指南

### 步驟 1：設定您的專案
建立一個新的 Java 專案（或加入現有專案），並將 Aspose.OCR JAR 放置於 classpath 上。若使用 Maven，請依下載套件說明加入相依性。

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### 步驟 2：定義文件目錄與圖像路徑
指定您的範例圖像所在的位置：

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### 步驟 3：建立 AsposeOCR 實例
`AsposeOCR` 是提供 OCR 功能的主要類別。

建立 OCR 引擎的實例：

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### 步驟 4：辨識圖像中的文字
載入您的圖像並呼叫 `RecognizePage` 以將圖片轉換為純文字。此單一方法呼叫會在一步完成圖像前處理、字符分割以及語言特定的辨識。

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

### 步驟 5：取得文字區域的矩形
取得每個段落（或其他區域類型）的邊界矩形。此步驟會回傳 `Rectangle` 物件的集合，精確包圍偵測到的文字區塊，讓您能夠突出顯示或進一步處理各個區段。

CODE_BLOCK_PLACEHOLDER_5_END

## 常見問題與疑難排解

| 症狀 | 可能原因 | 解決方式 |
|---------|--------------|-----|
| `IOException` on `RecognizePage` | 檔案路徑不正確或缺少讀取權限 | 確認 `imagePath` 指向現有的 PNG/JPG，且應用程式具有檔案系統存取權限。 |
| Empty result string | 圖像品質低或語言不受支援 | 對圖像進行前處理（提升對比度、二值化）或使用 `api.setLanguage("eng")` 指定正確語言。 |
| No rectangles returned | 使用了錯誤的 `AreasType`（例如期望段落卻使用 `WORDS`） | 依需求切換為 `AreasType.PARAGRAPHS` 或 `AreasType.LINES`。 |

## 常見問答

**Q: Aspose.OCR 是否相容於 Java 11？**  
A: 是的，Aspose.OCR 可在 Java 11 及之後的版本上運作。

**Q: 我可以在個人與商業專案中使用 Aspose.OCR 嗎？**  
A: 可以，您可在任何類型的專案中使用。授權細節請參閱 [here](https://purchase.aspose.com/buy)。

**Q: 如何取得評估用的臨時授權？**  
A: 您可在 [here](https://purchase.aspose.com/temporary-license/) 取得臨時授權。

**Q: 我可以在哪裡找到社群支援或官方協助？**  
A: 請前往 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 取得支援與討論。

**Q: Aspose.OCR 是否支援多執行緒？**  
A: 是的，該函式庫具備執行緒安全性，可在並行環境中使用以提升效能。

## 結論

在本 **aspose ocr java tutorial** 中，您學會了如何使用 Aspose.OCR for Java **convert image to text**、擷取段落，並取得環繞每個文字區塊的精確矩形。這些功能讓您能建立可搜尋的 PDF、在 UI 蓋層上標示文字，或將結構化資料輸入後續流程。請進一步探索 API，以自訂語言設定、處理不同圖像格式，或整合雲端儲存。

---

**最後更新：** 2026-06-19  
**測試版本：** Aspose.OCR 23.10 for Java  
**作者：** Aspose  

{{< blocks/products/products-backtop-button >}}

## 相關教學

- [擷取文字圖像 – Aspose.OCR for Java OCR 基礎](/ocr/java/ocr-basics/)
- [使用 Aspose.OCR 偵測區域模式從圖像擷取文字 (Java)](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [使用 Aspose.OCR BufferedImage 在 Java 中將圖像轉為文字](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}