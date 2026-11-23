---
category: general
date: 2026-10-19
description: 了解如何在 Aspose OCR Java 程式碼中啟用 GPU，以從圖像提取文字。將相片轉換為文字，並高效辨識相片中的文字。
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert photo to text
- how to extract text
- recognize text from photo
lastmod: 2026-10-19
og_description: 在 Java 中啟用 GPU 進行 OCR 可讓您快速從圖像提取文字，將處理時間縮短至現代 GPU 上的最高 90%。了解逐步設定、程式碼範例與除錯技巧。
og_image_alt: Diagram illustrating how to enable GPU in Aspose OCR Java code – how
  to enable gpu
og_title: 如何在 Java 中啟用 GPU 進行 OCR – 快速文字提取
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: Learn how to enable GPU in Aspose OCR Java code to extract text from
    image. Convert photo to text and recognize text from photo efficiently.
  headline: How to Enable GPU for OCR in Java – Extract Text from Image
  type: TechArticle
- questions:
  - answer: Yes, as long as you have a Metal‑compatible GPU and the appropriate Aspose
      OCR binary for macOS. The same `setUseGpu(true)` call applies.
    question: Does this work on macOS?
  - answer: The Community Edition includes CPU‑only inference. To unlock GPU you need
      a licensed version (or a trial that includes GPU support).
    question: Can I use the free Community Edition?
  - answer: Call `ocrEngine.getConfig().setLanguage("spa")` for Spanish, `"fra"` for
      French, etc. Language packs are bundled with the library.
    question: What if I need to **recognize text from photo** in a language other
      than English?
  - answer: Yes—`ocrResult.getWords()` returns a collection where each `Word` object
      has a `getConfidence()` method.
    question: Is there a way to get confidence scores for each word?
  - answer: After creating the engine, invoke `ocrEngine.getConfig().setRequireGpu(true)`.
      The library will throw an exception if no compatible GPU is found, preventing
      silent CPU fallback.
    question: How can I enforce a strict GPU‑only mode?
  type: FAQPage
tags:
- OCR
- Java
- GPU
- Aspose
title: 如何在 Java 中啟用 GPU 進行 OCR – 從圖像提取文字
url: /zh-hant/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中啟用 GPU 進行 OCR – 從圖像提取文字

有沒有想過在高解析度照片上執行 OCR 時如何**啟用 GPU**？你並不孤單。許多 Java 開發者在僅使用 CPU 的環境下，當 OCR 流程因圖像尺寸超過數百萬像素而變得緩慢時，常會卡住。好消息是？使用 Aspose OCR 啟用 GPU 加速非常簡單，且能讓你在極短的時間內**從圖像提取文字**。

在本教學中，我們將逐步說明整個流程：從設定 Aspose OCR 函式庫、打開 GPU 標誌、輸入大型圖片，最後**將相片轉換為文字**。完成後，你將能可靠地**啟用 GPU**，並且了解在具備多個 GPU 的機器上如何**從相片辨識文字**。不需要任何外部參考——所有資訊都在此處。

## 快速回答
- **啟用 GPU 會有什麼作用？** 它會將 OCR 神經網路推論卸載至顯示卡，於現代硬體上將處理時間縮短最多 90 %。
- **我需要特別的授權嗎？** 是的，GPU 支援僅在授權的 Aspose OCR for Java 版（或包含 GPU 核心的試用版）中提供。
- **支援哪些 GPU？** NVIDIA GPU（CUDA 12.x，運算能力 3.5+）以及 AMD GPU（ROCm 5.x，運算能力 6.0+）。
- **能自動回退到 CPU 嗎？** 函式庫會偵測缺失或不相容的 GPU，並透明地切換至 CPU，但你也可以強制僅使用 GPU 模式。
- **程式碼與 Java 17 相容嗎？** 完全相容——Aspose OCR 23.x 以 Java 11+ 為目標，且在 Java 17 上運行無礙。

## 什麼是 OCR 的 GPU 加速？

GPU 加速 OCR 是指使用圖形處理器來執行辨識字元的深度學習模型，而非使用 CPU。此方式可大幅提升文字提取速度，尤其針對大型或批次處理的圖像。將繁重的卷積層搬移至 GPU 後，延遲降低、吞吐量提升，使高解析度照片的即時處理成為可能。

## 為什麼要使用 Aspose OCR 的 GPU 模式？

Aspose OCR 支援**超過 50 種輸入格式**（JPEG、PNG、BMP、TIFF、PDF 等），在 RTX 3080 上可於一秒內處理 20 MP 圖像，而高階 CPU 需約 8 秒。函式庫亦提供內建回退、超過 30 種語言的語言包，以及只需單一旗標即可啟用 GPU 的簡易 Java API。

## 前置條件

- 已安裝 Java 17 或更新版本。  
- 支援的 NVIDIA 或 AMD GPU，且驅動程式為最新（NVIDIA 使用 CUDA 12.x，AMD 使用 ROCm 5.x）。  
- Aspose OCR for Java JAR 檔案 – 從 Aspose 官方網站下載最新的 23.x 版本。  
- Maven 或 Gradle 以管理相依性（本教學將示範 Maven 片段）。  
- 你想要處理的高解析度圖像（例如 `high-res-photo.jpg`）。

若缺少上述任一項目，程式仍會編譯通過，但 GPU 旗標將被忽略，並回退至 CPU 處理。

## 如何在 Java 中啟用 GPU 進行 OCR？

載入 OCR 引擎，呼叫 `setUseGpu(true)`，然後使用 `recognize` 方法處理圖像。這一行即可啟動支援卷積神經網路的 GPU 核心。**`setUseGpu(true)` 會為 OCR 引擎啟用 GPU 處理。** OCR 引擎是 `com.aspose.ocr.OcrEngine` 的實例，用於執行文字辨識。

## 步驟 1 – 將 Aspose OCR 加入你的建置 (如何啟用 GPU)

首先，告訴你的專案 OCR 函式庫的所在位置。在 Maven 中，將以下相依性加入你的 `pom.xml`：

```xml
<!-- Step 1: Include Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

> **小技巧：** 若你使用 Gradle，等價寫法為 `implementation 'com.aspose:aspose-ocr:23.10'`。保持函式庫為最新版本可確保取得最新的 GPU 核心與錯誤修正。

現在函式庫已在 classpath 中，我們即可在 OCR 引擎中**啟用 GPU**。

## 步驟 2 – 建立 OCR 引擎並開啟 GPU (如何啟用 GPU)

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Instantiate the OCR engine – this is the core object.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration.
        // This is the line that answers the question "how to enable gpu".
        ocrEngine.getConfig().setUseGpu(true);

        // Optional: If your system has more than one GPU, pick the one you want.
        // The device ID is zero‑based, so 0 refers to the first GPU.
        // ocrEngine.getConfig().setGpuDeviceId(0);

        // Step 2.3: Process the image and get the result.
        OcrResult ocrResult = ocrEngine.processImage("YOUR_DIRECTORY/high-res-photo.jpg");

        // Step 2.4: Print the recognized text – now you have converted photo to text.
        System.out.println(ocrResult.getText());
    }
}
```

> **為什麼重要：** 設定 `setUseGpu(true)` 會告訴底層原生函式庫將繁重的卷積神經網路工作卸載至 GPU。以現代 RTX 3080 為例，同一張圖像在 CPU 上需 8 秒，使用 GPU 可在不到 1 秒完成。若跳過此步驟，你仍能**從相片辨識文字**，但無法獲得效能提升。

## 步驟 3 – 驗證 GPU 是否真的在使用中

你可能會想，「GPU 真的是在執行工作嗎？」最簡單的檢查方式是啟用除錯日誌時，觀察 Aspose OCR 函式庫的主控台輸出：

```java
// Enable verbose logging – helpful for confirming GPU usage.
ocrEngine.getConfig().setLogLevel(com.aspose.ocr.Config.LogLevel.DEBUG);
```

執行程式時，你會看到類似以下的行：

```
[DEBUG] Using GPU device 0 (NVIDIA GeForce RTX 3080) for OCR processing.
```

若未看到該訊息，請再次確認驅動程式安裝情況，並確保 GPU 符合最低運算能力（NVIDIA 為 3.5，AMD 為 6.0）。

## 步驟 4 – 處理多 GPU 與邊緣案例

### 選擇不同的 GPU

如果你的工作站有多於一個 GPU（例如，內建的 Intel GPU 與獨立的 NVIDIA 顯示卡），你可以指定較快的那一個：

```java
ocrEngine.getConfig().setGpuDeviceId(1); // 1 = second GPU in the system
```

### 若未偵測到 GPU 該怎麼辦？

當無法找到合適的 GPU 時，Aspose OCR 會優雅地回退至 CPU。為避免靜默回退，你可以加入防護。**`setRequireGpu(true)` 會強制函式庫使用 GPU，若未找到則拋出例外。** 這可確保你在 GPU 不可用時得到提示。

```java
if (!ocrEngine.getConfig().isGpuAvailable()) {
    throw new IllegalStateException("No compatible GPU found – cannot enable GPU acceleration.");
}
```

### 大圖像與記憶體限制

處理 100 MP 圖像仍可能耗盡 GPU 記憶體。實用的技巧是將圖像**適度縮小**，以符合記憶體限制，同時保留文字清晰度：

```java
ocrEngine.getConfig().setMaxImageDimension(4096); // caps width/height to 4096px
```

### 支援的圖像格式

Aspose OCR 能辨識 JPEG、PNG、BMP、TIFF，甚至 PDF。若需**從圖像提取文字**的檔案為其他格式，請先使用如 ImageIO 等函式庫進行轉換。

## 步驟 5 – 預期輸出與驗證

程式執行完畢後，主控台會印出原始 OCR 文字。對於一般的收據相片，你可能會看到：

```
Store: Coffee Corner
Date: 2026-02-25
Items:
  - Latte $4.50
  - Croissant $2.75
Total: $7.25
```

若輸出看起來亂碼，請考慮以下因素：

* 確保圖像光線充足且未過度壓縮。  
* 若文字非英文，調整 `setLanguage` 選項。  
* 確認 GPU 核心版本與驅動程式相符（版本不匹配可能導致細微異常）。

**`ocrResult.getWords()` 會回傳 `Word` 物件的集合，每個物件皆可透過 `getConfidence()` 取得信心分數。** 這讓你能篩選低信心的結果。

## 步驟 6 – 更進一步：批次處理與非同步呼叫

實務專案常需對**圖像集合提取文字**。你可以將上述邏輯包在迴圈中，或使用 Java 的 `CompletableFuture` 讓多個 OCR 任務平行執行，每個任務使用獨立的 GPU 串流（若硬體支援）。以下是一個快速示意：

```java
import java.util.concurrent.*;
import java.nio.file.*;

public class BatchGpuOcr {
    public static void main(String[] args) throws Exception {
        ExecutorService pool = Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors());

        Files.list(Paths.get("photos/"))
             .filter(p -> p.toString().endsWith(".jpg"))
             .forEach(path -> pool.submit(() -> {
                 OcrEngine engine = new OcrEngine();
                 engine.getConfig().setUseGpu(true);
                 OcrResult result = engine.processImage(path.toString());
                 System.out.println("Result for " + path.getFileName() + ":\n" + result.getText());
             }));

        pool.shutdown();
        pool.awaitTermination(1, TimeUnit.HOURS);
    }
}
```

此方法讓你在規模化時仍能**將相片轉換為文字**，同時利用 GPU 加速。

## 常見問題 (FAQ)

**Q: 這在 macOS 上可用嗎？**  
A: 可以，只要你有相容 Metal 的 GPU 且有對應的 Aspose OCR macOS 二進位檔。`setUseGpu(true)` 呼叫相同。

**Q: 我可以使用免費的 Community Edition 嗎？**  
A: Community Edition 僅提供 CPU 推論。若要解鎖 GPU，需要授權版（或包含 GPU 支援的試用版）。

**Q: 若需在非英語語言中**從相片辨識文字**該怎麼辦？**  
A: 呼叫 `ocrEngine.getConfig().setLanguage("spa")` 取得西班牙語，`"fra"` 取得法語，依此類推。語言包已隨函式庫捆綁。

**Q: 有辦法取得每個字的信心分數嗎？**  
A: 有——`ocrResult.getWords()` 會回傳集合，每個 `Word` 物件都有 `getConfidence()` 方法。

**Q: 如何強制僅使用 GPU 模式？**  
A: 建立引擎後，呼叫 `ocrEngine.getConfig().setRequireGpu(true)`。若未找到相容的 GPU，函式庫會拋出例外，避免靜默回退至 CPU。

## 結論

我們已說明如何在 Java 中為 Aspose OCR **啟用 GPU**，示範完整可執行的範例，並探討在想要**從圖像提取文字**、**將相片轉換為文字**或**從相片辨識文字**時的常見陷阱。只要切換單一旗標並確保驅動程式為最新，即可為每次 OCR 呼叫節省數秒，且能輕鬆擴展至大量圖像批次。

準備好下一步了嗎？試著將 OCR 輸出導入自然語言處理管線，或嘗試不同的圖像前處理濾鏡以提升準確度。結合 GPU 加速的 OCR 與現代 Java 工具，無所不能。

---

![示意圖說明如何在 Aspose OCR Java 程式碼中啟用 GPU – 如何啟用 GPU](gpu-ocr-diagram.png)

[示意圖說明如何在 Aspose OCR Java 程式碼中啟用 GPU – 如何啟用 GPU](gpu-ocr-diagram.png)

*圖片替代文字:* 「示意圖說明如何在 Aspose OCR Java 程式碼中啟用 GPU – 如何啟用 GPU」

---

**最後更新：** 2026-10-19  
**測試環境：** Aspose OCR for Java 23.10  
**作者：** Aspose  

```xml
<!-- Step 1: Include Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

## 相關教學

- [如何為 OCR 配置 GPU 以辨識圖像文字](/ocr/java/advanced-ocr-techniques/how-to-configure-gpu-for-ocr-recognize-text-from-image/)
- [使用 Aspose OCR GPU Java 辨識圖像文字](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)
- [使用 Aspose OCR Java 指南從圖像提取文字](/ocr/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}