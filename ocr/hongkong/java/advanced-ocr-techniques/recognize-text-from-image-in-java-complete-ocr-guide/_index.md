---
category: general
date: 2026-08-12
description: 使用 Java OCR 引擎識別圖像中的文字。了解如何從圖像提取文字、提升 OCR 準確度，以及對 PNG 檔案進行 OCR 前的圖像預處理。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- how to extract text from image
- how to improve OCR accuracy
- how to preprocess image for OCR
- perform OCR on PNG
language: zh-hant
lastmod: 2026-08-12
og_description: 使用 Java 從圖像辨識文字。本教學示範如何從圖像提取文字、提升 OCR 準確度，並使用多執行緒與 GPU 在 PNG 圖檔上執行
  OCR。
og_image_alt: Diagram showing Java OCR engine recognizing text from image
og_title: 在 Java 中辨識圖片文字 – 步驟式 OCR 教學
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  headline: recognize text from image in Java – complete OCR guide
  type: TechArticle
- description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  name: recognize text from image in Java – complete OCR guide
  steps:
  - name: Explanation of each step
    text: '| Step | Why it matters | How it helps you **recognize text from image**
      | |------|----------------|-----------------------------------------------|
      | 1️⃣ Create the OCR engine | Instantiates the core component that drives all
      subsequent operations. | Provides the entry point for all OCR actions. | '
  - name: Expected output
    text: 'If `sample-image.png` contains the sentence “Hello, world! 123”, the console
      will display something similar to:'
  - name: 1. Binarization with Otsu’s method
    text: '```java import java.awt.image.BufferedImage; import com.example.image.Binarizer;
      // hypothetical helper class'
  - name: 2. Scaling to 300 dpi
    text: '```java import com.example.image.Resizer;'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: 在 Java 中從圖像識別文字 – 完整 OCR 指南
url: /zh-hant/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java 進行圖像文字辨識 – 完整 OCR 教學

如果你需要在 Java 應用程式中 **從圖像辨識文字**，本教學會一步步示範。完成本指南後，你將能夠從圖像檔案中擷取文字、提升 OCR 準確度，並在支援多核心與 GPU 的環境下對 PNG 資產執行 OCR。

許多開發者會好奇 **如何在不自行開發神經網路的情況下從圖像擷取文字**。解決方案是使用成熟的 OCR 引擎，為速度與準確度進行設定，並套用適當的前處理步驟。以下章節會逐一說明每個需求，讓你可以直接把程式碼複製到專案中。

## 你將學到

* 在 Java 中設定 OCR 引擎。  
* 啟用多執行緒與可選的 GPU 加速。  
* 為英文與西班牙文加入語言套件。  
* 套用影像前處理濾鏡以提升辨識品質。  
* 開啟內建拼字校正器，取得更乾淨的輸出。  
* 在 PNG 檔案上執行 OCR，並印出辨識結果。

不需要任何外部服務——全部在本機執行，適合離線或對隱私有高要求的應用。

## 前置條件

* Java 17 或更新版本（程式碼使用 `var` 語法，但可向下移植）。  
* 提供 `OcrEngine`、`Language` 與 `EngineOptions` 類別的 OCR 函式庫（例如 **GroupDocs.Parser**、**Aspose.OCR**，或任何相容的 SDK）。  
* Maven 或 Gradle 用於相依管理。  
* 一張範例 PNG 圖片（`sample-image.png`）放置於 `YOUR_DIRECTORY`。

> **專業提示：** 若你計畫處理上千張圖像，請為 GPU 緩衝區配置足夠的記憶體，且僅在需要原始 OCR 輸出時才關閉拼字校正器。

## 使用 Java OCR 引擎辨識圖像文字

以下是一個完整、可執行的 Java 程式，依照原始片段中的八個步驟撰寫。程式碼包含匯入、`main` 方法與說明每行用途的內嵌註解。

```java
// File: OcrDemo.java
import com.example.ocr.OcrEngine;            // Replace with your OCR library's package
import com.example.ocr.Language;
import com.example.ocr.EngineOptions;
import com.example.ocr.ImagePreprocessingOptions;

public class OcrDemo {

    public static void main(String[] args) {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable multi‑core processing for faster throughput
        ocrEngine.getEngineOptions().setUseMultiThreading(true);

        // Step 3: (Optional) Turn on GPU acceleration if a compatible GPU is present
        ocrEngine.getEngineOptions().setUseGpu(true);

        // Step 4: Add the languages you want to recognize (English and Spanish)
        ocrEngine.getLanguage().add(Language.English);
        ocrEngine.getLanguage().add(Language.Spanish);

        // Step 5: Apply common image‑preprocessing filters to improve OCR accuracy
        ImagePreprocessingOptions imgOpts = ocrEngine.getImagePreprocessingOptions();
        imgOpts.setRotate(true);   // Auto‑rotate based on EXIF orientation
        imgOpts.setDeskew(true);   // Straighten skewed text lines
        imgOpts.setDenoise(true);  // Reduce background noise

        // Step 6: Enable the built‑in spell corrector for cleaner output
        ocrEngine.getEngineOptions().setUseSpellCorrector(true);

        // Step 7: Perform OCR on the target PNG image
        // This demonstrates how to perform OCR on PNG files efficiently.
        String imagePath = "YOUR_DIRECTORY/sample-image.png";
        String ocrResult = ocrEngine.recognizeImage(imagePath);

        // Step 8: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(ocrResult);
    }
}
```

### 各步驟說明

| 步驟 | 為何重要 | 如何協助你 **從圖像辨識文字** |
|------|----------|--------------------------------|
| 1️⃣ 建立 OCR 引擎 | 實例化核心元件，驅動後續所有操作。 | 提供所有 OCR 動作的入口點。 |
| 2️⃣ 啟用多核心處理 | 現代 CPU 具多核心，利用它可縮短總處理時間。 | 在平行執行 **對 PNG 執行 OCR** 時加速批次工作。 |
| 3️⃣ 開啟 GPU 加速（可選） | GPU 在平行像素運算上表現優異，特別是大圖像。 | 在支援的硬體上可將辨識時間縮短最高 70 %。 |
| 4️⃣ 加入語言套件 | OCR 準確度取決於語言模型；僅指定需要的語言可減少誤判。 | 在多語言情境下 **如何從圖像擷取文字** 時，提高正確辨識的機率。 |
| 5️⃣ 影像前處理 | 旋轉、去斜與去噪可修正常見掃描問題。 | 透過向引擎提供更乾淨的位圖，直接 **如何提升 OCR 準確度**。 |
| 6️⃣ 拼字校正器 | 後處理步驟，修正常見的 OCR 拼寫錯誤。 | 產生更易讀的輸出，免除手動清理。 |
| 7️⃣ 在 PNG 上執行 OCR | `recognizeImage` 方法讀取檔案、套用前處理，並執行辨識管線。 | 示範 **對 PNG 執行 OCR** 同時處理格式特有的細節（如無損壓縮）。 |
| 8️⃣ 印出結果 | 立即回饋，驗證是否成功。 | 讓你確認文字是否已正確 **從圖像辨識**。 |

### 預期輸出

若 `sample-image.png` 內的句子為 “Hello, world! 123”，控制台會顯示類似以下內容：

```
=== OCR Result ===
Hello, world! 123
```

實際輸出可能因圖像品質與語言設定略有差異，但拼字校正器通常會修正諸如 “Helli” → “Hello” 的小錯誤。

## 如何為 OCR 前處理影像 – 深入探討

雖然上述程式碼使用引擎內建的前處理，你也可以在將影像交給 OCR 引擎前自行套用自訂濾鏡。以下列出兩種常見技術：

### 1. 使用 Otsu 方法二值化

```java
import java.awt.image.BufferedImage;
import com.example.image.Binarizer; // hypothetical helper class

BufferedImage original = ImageIO.read(new File(imagePath));
BufferedImage binary = Binarizer.otsuThreshold(original);
ocrEngine.recognizeImage(binary);
```

二值化將影像轉為黑白，常能 **如何提升 OCR 準確度**，特別是低對比度的掃描件。

### 2. 縮放至 300 dpi

```java
import com.example.image.Resizer;

BufferedImage scaled = Resizer.scaleToDPI(original, 300);
ocrEngine.recognizeImage(scaled);
```

大多數 OCR 引擎要求至少 300 dpi 才能達到最佳字元辨識。縮放可防止引擎誤讀過小的字形。

> **注意：** 若同時啟用自訂前處理與引擎內建選項，引擎會在你的處理之後再套用自己的濾鏡。請依影像特性選擇最適合的順序。

## 如何從圖像擷取文字 – 處理邊緣案例

| 情境 | 推薦調整 |
|------|----------|
| **背景噪點過多** | 提升 `setDenoise(true)` 強度，或在 OCR 前先執行中值濾鏡。 |
| **傾斜角度 > 15°** | 同時使用 `setDeskew(true)`，並透過 `imgOpts.setRotateAngle(θ)` 手動設定旋轉角度。 |
| **混合語言（例如英文 + 西班牙文）** | 如步驟 4 所示加入兩套語言包；引擎會自動切換語境。 |
| **大型 PDF 轉 PNG** | 將每頁另存為 PNG，分別處理後再彙總結果；多執行緒（步驟 2）可保持總耗時低。 |
| **GPU 不可用** | 保持 `setUseGpu(true)`，但以 try‑catch 包住；若無法使用 GPU，引擎會自動回退至 CPU，且不會崩潰。 |

## 在 PNG 上執行 OCR – 批次處理範例

當需要在目錄內的多個 **對 PNG 執行 OCR** 時，只要使用同一個引擎實例的簡單迴圈即可：

```java
Path dir = Paths.get("YOUR_DIRECTORY");
try (Stream<Path> files = Files.list(dir)) {
    files.filter(p -> p.toString().endsWith(".png"))
         .forEach(p -> {
             String text = ocrEngine.recognizeImage(p.toString());
             System.out.println("File: " + p.getFileName());
             System.out.println(text);
             System.out.println("---");
         });
}
```

因為引擎已配置多核心與 GPU，此迴圈能在不額外撰寫程式碼的情況下，同時平行處理數十張影像。

## 完整可執行範例

將所有內容整合後，以下是一個可直接貼到 IDE、加入相應 Maven 相依後立即執行的自包含類別：



## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化你所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}