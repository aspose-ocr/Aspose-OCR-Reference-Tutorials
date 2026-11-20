---
category: general
date: 2026-09-23
description: 了解如何在 Java 中使用 Aspose OCR 進行圖像文字辨識、從圖像中提取文字，並使用自訂字典啟用拼寫校正。
draft: false
keywords:
- how to perform ocr
- how to extract text from image
- java ocr maven dependency
- java image to text conversion
- aspose ocr java
lastmod: 2026-09-23
og_description: 如何在 Java 中使用 Aspose OCR 進行圖像文字辨識。本指南示範載入圖像、提取圖像文字，並加入拼寫校正以獲得精確結果。
og_image_alt: 'Aspose OCR Java tutorial: extracting text from images with spell correction'
og_title: 如何在 Java 中使用 Aspose OCR 進行圖像文字辨識
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  headline: How to perform OCR on images with Aspose OCR in Java
  type: TechArticle
- description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  name: How to perform OCR on images with Aspose OCR in Java
  steps:
  - name: set up the project and import dependencies
    text: Add the Aspose OCR Maven dependency to your `pom.xml`. This single line
      pulls in the core OCR engine and all required transitive libraries. > **Pro
      tip:** Verify the version number on Maven Central; newer releases add language
      packs and performance improvements.
  - name: load the image for OCR
    text: '`OcrEngine` works with any `InputStream`. Use `ImageStream` to wrap a file
      path, byte array, or URL. **Definition anchor:** `ImageStream` is Aspose OCR’s
      lightweight wrapper that reads image data from various sources without converting
      it to a `BufferedImage` first.'
  - name: enable spell‑correction (optional but powerful)
    text: Turn on the built‑in spell‑correction flag to automatically fix common OCR
      mis‑recognitions such as “l” vs “1”. Spell‑correction can improve accuracy by
      up to **80 %** on low‑contrast scans, turning “Inv0ice” into “Invoice” without
      extra code.
  - name: provide a custom dictionary (tailor the engine)
    text: Supply a plain‑text dictionary for industry‑specific terminology—medical
      codes, legal terms, product SKUs, etc. **Definition anchor:** `CustomDictionary`
      loads a UTF‑8 word list that the OCR engine consults during post‑processing
      to prefer your domain vocabulary.
  - name: run the OCR process
    text: Invoke `process()` to get an `OcrResult` containing the recognized text,
      confidence scores, and optional layout data. If an error occurs, `ocrResult.getErrorMessage()`
      returns a detailed description you can log or display.
  - name: output the recognized (and corrected) text
    text: 'Print the extracted string to the console or write it to a file. For quick
      testing, a simple `System.out.println` is sufficient. Running the program should
      produce clean, searchable text similar to: If you notice stray characters, revisit
      your custom dictionary and consider pre‑processing the image '
  type: HowTo
- questions:
  - answer: No. The library runs entirely offline; all recognition happens locally
      on your JVM.
    question: Does Aspose OCR require an internet connection?
  - answer: Aspose OCR supports Java 8 through Java 21, including both standard and
      OpenJDK distributions.
    question: Which Java versions are supported?
  - answer: Yes. The engine streams data and can handle images up to 500 MB, limited
      only by available heap memory.
    question: Can I process images larger than 10 MB?
  - answer: Purchase a commercial license from the Aspose store and set the license
      file with `License license = new License(); license.setLicense("Aspose.OCR.lic");`.
    question: How do I license Aspose OCR for production?
  - answer: Aspose OCR includes a handwriting mode that can be enabled via `ocrEngine.getEngineOptions().setHandwriting(true);`,
      improving accuracy on cursive scripts.
    question: Is there built‑in support for handwritten text?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- image to text
- OCR Maven dependency
title: 如何在 Java 中使用 Aspose OCR 進行圖像文字辨識
url: /zh-hant/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在圖像上執行 OCR – 完整 Java 教程

如果您正在尋找一種可靠的方法在 Java 中 **how to perform OCR** 圖像檔案，您已來對地方。使用 Aspose OCR for Java，您只需幾行程式碼即可從圖像資產提取文字，透過自訂字典提升準確度，並啟用拼寫校正以清除雜訊掃描。本教程將逐步說明每個步驟——從載入圖像進行 OCR 到列印校正後的文字——讓您今天即可將圖像轉文字的轉換整合到應用程式中。

## 快速答案
- **開始 OCR 的主要類別是什麼？** `OcrEngine` 是 Aspose OCR 的核心類別，用於執行光學字符辨識。
- **哪個 Maven 套件可加入 OCR 支援？** Add `com.aspose:aspose-ocr` to your `pom.xml`.
- **開發時需要授權嗎？** 免費的臨時授權可用於測試；正式環境需商業授權。
- **能否提升低品質掃描的準確度？** 可以——啟用拼寫校正並提供自訂字典。
- **是否內建多頁支援？** 在迴圈中處理每頁圖像；引擎支援執行緒安全的並行執行。

## 什麼是 how to perform OCR？
短語 **how to perform OCR** 指的是將圖像中的印刷或手寫文字轉換為可編輯、可搜尋的數位字符的過程，使用光學字符辨識技術。Aspose OCR 以單次掃描的引擎實作此過程，支援超過 20 種點陣格式與 50 多種語言。

## 為何使用 Aspose OCR for Java？
Aspose OCR 支援 **20+ image formats**（包括 PNG、JPEG、TIFF、BMP 與 GIF），且能在不將整個文件載入記憶體的情況下處理 **multi‑hundred‑page batches**，在一般 4 核心伺服器上可達 **每分鐘 300 頁**。其內建的拼寫校正與自訂字典功能，能將噪聲發票的 OCR 錯誤率從 12 % 降低至低於 2 %。

## 前置條件
- **Java Development Kit (JDK) 8+** – 標準 Java 執行環境。
- **Aspose OCR for Java** library – 從 Maven Central 或 Aspose 下載入口取得最新 JAR。
- 要處理的圖像檔案（例如 `invoice.png`）。
- （可選）`custom_dict.txt` – 包含領域特定詞彙的 UTF‑8 純文字檔，每行一個詞。

這就是全部需求——不需外部服務或龐大框架。

## 如何在 Java 中對圖像執行 OCR？
載入圖像、啟用拼寫校正、（可選）提供自訂字典、執行引擎並讀取結果。此方法適用於單頁檔案與批次處理，且引擎會自動處理圖像解碼、語言偵測與信賴度計分，為您提供可靠的文字輸出，便於後續處理。以下章節將逐步說明每個步驟，並提供可直接複製的完整程式碼。

### 步驟 1：設定專案並匯入相依性
在 `pom.xml` 中加入 Aspose OCR 的 Maven 相依性。此單行會拉入核心 OCR 引擎及所有必要的傳遞相依庫。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

> **小技巧：** 在 Maven Central 上確認版本號；較新版本會加入語言套件與效能改進。

### 步驟 2：載入圖像以進行 OCR
`OcrEngine` 可與任何 `InputStream` 搭配使用。使用 `ImageStream` 包裝檔案路徑、位元組陣列或 URL。

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**定義說明：** `ImageStream` 是 Aspose OCR 的輕量級包裝器，可從各種來源讀取圖像資料，且不需先轉換為 `BufferedImage`。

### 步驟 3：啟用拼寫校正（可選但強大）
開啟內建的拼寫校正旗標，可自動修正常見的 OCR 識別錯誤，例如 “l” 與 “1”。

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

拼寫校正可在低對比度掃描上將準確度提升至 **80 %**，將 “Inv0ice” 轉為 “Invoice”，且不需額外程式碼。

### 步驟 4：提供自訂字典（客製化引擎）
提供純文字字典以涵蓋特定產業術語——醫療代碼、法律用語、產品 SKU 等。

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

**定義說明：** `CustomDictionary` 會載入 UTF‑8 詞彙表，OCR 引擎在後處理時會參考此表以優先使用您的領域詞彙。

### 步驟 5：執行 OCR 程序
呼叫 `process()` 以取得 `OcrResult`，其中包含辨識文字、信賴度分數以及可選的版面資料。

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

若發生錯誤，`ocrResult.getErrorMessage()` 會回傳詳細描述，您可以將其記錄或顯示。

### 步驟 6：輸出辨識（且已校正）的文字
將提取的字串印到主控台或寫入檔案。快速測試時，簡單的 `System.out.println` 即可。

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

執行程式後應產生乾淨、可搜尋的文字，類似於：

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

若發現雜散字元，請重新檢查自訂字典，並考慮對圖像進行前處理（提升對比、去雜訊或轉為灰階）。

## 如何使用自訂字典從圖像提取文字？
在處理前載入字典，然後呼叫 `ocrEngine.setCustomDictionary(customDict)`。引擎會優先使用列表中的詞彙，顯著降低專業詞彙的誤判。提供領域特定詞彙可協助 OCR 後處理器解決模糊字符，例如區分字母 “O” 與數字 “0”，從而提升技術文件的整體準確度。

## 如何正確加入 Java OCR Maven 相依性？
將以下程式碼片段加入 `pom.xml` 的 `<dependencies>` 區段。此相依性會拉入核心 Aspose OCR 程式庫及所有必要的傳遞元件，確保 OCR 引擎可在不需額外設定的情況下實例化。更新檔案後務必執行 `mvn clean install`，讓 Maven 從中央倉庫解析最新版本。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

## 常見問題與邊緣情況

### 如果圖像是其他格式（PDF、TIFF 等）？
Aspose OCR 可直接處理點陣格式。對於 PDF，需先將每頁提取為圖像——Aspose PDF for Java 提供 `PdfExtractor` 可高效完成此作業。取得 `BufferedImage` 或位元組串流後，使用相同的 `setImage` 呼叫即可。此方式讓您在不將整個 PDF 讀入記憶體的情況下處理多頁文件，保持工作流程快速且具擴展性。

### 如何處理多頁文件？
遍歷每頁圖像，建立新的 `OcrEngine`（或重設現有引擎），並串接 `OcrResult.getText()` 的結果。此方法使每頁的拼寫檢查上下文保持獨立。透過順序或平行執行緒處理頁面，您可維持高吞吐量，同時確保每頁皆受相同字典與拼寫校正設定的惠益。

### 能否限制語言或字元集？
可以。呼叫 `ocrEngine.getEngineOptions().setLanguage(Language.English)`（或任何支援的語言）即可縮小辨識範圍，處理速度可提升至 **30 %**。限制語言會減少引擎需考慮的字元集，降低歧義，並提升速度與準確度，特別是僅包含拉丁字元的文件。

### 大批次處理的效能如何？
引擎對唯讀操作具執行緒安全性。建立執行緒池，將每張圖像指派給獨立的 `OcrEngine` 實例。於 4 核心機器上，平行執行可達 **≈250 頁/分鐘**。請確保配置足夠的堆積記憶體，並監控 CPU 使用率，以免在處理數千張高解析度圖像時出現瓶頸。

## 提升準確度的技巧

- **前處理圖像**：在 OCR 前提升對比、套用中值濾波或轉為灰階。
- **使用 300 dpi 或更高** 的掃描；較低解析度會大幅提升錯誤率。
- **保持自訂字典的聚焦**：過多不相關詞彙會干擾拼寫檢查器。
- **使用正規表達式後處理**：在提取後驗證日期、數字或 ID，以捕捉剩餘異常。

## 後續步驟

既然您已了解如何在圖像上 **how to perform OCR** 以及如何 **how to extract text from image** 檔案，您可以進一步探索：

- 將 OCR 輸出儲存為具隱藏文字層的可搜尋 PDF。
- 直接將提取的發票資料存入關聯式資料庫。
- 套用機器學習模型進一步清理手寫筆記。
- 將 OCR 工作流程以 RESTful 網路服務方式公開，供使用者上傳圖片使用。

上述每項延伸皆建立在前述核心步驟之上，您會發現過渡相當順暢。

---

**最後更新：** 2026-09-23  
**測試環境：** Aspose OCR 24.12 for Java  
**作者：** Aspose  



## 常見問答

**Q: Aspose OCR 是否需要網際網路連線？**  
A: 不需要。此程式庫完全離線執行，所有辨識皆在您的 JVM 本機完成。

**Q: 支援哪些 Java 版本？**  
A: Aspose OCR 支援 Java 8 至 Java 21，包括標準版與 OpenJDK 發行版。

**Q: 能處理大於 10 MB 的圖像嗎？**  
A: 可以。引擎以串流方式處理資料，最高可支援至 500 MB 圖像，僅受可用堆積記憶體限制。

**Q: 如何為生產環境取得 Aspose OCR 授權？**  
A: 從 Aspose 商店購買商業授權，並使用以下程式碼設定授權檔：`License license = new License(); license.setLicense("Aspose.OCR.lic");`。

**Q: 是否內建手寫文字支援？**  
A: Aspose OCR 包含手寫模式，可透過 `ocrEngine.getEngineOptions().setHandwriting(true);` 啟用，提升對草寫文字的辨識準確度。

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

## 相關教學

- [Perform Ocr On Image With Aspose Ocr Java Step By Step Guide](/ocr/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/)
- [Preprocess Image Ocr In Java Boost Accuracy Extract Text](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [How To Enable Gpu For Ocr In Java Recognize Text From Image](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}