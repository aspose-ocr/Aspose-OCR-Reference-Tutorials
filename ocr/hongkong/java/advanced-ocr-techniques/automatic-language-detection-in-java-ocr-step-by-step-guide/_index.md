---
category: general
date: 2026-02-27
description: 自動語言偵測讓您在 Java 中從 PNG 等影像檔案提取文字——請參考一個支援自動語言偵測的 Java OCR 範例。
draft: false
keywords:
- automatic language detection
- extract text from image
- convert png to text
- java ocr example
- enable auto language detection
language: zh-hant
og_description: Java OCR 的自動語言偵測讓從圖像檔案提取文字變得輕鬆。了解如何使用完整的 Java OCR 範例啟用自動語言偵測。
og_title: Java OCR 中的自動語言偵測 – 完整指南
tags:
- Java
- OCR
- Aspose
title: Java OCR 自動語言偵測 – 逐步指南
url: /zh-hant/java/advanced-ocr-techniques/automatic-language-detection-in-java-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCR 中的自動語言偵測 – 完整教學

有沒有曾經在從混合英文與俄文的螢幕截圖中擷取文字時，需要 **自動語言偵測**？你並非唯一遇到這個問題的人。在許多實際應用中——例如收據掃描器、多語言表單或社交媒體圖片機器人——事先手動選擇語言是一大痛點。  

好消息是 Aspose OCR for Java 能夠自動偵測語言，讓你只需 **從圖像中擷取文字**，無需任何手動設定。在本教學中，我們將示範一個 **java ocr example**，啟用 **自動語言偵測**、處理混合語言的 PNG，並將結果輸出到主控台。完成後，你將清楚知道如何僅用幾行程式碼 **convert png to text**。

## 需求環境

- Java 17（或任何較新的 JDK）——API 支援 Java 8 以上，但較新的執行環境可提供更佳效能。
- Aspose OCR for Java 函式庫（截至 2026‑02‑27 的最新版本）。可從 Maven Central 取得：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

- 一個包含多種語言的圖像檔案。示範中我們使用 `mixed-eng-rus.png`（英文 + 俄文）。  
- 一個不錯的 IDE（IntelliJ IDEA、Eclipse、VS Code…）——皆可使用。

> **小技巧：** 若沒有測試圖像，只需自行建立一個包含幾個英文單詞及其俄文對應的 PNG。OCR 引擎不在乎圖像來源，只關注像素資料。

以下是完整、可直接執行的程式範例。

![混合語言 PNG 的自動語言偵測](/images/mixed-eng-rus.png "自動語言偵測範例")

## 步驟 1：設定 OCR 引擎

首先，建立 `OcrEngine` 的實例。此物件是函式庫的核心，負責保存所有設定選項，其中就包括啟用 **自動語言偵測** 的設定。

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection
        ocrEngine.setAutoDetectLanguage(true);
```

為什麼在此啟用它？  
因為若未呼叫 `setAutoDetectLanguage(true)`，引擎會預設使用一種語言（通常為英文）。當圖像混合多種文字時，偵測步驟能大幅提升準確度——可視為 OCR 版的多語言口譯員，在翻譯前先聆聽語言。

## 步驟 2：提供圖像並執行 OCR 處理

現在將引擎指向 PNG 檔案。`processImage` 方法會回傳一個 `OcrResult` 物件，內含辨識出的文字、信心分數，甚至偵測到的語言代碼。

```java
        // Step 3: Process the image that contains both English and Russian text
        OcrResult ocrResult = ocrEngine.processImage("YOUR_DIRECTORY/mixed-eng-rus.png");
```

需要留意的幾點：

- **路徑處理：** 使用絕對路徑，或將圖像放在專案的 resources 資料夾，並透過 `getResourceAsStream` 讀取。
- **效能小技巧：** 若要處理大量圖像，請重複使用同一個 `OcrEngine` 實例，而非每次都新建。引擎會快取語言模型，後續呼叫會更快。

## 步驟 3：取得並顯示辨識文字

最後，從 `OcrResult` 中取得純文字。`getText()` 方法會去除所有版面資訊，回傳乾淨的字串，供你儲存、搜尋或傳遞給其他系統使用。

```java
        // Step 4: Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

執行程式後，你應該會看到類似以下的輸出：

```
Hello world!
Привет мир!
```

此輸出證實引擎正確辨識了英文與俄文區塊，這全賴 **自動語言偵測**。若關閉此旗標，俄文部分很可能會變成亂碼，說明在混合語言情境下自動偵測功能是多麼重要。

## 常見變形與例外情況

### 不使用語言偵測的 PNG 轉文字

若你確定圖像僅包含單一語言，可省略自動偵測步驟：

```java
ocrEngine.setLanguage(OcrLanguage.English);
```

但請記住，一旦出現其他文字腳本的雜散字元，準確度會急劇下降。

### 處理大型圖像

對於高解析度掃描，建議在輸入圖像前先將解析度縮減至最高 300 DPI。OCR 引擎在 150‑300 DPI 的範圍內表現最佳；超過此範圍只會浪費記憶體，卻無明顯效益。

```java
BufferedImage original = ImageIO.read(new File("large.png"));
BufferedImage resized = ImageUtil.resize(original, 1024, 0); // keep aspect ratio
ocrEngine.processImage(resized);
```

### 在 Web 服務中從圖像擷取文字

若將此功能以 REST 端點提供，請記得：

- 驗證上傳的檔案類型（僅接受 PNG/JPEG）。
- 在背景執行緒或非同步任務中執行 OCR，以免阻塞請求執行緒。
- 將文字以 JSON 格式回傳：

```json
{ "extractedText": "Hello world!\nПривет мир!" }
```

## 完整範例（結合所有步驟）

以下是完整程式碼，你可以直接複製貼上到 `MixedLanguageDemo.java` 檔案中。程式內含匯入語句、錯誤處理，以及說明每一行的註解。

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates automatic language detection with Aspose OCR for Java.
 * This example loads a PNG that contains both English and Russian text,
 * enables auto‑detect, and prints the extracted text.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable automatic language detection so the engine picks the right script(s)
        ocrEngine.setAutoDetectLanguage(true);

        // Path to the image – replace with your actual location
        String imagePath = "YOUR_DIRECTORY/mixed-eng-rus.png";

        // Process the image and obtain the result
        OcrResult ocrResult = ocrEngine.processImage(imagePath);

        // Output the recognized text – should contain both English and Russian lines
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

使用以下指令執行：

```bash
mvn compile exec:java -Dexec.mainClass=MixedLanguageDemo
```

若環境設定正確，主控台會先顯示英文行，接著顯示其俄文對應行。

## 重點回顧與後續步驟

我們已示範一個 **java ocr example**，**啟用自動語言偵測**、處理混合語言的 PNG，並 **從圖像檔案中擷取文字**，全程不需手動指定語言。以下為重點摘要：

1. 開啟 `setAutoDetectLanguage(true)`，讓 Aspose 處理多語言內容。
2. 使用 `processImage` 讀取任意 PNG（或 JPEG），再透過 `getText()` 取得乾淨的字串。
3. 同樣的流程也適用於 PDF、TIFF，甚至即時相機串流——只需更換輸入來源。

想更進一步？可嘗試以下想法：

- **批次處理：** 迭代資料夾中的 PNG，將每筆結果寫入資料庫。
- **語言特定後處理：** 偵測後，將英文文字送至拼寫檢查器，俄文文字送至音譯服務。
- **結合 AI：** 將擷取的文字輸入語言模型，以進行摘要或翻譯。

目前就說到這裡。若遇到任何問題——例如引擎未偵測到預期的語言——請再次確認圖像是否清晰，且使用的是最新的 Aspose OCR 版本。祝開發順利，盡情體驗 Java 專案中 **自動語言偵測** 的威力！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}