---
category: general
date: 2026-04-26
description: 使用 Aspose OCR 於 Java，將圖片製作成可搜尋的 PDF。學習如何將圖片轉換為 PDF、將圖片 OCR 為 PDF，以及快速擷取圖片中的文字。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- extract text from image
- how to set language
language: zh-hant
og_description: 使用 Aspose OCR 從圖像建立可搜尋的 PDF。本指南示範如何將圖像轉換為 PDF、將圖像 OCR 為 PDF，以及從圖像中擷取文字。
og_title: 使用 Java OCR 從圖像生成可搜尋的 PDF
tags:
- Java
- OCR
- PDF
title: 使用 Java OCR 從圖片建立可搜尋的 PDF
url: /zh-hant/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像建立可搜尋的 PDF（使用 Java OCR）

是否曾需要從掃描的發票 **建立可搜尋的 PDF**，卻不知從何下手？你並非唯一遇到此問題的人——許多開發者在想要一個真的可以搜尋的 PDF 時，都會卡在這裡。好消息是？使用 Aspose OCR for Java，你可以 **將圖像轉換為 PDF**，即時執行 OCR，僅用幾行程式碼就能得到整潔的可搜尋檔案。

在本教學中，我們將完整示範整個流程：載入圖片、告訴引擎預期的語言、執行 OCR，最後儲存 **可搜尋的 PDF**。結束時，你還會知道如何手動 **extract text from image**、微調語言設定，並處理幾個常見的邊緣案例。無需外部服務、無需晦澀的指令列工具——純粹的 Java。

## 需要的環境

- Java 17 或更新版本（API 亦支援較舊版本，但 17 為最佳選擇）。  
- Aspose OCR for Java 函式庫 – 可從 Maven Central 取得最新 JAR（`com.aspose:aspose-ocr:23.10`）。  
- 包含可辨識文字的圖像檔（支援 PNG、JPG 或 TIFF）。  
- 一點點 IDE 使用耐心 – IntelliJ IDEA 或 VS Code 均可。

如果你已經具備上述條件，太好了！如果還沒有，以下的 Maven 片段會讓你快速上手：

```xml
<!-- Add to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

基礎建設已就緒，現在讓我們深入程式碼。

## 步驟 1：初始化 OCR 引擎 – **create searchable pdf** 的核心

在任何轉換發生之前，你必須建立一個 `OcrEngine` 實例。把它想成會讀取像素並轉換成字元的大腦。

```java
import com.aspose.ocr.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

*為什麼這很重要：* 引擎保存所有辨識設定（語言、精確模式等）。只建立一次並在多張圖像間重複使用，比每個檔案都重新建立引擎更有效率。

## 步驟 2：**How to set language** – 提升法文、德文或任何文字的辨識準確度

如果你知道來源文件的語言，請告訴 OCR 引擎。這會加快處理速度並減少誤辨識。

```java
        // Step 2: (Optional) Specify the language to improve text extraction
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

你可以將 `OcrLanguage.FRENCH` 替換為 `ENGLISH`、`SPANISH`、`GERMAN` 等等。若不確定語言，直接省略此行讓 Aspose 自行判斷——但準確度可能會稍微下降。

## 步驟 3：載入你想要 **convert image to pdf** 的圖像

`setImage` 方法接受檔案路徑、`InputStream`，甚至是 `java.awt.Image` 物件。如果你有位元組陣列（例如來自網路上傳），只要包在 `ByteArrayInputStream` 中直接傳入即可。

```java
        // Step 3: Load the image that contains the text to be recognized
        ocrEngine.setImage("YOUR_DIRECTORY/french_invoice.png");
```

## 步驟 4：執行 OCR 並在一次呼叫中完成 **ocr image to pdf**

Aspose 讓這一步變得毫不費力：`recognizeToPdf` 會執行辨識引擎，並一次寫入可搜尋的 PDF。

```java
        // Step 4: Recognize the text and save it as a searchable PDF
        ocrEngine.recognizeToPdf("YOUR_DIRECTORY/french_invoice_searchable.pdf");
```

在底層，函式庫會建立一個與原始圖像對齊的隱形文字層。當你在 Adobe Reader 開啟產生的檔案時，輸入關鍵字於搜尋框，即可立即跳到相符位置。

## 步驟 5：驗證結果 – 輸出會是什麼樣子？

```java
        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF generated.");
    }
}
```

執行程式後，開啟 `french_invoice_searchable.pdf`。嘗試搜尋發票中確定會出現的詞彙（例如 “Total”）。若高亮正確定位到相應位置，代表你已成功 **create searchable pdf**。  
![Create searchable PDF example](example.png)<!-- alt text includes primary keyword -->

### 預期輸出

```
Searchable PDF generated.
```

以及位於 `YOUR_DIRECTORY` 的 PDF 檔案，你可以分享、索引或歸檔。

## 步驟 6：從圖像中提取原始文字（可選）

有時你需要純文字進一步處理——例如寫入資料庫或進行情感分析。Aspose 允許直接取得辨識出的文字：

```java
        // Optional: Get the extracted text as a String
        String extractedText = ocrEngine.getText();
        System.out.println("Extracted text:");
        System.out.println(extractedText);
```

此程式碼片段示範了 **extract text from image**，而不需要產生 PDF。當你只關心內容而非視覺排版時，非常方便。

## 處理多頁或多張圖像

如果來源是多頁 TIFF 或 JPEG 資料夾，如何處理？你可以遍歷檔案，對每張呼叫 `recognizeToPdf`，然後使用 Aspose PDF 或其他函式庫合併 PDF。以下是一個快速範例：

```java
import java.io.File;
import com.aspose.pdf.*;

public class MultiPageDemo {
    public static void main(String[] args) throws Exception {
        OcrEngine engine = new OcrEngine();
        File folder = new File("YOUR_DIRECTORY/images");
        Document finalDoc = new Document();

        for (File img : folder.listFiles((d, n) -> n.matches(".*\\.(png|jpg|tif)"))) {
            engine.setImage(img.getAbsolutePath());
            // Save each page as a temporary PDF
            String tempPdf = img.getName() + ".pdf";
            engine.recognizeToPdf(tempPdf);
            // Append to final document
            Document pageDoc = new Document(tempPdf);
            finalDoc.getPages().add(pageDoc.getPages().get_Item(1));
        }
        finalDoc.save("YOUR_DIRECTORY/combined_searchable.pdf");
        System.out.println("All pages merged into searchable PDF.");
    }
}
```

**專業提示：** 合併完成後刪除暫存的 PDF，以保持工作區整潔。

## 常見陷阱與避免方法

- **低解析度圖像：** OCR 準確度在低於 150 dpi 時會急劇下降。若可能，請提升解析度或重新掃描。  
- **頁面傾斜：** 旋轉的圖像會讓引擎困惑。使用 `ocrEngine.getImagePreprocessingSettings().setDeskew(true)` 來自動校正輕微傾斜。  
- **不支援的語言：** 確認你設定的語言已包含在 Aspose OCR 授權中，否則引擎會退回使用英文。  
- **大型檔案：** 處理 30 MB 的 TIFF 可能會佔用大量記憶體。考慮將其切割成較小的區塊，或增加 JVM 堆大小（`-Xmx2g`）。

## 下一步 – 接下來該怎麼做

既然你已掌握 **create searchable pdf** 的基礎，接下來可以探索：

- **批次轉換：** 結合多頁模式與排程器，於每晚自動處理新掃描檔。  
- **Metadata 注入：** 使用 Aspose PDF 為可搜尋的 PDF 加入標題、作者或自訂標籤。  
- **數位簽章：** OCR 完成後以憑證保護 PDF，確保法律文件的合規性。  

所有這些延伸功能仍然依賴我們先前討論的核心概念：初始化 OCR 引擎、（可選）設定語言、載入圖像，最後呼叫 `recognizeToPdf`。

---

### TL;DR

我們示範了一個完整且可執行的範例，說明如何使用 Aspose OCR for Java **create searchable PDF**。步驟包括初始化引擎、（可選）設定語言（即 “how to set language”）、載入圖像、執行 OCR、儲存可搜尋的 PDF，並可選擇提取純文字。還涵蓋了多頁處理、常見陷阱以及進一步自動化的想法。

試著用自己的收據、合約或手寫筆記來實作——只要幾秒鐘，就能把靜態圖片變成完整可搜尋的文件。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}