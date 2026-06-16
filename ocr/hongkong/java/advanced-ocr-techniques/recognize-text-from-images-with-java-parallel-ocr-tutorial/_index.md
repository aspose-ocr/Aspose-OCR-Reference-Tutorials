---
category: general
date: 2026-01-12
description: 學習如何使用 Aspose OCR 在 Java 中從圖像識別文字，並從 PNG 檔案提取文字。平行處理讓它更快。
draft: false
keywords:
- recognize text from images
- extract text from png
language: zh-hant
og_description: 發現使用 Aspose OCR 及平行處理，在 Java 中辨識圖像文字並從 PNG 檔案提取文字的最簡單方法。
og_title: 使用 Java 從圖像辨識文字 – 平行 OCR 指南
tags:
- OCR
- Java
- Aspose
title: 使用 Java 從圖像辨識文字 – 平行 OCR 教學
url: /zh-hant/java/advanced-ocr-techniques/recognize-text-from-images-with-java-parallel-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java 進行圖像文字辨識 – 平行 OCR 教學

是否曾經需要 **recognize text from images**，卻卡在「我要怎麼做？」的問題上？你並不是唯一的使用者。無論是數位化發票、從螢幕截圖提取資料，或是建立可搜尋的檔案庫，能夠 *recognize text from images* 都是顛覆性的改變。  

在本指南中，我們將逐步說明一個完整、可直接執行的 Java 範例，它不僅能 **recognize text from images**，還示範如何使用 Aspose OCR 內建的平行引擎 **extract text from png** 檔案。無需外部腳本、沒有遺漏的部分——只有直接的程式碼與清晰的說明。

## 您將學到什麼

- 在 Java 專案中設定 Aspose OCR  
- 啟用平行處理以加速批次工作  
- 載入 PNG 檔案集合並有效率地 **extract text from png**  
- 處理常見陷阱（大型檔案、空結果、執行緒上限）  
- 在文章結尾查看完整、可執行的原始程式碼  

完成後，您將擁有一個可直接複製貼上的解決方案，能夠套用到任何基於圖像的文字擷取工作流程。

## 前置條件

| 需求 | 原因說明 |
|-------------|----------------|
| Java 8 或更新版本 | Aspose OCR 的 Java API 目標為 Java 8 以上 |
| Maven 或 Gradle（用於相依管理） | 簡化加入 Aspose OCR 函式庫 |
| 您想處理的幾張 PNG 圖片 | 本教學使用 `doc1.png`‑`doc4.png` 作為範例 |
| 基本的 Java 語法知識 | 程式碼相當直接，但您仍需編譯與執行它 |

如果缺少上述任一項，請從 Oracle 或 AdoptOpenJDK 下載最新的 JDK，並建立一個簡易的 Maven 專案——不需要任何花俏的設定。

![recognize text from images diagram](image.png){alt="recognize text from images 圖示"}

## 第一步 – 將 Aspose OCR 加入您的專案

首先，告訴 Maven（或 Gradle）下載 Aspose OCR 函式庫。在 `pom.xml` 檔案中，加入以下內容：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

如果您偏好使用 Gradle，等價的設定如下：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** 檢查 [Aspose OCR Maven repository](https://repo.aspose.com/repo) 以取得最新版本。保持函式庫為最新可確保您獲得最新的 OCR 改進與錯誤修正。

## 第二步 – 啟用平行處理（祕密武器）

Aspose OCR 能將工作負載分散至多個 CPU 核心。這就是即使面對數十個 PNG 檔案，我們仍能保持 **recognize text from images** 操作快速的原因。

```java
// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Configure parallel options – up to 4 cores in this demo
ParallelOptions parallelOptions = new ParallelOptions();
parallelOptions.setMaxDegreeOfParallelism(4); // Adjust based on your machine
ocrEngine.setParallelOptions(parallelOptions);
```

為什麼要設定上限？過度分配執行緒會使其他程序資源不足，尤其在共享伺服器上。四核心對大多數桌面電腦而言是安全的預設值；若您知道硬體能支援更多，可自行提升。

## 第三步 – 準備 PNG 檔案清單

本教學聚焦於 **extract text from png** 檔案，但相同程式碼亦適用於 JPEG、BMP 等格式。將您的圖像放入資料夾，並如以下方式引用：

```java
String[] imageFiles = {
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
};
```

> **Note:** 將 `YOUR_DIRECTORY` 替換為 PNG 檔案所在的絕對或相對路徑。若需處理動態資料夾，可使用 `Files.list(Paths.get("YOUR_DIRECTORY"))` 自動建立陣列。

## 第四步 – 對每張圖像執行 OCR（引擎負責繁重工作）

即使已啟用平行處理，我們仍會遍歷檔案陣列。Aspose OCR 會在內部根據我們設定的執行緒分配辨識工作。

```java
for (String imagePath : imageFiles) {
    // Load the image into the engine
    ocrEngine.setImage(imagePath);
    
    // Perform recognition
    OcrResult result = ocrEngine.recognize();
    
    // Guard against empty results
    String text = result.getText();
    if (text == null || text.isEmpty()) {
        System.out.println("[" + imagePath + "] => No text found.");
        continue;
    }
    
    // Print a short preview (first 50 characters)
    System.out.println("[" + imagePath + "] => " +
        text.substring(0, Math.min(50, text.length())) + "...");
}
```

### 為什麼使用迴圈而不是平行串流？

Aspose OCR 已根據 `ParallelOptions` 在內部分割圖像處理。將呼叫再包裹於外部平行串流會造成雙重包裝，甚至可能降低效能。請信任函式庫自行管理執行緒。

## 第五步 – 邊緣情況與實用技巧

| 情況 | 處理方式 |
|-----------|------------|
| **Huge PNG ( > 10 MB )** | 增加 JVM 堆積大小 (`-Xmx2g`) 或在送入引擎前調整圖像大小。 |
| **Mixed image formats** | 使用 `ocrEngine.setImage(new File(imagePath))` —— 引擎會自動偵測格式。 |
| **Need the full text, not just a preview** | 將 `result.getText()` 存入 `StringBuilder`，或寫入檔案以供後續分析。 |
| **Running on a CI server without a GUI** | 不需要額外步驟——Aspose OCR 完全無頭。 |
| **License expiration** | 使用 `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` 註冊臨時授權，以避免評估水印。 |

## 完整可執行範例

以下是完整的 Java 類別，您可以直接複製、貼上並執行。它包含了我們討論的所有部分，並附有少量說明以增進清晰度。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.parallel.*;

public class ParallelOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create and initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing (up to 4 CPU cores)
        ParallelOptions parallelOptions = new ParallelOptions();
        parallelOptions.setMaxDegreeOfParallelism(4); // Adjust as needed
        ocrEngine.setParallelOptions(parallelOptions);

        // Step 3: Define the PNG files to be processed
        String[] imageFiles = {
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.png",
            "YOUR_DIRECTORY/doc3.png",
            "YOUR_DIRECTORY/doc4.png"
        };

        // Step 4: Recognize text from each image (engine handles parallelism internally)
        for (String imagePath : imageFiles) {
            // Load the image
            ocrEngine.setImage(imagePath);

            // Perform OCR
            OcrResult result = ocrEngine.recognize();

            // Extract the recognized text
            String text = result.getText();

            // Guard against empty results
            if (text == null || text.isEmpty()) {
                System.out.println("[" + imagePath + "] => No text found.");
                continue;
            }

            // Step 5: Output a short preview (first 50 characters)
            System.out.println("[" + imagePath + "] => " +
                text.substring(0, Math.min(50, text.length())) + "...");
        }
    }
}
```

### 預期輸出

如果 `doc1.png` 包含文字 “Invoice #12345 – Total $250.00”，您會看到類似以下的輸出：

```
[YOUR_DIRECTORY/doc1.png] => Invoice #12345 – Total $250.00...
[YOUR_DIRECTORY/doc2.png] => No text found.
[YOUR_DIRECTORY/doc3.png] => Customer Name: John Doe...
[YOUR_DIRECTORY/doc4.png] => ...
```

預覽會截斷於 50 個字元，但完整字串仍存於 `result.getText()`，可供任何後續處理使用。

## 結論

您現在擁有一套穩固、可投入生產環境的模式，使用 Aspose OCR 在 Java 中 **recognize text from images**，同時也已了解如何以平行加速 **extract text from png** 檔案。主要步驟——引擎設定、平行配置、圖像清單準備與結果處理——皆已說明，並提供多項實用技巧以避免常見問題。

接下來可以做什麼？嘗試將 PNG 清單改為動態目錄掃描，將 OCR 輸出導入如 Elasticsearch 的搜尋索引，或試驗語言特定的 OCR 設定（`ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH)`）。掌握核心工作流程後，您可以盡情發揮創意。

如果您在實作過程中遇到任何問題或有擴充本教學的想法，歡迎在下方留言。祝編程愉快，盡情將那些頑固的圖像轉換為可搜尋的文字！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}