---
category: general
date: 2026-02-09
description: 學習如何在 Java 中使用 Aspose OCR 進行批次文字辨識。一次呼叫即可從 PNG、JPG 與 TIFF 圖檔中提取文字。
draft: false
keywords:
- how to batch ocr
- extract text from images
- recognize text from png
- recognize text from jpg
- recognize text from tiff
language: zh-hant
og_description: 掌握在 Java 中批量 OCR 的技巧。本教程示範如何使用 Aspose OCR 從 PNG、JPG 與 TIFF 圖像中提取文字，並提供清晰的程式碼範例。
og_title: 如何在 Java 中批量 OCR – 高效從圖像提取文字
tags:
- OCR
- Java
- Aspose
title: 如何在 Java 中批量 OCR – 圖像文字提取完整指南
url: /zh-hant/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

.

Proceed.

Make sure to keep bold formatting.

Also note "Pro tip:" inside blockquote.

Proceed.

Now produce final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中批量 OCR – 從圖像提取文字的完整指南

有沒有想過 **如何批量 OCR** 幾張圖片而不必為每個檔案寫迴圈？你並不是唯一有此需求的人。在許多實務專案中，你會收到一個充滿掃描檔的資料夾──PNG 收據、JPG 截圖，甚至是多頁的 TIFF，且需要快速取得文字。

好消息是 Aspose OCR 正好提供這項功能：只要一次方法呼叫，即可同時辨識 PNG、JPG 與 TIFF 檔案的文字。本教學將一步步說明完整流程，從專案設定到結果輸出，讓你今天就能開始從圖像中提取文字。

## 本教學涵蓋內容

* **如何批量 OCR**，使用 Aspose 的 `OcrBatchProcessor`。
* 從不同格式（PNG、JPG、TIFF）的圖像 **提取文字** 的方式。
* 控制平行度以保持應用程式回應性的技巧。
* 完整、可直接執行的 Java 程式碼，讓你複製貼上後立即運行。

不需要任何 Aspose 的使用經驗——只要有基本的 Java 環境與任意 IDE 即可。完成後，你將具備批量辨識 PNG、JPG、TIFF 檔案文字的堅實基礎。

---

![說明如何批量 OCR 多個圖像檔案的圖示](/images/batch-ocr-diagram.png "如何批量 OCR")

*圖片說明：說明如何批量 OCR 圖示，展示多個圖像檔案一起處理的流程。*

## 前置條件

| 前置條件 | 為何重要 |
|----------|----------|
| Java 17 或更新版本 | Aspose OCR 針對現代 JVM 設計。 |
| Maven 或 Gradle | 簡化加入 Aspose OCR 套件的流程。 |
| 基本的 Java 知識 | 需要了解程式流程。 |
| 一組範例圖像（`.png`、`.jpg`、`.tif`） | 觀察提取結果。 |

如果你已具備上述條件，太好了——讓我們直接開始。

## 步驟 1：將 Aspose OCR 加入專案

首先需要取得 Aspose OCR 的 JAR。使用 Maven 時，將以下內容放入 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

如果你偏好 Gradle，等價的設定如下：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

加入相依性後，系統會自動載入 **recognize text from png**、**recognize text from jpg**、**recognize text from tiff** 所需的全部組件，無需額外的原生函式庫。

## 步驟 2：定義要處理的圖像檔案

接下來告訴 OCR 引擎要處理哪些檔案。這正是 **如何批量 OCR** 發揮威力的地方——只要傳入檔案路徑清單，讓函式庫自行完成繁重工作。

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **專業提示：** 請使用絕對路徑或 `Paths.get(...)`，以避免在不同作業系統上產生意外。

## 步驟 3：建立批次處理器並調整平行度

Aspose OCR 內建 `OcrBatchProcessor`，可同時執行多個辨識任務。限制執行緒數量可防止在處理大量圖像時佔用過多 CPU。

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

為何要限制平行度？在一般筆記型電腦上同時開太多執行緒，可能會導致效能下降而非提升。使用 `setMaxParallelism` 能在速度與穩定性之間取得平衡。

## 步驟 4：執行批次 OCR 呼叫

以下程式碼展示 **如何批量 OCR** 的核心：一次 `recognize` 呼叫，回傳每張圖像對應的 `RecognitionResult` 物件清單。

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

此方法會阻塞，直到所有圖像處理完成，然後返回文字結果。若需要非阻塞行為，可將其包裝在 `CompletableFuture` 中，但對於大多數腳本而言，同步呼叫更簡潔。

## 步驟 5：印出提取的文字

最後，遍歷結果並顯示辨識出的字串。這一步證明我們已成功 **從圖像提取文字**，且支援多種格式。

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### 預期輸出

```
File: YOUR_DIRECTORY/img1.png
The quick brown fox jumps over the lazy dog.
---
File: YOUR_DIRECTORY/img2.jpg
Invoice #12345
Total: $567.89
---
File: YOUR_DIRECTORY/img3.tif
Page 1 of 3
Report generated on 2026-02-09
---
```

若 OCR 引擎無法讀取某個檔案，`getText()` 會回傳空字串，你可以加入簡單的檢查來記錄警告。

## 完整可執行範例

將以下程式碼全部複製到 `BatchOcrTutorial.java`，依需求調整圖像路徑，然後執行 `javac && java`。

```java
import com.aspose.ocr.*;
import java.util.Arrays;
import java.util.List;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/img1.png",
                "YOUR_DIRECTORY/img2.jpg",
                "YOUR_DIRECTORY/img3.tif");

        // Step 2: Create the batch OCR processor and optionally limit parallelism
        OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();
        ocrProcessor.setMaxParallelism(4); // limit to 4 concurrent threads

        // Step 3: Perform OCR on all images in a single batch call
        List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);

        // Step 4: Output the recognized text for each file
        for (int i = 0; i < recognitionResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(recognitionResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

執行後，主控台會依序印出每個 PNG、JPG、TIFF 檔案的提取文字——正是當 **如何批量 OCR** 成為你關注焦點時的理想解決方案。

## 常見問題與特殊情況

### 若圖像超過三張怎麼辦？

只要在 `imageFiles` 清單中再加入條目即可。批次處理器會自動依照 `setMaxParallelism` 設定的執行緒數量分配工作。

### 圖像放在子資料夾，需要手動列出每個檔案嗎？

可以程式化地收集特定副檔名的所有檔案：

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

這樣的寫法保持彈性，同時仍符合 **如何批量 OCR** 的需求。

### 如何處理低信心度的結果？

`RecognitionResult` 提供 `getConfidence()` 方法。你可以過濾低於門檻的結果，並使用較高 DPI 重新嘗試：

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Aspose OCR 支援其他語言嗎？

支援——只要在 `recognize` 前呼叫 `ocrProcessor.setLanguage(OcrLanguage.Spanish)`（或任何支援的列舉），即可辨識非英文文字，讓 **從圖像提取文字** 真正具備多語言能力。

## 效能優化建議

* **批次大小** 會影響效能——較大的批次可減少開銷，但過大可能佔用過多記憶體。建議以 50–200 張圖像為單位測試。
* **平行度**——在四核心 CPU 上，`setMaxParallelism(4)` 通常能取得最佳吞吐量。依照伺服器負載自行調整。
* **圖像前處理**——在 OCR 前將圖像轉為灰階或提升對比度，可提升噪點掃描的辨識率。

## 結論

現在你已掌握在 Java 中使用 Aspose OCR **批量 OCR** 的方法，了解如何 **從圖像提取文字**，以及為何平行度控制如此重要。完整程式碼示範了如何一次性辨識 PNG、JPG、TIFF 檔案。

接下來可以嘗試將 OCR 結果寫入搜尋索引、資料庫，或交給 AI 摘要工具。亦可探索 PDF 輸入（Aspose OCR 支援）或結合 OpenCV 等圖像前處理函式庫，以進一步提升準確度。

祝開發順利，記得批量 OCR 不必是難題。只要選對工具、遵循清晰模式，你就能在短時間內把大量圖片轉換成可搜尋的文字。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}