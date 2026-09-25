---
category: general
date: 2026-02-17
description: 建立 OCR 引擎（Java）並快速讀取 TIFF 檔案。學習如何使用 Aspose.OCR 逐步辨識大型影像中的文字。
draft: false
keywords:
- create ocr engine java
- read tiff file java
- recognize text from large image
- Aspose OCR Java
- large image processing Java
language: zh-hant
og_description: 立即建立 OCR 引擎 Java。本教學示範如何在 Java 中讀取 TIFF 檔案，並使用 Aspose.OCR 從大型圖像中辨識文字。
og_title: 創建 OCR 引擎 Java – 大型圖像文字辨識完整指南
tags:
- OCR
- Java
- Aspose
title: 建立 OCR 引擎 Java – 從大型圖像辨識文字
url: /zh-hant/java/advanced-ocr-techniques/create-ocr-engine-java-recognize-text-from-large-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 OCR 引擎 Java – 從大型圖像辨識文字  

曾經需要 **create OCR engine Java** 程式碼來處理巨大的 TIFF 地圖，但不知從何入手嗎？你並不孤單——大多數開發者在圖像尺寸超過一般記憶體限制時都會卡住。  

在本指南中，我們將逐步說明一個完整、可直接執行的範例，該範例 **creates an OCR engine in Java**、示範如何使用 `InputStream` **read TIFF file Java**，最後在不耗盡堆積記憶體的情況下 **recognizes text from large image** 檔案。完成後，你將擁有一個可直接放入任何 Maven 或 Gradle 專案的獨立程式。  

## 你需要的條件  

- **Java Development Kit (JDK) 8 or newer** – 程式碼僅使用標準 I/O 以及 Aspose.OCR。  
- **Aspose.OCR for Java** library（截至 2026‑02 的最新版本）– 你可以從 Aspose 官方網站或 Maven Central 取得 JAR。  
- 一個 **large TIFF file**（例如多百萬像素的地圖），你想要進行 OCR。  
- 你的 **Aspose.OCR license file** (`Aspose.OCR.lic`)。若未提供授權檔，引擎會以評估模式運作，且會出現浮水印。  

> **Pro tip:** 將 TIFF 放在來源資料夾旁邊或使用絕對路徑；引擎會在內部自動切割圖像，無需自行分割。  

![建立 OCR 引擎 Java 工作流程](ocr-workflow.png){alt="建立 OCR 引擎 Java 工作流程圖"}  

## Step 1 – 套用你的 Aspose.OCR 授權 (Create OCR Engine Java)  

在引擎執行任何繁重工作之前，你必須註冊授權。跳過此步驟會強制使用評估模式，限制頁數並在輸出中加入水印。  

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

*Why this matters:* `License` 物件告訴 OCR 引擎解鎖完整解析度的切割演算法，這對有效處理 **large image** 極為重要。  

## Step 2 – 建立 OCR 引擎實例 (Create OCR Engine Java)  

現在我們啟動核心的 `OcrEngine`。可將其視為稍後讀取像素並輸出 Unicode 文字的大腦。  

```java
/** Returns a fresh OcrEngine ready for recognition. */
public static OcrEngine buildEngine() {
    // No special configuration needed for basic text extraction.
    // You can tweak language, DPI, or preprocessing here if required.
    return new OcrEngine();
}
```  

*Why we keep it simple:* 對於大多數情況，預設設定已包含自動語言偵測與最佳切割。過度設定反而會在處理巨型檔案時降低速度。  

## Step 3 – 使用 InputStream 載入 TIFF 檔案 (Read TIFF File Java)  

大型 TIFF 可能高達數百 MB。將整個檔案載入 `BufferedImage` 會使堆積記憶體爆炸。相反地，我們將 `InputStream` 提供給引擎；Aspose.OCR 會即時讀取並切割圖像。  

```java
import java.io.*;

public static InputStream openTiff(String filePath) throws FileNotFoundException {
    // Using try‑with‑resources later guarantees the stream is closed.
    return new FileInputStream(filePath);
}
```  

*Edge case:* 若你的 TIFF 使用 CCITT Group 4 壓縮，Aspose.OCR 仍能處理，但可設定 `ocrEngine.getConfiguration().setTiffCompression(TiffCompression.CCITT4)` 以獲得微幅加速。  

## Step 4 – 準備 OCR 輸入並提示格式  

`OcrInput` 物件可容納多張圖像，但本示範僅需一張。提供格式字串 (`"tif"`) 可協助引擎跳過格式偵測，省下數毫秒。  

```java
import com.aspose.ocr.*;

public static OcrInput buildInput(InputStream imageStream) throws Exception {
    OcrInput input = new OcrInput();
    input.add(imageStream, "tif");   // second argument is the optional file extension hint
    return input;
}
```  

*Why the hint is useful:* 處理 **large images** 時，每毫秒都很重要。格式提示讓解析器略過昂貴的標頭分析。  

## Step 5 – 從大型圖像辨識文字 (Recognize Text from Large Image)  

完成所有設定後，實際的 OCR 呼叫只需一行程式碼。引擎會回傳 `OcrResult`，其中包含純文字、信心分數，若需要亦可取得文字框的座標。  

```java
public static OcrResult runRecognition(OcrEngine engine, OcrInput input) throws Exception {
    // The recognize method performs tiling internally, so memory usage stays low.
    return engine.recognize(input);
}
```  

*What happens under the hood:* Aspose.OCR 會將 TIFF 分割成可管理的切片（預設 1024 × 1024 px），對每個切片執行神經網路模型，最後將結果拼接。這就是為何你能 **recognize text from large image** 檔案而不需手動前處理。  

## Step 6 – 顯示擷取文字的預覽  

將整份文件印到主控台可能會太多。這裡只顯示前 200 個字元，並加上省略號，讓你能快速驗證輸出。  

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

*預期的主控台輸出:*  

```
The quick brown fox jumps over the lazy dog. This map shows the historic...
```  

如果看到亂碼，請再次確認已選擇正確的語言（預設為 English）且 TIFF 檔未損毀。  

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

編譯指令：  

```bash
javac -cp "aspose-ocr-23.12.jar" LargeImageDemo.java
java -cp ".:aspose-ocr-23.12.jar" LargeImageDemo
```  

將 `aspose-ocr-23.12.jar` 替換為你實際下載的版本。  

## 常見問題與技巧  

| Issue | Why it Happens | Quick Fix |
|------|----------------|-----------|
| **OutOfMemoryError** | 將 TIFF 載入 `BufferedImage` 而非以串流方式讀取。 | 始終如範例使用 `InputStream`；讓 Aspose 處理切割。 |
| **Blank output** | 檔案副檔名提示錯誤（`"tif"` 與 `"tiff"`）。 | 使用傳給 `add` 的完全相同字串。 |
| **Garbage characters** | 授權未套用或已過期。 | 確認 `.lic` 檔案路徑，並在建立引擎前重新套用授權。 |
| **Slow recognition** | 使用自訂的 `OcrConfiguration` 且設定高 DPI。 | 大多數情況下使用預設值；僅在需要更高精度時才調整。 |

### 何時調整設定  

- **Multi‑language documents:** `ocrEngine.getConfiguration().setLanguage(Language.English, Language.French);`  
- **Higher accuracy on tiny fonts:** `ocrEngine.getConfiguration().setPreprocessOptions(PreprocessOptions.ENHANCE);`  

但請記住，每增加一個選項都可能增加 CPU 時間，尤其在 **large image** 上。請先以單一切片測試。  

## 後續步驟  

既然你已了解如何 **create OCR engine Java**、**read TIFF file Java**，以及 **recognize text from large image**，接下來可能想要：

1. **Export the result to a PDF** – 結合 Aspose.PDF 與 OCR 文字，以產生可搜尋的文件。  
2. **Store bounding boxes** – 使用 `ocrResult.getWords()` 取得座標以進行標示。  
3. **Parallelize tile processing** – 針對超大型衛星影像，啟動多執行緒…  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}