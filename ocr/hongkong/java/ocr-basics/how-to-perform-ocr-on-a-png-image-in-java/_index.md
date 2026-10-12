---
category: general
date: 2026-10-11
description: 學習如何在 Java 中對 PNG 圖片執行 OCR，從圖片提取文字，並使用簡單的 OcrEngine 範例將圖片轉換為文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: zh-hant
lastmod: 2026-10-11
og_description: 如何在 Java 中對 PNG 圖像執行 OCR，從圖像提取文字，並使用簡潔、可直接執行的範例將圖像轉換為文字。
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: 如何在 Java 中對 PNG 圖片執行 OCR – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: 如何在 Java 中對 PNG 圖片執行光學字符辨識
url: /zh-hant/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中對 PNG 圖像執行 OCR

如果您需要對圖像檔案**執行 OCR**，學習在 Java 中**如何執行 OCR**對許多自動化任務至關重要。無論是數位化收據、索引掃描文件，或是建立可搜尋的相片檔案庫，**從圖像中提取文字**的能力都能節省無數人工時間。

本教學示範一個完整且可執行的解決方案，載入 PNG、執行 OCR 引擎，並**從 PNG 檔案辨識文字**。您還會看到如何**將圖像轉換為文字**，以及處理常見的問題，例如低解析度輸入或非 ASCII 字元。

## 您將達成的目標

* **load image java** 程式碼，可從磁碟讀取 PNG，
* 初始化輕量級 OCR 引擎，
* **extract text from image** 並將結果印到主控台，
* 將此解決方案調整為其他圖像格式或批次處理。

不需要外部服務——只需一個開源 OCR 函式庫 (Tess4J) 與 Java SE 執行環境。

---

## 前置條件

* Java 17 或更新版本（程式碼以 JDK 17 編譯）。
* Maven 或 Gradle 用於相依性管理。
* 具備基本的命令列與您選擇的 IDE 使用經驗。
* `tess4j` 函式庫（Tesseract 的 Java 包裝器）。加入以下 Maven 相依性：

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

如果您使用 Gradle，等效設定如下：

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

您還需要 Tesseract 資料檔（`.traineddata`）。從官方儲存庫下載英文資料包，並將其放置於專案根目錄下名為 `tessdata` 的資料夾中。

---

## 步驟 1：在 Java 中載入圖像

使用標準的 `ImageIO` 類別載入 PNG 十分簡單。以下程式碼示範了安全且具例外處理的 **load image java**：

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**為什麼這很重要：** `ImageIO.read` 會自動偵測圖像格式，但我們會明確檢查 `null`，以避免 PNG 損壞時的靜默失敗。當您為 OCR **load image java** 時，此模式是最佳實踐。

---

## 步驟 2：初始化 OCR 引擎

Tess4J 包裝了原生的 Tesseract 二進位檔，提供簡易的 Java API。以下方法會建立 `Tesseract` 實例，指向 `tessdata` 資料夾，並將語言設定為英文：

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**為什麼要這樣做：** 只初始化一次引擎並在多張圖像間重複使用，可減少啟動開銷。`setOcrEngineMode` 呼叫會選擇預設模式，對大多數 PNG 表現良好。若遇到雜訊較多的掃描，可嘗試其他模式（例如 `OEM_LSTM_ONLY`）。

---

## 步驟 3：執行 OCR 並**從 PNG 辨識文字**

現在我們將圖像載入器與 OCR 引擎結合。以下方法會對 `BufferedImage` 執行 OCR，並回傳提取的字串：

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**完整可執行範例**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**預期輸出**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

主控台會顯示引擎從 `sample.png` 提取的精確字元。若 PNG 只包含單一單詞，輸出將是該單詞並換行。

---

## 步驟 4：常見變體與邊緣案例

### 4.1 處理低解析度 PNG

Tesseract 在至少 300 DPI 的圖像上表現最佳。若來源 PNG 較小，請在 OCR 前將其放大：

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

在呼叫 `extractText` 前使用 `upscale(image, 2)` 以提升準確度。

### 4.2 提取非英文文字

若要**extract text from image** 包含其他語言的內容，請下載相應的 `.traineddata` 檔案，並設定語言代碼：

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 批次處理多個 PNG

如果您需要在資料夾中**recognize text from PNG** 檔案，請遍歷目錄：

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 處理 OCR 錯誤

常見的 OCR 錯誤包括將 `0`（零）誤讀為 `O`，或將 `1` 誤讀為 `l`。使用正規表達式進行後處理可清理結果：

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## 在 Java 中可靠 OCR 的專業技巧

| Tip | Reason |
|-----|--------|
| **使用無損 PNG** | JPEG 的壓縮雜訊會混淆引擎。 |
| **修剪白色邊框** | 多餘的空白會增加處理時間，且可能導致偽陽性。 |
| **僅在版面未知時設定 `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`**；若已知版面，請選擇特定模式（例如 `PSM_SINGLE_BLOCK`）。 |
| **快取 `ITesseract` 實例** |

## 接下來您應該學習什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可運作的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何在 Java 中使用 Aspose OCR 讀取圖像文字 – 完整指南](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [如何在 Java 中使用 OCR – 快速辨識圖像文字](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Java 批次圖像 OCR – 快速從 PNG 檔提取文字](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}