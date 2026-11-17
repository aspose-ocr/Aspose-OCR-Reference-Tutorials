---
category: general
date: 2026-11-17
description: 學習如何在 Java 中對圖像執行 OCR，並使用簡單的程式碼範例從圖片中提取文字。包括讀取圖像的 Java 小技巧。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: zh-hant
lastmod: 2026-11-17
og_description: 如何在 Java 中對圖片執行 OCR 並快速提取文字。跟隨本指南，即可讀取圖片、將圖片轉換為文字，並提供可直接執行的範例。
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: 如何在 Java 中對圖像執行 OCR – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: 在 Java 中對圖像執行 OCR 的逐步指南
url: /zh-hant/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中執行 OCR（光學字符辨識）– 步驟指南

如果你需要 **如何執行 OCR** 在圖片上，本教學將向你展示一個完整且可執行的 Java 解決方案。你將會看到如何讀取影像檔案、設定 OCR 引擎，以及擷取引擎辨識出的文字。

處理掃描文件、收據或螢幕截圖時，通常需要將視覺內容轉換為可搜尋的文字。本指南會一步步帶領你，從載入影像到列印擷取的文字，並且說明常見的陷阱，例如不支援的檔案格式與空結果。

## 前置條件

* 已安裝 Java Development Kit (JDK) 8 或更新版本。
* 具備建置工具（Maven 或 Gradle）以取得 OCR 函式庫。
* 一個你想處理的影像檔案（JPEG、PNG、BMP）。

此程式碼使用 **OCR library from the `com.asprise.ocr` package**，因為它只需單一 JAR 且可在所有主要平台上運作。若要改用其他供應商（如 Tesseract、Google Vision 等），只需交換 import 陳述式與引擎初始化程式碼。

## 步驟 1：加入 OCR 相依性

若使用 Maven，請將以下相依性加入你的 `pom.xml`：

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

若使用 Gradle，請在 `build.gradle` 中加入此行：

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

這些行可確保 **read image Java** 程式碼能編譯，且 OCR 引擎在執行時可用。

## 步驟 2：使用 Java 讀取影像

讀取影像檔案是任何 **extract text image** 工作流程中的第一個具體步驟。Java 內建的 `ImageIO` 類別可處理大多數常見格式。

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**為何重要：** `ImageIO.read` 會在不支援的格式或檔案損壞時回傳 `null`。上述方法會記錄問題並回傳 `null`，讓後續步驟能優雅地處理。

## 步驟 3：建立並設定 OCR 引擎

OCR 引擎必須知道要辨識哪種語言。設定語言可大幅提升準確度，尤其是非英文文件。

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**為何重要：** 啟動引擎是一項相對耗時的操作，因此若你的應用程式批次處理影像，應該只建立一次並重複使用。

## 步驟 4：執行 OCR 並將影像轉換為文字

現在影像已載入且引擎已就緒，你可以執行辨識步驟。這就是 **how to perform OCR** 的核心。

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**邊緣案例處理：** 若影像為 `null`，此方法會回傳空字串而非拋出 `NullPointerException`。這使得處理使用者提供的檔案時，周圍程式碼更具韌性。

## 步驟 5：顯示擷取的文字

最後，將結果印出至主控台，或傳遞給其他元件（例如資料庫或 UI 小工具）。

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

當你使用 `java OcrDemo sample.jpg` 執行程式時，主控台會顯示辨識出的字元。這完成了 **convert image to text** 的循環。

### 預期輸出

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

若影像中沒有可辨識的字元，程式會印出 `(no text detected)`。

## 常見變化與調整方式

| Variation | What changes | When to use |
|-----------|--------------|-------------|
| **不同語言** | 將 `"eng"` 替換為 `"spa"`（西班牙語）、`"fra"`（法語）等。 | 文件使用非英文語言時 |
| **批次處理** | 對檔案路徑清單進行迴圈，重複使用相同的 `Ocr` 實例。 | 大量掃描頁面時 |
| **更高準確度** | 使用 `Ocr.SPEED_SLOW` 或啟用 `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` 以僅辨識數字。 | 當 OCR 品質至關重要時（例如發票號碼） |
| **Tesseract 替代方案** | 將 import 換成 `net.sourceforge.tess4j.Tesseract`，並調整初始化程式碼。 | 已依賴 Tesseract 的專案 |

## 專業技巧

* **在送入引擎前先調整大型影像尺寸**；OCR 速度會隨像素數量而變化。
* **預處理** 影像（灰階、對比度提升），若來源噪點較多，可使用 OpenCV 等函式庫。
* **快取 OCR 引擎**，若在短時間內多次呼叫——啟動與關閉引擎會產生額外開銷。
* **使用正規表達式驗證結果**，當你預期特定格式（例如日期、電話號碼）時。

## 結論

現在你已了解如何在 Java 中 **how to perform OCR** 於影像，從讀取檔案到顯示擷取的文字。本教學涵蓋了 **read image Java**、**extract text image**、**convert image to text** 與 **image to text java** 技術，並提供了實務情境的實用技巧。

接下來你可以：

* 將 OCR 步驟整合至接收上傳的 Web 服務。
* 將輸出與搜尋索引結合，對掃描文件進行全文搜尋。
* 探索進階 OCR 選項，如多語言支援或自訂字元集。

祝開發順利，盡情將圖片轉換為可搜尋的文字！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [如何在 Java 中使用 OCR – 以拼寫校正提取影像文字](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [使用 Aspose OCR 在 Java 中將影像轉換為文字 – 完整指南](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [如何在 Java 中啟用 GPU 進行 OCR – 提取影像文字](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}