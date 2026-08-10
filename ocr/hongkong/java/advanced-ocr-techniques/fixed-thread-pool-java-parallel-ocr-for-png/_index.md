---
category: general
date: 2026-02-17
description: 學習如何使用 Java 的固定執行緒池，對 PNG 圖像進行平行 OCR 辨識以提取文字，並正確關閉執行服務。
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: zh-hant
og_description: 了解如何使用固定執行緒池的 Java 並行從 PNG 圖像提取文字、轉換掃描頁面的文字，並安全關閉執行服務。
og_title: 固定執行緒池 Java – PNG 平行 OCR
tags:
- java
- ocr
- multithreading
- aspose
title: 固定執行緒池 Java – PNG 並行 OCR
url: /zh-hant/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

.

Let's assemble.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 固定執行緒池 Java – PNG 並行 OCR

有沒有想過如何使用 **fixed thread pool java** 加速大量 PNG 檔案的 OCR？在本教學中，我們將逐步說明如何並行 **extract text from PNG** 圖片、將 **convert scanned pages text** 轉換為可編輯的字串，並在工作完成後安全地 **shut down executor service**。

如果你曾經盯著一個單執行緒的迴圈耗費數分鐘，你一定了解在每頁完成之前必須等待的沮喪。好消息是，只要幾行 Java 程式碼加上 Aspose OCR，你就能釋放所有 CPU 核心的效能，將掃描頁面轉換為可搜尋的文字，並保持應用程式的回應性。  

以下你會找到一個完整、可直接執行的範例，並附上每個部分重要性的說明、常見陷阱，以及可套用於任何 OCR 函式庫的技巧。

---

## 你需要的條件

- **Java 17**（或任何較新的 JDK）——程式碼僅少量使用現代的 `var` 語法，但在較舊版本上亦可運作。  
- **Aspose.OCR for Java** 函式庫——你可以從 Maven Central 取得，或從 Aspose 下載試用版。  
- 一組你想要處理的 **PNG** 檔案——例如掃描收據、書本頁面或螢幕截圖。  
- 對 Java 並發有基本了解——非必須，但會有幫助。

就是這樣。無需外部服務、無需 Docker，只要純粹的 Java 加上一點多執行緒的魔法。

---

## 步驟 1：新增 Aspose OCR 相依性與授權（可選）

首先，確保 Aspose OCR JAR 已加入你的 classpath。若使用 Maven，請加入以下內容：

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

如果沒有授權，函式庫會以評估模式執行；程式碼仍可正常運作。若要載入授權（建議於正式環境使用），請將 `Aspose.OCR.lic` 放置於 resources 資料夾，並使用以下程式碼：

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **專業提示：** 請將授權檔案置於版本控制系統之外，以免意外洩漏。

---

## 步驟 2：建立執行緒安全的 `OcrEngine` 實例

只要在各任務間重複使用同一個實例，Aspose OCR 的 `OcrEngine` 即為執行緒安全。只建立一次即可節省記憶體，並避免每張影像都重新初始化引擎的開銷。

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

為什麼要重複使用？可以把引擎想像成一位需要載入語言模型到記憶體的重量級工作者。每張影像都產生一個新引擎，就像為每個小任務都聘請一位新專家——既昂貴又沒必要。

---

## 步驟 3：設定 Fixed Thread Pool Java

現在登場的是本教學的主角：**fixed thread pool java**。我們會將其大小設定為邏輯處理器的數量，讓每個核心都有工作而不會過度分配。

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

使用 *fixed*（固定）池（而非 cached）可讓資源使用更可預測，並避免在一次收到數百張影像時出現可怕的「記憶體不足」尖峰。

---

## 步驟 4：列出要處理的 PNG 檔案（Extract Text from PNG）

收集想要 OCR 的影像路徑。在實際專案中，你可能會掃描目錄或從資料庫讀取；此處我們直接硬編碼幾個範例。

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **注意：** 檔案副檔名 **png** 很重要，因為 Aspose OCR 會自動偵測格式，但你也可以提供 JPEG 或 TIFF。

---

## 步驟 5：提交 OCR 任務 – Parallel OCR Processing

每張影像會變成一個 Callable，回傳辨識出的文字。由於 `OcrEngine` 為共享實例，我們只需將檔案路徑傳入任務即可。

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

為什麼要用 `Future` 包起來？它讓我們能立即發送所有工作，之後再依提交順序收集結果——在 **convert scanned pages text** 回到文件時，能完美保留頁面順序。

---

## 步驟 6：取得結果並顯示（Convert Scanned Pages Text）

現在我們等待每個 `Future` 完成並印出結果。`get()` 呼叫只會阻塞至該任務完成，而不會阻塞整個執行緒池。

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

典型的主控台輸出如下：

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

如果你想將結果寫入檔案，只需將 `System.out.println` 改為 `Files.writeString` 呼叫即可。

---

## 步驟 7：乾淨地關閉 Executor Service

當所有任務完成後，務必 **shut down executor service**；否則 JVM 可能會保留非 daemon 執行緒，導致無法正常結束。

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

`awaitTermination` 模式讓執行緒池有機會在被強制關閉前完成未完成的工作。忽略此步驟是長時間執行的應用程式常見的記憶體泄漏來源。

---

## 完整範例程式

將上述所有步驟整合起來，以下是完整程式碼，你可以直接複製貼上到 `ParallelBatchDemo.java` 並執行：

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}