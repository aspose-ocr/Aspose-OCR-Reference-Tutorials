---
category: general
date: 2026-06-16
description: 使用 Aspose OCR 在 Java 中快速辨識文字圖像。了解如何設定 GPU 裝置、提取文字 JPG，並使用 GPU 加速讀取文字圖片。
draft: false
keywords:
- recognize text image
- set gpu device
- extract text jpg
- how to recognize text
- read text picture
language: zh-hant
og_description: 使用 Aspose OCR 在 Java 中辨識文字圖像。本指南說明如何設定 GPU 裝置、提取文字 JPG，並高效讀取文字圖片。
og_title: 在 Java 中使用 Aspose OCR + GPU 識別文字圖像
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text image quickly with Aspose OCR in Java. Learn how to
    set gpu device, extract text jpg, and read text picture using GPU acceleration.
  headline: recognize text image in Java using Aspose OCR + GPU
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- GPU
title: 在 Java 中使用 Aspose OCR + GPU 進行文字圖像辨識
url: /zh-hant/java/advanced-ocr-techniques/recognize-text-image-in-java-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中使用 Aspose OCR + GPU 識別文字圖像

有沒有想過在 Java 應用程式中識別文字圖像時，卻不會把 CPU 磨到停不下來？你並不孤單——開發者不斷追求更快、更可靠的 OCR 流程。在本教學中，我們將一步步示範完整的 GPU 加速解決方案，讓你瞬間從 JPG 圖片中擷取文字。

我們會先設定 Aspose OCR，接著啟用 GPU 加速，最後示範如何讀取文字圖片檔案、輸出結果，並處理偶發的錯誤。完成後，你將會知道 **如何在任何圖像上識別文字**，無論是掃描發票或是隨手截圖。

## 你需要的環境

- **Java 17**（或任何近期的 JDK）– 程式碼可在所有現代執行環境上運行。  
- **Aspose.OCR for Java** – 可透過 Maven Central 取得。  
- 支援 CUDA 的 **GPU**（可選，但強烈建議以提升速度）。  
- 一張 JPEG 範例圖（例如 `sample.jpg`），即你想要處理的圖片。  

不需要其他第三方函式庫；其餘全部由 Aspose OCR 打包提供。

## Step 1: Add Aspose OCR to Your Project

如果你使用 Maven，只要把以下相依性加入 `pom.xml` 即可。Gradle 使用者可複製等價的 `implementation` 行。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **小技巧：** 免費評估版會加上小水印。正式上線時，請從 Aspose 入口網站取得授權，並在任何 OCR 操作前呼叫  
> `License license = new License(); license.setLicense("Aspose.OCR.lic");`

## Step 2: Load the Image You Want to Process

當你想要 **識別文字圖像** 時，第一步就是把圖片餵給 OCR 引擎。Aspose 提供便利的 `ImageStream` 包裝類別，可從檔案路徑、`InputStream` 或甚至位元組陣列讀取。

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {
        // Load the image – replace the path with your own picture
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

請注意，我們保持程式碼盡可能簡潔；`setImage` 方法接受 Aspose 支援的任何點陣圖格式，包括 JPEG、PNG 與 BMP。

## Step 3: Enable GPU Acceleration (set gpu device)

接下來的重點是：我們會 **設定 GPU 裝置**，讓 OCR 引擎在顯示卡上執行而非 CPU。這能在處理高解析度圖像時節省數秒時間。

```java
        // Enable GPU acceleration – this is where the magic happens
        engine.getRecognitionSettings().setUseGpu(true);

        // Optional: pick a specific GPU if you have more than one
        // engine.getRecognitionSettings().setGpuDeviceId(0);
```

如果你的機器有多張 GPU，請取消註解 `setGpuDeviceId` 那一行，並將 `0` 改成你想使用的裝置索引。若找不到相容的 GPU，Aspose 會自動回退到 CPU，無需擔心程式崩潰。

## Step 4: Perform OCR – how to recognize text

在載入圖片且 GPU 已啟動後，我們終於可以 **執行文字識別**。`recognize()` 方法會跑完整個流程——前處理、分割、字元分類與後處理。

```java
        // Execute the OCR process
        OcrResult result = engine.recognize();
```

回傳的 `OcrResult` 物件包含原始字串、信心分數，甚至若需要版面資訊，還會提供邊界框。

## Step 5: Output the Recognized Text – extract text jpg / read text picture

只要簡單地把結果印到主控台，就能 **擷取文字 jpg** 與 **讀取文字圖片**。在實務應用中，你可能會把結果寫入資料庫或檔案。

```java
        // Show the recognized text in the console
        System.out.println("Recognized text:");
        System.out.println(result.getText());
    }
}
```

執行程式後，應該會看到類似以下的輸出：

```
Recognized text:
Invoice #12345
Date: 2026-06-15
Total: $1,250.00
```

若圖片雜訊較多，你可以微調 Aspose 的前處理設定（對比度、二值化等）——但預設設定已能處理大多數乾淨的 JPG 檔案。

## Full Working Example

把所有步驟整合起來，以下是一個完整、可直接執行的類別範例：

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the image to be processed
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Step 2: Enable GPU acceleration for faster recognition
        engine.getRecognitionSettings().setUseGpu(true);
        // Optional: specify a GPU device index if multiple GPUs are present
        // engine.getRecognitionSettings().setGpuDeviceId(0);

        // Step 3: Perform OCR on the loaded image
        OcrResult result = engine.recognize();

        // Step 4: Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(result.getText());
    }
}
```

> **預期輸出：** 主控台會列印出 `sample.jpg` 中的完整文字內容。若圖片是收據的照片，則每一行會以獨立字串顯示，保留換行。

## Edge Cases & Common Pitfalls

| 情境 | 需要留意的地方 | 建議解決方式 |
|-----------|-------------------|---------------|
| **多張 GPU** | 預設使用的 GPU 可能不是效能最好的。 | 使用 `setGpuDeviceId` 指定高效能卡。 |
| **大型圖像記憶體不足** | 超高解析度的 JPG 可能耗盡 GPU 記憶體。 | 先縮小圖像 (`engine.getPreprocessingSettings().setResizeFactor(0.5)`)。 |
| **信心分數低** | 圖片模糊時部分字元可能辨識錯誤。 | 開啟 `engine.getRecognitionSettings().setUseLanguageModel(true)` 以使用語言模型進行上下文校正。 |
| **不支援的圖像格式** | Aspose OCR 支援多種格式，但不支援 RAW 感測器資料。 | 先將檔案轉為 JPEG 或 PNG 再送入引擎。 |

處理好上述情況，即可確保你的 **識別文字圖像** 工作流程在各種環境下皆保持穩定。

## Pro Tips for Faster and Cleaner OCR

- **批次處理：** 為多張圖片重複使用同一個 `OcrEngine` 實例；GPU 內容會保持存活，減少初始化開銷。  
- **執行緒安全：** 每條執行緒應自行建立 `OcrEngine` 物件；此類別本身不具執行緒安全性。  
- **提前授權：** 在應用程式啟動時即載入 Aspose 授權，以避免評估版水印。  
- **記錄日誌：** 若需除錯特定圖片失敗原因，可開啟 `engine.getLogSettings().setEnableLogging(true)`。

## Conclusion

我們已示範如何在 Java 中使用 Aspose OCR 搭配 GPU 加速 **識別文字圖像**。只要依序完成加入函式庫、載入 JPEG、**設定 GPU 裝置**、執行 OCR 引擎，最後 **擷取文字 jpg** 或 **讀取文字圖片**，就能把圖片中的文字快速轉換為可編輯的文字。

## What Should You Learn Next?

以下教學與本篇內容緊密相關，能進一步深化你的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，或在專案中探索替代實作方式。

- [使用 Aspose OCR 識別文字圖像 – 完整 Java OCR 教學](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [使用 Aspose.OCR Detect Areas Mode 從 Java 圖片擷取文字](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [使用 Aspose.OCR BufferedImage 在 Java 中將圖像轉換為文字](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}