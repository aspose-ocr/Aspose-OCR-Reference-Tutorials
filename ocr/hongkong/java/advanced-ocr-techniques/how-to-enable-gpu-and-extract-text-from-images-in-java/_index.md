---
category: general
date: 2026-09-16
description: 學習如何在 Java 中啟用 GPU 以加快 OCR 速度，從圖像檔案辨識文字，並使用 Aspose OCR 將圖像轉換為文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize text from image
- extract text from image
- how to perform ocr
- convert image to text
language: zh-hant
lastmod: 2026-09-16
og_description: 如何在 Java 中啟用 GPU 進行 OCR，從圖像檔案辨識文字，並使用 Aspose OCR 將圖像轉換為文字 – 完整一步步教學
og_image_alt: Screenshot showing Java code that enables GPU for OCR and extracts text
  from an image
og_title: 如何在 Java 中啟用 GPU 並從圖片中擷取文字
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  headline: How to enable GPU and extract text from images in Java
  type: TechArticle
- description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  name: How to enable GPU and extract text from images in Java
  steps:
  - name: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
    text: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
  - name: '**Segmentation** – locate text lines, words, and characters.'
    text: '**Segmentation** – locate text lines, words, and characters.'
  - name: '**Classification** – match each character against the built‑in language
      model.'
    text: '**Classification** – match each character against the built‑in language
      model.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: 如何在 Java 中啟用 GPU 並從圖像中提取文字
url: /zh-hant/java/advanced-ocr-techniques/how-to-enable-gpu-and-extract-text-from-images-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中啟用 GPU 並從圖像中提取文字

如果您需要 **啟用 GPU** 以進行光學字符識別，本指南會向您展示完整步驟。開啟 GPU 加速後，您可以 **從圖像中識別文字** 的速度比僅使用 CPU 快上數倍。此範例使用 Aspose OCR for Java，但其概念同樣適用於任何支援 GPU 的 OCR 函式庫。

在本教學中，您將學會如何：

* 在 OCR 引擎中啟用 GPU 加速。  
* 載入圖像並 **從圖像中提取文字**。  
* 僅用幾行程式碼即可 **將圖像轉換為文字**。  

不需要任何外部服務——所有操作皆在本機執行。只需具備基本的 Java 開發環境與 Aspose OCR for Java 函式庫，即可開始。

## 前置條件

在開始之前，請確保您具備以下條件：

| 需求 | 版本 / 詳細資訊 |
|-------------|------------------|
| Java Development Kit (JDK) | 8 或更新版本 |
| Maven or Gradle (for dependency management) | 任何較新版本 |
| GPU with CUDA support (optional but recommended) | NVIDIA GPU，驅動程式版本 ≥ 450 |
| Aspose OCR for Java library | 23.9 或更新版本（從 Aspose 官方網站下載） |

如果您沒有 GPU，程式仍可執行，只是會改為使用 CPU。

## 步驟 1：將 Aspose OCR 加入您的專案

For Maven，請將以下相依性加入您的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

For Gradle，請將以下內容放入 `build.gradle`：

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

這些條目會自動下載 OCR 引擎及原生 GPU 二進位檔。

## 步驟 2：如何為 OCR 引擎啟用 GPU

主要工作是告訴 `OcrEngine` 使用 GPU。Aspose OCR 提供一個簡單的旗標：

```java
// Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the “how to enable gpu” step
ocrEngine.setGpuEnabled(true);
```

**為什麼這很重要：** 當呼叫 `setGpuEnabled(true)` 後，函式庫會載入基於 CUDA 的核心，將影像前處理與字元分割階段平行化。在現代的 NVIDIA 顯示卡上，速度可提升 2‑4 倍，相較於預設的 CPU 路徑。

> **專業提示：** 在啟用旗標前，先執行 `SystemInfo.isCudaSupported()` 以確認 GPU 是否被偵測到。若回傳 `false`，引擎會自動回退至 CPU。

## 步驟 3：載入要處理的圖像

您可以將任何 Aspose 支援的影像格式（JPEG、PNG、BMP、TIFF 等）提供給 OCR 引擎。以下示範如何載入 JPEG 檔案：

```java
// Load the image that contains the text to be recognized
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

**特殊情況：** 若影像檔案過大（超過 5 MB），建議先縮小尺寸以降低記憶體使用。OCR 引擎在約 300 dpi 的影像上表現最佳。

## 步驟 4：執行 OCR 並 **從圖像中識別文字**

現在引擎已完成設定且影像已載入，您可以執行辨識：

```java
// Execute OCR – this is the core “how to perform ocr” step
String recognizedText = ocrEngine.recognize();
```

`recognize()` 方法會回傳純文字 `String`。在內部，引擎會經過多個階段：

1. **前處理** – 去斜、二值化並增強對比度（GPU 加速）。  
2. **分割** – 偵測文字行、單詞與字元。  
3. **分類** – 將每個字元與內建語言模型比對。  

由於 GPU 已啟用，步驟 1 與 2 可從平行執行中獲得最大效益。

## 步驟 5：顯示或儲存提取的文字

最後，將結果輸出至主控台、檔案或任何後續處理程序：

```java
// Show the extracted text – this completes the “convert image to text” flow
System.out.println("Recognized text:\n" + recognizedText);

// Optional: write the text to a file
Files.write(Paths.get("output.txt"), recognizedText.getBytes(StandardCharsets.UTF_8));
```

**典型輸出**（以包含 “Hello World” 的範例圖像為例）：

```
Recognized text:
Hello World
```

若 OCR 無法偵測到任何字元，`recognizedText` 會是空字串。此時請再次檢查影像品質，或關閉 GPU 以比較效能差異。

## 處理常見陷阱

| 問題 | 原因 | 解決方案 |
|-------|-------|-----|
| **GPU not detected** | 缺少 CUDA 驅動程式或 GPU 不受支援 | 安裝最新的 NVIDIA 驅動程式，並使用 `nvidia-smi` 確認。 |
| **Incorrect characters** | 對比度低或背景雜訊 | 在送入引擎前先前處理影像（例如提升對比度）。 |
| **Out‑of‑memory error** | 在有限的 GPU 記憶體上處理過大影像 | 將影像寬度調整至 ≤ 2000 px，或分塊處理。 |
| **Language mismatch** | 預設語言模型為英文，但文字為其他語言 | 在 `recognize()` 前呼叫 `ocrEngine.setLanguage(OcrLanguage.SPANISH)`（或相應的列舉值）。 |

## 完整、可執行範例

以下是一個完整的 Java 類別，將所有步驟整合在一起。將其儲存為 `GpuEnabledOcrExample.java`，調整影像路徑後，即可使用 `javac`/`java` 或於 IDE 中執行。

```java
import com.aspose.ocr.*;
import java.nio.file.*;

public class GpuEnabledOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Turn on GPU acceleration for faster processing
        // This is the core "how to enable gpu" call
        ocrEngine.setGpuEnabled(true);

        // Optional sanity check – ensures CUDA is available
        if (!SystemInfo.isCudaSupported()) {
            System.out.println("CUDA not detected. Falling back to CPU.");
        }

        // Step 3: Load the image that contains the text to be recognized
        // Replace with the absolute path to your image file
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Perform the OCR operation and obtain the recognized text
        // This answers "how to perform ocr" and "recognize text from image"
        String recognizedText = ocrEngine.recognize();

        // Step 5: Display the extracted text – completes "convert image to text"
        System.out.println("Recognized text:\n" + recognizedText);

        // (Optional) Save the result to a text file
        Path output = Paths.get("recognized_output.txt");
        Files.write(output, recognizedText.getBytes());
        System.out.println("Text saved to " + output.toAbsolutePath());
    }
}
```

### 預期結果

執行程式會將提取的文字印在主控台，並寫入 `recognized_output.txt`。啟用 GPU 後，對於 2 MP 的影像，總執行時間通常在 NVIDIA RTX 3060 上低於 200 ms，較僅使用 CPU 時約 500 ms 大幅縮短。

## 結論

您現在已了解如何在 Java 中為 Aspose OCR **啟用 GPU**、**從圖像中識別文字**，以及僅用幾行簡單程式碼 **將圖像轉換為文字**。透過 GPU 加速，您可獲得更快的處理速度，這對於批次或即時應用（如發票掃描、收據處理與文件數位化）至關重要。

**下一步**

* 嘗試不同的語言模型（`ocrEngine.setLanguage`），以 **從圖像中提取文字**，支援法文、德文或中文等。  
* 將 OCR 輸出與 Apache Tika 結合，自動索引提取的內容。  
* 若需在 PDF 文件中 **從圖像中識別文字**，可探索逐頁串流大型 PDF 的方式。

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並在此基礎上延伸。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何在 Java 中使用 Aspose OCR 讀取圖像文字 – 完整指南](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [使用 Aspose OCR 識別圖像文字 – 完整 Java OCR 教學](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [圖像轉文字 Java：使用 Aspose.OCR 進行圖像到文字的轉換](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}