---
category: general
date: 2026-07-05
description: 使用 Java 在將 PNG 轉 PDF 時壓縮 PDF 圖像。學習 OCR 的影像前處理、辨識 JPG 文字，並在同一教學中完成批次 OCR
  轉 PDF。
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: zh-hant
og_description: 壓縮 PDF 圖像並使用 Java 將 PNG 轉換為 PDF。本指南涵蓋 OCR 的圖像前處理、辨識文字 JPG，以及批次 OCR
  轉 PDF。
og_title: 使用 Java 壓縮 PDF 圖片 – 完整批次 OCR 教學
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: 使用 Java 壓縮 PDF 圖像 – 完整批次 OCR 轉 PDF 指南
url: /zh-hant/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java 壓縮 PDF 圖像 – 完整批次 OCR 轉 PDF 指南

有沒有過需要 **壓縮 PDF 圖像** 同時把一整個 PNG 資料夾轉成可搜尋 PDF 的時候？你並不是唯一遇到這個問題的人。在許多自動化流程中，最大的痛點往往是同時兼顧影像品質、OCR 正確率與最終 PDF 檔案大小。

在本教學中，我們將示範一套實用解決方案，能 **將 PNG 轉成 PDF**、套用 **OCR 前置影像處理**，最後 **壓縮 PDF 圖像**，讓輸出檔案保持輕量。完成後，你將會知道如何 **辨識文字 JPG** 檔案、建立 **批次 OCR 轉 PDF** 工作流程，並讓 PDF 保持整潔。

## 你將學會

- 為 Java 設定 Aspose OCR 並套用授權
- 為引擎配置多執行緒、GPU 加速與拼寫校正
- 建立可重用的 **OCR 前置影像處理** 流程（去噪、對比、二值化）
- 使用 **PdfSaveOptions** 來 **壓縮 PDF 圖像** 而不犧牲可讀性
- 以迴圈方式 **將 PNG 轉成 PDF** 並批量 **辨識文字 JPG**
- 完整、可直接執行的 Java 程式碼範例，隨時可放入任何專案

> **先決條件**：Java 8 以上、Maven 或 Gradle、Aspose OCR for Java 授權檔，以及一個要處理的 PNG/JPG 圖片資料夾。

---

## Step 1: 套用 Aspose OCR 授權（正式環境必備）

在呼叫任何 OCR API 之前，必須先載入有效的授權；否則只能使用試用版的限制功能。

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*為什麼這很重要*：取得授權後，引擎即可啟用 GPU 支援、更高的辨識準確度，並移除會讓 PDF 檔案變大的浮水印。

---

## Step 2: 設定 OCR 引擎 – 執行緒、GPU 與拼寫校正

快速的 OCR 引擎是任何 **批次 OCR 轉 PDF** 工作的核心。我們會依主機 CPU 可用的核心數量啟動多執行緒，若有相容的顯示卡則開啟 GPU 加速，並加強拼寫校正以減少 OCR 錯誤。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*小技巧*：若在沒有 GPU 的無頭伺服器上執行，只要將 `gpu.setEnabled(false)` 設為 false，即可正常運作，只是速度會稍慢一些。

---

## Step 3: 建立影像前置處理流程

原始掃描檔常會有噪點、低對比或光線不均等問題。**OCR 前置影像處理** 能顯著提升辨識率，特別是在 **辨識文字 JPG** 的情境下。

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*為什麼要這樣串接*：先去噪可以避免二值化時放大雜訊；接著調整對比讓字元更突出；最後的二值化則提供 OCR 引擎乾淨的二元影像。

---

## Step 4: 設定 PDF 儲存選項 – 高效 **壓縮 PDF 圖像**

Aspose 允許細部調整 PDF 輸出。我們會開啟影像壓縮，並設定一個在檔案大小與可讀性之間取得平衡的品質等級。

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*結果*：每個可搜尋的 PDF 都會明顯變小，非常適合歸檔或以電子郵件傳送。

---

## Step 5: 處理資料夾 – 在同一迴圈中 **將 PNG 轉成 PDF** 並 **辨識文字 JPG**

現在把所有步驟整合起來。迴圈會遍歷輸入目錄，對每個 PNG 或 JPG 執行 OCR，並將可搜尋的 PDF 寫入輸出資料夾。PDF 檔名會與原始影像檔名保持一致。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### 預期輸出

執行程式時會為每張影像印出一行訊息，例如：

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

打開任一產生的 PDF，你會看到可選取、可搜尋的文字，同時檔案大小通常比未壓縮的版本小 **30‑50 %**。

---

## 常見問題與特殊情境

### 我的伺服器沒有 GPU 該怎麼辦？
只要將 `gpuSettings.setEnabled(false)` 即可。其餘流程不變，仍會使用多執行緒的 CPU 處理。

### PDF 檔案仍然太大，我可以再降低品質嗎？
可以。調整 `options.setImageQuality(70)`，甚至 `50`。數值越低檔案越小，但細小字形可能會變得模糊，建議先用樣本測試。

### 如何支援其他影像格式（TIFF、BMP）？
在過濾 lambda 中加入相應的副檔名：

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

相同的前置處理流程可適用於大多數點陣圖格式。

### 想保留原始彩色影像而不是二值化，該怎麼做？
在前置處理建構子中將 `.addBinarize()` 改成 `.addGrayscale()`，即可保留彩色資訊供後續分析使用。

---

## 生產環境批次 OCR 的進階技巧

- **記憶體管理**：如範例所示，重複使用單一 `OcrEngine` 實例，避免每張影像都建立/銷毀物件的開銷。
- **錯誤處理**：將每個檔案的處理區塊包在 `try/catch`，記錄失敗但不會中斷整批作業。
- **日誌記錄**：使用正式的日誌框架（SLF4J、Log4j）取代 `System.out.println`，以因應規模化需求。
- **平行處理**：資料量極大時，可考慮以平行串流處理子目錄，但需留意 GPU 資源的競爭情形。
- **安全性**：將授權檔放在版本庫之外，並以檔案系統權限加以保護。

---

## 結論

我們已示範如何在執行 **批次 OCR 轉 PDF** 時 **壓縮 PDF 圖像**，同時完成 **將 PNG 轉成 PDF**、**辨識文字 JPG**，並套用穩健的 **OCR 前置影像處理** 流程。完整的 Java 程式碼自包含、可在任何現代 JDK 上執行，產出輕量的可搜尋 PDF，適合歸檔或後續分析。

接下來可以嘗試調整前置處理參數、測試非英語的 OCR 語言，或將工作流程整合到監控資料夾、即時處理檔案的 Spring Boot 微服務中。授權載入、引擎設定、前置處理與 PDF 壓縮這幾個核心概念不會改變，為任何 OCR 驅動的專案奠定堅實基礎。

有任何問題或想分享自己的調整嗎？歡迎在下方留言，祝開發順利！

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")

## 接下來可以學什麼？

以下教學與本指南的技術緊密相關，提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能或探索其他實作方式。

- [辨識 PDF 文字 – 使用 Aspose.OCR for Java 的 OCR 操作](/ocr/english/java/ocr-operations/)
- [使用 Aspose OCR 辨識文字影像 – 完整 Java OCR 教學](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [使用 Aspose.OCR BufferedImage 在 Java 中將影像轉成文字](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}