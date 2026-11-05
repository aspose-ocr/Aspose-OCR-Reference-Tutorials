---
category: general
date: 2026-06-16
description: Java 的 OCR 邊框教學示範如何從圖像中提取文字、讀取圖像文字，並取得 JPG 檔案的 OCR 可信度分數。
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: zh-hant
og_description: Java 中的 OCR 邊界框讓您能夠從 JPG 檔案辨識文字、從圖像擷取文字，並檢視 OCR 置信度分數——全部於簡易程式範例中。
og_title: Java 中的 OCR 邊界框 – 從圖像提取文字
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: Java 中的 OCR 邊框 – 從圖像提取文字
url: /zh-hant/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Bounding Box in Java – Extract Text from Image

有沒有想過如何在 Java 圖片中取得每段文字的 **ocr bounding box**？在本教學中，我們將示範如何 **extract text from image** 檔案、**read text from image**，以及在 **recognize text from jpg** 時查看 **ocr confidence score**。簡短的答案是：只要幾行程式碼搭配現代 OCR 函式庫，並說明每個呼叫的意義即可。

以下提供完整、可直接執行的範例、逐步說明，以及可直接複製到自己專案的實用技巧。完成後，你將能輸出類似以下的結果：

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## 需要的環境

- **Java 11** 或更新版本（以下語法使用 `var` 關鍵字以簡化，舊版 JDK 可自行移除）。  
- 提供 Java API 的 OCR 函式庫——本教學使用 **[Tesseract4J](https://github.com/nguyenq/tess4j)**，它是流行的 Tesseract 引擎的輕量包裝。  
- 一張包含清晰印刷文字的 JPEG 圖片（`.jpg`）。  
- 你慣用的 IDE（IntelliJ IDEA、Eclipse、VS Code…）皆可。

如果缺少函式庫，只要加入以下 Maven 依賴：

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

現在開始吧。

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## OCR Bounding Box：設定引擎

首先必須建立 OCR 引擎實例。把它想像成開啟之後會讀取像素的掃描器。

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**為什麼這很重要：**  
若未設定 `datapath`，Tesseract 不會知道語言資料所在位置，會拋出「Failed loading language」的神祕錯誤。`setLanguage` 只在需要非預設英文語系時才必須，但明確寫出可以讓程式碼對未來的閱讀者更清晰。

## 載入要處理的圖片

接著，把想要分析的 JPEG 傳給引擎。函式庫接受 `File` 或 `BufferedImage`，這裡為了簡潔使用 `File`。

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**小技巧：**  
如果圖片放在 resources（例如 JAR 內），請使用 `getResourceAsStream` 並以 `ImageIO.read` 包裝。如此一來，教學既能在本機執行，也能在打包後的應用程式中使用。

## 執行 OCR 辨識

現在正式請引擎讀取圖片。結果會是一段純文字字串，我們同時也想取得 **ocr confidence score** 與每行的 **ocr bounding box**。

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**為什麼使用 `getWords` 而不是直接的 `doOCR`：**  
`doOCR` 只回傳原始字串，會捨棄空間資訊。透過 `getWords` 搭配 `RIL_WORD`（若想要行層級的框則使用 `RIL_TEXTLINE`），即可取得 `Word` 物件清單，裡面包含文字、信心值與邊界矩形。這正是 **ocr bounding box** 功能的核心。

## 了解輸出結果

將上述程式碼對乾淨的 JPEG 執行後，會得到類似以下的輸出：

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – 辨識出的字元。  
- **Confidence** – 0 到 1 之間的浮點值，數值越高表示引擎越有把握。  
- **Box** – 包住該字的矩形座標 (x, y, width, height)，單位為像素。

現在你不只可以 **read text from image**，還能精確知道每段文字在畫布上的位置——非常適合做高亮、裁切，或輸入後續的 NLP 流程。

## 邊緣情況與常見陷阱

| 情境 | 需要留意的地方 | 解決方法 / 替代方案 |
|-----------|-------------------|-------------------|
| 圖片模糊或對比度低 | 信心分數會急速下降（常低於 0.6）。 | 使用 OpenCV 前處理：提升對比、套用二值化。 |
| JPEG 含有旋轉文字 | 边框可能倾斜或缺失。 | 設定 `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)`，讓 Tesseract 自動偵測方向。 |
| 大圖導致 OutOfMemoryError | 載入大型圖片時 Java 堆積會爆炸。 | 在 OCR 前先縮小圖片 (`ImageIO.read` → `BufferedImage.getScaledInstance`)。 |
| 需要行層級的框而非字層級 | `RIL_WORD` 只回傳每字的框。 | 改用 `ITesseract.PageIteratorLevel.RIL_TEXTLINE`。 |
| 非英文字符顯示為 � | 語言資料未正確載入。 | 下載對應的 `.traineddata` 檔案，並將 `setDatapath` 指向其資料夾。 |

提前處理這些問題，可為你省下大量除錯時間。

## 完整可執行範例（一步到位）

以下是一個可自行複製貼上到 `src/main/java` 資料夾，並以 `mvn exec:java` 執行的完整 Java 類別，整合了前述所有步驟。

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## 接下來該學什麼？

以下教學與本篇內容緊密相關，能在此基礎上延伸更多技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握其他 API 功能，或在自己的專案中探索替代實作方式。

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}