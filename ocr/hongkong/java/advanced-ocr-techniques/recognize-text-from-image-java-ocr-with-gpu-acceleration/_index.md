---
category: general
date: 2026-04-29
description: 學習如何使用 Aspose OCR 在 Java 中辨識圖像文字。包括從 jpg 提取文字、載入圖像進行 OCR，以及設定 GPU 裝置
  ID 的步驟。
draft: false
keywords:
- recognize text from image
- extract text from jpg
- how to extract text image
- load image for OCR
- set GPU device ID
language: zh-hant
og_description: 使用 Aspose OCR 快速辨識圖像文字。本指南說明如何載入圖像進行 OCR、從 JPG 提取文字，以及設定 GPU 裝置 ID。
og_title: 從圖像辨識文字 – 支援 GPU 加速的 Java OCR
tags:
- Java
- OCR
- GPU
- Aspose
title: 從圖像辨識文字 – Java OCR（GPU 加速）
url: /zh-hant/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 辨識影像文字 – Java OCR 與 GPU 加速

有沒有試過從影像中辨識文字，結果卻變成亂碼？你並不孤單。無論是在數位化收據、掃描護照，或是從產品標籤提取資料的專案中，OCR 的品質往往決定整個流程的成敗。  

好消息是？使用 Aspose OCR，你可以在幾秒鐘內 **recognize text from image**，若配備 CUDA 相容的 GPU，處理時間還能進一步縮短。在本教學中，我們將逐步說明如何載入影像供 OCR 使用、啟用 GPU 加速，最後從 JPG 檔案中提取文字。完成後，你將清楚知道如何 **extract text from jpg** 檔案、如何 **set GPU device ID**，以及每個步驟的意義。

## 需要的環境

- **Java Development Kit (JDK) 11+** – 這段程式碼使用標準的 Java 語言功能。
- **Aspose OCR for Java** 函式庫（截至 2026 年的最新版本）。你可以從 Maven Central 取得，或從 Aspose 官方網站下載 JAR。
- **CUDA‑enabled GPU**（驅動程式 11 以上）（可選，但強烈建議以提升速度）。
- 一張範例影像，例如 `sample.jpg`，放在程式碼可參考的資料夾中。

不需要外部服務或雲端金鑰——只要一個本機的 Java 專案與具備 GPU 的機器即可。

## 步驟 1 – 載入影像供 OCR 使用

在辨識文字之前，你必須先提供 OCR 引擎可讀取的影像。這就是 **load image for OCR** 步驟的用途。

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the image
        OcrEngine engine = new OcrEngine();

        // Load a JPG file – this is the “extract text from jpg” part
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **Why this matters:** `ImageStream.fromFile` 方法支援多種格式（JPG、PNG、BMP）。使用 JPG 可保持檔案尺寸小，對於在 GPU 上處理數百張影像時特別方便。

## 步驟 2 – 啟用 GPU 加速並設定 GPU 裝置 ID

如果你的機器配備 CUDA 相容的 GPU，你可以指示 Aspose OCR 在顯示卡上執行繁重的運算。這就是 **set GPU device ID** 步驟。

```java
        // Step 2: Enable GPU acceleration (requires CUDA 11+ and a compatible driver)
        engine.getProcessingSettings().setUseGpu(true);

        // Optional: Choose a specific GPU device (0 = first GPU)
        engine.getProcessingSettings().setGpuDeviceId(0);
```

> **Pro tip:** 若有多張 GPU，你可以嘗試不同的 `gpuDeviceId` 數值，觀察哪一張提供最佳吞吐量。預設值（`0`）通常指向主要的 GPU。

## 步驟 3 – 執行 OCR 程序

現在影像已載入，且引擎已為 GPU 工作做好準備，是時候真正辨識文字了。

```java
        // Step 3: Run the OCR process
        OcrResult result = engine.recognize();
```

> **What’s happening under the hood?** OCR 引擎會將影像切割成文字行，對每個片段執行神經網路，然後將結果拼接。當 `setUseGpu(true)` 啟用時，這個神經網路會在 GPU 上執行，而非 CPU，從而大幅降低延遲。

## 步驟 4 – 提取並顯示辨識結果文字

最後一步是 **extract text from jpg** 並將結果顯示給使用者。`OcrResult` 物件包含純文字、信心分數，甚至在之後需要時的邊界框。

```java
        // Step 4: Display the recognized text
        System.out.println("Recognized text:");
        System.out.println(result.getText());

        // Optional: Print confidence (helps with quality checks)
        System.out.println("Overall confidence: " + result.getConfidence());
    }
}
```

### 預期輸出

如果 `sample.jpg` 內含句子 “Hello World”，控制台應會印出：

```
Recognized text:
Hello World
Overall confidence: 0.98
```

信心值介於 0 到 1 之間；0.8 以上的值在乾淨的掃描中通常相當可靠。

## 步驟 5 – 常見變化與邊緣情況

### 使用 PNG 或 BMP 檔案

如果來源影像不是 JPG，只需更改檔案副檔名：

```java
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.png"));
```

其餘工作流程保持相同——只要 Aspose 支援，**how to extract text image** 就不受檔案格式限制。

### 處理低解析度影像

低解析度的圖片常會產生較低的信心分數。你可以透過以下方式提升結果：

1. 使用 OpenCV 等函式庫將影像升級再送入 Aspose。
2. 調整 `engine.getProcessingSettings().setResolution(300);`，以強制內部處理使用更高 DPI。

### 僅使用 CPU 執行

如果沒有 CUDA 相容的 GPU，只需省略 GPU 相關程式碼：

```java
engine.getProcessingSettings().setUseGpu(false);
```

OCR 會回退至 CPU，雖較慢但仍能正常運作。

## 生產環境實用技巧

- **Batch Processing:** 將 OCR 邏輯包在迴圈中，並重複使用同一個 `OcrEngine` 實例。這可減少重複載入原生函式庫的開銷。
- **Error Handling:** 必須捕捉 `IOException` 與 `OcrException`，以優雅地處理損壞的檔案。
- **Memory Management:** 處理完畢後，呼叫 `engine.dispose();` 釋放原生 GPU 記憶體，特別是在處理數千張影像時。

```java
        // Clean up resources
        engine.dispose();
```

- **Logging:** 將 `result.getConfidence()` 與提取的文字一起儲存。低信心的條目可送至人工審核佇列。

## 完整範例程式

以下是完整、獨立的程式碼，你可以直接複製貼上到 IDE 中。只需將 `YOUR_DIRECTORY` 替換為你的影像資料夾路徑。

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Load a JPG image – this is how you extract text from jpg
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Enable GPU acceleration (requires CUDA 11+ and a compatible driver)
        engine.getProcessingSettings().setUseGpu(true);

        // Optional: Select a specific GPU device (0 = first GPU)
        engine.getProcessingSettings().setGpuDeviceId(0);

        // Run the OCR process
        OcrResult result = engine.recognize();

        // Show the recognized text
        System.out.println("Recognized text:");
        System.out.println(result.getText());

        // Show confidence for quality checks
        System.out.println("Overall confidence: " + result.getConfidence());

        // Release native resources
        engine.dispose();
    }
}
```

> **Result verification:** 將印出的文字與原始影像比較。若信心值偏低，請參考「常見變化與邊緣情況」章節中的建議。

## 結論

我們已完整說明如何在 Java 中使用 Aspose OCR **recognize text from image**，從載入檔案、啟用 GPU 加速到最終提取文字。依循這些步驟，你可以可靠地 **extract text from jpg** 檔案、透過 **set GPU device ID** 控制使用哪張 GPU，甚至將流程套用到其他影像格式。

準備好接受下一個挑戰了嗎？試著將此 OCR 流程串接至資料庫寫入，或將結果輸入自然語言處理模型以自動分類。可能性無窮，而核心模式——**load image for OCR → enable GPU → recognize → extract**——始終如一。

如果遇到任何問題，請再次確認 CUDA 驅動版本、確保 Aspose OCR JAR 與你的 JDK 相容，並記得在每個批次後釋放引擎。祝開發順利，願你的 OCR 永遠精準！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}