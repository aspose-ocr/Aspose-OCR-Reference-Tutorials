---
category: general
date: 2026-08-18
description: 如何在 Java 中啟用 GPU 進行 OCR，快速辨識圖像文字、提取文字 JPG、加入過濾器，並使用 Aspose.OCR 設定語言。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize image text
- extract text jpg
- how to add filter
- how to set language
language: zh-hant
lastmod: 2026-08-18
og_description: 如何在 Java 中啟用 GPU 進行 OCR，並使用 Aspose.OCR 即時辨識影像文字、從 JPG 提取文字、加入濾鏡及設定語言。
og_image_alt: Screenshot showing Java code that enables GPU for OCR with Aspose.OCR
og_title: 如何在 Java 中啟用 GPU 進行 OCR – 完整的 Aspose.OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  headline: How to enable GPU for OCR in Java using Aspose.OCR
  type: TechArticle
- description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  name: How to enable GPU for OCR in Java using Aspose.OCR
  steps:
  - name: 3.1 Set the OCR language
    text: '```java // Choose the language for recognition – this is the “how to set
      language” step engine.setLanguage(OcrLanguage.ENGLISH); ```'
  - name: 3.2 Add a preprocessing filter
    text: 'Noise, compression artifacts, or uneven lighting can hurt accuracy. Adding
      a denoise filter is the typical **how to add filter** approach:'
  - name: Expected output
    text: '``` Recognized text: The quick brown fox jumps over the lazy dog. ```'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: 如何在 Java 中使用 Aspose.OCR 為 OCR 啟用 GPU
url: /zh-hant/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose.OCR 啟用 GPU 進行 OCR

如果您需要在 Java 中 **啟用 GPU** 進行 OCR，本指南將逐步說明具體操作。啟用 GPU 加速可讓您 **辨識影像文字** 的速度提升數倍，這在大量 **擷取 JPG 文字** 時尤為重要。我們還會說明 **如何加入濾鏡**、**如何設定語言**，以及如何取得最終結果。

完成本教學後，您將擁有一個完整且可執行的程式，能夠：

* 啟動具備 GPU 支援的 Aspose.OCR 引擎。  
* 設定 OCR 語言（例如 English）。  
* 套用去噪濾鏡以提升準確度。  
* 載入 JPEG 影像、執行辨識，並印出擷取的文字。

> **先決條件：** Java 17 或更新版本、Maven，以及 Aspose.OCR for Java 授權（免費試用版可用於評估）。

---

![如何在 Java 中啟用 GPU 進行 OCR](/images/ocr-gpu.png){alt="如何在 Java 中啟用 GPU 進行 OCR"}

## 您需要的項目

| 項目 | 原因 |
|------|--------|
| **Java Development Kit (JDK) 17+** | 必須編譯與執行範例程式。 |
| **Maven** | 簡化 Aspose.OCR 的相依管理。 |
| **Aspose.OCR for Java** | 提供 `OcrEngine` 類別與 GPU 支援。 |
| **範例 JPEG 影像** (`sample.jpg`) | 用於示範 **擷取 JPG 文字**。 |
| **相容 GPU 硬體**（可選，但建議） | 讓我們能設定效能提升。 |

---

## 步驟 1：設定 Maven 專案

建立新的 Maven 專案（或在現有專案中加入），並加入 Aspose.OCR 相依性：

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-gpu-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Aspose.OCR for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.12</version> <!-- Use the latest stable version -->
        </dependency>
    </dependencies>
</project>
```

> **專業提示：** 請保持版本號為最新；較新版會改善 GPU 處理並加入語言套件。

---

## 步驟 2：初始化 OCR 引擎並 **啟用 GPU**

解決方案的核心是 `OcrEngine`。建立它相當簡單，但必須明確開啟 GPU 加速：

```java
import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration (this is the “how to enable GPU” part)
        engine.setUseGpu(true); // <-- GPU is now active

        // Step 2.3: Configure language and preprocessing filter (covered later)
```

**為什麼要啟用 GPU？**  
呼叫 `setUseGpu(true)` 後，Aspose.OCR 會將大量影像處理核心轉交給顯示卡。於現代 NVIDIA/AMD GPU 上，辨識速度可從每頁約 200 ms 降至 < 80 ms，對大量批次處理而言可大幅縮短總時間。

---

## 步驟 3：**設定語言** 與 **加入濾鏡**

### 3.1 設定 OCR 語言

```java
        // Choose the language for recognition – this is the “how to set language” step
        engine.setLanguage(OcrLanguage.ENGLISH);
```

Aspose.OCR 內建超過 100 種語言套件。將 `ENGLISH` 替換為 `FRENCH`、`CHINESE_SIMPLIFIED` 等，即可符合您的來源文字。

### 3.2 加入前處理濾鏡

噪點、壓縮產生的雜訊或光線不均都會影響準確度。加入去噪濾鏡是典型的 **如何加入濾鏡** 作法：

```java
        // Add a denoising filter to improve OCR quality – “how to add filter”
        engine.addPreprocessFilter(FilterType.DENOISE);
```

其他實用濾鏡包括 `FilterType.CONTRAST`、`FilterType.BRIGHTNESS` 與 `FilterType.BINARIZE`。可透過多次呼叫 `addPreprocessFilter` 來串接多個濾鏡。

---

## 步驟 4：載入影像 – **擷取 JPG 文字**

現在把引擎指向我們要處理的 JPEG 檔案：

```java
        // Load the JPEG image – this demonstrates “extract text JPG”
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

將 `YOUR_DIRECTORY` 替換為 `sample.jpg` 所在的實際路徑。Aspose.OCR 亦支援 PNG、BMP、TIFF 與 PDF，使用相同呼叫即可處理這些格式。

---

## 步驟 5：執行 OCR 並 **辨識影像文字**

引擎設定完成後，呼叫辨識例程：

```java
        // Run the OCR operation – “recognize image text”
        engine.recognize();

        // Retrieve the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);
    }
}
```

`recognize()` 方法會在 GPU（若已啟用）上處理影像，並填入內部文字緩衝區。`getText()` 會回傳純文字 `String`，您可以寫入檔案、資料庫，或傳給下游的 NLP 流程。

### 預期輸出

```
Recognized text: The quick brown fox jumps over the lazy dog.
```

若影像包含多行文字，回傳的字串會保留換行符號（`\n`），以維持原始排版。

---

## 步驟 6：驗證 GPU 使用情況（可選）

若要確認確實使用了 GPU，請開啟 Aspose 記錄功能：

```java
        // Enable diagnostic logging (optional)
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
```

執行後檢查 `ocr-debug.log`；您應該會看到類似 `GPU device: NVIDIA GeForce RTX 3080` 與 `Processing time (GPU): 78 ms` 的條目。若日誌顯示 **CPU**，請再次確認驅動程式安裝與 `setUseGpu(true)` 呼叫是否正確。

---

## 常見問題與避免方式

| 症狀 | 可能原因 | 解決方法 |
|---------|--------------|-----|
| **`java.lang.UnsatisfiedLinkError: no aspose_ocr_native`** | 缺少原生 GPU 函式庫 | 安裝最新的 GPU 驅動，並確保 `aspose-ocr` 原生二進位檔位於 `java.library.path` 中。 |
| **暗圖像辨識率低** | 未使用前處理濾鏡 | 加入 `engine.addPreprocessFilter(FilterType.BRIGHTNESS)` 或提升 `FilterType.CONTRAST`。 |
| **大量批次出現 `OutOfMemoryError`** | GPU 記憶體耗盡 | 將影像分批處理，或在高解析度下關閉 GPU（`engine.setUseGpu(false)`）。 |
| **語言輸出不正確** | 設定錯誤的語言 | 確認 `engine.setLanguage(OcrLanguage.YOUR_LANGUAGE)` 與來源文字相符。 |

---

## 完整、可執行的範例

以下是可直接貼到 `src/main/java/com/example/HelloWorldOcr.java` 的完整 Java 類別，包含所有步驟、錯誤處理與可選記錄。

```java
package com.example;

import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // -------------------------------------------------
        // 1️⃣ Enable GPU acceleration – how to enable GPU
        // -------------------------------------------------
        engine.setUseGpu(true);

        // -------------------------------------------------
        // 2️⃣ Set language – how to set language
        // -------------------------------------------------
        engine.setLanguage(OcrLanguage.ENGLISH); // Change if needed

        // -------------------------------------------------
        // 3️⃣ Add preprocessing filter – how to add filter
        // -------------------------------------------------
        engine.addPreprocessFilter(FilterType.DENOISE);
        // Optional: engine.addPreprocessFilter(FilterType.CONTRAST);

        // -------------------------------------------------
        // 4️⃣ Load the JPEG image – extract text JPG
        // -------------------------------------------------
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        engine.setImage(ImageStream.fromFile(imagePath));

        // -------------------------------------------------
        // 5️⃣ Perform OCR – recognize image text
        // -------------------------------------------------
        engine.recognize();

        // Retrieve and display the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);

        // -------------------------------------------------
        // 6️⃣ Optional: write output to a file
        // -------------------------------------------------
        java.nio.file.Files.writeString(
                java.nio.file.Paths.get("output.txt"),
                text,
                java.nio.charset.StandardCharsets.UTF_8
        );

        // -------------------------------------------------
        // 7️⃣ Optional: enable debug logging to verify GPU usage
        // -------------------------------------------------
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
    }
}
```

**執行程式**

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HelloWorldOcr
```

您應該會在主控台看到辨識後的文字，且 `output.txt` 內會保存相同內容。`ocr-debug.log` 檔案則會證實 GPU 已被使用。

---

## 結論

本教學示範了 **如何在 Java 中啟用 GPU** 以使用 Aspose.OCR，並說明了 **辨識影像文字**、**擷取 JPG 文字**、**如何加入濾鏡**、**如何設定語言**——全部集中於一個自包含的程式。啟用 GPU 可獲得顯著的速度提升，而濾鏡與語言設定則確保在各種影像來源下保持高準確度。

**後續步驟**

* 嘗試使用 `FilterType.BINARIZE` 等額外濾鏡，以提升掃描文件的辨識率。  
* 切換至其他語言（`OcrLanguage.SPANISH`、`OcrLanguage.CHINESE_SIMPLIFIED`）以擴充多語言支援。  
* 結合 Apache PDFBox，直接從 PDF 頁面抽取文字。

歡迎將此程式碼改寫為批次處理、整合至 Spring Boot 服務，或連接訊息佇列以實作即時 OCR 工作負載。祝開發順利！

## 您接下來可以學習什麼？

以下教學與本指南緊密相關，能進一步深化您對 API 功能的掌握，並探索在專案中使用的其他實作方式。

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Preprocess Image OCR in Java with Aspose OCR – Boost Accuracy & Extract Text](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}