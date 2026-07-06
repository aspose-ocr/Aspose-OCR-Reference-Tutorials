---
category: general
date: 2026-03-26
description: 使用 Aspose.OCR Java 建立可搜尋的 PDF – 學習載入影像 OCR、設定主要語言、從影像提取文字並儲存 OCR PDF。
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: zh-hant
og_description: 使用 Aspose.OCR Java 建立可搜尋的 PDF。逐步指南：載入影像進行 OCR、設定主要語言、從影像擷取文字，並儲存為
  OCR PDF。
og_title: 使用 Aspose.OCR 建立可搜尋 PDF – Java 指南
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: 使用 Aspose.OCR 建立可搜尋的 PDF – Java 指南
url: /zh-hant/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.OCR 建立可搜尋 PDF – Java 指南

是否曾需要從掃描文件 **create searchable pdf** 但不確定從何開始？您並不孤單——許多開發者在首次於 Java 中處理 OCR 時都會碰到這道牆。好消息是 Aspose.OCR 讓整個流程——從載入影像、設定主要語言到最終儲存具 OCR 功能的 PDF——相當輕鬆。在本教學中，我們將示範一個完整、可執行的範例，**extracts text from image**、讓您 **set primary language**，最後 **save OCR pdf**，可在任何閱讀器開啟。

我們還會涵蓋一些實用技巧，例如啟用 GPU 加速以提升處理速度，以及處理混合語言文件（本例為 Tamil + English）。完成後，您將擁有一段穩固、可直接投入專案的 production‑ready 程式碼片段。

## 您需要的環境

- **Java 17**（或任何較新的 JDK；Aspose.OCR 支援 Java 8+）
- **Aspose.OCR for Java** 函式庫（從官方網站下載或透過 Maven 加入）
- **license file**（或 30 天試用版）
- 包含文字的影像檔（示範使用 `sample-mixed-tamil-eng.jpg`）

不需要額外框架或原生相依性——僅需純 Java 與 Aspose.JAR 檔案。

---

## 步驟 1：建立可搜尋 PDF – 設定專案

在深入程式碼之前，先確保專案已準備好 **create searchable pdf** 檔案。

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Pro tip:** 保持版本號為最新；較新的版本通常包含針對 GPU 使用的效能修正。

現在建立一個名為 `RecentFeaturesDemo` 的簡易 Java 類別。此類別將容納我們需要的所有邏輯，以 **load image OCR**、設定語言參數，最後 **save OCR pdf**。

## 步驟 2：載入影像 OCR 並初始化引擎

管線中的第一個實際步驟是 **load image OCR**。這會告訴 Aspose.OCR 要分析哪個檔案。

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Why this matters:** 啟用 GPU (`setUseGpu(true)`) 可在現代硬體上將處理時間縮短最多 70 %，且平行處理可確保 GPU 忙碌時 CPU 不會閒置。

## 步驟 3：設定主要語言（以及次要語言）

如果跳過此步驟，Aspose.OCR 會嘗試自行猜測語言，速度較慢且準確度較低。以下說明如何 **set primary language** 為 Tamil，並將 English 加入為備援語言。

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Explanation:** 主要語言會影響辨識時使用的字元集與字典。加入次要語言對於混合文字文件（例如同時包含 Tamil 與 English 文字的收據）至關重要。  
> **Edge case:** 若文件包含超過兩種語言，可對每個額外語言呼叫 `addAdditionalLanguage(...)`。

## 步驟 4：前處理影像 – 去斜與去噪

掃描影像常會出現旋轉或背景噪點。前處理可協助 OCR 引擎更可靠地 **extract text from image**。

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Tip:** 若您確定影像已相當乾淨，可省略 `setDenoise(true)`，以節省數毫秒的時間。

## 步驟 5：載入影像檔案

引擎已就緒，現在指向我們想要分析的檔案。

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **What if the path is wrong?** Aspose.OCR 會拋出明確的 `FileNotFoundException`。若需優雅的錯誤處理，可將呼叫包在 try‑catch 中。

## 步驟 6：執行 OCR 並從影像擷取文字

在完成所有設定後，現在是實際執行辨識的時候。此步驟同時 **extracts text from image**，並準備建立 PDF 所需的資料。

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

示範影像的典型主控台輸出如下：

```
வணக்கம் World
This is a mixed language sample.
```

您會看到 Tamil 行正確呈現，接著是 English。這正是正確使用 **set primary language** 的成果。

## 步驟 7：儲存 OCR PDF – 最後一步

最後一步是 **save OCR pdf**。Aspose.OCR 能在原始影像上嵌入隱形文字層，使 PDF 具備搜尋功能。

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

在 Adobe Reader 開啟 `searchable.pdf`，按 **Ctrl + F**，即可搜尋 Tamil 與 English 兩種文字——正是 **create searchable pdf** 工作流程所承諾的功能。

## 完整可執行範例（複製貼上）

以下是可直接編譯執行的完整程式碼。請將佔位路徑替換為您自己的目錄。

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

使用以下指令執行：

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

您應會在主控台看到擷取的文字，接著顯示 **searchable pdf** 已寫入磁碟的確認訊息。

## 常見問題與邊緣情況

### 如果需要從位元組陣列 **load image OCR**？

您可以將 `ImageStream.fromFile(imagePath)` 改為 `ImageStream.fromBytes(byteArray)`。當影像來自資料庫或 Web 服務時，此方式相當方便。

### 如何處理已包含影像的 PDF？

Aspose.OCR 可直接對 PDF 頁面操作：`ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`。引擎會在辨識前先將每頁光柵化。

### 我的 GPU 未被偵測——還要保留 `setUseGpu(true)` 嗎？

若 `setUseGpu(true)` 失敗，Aspose.OCR 會自動回退至 CPU。您可在啟用前檢查 `ocrEngine.getEngineSettings().isGpuAvailable()`。

### 能否使用自訂中繼資料 **save OCR pdf**？

可以。辨識完成後，於呼叫 `save` 前使用 `ocrEngine.getPdfSaveOptions().setTitle("My Document")` 或 `setAuthor("John Doe")` 來設定自訂中繼資料。

## 大批量處理的效能技巧

- **Batch processing:** 在多張影像間重複使用同一個 `OcrEngine` 實例。每次執行後僅呼叫 `ocrEngine.clear()`。
- **Thread pool:** 將每個影像任務包裝成 `Callable`，提交給 `ExecutorService`。因為已啟用平行處理，每個執行緒都能受惠於多核心使用。
- **Memory management:** 對於千兆像素的影像，可使用 `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` 進行降採樣，以維持合理的記憶體使用。

## 結論

我們剛剛示範了使用 Aspose.OCR for Java 完整的 **create searchable pdf** 工作流程。從 **load image OCR** 開始，我們

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}