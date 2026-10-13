---
category: general
date: 2026-09-28
description: 學習如何使用 Aspose OCR 於 Java 從 TIFF 提取文字。本逐步教學示範如何建立 OCR 引擎、讀取大型 TIFF 檔案，並有效辨識文字。
draft: false
keywords:
- extract text from tiff
- aspose ocr java tutorial
- read tiff file java
- large image ocr java
- ocr engine java
lastmod: 2026-09-28
og_description: 使用 Aspose OCR 於 Java 從 TIFF 提取文字。跟隨本教學建立 OCR 引擎、讀取大型 TIFF 檔案，並獲得精確結果。
og_image_alt: Diagram showing OCR engine workflow for large TIFF files in Java
og_title: 從 TIFF 提取文字 – Aspose OCR Java 指南
schemas:
- author: Aspose
  dateModified: '2026-09-28'
  description: Learn how to extract text from TIFF using Aspose OCR in Java. This
    step‑by‑step tutorial shows you how to create an OCR engine, read large TIFF files,
    and recognize text efficiently.
  headline: Extract text from TIFF with Aspose OCR in Java
  type: TechArticle
- questions:
  - answer: Yes, provided you have a valid Aspose.OCR license. The library’s commercial
      license covers both development and production use.
    question: Can I use this solution in a commercial application?
  - answer: TIFF does not have a standard password mechanism, so the library treats
      it as a regular image. For encrypted containers (e.g., ZIP), decrypt before
      passing the stream to the engine.
    question: Does Aspose.OCR support password‑protected TIFF files?
  - answer: Aspose.OCR for Java supports JDK 8 through JDK 21, including both Java
      SE and OpenJDK distributions.
    question: Which Java versions are officially supported?
  - answer: 'Enable preprocessing: `ocrEngine.getConfiguration().setPreprocessOptions(PreprocessOptions.CONTRAST_ENHANCE);`
      This boosts OCR confidence on noisy images.'
    question: How can I improve accuracy on low‑contrast scans?
  - answer: The engine can handle images up to several gigabytes, limited only by
      available disk space for temporary tiles. Memory usage stays under 200 MB thanks
      to streaming.
    question: Is there a limit to the image size I can process?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: 從 TIFF 中提取文字 – 使用 Aspose OCR 於 Java
url: /zh-hant/java/advanced-ocr-techniques/create-ocr-engine-java-recognize-text-from-large-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 在 Java 中從 TIFF 提取文字  

如果您需要從數十或數百兆位元組大小的 TIFF 檔案**提取文字**，本教學提供了可投入生產的解決方案。您將學習如何在 Java 中建立 OCR 引擎、透過 `InputStream` 串流處理大型 TIFF，並在不耗盡 JVM 堆積的情況下取得準確的 Unicode 文字。

## 快速解答
- **什麼函式庫能處理大型 TIFF OCR？** Aspose.OCR for Java。  
- **最低 Java 版本？** JDK 8 或更新版本。  
- **需要授權嗎？** 需要，有效的 `.lic` 檔案可解鎖全解析度分割。  
- **可以處理多頁 TIFF 嗎？** 當然可以 – 引擎會自動分割每一頁。  
- **50 MP 圖片的典型執行時間？** 在標準 4 核心伺服器上約 12 秒。

## 什麼是從 TIFF 提取文字？

**從 TIFF 提取文字**是指使用光學字符辨識 (OCR) 將 TIFF 圖像的視覺內容轉換為可搜尋、可編輯的 Unicode 字元。此過程讓您能為掃描地圖建立索引、自动化掃描表單的資料輸入，並使大型檔案圖像可搜尋，而無需手動重新輸入其內容。最終得到的純文字可儲存、建立索引，或供後續分析管線使用。

## 為什麼使用 Aspose OCR for Java？

Aspose.OCR 支援 **50 多種影像格式**，能在不將整個檔案載入記憶體的情況下處理 **數百頁的 TIFF**，並提供內建語言偵測與自動分割功能。與單純使用 `BufferedImage` 的做法相比，這些特性可將記憶體使用量降低最高達 90 %，同時在噪點或低對比度掃描件上仍保持高準確度。此函式庫亦能輕鬆與其他 Aspose 產品整合，用於 PDF 產生或文件轉換。

## 前置條件
- Java Development Kit (JDK) 8 或更新版本。  
- Aspose.OCR for Java（截至 2026 年 2 月的最新版本）。  
- 您想要處理的大型 TIFF 檔案。  
- Aspose.OCR 授權檔 (`Aspose.OCR.lic`)。  

> **專業提示：** 將 TIFF 檔案放在與原始碼相同的目錄，或使用絕對路徑引用；引擎會在內部自動分割圖像，您無需自行切割圖像。

![Create OCR Engine Java workflow](ocr-workflow.png){alt="建立 OCR 引擎 Java 工作流程圖"}  
[建立 OCR 引擎 Java 工作流程](ocr-workflow.png)

## 如何在 Java 中從 TIFF 提取文字？

使用 `InputStream` 載入您的 TIFF，套用授權，實例化 OCR 引擎，然後呼叫 `recognize`。引擎會將圖像分割成多塊，對每個區塊執行神經網路模型，並將結果拼接，於一次呼叫即返回最終文字。此方法避免將整張圖像載入記憶體，適用於千兆像素檔案，同時使 CPU 使用量可預測。

### 步驟 1 – 套用您的 Aspose.OCR 授權（建立 OCR 引擎 Java）

`License` 類別告訴 OCR 引擎解鎖全解析度分割演算法，這對於有效處理 **大型圖像** 至關重要。

```java
import com.aspose.ocr.*;

public class LicenseHelper {
    /** Loads the Aspose.OCR license from the given path. */
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);   // throws if the file is missing or invalid
    }
}
```  

*為什麼這很重要：* 若未套用授權，引擎將以評估模式運行，限制頁數並在輸出中加入浮水印。

### 步驟 2 – 實例化 OCR 引擎（建立 OCR 引擎 Java）

`OcrEngine` 是執行像素轉文字轉換的核心物件。

```java
/** Returns a fresh OcrEngine ready for recognition. */
public static OcrEngine buildEngine() {
    // No special configuration needed for basic text extraction.
    // You can tweak language, DPI, or preprocessing here if required.
    return new OcrEngine();
}
```  

*為什麼保持簡單：* 預設設定已包含自動語言偵測與最佳分割。過度設定實際上會在大型檔案上降低速度。

### 步驟 3 – 使用 `InputStream` 載入 TIFF 檔案（讀取 TIFF 檔案 Java）

串流檔案可防止 JVM 分配巨大的 `BufferedImage`。Aspose.OCR 會即時讀取並分割圖像。

```java
import java.io.*;

public static InputStream openTiff(String filePath) throws FileNotFoundException {
    // Using try‑with‑resources later guarantees the stream is closed.
    return new FileInputStream(filePath);
}
```  

*邊緣情況：* 若您的 TIFF 使用 CCITT Group 4 壓縮，您可以選擇設定 `ocrEngine.getConfiguration().setTiffCompression(TiffCompression.CCITT4)` 以獲得適度的速度提升。

### 步驟 4 – 準備 OCR 輸入並提示格式

`OcrInput` 可以容納多張影像，但此示範僅需一張。提供格式字串 (`"tif"`) 可省去昂貴的格式偵測。

```java
import com.aspose.ocr.*;

public static OcrInput buildInput(InputStream imageStream) throws Exception {
    OcrInput input = new OcrInput();
    input.add(imageStream, "tif");   // second argument is the optional file extension hint
    return input;
}
```  

*提示有用的原因：* 處理 **大型圖像** 時，每毫秒都很重要。格式提示告訴解析器跳過昂貴的標頭分析。

### 步驟 5 – 從大型圖像辨識文字（從大型圖像辨識文字）

OCR 呼叫會回傳包含純文字、信心分數以及可選的邊界框的 `OcrResult`。

```java
public static OcrResult runRecognition(OcrEngine engine, OcrInput input) throws Exception {
    // The recognize method performs tiling internally, so memory usage stays low.
    return engine.recognize(input);
}
```  

*底層運作原理：* Aspose.OCR 將 TIFF 分割成 1024 × 1024 px 的區塊，對每個區塊執行神經網路模型，並將結果拼接。這就是您能在不進行手動前處理的情況下 **從大型圖像辨識文字** 的原因。

### 步驟 6 – 顯示提取文字的預覽

印出整個文件可能會使主控台淹沒。顯示前 200 個字元即可快速驗證輸出。

```java
public static void printPreview(OcrResult result) {
    String text = result.getText();
    if (text.length() > 200) {
        System.out.println(text.substring(0, 200) + "…");
    } else {
        System.out.println(text);
    }
}
```  

**預期的主控台輸出：**  

```
The quick brown fox jumps over the lazy dog. This map shows the historic...
```  

如果看到亂碼，請再次確認已選擇正確的語言（預設為英語）且 TIFF 檔案未損壞。

## 完整範例

將所有部件組合起來，即可得到一個可編譯執行的單一類別：

```java
import com.aspose.ocr.*;
import java.io.*;

public class LargeImageDemo {

    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Apply your Aspose.OCR license (Create OCR Engine Java)
        // -------------------------------------------------
        LicenseHelper.applyLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Build the OCR engine (Create OCR Engine Java)
        // -------------------------------------------------
        OcrEngine ocrEngine = buildEngine();

        // -------------------------------------------------
        // 3️⃣ Open the huge TIFF (Read TIFF File Java)
        // -------------------------------------------------
        try (InputStream imageStream = openTiff("YOUR_DIRECTORY/huge-map.tif")) {

            // -------------------------------------------------
            // 4️⃣ Prepare OCR input, hint the format
            // -------------------------------------------------
            OcrInput ocrInput = buildInput(imageStream);

            // -------------------------------------------------
            // 5️⃣ Recognize text from large image (Recognize Text from Large Image)
            // -------------------------------------------------
            OcrResult ocrResult = runRecognition(ocrEngine, ocrInput);

            // -------------------------------------------------
            // 6️⃣ Show a preview of the extracted text
            // -------------------------------------------------
            printPreview(ocrResult);
        }
    }

    // Helper methods from previous sections ------------------------------------
    public static void applyLicense(String path) throws Exception {
        License lic = new License();
        lic.setLicense(path);
    }

    public static OcrEngine buildEngine() {
        return new OcrEngine();
    }

    public static InputStream openTiff(String filePath) throws FileNotFoundException {
        return new FileInputStream(filePath);
    }

    public static OcrInput buildInput(InputStream stream) throws Exception {
        OcrInput input = new OcrInput();
        input.add(stream, "tif");
        return input;
    }

    public static OcrResult runRecognition(OcrEngine engine, OcrInput input) throws Exception {
        return engine.recognize(input);
    }

    public static void printPreview(OcrResult result) {
        String txt = result.getText();
        System.out.println(txt.length() > 200 ? txt.substring(0, 200) + "…" : txt);
    }
}
```  

編譯方式：  

```bash
javac -cp "aspose-ocr-23.12.jar" LargeImageDemo.java
java -cp ".:aspose-ocr-23.12.jar" LargeImageDemo
```  

將 `aspose-ocr-23.12.jar` 替換為您下載的實際版本。

## 常見陷阱與技巧  

| 問題 | 發生原因 | 快速解決方案 |
|------|----------|--------------|
| **OutOfMemoryError** | 將 TIFF 載入 `BufferedImage` 而非串流導致。 | 始終如範例使用 `InputStream`；讓 Aspose 處理分割。 |
| **Blank output** | 檔案副檔名提示錯誤（`"tif"` 與 `"tiff"`）。 | 使用傳遞給 `add` 的完全相同字串。 |
| **Garbage characters** | 未套用授權或授權已過期。 | 確認 `.lic` 檔案路徑，並在建立引擎前套用授權。 |
| **Slow recognition** | 自訂 `OcrConfiguration` 設定過高 DPI。 | 保持預設設定；僅在需要更高準確度時才調整。 |

### 何時調整設定  

- **多語言文件：** `ocrEngine.getConfiguration().setLanguage(Language.English, Language.French);`  
- **在細小字體上提升準確度：** `ocrEngine.getConfiguration().setPreprocessOptions(PreprocessOptions.ENHANCE);`  

請記住，每個額外選項都可能增加 CPU 時間，尤其在 **大型圖像** 上。請先以單一區塊測試。

## 從 TIFF 提取文字之後的下一步是什麼？

既然您已能有效 **從 TIFF 提取文字**，可考慮擴充工作流程以建立可搜尋的 PDF、儲存用於標註的邊界框座標，或將區塊處理平行化至多個 CPU 核心。這些增強功能讓您能構建端對端的文件管線，將大量掃描檔案轉換為完整可搜尋、已建立索引的資源，適用於企業搜尋或 GIS 應用。

## 常見問答

**Q: 我可以在商業應用中使用此解決方案嗎？**  
A: 可以，只要您擁有有效的 Aspose.OCR 授權。此函式庫的商業授權涵蓋開發與生產環境的使用。

**Q: Aspose.OCR 支援受密碼保護的 TIFF 檔案嗎？**  
A: TIFF 沒有標準的密碼機制，因此函式庫將其視為普通影像。若是加密的容器（例如 ZIP），請在傳遞串流給引擎前先解密。

**Q: 官方支援哪些 Java 版本？**  
A: Aspose.OCR for Java 支援 JDK 8 至 JDK 21，包括 Java SE 與 OpenJDK 版本。

**Q: 如何提升低對比度掃描的準確度？**  
A: 啟用前處理：`ocrEngine.getConfiguration().setPreprocessOptions(PreprocessOptions.CONTRAST_ENHANCE);` 這可提升噪點影像的 OCR 信心。

**Q: 可處理的圖像大小有上限嗎？**  
A: 引擎可處理高達數 GB 的圖像，唯一限制是暫存區塊所需的磁碟空間。由於使用串流，記憶體使用量維持在 200 MB 以下。

---

**最後更新：** 2026-09-28  
**測試環境：** Aspose.OCR 23.12 for Java  
**作者：** Aspose

## 相關教學

- [使用 Aspose Ocr Java 教學從影像辨識文字](/ocr/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-tutorial/)
- [使用 Aspose Ocr Java 快速指南提取影像文字](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)
- [使用 Aspose Ocr GPU Java 辨識文字影像](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}