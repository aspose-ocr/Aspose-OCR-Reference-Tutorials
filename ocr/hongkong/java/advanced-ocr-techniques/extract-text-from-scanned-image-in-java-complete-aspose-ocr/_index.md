---
category: general
date: 2026-06-06
description: 使用 Aspose OCR for Java 從掃描圖像中提取文字。了解如何使用平行處理辨識 TIFF 檔案的文字。
draft: false
keywords:
- extract text from scanned image
- recognize text from tiff
- Aspose OCR Java tutorial
- parallel OCR processing
- Java image recognition
language: zh-hant
og_description: 使用 Aspose OCR 從掃描圖像中提取文字。本指南說明如何使用 Java 高效辨識 tiff 檔案中的文字。
og_title: 從掃描圖像提取文字 – Aspose OCR Java 教程
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  headline: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  type: TechArticle
- description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  name: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  steps:
  - name: Maven users
    text: 'Add the following dependency to your `pom.xml`:'
  - name: Manual JAR setup
    text: Download the latest `aspose-ocr-xx.jar` from the Aspose website and place
      it on your classpath.
  - name: Expected Output
    text: '``` === Extracted Text === Invoice Number: 12345 Date: 2024‑05‑01 Total:
      $1,250.00 ... ```'
  - name: What’s Next?
    text: '- **Batch processing**: Loop over a directory of TIFFs, store each result
      in its own file. - **Integrate with Elasticsearch**: Index the extracted text
      for fast full‑text search. - **Add language detection**: Use `OcrLanguage.AutoDetect`
      for multi‑lingual documents.'
  type: HowTo
- questions:
  - answer: Absolutely. `OcrInputImage` accepts any format that Java’s ImageIO can
      read. Just replace the file extension in the path.
    question: Does this work with PNG or JPEG files?
  - answer: You could, but remember other services may need CPU cycles. A good rule
      of thumb is “total cores – 1” for dedicated OCR workers.
    question: My server has 8 cores—should I set `setMaxThreads(8)`?
  - answer: 'Check that the image isn’t completely white, that you set the correct
      language, and that the resolution is at least 200 DPI. Low‑quality scans often
      need pre‑processing (deskew, contrast boost) before feeding them to Aspose OCR.
      --- ## Wrap‑Up We’ve just **extracted text from scanned image** files u'
    question: What if the OCR result is empty?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- Image Processing
title: 在 Java 中從掃描影像提取文字 – 完整的 Aspose OCR 指南
url: /zh-hant/java/advanced-ocr-techniques/extract-text-from-scanned-image-in-java-complete-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從掃描圖像提取文字 – 完整 Aspose OCR 指南

有沒有曾經需要**從掃描圖像提取文字**卻卡在「怎麼做？」上？你並不孤單。無論是數位化舊檔案、從發票中抽取資料，或是建立可搜尋的 PDF 資料庫，從 TIFF 掃描檔取得可靠文字都可能是個痛點。

好消息：使用 Aspose OCR for Java，你只需幾行程式碼就能**recognize text from tiff**檔案，甚至透過限制引擎使用少量 CPU 核心來提升速度。在本教學中，我們將一步步說明整個流程——從設定函式庫到處理結果——讓你可以立即 copy‑paste 一個可執行的範例。

## 本教學涵蓋內容

- 安裝 Aspose OCR for Java（Maven 或手動 JAR）
- 載入大型掃描 TIFF 圖像
- 設定引擎使用最多 4 個執行緒（平行 OCR）
- 執行 OCR 程序並印出提取的文字
- 常見問題（記憶體、多頁 TIFF）與避免方式
- 快速效能小技巧：何時調整 `setMaxThreads`

完成後，你將能可靠地**extract text from scanned image**檔案，並了解在生產環境中*recognize text from tiff*時為何調整執行緒數量很重要。

---

![extract text from scanned image example](example.png "Screenshot showing extracted text from a scanned TIFF image")

## 前置條件

在開始之前，請確保你已具備：

1. **Java Development Kit (JDK) 8+** – 任意近期版本皆可。
2. **Maven**（或手動加入 JAR 的能力）– 本教學以 Maven 為例說明。
3. 一份 **Aspose OCR for Java** 授權（免費評估版亦可使用，但會加上浮水印）。  
4. 一個 **大型 TIFF 掃描檔**（例如 `large_scan.tif`）供你處理。

如果上述任何項目你不熟悉，也別擔心——以下每一步都會詳細說明。

## 第 1 步：將 Aspose OCR 加入專案

### Maven 使用者

在你的 `pom.xml` 中加入以下相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version on Maven Central -->
</dependency>
```

### 手動 JAR 設定

從 Aspose 官方網站下載最新的 `aspose-ocr-xx.jar`，並將其放入 classpath。

> **專業提示：** 將 JAR 放在 `libs/` 資料夾，並在 IDE 的專案設定中引用。這樣可避免日後出現「class not found」的驚喜。

## 第 2 步：建立簡易 Java 類別

在你的來源資料夾（`src/main/java`）內建立名為 `ParallelOcrDemo.java` 的檔案。此類別將承載完整的 OCR 工作流程。

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Load the scanned TIFF image you want to process
        // Replace the path with the actual location of your image
        ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/large_scan.tif"));

        // Step 2.3: Limit the engine to use up to 4 CPU cores.
        // This is useful on servers where you don't want to hog all cores.
        ocrEngine.getSettings().setMaxThreads(4);

        // Step 2.4: Run the OCR operation
        OcrResult ocrResult = ocrEngine.process();

        // Step 2.5: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **為何限制執行緒數量：** 預設情況下 Aspose OCR 會嘗試使用所有核心，這可能會讓共享機器上的其他服務資源不足。設定 `setMaxThreads(4)` 可讓引擎最多同時執行四個平行工作者——在大多數現代 CPU 上即可獲得明顯加速，同時不會壟斷資源。

## 第 3 步：編譯與執行

在專案根目錄開啟終端機，執行：

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ParallelOcrDemo"
```

若未使用 Maven，請以 `javac` 編譯後執行：

```bash
javac -cp "libs/*" src/main/java/com/example/ocr/ParallelOcrDemo.java
java -cp "libs/*:src/main/java" com.example.ocr.ParallelOcrDemo
```

### 預期輸出

```
=== Extracted Text ===
Invoice Number: 12345
Date: 2024‑05‑01
Total: $1,250.00
...
```

主控台會顯示掃描頁面的純文字版本。若圖像包含多頁，Aspose OCR 會依序串接它們。

## 第 4 步：處理多頁 TIFF（邊緣案例）

常見情況是 **multi‑page TIFF**——例如掃描書本。預設的 `OcrInputImage` 只會讀取第一個影格。若要處理全部頁面，請以 `FileInputStream` 建立 `OcrInputImage`，並啟用多頁支援：

```java
import java.io.FileInputStream;
import com.aspose.ocr.*;

FileInputStream fis = new FileInputStream("YOUR_DIRECTORY/multi_page.tif");
ocrEngine.setImage(new OcrInputImage(fis, true)); // 'true' enables multi‑page
```

現在 `ocrEngine.process()` 會回傳單一 `OcrResult`，其中包含每一頁串接後的文字。

## 第 5 步：微調辨識準確度

如果發現**亂碼**或遺漏字詞，可嘗試以下調整：

| 設定 | 功能說明 | 使用時機 |
|------|----------|----------|
| `ocrEngine.getSettings().setLanguage(OcrLanguage.English)` | 強制使用英語語言模型（對英語掃描更快且更準確） | 文件為單語英語時 |
| `ocrEngine.getSettings().setResolution(300)` | 在辨識前將低解析度影像升級 | 掃描解析度低於 200 DPI 時 |
| `ocrEngine.getSettings().setNoiseRemoval(true)` | 嘗試清除斑點與雜訊 | 掃描噪點較多時 |

範例程式碼：

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setNoiseRemoval(true);
```

## 第 6 步：將結果匯出至檔案

將結果印到主控台適合示範，但正式程式通常會將輸出寫入有用的檔案：

```java
import java.io.FileWriter;
import java.io.IOException;

// After processing
String extractedText = ocrResult.getText();
try (FileWriter writer = new FileWriter("output.txt")) {
    writer.write(extractedText);
}
System.out.println("Text saved to output.txt");
```

如此一來，你就擁有可供搜尋索引、資料庫或下游分析管線使用的純文字檔。

---

## 常見問題 (FAQ)

**Q: 這能用於 PNG 或 JPEG 檔案嗎？**  
**A:** 完全可以。`OcrInputImage` 接受任何 Java ImageIO 能讀取的格式，只要把路徑的副檔名換成相應的即可。

**Q: 我的伺服器有 8 核心——應該設定 `setMaxThreads(8)` 嗎？**  
**A:** 雖然可以，但請記得其他服務也需要 CPU 時脈。一般的經驗法則是「總核心數 – 1」給專屬 OCR 工作者較為安全。

**Q: 若 OCR 結果是空的該怎麼辦？**  
**A:** 請確認影像不是全白、已設定正確的語言，且解析度至少 200 DPI。低品質掃描常需要前置處理（去斜、提升對比）後再交給 Aspose OCR。

## 結語

我們已使用 Aspose OCR for Java **extract text from scanned image**，並了解如何以平行處理有效**recognize text from tiff**。完整程式碼就在上方的程式碼片段，你可以立即 copy‑paste 到自己的專案中。

### 接下來可以做什麼？

- **批次處理**：遍歷 TIFF 目錄，將每個結果存成獨立檔案。  
- **整合 Elasticsearch**：將提取的文字建立索引，以實現快速全文搜尋。  
- **加入語言偵測**：使用 `OcrLanguage.AutoDetect` 處理多語言文件。  

試著實作這些想法，你很快就能把大量掃描文件轉換成可搜尋、可操作的資料。

祝開發順利，若遇到問題歡迎留言討論！

## 接下來該學什麼？

以下教學與本指南所示技術緊密相關，提供完整可執行的程式碼範例與逐步說明，助你掌握更多 API 功能，並在自己的專案中探索其他實作方式。

- [如何使用 Aspose.OCR for Java 識別 TIFF](/ocr/english/java/ocr-operations/recognize-tiff/)
- [提取文字圖像 – Aspose.OCR for Java OCR 基礎](/ocr/english/java/ocr-basics/)
- [使用 Aspose.OCR 偵測區域模式的 Java 圖像文字提取](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}