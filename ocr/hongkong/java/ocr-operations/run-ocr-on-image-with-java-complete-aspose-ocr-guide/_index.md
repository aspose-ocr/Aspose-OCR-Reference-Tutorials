---
category: general
date: 2026-02-09
description: 使用 Aspose OCR 在 Java 中對圖像執行 OCR – 學習如何從 PNG 提取文字，並在幾個步驟內啟用自動偵測語言的 OCR。
draft: false
keywords:
- run OCR on image
- extract text from PNG
- auto detect language OCR
- Aspose OCR Java
- Hindi OCR example
language: zh-hant
og_description: 即時對圖像執行 OCR。本指南說明如何從 PNG 檔案提取文字，並使用 Aspose OCR for Java 啟用自動語言偵測 OCR。
og_title: 使用 Java 在圖像上執行 OCR – 完整 Aspose OCR 教學
tags:
- OCR
- Java
- Aspose
title: 使用 Java 在圖像上執行 OCR – 完整 Aspose OCR 指南
url: /zh-hant/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java 執行影像 OCR – 完整 Aspose OCR 指南

有沒有曾經需要 **在影像上執行 OCR** 檔案，但不知從何入手？或許你手上有幾張包含印地語文字的 PNG 截圖，想知道 Java 能否在不使用大型機器學習環境的情況下擷取文字。好消息是：可以，而且使用 Aspose OCR 非常簡單。

在本教學中，我們將示範一個實務範例，該範例 **extracts text from PNG** 檔案、說明如何啟用 **auto detect language OCR**，並提供一個可直接執行的 Java 程式。完成後，你將擁有一段能在主控台印出印地語字元的可執行程式碼，並了解每一行程式碼的意義。

## 需要的環境

- **Java Development Kit (JDK) 8** 或更新版本 – 程式碼可在任何較新的版本編譯。  
- **Aspose.OCR for Java** 函式庫 – 從 Aspose 官方網站或 Maven Central 取得最新 JAR。  
- 一張示範影像（`hindi_sample.png`）包含天城文（Devanagari）字形 – 可使用任何截圖工具自行製作。  
- 任一 IDE 或簡易文字編輯器 – 我使用 IntelliJ IDEA，但直接使用 `javac` 亦可。

不需要外部服務、雲端 API 金鑰，只要本機的 JAR 與一張圖片。很簡單，對吧？

## 步驟 1：將 Aspose OCR 加入專案

首先，確保 Aspose OCR JAR 已加入 classpath。若使用 Maven，請加入以下相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

如果偏好手動方式，下載 `aspose-ocr-23.10.jar` 並放入 `libs/` 資料夾，之後使用以下指令編譯：

```bash
javac -cp "libs/*" LanguageExample.java
```

> **小技巧：** 在原始檔案的最上方以註解保留 JAR 版本號，方便未來回顧時知道使用的是哪個 API 介面。

## 步驟 2：建立 OCR Engine 實例

現在我們建立負責所有繁重工作的核心物件。可將 `OcrEngine` 視為此操作的“大腦”。

```java
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

為什麼在此處實例化？引擎會保存設定（例如語言）與可重複使用的資源，於整個應用程式只建立一次即可降低開銷。

## 步驟 3：設定語言（並啟用 Auto‑Detect）

若事先知道語言——例如印地語——可告訴引擎只辨識天城文。這樣可提升準確度並加快處理速度。

```java
// Step 3a: Force Hindi (Devanagari) recognition
ocrEngine.getConfiguration().setLanguage(Language.HINDI);

// Step 3b (optional): Let the engine guess the language if you're unsure
ocrEngine.getConfiguration().setAutoDetectLanguage(true);
```

`setAutoDetectLanguage(true)` 這一行即是 **auto detect language OCR** 的開關。當輸入混合語言的影像時，引擎會自動嘗試辨識每種文字。對於無法手動標記每個檔案的批次工作非常方便。

## 步驟 4：在 PNG 影像上執行 OCR

這裡才是真正對 **run OCR on image** 資料執行的地方。`recognize` 方法接受檔案路徑、讀取位圖，並回傳 `RecognitionResult`。

```java
// Step 4: Perform OCR on the PNG file
RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");
```

將 `YOUR_DIRECTORY` 替換為實際的資料夾路徑。若找不到檔案，Aspose 會拋出明確的例外，無需事後猜測失敗原因。

## 步驟 5：取得並顯示擷取的文字

最後，從結果物件中取得辨識出的字串並印出。若終端機支援 UTF‑8，印出印地語時會顯示 Unicode 字元。

```java
// Step 5: Output the recognized Hindi text
System.out.println("Hindi text:");
System.out.println(result.getText());
```

**預期輸出**（假設示範影像顯示「नमस्ते दुनिया」）：

```
Hindi text:
नमस्ते दुनिया
```

若已啟用 auto‑detect 且影像同時包含英文，輸出將會同時呈現兩種文字，且混合顯示。

## 完整可執行範例

以下為完整可執行的程式。將其複製貼上至 `LanguageExample.java`，調整影像路徑，即可執行。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Specify the language to be recognized (Hindi – Devanagari script)
        ocrEngine.getConfiguration().setLanguage(Language.HINDI);

        // Step 3: (Optional) Enable automatic fallback to language detection
        ocrEngine.getConfiguration().setAutoDetectLanguage(true);

        // Step 4: Run OCR on the input image
        RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");

        // Step 5: Print the extracted Hindi text
        System.out.println("Hindi text:");
        System.out.println(result.getText());
    }
}
```

> **注意：** 若使用 IDE，請確保專案的建置路徑已包含 Aspose OCR JAR。於 IntelliJ 中，前往 *File → Project Structure → Libraries* 並將 JAR 加入。

## 常見問題與特殊情況

### 如果我的 PNG 解析度太低？

OCR 準確度在低於 150 dpi 時會急速下降。可使用 ImageMagick 等工具（`convert input.png -resize 200% output.png`）先將影像放大，再送入引擎。`auto detect language OCR` 旗標仍然有效，但誤辨率會減少。

### 我可以在迴圈中處理多張影像嗎？

當然可以。將 `recognize` 呼叫包在 `for` 迴圈中，並重複使用同一個 `OcrEngine` 實例。重複使用引擎可避免每次迭代重新載入語言模型，從而節省記憶體與 CPU 時間。

```java
String[] files = {"img1.png", "img2.png", "img3.png"};
for (String file : files) {
    RecognitionResult r = ocrEngine.recognize(file);
    System.out.println("Text from " + file + ":");
    System.out.println(r.getText());
}
```

### 如何處理非 Unicode 終端機？

若終端機顯示亂碼，請在啟動 Java 時設定檔案編碼為 UTF‑8：

```bash
java -Dfile.encoding=UTF-8 -cp "libs/*" LanguageExample
```

### 有辦法取得信心分數嗎？

可以。`RecognitionResult` 內含 `getConfidence()`，會回傳每行辨識結果的 0~1 浮點數。可遍歷 `result.getLines()` 取得這些值，方便過濾低信心的結果。

## 生產環境使用的進階建議

- **快取語言模型**：若處理數千張影像，請讓引擎在整批作業期間保持存活。  
- **平行處理**：將每張影像包在 `Callable` 中，交給執行緒池。需注意引擎非執行緒安全，請每個執行緒各自建立實例。  
- **日誌記錄**：大型作業請使用正式的 logger（如 SLF4J）取代 `System.out.println`。  
- **記憶體管理**：完成後呼叫 `ocrEngine.dispose()` 釋放原生資源。

## 視覺概覽

![在影像上執行 OCR 範例圖](ocr_flow.png "在影像上執行 OCR 範例圖")

上圖說明了流程：**run OCR on image → language configuration → auto detect language OCR（可選）→ extract text from PNG**。

## 結論

我們剛剛示範了如何使用 Aspose OCR for Java **run OCR on image** 檔案、如何以語言特定設定 **extract text from PNG**，以及如何切換 **auto detect language OCR** 以因應彈性多語言情境。完整程式碼範例已備妥，可直接複製、編譯與執行——無隱藏步驟，也不需外部服務。

準備好接受下一個挑戰了嗎？試著將 `Language.HINDI` 換成 `Language.AUTO`，並輸入混合文字的文件，或嘗試 PDF 輸入（Aspose OCR 亦支援 PDF）。你也可以將此程式碼片段整合至 Spring Boot REST 端點，將 OCR 以 Web 服務形式提供。

祝程式開發愉快，願你的影像永遠可讀！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}