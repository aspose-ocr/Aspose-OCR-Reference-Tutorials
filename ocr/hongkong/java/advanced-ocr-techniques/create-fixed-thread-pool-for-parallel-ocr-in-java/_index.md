---
category: general
date: 2026-05-03
description: 在 Java 中建立固定執行緒池，以快速從圖像中提取文字。了解如何執行 OCR、將圖像轉換為文字，並透過平行 OCR 處理提升效能。
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: zh-hant
og_description: 在 Java 中建立固定執行緒池，以快速從圖像提取文字。學習如何執行 OCR、將圖像轉換為文字，並透過平行 OCR 處理提升效能。
og_title: 在 Java 中建立固定執行緒池以進行平行 OCR
tags:
- Java
- OCR
- Multithreading
title: 在 Java 中建立固定執行緒池以進行平行 OCR
url: /zh-hant/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 為 Java 建立固定執行緒池以平行執行 OCR

是否曾需要 **建立固定執行緒池** 來加速 OCR 工作，但不知從何下手？你並不孤單。在許多以影像為主的專案中，瓶頸往往是單執行緒的 OCR 呼叫，而解決方式其實相當簡單：啟動一個工作執行緒池，讓它們平行處理檔案。

在本教學中，你將學會如何使用 Aspose OCR **從影像中擷取文字**、如何 **有效率地執行 OCR**，以及如何 **將影像轉換為文字** 而不會讓 CPU 爆炸。完成後，你將擁有一個可直接執行的 Java 程式，示範 **平行 OCR 處理** 在數張範例圖片上的運作。

## 你將會建立什麼

我們會組合一個小型主控台應用程式，具備以下功能：

* 讀取一系列影像路徑（PNG、JPG、TIFF、BMP）。
* **建立固定執行緒池**，大小依 CPU 核心數決定。
* 為每張影像分派一個 OCR 任務。
* 收集辨識出的文字並印出到主控台。
* 整潔地關閉執行緒服務。

不需要外部建置工具、也不需要花俏框架——只要純 Java 加上 Aspose OCR 函式庫。只要你有 Java 8+ 與一個不錯的 IDE，就可以開始。

## 前置條件

* **Java Development Kit (JDK) 8 或更新版本** – 程式碼使用 lambda，舊版會編譯失敗。
* **Aspose OCR for Java** – 從 Aspose 官方網站下載 JAR，或透過 Maven (`com.aspose:aspose-ocr`) 取得。
* 一個放置測試影像的資料夾（程式碼指向 `YOUR_DIRECTORY`）。  
* 基本的 Java 並行程式設計概念（其餘會在教學中說明）。

> *小技巧：* 若使用 Maven，將相依性加入 `pom.xml`，讓 IDE 自動處理 classpath。

---

## 步驟 1：加入必要的匯入

首先，將我們需要的類別匯入。這不只是樣板程式碼；每個匯入都告訴 JVM OCR 引擎、影像處理工具與並行工具的所在位置，讓我們能 **建立固定執行緒池**。

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – 核心 OCR API。  
* `java.util.*` – 用於儲存影像路徑與結果的集合。  
* `java.util.concurrent.*` – 包含 `ExecutorService` 與 `Future` 的並行套件。

---

## 步驟 2：定義要處理的影像

接著，我們列出想要 **從影像中擷取文字** 的檔案。使用 `Arrays.asList` 可讓程式碼保持簡潔，且不必修改其他邏輯即可換成自己的目錄。

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

隨意新增更多項目；執行緒池會依 CPU 核心數自動調整規模。

---

## 步驟 3：**建立固定執行緒池** 以符合 CPU 核心數

這是本教學的核心。我們先取得可用的核心數，然後讓 `Executors` 工廠產生大小恰好的執行緒池。為什麼要固定？因為可預測的執行緒數量可避免「執行緒爆炸」的問題，免得耗盡作業系統資源。

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` 會回傳邏輯核心數（含超執行緒）。  
* `newFixedThreadPool(coreCount)` 確保永遠不會超過 CPU 的承載上限，這是 **平行執行 OCR** 最安全的方式。

---

## 步驟 4：為每張影像提交 OCR 任務

現在，我們把每個檔案路徑轉成一個 callable，**執行 OCR**、辨識文字，並回傳結果。請注意，我們在 lambda 內部新建 `OcrEngine`，避免執行緒間共享引擎狀態而產生不安全問題。

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* 每次 `submit` 都把 lambda 交給執行緒池，由空閒執行緒排程執行。  
* `Future<String>` 物件讓我們稍後取得辨識文字，若需要也能保留原本的順序。

---

## 步驟 5：取得並顯示辨識出的文字

所有任務排入佇列後，我們只要遍歷 `Future` 清單，呼叫 `get()` 讓程式阻塞至每個 OCR 工作完成。這裡就是 **將影像轉換為文字** 的實作：`engine.getText()` 會回傳原始字串。

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

典型的主控台輸出如下：

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

如果檔案處理失敗（例如檔案損毀），會看到以 `Failed:` 開頭的行，後面接檔案路徑——方便快速除錯。

---

## 步驟 6：清理 Executor Service

千萬別忘記關閉執行緒池，否則 JVM 可能會因為仍有工作在執行而無法結束。優雅的關閉會讓已在執行的任務完成後才結束程式。

```java
executor.shutdown();
```

如果需要設定逾時，可再呼叫 `awaitTermination`，但對大多數命令列工具而言，直接 `shutdown()` 已足夠。

---

## 完整範例程式

以下是完整、可直接執行的程式碼。將它貼到 `ParallelOcrTutorial.java` 檔案中，調整影像路徑後，照常使用 `javac` + `java` 編譯執行。

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**預期結果：** 每張影像的文字內容會依 `imagePaths` 清單的順序印出到主控台。若有影像無法處理，則會顯示失敗訊息而不是空白行。

---

## 常見問題與邊緣情況

### 如果影像數量超過執行緒數量？

固定執行緒池會自動將多餘的任務排入佇列。當某個執行緒完成目前的 OCR 工作後，就會接著處理下一個。這種排程行為正是 **平行 OCR 處理** 的精髓——在不超載 CPU 的前提下取得最高吞吐量。

### 可以更換語言嗎？

當然可以。將 `engine.getLanguage().setEnglish(true);` 換成相應的語言旗標，例如 `setFrench(true)`，或在 `recognize()` 前呼叫多個 setter 以同時啟用多種語言。

### 如何處理非常大的影像？

大型檔案會佔用每個執行緒大量記憶體。若出現 `OutOfMemoryError`，可考慮在送給引擎前先縮小影像，或使用 `-Xmx` 增加 JVM 堆積大小。另一種做法是改用 **cached thread pool** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}