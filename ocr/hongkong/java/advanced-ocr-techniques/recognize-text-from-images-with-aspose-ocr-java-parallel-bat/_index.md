---
category: general
date: 2026-05-31
description: 使用 Aspose OCR Java 快速辨認圖片文字。了解如何從 PNG 檔案提取文字，並設定 OCR 語言以獲得最佳效果。
draft: false
keywords:
- recognize text from images
- extract text from png
- set OCR language
- Aspose OCR Java
- parallel OCR processing
language: zh-hant
og_description: 使用 Aspose OCR Java 高效識別圖像中的文字。本教程展示如何從 PNG 檔案提取文字，以及如何設定 OCR 語言以進行批次處理。
og_title: 從圖片中辨識文字 – Aspose OCR Java 平行批次
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  headline: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  type: TechArticle
- description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  name: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  steps:
  - name: How It Works
    text: '- **Thread Count** – The processor creates a thread pool of the size you
      specify. On a quad‑core laptop, `4` is a sweet spot; increase it for servers
      with more cores. - **Language Setting** – By calling `setLanguage(OcrLanguage.FRENCH)`,
      we tell the OCR engine to bias its dictionary toward French ch'
  - name: 1️⃣ Missing or Corrupt Images
    text: If an image path is invalid, `OcrBatchProcessor` throws an `IOException`.
      Wrap the call in a try‑catch block, log the problematic file, and continue with
      the rest of the batch.
  - name: 2️⃣ Mixed Languages in One Batch
    text: 'When you have documents in multiple languages, you can either:'
  - name: 3️⃣ Memory Constraints
    text: Processing very large images (e.g., >10 MB) can inflate heap usage. Pre‑scale
      the images or increase the JVM’s `-Xmx` flag if you encounter `OutOfMemoryError`.
  - name: 4️⃣ Customizing OCR Settings
    text: 'Beyond language, you can tweak recognition speed vs. accuracy:'
  - name: LicenseUtil.java
    text: '```java import com.aspose.ocr.*;'
  - name: ImageProvider.java
    text: '```java import java.util.*;'
  - name: ParallelBatchDemo.java
    text: '```java import com.aspose.ocr.*; import java.util.*;'
  type: HowTo
tags:
- Java
- OCR
- Aspose
- Image Processing
title: 使用 Aspose OCR 從圖像中辨識文字 – Java 平行批次指南
url: /zh-hant/java/advanced-ocr-techniques/recognize-text-from-images-with-aspose-ocr-java-parallel-bat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像辨識文字 – Aspose OCR Java 平行批次教學

有沒有想過如何 **從圖像辨識文字**，卻不會卡住使用者介面？也許你有一個資料夾裡堆滿了掃描檔、螢幕截圖，甚至是 PNG 與 JPEG 混合的檔案，且急需取得文字。好消息是，使用 Aspose OCR for Java，你可以啟動多執行緒批次，**從 png 提取文字**（以及其他格式），同時悠閒地喝咖啡。

在本教學中，我們將逐步示範一個完整、可直接執行的範例，說明如何 **設定 OCR 語言**、啟動四個平行工作執行緒，並輸出結果。完成後，你將擁有一個可直接放入任何 Java 專案的實用範本——沒有多餘的雜項，只有你需要的程式碼。

## 你將學會

- 如何套用 Aspose OCR 授權，以免受到評估版限制的困擾。  
- 在平行環境下 **從圖像辨識文字** 的完整步驟，提升多核心機器的吞吐量。  
- 為何以及如何 **設定 OCR 語言**（示範中使用法文）以提升辨識精度。  
- 一個實用的 **從 png 檔提取文字** 方法，同樣的邏輯亦適用於 JPG、TIFF、BMP 等格式。  

**先決條件** – 需要 Java 8 或更新版本、Maven 或 Gradle 來取得 Aspose OCR 套件，以及有效的 Aspose OCR 授權檔 (`Aspose.OCR.Java.lic`)。不需要特殊的 IDE 技巧；任何能編譯 Java 的編輯器皆可。

---

## 步驟 1：加入 Aspose OCR 相依性

首先，確保 Aspose OCR JAR 已加入 classpath。若使用 Maven，請加入以下內容：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle：

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **小技巧：** 留意 Aspose 的發行說明；他們常會加入語言套件或效能調整，能為批次執行節省數秒時間。

## 步驟 2：套用 Aspose OCR 授權

若未套用授權，函式庫會以示範模式執行，並在輸出結果中嵌入浮水印。請於應用程式啟動時載入授權檔（僅需載入一次）。

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    /** Loads the Aspose OCR license from the given path. */
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

呼叫 `LicenseUtil.applyLicense("Aspose.OCR.Java.lic")` 可確保之後的每一次 **從圖像辨識文字** 呼叫皆不受限制。

## 步驟 3：準備影像清單

你可以將任意檔案路徑集合提供給批次處理器。以下示範 **從 png 提取文字**，同時處理 JPEG 與 TIFF 檔案——只需將路徑換成自己的目錄即可。

```java
import java.util.*;

public class ImageProvider {
    /** Returns a list of absolute image paths to be processed. */
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",   // PNG – our primary example
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

> **為何使用 List？** `OcrBatchProcessor` 需要一個 `List<String>`，以便自動將工作分配至多個執行緒。

## 步驟 4：設定並執行平行批次處理器

現在進入教學的核心：建立 `OcrBatchProcessor`、指定要啟動的執行緒數量，並 **設定 OCR 語言** 為法文（如需可改為 `OcrLanguage.ENGLISH` 或其他支援的語言）。

```java
import com.aspose.ocr.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // 2️⃣ Gather image files
        List<String> imagePaths = ImageProvider.getImagePaths();

        // 3️⃣ Create and configure the batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // 4 parallel workers
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // 4️⃣ Run OCR on the entire batch – this is where we **recognize text from images**
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // 5️⃣ Output the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### 工作原理

- **執行緒數量** – 處理器會建立指定大小的執行緒池。在四核心筆記型電腦上，`4` 為理想值；若是多核心伺服器可適度提升。  
- **語言設定** – 透過呼叫 `setLanguage(OcrLanguage.FRENCH)`，我們告訴 OCR 引擎偏向法文字元的字典，這能大幅提升非英語文件的辨識準確度。  
- **批次辨識** – `recognize` 方法會在內部遍歷提供的清單，分配工作，並回傳保留原始順序的 `List<OcrResult>`。這是最直接的 **從圖像辨識文字** 方式，無需自行編寫執行緒管理程式碼。

## 步驟 5：驗證輸出

執行程式後，應會看到類似以下的輸出：

```
File: YOUR_DIRECTORY/doc1.png
Bonjour le monde! Ceci est un test d'OCR.
---
File: YOUR_DIRECTORY/doc2.jpg
Hello world! This is an OCR test.
---
File: YOUR_DIRECTORY/doc3.tif
¡Hola mundo! Prueba de OCR.
---
```

若法文檔案 (`doc1.png`) 含有法文文字，**設定 OCR 語言** 的步驟將協助正確捕捉帶重音的字元。對於 PNG 檔，此示範說明了在同一批次中同時處理其他格式的同時，**從 png 提取文字** 的乾淨方式。

---

## 處理常見例外情況

### 1️⃣ 缺少或損毀的影像

若影像路徑無效，`OcrBatchProcessor` 會拋出 `IOException`。請將呼叫包在 try‑catch 區塊中，記錄有問題的檔案，並繼續處理其餘批次。

```java
try {
    List<OcrResult> results = batchProcessor.recognize(imagePaths);
} catch (IOException ex) {
    System.err.println("Failed to process: " + ex.getMessage());
}
```

### 2️⃣ 單批次混合多語言

當文件包含多種語言時，你可以：

- 分別執行多個批次，每個批次使用各自的 `setLanguage`。  
- 或不設定語言 (`OcrLanguage.AUTO_DETECT`) 讓 Aspose 自行偵測，雖然可能會降低準確度。

### 3️⃣ 記憶體限制

處理非常大的影像（例如 >10 MB）會增加堆積記憶體使用量。若遇到 `OutOfMemoryError`，可先縮小影像尺寸或提升 JVM 的 `-Xmx` 參數。

```bash
java -Xmx2g -cp yourapp.jar ParallelBatchDemo
```

### 4️⃣ 自訂 OCR 設定

除了語言外，你還可以調整辨識速度與精確度的平衡：

```java
batchProcessor.setRecognitionMode(OcrRecognitionMode.ACCURATE); // default is BALANCED
```

選擇 `ACCURATE` 會較慢，但對於噪點較多的掃描件可得到更佳結果。

---

## 完整範例（全部檔案）

以下提供完整的來源檔案。將它們複製到 Maven 專案中，調整授權路徑與影像目錄，然後執行 `mvn exec:java -Dexec.mainClass=ParallelBatchDemo`。

### LicenseUtil.java
```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

### ImageProvider.java
```java
import java.util.*;

public class ImageProvider {
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

### ParallelBatchDemo.java
```java
import com.aspose.ocr.*;
import java.util.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // Apply license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // Gather images
        List<String> imagePaths = ImageProvider.getImagePaths();

        // Configure batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // Parallelism
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // Recognize text from images
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // Output results
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

執行後，你會在主控台看到每個檔案的提取文字——這正是建構可搜尋檔案庫、資料輸入自動化或無障礙工具時所需的功能。

---

## 結論

我們剛剛介紹了一套完整、可投入生產環境的模式，使用 Aspose OCR for Java **從圖像辨識文字**。透過設定批次處理器，你可以平行 **從 png 提取文字**（以及其他格式），且 **設定 OCR 語言** 的功能可確保多語言工作負載取得最高的辨識準確度。

接下來的步驟？可以嘗試將語言改為 `OcrLanguage.SPANISH`，或使用 `OcrRecognitionMode.ACCURATE` 來處理較困難的掃描件。你也可以將結果寫入資料庫、匯入搜尋索引，或傳送至翻譯 API。

遇到較複雜的情況——例如對 PDF 或雲端儲存的影像進行 OCR？這些都是今天所建構功能的自然延伸。深入探索、微調設定，讓 OCR 引擎負責繁重的工作。

祝開發順利，願你的文字提取又快又準！

## 接下來你可以學習什麼？

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}