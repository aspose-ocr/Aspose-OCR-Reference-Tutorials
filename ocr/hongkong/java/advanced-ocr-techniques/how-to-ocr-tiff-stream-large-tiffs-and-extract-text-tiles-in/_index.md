---
category: general
date: 2026-04-29
description: 學習如何使用 Aspose OCR 串流模式對 TIFF 檔案進行 OCR。本指南將向您展示如何高效地從分割式 TIFF 圖像中提取文字瓦片。
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: zh-hant
og_description: 如何使用 Aspose OCR 串流對 TIFF 進行 OCR。逐步程式碼，從大型 TIFF 圖像中提取文字區塊。
og_title: 如何 OCR TIFF – 完整串流指南
tags:
- OCR
- Java
- Aspose
- TIFF
title: 如何 OCR TIFF – 在 Java 中串流大型 TIFF 並提取文字瓦片
url: /zh-hant/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何 OCR TIFF – 在 Java 中串流大型 TIFF 並提取文字區塊

有沒有想過 **how to ocr tiff** 檔案太大而無法一次載入記憶體？你並非唯一遇到此問題的人。許多開發者在 TIFF 影像被切割成數十個區塊時卡住，而一般的 `ocrEngine.recognize()` 呼叫會直接失效。  

好消息是？Aspose OCR 的串流模式允許你將每個區塊作為獨立的串流輸入，從而 **extract text tiles** 而不會耗盡堆積記憶體。本文將逐步說明一個完整、可直接執行的 Java 範例，解釋每行程式碼的意義，並指出需要避免的陷阱。

> **你將得到：** 一個可執行的程式，能即時拼接分割的 TIFF、列印合併後的文字，並示範如何將程式碼套用到其他語言或影像格式。

---

## 前置條件

- **Java 17** 或更新版本（程式碼使用 try‑with‑resources，JDK 8+ 亦可執行，但 JDK 17 為目前的 LTS）。
- **Aspose.OCR for Java** 套件（v23.10 或更新）。透過 Maven 加入：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- 一個包含各個 TIFF 區塊的資料夾（例如 `tile_0.tif`、`tile_1.tif`、…）。  
- 可選：IntelliJ IDEA 或 VS Code 等 IDE——但簡易文字編輯器亦可使用。

---

## Step 1 – 準備區塊路徑（為何重要）

在 OCR 引擎能執行任何操作之前，必須先知道每張影像片段的所在位置。硬編碼路徑對示範而言沒問題，但在正式環境中通常會掃描目錄或讀取清單檔。

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **專業提示：** 請保持區塊的字典序（0、1、2…），因為引擎會依你提供串流的順序串接辨識出的文字。

---

## Step 2 – 為 OCR 引擎啟用串流模式（主要關鍵字）

現在建立 `OcrEngine` 實例並開啟串流。這正是 **how to ocr tiff** 而不必一次載入整張影像的核心。

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**為何使用串流？**  
呼叫 `setEnableStreaming(true)` 後，引擎會將每個傳入的 `ImageStream` 視為前一個的延續，於內部建立虛擬畫布，虛擬拼接區塊，最後一次性執行 OCR。如此即可避免在一次載入多 GB TIFF 時產生的 “OutOfMemoryError”。

---

## Step 3 – 將每個區塊加入為 Input Stream（次要關鍵字）

以下迴圈負責把每個區塊餵給引擎。`try‑with‑resources` 區塊確保檔案句柄能即時關閉，這在處理大量檔案時相當關鍵。

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

請注意 **extract text tiles** 這個詞自然出現在說明中：每次迭代都會 *extract* 該區塊的文字並加入累積結果集。

---

## Step 4 – 執行辨識並輸出合併文字（主要關鍵字）

所有區塊排入佇列後，只需一次呼叫即可對虛擬影像執行 OCR。結果包含完整文字，就像你只有一張巨大的 TIFF。

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**預期輸出**（假設各區塊分別包含 “Hello World” 這句話的片段）：

```
=== OCR Output ===
Hello World
```

若你的區塊包含多行文字，會依照你提供的順序依次顯示。亦可將 `ocrResult.getText()` 寫入檔案，以供後續處理。

---

## Step 5 – 完整可執行範例（一次呈現全部步驟）

以下程式碼可直接複製貼上至 `StreamingExample.java`，內含所有 import、註解與錯誤處理。

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

儲存、編譯並執行：

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

你應該會在主控台看到串接後的 OCR 文字。

---

## 進階技巧與常見陷阱（為何這樣可行）

| Issue | Why It Happens | How to Fix / Optimize |
|-------|----------------|-----------------------|
| **Out‑of‑memory errors** | 將完整大小的 TIFF 載入 `BufferedImage` 會耗盡整個堆積記憶體。 | 使用串流模式 (`setEnableStreaming(true)`)——引擎永不會實體化整張影像。 |
| **Tile order mismatch** | 檔名以字母順序排序會導致數字順序錯亂（例如 `tile_10.tif` 會排在 `tile_2.tif` 前）。 | 為數字補零 (`tile_00.tif`、`tile_01.tif`) 或使用程式碼 `Comparator` 進行數值排序。 |
| **Wrong language** | OCR 預設為英文，非英文文字會變成亂碼。 | 呼叫 `ocrEngine.getLanguageSettings().setLanguage("fr")`（或任何支援的 ISO 代碼）。 |
| **Partial failures** | 單一損毀的區塊會導致整個流程中斷。 | 為每個區塊捕捉 `IOException`，記錄後決定是繼續還是中止。 |
| **Performance bottleneck** | 讀取大量小檔案時磁碟 I/O 成為瓶頸。 | 將區塊打包成 ZIP 並從記憶體串流，或使用高速 SSD。 |

---

## 何時使用串流模式 vs. 單張影像 OCR

- **串流模式** 適用於：
  - 多頁 TIFF 或千億像素掃描。
  - 記憶體受限的情境（例如 Docker 容器、行動裝置）。
  - 已經以影像區塊形式接收資料的管線（例如相機即時串流）。

- **單張影像 OCR** 適用於：
  - 小型 PNG/JPEG 檔案（< 5 MB）。
  - 一次性掃描且簡易性比效能更重要的情況。

---

## 結論

你現在已掌握使用 Aspose OCR 串流功能 **how to ocr tiff** 的完整流程，並能有效 **extract text tiles**。從初始化引擎、啟用串流、逐一加入區塊，到最終辨識虛擬畫布，已涵蓋「什麼、為何、如何」的全部要點，足以支援正式環境的程式碼。

接下來的步驟？試著將 `"en"` 換成其他語言，或改用不同的影像格式（`.png`、`.jpg`）。你也可以直接把 OCR 結果寫入搜尋索引或 PDF 產生器。模式不變：串流 → 拼接 → 辨識。

對於需要處理上百個區塊的擴充需求，或在錯誤處理上有疑問，歡迎在下方留言，我們一起討論。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}