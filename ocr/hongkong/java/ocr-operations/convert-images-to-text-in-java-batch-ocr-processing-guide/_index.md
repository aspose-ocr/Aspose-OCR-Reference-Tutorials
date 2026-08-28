---
category: general
date: 2026-08-28
description: 了解如何在 Java 中使用 Aspose OCR 從 png 圖像提取文字。本教學涵蓋 batch OCR processing、reading
  images from a folder 以及 filtering files by extension。
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: 了解如何在 Java 中使用 Aspose OCR 從 png 圖像提取文字。本教學涵蓋 batch OCR processing、reading
  images from a folder 以及 filtering files by extension。
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: 如何在 Java 中從 png 提取文字 – batch OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: 如何在 Java 中從 png 提取文字 – batch OCR 指南
url: /zh-hant/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中從 png 提取文字 – 批次 OCR 指南

如果你曾經需要 **從 png 提取文字** 檔案，但不確定如何將操作規模擴展到多於少量圖片，你來對地方了。許多開發者從單張圖片的 OCR 呼叫開始，當資料夾增至數十或數百個檔案時，便會迅速碰到效能瓶頸。使用 Aspose OCR for Java，你可以建立一個強大的批次 OCR 流程，遍歷目錄、僅篩選你關心的影像類型、平行執行辨識，並以與來源檔案相同的順序返回結果。閱讀完本指南後，你將擁有一段可直接使用的 Java 程式碼，可靠且高效地處理 **批次 OCR 處理**。

![將影像轉換為文字範例](https://example.com/convert-images-to-text.png "Java 主控台輸出螢幕截圖，顯示從 PNG 檔案轉換的文字")

## 快速解答
- **什麼函式庫負責 OCR？** Aspose OCR for Java.
- **我可以同時處理 PNG 與 JPG 嗎？** 是的 – 範例會同時篩選兩種副檔名。
- **OCR 引擎是執行緒安全的嗎？** 單一共享的 `AsposeOCR` 實例在並行使用時是安全的。
- **測試需要授權嗎？** 可從 Aspose 取得免費的臨時金鑰。
- **子資料夾會自動被掃描嗎？** `Files.walk` 會遞迴遍歷整個目錄樹。

## 什麼是從 png 提取文字？

`extract text from png` 指的是對 Portable Network Graphics（PNG）檔案套用光學字符辨識（OCR）的過程，將可見的字符轉換為可搜尋、可編輯的字串。Aspose OCR 的引擎會讀取像素資料、辨識字形，並在一次方法呼叫中返回 Unicode 文字。

## 為什麼使用 Aspose OCR for Java？

Aspose OCR 支援 **30 多種語言**，在標準 8 核心伺服器上每分鐘可處理高達 **500 張影像**，且能處理最高 **200 MB** 的檔案而不需將整張影像載入記憶體。這些具體的效能指標意味著，你可以在一般硬體上可靠地執行大規模批次工作，而不會觸及記憶體上限。

## 前置條件
- Java 17（或任何近期的 LTS 版本）。
- Maven 或 Gradle 用於相依管理。
- 包含欲處理的 PNG/JPG 影像的目錄。
- 具備 Java Streams 與 `java.nio.file` 套件的基本知識。
- （可選）用於評估的 Aspose OCR 臨時授權金鑰。

> **專業提示：** 免費的臨時金鑰在 30 天後過期，但它可讓你在測試時完整存取 API。

## 批次 OCR 流程如何保持順序？

`Future<OcrResult>` 代表一個待處理的 OCR 結果，處理完成後即可取得。流程透過將 `Future<OcrResult>` 物件存放在與輸入 `Path` 集合順序相同的清單中，來保留原始檔案順序。稍後當你遍歷這些 futures 並呼叫 `get()` 時，每次呼叫只會阻塞對應的影像，因此輸出序列與輸入序列相符，無需額外排序邏輯。

## 什麼是 Aspose OCR for Java？

`AsposeOCR` 是 Aspose OCR 函式庫的核心類別，封裝了所有語言套件、辨識設定與內部原生資源。它設計為在應用程式生命週期內只實例化一次，並可安全地在多執行緒間共享。由於語言資料僅載入一次，重複使用同一實例可減少初始化開銷，提升批次操作的吞吐量。

## 如何設定專案並加入 Aspose OCR

首先，建立一個 Maven（或 Gradle）專案，並在 `pom.xml` 中加入 Aspose OCR 的相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **為什麼這很重要：** 事先宣告相依性可確保編譯器能找到 `AsposeOCR`、`ParallelRecognizer` 以及相關類別。它同時保證所有機器使用相同版本，對於可重現的 **批次 OCR 處理** 至關重要。

建置完成後重新整理 IDE；你應該會在 **External Libraries** 下看到 Aspose 套件。

## 如何初始化 OCR 引擎 – 共享單一實例

`AsposeOCR` 是 Aspose OCR 函式庫提供的主要 OCR 引擎類別。我們在整個執行過程中只需要 **一個** OCR 引擎實例。將它在執行緒間共享可節省記憶體，並加快速度，因為引擎只會載入一次語言套件。

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` 為執行緒安全的，因此你可以安全地將它交給 `ParallelRecognizer`，由其管理工作執行緒池。

> **說明：** `ParallelRecognizer` 將引擎包裝在執行緒池中。當你提交多個檔案時，每個檔案都會獲得自己的工作執行緒，從而在多核心 CPU 上實現真正的平行處理。

## 如何從資料夾讀取影像 – 遍歷目錄樹

`Files.walk` 是 Java NIO 的方法，可遞迴遍歷檔案樹並回傳 `Path` 物件的串流。現在我們需要 **從資料夾讀取影像**，並收集所有 PNG 或 JPG。`Files.walk` API 讓這一步變成單行程式碼，但我們會加入過濾條件，只在需要時 **從 png 提取文字**。

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **為什麼在此過濾：** 使用 `filter` 讓我們能夠提前 **依副檔名過濾檔案**，減少之後不必要的 I/O。它也讓程式碼更易讀——無需使用複雜的正規表達式。

## 如何非同步提交 OCR 工作

`recognizeAsync` 將影像提交給 OCR 引擎進行非同步處理，並回傳代表待處理結果的 `Future<OcrResult>`。當檔案清單準備好後，我們將每個路徑推送至 `ParallelRecognizer`。`recognizeAsync` 方法回傳的 `Future<OcrResult>` 會被儲存以供之後取得。

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **底層發生了什麼？** 每次呼叫都會將任務排入 recognizer 內部的執行緒服務。任務平行執行，因此含有 100 張影像的資料夾可在單執行緒迴圈所需時間的一小部分內完成處理。

## 如何在保留檔案順序的同時取得結果

`Future<OcrResult>` 保存非同步 OCR 任務的結果，並提供 `get()` 方法取得辨識文字。由於我們以與 `imagePaths` 相同的順序儲存 futures，僅需遍歷清單並呼叫 `get()`。此呼叫只會阻塞至該影像完成，從而在不需額外記錄的情況下保留順序。

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**範例主控台輸出**（為簡潔起見已截斷）：

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **邊緣案例處理：** 若某張影像拋出例外（檔案損毀、不支援的格式），我們會捕獲並繼續處理其餘影像——這是可靠 **批次 OCR 處理** 流程的必要習慣。

## 如何清理資源 – 關閉 recognizer

`ParallelRecognizer.shutdown()` 會停止內部執行緒池，確保所有 OCR 任務在應用程式退出前完成。千萬別忘記關閉內部執行緒池，否則 JVM 可能在退出時掛起。

```java
recognizer.shutdown();
```

就這樣！程式現在可以遍歷任何目錄，篩選 PNG/JPG 檔案，平行執行 OCR，並以原始順序列印結果。

---

## 完整可執行範例（複製貼上）

以下是完整、可直接執行的 Java 類別。將 `"YOUR_DIRECTORY"` 替換為你的影像資料夾路徑，然後在 IDE 或命令列執行它。

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

執行此類別，觀察主控台充滿提取出的字串，並慶祝你已 **將影像轉換為文字**，且未撰寫任何會在 I/O 上阻塞的迴圈。

---

## 常見問題 (FAQs)

**Q: 我也可以處理 PDF 或 TIFF 嗎？**  
A: 當然可以。Aspose OCR 支援超過 30 種格式——包括 PDF、TIFF、BMP 與 GIF——只要在目錄遍歷步驟的過濾條件中加入相應的副檔名即可。

**Q: 如果需要除英文之外的語言，例如西班牙文，該怎麼做？**  
A: 將 `RecognitionLanguage.ENGLISH` 改為 `RecognitionLanguage.SPANISH`（或任何支援的語言）。語言套件已隨函式庫捆綁，無需額外下載。

**Q: 我的資料夾包含子資料夾——會被掃描嗎？**  
A: 會。`Files.walk` 會遞迴遍歷整個樹狀結構，因此每個巢狀的 PNG/J

**Q: 如何處理超過 200 MB 的超大型影像？**  
A: 透過呼叫 `ocrEngine.setUseStreaming(true)` 開啟串流模式。這會指示引擎分塊讀取影像，顯著降低峰值記憶體使用量。

**Q: 有方法限制同時執行的 OCR 執行緒數量嗎？**  
A: 有。建立 `ParallelRecognizer` 時，將想要的最大執行緒數作為第二個參數傳入（例如 `new ParallelRecognizer(ocrEngine, 4)`）。

---

**最後更新：** 2026-08-28  
**測試環境：** Aspose OCR for Java 24.10  
**作者：** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## 相關教學

- [在 Java 中批次 OCR 處理的影像轉文字指南](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [在 Java 中讀取影像文字的完整 Aspose OCR 指南](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [使用 Aspose.OCR 從影像提取文字 – 允許的字符](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}