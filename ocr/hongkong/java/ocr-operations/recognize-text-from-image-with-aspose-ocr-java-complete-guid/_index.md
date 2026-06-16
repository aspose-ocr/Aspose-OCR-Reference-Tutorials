---
category: general
date: 2026-03-18
description: 學習如何在 Java 中使用 Aspose OCR 從圖像辨識文字。此一步一步的教學示範如何載入圖像進行 OCR 並關閉拼寫校正功能。
draft: false
keywords:
- recognize text from image
- load image for ocr
- aspose ocr java example
- extract text from image
- turn off spell corrector
language: zh-hant
og_description: 使用 Aspose OCR 在 Java 中辨識圖像文字。於本實用教學中學習如何載入圖像進行 OCR 以及關閉拼寫校正功能。
og_title: 使用 Aspose OCR Java 從圖像識別文字 – 完整指南
tags:
- Aspose OCR
- Java
- Image Processing
title: 使用 Aspose OCR Java 從圖像辨識文字 – 完整指南
url: /zh-hant/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-complete-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR Java 識別圖片文字 – 完整指南

是否曾需要 **從圖片中識別文字**，卻不確定該選哪個函式庫？你並不孤單。在許多實務專案中——例如掃描收據、數位化表單，或從螢幕截圖中抽取說明文字——從點陣圖取得乾淨、原始文字是日常挑戰。

在本教學中，我們將手把手示範一個 **Aspose OCR Java 範例**，說明如何 **載入圖片以進行 OCR**、執行辨識引擎，甚至在需要保留原始字元時 **關閉拼寫校正**。完成後，你將擁有一個可直接執行的程式，能從圖片中抽取文字而不會被額外調整。

## 你將學到什麼

- 清楚了解 **Aspose OCR** 在 Java 中的工作流程。
- 完整程式碼，能 **從圖片中識別文字** 並 **以原始形式抽取文字**。
- 何時需要停用內建拼寫校正，以及安全的停用方式。
- 一個快速的驗證步驟，讓你確認輸出符合預期。

### 前置條件（最低需求）

- 已在機器上安裝 Java 8 或更新版本。
- Maven 或 Gradle 來管理相依性（我們會示範 Maven 片段）。
- `Aspose.OCR` JAR 檔（可從 Aspose 官方網站取得免費試用版）。
- 一張包含欲讀取文字的圖片檔（PNG、JPG、BMP 等）。示範使用 `mixed-lang.png`。

> **專業小技巧：** 若要大量處理圖片，建議以串流方式載入，以避免檔案句柄泄漏。

---

![Diagram showing OCR pipeline – recognize text from image](ocr-pipeline.png)

*Alt text: 圖示說明使用 Aspose OCR 從圖片中識別文字的步驟。*

## 第一步 – 建立專案並加入 Aspose OCR 相依性

在呼叫任何 OCR 方法之前，必須先將函式庫加入 classpath。若使用 Maven，請將以下內容放入 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

如果偏好 Gradle，等價寫法如下：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

相依性解決後，即可匯入我們將使用的兩個類別：

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
```

> **為什麼這很重要：** 透過建置工具加入 JAR 可保證在不同環境中使用相同版本，避免日後出現「找不到類別」的問題。

## 第二步 – 建立 OCR 引擎並關閉拼寫校正

Aspose OCR 內建拼寫校正功能，會嘗試猜測你本來想寫的內容。這對乾淨的文件很有幫助，但若你在掃描多語言標示或程式碼片段時，會被「校正」成不想要的文字。以下示範如何停用它：

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Disable the automatic spell correction
ocrEngine.getSpellCorrector().setEnabled(false);
```

**底層發生了什麼？** `SpellCorrector` 物件會在原始字形解碼後，執行一次基於字典的校正。呼叫 `setEnabled(false)` 後，我們告訴引擎跳過這一步，保留它偵測到的精確字元序列。

## 第三步 – 載入圖片以進行 OCR

現在正式 **載入圖片以進行 OCR**。Aspose 的 `Image.load` 方法接受檔案路徑、`InputStream`，甚至是位元組陣列。為了簡化示範，我們使用檔案路徑：

```java
// Replace the path with the location of your image file
Image inputImage = Image.load("YOUR_DIRECTORY/mixed-lang.png");
```

> **邊緣情況：** 若圖片大於 5 MB，建議先縮小尺寸。大型圖片會增加記憶體使用，且可能拖慢辨識引擎。

## 第四步 – 識別文字並取得原始輸出

引擎與圖片皆已就緒，實際的辨識只需要一行程式碼：

```java
// Perform OCR and store the raw text
String rawText = ocrEngine.recognize(inputImage);
```

`recognize` 方法會回傳一個 `String`，其中 **從圖片中抽取文字** 完全如同引擎看到的樣子——不會經過拼寫檢查或後處理。

## 第五步 – 顯示結果（無拼寫檢查）

最後，將原始 OCR 輸出印到主控台，讓你自行驗證：

```java
System.out.println("Raw OCR (no spell‑check):\n" + rawText);
```

執行程式後，應會看到類似以下的輸出：

```
Raw OCR (no spell‑check):
Hello, 世界!
12345
```

若圖片中混雜多種語言或特殊符號，因為已關閉拼寫校正，它們會保持原樣顯示。

## 完整、可執行的範例

將上述所有片段整合起來，以下是 **完整的 Aspose OCR Java 範例**，可直接貼到 `SpellCorrectionDemo.java` 檔案中：

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;

public class SpellCorrectionDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Turn off the built‑in spell corrector
        ocrEngine.getSpellCorrector().setEnabled(false);

        // Step 3: Load the image you want to recognize
        Image inputImage = Image.load("YOUR_DIRECTORY/mixed-lang.png");

        // Step 4: Run OCR on the image and obtain the raw text
        String rawText = ocrEngine.recognize(inputImage);

        // Step 5: Display the OCR result without spell‑checking
        System.out.println("Raw OCR (no spell‑check):\n" + rawText);
    }
}
```

### 如何執行

1. 將檔案存為 `SpellCorrectionDemo.java`。
2. 編譯：`javac -cp "path/to/aspose-ocr-23.9.jar" SpellCorrectionDemo.java`
3. 執行：`java -cp ".;path/to/aspose-ocr-23.9.jar" SpellCorrectionDemo`

將 `path/to` 替換為實際的 Aspose JAR 所在路徑。

## 常見問題與注意事項

### 若圖片是其他格式（例如 PDF）該怎麼辦？

Aspose OCR 也能直接讀取 PDF 頁面，但需要先將 PDF 頁面轉為圖片，或使用 `OcrEngine.recognizePdf` 的重載方法。這是另一篇教學的範圍，但 **從圖片中識別文字** 的原理相同。

### 停用拼寫校正會影響效能嗎？

會稍微提升效能。跳過字典校正可省下每頁數毫秒的時間，若一次處理上千檔案，累積下來會有明顯差異。代價是失去自動拼寫修正功能——請依據資料品質自行決定。

### 我仍然可以取得語言特定的結果嗎？

可以。引擎會自動偵測文字腳本，但你也可以透過 `ocrEngine.setLanguage(OcrEngine.Language.English)` 之類的方式強制指定語言。當你確定圖片只包含單一語言時，這能提升辨識準確度。

### 如何處理多頁 TIFF？

將每一頁視為獨立的 `Image` 物件：`Image.load("file.tif", pageIndex)`。遍歷所有頁面，分別辨識後再串接結果即可。

## 實務專案的專業建議

- **批次處理：** 將 OCR 邏輯封裝成接受 `InputStream` 的方法，讓你能直接從 S3、Azure Blob 或其他儲存服務串流圖片，免於寫入本機磁碟。
- **記憶體管理：** 使用完畢後呼叫 `ocrEngine.dispose()`，釋放原生資源。
- **日誌記錄：** 將原始輸出寫入日誌檔以作稽核，特別是在關閉拼寫校正的情況下尤為重要。
- **測試：** 編寫單元測試，提供已知圖片並斷言預期的原始字串，確保未來升級函式庫時行為不會悄悄改變。

## 結論

我們已示範如何使用 Aspose OCR for Java **從圖片中識別文字**、**載入圖片以進行 OCR**，以及在需要保留原始字元時 **關閉拼寫校正** 的完整步驟。上方的簡短、獨立程式碼片段可直接嵌入任何 Java 專案，而說明則提供每行程式碼背後的「為什麼」。

接下來，你可以探索 **批次抽取圖片文字**、嘗試語言提示，或將輸出整合至搜尋索引。無論選擇哪條路，本文所涵蓋的基礎都能讓你的 OCR 流程可靠且易於維護。

有任何新想法或實作方式嗎？歡迎留言或分享你的 **Aspose OCR Java 範例**。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}