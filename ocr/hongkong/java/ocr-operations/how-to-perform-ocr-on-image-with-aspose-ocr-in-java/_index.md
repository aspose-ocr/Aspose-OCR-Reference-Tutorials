---
category: general
date: 2026-09-10
description: 使用 Aspose OCR Java 執行圖像 OCR。學習如何從 JPEG 識別文字、從圖像提取文字，並高效將圖像轉換為文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- recognize text from JPEG
- extract text from image
- convert image to text
- load image for OCR
language: zh-hant
lastmod: 2026-09-10
og_description: 使用 Aspose OCR Java 執行影像 OCR。本教學示範如何從 JPEG 辨識文字、從影像擷取文字，並以幾行程式碼將影像轉換為文字。
og_image_alt: Screenshot of Java code that performs OCR on an image using Aspose OCR
og_title: 使用 Aspose OCR 於圖像執行 OCR – Java 指南
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  headline: How to perform OCR on image with Aspose OCR in Java
  type: TechArticle
- description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  name: How to perform OCR on image with Aspose OCR in Java
  steps:
  - name: Prerequisites
    text: '* Java Development Kit (JDK) 8 or later. * Maven or Gradle to manage dependencies
      (the example uses Maven). * A valid Aspose OCR for Java license (or a temporary
      evaluation key). * An image file named `sample.jpg` placed in a known directory.'
  - name: Load image for OCR
    text: '```java // Step 1: Load the image you want to process String imagePath
      = "YOUR_DIRECTORY/sample.jpg"; ImageStream imageStream = ImageStream.fromFile(imagePath);
      ```'
  - name: Create and configure the OCR engine
    text: '```java // Step 2: Create an OCR engine instance OcrEngine engine = new
      OcrEngine();'
  - name: Recognize text from JPEG
    text: '```java // Step 3: Attach the image to the engine engine.setImage(imageStream);'
  - name: Extract text from image and output
    text: '```java // Step 5: Output the recognized text System.out.println("=== Recognized
      Text ==="); System.out.println(result.getText()); ```'
  - name: Expected output
    text: 'Assuming `sample.jpg` contains the text “Hello World”, the console will
      display:'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: 如何在 Java 中使用 Aspose OCR 進行圖像文字辨識
url: /zh-hant/java/ocr-operations/how-to-perform-ocr-on-image-with-aspose-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose OCR 執行影像 OCR

如果您需要在 Java 應用程式中 **執行影像 OCR**，本指南提供完整、可直接執行的解決方案。您將會看到如何 **從 JPEG 檔案辨識文字**、**從影像資料擷取文字**，以及使用 Aspose OCR 的現代 API **將影像轉換為文字**。

本教學逐步說明所有必要步驟——從載入影像到印出辨識出的文字——讓您能在不搜尋其他資源的情況下整合 OCR 功能。除了 Aspose OCR for Java 函式庫外，無需任何外部工具。

## 您將完成的工作

* **載入影像以進行 OCR**，直接從檔案系統讀取。  
* 啟用 Aspose OCR 的前處理（例如去噪）以提升準確度。  
* **從 JPEG** 以及其他點陣格式**辨識文字**。  
* **從影像擷取文字** 並輸出至主控台。  
* 了解如何在可投入生產的程式碼範例中 **將影像轉換為文字**。

### 前置條件

* Java Development Kit (JDK) 8 或更新版本。  
* 使用 Maven 或 Gradle 管理相依性（範例使用 Maven）。  
* 有效的 Aspose OCR for Java 授權（或暫時的評估金鑰）。  
* 一個名為 `sample.jpg` 的影像檔案，放置於已知目錄中。

> **專業提示：** 使用高解析度 JPEG（300 dpi 或更高）以獲得最佳辨識率。

## 步驟 1：將 Aspose OCR 加入您的專案

如果您使用 Maven 管理相依性，請將以下程式碼片段插入您的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version>
</dependency>
```

若使用 Gradle，請加入：

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

這些座標會取得最新的穩定版 Aspose OCR 函式庫，內含稍後會使用的前處理功能。

## 執行影像 OCR – 逐步說明

以下各節將完整程式分解說明。每個區塊皆為獨立可直接複製、貼上並執行的程式碼。

### 載入影像以進行 OCR

```java
// Step 1: Load the image you want to process
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ImageStream imageStream = ImageStream.fromFile(imagePath);
```

*為何重要：*  
`ImageStream.fromFile` 讀取 JPEG 的原始位元組，並為 OCR 引擎做好準備。此方法支援 Aspose OCR 所支援的任何點陣格式，因此您可以在不修改程式碼的情況下將 JPEG 替換為 PNG 或 BMP。

### 建立並設定 OCR 引擎

```java
// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();

// Enable preprocessing to improve accuracy (e.g., denoising)
engine.getPreprocessing().setDenoise(true);
```

*為何重要：*  
實例化 `OcrEngine` 會分配核心辨識引擎。啟用 **denoise** 旗標可移除常干擾字元偵測的視覺噪點，尤其是在掃描的 JPEG 中。

### 從 JPEG 辨識文字

```java
// Step 3: Attach the image to the engine
engine.setImage(imageStream);

// Step 4: Perform OCR recognition
OcrResult result = engine.recognize();
```

*為何重要：*  
`engine.setImage` 將影像資料綁定至 OCR 流程。`engine.recognize()` 執行完整的辨識程序，回傳包含擷取文字與信心指標的 `OcrResult`。

### 從影像擷取文字並輸出

```java
// Step 5: Output the recognized text
System.out.println("=== Recognized Text ===");
System.out.println(result.getText());
```

*為何重要：*  
`result.getText()` 提供影像內容的純文字表示。將其印至主控台即可證明 **將影像轉換為文字** 已成功，且您可以將此字串重新導向至檔案、資料庫或下游服務。

## 完整、可執行的範例

以下為結合所有步驟的完整 Java 類別。請將 `YOUR_DIRECTORY` 替換為 JPEG 檔案的絕對路徑。

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the image for OCR
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ImageStream imageStream = ImageStream.fromFile(imagePath);

        // Create and configure the OCR engine
        OcrEngine engine = new OcrEngine();
        engine.getPreprocessing().setDenoise(true); // improve accuracy

        // Attach the image and run recognition
        engine.setImage(imageStream);
        OcrResult result = engine.recognize();

        // Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### 預期輸出

假設 `sample.jpg` 包含文字 “Hello World”，主控台將顯示：

```
=== Recognized Text ===
Hello World
```

若影像包含多行文字，則每行會在輸出中各自換行顯示。

## 常見變化與邊緣案例

| 情境 | 建議調整 |
|---|---|
| **低解析度 JPEG** (≤150 dpi) | 增加 `engine.getPreprocessing().setUpsample(true);` 讓 Aspose 在辨識前進行升解析度。 |
| **彩色背景**（例如掃描表單） | 啟用 `engine.getPreprocessing().setBinarize(true);` 將影像轉為黑白。 |
| **非拉丁文字**（例如西里爾文） | 設定語言：`engine.getLanguage().setLanguage(OcrLanguage.RUSSIAN);`。 |
| **大量批次處理** | 在多張影像間重複使用同一個 `OcrEngine` 實例，以減少啟動開銷。 |
| **需要信心分數** | 透過 `result.getConfidence()` 取得每個字元的信心值。 |

這些調整說明了您如何在不同情況下 **載入影像以進行 OCR**，同時仍能可靠地 **執行影像 OCR**。

## 效能考量

* **記憶體使用量：** 每個 `ImageStream` 會將整張影像載入記憶體。對於非常大的檔案（例如 >10 MB），可考慮使用 `ImageStream.fromByteArray` 以分塊串流方式讀取影像。  
* **執行緒安全性：** `OcrEngine` 並非執行緒安全。若計畫平行化 OCR 任務，請為每個執行緒建立獨立的實例。  
* **授權模式：** 評估模式會限制每個工作階段可處理的頁數。於生產環境部署授權版以解除此限制。

## 結論

現在您已了解如何在 Java 中使用 Aspose OCR **執行影像 OCR**。本教學涵蓋了載入影像、啟用前處理、從 JPEG 辨識文字、擷取文字，以及將影像轉換為文字——全部於一個簡潔的程式中完成。  

接下來您可以探索相關主題，例如批次 **從 JPEG 辨識文字**、將輸出整合至搜尋索引，或結合 OCR 與自然語言處理，以打造更智慧的文件流程。請嘗試不同的前處理選項，以取得對您特定影像來源的最佳準確度。

--- 

*程式輸出示意圖*  
![perform OCR on image Java example](image-placeholder.png){alt="使用 Aspose OCR Java 執行影像 OCR"}

## 接下來您可以學習什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上進一步說明。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [使用 Aspose OCR 辨識影像文字 – 完整 Java OCR 教學](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [如何使用 Aspose.OCR 以語言辨識影像文字](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [在 Java 中使用 Aspose OCR 前處理影像 OCR – 提升準確度與擷取文字](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}