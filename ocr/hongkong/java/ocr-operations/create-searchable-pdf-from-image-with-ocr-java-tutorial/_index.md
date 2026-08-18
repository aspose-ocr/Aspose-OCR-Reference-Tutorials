---
category: general
date: 2026-01-07
description: 使用 Aspose OCR 於 Java 建立可搜尋的 PDF。了解如何將圖片轉換為 PDF、從圖片辨識文字以及從 JPG 產生 PDF。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- how to use ocr
- generate pdf from jpg
language: zh-hant
og_description: 使用 Aspose OCR（Java）將圖片轉換為可搜尋的 PDF。逐步指南教您如何將圖片轉為 PDF、辨識圖片文字，並從 JPG
  產生 PDF。
og_title: 從圖像建立可搜尋的 PDF – Java OCR 指南
tags:
- OCR
- Java
- PDF
- Aspose
title: 使用 OCR 從圖片建立可搜尋的 PDF – Java 教學
url: /zh-hant/java/ocr-operations/create-searchable-pdf-from-image-with-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 OCR 從圖像建立可搜尋 PDF – Java 教程

曾經需要 **建立可搜尋 PDF**，卻不知從何下手嗎？你並不孤單——許多開發者在第一次嘗試將 JPEG 轉換成可搜尋的 PDF 時，都會卡在這裡。

在本指南中，我們將一步步示範完整、可執行的範例，教你如何 **將圖像轉換為 PDF**、**從圖像辨識文字**，最後 **從 JPG 產生 PDF**，全部使用 Aspose OCR for Java。沒有模糊的參考，只有可以直接複製貼上並立即執行的程式碼。

## 需要的環境

在開始之前，請確保你的機器上已具備以下條件：

* **Java 17** 或更新版本（API 支援任何近期的 JDK）。  
* **Aspose.OCR for Java** 套件——可從 Maven Central 或 Aspose 官方網站取得最新 JAR。  
* 一張範例圖像，例如 `sample.jpg`，放在可供引用的資料夾內。  
* 你慣用的 IDE 或簡易文字編輯器加上終端機——隨你喜好。

就這些。沒有笨重的框架，也不需要額外的原生依賴。現在就開始吧。

## 第一步 – 建立可搜尋 PDF：初始化 OCR 引擎

首先，我們建立一個 `OcrEngine` 實例，並指向來源圖像。這個物件是 Aspose OCR 的核心，負責從載入位圖到輸出辨識文字的全部工作。

```java
import com.aspose.ocr.*;

public class HelloOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the image you want to turn into a searchable PDF
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **為什麼重要：** 正確初始化引擎可確保程式庫能讀取你提供的圖像格式。若路徑錯誤，會拋出 `FileNotFoundException`，整個流程就會中斷。

## 第二步 – 提升效能：啟用 GPU、多核心 CPU 與拼寫校正

OCR 在處理大型文件時相當耗費 CPU。Aspose 提供了多個參數讓你可以調整，以加快速度並提升準確度。

```java
        // 2️⃣ Turn on performance helpers – GPU, multi‑core CPU, and spell correction
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)                 // uses GPU if one is available
                 .setUseMultiCore(true)           // spreads work across CPU cores
                 .setEnableSpellCorrection(true); // cleans up common OCR mistakes
```

> **小技巧：** 若你的伺服器沒有 GPU，將 `setUseGpu(false)` 設為 false 不會有負面影響——程式會自動回退至多核心 CPU 處理。

## 第三步 – 改善圖像品質：校正傾斜與去除雜訊（可選但建議）

掃描件很少是完美的。輕微的傾斜或雜訊都可能影響辨識結果。`ImageProcessingOptions` 類別讓你在引擎讀取之前先清理圖像。

```java
        // 3️⃣ Pre‑process the image – straighten it and remove noise
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)   // automatically rotates tilted text
                 .setDespeckle(true); // reduces background speckles
```

> **邊緣情況：** 若來源圖像已經相當乾淨，你可以略過此步驟。雖然不會造成錯誤，但會多消耗幾毫秒的處理時間。

## 第四步 – 從圖像辨識文字並產生 PDF

現在魔法發生了。我們呼叫 `recognize()`，引擎會回傳 `OcrResult`。接著可以將結果儲存為多種格式——PDF 是最常見的可搜尋文件格式。

```java
        // 4️⃣ Perform OCR and get the result object
        OcrResult ocrResult = ocrEngine.recognize();

        // 5️⃣ Save the result as a searchable PDF (you could also choose TXT, DOCX, etc.)
        ocrResult.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);
    }
}
```

> **執行結果：** `sample-output.pdf` 會把原始圖像作為背景層，辨識出的文字則以隱形覆蓋層的形式放在上方。用 Adobe Reader 開啟並嘗試選取文字，你會感到驚喜。

## 第五步 – 驗證可搜尋 PDF 的產出

檔案寫入後，最好再次確認 PDF 真的是可搜尋的。

```java
import java.awt.Desktop;
import java.io.File;

public class VerifyPdf {
    public static void main(String[] args) throws Exception {
        File pdf = new File("YOUR_DIRECTORY/sample-output.pdf");
        if (pdf.exists() && Desktop.isDesktopSupported()) {
            Desktop.getDesktop().open(pdf); // opens the PDF in the default viewer
        } else {
            System.out.println("PDF not found or cannot be opened on this platform.");
        }
    }
}
```

開啟 PDF，按 **Ctrl F**，輸入圖像中確定出現的關鍵字——若搜尋成功，即表示你已成功 **create searchable pdf**！

## 真實情境下的 OCR 使用方式（加分篇）

* **批次處理：** 將程式碼包在迴圈中，對資料夾內的多張 JPG 逐一執行。記得重複使用同一個 `OcrEngine` 實例，以降低記憶體使用。  
* **語言支援：** Aspose OCR 支援超過 60 種語言。只要呼叫 `ocrEngine.getEngineOptions().setLanguage(Language.English);`（或其他列舉值）即可。  
* **錯誤處理：** 捕捉 `OcrException`，以優雅方式處理損毀的檔案。  

這些調整讓解決方案足以應付正式環境的工作流程。

## 完整 Java 範例 – 從 JPG 建立可搜尋 PDF

以下是完整、可直接編譯執行的程式。請將 `YOUR_DIRECTORY` 替換為你機器上的實際路徑。

```java
import com.aspose.ocr.*;

public class CreateSearchablePdf {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // -------------------------------------------------
        // 2️⃣ Performance helpers
        // -------------------------------------------------
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)
                 .setUseMultiCore(true)
                 .setEnableSpellCorrection(true);

        // -------------------------------------------------
        // 3️⃣ Image pre‑processing (optional but helpful)
        // -------------------------------------------------
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)
                 .setDespeckle(true);

        // -------------------------------------------------
        // 4️⃣ Run OCR and save as searchable PDF
        // -------------------------------------------------
        OcrResult result = ocrEngine.recognize();
        result.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);

        System.out.println("✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf");
    }
}
```

**預期輸出：**  

```
✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf
```

開啟產生的 PDF，應該能搜尋到 `sample.jpg` 中出現的任何文字。若看不到文字層，請再次確認圖像路徑，並確保 OCR 引擎沒有拋出隱藏的例外。

## 結論

我們剛剛示範了如何使用 Aspose OCR for Java **建立可搜尋 PDF**，從載入圖像、調整效能設定、清理圖像，到最終辨識文字並儲存為可搜尋的 PDF——每一步都說明了 *為什麼* 與 *如何*。

現在，你可以在自己的應用程式中 **convert image to PDF**、**recognize text from image**，以及 **generate PDF from JPG**。接下來可以嘗試批次處理整個掃描資料夾、實驗不同語言，或為輸出 PDF 加上密碼保護。可能性無限。

有關邊緣案例、授權或效能調校的問題嗎？歡迎在下方留言，祝開發順利！

![Diagram illustrating OCR pipeline – create searchable pdf](/images/ocr-pipeline.png "建立可搜尋 PDF 流程圖")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}