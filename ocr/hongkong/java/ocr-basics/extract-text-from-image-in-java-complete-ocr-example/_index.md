---
category: general
date: 2026-01-12
description: 使用 Aspose OCR 於 Java 從圖像提取文字。了解如何使用 Java OCR 範例從發票圖像中提取文字，並獲取 OCR 輸出文字。
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: zh-hant
og_description: 使用 Aspose OCR 在 Java 中提取圖像文字。本指南示範如何從發票圖像中提取文字，包含 Java OCR 範例，並輸出
  OCR 文字。
og_title: 在 Java 中從圖片提取文字 – 完整 OCR 範例
tags:
- OCR
- Java
- Aspose
title: 在 Java 中從圖像提取文字 – 完整 OCR 範例
url: /zh-hant/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字（Java） – 完整 OCR 範例

Ever wondered how to **從圖像中提取文字** files without pulling your hair out? Maybe you have a stack of scanned invoices and you need the numbers fast. In my experience, the easiest way is to let a dedicated OCR library do the heavy lifting. This tutorial shows *how to extract text* from a typical invoice image using Aspose OCR for Java, and it even demonstrates a **java ocr example** that outputs the OCR text you can pipe into your downstream system.

We'll walk through everything you need to know: from setting up the project, defining the region of interest (ROI) that focuses on the header and total amount, to finally printing the extracted text. By the end, you’ll be able to **process invoice image** files automatically and retrieve clean, searchable text.

> **您將獲得：** 一個可直接執行的 Java 程式、每一步的清晰說明，以及處理真實發票的實用技巧。

---

## 前置條件

- 已安裝 Java Development Kit (JDK) 8 或更新版本。
- 用於相依管理的 Maven 或 Gradle（示範使用 Maven）。
- Aspose OCR for Java 授權（免費試用版可用於測試）。
- 一張發票圖像（`invoice.png`）放置於已知目錄中。

If any of these sound unfamiliar, don’t worry—most of them are just a download away, and the code will still compile with the community edition.

## 步驟 1：設定 Maven 專案

首先，建立一個新的 Maven 專案（或在現有專案中加入）。在 `pom.xml` 中加入 Aspose OCR 相依性：

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **專業提示：** 保持版本號為最新；較新的版本通常能提升對發票中複雜字體的辨識準確度。

儲存檔案後，執行 `mvn clean install` 以將函式庫下載至本機儲存庫。

## 步驟 2：載入發票圖像

現在函式庫已就緒，讓我們撰寫一個小型 Java 類別。首先建立 `OcrEngine` 實例，並指向要讀取的圖像。

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

為什麼要在載入圖像 **之前** 建立引擎？引擎會保存語言、DPI 與 ROI 等設定。提前設定圖像可確保這些設定套用到即將處理的檔案上。

## 步驟 3：定義感興趣區域（ROI）

發票通常包含大量雜訊——表格、標誌與細小字體。將 OCR 限定於標頭與總金額，可大幅提升速度與準確度。Aspose 允許使用矩形描述這些區域。

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

座標以像素為單位（`x`、`y`、`width`、`height`）。若發票尺寸不一，可動態計算這些值——例如先檢查圖像尺寸。若需要批次處理的 **process invoice image** 解決方案，這是一個不錯的延伸。

## 步驟 4：在指定區域執行 OCR

設定好 ROI 後，OCR 引擎即可將注意力集中在關鍵區域。`recognize()` 方法會回傳包含提取文字的 `OcrResult`。

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

在背後，Aspose 會執行多項前處理步驟：二值化、除噪與字元分割。您無需手動呼叫，只要讓 `recognize()` 完成即可。

## 步驟 5：輸出提取的文字

最後，我們將文字印出至主控台。在實際應用中，您可能會將其存入資料庫、傳入下游分析管線，或產生可搜尋的 PDF。

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

執行程式後，您應該會看到類似以下的輸出：

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

若輸出呈現亂碼，請再次確認矩形座標或提升圖像解析度。OCR 引擎偏好清晰的高 DPI 掃描。

## 完整範例程式

以下是完整、獨立的 Java 檔案，您可直接複製貼上至 `src/main/java/RoiExample.java`。不需要外部程式碼片段——所有必需的內容皆在此。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **Note:** 將 `YOUR_DIRECTORY` 替換為發票圖像的絕對路徑。若使用相對路徑，請確保工作目錄與執行 `java` 指令的目錄相符。

## 常見問題與邊緣案例

### 若發票尺寸變化該怎麼辦？

You can compute ROI dynamically:

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### 如何處理多語言？

Aspose OCR supports language packs. Just set the language before calling `recognize()`:

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### 若 OCR 回傳空字串該怎麼辦？

Typical culprits are:

- 圖像解析度低（< 300 DPI）。升級或要求更高品質的掃描。
- 背景過暗或過亮。於 OCR 前套用簡單的對比度增強濾鏡。
- ROI 座標不正確，導致完全錯過文字。

## 生產環境 OCR 的技巧

- **批次處理：** 將邏輯包在迴圈中，遍歷發票檔案目錄。記錄每個結果以便稽核。
- **錯誤處理：** 捕獲 `OcrException`，優雅地跳過損壞的圖像，避免中斷整個工作。
- **效能：** 在多張圖像間重複使用單一 `OcrEngine` 實例；每個檔案重新建立引擎會產生不必要的開銷。
- **驗證：** 提取後，對總金額使用正則表達式（`\$\d{1,3}(,\d{3})*(\.\d{2})?`）檢查，以確保數字合理。

實作上述建議，可將簡單的 **java ocr example** 轉變為穩健、可擴充的解決方案，滿足任何需要每晚 **process invoice image** 檔案的企業需求。

## 結論

我們剛剛說明了如何在 Java 中使用 Aspose OCR **extract text from image** 檔案，並聚焦於實務的發票處理情境。透過定義感興趣區域、執行 OCR 引擎，並印出 **output OCR text**，您現在已具備建構自動化資料擷取管線的堅實基礎。

接下來的步驟？嘗試將 ROI 擴展至包含明細表格、測試不同語言設定，或將提取的字串輸入 PDF 產生庫以產生可搜尋的文件。結合 OCR 與現代 Java 工具，您的可能性無限。

對於其他文件類型的 **how to extract text** 有更多問題，或需要協助微調不尋常版面的 ROI？歡迎在下方留言——祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}