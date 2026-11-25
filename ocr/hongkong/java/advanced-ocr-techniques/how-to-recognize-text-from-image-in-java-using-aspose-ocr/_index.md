---
category: general
date: 2026-09-29
description: 學習如何使用 Java 和 Aspose OCR 從圖像中辨識文字。本指南亦示範如何從 JPG 提取文字以及如何提升 OCR 準確度。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- extract text from jpg
- how to improve OCR accuracy
- Aspose OCR Java
- Java image processing
language: zh-hant
lastmod: 2026-09-29
og_description: 使用 Aspose OCR 在 Java 中辨識圖像文字。跟隨此逐步教學從 jpg 提取文字，並了解如何提升 OCR 準確度。
og_image_alt: Java code screenshot that recognizes text from image using Aspose OCR
og_title: 在 Java 中辨識圖像文字 – 完整 Aspose OCR 教學
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to recognize text from image with Java and Aspose OCR. This
    guide also shows how to extract text from jpg and how to improve OCR accuracy.
  headline: How to recognize text from image in Java using Aspose OCR
  type: TechArticle
- description: Learn how to recognize text from image with Java and Aspose OCR. This
    guide also shows how to extract text from jpg and how to improve OCR accuracy.
  name: How to recognize text from image in Java using Aspose OCR
  steps:
  - name: '**Pre‑process the image** – apply contrast stretching or binarization using
      OpenCV before handing it to Aspose OCR. Cleaner edges give higher confidence.'
    text: '**Pre‑process the image** – apply contrast stretching or binarization using
      OpenCV before handing it to Aspose OCR. Cleaner edges give higher confidence.'
  - name: '**Crop unnecessary margins** – the engine spends time analyzing blank space,
      which can lower the overall confidence score.'
    text: '**Crop unnecessary margins** – the engine spends time analyzing blank space,
      which can lower the overall confidence score.'
  - name: '**Choose the correct language pack** – loading only the languages you need
      speeds up recognition and reduces false positives.'
    text: '**Choose the correct language pack** – loading only the languages you need
      speeds up recognition and reduces false positives.'
  - name: '**Use the latest Aspose OCR version** – each release includes updated neural
      models that improve accuracy out‑of‑the‑box.'
    text: '**Use the latest Aspose OCR version** – each release includes updated neural
      models that improve accuracy out‑of‑the‑box.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: 如何在 Java 中使用 Aspose OCR 進行圖像文字辨識
url: /zh-hant/java/advanced-ocr-techniques/how-to-recognize-text-from-image-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose OCR 識別圖像文字

如果您需要在 Java 應用程式中 **從圖像識別文字**，本教學提供一個可直接執行的解決方案。您將會看到如何從 jpg 檔案擷取文字、啟用 GPU 加速，以及套用拼寫校正，以回應常見的問題 *如何提升 OCR 準確度*。

本指南涵蓋您所需的一切：Maven 設定、完整原始碼、每個設定選項的說明，以及處理低品質圖片的技巧。完成後，您將擁有一個能將識別結果輸出至主控台的可執行程式。

## 前置條件

在開始之前，請確保您已具備：

* 已安裝 Java 17（或更新版本）— Aspose OCR 支援 Java 8 以上，但較新的執行環境可提供更佳效能。  
* Maven 3.8+ 用於相依管理。  
* Aspose OCR for Java 授權（免費試用版可用於評估）。  
* 一張包含清晰可辨文字的 JPG 圖片（`sample.jpg`）。

若缺少上述任一項，請從 [oracle.com/java](https://www.oracle.com/java/technologies/downloads/) 下載 JDK，並依照 Apache 官方網站的說明安裝 Maven。

## 將 Aspose OCR 加入專案

建立 `pom.xml`（或在現有檔案中加入）並加入 Aspose OCR 相依：

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <dependencies>
    <dependency>
      <groupId>com.aspose</groupId>
      <artifactId>aspose-ocr</artifactId>
      <version>23.12</version> <!-- latest stable at time of writing -->
    </dependency>
  </dependencies>
</project>
```

執行 `mvn clean compile` 以下載函式庫。此相依會自動帶入 GPU 使用與拼寫校正所需的所有原生二進位檔。

## 步驟 1：設定 OCR 引擎以識別圖像文字

首先建立 `OcrEngine` 實例。此物件負責協調整個 OCR 流程。

```java
// Step 1: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

建立引擎時尚未載入任何圖像；它僅僅是準備內部資源。這樣的分離讓您可以在批次處理時重複使用同一個引擎。

## 步驟 2：啟用 GPU 加速以提升處理速度

若您的機器配備相容的 GPU，開啟它可將辨識時間縮短最多 70 %。這直接回應了 *如何提升 OCR 準確度* 中速度的部分，讓您在不犧牲效能的情況下使用更高解析度的圖像。

```java
// Step 2 (optional): Use GPU if available
engine.getConfiguration().setUseGpu(true);
```

> **專業提示：** 在無頭伺服器上執行時，請確認已安裝 CUDA 驅動程式；否則呼叫會自動回退至 CPU，且不會拋出錯誤。

## 步驟 3：開啟拼寫校正以提升 OCR 準確度

拼寫校正是一個輕量的語言模型，可修正常見的辨識錯誤（例如 “l0ve” → “love”）。啟用此功能是提升列印文字 *如何提升 OCR 準確度* 的最有效方法之一。

```java
// Step 3 (optional): Enable spell correction
engine.getConfiguration().setSpellCorrector(true);
```

若您處理的是手寫筆記，建議關閉此功能，因為模型是針對列印字體進行調校的。

## 步驟 4：載入要從 jpg 擷取文字的圖像

現在載入圖像檔案。`ImageStream.fromFile` 輔助方法接受 Aspose OCR 支援的任何格式，但此範例以 JPG 為例，因為它是最常見的網路格式。

```java
// Step 4: Load the image that contains the text to be recognized
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

**為什麼選擇 JPG？** JPEG 壓縮可能產生干擾 OCR 的雜訊。為了取得最佳準確度，請提供 DPI 至少為 300 的圖像，並避免過度壓縮。若您使用 PNG 或 TIFF，也可以直接傳給 `fromFile`；程式碼不需要變更。

## 步驟 5：執行 OCR 並取得識別文字

最後，呼叫 `recognize()` 並將結果印出。此方法會回傳一個 `OcrResult` 物件，內含原始文字、信心分數以及每個單字的邊界框。

```java
// Step 5: Run OCR and get the result
OcrResult result = engine.recognize();
System.out.println("=== Recognized text ===");
System.out.println(result.getText());
```

### 預期輸出

```
=== Recognized text ===
Welcome to Aspose OCR demo.
This text was extracted from a JPG image.
```

如果輸出出現亂碼，請重新檢查 **步驟 3**（拼寫校正）並確認圖像符合 DPI 建議。

## 常見變化與邊緣情況

| 情境 | 建議調整 |
|-----------|------------------------|
| **低解析度圖像 (< 150 DPI)** | 在送入引擎前先放大圖像，或使用 `engine.getConfiguration().setScaleFactor(2.0)` 讓引擎內部重新取樣。 |
| **多語言文件** | 設定 `engine.getConfiguration().setLanguage("eng,spa")` 以載入英文與西班牙文詞典。 |
| **大量檔案批次** | 重複使用同一個 `OcrEngine` 實例，僅對每個新檔案呼叫 `engine.setImage(...)`。可避免重複載入原生函式庫。 |
| **記憶體受限環境** | 關閉 GPU (`setUseGpu(false)`) 與拼寫校正 (`setSpellCorrector(false)`) 以降低 RAM 用量。 |
| **從 PNG 而非 JPG 擷取文字** | 無需更改程式碼，只要把 `fromFile` 指向 `.png` 路徑即可，函式庫會自動偵測格式。 |

## 提升 OCR 準確度的專業技巧

1. **前置處理圖像** – 使用 OpenCV 進行對比拉伸或二值化，再交給 Aspose OCR。較乾淨的邊緣可提升信心分數。  
2. **裁切不必要的邊框** – 引擎會分析空白區域，這會降低整體信心分數。  
3. **選擇正確的語言包** – 僅載入所需語言可加快辨識速度並減少誤判。  
4. **使用最新的 Aspose OCR 版本** – 每個新發行版皆包含更新的神經模型，能即時提升準確度。

## 完整、可執行的範例

以下為完整的 Java 類別，將所有步驟整合在一起。將檔案儲存為 `SimpleOcr.java`，調整圖像路徑後執行 `mvn exec:java -Dexec.mainClass=SimpleOcr`。

```java
import com.aspose.ocr.*;

public class SimpleOcr {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: (Optional) Enable GPU acceleration for faster processing
        engine.getConfiguration().setUseGpu(true);

        // Step 3: (Optional) Enable spell correction to improve OCR accuracy
        engine.getConfiguration().setSpellCorrector(true);

        // Step 4: Load the image that contains the text to be recognized
        // This example extracts text from jpg, but any supported format works.
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Step 5: Perform OCR and retrieve the recognized text
        OcrResult result = engine.recognize();

        System.out.println("=== Recognized text ===");
        System.out.println(result.getText());
    }
}
```

執行程式後，主控台會印出識別出的文字，證明您已成功學會 **從圖像識別文字**、**從 jpg 擷取文字**，以及 **如何提升 OCR 準確度** 的關鍵技巧。

## 結論

本教學說明了如何在 Java 中使用 Aspose OCR **從圖像識別文字**、**從 jpg 擷取文字**，以及多種實用方法來回應 *如何提升 OCR 準確度*。此方法完全自給自足：只需 Maven 相依、一本 JPEG 檔案與少數設定旗標。

接下來您可以探索：

* 使用 Aspose PDF 將識別文字轉換為可搜尋的 PDF。  
* 以簡單迴圈處理整個資料夾的圖像（批次 OCR）。  
* 將 OCR 引擎整合至 Spring Boot REST 端點，以提供即時圖像處理服務。

歡迎嘗試不同的圖像品質、語言包與硬體設定，觀察各因素對 OCR 效能的影響。祝開發順利！

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步深化您對 API 功能的掌握，並探索其他實作方式：

- [Preprocess Image OCR in Java with Aspose OCR – Boost Accuracy & Extract Text](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [How to Use OCR in Java – Recognize Text from Image Quickly](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Recognize Text from Image with Aspose OCR – Full Java Guide](/ocr/english/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}