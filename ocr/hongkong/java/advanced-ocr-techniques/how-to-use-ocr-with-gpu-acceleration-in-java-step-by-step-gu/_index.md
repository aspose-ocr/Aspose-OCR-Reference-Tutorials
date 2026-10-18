---
category: general
date: 2026-02-09
description: 如何快速使用 Aspose OCR 進行文字辨識，從圖像中辨識文字並從 PNG 提取文字，同時設定模式與 GPU 記憶體上限。
draft: false
keywords:
- how to use ocr
- recognize text from image
- extract text from png
- how to set mode
- set gpu memory limit
language: zh-hant
og_description: 如何高效使用 OCR — 學習從圖像識別文字、從 PNG 提取文字、設定模式，以及在 Java 中控制 GPU 記憶體上限。
og_title: 如何在 Java 中使用 GPU 加速的 OCR
tags:
- OCR
- Java
- GPU
- Aspose
title: 如何在 Java 中使用 GPU 加速的 OCR – 步驟指南
url: /zh-hant/java/advanced-ocr-techniques/how-to-use-ocr-with-gpu-acceleration-in-java-step-by-step-gu/
---







{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 GPU 加速的 OCR – 完整程式教學

有沒有想過 **如何使用 OCR** 從圖片中擷取文字，而不必寫上千行程式碼？你並不孤單。在許多專案——發票掃描、收據處理，或只是將舊文件數位化——開發者都需要一種可靠的方法來 **recognize text from image** 檔案，尤其是常包含乾淨高解析度圖形的 PNG。  

好消息是？Aspose OCR 讓這變得輕而易舉，且只要稍作設定調整，就能將繁重的運算交給 GPU。在本教學中，我們將逐步說明整個流程：從載入 PNG、**setting mode** 以使用 GPU 處理、**setting GPU memory limit**，最後列印擷取的文字。完成後，你將擁有一個可執行的 Java 程式，正好符合需求。

## 你將學會什麼

- 如何安裝與匯入 Aspose OCR for Java。
- 如何使用此函式庫 **recognize text from image** 檔案。
- 如何有效率地 **extract text from PNG**。
- 如何 **set mode** 為 GPU，並使用 **set GPU memory limit** 來控制記憶體使用。
- 常見陷阱與實務使用技巧。

### 前置條件

- Java 8 或更新版本（程式碼亦可在 JDK 11 上編譯）。
- 若需 GPU 加速，需具備支援 CUDA 的 NVIDIA GPU 及相容驅動程式。
- Aspose OCR for Java JAR（從 Aspose 官方網站下載或透過 Maven/Gradle 加入）。
- 一張範例 PNG 圖片（例如 `sample1.png`），放置於可參考的資料夾中。

---

## 如何使用 OCR – 啟用 GPU 模式

首先，你需要告訴 Aspose OCR 你希望它在 GPU 而非 CPU 上執行。這正是 **how to set mode** 關鍵字發揮作用的地方。

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Step 2: Grab the configuration object
OcrEngineConfiguration config = ocrEngine.getConfiguration();

// Step 3: Switch processing mode to GPU
config.setProcessingMode(ProcessingMode.GPU);   // requires a CUDA‑compatible driver

// (Optional) Step 4: Limit GPU memory usage to 1024 MB
config.setGpuMemoryLimit(1024);                 // set gpu memory limit (MB)
```

**為何這很重要：**  
GPU 處理在大量批次或高解析度影像時可顯著加速，但同時也會消耗顯示記憶體。透過呼叫 `setGpuMemoryLimit`，可防止應用程式佔用整個 GPU，這在同一設備同時執行其他工作負載（例如 UI 或機器學習模型）時尤為重要。

---

## 使用 Aspose OCR 進行文字辨識

現在引擎已完成設定，我們需要指向要讀取的檔案。這就是 **recognize text from image** 的核心。

```java
// Step 5: Define the image to be processed
ImageRecognitionResult imageInfo = new ImageRecognitionResult();
imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

// Step 6: Run the OCR operation
RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);
```

**背後發生了什麼？**  
Aspose OCR 會載入 PNG，進行前處理（二值化、去斜等），然後在 GPU 上執行 OCR 神經網路。結果物件包含原始文字以及每行的信心分數。

---

## 在設定 GPU 記憶體限制下擷取 PNG 文字

辨識完成後，擷取純文字相當簡單，但許多開發者會忘記驗證輸出。以下說明如何安全地 **extract text from PNG** 並顯示。

```java
// Step 7: Output the recognized text
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**預期輸出（範例）：**

```
Recognized text:
Invoice #12345
Date: 2026-02-09
Total: $1,250.00
Thank you for your business!
```

若影像含有雜訊或不常見的字型，可能會出現亂碼。此時可考慮調整前處理選項（例如 `config.setLanguage(Language.ENGLISH)` 或 `config.setAutoSkewCorrection(true)`）。

---

## 完整、可執行範例

以下為完整的 Java 程式，將所有步驟整合在一起。將其複製貼上至名為 `GpuExample.java` 的檔案，調整圖片路徑，然後使用 `javac`/`java` 或在 IDE 中執行。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.configuration.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the image to be processed
        ImageRecognitionResult imageInfo = new ImageRecognitionResult();
        imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

        // Step 2: Create the OCR engine and enable GPU processing
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration config = ocrEngine.getConfiguration();

        // Step 3: Set processing mode to GPU (requires CUDA driver)
        config.setProcessingMode(ProcessingMode.GPU);

        // Step 4 (optional): Limit GPU memory usage to 1024 MB
        config.setGpuMemoryLimit(1024);

        // Step 5: Perform recognition
        RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);

        // Step 6: Print the extracted text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**執行程式**

```bash
javac -cp "path/to/aspose-ocr.jar" GpuExample.java
java -cp ".:path/to/aspose-ocr.jar" GpuExample
```

請確保 JAR 已加入 classpath；否則會拋出 `ClassNotFoundException`。

---

## 專業技巧與常見陷阱

- **GPU 驅動程式版本：** 若缺少或不相容的 CUDA 驅動，`ProcessingMode.GPU` 旗標會拋出例外。請使用 `nvidia-smi` 再次確認。
- **記憶體預算：** 若同時處理大量影像，請提升 `setGpuMemoryLimit` 數值或改為順序執行，以避免記憶體不足錯誤。
- **影像格式：** 雖然 PNG 表現良好，但高壓縮的 JPEG 可能導致辨識錯誤。建議在 OCR 前先轉為無損 PNG。
- **語言支援：** 預設 Aspose OCR 假設使用英文。若需其他語言，請在 `recognize` 前呼叫 `config.setLanguage(Language.SPANISH)`（或相應列舉）。
- **效能測試：** 使用 `System.nanoTime()` 分別在有無 GPU 的情況下快速基準測試，以驗證加速幅度是否值得額外的複雜度。

---

## 常見問答

**這在 macOS 或 Linux 上可用嗎？**  
是的——Aspose OCR 為跨平台。只要確保你的作業系統上安裝了相容 CUDA 的 GPU 及正確的驅動程式即可。

**如果沒有 GPU 該怎麼辦？**  
只要省略 `setProcessingMode(ProcessingMode.GPU)` 這一行，引擎會自動回退至 CPU 模式。

**能直接處理 PDF 嗎？**  
Aspose OCR 專注於點陣圖影像。若要處理 PDF，請先將每頁匯出為影像（例如使用 Aspose PDF），再將 PNG 輸入 OCR 流程。

---

## 結論

總而言之，使用 Aspose 在 Java 中 **how to use OCR** 只需三個明確步驟：設定引擎（包含 **how to set mode** 與 **set GPU memory limit**）、指向你的 PNG，然後讀取產生的字串。上方程式碼片段是一個完整、端對端的解決方案，可直接嵌入任何 Java 專案。

現在你已掌握 **recognize text from image** 與 **extract text from PNG**，可以擴展工作流程：批次處理資料夾、將結果存入資料庫，甚至將文字輸入後續的 NLP 管線。無限可能——只要留意 GPU 記憶體與驅動相容性即可。

對 OCR、GPU 加速或 Aspose 功能有更多疑問嗎？歡迎留下評論，或參閱官方 Aspose OCR 文件以獲得更深入的客製化選項。祝程式開發愉快！ 🚀

![如何使用 OCR 圖解](https://example.com/images/ocr-gpu-diagram.png "如何使用 OCR 圖解")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}