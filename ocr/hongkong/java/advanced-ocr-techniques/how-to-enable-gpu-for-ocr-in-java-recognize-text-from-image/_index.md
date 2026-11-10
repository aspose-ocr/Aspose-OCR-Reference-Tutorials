---
category: general
date: 2026-08-22
description: 如何在 Java OCR 中啟用 GPU，以快速從圖像識別文字。了解如何從 PNG 提取文字、設定圖像選項，並使用 Aspose OCR
  高效識別文字。
draft: false
keywords:
- how to enable gpu
- recognize text image java
- aspose ocr java tutorial
- extract text from png
- set image options
lastmod: 2026-08-22
og_description: 如何在 Java OCR 中啟用 GPU，以快速從圖像識別文字。本指南將示範如何從 PNG 提取文字、設定圖像選項，並使用 Aspose
  OCR 高效識別文字。
og_image_alt: Java OCR GPU example code snippet showing Aspose OCR usage
og_title: 如何在 Java 中啟用 GPU 進行 OCR – 快速文字提取
schemas:
- author: Aspose
  dateModified: '2026-08-22'
  description: How to enable GPU in Java OCR to recognize text from image quickly.
    Learn to extract text from PNG, set image options, and recognize text efficiently
    using Aspose OCR.
  headline: How to Enable GPU for OCR in Java – Recognize Text from Image Fast
  type: TechArticle
- description: How to enable GPU in Java OCR to recognize text from image quickly.
    Learn to extract text from PNG, set image options, and recognize text efficiently
    using Aspose OCR.
  name: How to Enable GPU for OCR in Java – Recognize Text from Image Fast
  steps:
  - name: '**Low‑resolution scans (< 150 dpi).** Upscale first or ask the user for
      a higher‑resolution scan.'
    text: '**Low‑resolution scans (< 150 dpi).** Upscale first or ask the user for
      a higher‑resolution scan.'
  - name: '**Handwritten notes.** The default model focuses on printed text; you’d
      need a custom trained model for cursive.'
    text: '**Handwritten notes.** The default model focuses on printed text; you’d
      need a custom trained model for cursive.'
  - name: '**Multiple languages.** Pass a comma‑separated list to `RecognitionLanguage`,
      e.g., `RecognitionLanguage.ENGLISH_FRENCH`.'
    text: '**Multiple languages.** Pass a comma‑separated list to `RecognitionLanguage`,
      e.g., `RecognitionLanguage.ENGLISH_FRENCH`.'
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR trial includes full GPU support; you just need to
      enable it in code.
    question: Does the free trial support GPU acceleration?
  - answer: Aspose OCR can rasterize PDF pages internally, but for best performance
      convert to high‑resolution PNG first.
    question: Can I process PDFs directly without converting to images?
  - answer: CUDA 11.2 or newer is recommended; older versions may work but are not
      officially tested.
    question: What CUDA version is required?
  - answer: Validate file size and type before processing, and run the OCR in a sandboxed
      thread to mitigate risks.
    question: Is it safe to run OCR on untrusted user uploads?
  - answer: Set `ocrEngine.setDebugMode(true)`; the console will list the selected
      GPU device and memory statistics.
    question: How do I enable logging to verify GPU usage?
  type: FAQPage
tags:
- OCR
- Java
- GPU
title: 如何在 Java 中啟用 GPU 進行 OCR – 快速從圖像識別文字
url: /zh-hant/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中啟用 GPU 進行 OCR – 快速從圖像辨識文字

在 Java OCR 應用程式中啟用 GPU 加速可以大幅縮短處理時間，特別是當您需要從大型圖像或大量批次中提取文字時。在本教學中，您將學習 **如何啟用 GPU**、如何 **從圖像辨識文字**，以及使用 Aspose OCR 函式庫 **從 PNG 提取文字** 的具體步驟。我們還會說明提升準確度的圖像前處理選項，並解答常見的「如何辨識文字」問題。

## 快速回答
- **最大的速度提升是什麼？** 在中階 RTX 2060 上可比僅使用 CPU 的 OCR 快 up to 5 倍。  
- **我需要特別的授權嗎？** 標準的 Aspose OCR 授權即可支援 GPU；只需啟用 GPU 旗標。  
- **需要哪個 Java 版本？** 建議使用 Java 17 或更新版本以獲得最佳效能。  
- **我可以在 Docker 內執行嗎？** 是的 – 只需在容器中加入 `--gpus all` 旗標並安裝 NVIDIA 驅動程式。  
- **程式碼是否相容其他圖像格式？** 相同的 API 可直接支援 JPEG、TIFF、BMP 與 PNG，無需變更。

## 您需要的條件

您需要一台具備 GPU 的機器、Aspose OCR for Java 函式庫，以及 Java 17（或更新）開發環境。典型的配置包括 NVIDIA RTX 3060 或任何相容 CUDA 的顯示卡、從 Maven Central 取得的最新 Aspose OCR JAR，還有用於效能測試的 PNG 發票範例。

**Direct answer (40‑70 words):** 要開始使用，您必須安裝 Java 17、將 Aspose OCR 相依性加入專案、確認 JVM 能偵測到至少一個 CUDA 裝置，並準備好測試圖像。滿足這些前置條件後，即可在 OCR 引擎中啟用 GPU，開始以 GPU 速度處理圖像。

- **Java 17**（或更新） – 程式碼在較舊版本亦可編譯，但 17 提供最佳的 API 支援。  
- **Aspose OCR for Java** – 從 Aspose 官方網站或 Maven Central 取得最新 JAR。  
- **相容 CUDA 的 GPU** – 例如 NVIDIA RTX 3060、RTX 2070，或任何具備適當驅動程式的現代顯示卡。  
- **測試圖像** – 大尺寸 PNG 發票非常適合用來測量效能。

> **Pro tip:** 在同時具備整合式與獨立顯示卡的筆記型電腦上，請透過驅動程式控制面板強制 JVM 使用獨立 GPU；否則函式庫會默默回退至 CPU。

![how to enable gpu example](image.png "how to enable gpu example")
[how to enable gpu example](image.png "how to enable gpu example")

*Alt text: 顯示 Java 程式碼片段的如何啟用 GPU 範例。*

## 步驟 1 – 安裝 Aspose OCR 並驗證 GPU 可用性

GpuSettings 是一個控制 Aspose OCR 引擎 GPU 使用的類別。

加入 Maven 相依性（或將 JAR 放入 `libs/` 目錄）：

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Check for the latest version -->
</dependency>
```

執行 sanity‑check 程式碼片段以列出可用裝置：

```java
import com.aspose.ocr.GpuSettings;

public class GpuCheck {
    public static void main(String[] args) {
        GpuSettings settings = new GpuSettings();
        System.out.println("GPU enabled? " + settings.getEnable());
        System.out.println("Detected GPU count: " + settings.getDeviceCount());
    }
}
```

如果輸出顯示非零的裝置數量，表示您的 JVM 已偵測到 GPU。若顯示為零，請再次確認驅動程式已安裝，且 `CUDA_PATH` 環境變數已設定。

## 步驟 2 – 如何在 Aspose OCR 中啟用 GPU

**Direct answer (40‑70 words):** 透過建立 `GpuSettings` 物件、呼叫 `setEnable(true)`，可選擇指定裝置 ID，並將此設定物件傳入 `AsposeOCR` 建構子，即可啟用 GPU。之後所有 OCR 呼叫皆會在選定的 GPU 上執行，提供效能章節中描述的速度提升。

`GpuSettings` 類別讓您在多顯示卡環境中切換 GPU 使用與選擇特定裝置。

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.GpuSettings;
import com.aspose.ocr.ImageProcessingOptions;
import com.aspose.ocr.RecognitionLanguage;
import com.aspose.ocr.OcrResult;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // 2️⃣ Enable GPU processing (auto‑detects available device)
        GpuSettings gpuSettings = new GpuSettings();
        gpuSettings.setEnable(true);          // turn GPU on
        gpuSettings.setDeviceId(0);           // first GPU (change if you have multiple)
        ocrEngine.setGpuSettings(gpuSettings);

        // 3️⃣ Optimize image preprocessing for GPU performance
        ImageProcessingOptions imgOpts = new ImageProcessingOptions();
        imgOpts.setAutoDeskew(true);
        imgOpts.setBinarization(true);
        ocrEngine.setImageProcessingOptions(imgOpts);

        // 4️⃣ Recognize text from an image file (PNG in this case)
        OcrResult result = ocrEngine.recognizeImage(
                "YOUR_DIRECTORY/large_invoice.png",
                RecognitionLanguage.ENGLISH);

        // 5️⃣ Output the detected text
        System.out.println("Detected text:\n" + result.getText());
    }
}
```

### 為何啟用 GPU？

GPU 加速將 OCR 模型執行的繁重矩陣乘法工作分散到數千個平行核心上。實際上，在一般的 RTX 2060 上可見 **2‑5 倍的速度提升**，較新卡片則更快。代價是記憶體佔用略增，但對於一般發票大小的 PNG 通常不是問題。

## 步驟 3 – 辨識圖像文字 Java – 最佳實踐

`recognizeImage` 方法會處理給定的圖像檔案並回傳提取的文字。

**Direct answer (40‑70 words):** 在啟用 GPU 後呼叫 `ocrEngine.recognizeImage(filePath)`；此方法會自動偵測檔案格式，在 GPU 上執行 OCR 模型，並回傳提取的文字。為獲得最佳準確度，請在呼叫前確保圖像已二值化與去傾斜。

上述程式碼已完成此操作，但以下提供一個僅聚焦 OCR 呼叫的精簡版本：

```java
// Assuming ocrEngine is already configured with GPU
String imagePath = "sample.png";
OcrResult ocrResult = ocrEngine.recognizeImage(imagePath, RecognitionLanguage.ENGLISH);
String extractedText = ocrResult.getText();

System.out.println("Extracted text from PNG:");
System.out.println(extractedText);
```

**您會注意到：** `recognizeImage` 方法會自動偵測檔案類型，您可直接提供 JPEG、TIFF 或 PNG，無需額外旗標。這就是為何 **從 PNG 提取文字** 能直接使用的原因。

### 處理大型檔案

如果您的 PNG 大於 5 MB，建議在 OCR 前先縮小尺寸：

```java
imgOpts.setResizeFactor(0.5); // shrink to 50 % of original dimensions
ocrEngine.setImageProcessingOptions(imgOpts);
```

降採樣可減少 GPU 記憶體使用，且通常因模型看到較乾淨的邊緣而提升準確度。

## 步驟 4 – 如何設定圖像選項以提升準確度

ImageOptions 是一個設定物件，可讓您在 OCR 前調整如去傾斜與二值化等前處理步驟。

**Direct answer (40‑70 words):** 使用 `ImageOptions` 物件在將圖像傳入 OCR 引擎前啟用自動去傾斜、二值化，以及可選的縮放。常見設定為 `setAutoDeskew(true)`、`setBinarization(true)`，以及對大型掃描設定 0.5 至 0.8 之間的縮放比例。這些設定可提升對比度與對齊度，協助神經網路更精確辨識字元，特別是噪點或傾斜的文件。

在討論前處理時，自然會出現 **如何設定圖像** 這個片語。Aspose OCR 提供以下幾個調整參數：

| 選項                     | 功能說明                               | 典型值 |
|----------------------------|--------------------------------------------|---------------|
| `setAutoDeskew(true)`      | 直線化傾斜的文字行              | true          |
| `setBinarization(true)`    | 轉換為黑白以提升對比度   | true          |
| `setResizeFactor(x)`       | 縮放圖像 (0 < x ≤ 1)               | 0.5‑0.8       |
| `setContrastAdjustment(y)` | 提升對比度 (0‑100)                    | 30            |

您可以任意順序組合這些設定；函式庫會在將圖像送入神經網路前依序套用。實驗是關鍵——不同的發票可能需要不同的閾值。

## 步驟 5 – 如何在特殊情況下辨識文字

`GpuExample` 類別示範了使用 Aspose OCR 搭配 GPU 加速的完整端對端 OCR 工作流程。

**Direct answer (40‑70 words):** 對於低解析度掃描，請先放大圖像或要求更高 DPI 的來源；對手寫筆記，需切換至自訂訓練模型；對多語言文件，將以逗號分隔的語言清單傳入 `RecognitionLanguage`。這些調整可確保 GPU 加速的引擎仍能提供可靠結果。

即使有 GPU 加速，某些情況仍會使 OCR 出錯：

1. **低解析度掃描 (< 150 dpi)。** 先放大圖像或請使用者提供更高解析度的掃描。  
2. **手寫筆記。** 預設模型針對印刷文字，若要辨識手寫需使用自訂訓練模型。  
3. **多語言。** 將以逗號分隔的語言清單傳入 `RecognitionLanguage`，例如 `RecognitionLanguage.ENGLISH_FRENCH`。

```java
ocrEngine.recognizeImage("multilang.png",
        RecognitionLanguage.ENGLISH_FRENCH);
```

## 預期輸出

執行完整的 `GpuExample` 類別對 `large_invoice.png`，應會印出類似以下內容：

```
Detected text:
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
...
```

如果看到亂碼，請再次確認 `gpuSettings.setEnable(true)` 確實生效（若啟用除錯日誌，主控台會列出 GPU 裝置）。

## 常見陷阱與專業提示

- **忘記設定 GPU 裝置 ID。** 在多 GPU 系統上，可能需要 `setDeviceId(1)`。  
- **在未使用 NVIDIA 執行環境的 Docker 中執行。** 在 `docker run` 指令中加入 `--gpus all`。  
- **混用僅 CPU 與 GPU 啟用的程式路徑。** 每個執行緒僅保留單一 `AsposeOCR` 實例，以避免狀態衝突。  
- **記憶體泄漏。** 完成後呼叫 `ocrEngine.dispose()`，特別是在長時間執行的服務中。

## 常見問答

**Q: 免費試用版支援 GPU 加速嗎？**  
A: 是的，Aspose OCR 試用版包含完整的 GPU 支援，只需在程式碼中啟用即可。

**Q: 可以直接處理 PDF 而不轉換成圖像嗎？**  
A: Aspose OCR 能在內部將 PDF 頁面光柵化，但為取得最佳效能，建議先轉換為高解析度 PNG。

**Q: 需要哪個 CUDA 版本？**  
A: 建議使用 CUDA 11.2 或更新版本；較舊版本可能可運作，但未經官方測試。

**Q: 在未受信任的使用者上傳檔案上執行 OCR 安全嗎？**  
A: 在處理前驗證檔案大小與類型，並在沙箱執行緒中執行 OCR 以降低風險。

**Q: 如何啟用日誌以驗證 GPU 使用情況？**  
A: 設定 `ocrEngine.setDebugMode(true)`；主控台會列出選取的 GPU 裝置與記憶體統計資訊。

## 結論

我們已說明了在 Java 中為 Aspose OCR **啟用 GPU** 的步驟，展示了 **從圖像辨識文字** 的方法，示範了 **從 PNG 提取文字** 的最簡方式，說明了 **如何設定圖像** 處理選項，並探討了在實務檔案中 **如何辨識文字** 的細節。啟用 GPU 後，您的 OCR 流程將明顯加速，適用於批次發票處理或即時文件掃描等高吞吐量情境。

準備好進一步了嗎？試著將預設的英文模型換成多語言模型，或針對雜訊收據實驗自訂前處理流程。只要有 GPU 承擔重任，您的可能性無限。

**最後更新：** 2026-08-22  
**測試環境：** Aspose OCR for Java 24.10  
**作者：** Aspose

## 相關教學

- [使用 Aspose OCR 完整 Java OCR 教學 – 辨識圖像文字](/ocr/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [如何在 Java 中設定 Aspose OCR 授權並驗證](/ocr/java/ocr-basics/set-license/)
- [使用 Aspose.OCR 偵測區域模式從圖像提取文字（Java）](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}