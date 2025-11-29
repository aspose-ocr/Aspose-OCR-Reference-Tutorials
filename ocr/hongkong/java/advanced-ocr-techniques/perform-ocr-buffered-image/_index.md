---
date: 2025-11-29
description: 學習如何使用 Java OCR 函式庫從圖像中提取文字。本指南展示如何安裝 Aspose OCR、處理多種語言，以及使用各種 OCR 圖像格式。
language: zh-hant
linktitle: Performing OCR on BufferedImage in Aspose.OCR for Java
second_title: Aspose.OCR Java API
title: 使用 Java OCR 函式庫 (Aspose.OCR) 對 BufferedImage 執行 OCR
url: /java/advanced-ocr-techniques/perform-ocr-buffered-image/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 BufferedImage 上使用 Java OCR 函式庫 (Aspose.OCR) 進行 OCR

## 簡介

如果您需要 **從 Java 中的影像擷取文字**，可靠的 *java ocr library* 是必不可少的。在本教學中，我們將示範如何使用 Aspose.OCR——一個功能強大的 Java OCR 函式庫，直接從 `BufferedImage` 進行文字辨識。您將看到如何設定函式庫、載入影像，並取得辨識後的字串，整個流程只需幾行程式碼。

## 快速答覆
- **什麼是最佳的 java ocr library？** Aspose.OCR for Java 提供高準確度與廣泛的語言支援。  
- **如何安裝 Aspose OCR？** 從 Aspose 官方網站下載 JAR，並將其加入專案的 classpath。  
- **可以辨識多種語言嗎？** 可以——Aspose.OCR 內建支援多語言 OCR。  
- **支援哪些影像格式？** 函式庫支援常見的 OCR 影像格式，如 PNG、JPEG、BMP 與 TIFF。  
- **典型的文字擷取程式碼是什麼？** 將影像載入 `BufferedImage`，建立 `AsposeOCR` 實例，然後呼叫 `RecognizePage`。

## 什麼是 Java OCR 函式庫？
*java ocr library* 是一組 Java 類別，能分析點陣圖並將視覺文字轉換為機器可讀的字串。Aspose.OCR for Java 就是這樣的一套函式庫，提供高精度辨識、語言偵測，以及對多種影像格式的支援。

## 為什麼選擇 Aspose.OCR for Java？
- **高準確度**，適用於印刷與手寫文件。  
- **支援多語言 OCR**，包括英文、法文、德文、中文等多種語言。  
- 簡易 API，可直接與 `BufferedImage` 搭配，免除中間檔案轉換。  
- 完整支援 **ocr image formats** 如 PNG、JPEG、BMP、TIFF 與 GIF。

## 前置條件

在開始之前，請確保您已具備以下項目：

1. **Java Development Kit (JDK)** – 任意近期版本（8 或以上）。從 [Oracle](https://www.oracle.com/java/technologies/javase-downloads.html) 下載。  
2. **Aspose.OCR for Java 函式庫** – 從 Aspose 下載頁面取得最新 JAR（[install aspose ocr](https://releases.aspose.com/ocr/java/)）。  
3. **放置範例影像的資料夾** – 在程式碼中將 `dataDir` 變數指向該資料夾。

## 匯入套件

開始之前，先匯入所需的類別。此區塊保持不變，只是將 Aspose OCR API 與 Java I/O 工具載入作用域。

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;
```

## 如何在 BufferedImage 上執行 OCR

我們將一步一步說明整個流程。每一步都包含簡短說明與對應的程式碼片段（保持原樣）。

### 步驟 1：設定文件目錄與影像路徑  
定義影像所在的位置，並指向要處理的檔案。

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

> **專業提示：** 開發階段建議使用絕對路徑以避免 `FileNotFoundException`，上線前再改為相對路徑。

### 步驟 2：建立 AsposeOCR 實例  
建立 OCR 引擎物件。此物件提供所有辨識方法的存取權。

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

### 步驟 3：從 BufferedImage 進行頁面辨識  
將影像載入 `BufferedImage`，執行 OCR 引擎，並將結果印出。

```java
// Recognize page from BufferedImage
try {
    BufferedImage loaded = ImageIO.read(new File(imagePath));
    String result = api.RecognizePage(loaded);
    System.out.println("Result BufferedImage: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

**發生了什麼？**  
1. `ImageIO.read` 讀取檔案並以 `BufferedImage` 形式載入記憶體。  
2. `api.RecognizePage` 執行實際的 OCR 作業。  
3. 辨識出的文字以 `String` 形式回傳，並印到主控台。

依需求重複上述三個步驟即可處理多張影像——只要更改 `imagePath` 即可。

## 常見問題與解決方案

| 問題 | 原因 | 解決方法 |
|------|------|----------|
| `NullPointerException` on `loaded` | 找不到影像檔或格式不支援 | 核對路徑，並確保檔案為支援的 **ocr image format**（PNG、JPEG、BMP、TIFF）。 |
| 輸出亂碼 | 未設定語言或字符不受支援 | AsposeOCR 會自動偵測語言，但可使用 `api.setLanguage("eng")` 明確指定英文或其他 ISO 代碼。 |
| 大影像效能緩慢 | 高解析度佔用大量記憶體 | 在辨識前使用 `BufferedImage.getScaledInstance` 降低影像尺寸。 |

## 常見問題 (原始版)

### Q1：Aspose.OCR 能處理多種語言嗎？

A1：可以，Aspose.OCR 支援廣泛的語言，適用於各種文字辨識需求。

### Q2：Aspose.OCR 與不同的影像格式相容嗎？

A2：絕對相容！Aspose.OCR 能處理多種格式的影像，為您的 OCR 專案提供彈性。

### Q3：Aspose.OCR 更新頻率如何？

A3：Aspose 會定期釋出更新，增強功能並修正問題。請參考他們的 [documentation](https://reference.aspose.com/ocr/java/) 取得最新資訊。

### Q4：購買前可以先試用 Aspose.OCR 嗎？

A4：可以，請於此處取得免費試用版 [here](https://releases.aspose.com/)。

### Q5：在哪裡可以取得 Aspose.OCR 的社群支援？

A5：請前往 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 參與討論與取得支援。

## 其他常見問題（新）

**Q：如何在 Maven 專案中安裝 Aspose OCR？**  
A：在 `pom.xml` 中加入 Aspose OCR 的相依性，座標請參考 Aspose 下載頁面提供的資訊。

**Q：可以使用此函式庫從掃描的 PDF 中擷取文字嗎？**  
A：可以——先將每頁 PDF 轉為影像（例如使用 Aspose.PDF），再套用相同的 `BufferedImage` OCR 工作流程。

**Q：函式庫支援彩色影像的 OCR 嗎？**  
A：支援。Aspose OCR 可處理彩色、灰階與二值影像；不過高對比的黑白影像通常能取得最佳準確度。

**Q：一次執行可以處理多少頁？**  
A：沒有硬性上限，但記憶體使用量會隨影像大小增加。建議將大量批次分段處理，以免發生 `OutOfMemoryError`。

**Q：如何提升手寫文字的辨識準確度？**  
A：啟用手寫模式（若有提供），或在辨識前先對影像做前處理，提高對比度並降低雜訊。

---

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**最後更新：** 2025-11-29  
**測試環境：** Aspose.OCR 24.11 for Java  
**作者：** Aspose