---
category: general
date: 2026-02-27
description: 學習如何在 Java 中使用 OCR，透過 Aspose OCR 的平行處理，從 TIFF 與 PDF 檔案中提取圖像文字。快速、簡單的指南。
draft: false
keywords:
- how to use ocr
- perform ocr on pdf
- extract text from tiff
- extract image text java
language: zh-hant
og_description: 學習如何在 Java 中使用 OCR，透過 Aspose OCR 的平行處理，從 TIFF 與 PDF 檔案中提取圖像文字。
og_title: 如何在 Java 中使用 OCR – 與 Aspose 的平行處理
tags:
- OCR
- Java
- Aspose
title: 如何在 Java 中使用 OCR – 使用 Aspose 進行平行處理
url: /zh-hant/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 OCR – 使用 Aspose 進行平行處理

有沒有想過 **如何使用 OCR** 從掃描文件中提取文字而不費吹灰之力？你並不是唯一有此疑問的人。開發人員在需要從圖像（尤其是 TIFF 和 PDF）中讀取文字，同時保持效能時，常常會碰壁。  

在本教學中，我們將示範一個完整、可直接執行的解決方案，使用 Aspose OCR **在 Java 中提取圖像文字**、開啟平行處理，甚至讓你限制執行緒數量。完成後，你將擁有一個單一類別，能夠 **在 PDF 上執行 OCR** 並 **從 TIFF 圖像提取文字**，速度遠快於單執行緒的做法。

> **學完你會得到什麼**  
> * 為何平行 OCR 重要的清晰說明。  
> * 完整的 Java 程式（不缺少匯入）。  
> * 調整執行緒使用與處理常見陷阱的技巧。  

## 前置條件

- Java 8 或更新版本（程式碼亦可在 JDK 11 上編譯）。  
- Aspose.OCR for Java 套件 – 可從 Maven Central 取得最新 JAR（`com.aspose:aspose-ocr`）。  
- 一個圖像檔案（`.tif`、`.tiff`）或想要處理的 PDF。  
- 适量的記憶體—平行處理會啟動多個執行緒，但 Aspose 記憶體使用效率高。

如果你已具備上述條件，讓我們開始吧。

![顯示 OCR 流程圖 – 如何在 Java 中使用 OCR 進行平行處理](how-to-use-ocr-pipeline.png)

*圖片說明：如何使用 OCR 範例圖*

---

## 第 1 步：設定專案並加入 Aspose OCR

### 為何這很重要

在 **在 PDF 上執行 OCR** 或任何圖像之前，必須先將程式庫放入 classpath。若缺少此套件，編譯器會拋出 `ClassNotFoundException`，導致卡在第二步。

### 如何操作

如果你使用 Maven，加入以下相依性：

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

Gradle 則使用：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **專業提示：** 請將版本號與 Aspose 發行說明保持同步；較新版本通常包含平行處理的效能改進。

---

## 第 2 步：建立 OCR 引擎並啟用平行處理

### 為何這很重要

預設情況下 Aspose OCR 只使用單一執行緒。當你處理多頁 PDF 或大量 TIFF 時，引擎會逐頁處理——既慢又低效。啟用平行處理可讓 CPU 同時處理多頁，顯著縮短執行時間。

### 程式碼

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Path to the input file (TIFF or PDF)
        String inputPath = "YOUR_DIRECTORY/input.tif";

        // 2️⃣ Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Turn on parallel processing – this is the core of how to use OCR efficiently
        ocrEngine.getConfig().setUseParallelProcessing(true);

        // 4️⃣ (Optional) Limit threads – you can cap it to the number of cores you have
        // ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors());

        // 5️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.processImage(inputPath);

        // 6️⃣ Output the recognised text
        System.out.println(ocrResult.getText());
    }
}
```

**關鍵程式行說明**

- `setUseParallelProcessing(true)`：告訴 Aspose 將工作負載分散至可用的 CPU 核心。  
- `setMaxThreads(...)`：若在共享伺服器上或想為其他服務保留資源，可限制執行緒池的大小。  
- `processImage(inputPath)`：同時支援圖像檔與 PDF 文件，因此同一呼叫即可 **在 PDF 上執行 OCR**，亦可處理 TIFF。

---

## 第 3 步：處理不同的輸入類型 – PDF 與 TIFF

### 為何這很重要

雖然 `processImage` 接受路徑字串，但底層處理方式不同。PDF 通常包含多頁，每頁會變成獨立的 OCR 工作。TIFF 可能是單頁或多頁；Aspose 會將每個影格視為一頁。

### 注意事項

| 輸入 | 常見問題 | 推薦解決方案 |
|------|----------|--------------|
| PDF | 大型 PDF 若同時載入所有頁面可能耗盡記憶體。 | 使用 `ocrEngine.getConfig().setMemoryOptimization(true);`（新版本可用）。 |
| 多頁 TIFF | 部分舊版 TIFF 使用不支援的壓縮方式。 | 先轉換為支援的格式，或使用 Aspose 的 `TiffImage` 輔助類別。 |

以下是一段快速程式碼範例，示範如何偵測檔案類型並記錄友善訊息：

```java
import java.nio.file.*;

String ext = Files.probeContentType(Paths.get(inputPath)).toLowerCase();
if (ext.contains("pdf")) {
    System.out.println("Processing a PDF – expect multiple pages.");
} else if (ext.contains("tiff") || ext.contains("tif")) {
    System.out.println("Processing a TIFF image.");
} else {
    System.out.println("Unsupported file type. This demo works with PDF and TIFF.");
}
```

---

## 第 4 步：驗證輸出 – 會看到什麼？

當程式執行完畢，會在主控台印出原始擷取的文字。以簡單的掃描發票為例，輸出可能如下：

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

若 OCR 在某頁無法辨識，Aspose 會插入占位行 `[Unrecognizable]`。之後可自行過濾，以取得乾淨的資料。

**快速檢查**

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

---

## 第 5 步：微調效能 – 何時調整執行緒數量

### 為何這很重要

執行緒數量多不一定代表更快。在四核心筆記型電腦上啟動八個執行緒可能產生上下文切換開銷。相反地，在 32 核心的伺服器上，你可能想釋放全部資源。

### 找到最佳設定的方法

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

以不同設定執行程式並計時：

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

記錄各次執行時間，挑選效能最高的組合，並在正式環境中固定使用。

---

## 第 6 步：擴充示範 – 批次處理多個檔案

如果需要 **從整個資料夾中提取圖像文字 java**，可將核心邏輯包在迴圈中：

```java
Path folder = Paths.get("YOUR_DIRECTORY");
try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder, "*.{tif,tiff,pdf}")) {
    for (Path file : stream) {
        System.out.println("\n--- Processing: " + file.getFileName() + " ---");
        OcrResult result = ocrEngine.processImage(file.toString());
        // Save or further process result.getText()
    }
}
```

此模式相當可擴展，因為引擎已在每個檔案的頁面上平行執行。外層迴圈為順序執行，若需飽和大量 CPU，可改為將每個檔案提交給 `ExecutorService`。

---

## 常見陷阱與避免方法

| 症狀 | 可能原因 | 解決方案 |
|------|----------|----------|
| `OutOfMemoryError` | 同時載入過多頁面（尤其是巨大的 PDF）。 | 開啟記憶體最佳化 (`setMemoryOptimization(true)`) 或改用 `processPage` 逐頁處理 PDF。 |
| 文字亂碼 | 語言/字元集設定錯誤。 | 呼叫 `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` 或相應的語言列舉。 |
| 雖已開啟平行旗標仍慢 | 作業系統限制執行緒建立或 JVM 設定了過低的堆積大小。 | 增加 `-Xmx` 堆積參數，並檢查 OS 執行緒上限 (`ulimit -u`)。 |
| 輸出空白 | 輸入影像解析度低於 300 dpi。 | 在 OCR 前提升影像解析度，或使用更高解析度的掃描器。 |

---

## 重點回顧 – 本文涵蓋內容

- 使用 Aspose 的 `OcrEngine` **在 Java 中使用 OCR**。  
- 啟用 **平行處理**，加速 **在 PDF 上執行 OCR** 與 **從 TIFF 提取文字**。  
- 調整執行緒數量以取得最佳效能。  
- 處理大型 PDF、多頁 TIFF 與語言設定等邊緣案例。  
- 將單檔示範擴展為可應付實務工作負載的批次處理器。

---

## 後續步驟

既然已掌握基礎，建議進一步探索以下相關主題：

- **從手寫筆記中提取圖像文字 java**（啟用 `setHandwritingRecognition(true)`）。  
- 結合 Apache Tika 進行 OCR 輸出之中繼資料抽取。  
- 將結果儲存至 Elasticsearch，建構可搜尋的文件庫。  
- 使用 Aspose OCR 搭配其他語言，如 Python 或 .NET——原理相同。

盡情嘗試不同的執行緒上限、影像格式與語言套件。玩得越多，對速度與準確度之間的取捨就會越了解。

### 祝編程愉快！

若在實作過程中遇到任何問題或有進一步優化的想法，歡迎在下方留言。我隨時樂於討論 OCR 小技巧——不費吹灰之力，只要寫程式。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}