---
category: general
date: 2026-01-02
description: 使用 Aspose OCR 於 Java 將圖像轉換為文字。精通批次 OCR 處理，從資料夾讀取圖像，並依副檔名過濾檔案。
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: zh-hant
og_description: 將圖像快速轉換為文字（使用 Java）。本教學涵蓋批次 OCR 處理、從資料夾讀取圖像，以及依副檔名過濾檔案。
og_title: 在 Java 中將圖片轉換為文字 – 完整批次 OCR 指南
tags:
- OCR
- Java
- Aspose
title: 將圖像轉換為文字（Java）— 批次 OCR 處理指南
url: /zh-hant/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中將圖像轉換為文字 – 批次 OCR 處理指南

是否曾需要**將圖像轉換為文字**，卻不確定如何一次處理數十個檔案？你並不孤單——開發人員經常需要從 PNG、JPG 以及其他掃描檔案中提取資料。好消息是？使用 Aspose OCR，你可以在幾分鐘內建立批次 OCR 處理管線，從資料夾結構中讀取圖像，甚至依副檔名過濾檔案，讓你只處理重要的部分。

在本教學中，我們將建立一個自包含的 Java 程式，遍歷目錄，挑選每個 `.png` 或 `.jpg`，非同步將每張圖片送至 Aspose OCR，並以原始順序印出擷取的文字。完成後，你將擁有一段可重複使用的程式碼片段，能在任何需要**將圖像轉換為文字**的大規模專案中直接使用。

---

![將圖像轉換為文字範例](https://example.com/convert-images-to-text.png "Java 主控台輸出截圖，顯示從 PNG 檔案轉換的文字")

## 您將建立的內容

- 一個在執行期間於所有執行緒間共享的 `AsposeOCR` 引擎（高效且執行緒安全）。  
- 一個 `ParallelRecognizer`，可平行執行 OCR 工作，完美支援**批次 OCR 處理**。  
- 使用 `java.nio.file.Files` **從資料夾讀取圖像** 的邏輯。  
- 簡易過濾器，可在仍處理 JPG 的同時 **從 PNG 檔案提取文字**。  
- 乾淨的內部執行緒池關閉機制，以避免資源洩漏。

### 前置條件

- Java 17（或任何近期的 LTS 版本）。  
- Maven 或 Gradle 以取得 Aspose OCR 函式庫。  
- 一個包含 PNG/JPG 圖片的資料夾，供你處理。  
- 基本的 Java Stream 使用經驗——不需要任何高階技巧。

> **專業提示：** 如果你還沒有授權，Aspose 提供免費的臨時金鑰，可用於測試。

---

## 步驟 1 – 設定專案並加入 Aspose OCR

首先，建立一個新的 Maven 專案（或 Gradle，視你喜好）。在 `pom.xml` 中加入 Aspose OCR 相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **為什麼這很重要：** 事先宣告相依性可確保編譯器能看到 `AsposeOCR`、`ParallelRecognizer` 以及相關類別。它同時保證所有機器使用相同版本，對於可重現的**批次 OCR 處理**至關重要。

建置完成後，重新整理你的 IDE，應該會在 `External Libraries` 下看到 Aspose 套件。

---

## 步驟 2 – 將圖像轉換為文字 – 初始化 OCR 引擎

整個執行過程只需要**一個** OCR 引擎實例。將它在執行緒間共享可節省記憶體，且因為語言包只載入一次，速度也會更快。

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

> **說明：** `ParallelRecognizer` 會將引擎包裝在執行緒池中。當你提交大量檔案時，每個檔案都會獲得自己的工作執行緒，從而在多核心 CPU 上實現真正的平行運算。

---

## 步驟 3 – 從資料夾讀取圖像 – 遍歷目錄樹

現在我們需要 **從資料夾讀取圖像**，並收集所有 PNG 或 JPG。`Files.walk` API 讓這一步只需一行程式碼，但我們會加入過濾條件，以在需要時 **只從 PNG 提取文字**。

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

> **為什麼在此過濾：** 使用 `filter` 能在早期 **依副檔名過濾檔案**，減少不必要的 I/O。這也讓程式碼更易讀——不必使用複雜的正規表達式。

---

## 步驟 4 – 批次 OCR 處理 – 非同步提交工作

取得檔案清單後，我們將每個路徑推送至 `ParallelRecognizer`。`recognizeAsync` 方法會回傳 `Future<OcrResult>`，我們會將它存起來以便稍後取得。

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

> **底層發生了什麼？** 每次呼叫都會將任務排入 recognizer 內部的 executor service。任務平行執行，因而即使資料夾內有 100 張圖片，也能在單執行緒迴圈所需時間的極小比例內完成處理。

---

## 步驟 5 – 以原始順序取得結果 – 保持檔案序列

因為我們將 futures 按照 `imagePaths` 的順序儲存，只要遍歷清單並呼叫 `get()` 即可。此呼叫僅會阻塞到該圖像完成，無需額外的排序機制即可保留原始順序。

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

**範例主控台輸出**（為簡潔起見已截斷）：

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

> **邊緣案例處理：** 若某張圖像拋出例外（檔案損毀、格式不支援），我們會捕獲例外並繼續處理其餘檔案——這是建立可靠**批次 OCR 處理**管線的必要習慣。

---

## 步驟 6 – 清理 – 關閉 Recognizer

千萬別忘記關閉內部執行緒池，否則 JVM 可能在結束時卡住。

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

就這樣！程式現在可以遍歷任意目錄，過濾 PNG/JPG 檔案，平行執行 OCR，並印出結果。

---

## 完整工作範例

以下是完整、可直接複製貼上的 Java 類別。將 `"YOUR_DIRECTORY"` 替換為你的圖像資料夾路徑，然後在 IDE 或命令列執行。

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

執行此類別，觀察主控台被擷取的字串填滿，並為你**將圖像轉換為文字**而不必寫任何會阻塞 I/O 的迴圈而感到慶祝。

---

## 常見問題 (FAQs)

**Q: 我也可以處理 PDF 或 TIFF 嗎？**  
A: 當然可以。Aspose OCR 支援多種格式，只要在步驟 2 的過濾條件中加入相應的副檔名即可。

**Q: 如果我需要其他語言，例如西班牙文，該怎麼做？**  
A: 將 `RecognitionLanguage.ENGLISH` 改為 `RecognitionLanguage.SPANISH`。請確保已安裝該語言包（Aspose 已內建大多數主要語言）。

**Q: 我的資料夾內有子資料夾——會被掃描嗎？**  
A: 會。`Files.walk` 會遞迴遍歷整個樹狀結構，因此每個巢狀的 PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}