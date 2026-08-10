---
category: general
date: 2026-06-16
description: 學習如何在 Java 中對圖像檔案執行 OCR。本教學涵蓋從 PNG 識別文字、從圖像提取文字、將圖像轉換為文字，以及載入圖像進行 OCR。
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: zh-hant
og_description: 使用 Java 對圖像執行 OCR。本指南示範如何從 PNG 識別文字、從圖像提取文字，以及透過可直接執行的範例將圖像轉換為文字。
og_title: 在 Java 中對圖像進行 OCR – 完整程式教學
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: 在 Java 中對圖像進行 OCR – 完整逐步指南
url: /zh-hant/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中對圖像執行 OCR – 完整逐步指南

曾經需要對圖像檔案 **perform OCR on image** 但不確定該選哪個 Java 函式庫嗎？你並不孤單。無論你是要打造收據掃描器、文件歸檔系統，或只是對將圖片轉換成可搜尋文字感到好奇，學習如何在 Java 中 **perform OCR on image** 是一項實用技能。

在本教學中，我們將逐步說明執行 **perform OCR on image** 所需的全部流程：載入圖像、設定引擎、辨識文字，最後印出結果。完成後，你將能夠 **recognize text from PNG** 檔案、**extract text from image** 來源，並以幾行程式碼 **convert image to text**。

## 先決條件

- Java 17 或更新版本（程式碼可在任何較新的 JDK 上編譯）
- 已安裝 Maven（或你喜歡的建置工具）
- 具備基本的 Java 語法知識
- 一個想要測試的 PNG 檔案（我們稱之為 `hello.png`）

> **專業提示：** 如果沒有 PNG 檔案，可透過截取任意文字的螢幕截圖，並將其儲存為 `hello.png`，放在名為 `resources` 的資料夾中。

## 我們將建立的內容

一個名為 `OcrDemo` 的小型主控台應用程式，具備以下功能：

1. **Loads image for OCR** – 從磁碟讀取 PNG。
2. **Performs OCR on image** – 使用 Tess4J 透過 Tesseract 引擎。
3. **Extracts text from image** – 回傳包含辨識內容的 `String`。
4. 將結果印出至主控台。

讓我們開始吧。

## 步驟 1：設定專案並加入 Tess4J

首先，建立一個新的 Maven 專案（若偏好 Gradle 亦可）。加入 Tess4J 相依套件，它封裝了廣受歡迎的 Tesseract OCR 引擎。

```xml
<!-- pom.xml -->
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
  </properties>

  <dependencies>
    <!-- Tess4J – Java wrapper for Tesseract OCR -->
    <dependency>
      <groupId>net.sourceforge.tess4j</groupId>
      <artifactId>tess4j</artifactId>
      <version>5.5.1</version>
    </dependency>
  </dependencies>
</project>
```

> **為什麼選擇 Tess4J？** 它持續維護、跨平台運作，並提供乾淨的 Java API 以執行 **perform OCR on image** 任務。

## 步驟 2：準備圖像載入邏輯

現在我們要撰寫一個協助方法，**load image for OCR**。此方法使用 Java 的 `ImageIO` 讀取 PNG 成 `BufferedImage`。

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

請注意，方法名稱清楚表達 **load image for OCR** 的意圖，使程式碼具備自說明性。

## 步驟 3：設定 OCR 引擎以 **Perform OCR on Image**

手上有圖像後，我們建立 `Tesseract` 實例，啟用自動語言偵測，並呼叫 `doOCR`。這就是我們 **perform OCR on image** 資料的核心流程。

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **為什麼啟用自動偵測？** 它讓引擎為圖像挑選最佳語言模型，特別適用於你 **convert image to text** 時來源混合英文與其他文字的情況。

## 步驟 4：整合所有程式 – 主應用程式

以下是入口點，能 **recognize text from PNG**、**extract text from image**，最後印出結果。這是一個完整且可執行的範例。

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### 預期輸出

如果 `hello.png` 包含文字 “Hello, OCR world!” ，主控台會顯示類似以下內容：

```
=== Recognized Text ===
Hello, OCR world!
```

實際輸出可能因圖像品質略有差異，但你應該能看到 PNG 中的文字。

## 步驟 5：處理常見邊緣情況

### 5.1 處理低解析度圖像

若來源 PNG 模糊，OCR 準確度會下降。快速解決方式是於送入引擎前先放大圖像：

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

在 `engine.recognize(image)` 前呼叫 `upscale(image, 2)` 以提升結果。

### 5.2 多語言文件

若預期會出現法文或德文，只需將語言代碼加入 `setLanguage`：

```java
tesseract.setLanguage("eng+fra+deu");
```

引擎將使用結合的語言模型嘗試 **extract text from image**。

### 5.3 跳過空白頁面

有時掃描的 PDF 頁面會呈現為空白 PNG。偵測空白圖像可節省處理時間：

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## 步驟 6：封裝與執行應用程式

1. **編譯：** `mvn clean compile`
2. **執行：** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

確保 `tessdata` 資料夾（內含語言檔案）與編譯後的 JAR 位於同一目錄，或在 `OcrEngine` 中指定其絕對路徑。

## 結論

你現在已掌握使用 Java **perform OCR on image** 檔案的完整、可投入生產的模式。從 **loading image for OCR** 到 **recognize text from PNG**，我們說明了如何 **extract text from image**、**convert image to text**，並處理低解析度掃描或多語言內容等挑戰。

接下來，你可以探索：

- **批次處理** – 迭代目錄中的 PNG，將每個結果寫入 `.txt` 檔案。
- **PDF 產生** – 將提取的文字嵌入可搜尋的 PDF。
- **雲端 OCR 服務** – 將本地 Tesseract 效能與 Google Vision、Azure Cognitive Services 等 API 進行比較。

歡迎自行實驗、調整參數，並分享你的發現。祝開發順利，願你的圖像永遠能轉換成乾淨、可搜尋的文字！

![顯示執行 OCR 工作流程的圖示](https://example.com/ocr-workflow.png "執行 OCR 圖像範例")

## 接下來你可以學什麼？

以下教學涵蓋與本指南技術密切相關的主題，並提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，或在自己的專案中探索替代實作方式。

- [使用 Aspose OCR 識別圖像文字 – 完整 Java OCR 教程](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [使用 Aspose.OCR BufferedImage 在 Java 中將圖像轉換為文字](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [使用 Aspose.OCR Detect Areas 模式在 Java 中提取圖像文字](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}