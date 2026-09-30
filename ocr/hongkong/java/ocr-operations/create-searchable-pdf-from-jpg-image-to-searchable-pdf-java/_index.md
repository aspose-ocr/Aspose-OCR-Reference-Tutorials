---
category: general
date: 2026-02-19
description: 使用 Aspose OCR 在 Java 中將 JPG 圖像製作成可搜尋的 PDF。將 JPG 轉換為 PDF，並快速辨識圖像中的文字。
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- recognize text from image
- extract text from jpg
- convert jpg to pdf
language: zh-hant
og_description: 使用 Aspose OCR 從 JPG 圖像建立可搜尋的 PDF。了解如何在 Java 中將 JPG 轉換為 PDF 並辨識圖像文字。
og_title: 從 JPG 建立可搜尋的 PDF – Java OCR 教學
tags:
- aspose-ocr
- java
- pdf
- ocr
title: 從 JPG 建立可搜尋 PDF – 圖像轉可搜尋 PDF Java 指南
url: /zh-hant/java/ocr-operations/create-searchable-pdf-from-jpg-image-to-searchable-pdf-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 JPG 建立可搜尋 PDF – 圖像轉可搜尋 PDF Java 指南

是否曾需要從掃描圖片 **create searchable PDF**，卻不知從何開始？你並非唯一遇到此問題的人——許多開發者在面對需要可搜尋的 JPG 時都會卡關。好消息是，使用 Aspose OCR for Java，你只需幾行程式碼即可將該圖像轉換為完整的可搜尋 PDF。

在本教學中，我們將逐步說明整個流程：載入 JPG、辨識文字，並將結果儲存為可搜尋的 PDF。完成後，你將了解如何 **convert jpg to pdf**、如何 **extract text from jpg**，以及為何此方法通常比在 PDF 產生後再進行 OCR 更可靠。

## 需要的環境

* **Java Development Kit (JDK) 8 或更新版** – 程式碼使用標準的 Java API。
* **Aspose OCR for Java** 函式庫 – 可從 Maven Central 取得或從 Aspose 官方網站下載 JAR。
* 一個包含可讀文字的 **sample JPG**（例如掃描發票或文件截圖）。

不需要額外的框架；此範例可在純 Java 專案中執行。

## 步驟 1 – 設定專案並加入 Aspose OCR

首先，建立一個新的 Maven 專案（或僅在 classpath 中放入 JAR 的資料夾）。若使用 Maven，請將以下相依性加入 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **專業提示：** 請務必在 Aspose Maven 套件庫上確認最新版本；較新的發行版包含效能調校與錯誤修正。

相依性解決後，即可撰寫能 **create searchable PDF** 的 Java 程式碼。

## 步驟 2 – 載入圖像（image to searchable pdf）

第一個實際步驟是將 OCR 引擎指向來源圖像。此時 **image to searchable pdf** 的轉換真正開始。

```java
import com.aspose.ocr.*;

public class SearchablePdfExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the JPG you want to turn into a searchable PDF
        // Replace "YOUR_DIRECTORY/input.jpg" with the actual path to your file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

> **為何重要：** `setImage` 告訴 Aspose 要分析哪個位圖。若提供低解析度的圖像，OCR 品質會受影響，請確保 JPG 至少為 300 dpi 以獲得最佳效果。

## 步驟 3 – 從圖像辨識文字

現在引擎已知道要處理哪張圖像，我們可以請它 **recognize text from image**。Aspose OCR 在底層完成繁重工作，處理語言偵測、字元分割與信賴度計分。

```java
        // Perform OCR and directly output a searchable PDF
        ocrEngine.recognize()
                 .save("YOUR_DIRECTORY/output-searchable.pdf", OcrOutputFormat.SEARCHABLE_PDF);
```

`recognize()` 呼叫會回傳流暢介面，讓我們可以鏈接 `save` 方法。透過指定 `OcrOutputFormat.SEARCHABLE_PDF`，函式庫會在 PDF 中嵌入隱形文字層，同時保留原始圖像外觀。

> **特殊情況：** 若你的 JPG 包含多頁（例如將多頁 TIFF 另存為多個 JPG），則需對每個檔案迴圈處理，並在之後合併產生的 PDF。相同的 OCR 引擎可在每次迭代中重複使用。

## 步驟 4 – 驗證結果

儲存操作完成後，簡單的主控台訊息會告知一切順利。

```java
        // Let the user know the PDF is ready
        System.out.println("Searchable PDF created.");
    }
}
```

當你在如 Adobe Acrobat 等檢視器中開啟 `output-searchable.pdf` 時，應能選取隱藏文字、複製或執行搜尋——正是 **searchable PDF** 所應具備的功能。

### 預期輸出

執行程式會印出：

```
Searchable PDF created.
```

產生的 PDF 會顯示原始 JPG，同時允許文字選取。若開啟 PDF 的「Properties → Description → PDF Producer」，會看到類似 `Aspose.OCR for Java` 的資訊。

## 完整範例程式

以下為完整、可直接執行的來源檔案。將其複製貼上至 IDE，調整檔案路徑後執行。

```java
import com.aspose.ocr.*;

public class SearchablePdfExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image containing the text to be recognized
        // Make sure the path points to a real JPG on your disk
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 3: Recognize the text and directly save it as a searchable PDF
        ocrEngine.recognize()
                 .save("YOUR_DIRECTORY/output-searchable.pdf", OcrOutputFormat.SEARCHABLE_PDF);

        // Step 4: Notify that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

> **如果 OCR 失敗怎麼辦？**  
> * 通常是因為圖像噪點過多或語言未即時支援。可透過前置處理圖像（提升對比、去斜）或明確設定語言，例如 `ocrEngine.getLanguage().setLanguage(OcrLanguage.English);` 來提升準確度。

## 常見問題與注意事項

| Question | Answer |
|----------|--------|
| **我可以提取純文字而不是 PDF 嗎？** | 可以。使用 `ocrEngine.recognize().save("output.txt", OcrOutputFormat.TEXT);` |
| **如果我要處理 PNG 呢？** | 相同的 API 可使用，只需在 `fromFile` 中更改檔案副檔名。 |
| **產生的 PDF 在所有檢視器上都真的可搜尋嗎？** | 現代檢視器（Adobe Reader、Foxit、Chrome）會支援隱形文字層。較舊的工具可能會忽略。 |
| **如何控制 PDF 頁面大小？** | Aspose OCR 預設使用圖像尺寸。若需自訂大小，可手動產生 PDF 並疊加 OCR 文字層——這屬於進階情境。 |

## 效能建議

* **批次處理：** 重新使用單一 `OcrEngine` 實例處理多張圖像，以避免重複載入原生函式庫。
* **執行緒安全性：** 此引擎 **不** 支援執行緒安全；若平行處理，請為每個執行緒建立一個實例。
* **記憶體使用量：** 大圖像會佔用大量記憶體。若遇到 `OutOfMemoryError`，請在送入引擎前縮小圖像尺寸。

## 往後步驟

既然已了解如何 **create searchable PDF**，你可能想探索相關任務：

* **Convert jpg to pdf**（不使用 OCR），可使用 Aspose PDF 函式庫產生純圖像 PDF。  
* **Extract text from jpg**，將文字輸出至 `.txt` 檔案以供索引。  
* **Combine multiple searchable PDFs**，使用 Aspose PDF 的 `PdfFileEditor` 合併為單一文件。  

以上皆建立在你剛設定的相同基礎上。

---

### 快速回顧

* 我們使用 Aspose OCR for Java **created a searchable PDF** 從 JPG。  
* 流程涵蓋載入圖像、辨識文字，並儲存為可搜尋的 PDF。  
* 你現在擁有可重複使用的模式，適用於 **image to searchable PDF**、**recognize text from image**、**extract text from jpg** 與 **convert jpg to pdf**。

使用自己的文件試試看，必要時調整語言設定，讓 OCR 為你完成繁重工作。祝開發愉快！  

![建立可搜尋 PDF 範例](placeholder.png){alt="建立可搜尋 PDF"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}