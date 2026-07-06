---
category: general
date: 2026-07-05
description: 面向 Java 開發者的混合語言 OCR 教學。學習如何在 Java 專案中從圖片取得 OCR 文字，並提供多語言 OCR 範例。
draft: false
keywords:
- mixed language OCR
- get OCR text
- image to text Java
- java OCR example
- multi language OCR
language: zh-hant
og_description: 混合語言 OCR 在 Java 中的說明。使用多語言 OCR 範例，即可從圖像中取得 OCR 文字，今天就能複製貼上使用。
og_title: 混合語言 OCR（光學字元辨識）於 Java – 完整程式教學
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Mixed language OCR tutorial for Java developers. Learn how to get OCR
    text from images to text Java projects with a multi language OCR example.
  headline: Mixed Language OCR in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Mixed language OCR tutorial for Java developers. Learn how to get OCR
    text from images to text Java projects with a multi language OCR example.
  name: Mixed Language OCR in Java – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Create a Maven Project
    text: 'Open a terminal and run:'
  - name: 2. Add the Aspose.OCR Dependency
    text: 'Edit the generated `pom.xml` and insert the following inside the `<dependencies>`
      block:'
  - name: How It Works
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **1** | `OcrEngine` object is created. | The engine encapsulates all OCR functionality;
      without it you can’t call any methods. | | **2** | `setRecognitionLanguage`
      receives `ENGLISH` and `MALAYALAM`. | Supplying both'
  - name: Low‑Quality Images
    text: 'If the image is blurry or has poor contrast, OCR accuracy drops dramatically.
      Consider these remedies:'
  - name: Unsupported Languages
    text: Aspose currently supports over 70 scripts, but Malayalam may require a language
      pack. If `RecognitionLanguage.MALAYALAM` throws an exception, download the additional
      language data from Aspose’s portal and place it in `resources/ocr-data`.
  - name: Large PDFs
    text: When processing multi‑page PDFs, feed each page as a separate image or use
      `OcrEngine.recognizePdf`. The same `setRecognitionLanguage` call applies to
      every page, giving you a seamless **multi language OCR** experience across a
      whole document.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Java 中的混合語言 OCR – 完整逐步指南
url: /zh-hant/java/advanced-ocr-techniques/mixed-language-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java 中的混合語言 OCR – 完整逐步指南

曾經需要 **mixed language OCR**，卻不確定如何在 Java 中實現嗎？你並不孤單。無論是將在英語與馬來亞拉姆語之間切換的舊文件數位化，或是打造支援多種文字的掃描應用程式，挑戰都是真實存在的。在本教學中，我們將完整示範如何從包含兩種語言的位圖中 **get OCR text**，並使用簡潔的 **image to text Java** 工作流程。

我們將逐步說明一個可直接執行的 **java OCR example**，解釋每一行程式碼的意義，並說明 **multi language OCR** 的細節，讓你避免常見的陷阱。完成後，你將擁有一個能將擷取的文字印到主控台的可執行程式——不會有未說明的神祕函式庫。

## 需要的條件

* **Java Development Kit (JDK) 17** 或更新版本 – 程式碼使用現代模組系統，但在 JDK 11+ 亦可運作。  
* **Maven**（或 Gradle） – 會自動下載 OCR 函式庫。  
* 支援多語言的 OCR 引擎 – 本教學將使用 **Aspose.OCR for Java**，它內建英語與馬來亞拉姆語支援。（如果你偏好 Tesseract，步驟相同，只需更換 import 陳述式。）  
* 一張名為 `mixed_english_malayalam.png` 的範例圖片，放置於專案內的 `resources` 資料夾中。  
* 一點點好奇心 – 其餘內容以下說明。

> **Pro tip:** 如果你使用 Windows，請在命令提示字元執行 `mvn -v` 以確認 Maven 已在 PATH 中。

## 設定專案

### 1. 建立 Maven 專案

在終端機中執行以下指令：

```bash
mvn archetype:generate -DgroupId=com.example.ocr \
    -DartifactId=mixed-ocr-demo -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

### 2. 新增 Aspose.OCR 相依性

編輯產生的 `pom.xml`，在 `<dependencies>` 區塊內加入以下內容：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- latest as of July 2026 -->
</dependency>
```

執行 `mvn clean install` 以下載 JAR 檔案。Maven 會處理所有事務，無需自行尋找本機 DLL。

## 撰寫混合語言 OCR 程式碼

在 `src/main/java/com/example/ocr/` 目錄下建立新類別 `MixedLanguageOcrDemo.java`，並貼上以下完整程式碼。每一行皆有註解，讓你了解我們 **why** 這樣做的原因。

```java
package com.example.ocr;

import com.aspose.ocr.*;
import com.aspose.ocr.recognition.*;

public class MixedLanguageOcrDemo {

    public static void main(String[] args) {
        // Step 1: Initialise the OCR engine – this is the entry point for all operations.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Tell the engine which languages to look for.
        // We pass both English and Malayalam; the engine will automatically switch
        // between scripts as it encounters them.
        ocrEngine.setRecognitionLanguage(
                RecognitionLanguage.ENGLISH,
                RecognitionLanguage.MALAYALAM);

        // Step 3: Load the image that contains mixed text.
        // Using a relative path keeps the example portable across machines.
        String imagePath = "resources/mixed_english_malayalam.png";

        // Optional: improve accuracy on low‑resolution scans.
        // Uncomment the next line if your image is under 300 DPI.
        // ocrEngine.setResolution(300);

        // Step 4: Perform the actual OCR operation.
        RecognitionResult result = ocrEngine.recognizeImage(imagePath);

        // Step 5: Extract the plain text – this is the "get OCR text" part.
        String extractedText = result.getText();

        // Step 6: Output the result to the console.
        System.out.println("=== Extracted Text ===");
        System.out.println(extractedText);
    }
}
```

### 工作原理說明

| 步驟 | 發生的情況 | 為何重要 |
|------|--------------|----------------|
| **1** | `OcrEngine` 物件已建立。 | 此引擎封裝所有 OCR 功能；若無它則無法呼叫任何方法。 |
| **2** | `setRecognitionLanguage` 接收 `ENGLISH` 與 `MALAYALAM`。 | 同時提供兩種語言即可啟用 **multi language OCR**；引擎會即時偵測文字腳本變換。 |
| **3** | 定義影像路徑。 | 使用相對路徑可避免硬編碼絕對位置，讓 **java OCR example** 更具可重用性。 |
| **4** | `recognizeImage` 處理位圖。 | 這裡執行大量運算——引擎分析像素、執行神經網路，並回傳 `RecognitionResult`。 |
| **5** | `getText()` 取得純文字字串。 | 這正是你需要的 **get OCR text** 方法，可用於後續處理（例如儲存至資料庫）。 |
| **6** | `System.out.println` 印出字串。 | 即時的視覺回饋可協助你驗證 **image to text Java** 流程是否正常。 |

> **Note:** 如果遇到 `java.lang.UnsatisfiedLinkError`，請確認本機函式庫資料夾已加入 `java.library.path`。Aspose 已為 Windows、macOS 與 Linux 提供所需的二進位檔案。

## 執行示範

使用 Maven 編譯並執行：

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.MixedLanguageOcrDemo"
```

你應該會看到類似以下的輸出：

```
=== Extracted Text ===
Welcome to the conference.
സ്വാഗതം
```

第一行為英語，第二行為馬來亞拉姆語——證明我們的 **mixed language OCR** 成功。

## 處理常見邊緣情況

### 低品質影像

若影像模糊或對比度不足，OCR 準確度會大幅下降。可考慮以下改善措施：

* **Pre‑process** 影像，可使用 OpenCV 等函式庫——轉為灰階、套用自適應閾值，並將解析度提升至至少 300 DPI。  
* 啟用 `ocrEngine.setAutoSkewCorrection(true)`，讓引擎校正旋轉的文字。  
* 若需更嚴格的信心過濾，可提升 `ocrEngine.setConfidenceThreshold(0.6f)` 的值。

### 不支援的語言

Aspose 目前支援超過 70 種文字，但馬來亞拉姆語可能需要額外的語言套件。若 `RecognitionLanguage.MALAYALAM` 拋出例外，請從 Aspose 入口網站下載相應語言資料，並放置於 `resources/ocr-data`。

### 大型 PDF

處理多頁 PDF 時，可將每頁作為單獨影像輸入，或使用 `OcrEngine.recognizePdf`。相同的 `setRecognitionLanguage` 呼叫會套用於每一頁，讓你在整份文件中獲得無縫的 **multi language OCR** 體驗。

## 擴充範例：從主控台到 Web 服務

若想透過 REST 端點公開此功能，可加入 Spring Boot：

```java
@RestController
@RequestMapping("/api/ocr")
public class OcrController {

    @PostMapping(value = "/extract", consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
    public String extractText(@RequestParam("file") MultipartFile file) throws IOException {
        OcrEngine engine = new OcrEngine();
        engine.setRecognitionLanguage(RecognitionLanguage.ENGLISH, RecognitionLanguage.MALAYALM);
        // Save multipart file to a temporary location
        Path temp = Files.createTempFile("upload-", ".png");
        Files.write(temp, file.getBytes());
        RecognitionResult res = engine.recognizeImage(temp.toString());
        return res.getText();
    }
}
```

現在任何客戶端都能 `POST` 影像，並以純 JSON 取得 **get OCR text** 結果。此小幅擴充示範了相同的 **java OCR example** 如何從單一檔案示範擴展至可投入生產的服務。

## 完整原始碼目錄快照

```
mixed-ocr-demo/
├─ pom.xml
└─ src/
   └─ main/
      ├─ java/
      │  └─ com/example/ocr/
      │     └─ MixedLanguageOcrDemo.java
      └─ resources/
         └─ mixed_english_malayalam.png
```

在文章中提供完整的專案結構，可讓讀者輕鬆將目錄複製至 IDE，立即執行。

![混合語言 OCR 範例輸出](https://example.com/assets/mixed-ocr-output.png "混合語言 OCR 範例輸出")

*Image alt text:* mixed language OCR example output – 顯示從同一張圖片中擷取的英語與馬來亞拉姆語文字。

## 重點回顧與後續步驟

我們已從頭到尾說明了在 Java 中的 **mixed language OCR** 流程：

* 設定 Maven 專案並加入 Aspose OCR 相依性。  
* 將引擎設定為英語 + 馬來亞拉姆語，執行辨識，並 **got OCR text**。  
* 討論影像品質、語言套件，以及如何將主控台應用程式轉換為 Web 服務。

如果你已準備好更進一步，可嘗試以下想法：

* 將 Aspose 換成 **Tesseract**，觀察開源引擎如何處理 **multi language OCR**。  
* 嘗試加入其他語言，如 Hindi 或 Tamil——只需將它們加入 `setRecognitionLanguage`。  
* 將結果整合至搜尋索引（例如 Elasticsearch），以實現基於 **image to text Java** 的掃描檔案搜尋功能。

如果有任何問題或想分享自己的調整，歡迎留下評論。祝編程愉快，願你的掃描檔永遠清晰如水晶！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並建立在此處示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索其他實作方式。

- [提取文字影像 – Aspose.OCR for Java OCR 基礎](/ocr/english/java/ocr-basics/)
- [如何使用 Aspose.OCR 依語言 OCR 影像文字](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [使用 Aspose OCR 辨識文字影像 – 完整 Java OCR 教學](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}