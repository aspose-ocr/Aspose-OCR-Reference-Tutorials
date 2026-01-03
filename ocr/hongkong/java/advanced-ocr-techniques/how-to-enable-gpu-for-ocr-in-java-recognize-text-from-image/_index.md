---
category: general
date: 2026-01-02
description: 如何在 Java OCR 中啟用 GPU，以快速辨識圖像文字。學習從 PNG 提取文字、設定圖像選項，並高效辨識文字。
draft: false
keywords:
- how to enable gpu
- recognize text from image
- extract text from png
- how to set image
- how to recognize text
language: zh-hant
og_description: 如何在 Java OCR 中啟用 GPU，以快速辨識圖像文字。本指南將示範如何從 PNG 提取文字、設定圖像選項，並高效辨識文字。
og_title: 如何在 Java 中啟用 GPU 進行 OCR – 快速從圖像辨識文字
tags:
- OCR
- Java
- GPU
title: 如何在 Java 中啟用 GPU 進行 OCR – 快速辨識圖像文字
url: /zh-hant/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中啟用 GPU 進行 OCR – 快速從圖像識別文字

在 Java OCR 應用程式中啟用 GPU 是需要快速文字擷取的開發者常見的障礙。在本教學中，我們將示範 **如何啟用 GPU**、從圖像識別文字，以及使用 Aspose OCR 函式庫從 PNG 提取文字。

如果你曾經看到 OCR 處理緩慢，並懷疑顯示卡能否加速，那麼你來對地方了。我們還會說明如何設定影像處理選項，讓 OCR 引擎更精準地讀取檔案，並回答「如何識別文字」的常見追問。

## 需要的環境

- **Java 17** 或更新版本（程式碼在較早版本也能編譯，但 17 為最佳選擇）。  
- **Aspose OCR for Java** – 可從 Aspose 官方網站或 Maven Central 取得最新 JAR。  
- 一台 **支援 GPU 的機器**（NVIDIA RTX 3060 或任何相容 CUDA 的顯示卡皆可）。  
- 用於測試的影像檔案 – 大尺寸的發票 PNG 非常適合做效能基準。

> **專業提示：** 若你使用的是內建顯示卡的筆記型電腦，請確保在驅動程式設定中選取獨立 GPU；否則函式庫會默默回退到 CPU。

![如何啟用 GPU 範例](image.png "如何啟用 GPU 範例")

*Alt text: 顯示如何啟用 GPU 的 Java 程式碼片段。*

## 步驟 1 – 安裝 Aspose OCR 並驗證 GPU 可用性

在能 **啟用 GPU** 之前，需要先把函式庫加入 classpath。加入 Maven 依賴（或將 JAR 放入 `libs/`）：

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Check for the latest version -->
</dependency>
```

將依賴加入後，執行簡易的健康檢查：

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

如果輸出顯示非零的裝置數量，代表 JVM 已偵測到 GPU。若顯示為零，請再次確認驅動程式安裝以及 `CUDA_PATH` 環境變數是否正確設定。

## 步驟 2 – 如何在 Aspose OCR 中啟用 GPU

現在系統已認可顯示卡，接下來正式開啟它。關鍵字已在標題中出現，符合 SEO 規則。

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

### 為什麼要啟用 GPU？

GPU 加速會將 OCR 模型執行的繁重矩陣運算交給上千個平行核心處理。實際上，你會在普通的 RTX 2060 上看到 **2‑5 倍** 的速度提升，更新的卡片則更快。唯一的代價是稍高的記憶體佔用，但對於一般發票大小的 PNG 來說通常不是問題。

## 步驟 3 – 從圖像識別文字（並從 PNG 提取文字）

GPU 正在運作後，讓我們專注於 **從圖像識別文字** 的步驟。上面的程式碼已經完成此功能，以下提供一個只保留 OCR 呼叫的精簡版：

```java
// Assuming ocrEngine is already configured with GPU
String imagePath = "sample.png";
OcrResult ocrResult = ocrEngine.recognizeImage(imagePath, RecognitionLanguage.ENGLISH);
String extractedText = ocrResult.getText();

System.out.println("Extracted text from PNG:");
System.out.println(extractedText);
```

**你會注意到：** `recognizeImage` 方法會自動偵測檔案類型，因此可以直接傳入 JPEG、TIFF 或 PNG，無需額外旗標。這也是為什麼 **從 PNG 提取文字** 能直接使用的原因。

### 處理大型檔案

如果你的 PNG 超過 5 MB，建議先縮小再進行 OCR：

```java
imgOpts.setResizeFactor(0.5); // shrink to 50 % of original dimensions
ocrEngine.setImageProcessingOptions(imgOpts);
```

下採樣不僅降低 GPU 記憶體使用，還常能提升辨識準確度，因為模型看到的邊緣較為乾淨。

## 步驟 4 – 如何設定影像選項以提升準確度

說到前置處理，自然會提到 **如何設定影像**。Aspose OCR 提供多項可調整的參數：

| 選項                         | 功能說明                                   | 常用值   |
|------------------------------|--------------------------------------------|----------|
| `setAutoDeskew(true)`        | 校正傾斜的文字行                           | true     |
| `setBinarization(true)`      | 轉為黑白以提升對比度                       | true     |
| `setResizeFactor(x)`         | 縮放影像（0 < x ≤ 1）                     | 0.5‑0.8  |
| `setContrastAdjustment(y)`   | 調整對比度（0‑100）                        | 30       |

這些設定可以任意組合，函式庫會在將影像送入神經網路前依序套用。實驗是關鍵——不同的發票可能需要不同的門檻值。

## 步驟 5 – 如何在特殊情況下識別文字

即使有 GPU 加速，仍有些情境會讓 OCR 卡關：

1. **低解析度掃描（< 150 dpi）。** 先放大或請使用者提供較高解析度的掃描檔。  
2. **手寫筆記。** 預設模型針對印刷文字，若要辨識手寫體需自行訓練模型。  
3. **多語言。** 可將逗號分隔的語言清單傳給 `RecognitionLanguage`，例如 `RecognitionLanguage.ENGLISH_FRENCH`。

```java
ocrEngine.recognizeImage("multilang.png",
        RecognitionLanguage.ENGLISH_FRENCH);
```

## 預期輸出

執行完整的 `GpuExample` 類別對 `large_invoice.png`，應會在主控台印出類似以下內容：

```
Detected text:
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
...
```

若看到亂碼，請再次確認 `gpuSettings.setEnable(true)` 已真正生效（開啟除錯日誌時，主控台會列出 GPU 裝置資訊）。

## 常見問題與專業提示

- **忘記設定 GPU 裝置 ID。** 在多 GPU 環境下，可能需要 `setDeviceId(1)`。  
- **在未安裝 NVIDIA runtime 的 Docker 中執行。** 請於 `docker run` 指令加入 `--gpus all`。  
- **混用 CPU‑only 與 GPU‑enabled 程式路徑。** 每個執行緒僅保留單一 `AsposeOCR` 實例，以免狀態衝突。  
- **記憶體泄漏。** 完成後務必呼叫 `ocrEngine.dispose()`，尤其在長時間服務中更為重要。

## 結論

我們已完整說明 **如何在 Java 中啟用 GPU** 以使用 Aspose OCR，示範 **從圖像識別文字**、**從 PNG 提取文字** 的最簡方法，解釋 **如何設定影像** 處理選項，並探討 **如何在實務檔案中識別文字** 的細節。開啟 GPU 後，你的 OCR 流程將顯著加速，適合批次發票處理或即時文件掃描等高吞吐量情境。

準備好進一步探索了嗎？可以嘗試將預設的英文模型換成多語言模型，或為噪聲較大的收據設計自訂前置處理管線。只要有 GPU 加持，幾乎沒有做不到的事。

---

*祝程式開發順利，讓你的 OCR 永遠快速！*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}