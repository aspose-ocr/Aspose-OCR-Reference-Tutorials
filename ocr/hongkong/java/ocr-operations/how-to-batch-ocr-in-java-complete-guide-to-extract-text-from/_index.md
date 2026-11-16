---
category: general
date: 2026-09-18
description: 了解如何使用 Aspose OCR 在 Java 中提取圖像文字。一次呼叫即可批次處理 PNG、JPG 和 TIFF 檔案，提高效率。
keywords:
- extract text from images
- convert images to text
- how to batch ocr
- extract text from png
- extract text from jpg
- extract text from tiff
lastmod: 2026-09-18
og_description: 精通使用批次 OCR 在 Java 中提取圖像文字。使用 Aspose OCR 一次呼叫即可轉換 PNG、JPG 和 TIFF 檔案。
og_image_alt: Diagram showing multiple image files processed together for batch OCR
og_title: 從 Java 圖像提取文字 – 批次 OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to extract text from images in Java using Aspose OCR. Batch
    process PNG, JPG, and TIFF files efficiently in a single call.
  headline: How to extract text from images in Java by batch OCR
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR is pure Java and requires no UI components, so it works
      perfectly on headless environments.
    question: Can I run this on a headless server?
  - answer: A commercial license is needed for production deployments; a free trial
      is available for evaluation.
    question: Is a license required for production use?
  - answer: Any OS that can run Java 17+, including Windows, Linux, and macOS.
    question: Which operating systems are supported?
  - answer: Over 60 languages are supported out of the box, ranging from English and
      Spanish to Arabic and Chinese.
    question: How many languages can Aspose OCR recognise?
  - answer: Individual image files up to 200 MB are supported; larger files should
      be split before processing.
    question: What is the maximum file size Aspose OCR can handle?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: 如何使用批次 OCR 從 Java 圖像中提取文字
url: /zh-hant/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用批次 OCR 從圖像提取文字

如果您需要快速 **從圖像提取文字**，且不想為每個檔案寫迴圈，批次 OCR 就是答案。在許多實務專案中，您會收到一整個資料夾的掃描檔——PNG 收據、JPG 截圖或多頁 TIFF——必須將它們轉換成可搜尋的文字。Aspose OCR 只需一次方法呼叫，即可同時處理 PNG、JPG 與 TIFF 檔案，為您節省開發時間與 CPU 資源。

## 快速回答
- **批次 OCR 會做什麼？** 它會在一次請求中處理多個圖像檔，並為每個檔案返回文字。
- **支援哪些格式？** 開箱即支援 PNG、JPG/JPEG 與多頁 TIFF。
- **需要額外的原生函式庫嗎？** 不需要，Aspose OCR JAR 已包含所有必需的元件。
- **我可以控制執行的執行緒數量嗎？** 可以，使用批次處理器的 `setMaxParallelism`。
- **需要哪個 Java 版本？** Java 17 或更新版本。

## 什麼是 Aspose OCR？
Aspose OCR 是一個 Java 函式庫，能在圖像檔案中辨識印刷與手寫文字，且不依賴外部套件。它支援超過 60 種語言，且每次批次最多可處理 100 張圖像，適合大規模文件數位化。

## 本教學涵蓋內容
載入圖像路徑清單、建立 `OcrBatchProcessor`、調整平行度、執行單一 `recognize` 呼叫，並印出提取的字串。完成後，您將擁有一個可直接執行的 Java 程式，能批次從 PNG、JPG 與 TIFF 檔案中提取文字。

- **如何使用 Aspose 的 `OcrBatchProcessor` 進行批次 OCR**。
- 各種格式（PNG、JPG、TIFF）**從圖像提取文字** 的方法。
- 控制平行度以保持應用程式回應性的技巧。
- 完整可執行的 Java 程式碼，您可以直接複製貼上並立即執行。

不需要任何 Aspose 的先前經驗——只要有基本的 Java 環境與您慣用的 IDE 即可。完成後，您將具備批次辨識 PNG、JPG 與 TIFF 檔案文字的堅實基礎。

---

![說明如何批次 OCR 多個圖像檔案](/images/batch-ocr-diagram.png "如何批次 OCR")

*圖片說明文字：顯示多個圖像檔案一起處理的批次 OCR 圖示。*

## 前置條件

| 需求 | 原因說明 |
|-------------|----------------|
| Java 17 或更新版本 | Aspose OCR 針對現代 JVM 設計。 |
| Maven or Gradle | 簡化 Aspose OCR 函式庫的加入。 |
| 基本的 Java 知識 | 需要了解程式流程。 |
| 一組範例圖像（`.png`、`.jpg`、`.tif`） | 以觀察提取效果。 |

如果您已具備上述條件，太好了——讓我們開始吧。

## 步驟 1：將 Aspose OCR 加入您的專案

您首先需要的是 Aspose OCR JAR。使用 Maven 時，將以下內容加入您的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

如果您偏好 Gradle，等價的設定如下：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

加入此相依性即可取得 **從 png 提取文字**、**從 jpg 提取文字** 與 **從 tiff 提取文字** 所需的全部元件。無需額外的原生函式庫。

## 步驟 2：定義要處理的圖像檔案

現在我們告訴 OCR 引擎要處理哪些檔案。這正是 **如何批次 OCR** 發揮威力的地方——只要傳入路徑清單，讓函式庫自行完成繁重工作。

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **專業提示：** 請使用絕對路徑或 `Paths.get(...)`，以避免在不同作業系統上出現意外情況。

## 步驟 3：建立批次處理器並調整平行度

Aspose OCR 內建 `OcrBatchProcessor`，可平行執行多個辨識。控制執行緒數量可防止在處理數十張圖像時佔用過多 CPU。

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

為什麼要限制平行度？在一般筆記型電腦上執行過多執行緒，可能會導致效能下降而非提升。設定 `setMaxParallelism` 可讓您在速度與穩定性之間取得平衡。

## 步驟 4：執行批次 OCR 呼叫

以下是 **如何批次 OCR** 的核心：一次 `recognize` 呼叫會返回 `RecognitionResult` 物件清單，每個圖像對應一個結果。  
`recognize` 會處理提供的圖像，並回傳包含提取文字的 `RecognitionResult` 物件清單。

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

此方法會阻塞，直到所有圖像處理完畢，才返回文字。若需要非阻塞行為，可將其包裝於 `CompletableFuture`，但對大多數腳本而言，同步呼叫能保持程式碼簡潔。

## 步驟 5：印出提取的文字

最後，遍歷結果並顯示辨識出的字串。這證明我們已成功 **從各種格式的圖像提取文字**。  
`RecognitionResult` 包含單一圖像的 OCR 輸出，包括提取的文字與信心分數。

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

若 OCR 引擎無法讀取檔案，`getText()` 會回傳空字串，您可以加入簡單檢查以記錄警告。

## 完整範例程式

將所有步驟整合起來，以下是完整且可直接執行的 Java 類別。將其複製到名為 `BatchOcrTutorial.java` 的檔案中，調整圖像路徑後執行 `javac && java`。

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

執行後，您會在主控台看到每個 PNG、JPG 與 TIFF 檔案的提取文字——正是當您心中有 **如何批次 OCR** 的疑問時所需要的。

## 常見問題與邊緣情況

### 如果有超過三張圖像該怎麼辦？

只要在 `imageFiles` 清單中加入更多項目即可。批次處理器會自動依您在 `setMaxParallelism` 設定的執行緒數量分配工作。

### 我的圖像在子資料夾中——需要手動列出每個檔案嗎？

`Files.list` 會回傳目錄中延遲載入的路徑串流。

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

此寫法保持程式碼彈性，同時仍符合 **如何批次 OCR** 的需求。

### 如何處理低信心的結果？

`getConfidence()` 會回傳數值型的信心分數，表示辨識文字的正確可能性。

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Aspose OCR 支援其他語言嗎？

是的——在 `recognize` 呼叫前使用 `ocrProcessor.setLanguage(OcrLanguage.Spanish)`（或任何支援的列舉）即可。這讓功能不僅限於英文，使 **從圖像提取文字** 真正具備多語言能力。

## 效能建議

* **批次大小很重要** – 較大的批次可減少開銷，但過大的清單可能佔用較多記憶體。建議以 50–200 張圖像為一批進行測試。
* **平行度** – 在四核心 CPU 上，`setMaxParallelism(4)` 通常能取得最佳吞吐量。請依伺服器工作負載調整。
* **圖像前處理** – 在 OCR 前將圖像轉為灰階或提升對比度，可提升準確度，特別是對噪點較多的掃描件。

## 結論

現在您已了解如何在 Java 中使用 Aspose OCR **批次 OCR**、如何 **從各種格式的圖像提取文字**，以及為何控制平行度很重要。完整的程式碼範例示範了在一次高效呼叫中辨識 PNG、JPG 與 TIFF 檔案的文字。

準備好進一步嗎？將 OCR 輸出導入搜尋索引、資料庫或 AI 摘要工具。您也可以嘗試 PDF 輸入（Aspose OCR 支援）或結合 OpenCV 等圖像前處理函式庫，以獲得更高的準確度。

祝開發順利，請記得——批次 OCR 不必是頭痛的問題。只要使用合適的工具與清晰的模式，您就能快速將大量圖片轉換為可搜尋的文字。

## 常見問答

**Q: 我可以在無頭伺服器上執行嗎？**  
A: 可以，Aspose OCR 完全基於 Java，無需 UI 元件，因而在無頭環境中亦能正常運作。

**Q: 生產環境需要授權嗎？**  
A: 需要商業授權才能於生產環境部署；亦提供免費試用供評估使用。

**Q: 支援哪些作業系統？**  
A: 任何能執行 Java 17+ 的作業系統，包括 Windows、Linux 與 macOS。

**Q: Aspose OCR 能辨識多少種語言？**  
A: 開箱即支援超過 60 種語言，從英語、西班牙語到阿拉伯語與中文皆在支援範圍內。

**Q: Aspose OCR 能處理的最大檔案大小為何？**  
A: 單一圖像檔案最高支援 200 MB；若檔案更大，請先分割後再處理。

---

**最後更新：** 2026-09-18  
**測試環境：** Aspose OCR 24.9 for Java  
**作者：** Aspose

## 相關教學

- [從圖像提取文字 – Java OCR 基礎](/ocr/java/ocr-basics/)
- [如何在 Java 中批次 OCR 完整指南 – 提取文字](/ocr/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/)
- [在 Java 中前處理圖像 OCR 提升準確度 – 提取文字](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}