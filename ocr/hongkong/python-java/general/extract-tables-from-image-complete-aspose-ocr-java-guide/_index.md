---
category: general
date: 2026-05-03
description: 使用 Aspose OCR Java 從圖像中提取表格。學習如何載入圖像進行 OCR，從 PNG 提取表格，轉換圖像表格文字，並快速識別收據圖像。
draft: false
keywords:
- extract tables from image
- extract table from png
- load image for ocr
- convert image table text
- recognize receipt image
language: zh-hant
og_description: 使用 Aspose OCR Java 從圖像中提取表格。本指南展示如何載入圖像進行 OCR、從 PNG 中提取表格、轉換圖像表格文字，以及辨識收據圖像。
og_title: 從圖像中提取表格 – Aspose OCR Java 教程
tags:
- Aspose OCR
- Java
- Image Processing
title: 從圖像提取表格 – 完整 Aspose OCR Java 指南
url: /zh-hant/python-java/general/extract-tables-from-image-complete-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像提取表格 – 完整 Aspose OCR Java 指南

是否曾需要 **extract tables from image** 檔案卻屢屢受阻？也許你有一張掃描的收據或拍攝的發票，而表格資料隱藏在 PNG 中。在本教學中，你將會看到如何 *load image for OCR*，將圖片轉換為結構化的列，並 **convert image table text** 成為可在 Java 中使用的資料。  

我們將逐步說明，從授權 Aspose OCR 引擎到列印偵測到的表格的每個儲存格。完成後，你將能夠 **recognize receipt image** 檔案，輕鬆提取其表格。

## 你將學會

- 如何初始化 Aspose OCR 引擎並套用授權。
- 為何啟用表格偵測是 **extract tables from image** 的關鍵。
- 執行 **load image for OCR** 並在 PNG 上進行辨識所需的完整程式碼。
- 處理多個表格、低解析度掃描以及常見陷阱的方法。
- 如何將 **convert image table text** 轉換為可列印（或可匯入資料庫）的格式。

不需要外部文件——所有你需要的資訊都在此。

## 前置條件

- Java 17 或更新版本（程式碼使用現代模組系統）。
- Aspose OCR for Java 授權檔 (`Aspose.OCR.Java.lic`)。若僅作測試，臨時評估金鑰亦可使用。
- 包含清晰表格的 PNG 圖片（例如 `receipt_with_table.png`）。  
- 使用 Maven 或 Gradle 取得 Aspose OCR 相依套件：

```xml
<!-- Maven snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

> **小技巧：** 將授權檔放在 `src/main/resources` 資料夾旁邊，以確保路徑在不同環境下保持穩定。

---

## 步驟 1 – 初始化 OCR 引擎以 **extract tables from image**

在引擎執行任何操作之前，需要先確認你是合法使用者。

```java
import com.aspose.ocr.*;

public class TableExtractor {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Apply your Aspose OCR license – this removes evaluation watermarks
        License license = new License();
        license.setLicense("Aspose.OCR.Java.lic");
        ocrEngine.setLicense(license);
```

*為何重要：* 若未使用有效授權，OCR 引擎將以試用模式運作，可能截斷結果或加入不必要的浮水印——導致表格提取不可靠。

---

## 步驟 2 – 啟用表格偵測（**extract table from png**）

表格偵測預設未啟用，需要手動開啟。

```java
        // Step 2: Turn on table detection so the engine looks for tabular structures
        ocrEngine.getConfig().setEnableTableDetection(true);
```

啟用此旗標會告訴 Aspose OCR 將對齊的文字群組視為列與欄，這正是當你想要 **extract tables from image** PNG 檔案時所需要的。

---

## 步驟 3 – **Load image for OCR** 與 **recognize receipt image**

現在我們真正將圖片送入引擎。

```java
        // Step 3: Load the PNG that contains the table
        // You can also use Image.fromStream(...) for in‑memory data
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/receipt_with_table.png");

        // Run the recognition process – this returns an OcrResult object
        OcrResult ocrResult = ocrEngine.recognize(inputImage);
```

若你處理的是 **recognize receipt image** 情境，可能需要先前處理圖片（去斜、提升對比度）。這超出本快速指南的範圍，但對噪點較多的掃描值得研究。

---

## 步驟 4 – 處理 OCR 結果並 **convert image table text**

`OcrResult` 物件可能包含一個或多個表格。讓我們遍歷它們並列印每個儲存格。

```java
        // Step 4: Iterate over every detected table
        if (ocrResult.getTables().isEmpty()) {
            System.out.println("No tables were detected. Try improving image quality.");
            return;
        }

        for (Table table : ocrResult.getTables()) {
            System.out.println("Table detected:");
            for (TableRow row : table.getRows()) {
                // Join each cell's text with a tab for easy copy‑paste
                String line = row.getCells()
                                 .stream()
                                 .map(Cell::getText)
                                 .reduce((a, b) -> a + "\t" + b)
                                 .orElse("");
                System.out.println(line);
            }
            System.out.println(); // Blank line between tables
        }
    }
}
```

**此程式的作用：**  

- 檢查是否找到任何表格；若未找到，建議調整影像品質。  
- 對每個表格，列印以 Tab 分隔的儲存格列，方便匯入 CSV。  
- `Cell::getText` 呼叫是 **convert image table text** 的核心——它從每個儲存格取得原始 OCR 文字。

### 預期輸出

假設 `receipt_with_table.png` 包含一個簡單的 3 × 2 表格，輸出會類似以下：

```
Table detected:
Item	Quantity
Apple	2
Banana	5
```

若圖片有多個表格，則每個表格之間會以空白行分隔。

---

## 步驟 5 – 驗證提取的表格並處理邊緣情況

### 常見陷阱

| 問題 | 發生原因 | 快速解決方案 |
|------|----------|--------------|
| **未偵測到表格** | 圖片過於模糊或對比度低 | 在 OCR 前使用二值化 (`ImageProcessing.applyThreshold`) |
| **合併儲存格** | 表格線條太淡，OCR 將其視為單一區塊 | 在 `ocrEngine.getConfig()` 中提升 `TableDetectionSensitivity` |
| **欄位順序錯誤** | 圖片傾斜導致對齊錯誤 | 使用 `ImageProcessing.deskew` 或將圖片旋轉 90° |

### 接下來該怎麼做

- **匯出為 CSV** – 將 `System.out.println(line);` 替換為 `FileWriter` 以持久化資料。  
- **寫入資料庫** – 將每列映射為 POJO，並使用 JPA 進行持久化。  
- **結合其他 API** – 於收據處理時，你也可以使用正規表達式從 OCR 文字中提取總金額。

---

## 完整範例（可直接複製貼上）

```java
import com.aspose.ocr.*;

public class TableExtractor {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine and apply license
        OcrEngine ocrEngine = new OcrEngine();
        License license = new License();
        license.setLicense("Aspose.OCR.Java.lic");
        ocrEngine.setLicense(license);

        // Enable table detection – crucial for extracting tables from image
        ocrEngine.getConfig().setEnableTableDetection(true);

        // Load the PNG image (replace with your actual path)
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/receipt_with_table.png");

        // Recognize the image – this step performs OCR on the whole picture
        OcrResult ocrResult = ocrEngine.recognize(inputImage);

        // Verify we have tables; otherwise suggest a quality fix
        if (ocrResult.getTables().isEmpty()) {
            System.out.println("No tables were detected. Try improving image quality.");
            return;
        }

        // Print each table row by row, converting image table text into tab‑separated values
        for (Table table : ocrResult.getTables()) {
            System.out.println("Table detected:");
            for (TableRow row : table.getRows()) {
                String line = row.getCells()
                                 .stream()
                                 .map(Cell::getText)
                                 .reduce((a, b) -> a + "\t" + b)
                                 .orElse("");
                System.out.println(line);
            }
            System.out.println(); // Blank line between tables
        }
    }
}
```

執行此程式，指向包含清晰表格的 PNG，即可在主控台看到整齊排版的列。

---

## 結論

現在你已擁有一套完整、端到端的解決方案，使用 Aspose OCR for Java 來 **extract tables from image** 檔案。從授權、**load image for OCR**、啟用 **extract table from png**，最後到 **convert image table text**，每一步皆有說明與實用技巧。  

接下來，試著將輸出串接成 CSV 檔、將列寫入關聯式資料庫，或將 OCR 步驟與收據總額提取流程結合。相同的模式同樣適用於發票、價目表以及任何以格線隱藏資料的掃描文件。  

對於處理低解析度收據或批次處理有任何疑問嗎？在下方留言，我們祝你開發順利！  

![Extract tables from image example](https://example.com/assets/extract-tables-from-image.png "Extract tables from image – sample output")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}