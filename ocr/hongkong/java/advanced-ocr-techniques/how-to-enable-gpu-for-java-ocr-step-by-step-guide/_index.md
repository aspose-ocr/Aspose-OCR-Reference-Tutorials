---
category: general
date: 2026-11-17
description: 如何在 Java OCR 中啟用 GPU，以快速從圖像中提取文字。了解如何設定 GPU、提取文字以及使用 Aspose OCR 進行 Java
  文字辨識。
draft: false
keywords:
- how to enable gpu
- high resolution ocr
- aspose ocr java
- extract text image java
- gpu acceleration ocr
lastmod: 2026-11-17
og_description: 快速啟用 Java OCR 的 GPU。本指南說明如何設定 GPU、從圖像提取文字，以及使用 Aspose OCR 進行 Java
  文字辨識。
og_image_alt: 'Developer guide: Enable GPU for Java OCR using Aspose OCR library'
og_title: 如何為 Java OCR 啟用 GPU – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: How to enable GPU in Java OCR to extract text from image fast. Learn
    how to configure GPU, extract text and recognize text java with Aspose OCR.
  headline: How to enable GPU for Java OCR – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes, you can pass a PDF file directly to `setImage`; the library rasterizes
      each page before OCR.
    question: Does Aspose OCR support PDF input?
  - answer: Use `ocrEngine.getConfiguration().setCustomDictionary(List<String>)` to
      improve recognition of specialized vocabulary.
    question: How do I add custom dictionaries for domain‑specific terms?
  - answer: Currently only CUDA‑compatible NVIDIA GPUs on Windows and Linux are supported;
      macOS users fall back to CPU.
    question: Is GPU acceleration available on macOS?
  - answer: Absolutely—`OcrResult` includes a `getConfidence()` method for each `OcrWord`
      object.
    question: Can I retrieve the confidence score for each recognized word?
  - answer: A commercial Aspose OCR license is required for production deployments;
      a free evaluation license works for development and testing.
    question: What license is required for production use?
  type: FAQPage
tags:
- gpu ocr
- java ocr
- aspose ocr
- high resolution ocr
- java image processing
title: 如何為 Java OCR 啟用 GPU – 逐步指南
url: /zh-hant/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何為 Java OCR 啟用 GPU – 步驟指南

如果你正在尋找 **如何在 Java 中啟用 GPU** 以從圖像中提取文字，你已經來對地方了。GPU 加速可以將 OCR 處理時間從數秒縮短到毫秒，尤其是在高解析度掃描時。本指南將逐步說明安裝 Aspose OCR、設定 GPU 裝置，以及執行一個在支援 GPU 與僅使用 CPU 的機器上皆能可靠運作的完整文字提取程式。

## 快速解答
- **最低需要的 Java 版本是什麼？** Java 17 或更新版本。
- **需要哪種 GPU？** 任何相容 CUDA 的 NVIDIA GPU（CUDA 11+）。
- **執行範例需要授權嗎？** 開發階段可使用免費試用版；正式上線需購買商業授權。
- **GPU OCR 快多少？** 相較於 CPU，在 4 MP 圖像上可提升至 5 倍。
- **可以自動回退到 CPU 嗎？** 可以 — Aspose OCR 會在偵測不到 GPU 時自動切換回 CPU。

## 什麼是 OCR 的 GPU 加速？
OCR 的 GPU 加速指的是將神經網路推論步驟在圖形處理器上執行，而非 CPU，從而利用上千條平行運算核心。這可大幅降低推論延遲，特別是對於高解析度圖像，CPU 否則會成為瓶頸。

## 為什麼選擇 Aspose OCR for Java？
Aspose OCR 支援 **超過 50 種輸入格式**（包括 PNG、JPEG、TIFF、PDF），且能在不將整個檔案載入記憶體的情況下處理上百頁文件。其 Java API 僅提供一個 `OcrEngine` 類別，將低階 CUDA 呼叫抽象化，讓你專注於業務邏輯。

## 前置條件
- 已安裝 Java 17+ JDK。
- Maven 3.6+ 或 Gradle 7+ 用於相依管理。
- 相容 CUDA 的 NVIDIA GPU，驅動程式需符合 CUDA 11.x 或更新版本。
- 具備網路連線以下載 Aspose OCR 函式庫。

## 如何為 Java OCR 啟用 GPU？
載入 Aspose OCR 函式庫，建立 `OcrEngine`，並在幾行程式碼內開啟 GPU 支援。引擎會自動偵測可用裝置；你也可以在多 GPU 環境中指定裝置 ID 以鎖定特定 GPU。

## OcrEngine 如何運作？
`OcrEngine` 是核心類別，負責影像前處理、神經網路推論與結果彙總。它接受檔案路徑、`java.io.File` 物件或 `java.awt.image.BufferedImage` 實例，提供彈性資料輸入方式。

## 如何設定 GPU 加速（how to configure GPU）
以下說明如何告訴 Aspose OCR 使用 GPU 以及選擇哪一個裝置。

要啟用 GPU 加速，你需要建立 `GpuConfiguration` 實例，呼叫 `setEnable(true)`，必要時使用 `setDeviceId(int)` 指定裝置，並透過 `setGpuConfiguration` 附加至 `OcrEngine`。此設定亦允許定義回退策略，例如在請求的裝置不可用時自動切換回 CPU，確保應用程式穩定運行。  

```java
        // Step 3: Enable GPU acceleration (optional: select a specific device)
        GpuConfiguration gpuConfig = new GpuConfiguration();
        gpuConfig.setEnabled(true);          // turn on GPU support
        gpuConfig.setDeviceId(0);            // choose GPU 0 (default first device)

        // Attach the GPU config to the OCR engine
        ocrEngine.setGpuConfiguration(gpuConfig);
```

為什麼要啟用 GPU？OCR 流程會執行多個卷積神經網路。將這些網路放到 GPU 上執行，可利用上千條平行核心，將推論時間從 CPU 的 3–5 秒縮短至現代 RTX 3080 上的 1 秒以下（以 4 MP 圖像為例）。若指定的裝置不存在，Aspose 會靜默回退至 CPU，避免程式崩潰。

### 邊緣案例處理

穩健的應用程式需要在嘗試使用 GPU 前先驗證已安裝 CUDA 驅動程式。

```java
        // Verify that a GPU was actually engaged
        if (!gpuConfig.isEnabled() || !gpuConfig.isDeviceAvailable()) {
            System.out.println("GPU not detected – falling back to CPU. " +
                               "Performance will be slower.");
        }
```

## 第一步 – 安裝 Aspose OCR 並準備圖像（how to enable GPU）

首先，將 Aspose OCR 相依加入專案。若使用 Maven，請加入：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- latest as of Jan 2026 -->
</dependency>
```

Gradle 使用者可加入：

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

將高解析度檔案（例如 `sample-highres.png`）放在程式碼可參考的資料夾中。為取得最佳 OCR 準確度，圖像解析度至少需為 300 dpi。

> **專業提示：** 若在沒有獨立 GPU 的筆記型電腦上測試，程式仍會執行；引擎會自動回退至 CPU。

![如何啟用 GPU 插圖](placeholder.png "顯示 Java OCR 流程與 GPU 加速的圖示 – 如何啟用 GPU")
[如何啟用 GPU 插圖](placeholder.png "顯示 Java OCR 流程與 GPU 加速的圖示 – 如何啟用 GPU")

## 第二步 – 建立 OCR 引擎並載入圖像（extract text from image）

`OcrEngine` 類別是代表單一 OCR 工作階段的最高層物件。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.*;

public class GpuOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to process
        // Replace with the absolute or relative path to your PNG/JPEG/TIFF
        ocrEngine.setImage("YOUR_DIRECTORY/sample-highres.png");
```

`setImage` 方法接受檔案路徑、`java.io.File` 或 `java.awt.image.BufferedImage`。提供高解析度來源可確保 GPU 有足夠像素讓所有核心保持忙碌，從而帶來顯著的速度提升。

## 第三步 – 設定 GPU 加速（how to configure GPU）

`GpuConfiguration` 物件讓你啟用 GPU 使用、選擇裝置，並為 OCR 引擎定義回退行為。

```java
        // Step 3: Enable GPU acceleration (optional: select a specific device)
        GpuConfiguration gpuConfig = new GpuConfiguration();
        gpuConfig.setEnabled(true);          // turn on GPU support
        gpuConfig.setDeviceId(0);            // choose GPU 0 (default first device)

        // Attach the GPU config to the OCR engine
        ocrEngine.setGpuConfiguration(gpuConfig);
```

## 第四步 – 執行文字辨識（recognize text java）

在引擎與 GPU 準備就緒後，即可開始提取文字。

`recognize()` 方法會執行 OCR 流程，並回傳包含純文字、信心分數及可選的邊框資料的 `OcrResult`。  

```java
        // Step 4: Perform the recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**預期輸出**（為簡潔起見已截斷）：

```
Recognized text:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

若圖像包含多種語言，可在呼叫 `recognize()` 前加入語言套件：

```java
ocrEngine.getLanguage().add(OcrLanguage.FRENCH);
ocrEngine.getLanguage().add(OcrLanguage.SPANISH);
```

## 第五步 – 檢視輸出與後續步驟

使用以下指令執行程式：

```bash
mvn compile exec:java -Dexec.mainClass=GpuOcrTutorial
```

在配備不錯的 GPU 機器上，OCR 可在 **4 MP 圖像下於一秒內完成**，相較於僅使用 CPU 時的 3–5 秒有明顯提升。此速度提升在批次處理或即時文件攝取管線中特別有價值。

### 常見問題

* **如果出現「CUDA driver version is insufficient」錯誤該怎麼辦？**  
  更新 NVIDIA 驅動程式至與 Aspose 捆綁的 CUDA 工具組相符的最新版本（截至 2026 年通常為 CUDA 11.x）。

* **可以一次處理多張圖像嗎？**  
  可以。於迴圈中重複使用同一個 `OcrEngine` 實例，可避免重複建立 GPU 上下文，提升吞吐量。

* **有記憶體限制嗎？**  
  GPU 記憶體使用量會隨圖像大小成長；對於特別大的 TIFF，建議將圖像切割成多塊後再送入引擎，以維持在一般 8 GB GPU 記憶體的限制內。

### 專業提示

* **固定 GPU** – 在多 GPU 伺服器上，使用 `gpuConfig.setDeviceId(1)` 讓第二顆 GPU 專屬 OCR，第一顆則處理其他工作負載。  
* **預熱** – 在啟動時對一張極小的測試圖像呼叫一次 `ocrEngine.recognize()`，可將神經網路載入 GPU，消除首次呼叫的延遲。  
* **執行緒安全** – 每個執行緒應擁有自己的 `OcrEngine` 實例；此類別本身非執行緒安全，跨執行緒共享會導致競爭條件。

## 常見問答

**Q: Aspose OCR 支援 PDF 輸入嗎？**  
A: 支援，你可以直接將 PDF 檔傳給 `setImage`；函式庫會在 OCR 前先將每頁光柵化。

**Q: 如何加入自訂詞典以辨識領域專有詞彙？**  
A: 使用 `ocrEngine.getConfiguration().setCustomDictionary(List<String>)` 以提升特定詞彙的辨識率。

**Q: GPU 加速在 macOS 上可用嗎？**  
A: 目前僅支援 Windows 與 Linux 上相容 CUDA 的 NVIDIA GPU；macOS 使用者會回退至 CPU。

**Q: 能取得每個辨識單字的信心分數嗎？**  
A: 完全可以 — `OcrResult` 為每個 `OcrWord` 物件提供 `getConfidence()` 方法。

**Q: 生產環境需要什麼授權？**  
A: 需要商業版 Aspose OCR 授權；開發與測試階段可使用免費評估授權。

---

**最後更新：** 2026-11-17  
**測試環境：** Aspose OCR 24.11 for Java  
**作者：** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- latest as of Jan 2026 -->
</dependency>
```

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

## 相關教學

- [Aspose Ocr Java Example Extract Text From Image With Gpu](/ocr/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-image-with-gpu/)
- [Recognize Text From Image Java Ocr With Gpu Acceleration](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [Gpu Accelerated Ocr Tutorial Java Guide To Fast Image To Tex](/ocr/java/advanced-ocr-techniques/gpu-accelerated-ocr-tutorial-java-guide-to-fast-image-to-tex/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}