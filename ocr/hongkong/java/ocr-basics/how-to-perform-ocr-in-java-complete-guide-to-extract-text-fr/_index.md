---
category: general
date: 2026-06-06
description: 如何在 Java 中執行 OCR – 快速從圖片提取文字、將圖片轉換為文字，並使用簡單程式碼範例讀取 JPG 中的文字。
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: zh-hant
og_description: 如何在 Java 中執行 OCR – 學習如何從圖像提取文字、將圖像轉換為文字，以及使用即用範例讀取 JPG 中的文字。
og_title: 如何在 Java 中執行 OCR – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: 如何在 Java 中執行 OCR – 完整指南：從圖像中提取文字
url: /zh-hant/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中執行 OCR – 從圖像提取文字的完整指南

有沒有想過 **如何在手機拍攝的圖片上執行 OCR**？你並非唯一的疑問者。無論你是要打造收據掃描應用，或只是需要從掃描的 PDF 中提取文字，**如何在 Java 中執行 OCR**都是一項快速見效的技能。在本教學中，我們將示範一個實用範例，**從圖像檔案中提取文字**、**將圖像轉換為文字**，甚至展示如何僅用幾行程式碼 **從 jpg 讀取文字**。

> *小技巧：* 同樣的方法也適用於 PNG、BMP，或任何 OCR 引擎支援的格式——只要更換檔名即可。

## 在 Java 中執行 OCR – 概觀

光學字符辨識（OCR）是一項將字母圖片轉換為實際、可搜尋文字的技術。在 Java 生態系統中有多個函式庫——Tesseract、Asprise，以及商業 SDK——皆提供類似的工作流程：載入圖像、告訴引擎預期的語言、執行辨識，然後取得結果。以下我們將使用一個通用的 `OcrEngine` 類別來保持範例簡潔，但你可以替換成任何遵循相同模式的具體實作。

### 你將學會

- 安裝 OCR 函式庫（是的，**ocr in java** 比你想像的更簡單）。
- 建立並設定 OCR 引擎實例。
- 載入 JPG（或任何圖像）並設定語言。
- 處理圖像並 **從圖像提取文字** 檔案。
- 將辨識出的字串印到主控台。

完成後，你將擁有一個獨立的 Java 程式，可直接放入任何專案並立即執行。

![如何執行 OCR 範例](ocr-example.png "如何在 Java 中執行 OCR 示意圖")

## 步驟 1 – 安裝並匯入 OCR 函式庫（ocr in java）

在撰寫任何 Java 程式碼之前，你需要一個實際負責繁重工作的函式庫。如果你使用 Maven，請加入如下相依性（將 `com.example.ocr` 替換為你所選 SDK 的真實 group ID）：

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

如果你偏好 Gradle：

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

將 JAR 放入 classpath 後，匯入你需要的類別：

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **為何重要：** 正確匯入類別可避免 “cannot find symbol” 錯誤，讓 IDE 開心——在你嘗試 **將圖像轉換為文字** 時，缺少匯入是最令人沮喪的事。

## 步驟 2 – 建立 OCR 引擎實例（how to perform OCR）

現在函式庫已就緒，啟動引擎。將引擎想像成會觀察像素並猜測字母的大腦。

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

建立引擎通常成本不高；大多數 SDK 會延遲分配內部緩衝區，因此在批次處理多張圖像時，你可以安全地重複使用同一實例。

## 步驟 3 – 載入圖像並設定語言（extract text from image）

下一步是提供給引擎可讀取的內容。此處我們從磁碟載入 JPEG，並告訴 OCR 引擎文字是蒙古語（ISO 639‑2 代碼 “mon”）。你可以依需求更改路徑或語言代碼。

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **附註：** 若未設定語言，引擎預設為英語，當文字實際為西里爾字母或其他文字時，準確度會大幅下降。盡可能指定正確的語言。

## 步驟 4 – 處理圖像並取得結果（convert image to text）

在圖像與語言設定完成後，請求引擎施展魔法。`process()` 呼叫會執行 OCR 演算法，並回傳包含辨識字串與信心分數的 `OcrResult` 物件。

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

在背後，引擎可能會執行前處理——去斜、二值化、降噪——讓你不必自行編寫這些步驟。這也是為何大多數現代 OCR 函式庫在 **將圖像轉換為文字** 任務上使用起來如此愉快。

## 步驟 5 – 輸出提取的文字（read text from jpg）

最後，從結果中取出純文字並加以利用。此示範僅將其印到主控台，但你也可以寫入檔案、送入搜尋索引，或傳遞給其他服務。

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

僅此一行即證明你已成功 **從 jpg 讀取文字**（或任何支援的格式）。若輸出呈現亂碼，請再次確認語言代碼與圖像品質。

## 完整可執行範例（結合所有步驟）

以下是一個完整、可直接執行的 Java 類別，將所有部份串接起來。將其複製到名為 `OcrDemo.java` 的檔案，調整圖像路徑與語言，然後執行 `javac OcrDemo.java && java OcrDemo`。

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### 預期輸出

若 `input.jpg` 包含蒙古語短句 “Сайн байна уу?”，主控台將顯示：

```
=== Recognized Text ===
Сайн байна уу?
```

若圖像模糊或語言代碼錯誤，將看到亂碼或空字串——這些常見陷阱我們接下來會討論。

## 常見問題與解決方法

| 症狀 | 可能原因 | 解決方式 |
|---------|--------------|-----|
| 西里爾字元亂碼 | 語言代碼錯誤（預設為英語） | 設定 `ocrEngine.getSettings().setLanguage("mon")` 或相應的語言代碼。 |
| 完全沒有輸出 | 圖像路徑錯誤或檔案無法讀取 | 確認路徑、確保檔案存在且程式具有讀取權限。 |
| 準確度低 (<70 %) | 圖像對比度低或已旋轉 | 前處理圖像：提升對比度、去斜或轉為灰階後再送入引擎。 |
| `OutOfMemoryError` 發生於大型 PDF | 一次載入大量高解析度頁面 | 一次處理單頁，或在 OCR 前將圖像縮小。 |

### 小技巧：批次處理

如果需要批量 **從圖像提取文字** 檔案，將核心邏輯包在迴圈中：

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

此程式碼片段示範了從單一 JPG 擴展至整個資料夾掃描檔的簡易性。

## 更進一步 – 接下來可以探索什麼？

- **語言套件：** 大多數 OCR SDK 允許下載額外的語言資料檔。新增語言套件可讓你 **將圖像轉換為文字**，支援除英語與蒙古語之外的其他語言。
- **PDF OCR：** 結合此程式碼與 Apache PDFBox 以

## 接下來應該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在此處示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [提取圖像文字 – Aspose.OCR for Java 基礎](/ocr/english/java/ocr-basics/)
- [在 Java 中使用 Aspose.OCR BufferedImage 將圖像轉換為文字](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [使用 Aspose.OCR 以語言 OCR 圖像文字](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}