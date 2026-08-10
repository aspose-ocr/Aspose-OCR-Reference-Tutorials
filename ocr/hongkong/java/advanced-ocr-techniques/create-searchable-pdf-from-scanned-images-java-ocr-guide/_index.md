---
category: general
date: 2026-06-22
description: 使用 Aspose OCR 在 Java 中建立可搜尋的 PDF。了解如何轉換掃描 PDF、處理混合語言 OCR 並提升準確度。
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- how to ocr document
- mixed language ocr
- aspose ocr java
language: zh-hant
og_description: 使用 Aspose OCR 在 Java 中建立可搜尋的 PDF。本教學示範如何對文件進行 OCR、處理混合語言文字，並輸出可搜尋的
  PDF。
og_title: 從掃描圖像建立可搜尋 PDF – Java OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  headline: Create Searchable PDF from Scanned Images – Java OCR Guide
  type: TechArticle
- description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  name: Create Searchable PDF from Scanned Images – Java OCR Guide
  steps:
  - name: Expected Output
    text: 'When you open `processed.pdf` in Adobe Reader (or any PDF viewer), you
      should be able to:'
  - name: 1. What if my document contains more than two languages?
    text: '`config.setLanguage` accepts a var‑args list, so you can pass as many `OcrLanguage`
      constants as you need:'
  - name: 2. Can I run this on a headless server without a GPU?
    text: Absolutely. Set `config.setUseGpu(false)` or simply omit the call. The engine
      will fall back to multi‑core CPU processing, which is still fast thanks to the
      thread pool we configured.
  - name: 3. How do I handle huge PDFs (hundreds of pages)?
    text: Aspose OCR streams pages one‑by‑one, so memory usage stays modest. However,
      you might want to split the PDF into smaller chunks using Aspose PDF’s `split`
      method, process each chunk, then merge the results back together.
  - name: 4. Is there a way to keep the original PDF’s metadata (author, creation
      date)?
    text: 'Yes. After you obtain `searchablePdf`, you can copy metadata from the original
      PDF:'
  type: HowTo
tags:
- OCR
- Java
- PDF
title: 從掃描圖像建立可搜尋 PDF – Java OCR 指南
url: /zh-hant/java/advanced-ocr-techniques/create-searchable-pdf-from-scanned-images-java-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從掃描圖像建立可搜尋的 PDF – Java OCR 指南

有沒有想過如何在不花大筆錢購買第三方服務的情況下，從一堆掃描頁面**建立可搜尋的 PDF**？你並不孤單。許多開發者在需要**轉換掃描 PDF**檔案，使使用者真的能搜尋時，常會卡在同一個問題上。

在本指南中，我們將逐步說明一個完整且可執行的範例，使用 **Aspose OCR for Java** 來**執行文件層級的 OCR** 任務、處理**混合語言 OCR**，最後產出精緻的可搜尋 PDF。完成後，你將擁有一個可自行放入任何 Maven 或 Gradle 專案的獨立程式，立即開始處理文件。

## 前置條件 – 你需要的項目

- 已在 PATH 中安裝並設定好 Java 17（或任何較新版本的 JDK）。  
- 你熟悉的 IDE 或編輯器（IntelliJ IDEA、Eclipse、VS Code…）。  
- Aspose.OCR for Java 程式庫 – 你可以從 [Aspose Maven repository](https://repo.aspose.com/repo/com/aspose/aspose-ocr/) 取得最新的 JAR。  
- 想要轉換成可搜尋的多頁掃描 PDF。  
- （可選）若要使用 `setUseGpu(true)` 以加速處理，需具備支援 GPU 的機器。

只要上述項目都準備好，你就可以直接複製貼上以下程式碼，按下 **Run**，而不必再去尋找缺少的相依性。

## 步驟 1：設定專案並匯入 Aspose OCR

首先，建立一個新的 Maven 模組（或 Gradle 專案），並加入 Aspose OCR 相依性：

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest version -->
</dependency>
```

如果你偏好使用 Gradle，等效的行是：

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

當建置同步完成後，你就能匯入我們需要的類別。

## 步驟 2：初始化 OCR 引擎

建立引擎相當簡單，但值得了解為何要提前這麼做。`OcrEngine` 物件保存了設定、執行緒與 GPU 設定，會影響之後的每一步操作。

```java
import com.aspose.ocr.*;

public class AdvancedOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine – this is the heart of the create searchable pdf process
        OcrEngine ocrEngine = new OcrEngine();
```

> **專業提示：** 只建立一次引擎並在多個檔案間重複使用，可減少開銷，尤其在處理大量 PDF 時更為有效。

## 步驟 3：載入掃描的 PDF（或影像串流）

Aspose OCR 使用影像串流，因此我們直接將掃描的 PDF 作為輸入。程式庫會在內部將每一頁光柵化，這就是為什麼可以一次從 PDF 開始，最終得到可搜尋的 PDF。

```java
        // Load the source PDF – replace the path with your actual file location
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page_scanned.pdf"));
```

如果你改為擁有一系列 TIFF 或 JPEG，僅需將 `ImageStream.fromFile` 指向那些檔案；其餘流程保持不變。

## 步驟 4：微調 OCR 設定以支援混合語言

這正是 **混合語言 OCR** 發揮威力的地方。透過傳入多個 `OcrLanguage` 列舉，你告訴引擎在同一頁上同時偵測英語與俄語（或其他任意組合）。

```java
        // Grab the mutable config object
        OcrConfig config = ocrEngine.getConfig();

        // Enable English + Russian detection – you can add more languages as needed
        config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN);

        // Speed vs. accuracy trade‑off: use all available cores
        config.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Turn on GPU acceleration if the runtime detects a compatible device
        config.setUseGpu(true);

        // Spell‑check improves accuracy for noisy scans
        config.setEnableSpellCorrection(true);

        // Tell Aspose we want a searchable PDF as the final output
        config.setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

> **為何重要：** 若未指定語言，引擎預設僅使用英語，這會大幅降低包含西里爾字母或其他文字的文件的辨識率。

## 步驟 5：加入前置處理濾鏡以清理掃描圖像

掃描的 PDF 常會有傾斜、斑點或低對比度等問題。加入 `DeskewFilter` 與 `DenoiseFilter` 可協助 OCR 引擎更清晰地辨識字元。

```java
        // Set up image preprocessing
        ImagePreprocessOptions preprocess = new ImagePreprocessOptions();
        preprocess.addFilter(new DeskewFilter());   // Straighten tilted pages
        preprocess.addFilter(new DenoiseFilter()); // Reduce background noise
        ocrEngine.setPreprocessOptions(preprocess);
```

如果原始素材特別髒亂，你可以串接其他濾鏡，例如 `ContrastFilter` 或 `BinarizationFilter`。

## 步驟 6：執行 OCR 並產生可搜尋的 PDF

現在開始進行繁重的工作。`recognizeToPdf()` 會執行 OCR 流程、套用前置處理步驟，並將辨識出的文字寫入 PDF 內的隱形文字層。

```java
        // Perform OCR and retrieve a searchable PDF document object
        PdfDocument searchablePdf = ocrEngine.recognizeToPdf();
```

回傳的 `PdfDocument` 是完整的 Aspose PDF 物件，表示你可以在儲存前進一步編輯中繼資料、加入書籤，或與其他 PDF 合併。

## 步驟 7：儲存結果並驗證

最後，將輸出寫入磁碟。主控台訊息會快速提示你一切順利。

```java
        // Save the searchable PDF to the desired location
        searchablePdf.save("YOUR_DIRECTORY/processed.pdf");
        System.out.println("OCR completed – searchable PDF saved at YOUR_DIRECTORY/processed.pdf");
    }
}
```

### 預期輸出

當你在 Adobe Reader（或任何 PDF 檢視器）開啟 `processed.pdf` 時，應該能夠：

1. **選取文字** – 點擊並拖曳任意單詞，即可複製。  
2. **搜尋** – 按下 `Ctrl+F`，輸入原始掃描中出現的片語。  
3. **保持原始版面** – 視覺外觀與掃描來源完全相同，僅新增了隱形文字層。

如果看到亂碼或缺頁，請再次確認語言設定，並確保來源 PDF 沒有密碼保護。

## 常見問題與邊緣案例

### 1. 若文件包含超過兩種語言該怎麼辦？

`config.setLanguage` 接受可變參數列表，你可以傳入任意多的 `OcrLanguage` 常數：

```java
config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN, OcrLanguage.CHINESE_SIMPLIFIED);
```

只要記得，每多加一種語言會稍微增加處理時間。

### 2. 能否在沒有 GPU 的無頭伺服器上執行？

當然可以。設定 `config.setUseGpu(false)` 或直接省略此呼叫。引擎會回退至多核心 CPU 處理，因為我們已配置執行緒池，速度仍相當快。

### 3. 如何處理巨大的 PDF（數百頁）？

Aspose OCR 會逐頁串流處理，因此記憶體使用量保持在可接受範圍。但你可能需要使用 Aspose PDF 的 `split` 方法將 PDF 分割成較小的區塊，分別處理後再將結果合併。

### 4. 有沒有方法保留原始 PDF 的中繼資料（作者、建立日期）？

有的。取得 `searchablePdf` 後，你可以從原始 PDF 複製中繼資料：

```java
PdfDocument original = new PdfDocument("YOUR_DIRECTORY/multi_page_scanned.pdf");
searchablePdf.getInfo().setAuthor(original.getInfo().getAuthor());
// repeat for other metadata fields
```

## 生產環境 OCR 的專業提示

- **批次處理：** 將整個流程包在迴圈中，遍歷目錄內的檔案。重複使用單一 `OcrEngine` 實例，以避免重複初始化的開銷。  
- **錯誤處理：** 捕獲 `OcrException` 以記錄失敗的檔案，然後繼續處理下一個文件。  
- **效能監控：** 在 `recognizeToPdf()` 前後使用 `System.nanoTime()` 記錄每個檔案的處理時間；這有助於決定是否要擴展至雲端工作池。  
- **安全性：** 若處理機密文件，考慮在儲存前使用 `searchablePdf.encrypt(...)` 加密輸出 PDF。

## 結論

我們剛剛已說明如何使用 **Aspose OCR for Java**，從掃描來源建立 **可搜尋的 PDF** 檔案。教學展示了如何 **轉換掃描 PDF**、設定 **混合語言 OCR**，以及微調前置處理濾鏡——同時保持程式碼簡潔、適合投入生產環境。  

接下來，你可以探索加入 OCR 產生的縮圖、與文件管理系統整合，或將抽取的文字輸入如 Elasticsearch 等搜尋索引。可能性與你需要數位化的文件一樣廣闊。

對於在 Java 中 **如何 OCR 文件** 有更多問題，或想更深入了解 PDF 操作嗎？在下方留下評論吧，祝編程愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在所示技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}