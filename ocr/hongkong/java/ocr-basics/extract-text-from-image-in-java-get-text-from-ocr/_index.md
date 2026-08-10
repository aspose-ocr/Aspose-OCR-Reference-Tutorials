---
category: general
date: 2026-05-25
description: 使用 OCR 在 Java 中從圖像提取文字。了解如何載入圖像以進行 OCR、從相片辨識文字，以及使用簡單程式範例取得 OCR 結果。
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: zh-hant
og_description: 在 Java 中逐步提取圖像文字。學習如何載入圖像進行 OCR、從相片辨識文字，並高效取得 OCR 結果。
og_title: 在 Java 中從圖像提取文字 – 從 OCR 獲取文字
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: 在 Java 中從圖像提取文字 – 從 OCR 取得文字
url: /zh-hant/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java 從影像提取文字 – 取得 OCR 文字

是否曾經需要 **從影像提取文字**，卻不確定該選哪個 Java 函式庫？你並不孤單。無論是數位化收據、從產品照片中抓取序號，或只是玩個有趣的副專案，將圖片轉換成可編輯文字都是常見的挑戰。

在本教學中，我們將逐步示範一個完整、可直接執行的範例，說明如何 **load image for OCR**、設定引擎，最後 **recognize text from photo**，讓你只需幾行程式碼即可 **get text from OCR**。不含模糊的參考——所有需要的內容都在此。

## 你將學到

* 如何在 Java 中設置輕量級的 OCR 引擎。  
* **load image for OCR** 的具體步驟以及如何處理不同的檔案路徑。  
* 為何在想要 **extract text from image** 且非英文時，設定語言非常重要。  
* 如何安全地輸出結果，以及當引擎未返回任何內容時的處理方式。  
* 幾個避免常見陷阱的專業技巧。

閱讀完本指南後，你將擁有一個獨立的程式，可讀取包含烏克蘭文字的 JPEG（或 PNG），並將辨識出的字串印到主控台。隨意更換語言或影像——所有功能皆模組化。

![使用 Java OCR 引擎從影像提取文字的流程圖](/images/extract-text-from-image-java.png)

*Alt text: 使用 Java OCR 引擎從影像提取文字的流程圖*

## 前置條件

* **Java Development Kit (JDK) 11+** – 程式碼使用現代模組系統，但舊版亦可在稍作調整後運作。  
* **Maven 或 Gradle** – 用於取得 OCR 函式庫（我們將使用 **Asprise OCR** 作為輕量、免費開發的選項）。  
* 一個範例影像檔（例如 `ukrainian_sign.jpg`），放置於程式可讀取的位置。  
* 具備 Java `main` 方法與例外處理的基本概念。

如果你已具備上述條件，即可開始。否則，請從 Oracle 或 AdoptOpenJDK 下載 JDK，並建立一個簡易的 Maven 專案——不需要太複雜。

## 步驟 1：加入 OCR 相依性

首先，告訴你的建置工具去取得 OCR 引擎。對於 Maven，將以下內容放入 `pom.xml`：

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

如果你偏好 Gradle，等價的設定如下：

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

這些坐標會下載一個緊湊的 JAR，內含 `OcrEngine`、`OcrLanguage` 以及我們將使用的輔助類別。對於基本的拉丁與西里爾字母腳本，無需額外的原生二進位檔案。

## 步驟 2：建立一個 Java 類別以 **Extract Text from Image**

現在我們來撰寫實際程式。將以下內容儲存為 `ExtractTextDemo.java`，放在 `src/main/java/com/example/ocr/` 目錄下。

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### 為何此結構可行

* **分段編號的區塊** 讓流程更易於追蹤，特別是當你在尋找 **load image for OCR** 或 **recognize text from photo** 的位置時。  
* 圍繞影像載入與辨識的 `try/catch` 可確保程式優雅失敗——當檔案路徑錯誤或 OCR 引擎找不到語言資料時特別有用。  
* 於步驟 2 早期設定語言，可大幅提升非英文腳本的準確度。若日後需要 **java image to text** 其他語言，只需將 `OcrLanguage.UKRAINIAN` 換成 `OcrLanguage.ENGLISH`、`FRENCH` 等。

## 步驟 3：建置並執行程式

在專案根目錄執行：

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

或是使用 Gradle 時：

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

假設 `ukrainian_sign.jpg` 包含文字 *«Ласкаво просимо»*（烏克蘭語「歡迎」），你應該會看到類似以下的輸出：

```
=== OCR Result ===
Ласкаво просимо
```

此輸出證明你已成功 **extract text from image** 並在一次執行中 **get text from OCR**。

## 步驟 4：微調工作流程 – 在實際專案中從 **Java Image to Text**

雖然示範程式相當簡潔，實務應用通常需要更多調整：

| 情境 | 調整項目 | 原因 |
|----------|----------------|--------|
| **批次處理** | 遍歷 `List<Path>`，將每個結果存入資料庫。 | 當有數百張照片時，可減少手動工作。 |
| **不同影像格式** | 使用 `ImageIO.read(new File(path))` 進行前置處理，然後將 `BufferedImage` 傳遞給 `ocrEngine.getImage().loadFromBufferedImage(bufImg)`。 | 支援 PNG、BMP，甚至在轉換後的 PDF。 |
| **效能調校** | 若可接受稍低的準確度，可呼叫 `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)`。 | 在低階硬體上加快辨識速度。 |
| **後處理** | 去除空白，替換常見的 OCR 錯讀（`0` → `O`、`1` → `I`）。 | 提升後續資料品質。 |

這些變化保留了核心概念——**recognize text from photo**——同時為生產環境提供彈性。

## 常見陷阱與專業提示

1. **語言設定錯誤** – 若忘記第 2 步，引擎會預設為英文，導致西里爾字元變成亂碼。務必再次確認語言代碼。  
2. **影像品質重要** – 低解析度或模糊的照片會降低準確度。必要時可先進行對比度增強或二值化前處理。  
3. **檔案路徑怪異** – 在 Windows 上，反斜線需跳脫 (`C:\\images\\file.jpg`)；使用 `java.nio.file` 的 `Path.of(...)` 可避免此問題。  
4. **記憶體洩漏** – `OcrEngine` 會佔用原生資源。使用完畢後呼叫 `ocrEngine.dispose()`，尤其在長時間服務中。  
5. **執行緒安全** – 引擎本身不是執行緒安全的。每個執行緒建立獨立實例或同步存取。

## 完整範例（全功能合一）

以下是一個可直接複製貼上至任何 IDE 的單一檔案。它包含 `dispose()` 呼叫以及一個小型輔助方法，使程式碼更整潔。

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

執行此程式會得到先前示範的相同主控台輸出。隨意將 `OcrLanguage.UKRAINIAN` 替換為 `OcrLanguage.ENGLISH` 或其他支援的語言，以觀察引擎的適應情況。

## 結論

我們已完整說明使用 Java **extract text from image** 所需的全部步驟：從加入 OCR 相依性，到 **load image for OCR**，

## 相關教學

- [使用 Aspose OCR 識別文字影像 – 完整 Java OCR 教學](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [如何使用 Aspose.OCR 以語言進行影像文字 OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [使用 Aspose.OCR BufferedImage 在 Java 中將影像轉換為文字](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}