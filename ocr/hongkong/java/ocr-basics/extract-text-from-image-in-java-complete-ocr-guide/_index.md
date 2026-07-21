---
category: general
date: 2026-07-21
description: 使用 Java OCR 從圖片中提取文字。了解如何將 PNG 轉換為文字、從 PNG 讀取文字、載入圖片以進行 OCR，以及僅需幾個步驟即可對圖片執行
  OCR。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: zh-hant
lastmod: 2026-07-21
og_description: 使用 Java 從圖像提取文字。本指南將教您如何將 PNG 轉換為文字、從 PNG 讀取文字、載入圖像進行 OCR，以及高效執行圖像
  OCR。
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: 在 Java 中從圖像提取文字 – 步驟式 OCR 教學
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: 在 Java 中從圖像擷取文字 – 完整 OCR 指南
url: /zh-hant/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字（Java） – 完整 OCR 指南

是否曾需要 **extract text from image**（從圖像中提取文字），卻不確定該選擇哪個 Java 函式庫？你並不孤單。無論是數位化收據、掃描 PDF，或是建立可搜尋的檔案庫，從 PNG 中抽取文字都是許多開發者每天面對的痛點。

在本教學中，我們將一步步示範一個實作解決方案，讓你能 **convert PNG to text**、**read text from PNG**、**load image for OCR**，以及 **perform OCR on image**——只需幾行簡潔的 Java 程式碼。完成後，你將擁有一個可直接放入任何專案的可執行程式。

## 你將構建的應用

我們將建立一個小型的 Java 主控台應用程式，具備以下功能：

1. 從磁碟載入 PNG 檔案。  
2. 將影像送至 OCR 引擎（Tess4J，Tesseract 的 Java 包裝器）。  
3. 將辨識出的文字印出到主控台。

不需要外部服務，也不靠魔法——僅使用純 Java 與開源 OCR 引擎。

## 前置條件

- **Java 17** 或更新版本（程式碼在較舊版本亦可編譯，但 Java 17 提供最新的語言功能）。  
- **Maven** 或 **Gradle** 用於相依管理。  
- 一個名為 `sample.png` 的範例 PNG，放在可參考的資料夾中（例如 `src/main/resources`）。  
- 基本了解 Java 的 `main` 方法與例外處理。

如果上述任一項目聽起來陌生，別擔心——每一步都會提供簡短的回顧說明。

## 步驟 1：設定專案並加入 OCR 函式庫

首先，建立一個新的 Maven 專案（如果偏好 Gradle 也可）。加入 Tess4J 相依性，該套件會為你自動帶入 Tesseract 二進位檔。

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
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

> **小技巧：** 若使用 Gradle，等效的寫法是 `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`。

加入此函式庫後，你即可使用 `Tesseract` 類別，它負責執行 **perform OCR on image**（對影像執行 OCR）的繁重工作。

## 步驟 2：載入影像以供 OCR

現在我們需要 **load image for OCR**。Tess4J 使用 `java.awt.image.BufferedImage`，因此我們將透過 `ImageIO` 讀取 PNG。

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

上述方法將 **load image for OCR** 的邏輯獨立抽離，使其餘程式碼更易於測試。請留意註解——它與原始片段相呼應，同時為了清晰度而加以說明。

## 步驟 3：對影像執行 OCR

影像已載入記憶體後，我們即可 **perform OCR on image**。`Tesseract` 物件即為我們的引擎；我們會將其設定為使用 Tess4J 隨附的預設英文語言資料。

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

此處我們將原本的「Step 1」與「Step 4」合併為單一方法，因為建立 `Tesseract` 物件成本低且我們希望程式碼保持簡潔。註解仍會引用原始步驟以利追蹤。

## 步驟 4：整合全部——主方法

最後，我們在 `main` 中將所有部份整合。這裡就是你會 **read text from PNG**，並在主控台看到輸出結果的地方。

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

執行 `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"`（或相對應的 Gradle 指令）時，應會看到類似以下的輸出：

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

此輸出證明你已成功 **extract text from image**、**convert PNG to text**，以及 **read text from PNG**，全部於同一個簡潔的程式中完成。

## 處理常見的邊緣情況

### 低品質影像

若 PNG 模糊或對比度低，OCR 的準確度會下降。快速的解決方式是先對影像進行前處理：

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### 多語言支援

Tess4J 能支援多種語言。只需下載相對應的 `.traineddata` 檔案，並將 `tesseract.setLanguage("spa")` 設為西班牙語即可，例如。

### 大型 PDF 或多頁影像

若需從 PDF 內的 **extract text from image** 檔案取得文字，可先使用 PDFBox 將每頁切割為 PNG，然後將每個 PNG 交給相同的 OCR 程序處理。

## 完整可執行範例（所有程式碼彙整於此）

以下為完整、可直接執行的 Java 類別。將其複製貼上至 `src/main/java/com/example/ocrdemo/OcrDemo.java` 即可開始使用。

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

執行此類別會印出 OCR 結果，證實你已成功 **performed OCR on image**，並將 PNG 轉換為可編輯的文字。

## 重點回顧與後續步驟

我們從使用輕量級 Java 環境 **extracting text from image** 開始。現在你已了解如何 **load image for OCR**、**perform OCR on image**，以及 **read text from PNG**——這些都是任何文件數位化流程的核心組件。

想更進一步嗎？試試以下想法：

- **批次處理：** 迭代目錄中的 PNG，將每個結果寫入 `.txt` 檔案。  
- **整合資料庫：** 將抽取的字串與中繼資料一起儲存，以供可搜尋的檔案庫使用。  
- **結合 NLP：** 將 OCR 輸出送入情感分析模型，快速獲得洞見。  

上述每項延伸皆基於我們所討論的核心概念，讓你可以立即著手實驗。

---

*祝編程愉快！如遇任何問題

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此技術為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose.OCR 偵測區域模式的 Java 圖像文字提取](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Java 圖像轉文字：使用 Aspose.OCR 將圖像轉換為文字](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [如何使用 Aspose.OCR 以語言執行圖像文字 OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}