---
category: general
date: 2026-03-28
description: 在 Java 中使用 Aspose OCR 進行圖片文字辨識。了解如何從 PNG 讀取文字，並透過內建拼寫校正提升 OCR 準確度。
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- read image text
- improve OCR accuracy
- Aspose OCR Java
- spell correction OCR
language: zh-hant
og_description: 使用 Aspose OCR for Java 在圖像上執行 OCR。本指南說明如何從 PNG 識別文字，並在數分鐘內提升 OCR 準確度。
og_title: 使用 Java 進行圖像 OCR – 完整指南
tags:
- OCR
- Java
- Aspose
- Image Processing
title: 使用 Java 進行圖像 OCR – 從 PNG 識別文字
url: /zh-hant/java/advanced-ocr-techniques/perform-ocr-on-image-with-java-recognize-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java 執行 OCR 於影像 – 從 PNG 識別文字

是否曾需要 **對影像執行 OCR**，卻總是得到雜亂的結果？你並不孤單——噪點掃描、低對比度 PNG、以及奇怪的字型，都會把本來清晰的文件變成一堆亂碼。

在本指南中，我們將一步步示範一個完整、可直接執行的 Java 範例，使用 Aspose OCR **從 PNG 識別文字**，同時說明如何透過函式庫的拼寫校正功能 **提升 OCR 準確度**。完成後，你就能在來源不完美的情況下，可靠地 **讀取影像文字**。

## 你將學會

- 如何在 Maven 專案中設定 Aspose OCR for Java。  
- 從載入檔案到擷取乾淨文字的完整 **對影像執行 OCR** 步驟。  
- 為何啟用拼寫校正能顯著提升輸出品質。  
- 常見陷阱（檔案遺失、不支援格式）以及如何優雅地處理。  
- 一段可直接複製貼上的完整程式碼範例，今天就能執行。

### 前置條件

- 已在機器上安裝 Java 8 或更新版本。  
- 具備 Maven 以管理相依性（任何支援 Maven 的 IDE 都可）。  
- 一張包含可讀文字的 PNG 影像——最好是有點噪點的，這樣才能看到拼寫校正的效果。

> **小技巧：** 若手邊沒有 PNG，隨便截取一張文件的螢幕截圖或招牌照片都行。噪點越多，你就越能體會準確度的提升。

---

## 步驟 1：加入 Aspose OCR 相依性

首先，將 Aspose OCR 函式庫加入 `pom.xml`。這一行會自動抓取最新版本（截至 2026 年 3 月）以及所有傳遞相依性。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

> **為什麼重要：** 沒有此函式庫就無法建立 `OcrEngine`，整個 **對影像執行 OCR** 流程在執行時會直接失敗。

---

## 步驟 2：初始化 OCR 引擎

建立引擎相當簡單，但將初始化與辨識呼叫分開有其微妙原因：這讓你可以在此調整語言、DPI，或最重要的拼寫校正設定。

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {

    public static void main(String[] args) {
        try {
            // Step 2: Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Pro tip: you can set the language here if you need something other than English
            // ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

請留意註解——當 PNG 含有非英文字符時，設定語言能大幅提升辨識成功率。  

---

## 步驟 3：啟用拼寫校正以 **提升 OCR 準確度**

Aspose OCR 內建拼寫校正模組，像是輕量字典。只要一行程式碼即可開啟，對最終輸出影響巨大，尤其是對噪點影像。

```java
            // Step 3: Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);
```

> **如果不需要呢？** 只要把旗標設為 `false` 即可。對於特定領域的文字，字典可能會把合法詞彙誤判為錯誤，此時關閉校正較為合適。

---

## 步驟 4：載入並辨識 PNG

現在我們真正 **讀取影像文字**。`recognizeImage` 方法接受路徑字串，也可以傳入 `java.io.InputStream`，方便從資料庫或網路取得影像。

```java
            // Step 4: Perform OCR on the input image
            String imagePath = "YOUR_DIRECTORY/noisy-image.png"; // replace with your actual path
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

若找不到檔案，Aspose 會拋出具說明性的例外——不必自行檢查 `File.exists()`。不過，像我們這樣把呼叫包在 `try/catch` 中，仍能為最終使用者提供友善的錯誤訊息。

---

## 步驟 5：輸出校正後的文字

最後，將結果印到主控台。實務上你可能會寫入資料庫或傳給下游服務，但主控台足以作為快速示範。

```java
            // Step 5: Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

**預期輸出**（假設 PNG 含有「Aspose OCR library」且有噪點）：

```
Corrected text:
Aspose OCR library
```

若關閉拼寫校正，可能會看到類似 “Asp0se OCR libr@ry” 的結果——這正說明 **提升 OCR 準確度** 為何重要。

---

## 步驟 6：驗證結果 – 是否真的 **讀取影像文字**？

盲目相信主控台輸出很危險，簡單的驗證可以為你省下大量時間。以下提供幾種驗證方式：

1. **長度檢查** – 比對 `ocrResult.getText().length()` 與預期字元數。  
2. **關鍵字搜尋** – 使用 `String.contains("Aspose")` 確認關鍵詞是否出現。  
3. **單元測試** – 若將此功能整合至更大系統，寫一個 JUnit 測試，斷言輸出與已知正確值相符。

```java
// Example sanity check
if (ocrResult.getText().contains("Aspose")) {
    System.out.println("✅ Text successfully read from image.");
} else {
    System.out.println("⚠️ Unexpected OCR result – consider tweaking settings.");
}
```

---

## 常見邊緣案例與處理方式

| 情況 | 為何發生 | 快速解決方案 |
|-----------|----------------|-----------|
| **找不到檔案** | 路徑錯誤或權限不足 | 在呼叫 `recognizeImage` 前，先檢查 `imagePath` 並使用 `Files.isReadable(Paths.get(imagePath))`。 |
| **不支援的格式** | Aspose OCR 支援 PNG、JPEG、BMP、TIFF 等 | 先使用 ImageIO 轉成 PNG，或改用 `ocrEngine.recognizeImage(InputStream)`。 |
| **DPI 極低** | OCR 引擎需要至少約 300 DPI 才能有不錯的準確度 | 使用 `BufferedImage` 搭配 `Graphics2D` 先將影像放大，再送入引擎。 |
| **領域專屬術語** | 拼寫校正可能把正確詞彙換成字典詞 | 關閉拼寫校正 (`setEnableSpellCorrection(false)`) 或透過 `ocrEngine.getRecognitionSettings().setCustomDictionary(...)` 提供自訂字典。 |

---

## 完整可執行範例（直接複製貼上）

以下為完整的來源檔案，已備妥可編譯執行。請將 `YOUR_DIRECTORY/noisy-image.png` 替換為實際測試影像的路徑。

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {
    public static void main(String[] args) {
        try {
            // Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);

            // Path to the PNG you want to process
            String imagePath = "YOUR_DIRECTORY/noisy-image.png";

            // Perform OCR on the input image
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

            // Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());

            // Simple verification that we actually read image text
            if (ocrResult.getText().toLowerCase().contains("aspose")) {
                System.out.println("✅ OCR succeeded – key term found.");
            } else {
                System.out.println("⚠️ OCR may need tweaking – key term missing.");
            }
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

執行方式：

```bash
mvn compile exec:java -Dexec.mainClass=SpellCorrectExample
```

執行後應會在主控台印出 **校正後的文字**，證明你已成功 **對影像執行 OCR**。

---

## 視覺摘要

![Perform OCR on image example](/images/ocr-example.png){alt="執行 OCR 圖像示例 – 文字校正前後"}

左側為噪點 PNG，右側則為經過拼寫校正後的乾淨文字輸出。

---

## 結論

我們剛剛完整走過如何使用 Aspose OCR for Java **對影像執行 OCR** 的端對端解決方案。只要啟用內建的拼寫校正旗標，即可 **提升 OCR 準確度**，讓即使來源不完美的影像也能得到可靠的文字內容。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}