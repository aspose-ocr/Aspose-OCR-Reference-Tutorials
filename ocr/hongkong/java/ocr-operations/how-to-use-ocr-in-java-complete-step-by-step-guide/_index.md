---
category: general
date: 2026-02-22
description: 如何在 Java 中使用 OCR 從圖像提取文字、提升 OCR 準確度，並載入圖像進行 OCR，附實用程式碼範例。
draft: false
keywords:
- how to use OCR
- extract text from image
- improve OCR accuracy
- load image for OCR
- OCR preprocessing
language: zh-hant
og_description: 如何在 Java 中使用 OCR 從圖像提取文字並提升 OCR 準確度。請跟隨本指南，獲得可直接執行的範例。
og_title: 在 Java 中使用 OCR 的完整逐步指南
tags:
- OCR
- Java
- Image Processing
title: 在 Java 中使用 OCR 的完整逐步指南
url: /zh-hant/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 OCR – 完整逐步指南

有沒有曾經需要在模糊的螢幕截圖上 **how to use OCR**，卻發現輸出像是亂碼？你並不是唯一遇到這種情況的人。在許多實際應用中——掃描收據、數位化表單或從 meme 中提取文字——取得可靠結果取決於幾個簡單的設定。

在本教學中，我們將逐步說明 **how to use OCR** 以 *extract text from image* 檔案，展示如何 **improve OCR accuracy**，以及示範使用流行的 Java OCR 函式庫正確的 **load image for OCR** 方法。完成後，你將擁有一個可直接嵌入任何專案的獨立程式。

## 你將學到

- 你需要的 **load image for OCR** 完整程式碼（無隱藏相依性）。
- 哪些前處理旗標能提升 **improve OCR accuracy** 以及它們的重要性。
- 如何讀取 OCR 結果並將其印到主控台。
- 常見陷阱——例如忘記設定感興趣區域（ROI）或忽略降噪——以及如何避免。

### 前置條件

- Java 17 或更新版本（程式碼可在任何近期 JDK 上編譯）。
- 提供 `OcrEngine`、`ImagePreprocessingOptions`、`OcrInput` 與 `OcrResult` 類別的 OCR 函式庫（例如本範例中使用的虛構 `com.example.ocr` 套件）。請改為使用你實際使用的函式庫。
- 一張範例圖片（`skewed_noisy.png`），放置於可參考的資料夾中。

> **專業提示：** 若你使用商業 SDK，請確保授權檔案已放在 classpath 上；否則引擎會拋出初始化錯誤。

---

## 步驟 1：建立 OCR 引擎實例 – **how to use OCR** 有效運用

首先，你需要一個 `OcrEngine` 物件。可以把它想像成解讀像素的“大腦”。

```java
// Step 1: Initialize the OCR engine
import com.example.ocr.OcrEngine;

OcrEngine ocrEngine = new OcrEngine();
```

*為什麼這很重要：* 沒有引擎，你就缺乏語言模型、字元集或影像啟發式的上下文。提前實例化也能讓你之後附加前處理選項。

---

## 步驟 2：設定影像前處理 – **improve OCR accuracy**

前處理是將雜訊掃描轉換為乾淨、機器可讀文字的祕密調味料。以下我們會啟用去斜、較高階的降噪、自動對比度，以及感興趣區域（ROI）以聚焦於圖片的相關部分。

```java
import com.example.ocr.ImagePreprocessingOptions;
import java.awt.Rectangle;

// Step 2: Set up preprocessing to improve OCR accuracy
ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
preprocessing.setDeskewEnabled(true); // Correct image rotation
preprocessing.setNoiseReductionLevel(
        ImagePreprocessingOptions.NoiseReduction.HIGH); // Reduce speckles
preprocessing.setAutoContrastEnabled(true); // Boost contrast
preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600)); // Process a sub‑region only

ocrEngine.setPreprocessingOptions(preprocessing);
```

*為什麼這很重要：*  
- **Deskew** 使旋轉的文字校正，對於掃描未完全平整的收據尤為重要。  
- **Noise reduction** 移除會被誤判為字元的雜散像素。  
- **Auto‑contrast** 擴展色調範圍，使淡弱的字母更突出。  
- **ROI** 告訴引擎忽略不相關的邊框，節省時間與記憶體。

如果省略其中任何一項，**improve OCR accuracy** 的結果很可能會下降。

---

## 步驟 3：載入影像以供 OCR – 正確 **load image for OCR**

現在我們實際將引擎指向要讀取的檔案。`OcrInput` 類別可以接受多張影像，但在此範例中我們保持簡單。

```java
import com.example.ocr.OcrInput;

// Step 3: Load the image you want to extract text from
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png"); // replace with your real path
```

*為什麼這很重要：* 路徑必須是絕對路徑或相對於工作目錄的路徑；否則引擎會拋出 `FileNotFoundException`。另外，請注意 `add` 方法名稱暗示你可以排隊多張影像——對批次處理非常方便。

---

## 步驟 4：執行 OCR 並輸出辨識文字 – **how to use OCR** 全流程

最後，我們請求引擎辨識文字並印出。`OcrResult` 物件包含原始字串、信心分數，以及逐行的中繼資料（若你之後需要的話）。

```java
import com.example.ocr.OcrResult;

// Step 4: Run OCR and print the extracted text
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**預期輸出**（假設範例圖片包含 “Hello, OCR World!”）：

```
=== OCR Output ===
Hello, OCR World!
```

如果結果看起來是亂碼，請回到步驟 2 並調整前處理選項——或許降低降噪等級或調整 ROI 矩形。

---

## 完整、可執行範例

以下是一個完整的 Java 程式，你可以直接複製貼上至名為 `OcrDemo.java` 的檔案中。它將我們討論的每一步結合起來。

```java
// OcrDemo.java – A complete, runnable example showing how to use OCR in Java
import com.example.ocr.OcrEngine;
import com.example.ocr.ImagePreprocessingOptions;
import com.example.ocr.OcrInput;
import com.example.ocr.OcrResult;
import java.awt.Rectangle;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (this is the key to improve OCR accuracy)
        ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
        preprocessing.setDeskewEnabled(true);
        preprocessing.setNoiseReductionLevel(
                ImagePreprocessingOptions.NoiseReduction.HIGH);
        preprocessing.setAutoContrastEnabled(true);
        preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600));
        ocrEngine.setPreprocessingOptions(preprocessing);

        // 3️⃣ Load the image you want to extract text from
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace the path with your own image location
        ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run the OCR engine and print the result
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

儲存檔案後，使用 `javac OcrDemo.java` 編譯，然後執行 `java OcrDemo`。若一切設定正確，你將在主控台看到提取的文字。

---

## 常見問題與邊緣情況

| 問題 | 答案 |
|----------|--------|
| **如果我的圖片是 JPEG 格式呢？** | `OcrInput.add()` 方法接受任何支援的點陣圖格式——PNG、JPEG、BMP、TIFF。只需在路徑中更改檔案副檔名即可。 |
| **我可以一次處理多頁嗎？** | 當然可以。對每個檔案呼叫 `ocrInput.add()`，然後將相同的 `ocrInput` 傳給 `recognize()`。引擎會回傳合併的 `OcrResult`。 |
| **如果 OCR 結果是空的怎麼辦？** | 再次確認 ROI 確實包含文字。也要確保已開啟 `setDeskewEnabled(true)`；90° 旋轉會讓引擎認為影像是空白的。 |
| **如何更換語言模型？** | 大多數函式庫在 `OcrEngine` 上提供 `setLanguage(String)` 方法。於 `recognize()` 之前呼叫，例如 `ocrEngine.setLanguage("eng")`。 |
| **有沒有辦法取得信心分數？** | 有，`OcrResult` 通常提供每行或每字元的 `getConfidence()`。可用來過濾低信心的結果。 |

---

## 結論

我們已完整說明在 Java 中 **how to use OCR** 的全流程：建立引擎、設定前處理以 **improve OCR accuracy**、正確 **load image for OCR**，最後印出提取的文字。完整程式碼已可直接執行，說明則解答了每行程式背後的「為什麼」。

準備好進一步嗎？試著更換 ROI 矩形以聚焦於影像的不同區域、實驗 `NoiseReduction.MEDIUM`，或將輸出整合至可搜尋的 PDF。你也可以探索相關主題，例如使用雲端服務 **extract text from image**，或以多執行緒佇列批次處理數千個檔案。

對 OCR、影像前處理或 Java 整合還有其他問題嗎？留下評論吧，祝開發愉快！

![如何使用 OCR 範例](/images/ocr-demo.png "如何使用 OCR – Java 範例展示前處理與結果")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}