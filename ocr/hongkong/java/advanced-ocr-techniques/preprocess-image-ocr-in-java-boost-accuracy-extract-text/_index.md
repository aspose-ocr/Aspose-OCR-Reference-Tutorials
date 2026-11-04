---
category: general
date: 2026-01-07
description: 預處理圖像 OCR 以提升 OCR 準確度，並使用 Aspose OCR 提取文字圖像 – 開發者逐步指南。
draft: false
keywords:
- preprocess image OCR
- extract text image
- improve OCR accuracy
- how to preprocess OCR
language: zh-hant
og_description: 圖像 OCR 前處理以提升 OCR 準確度，並使用 Aspose OCR 提取文字圖像。完整的 Java 教學與程式碼。
og_title: 在 Java 中預處理圖像 OCR — 提升準確度
tags:
- OCR
- Java
- Image Processing
title: 在 Java 中預處理影像 OCR – 提升準確度並提取文字
url: /zh-hant/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中預處理圖像 OCR – 完整指南

是否曾因 **preprocess image OCR** 而苦惱，因為你的掃描檔看起來像是一堆斑點與傾斜的文字？你並不孤單。大多數開發者在原始圖像雜訊太多、傾斜或對比度低時，會卡住，OCR 引擎會輸出亂碼而非預期的句子。  

好消息是，只要進行幾個前處理步驟，就能顯著 **improve OCR accuracy**，將模糊的快照轉換為乾淨、機器可讀的文字。在本教學中，我們將逐步說明如何使用 Aspose OCR for Java **how to preprocess OCR**，並且讓你看到如何可靠地 **extract text image** 內容。  

我們將涵蓋你所需的一切：必備函式庫、逐步程式碼、每個選項的重要性說明，以及可能遇到的邊緣案例提示。完成後，你將擁有一個可直接執行的程式，能處理雜訊 JPEG、進行清理，並將提取的文字印到主控台。

## 需要的條件

- 已安裝 Java Development Kit (JDK) 8 或更新版本。
- 使用 Maven 或 Gradle 來管理相依性（我們將示範 Maven 片段）。
- 取得 Aspose OCR for Java 授權（免費試用版可用於測試）。
- 準備一張範例圖像，例如 `skewed-noisy.jpg`，放置於已知目錄下。

就這樣——不需要額外的影像處理函式庫，因為 Aspose OCR 已內建前處理功能。

## 步驟 1：在專案中設定 Aspose OCR

首先，將 Aspose OCR 相依性加入你的 `pom.xml`。這會下載核心引擎以及稍後會用到的影像處理輔助工具。

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- use the latest version available -->
</dependency>
```

如果你偏好使用 Gradle，等價的設定如下：

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **專業提示：** 請保持相依性為最新版本；較新版通常包含更智慧的去傾斜演算法，進一步 **improve OCR accuracy**。

## 前處理圖像 OCR – 步驟 2：載入圖像

現在函式庫已就緒，我們可以建立 `OcrEngine` 實例，並指向要清理的圖像。

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to preprocess
        // Replace "YOUR_DIRECTORY" with the actual folder path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/skewed-noisy.jpg"));
```

為什麼要先實例化引擎？Aspose OCR 將前處理管線直接綁定於引擎，因此之後設定的任何選項都會作用於同一圖像串流。這可確保 **extract text image** 操作在已清理的版本上執行，而非原始檔案。

## 提升 OCR 準確度 – 步驟 3：設定前處理選項

魔法發生在 `ImageProcessingOptions` 中。每個旗標皆針對常見的影響 OCR 效能的缺陷。

```java
        // Step 3: Configure image preprocessing options
        ImageProcessingOptions processingOptions = ocrEngine.getImageProcessingOptions();

        // Straighten rotated text – essential for skewed scans
        processingOptions.setDeskew(true);

        // Remove isolated pixels that look like speckles
        processingOptions.setDespeckle(true);

        // Boost contrast by 30% – helps low‑contrast prints
        processingOptions.setContrastBoost(1.3f);
```

- **Deskew**：偵測旋轉角度並將圖像旋回水平。若未執行此步驟，OCR 引擎可能會誤判字元。
- **Despeckle**：清除可能被誤認為標點或雜散字母的隨機雜訊。
- **Contrast Boost**：提升前景（文字）與背景之間的差異，這是 **how to preprocess OCR** 在淡印文字時的關鍵因素。

可根據來源素材自行開關這些旗標。例如，完美掃描的文件可能不需要 `setDespeckle(true)`，即可節省數毫秒的處理時間。

## 提取文字圖像 – 步驟 4：對前處理後的圖像執行 OCR

圖像清理完成後，我們最終請求 Aspose OCR 辨識文字。

```java
        // Step 4: Run OCR on the preprocessed image
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

`recognize()` 內部會套用我們先前設定的前處理管線，接著執行字元分割與辨識。結果是一段純文字字串，可供後續流程使用——搜尋索引、資料輸入自動化，隨你需求。

## 如何前處理 OCR – 常見陷阱與邊緣案例

### 1. 圖像尺寸很重要
非常大的圖像（例如 > 5 MP）可能導致記憶體壓力。若遭遇 `OutOfMemoryError`，請先使用 `processingOptions.setResizeFactor(0.5f)` 重新調整圖像大小。

### 2. 彩色與灰階
Aspose OCR 在灰階圖像上表現最佳。若來源為彩色，請在去傾斜前啟用 `processingOptions.setConvertToGrayscale(true)`。

### 3. 多頁 PDF
處理 PDF 時，請先將每頁提取為圖像，然後在迴圈中套用相同的管線。API 提供 `PdfImageExtractor` 以完成此工作。

### 4. 語言支援
若文字不是英文，請明確設定語言：

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

若省略此步驟，可能會降低 **improve OCR accuracy**，因為引擎會自行猜測字元集。

## 完整可執行範例（即貼即用）

以下為完整程式碼，已可直接編譯執行。請將佔位路徑替換為實際圖像位置。

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image to be processed
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/skewed-noisy.jpg"));

        // Step 3: Configure image preprocessing options
        ImageProcessingOptions processingOptions = ocrEngine.getImageProcessingOptions();
        processingOptions.setDeskew(true);          // straighten rotated text
        processingOptions.setDespeckle(true);      // remove isolated pixels
        processingOptions.setContrastBoost(1.3f);   // boost contrast by 30%
        // Optional: processingOptions.setConvertToGrayscale(true);

        // Step 4: Run OCR on the preprocessed image
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**預期輸出**（為簡潔起見已截斷）：

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
```

若看到亂碼，請再次確認圖像路徑正確，且前處理旗標與圖像狀況相符。

## 視覺摘要

<img src="preprocess-ocr.png" alt="圖像 OCR 前處理示範" style="max-width:100%;">

此圖示說明流程：**Load → Deskew → Despeckle → Contrast Boost → Recognize → Extract Text**。每個區塊皆對應上方的程式碼片段。

## 結論

我們剛剛示範了在 Java 中使用 Aspose OCR **preprocess image OCR** 的實用方法，涵蓋從專案設定到微調選項，這些選項可 **improve OCR accuracy**。透過套用去傾斜、去雜訊與對比度提升，你可以將雜訊且傾斜的 JPEG 轉換為乾淨、可搜尋的文字——這正是你在想要 **extract text image** 用於下游應用時所需要的。  

接下來可以做什麼？試著探索其他前處理功能，例如針對二值圖像的 `setBinarizationThreshold`，或將多張圖像串接成單一批次作業。你也可以將結果與 Apache Tika 結合以進行索引，或輸入語言模型進行情感分析。只要掌握了 **how to preprocess OCR** 的基礎，便可無限發揮。  

對特定檔案類型或語言有疑問嗎？在下方留言，我們會回覆。祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}