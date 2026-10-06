---
category: general
date: 2026-02-27
description: 學習如何在 Aspose OCR Java 程式碼中啟用 GPU，以從圖像中提取文字。將相片轉換為文字，並高效辨識相片中的文字。
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert photo to text
- how to extract text
- recognize text from photo
language: zh-hant
og_description: 如何在 Aspose OCR Java 中啟用 GPU，快速從圖像提取文字。輕鬆將相片轉換為文字，並辨識相片中的文字。
og_title: 如何在 Java 中啟用 GPU 進行 OCR – 快速文字提取
tags:
- OCR
- Java
- GPU
- Aspose
title: 在 Java 中啟用 GPU 進行光學字符辨識 – 從圖像提取文字
url: /zh-hant/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中啟用 GPU 進行 OCR – 從圖像提取文字

有沒有想過 **如何在執行 OCR 時啟用 GPU**，尤其是處理高解析度照片時？你並不孤單。許多 Java 開發者在僅使用 CPU 的環境下，當圖像大小超過幾百萬像素時，OCR 流程會變得非常緩慢。好消息是：使用 Aspose OCR 啟用 GPU 加速非常簡單，且能在極短的時間內 **從圖像中提取文字**。

在本教學中，我們將一步步說明整個流程：從設定 Aspose OCR 函式庫、打開 GPU 開關、載入大型圖片，最後 **將照片轉換為文字**。完成後，你將能可靠地 **提取文字**，並了解如何在多 GPU 機器上 **從照片中辨識文字**。不需要外部參考文件——所有內容都在此處。

## 前置條件

在開始之前，請確保你已具備以下條件：

* 已安裝 Java 17 或更新版本（最新的 LTS 版最佳）。
* 支援的 NVIDIA 或 AMD GPU，且已安裝最新驅動（NVIDIA 使用 CUDA 12.x，AMD 使用 ROCm）。
* Aspose OCR for Java JAR——從 Aspose 官網取得最新的 23.x 版。
* Maven 或 Gradle 以管理相依性（我們將示範 Maven 片段）。
* 一張高解析度圖像（例如 `high-res-photo.jpg`）供處理。

若缺少上述任一項，程式仍能編譯，但 GPU 開關會被忽略，會退回使用 CPU 處理。

## 步驟 1 – 將 Aspose OCR 加入建置 (如何啟用 GPU)

首先，告訴專案 OCR 函式庫的所在位置。於 Maven 中，於 `pom.xml` 加入以下相依性：

```xml
<!-- Step 1: Include Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

> **小技巧：** 若使用 Gradle，等價寫法為 `implementation 'com.aspose:aspose-ocr:23.10'`。保持函式庫為最新版本，可確保取得最新的 GPU 核心與錯誤修正。

現在函式庫已在 classpath 中，我們就可以在 OCR 引擎中 **啟用 GPU**。

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

> **為什麼重要：** 設定 `setUseGpu(true)` 會告訴底層原生函式庫將繁重的卷積神經網路運算交給 GPU。以 RTX 3080 為例，同一張圖片在 CPU 上需要 8 秒，使用 GPU 可在不到 1 秒內完成。若省略此步驟，仍能 **從照片中辨識文字**，但無法獲得效能提升。

## 步驟 3 – 驗證 GPU 是否真的在使用

你可能會問，「GPU 真的是在工作嗎？」最簡單的檢查方式是開啟 Aspose OCR 的除錯日誌，觀察主控台輸出：

```java
// Enable verbose logging – helpful for confirming GPU usage.
ocrEngine.getConfig().setLogLevel(com.aspose.ocr.Config.LogLevel.DEBUG);
```

執行程式時，你會看到類似以下的訊息：

```
[DEBUG] Using GPU device 0 (NVIDIA GeForce RTX 3080) for OCR processing.
```

若未看到此訊息，請再次確認驅動程式安裝情況，並確保 GPU 符合最低運算能力（NVIDIA 3.5，AMD 6.0）。

## 步驟 4 – 處理多 GPU 與邊緣情況

### 選擇不同的 GPU

如果工作站有多張 GPU（例如內建 Intel GPU 與獨立 NVIDIA 卡），可以指定較快的那張：

```java
ocrEngine.getConfig().setGpuDeviceId(1); // 1 = second GPU in the system
```

### 若未偵測到 GPU 該怎麼辦？

Aspose OCR 在找不到合適的 GPU 時會自動回退至 CPU。若想避免靜默回退，可加入以下防護：

```java
if (!ocrEngine.getConfig().isGpuAvailable()) {
    throw new IllegalStateException("No compatible GPU found – cannot enable GPU acceleration.");
}
```

### 大圖與記憶體限制

處理 100 MP 圖片仍可能耗盡 GPU 記憶體。一個實用技巧是 **適度縮小圖像**，在不影響文字清晰度的前提下，保持在記憶體上限內：

```java
ocrEngine.getConfig().setMaxImageDimension(4096); // caps width/height to 4096px
```

### 支援的圖像格式

Aspose OCR 支援 JPEG、PNG、BMP、TIFF，甚至 PDF。若需要 **從圖像中提取文字** 的檔案是其他格式，請先使用如 ImageIO 等函式庫轉換。

## 步驟 5 – 預期輸出與驗證

程式結束時，主控台會印出原始 OCR 文字。以一般收據照片為例，可能會看到：

```
Store: Coffee Corner
Date: 2026-02-25
Items:
  - Latte $4.50
  - Croissant $2.75
Total: $7.25
```

若輸出雜亂，請考慮：

* 確認圖像光線充足且未過度壓縮。
* 若文字非英文，調整 `setLanguage` 參數。
* 確認 GPU 核心版本與驅動程式相符（版本不匹配可能導致細微異常）。

## 步驟 6 – 進階應用：批次處理與非同步呼叫

實務上常需要 **從圖像中提取文字** 的集合。你可以將上述邏輯包在迴圈中，或使用 Java 的 `CompletableFuture` 讓多個 OCR 工作平行執行，並在支援的硬體上使用不同的 GPU 串流。以下是一個快速示範：

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

此方式讓你在規模化處理時仍能 **將照片轉換為文字**，同時受惠於 GPU 加速。

## 常見問題 (FAQ)

**Q: 這在 macOS 上可用嗎？**  
A: 可以，只要你的 GPU 支援 Metal，且下載相對應的 Aspose OCR macOS 二進位檔。`setUseGpu(true)` 呼叫方式相同。

**Q: 可以使用免費的 Community Edition 嗎？**  
A: Community Edition 只提供 CPU 推論。若要解鎖 GPU，需要購買授權版（或使用含 GPU 支援的試用版）。

**Q: 若要 **從照片中辨識文字**，但語言不是英文該怎麼辦？**  
A: 呼叫 `ocrEngine.getConfig().setLanguage("spa")` 取得西班牙文，`"fra"` 取得法文，依此類推。語言包已隨函式庫一起提供。

**Q: 有辦法取得每個單字的信心分數嗎？**  
A: 有——`ocrResult.getWords()` 會回傳 `Word` 物件集合，每個 `Word` 都有 `getConfidence()` 方法。

## 結論

我們已說明 **如何在 Java 中啟用 GPU** 以使用 Aspose OCR，示範完整可執行範例，並探討在 **從圖像中提取文字**、**將照片轉換為文字**、或 **從照片中辨識文字** 時的常見陷阱。只要切換一次旗標、確保驅動程式為最新，即可在每次 OCR 呼叫上節省數秒，並在大量圖像批次處理時毫無壓力。

準備好下一步了嗎？試著將 OCR 輸出導入自然語言處理管線，或實驗不同的圖像前處理濾鏡以提升準確度。結合 GPU 加速的 OCR 與現代 Java 工具，讓你的應用無限可能。

---

![Diagram showing how to enable GPU in Aspose OCR Java code – how to enable gpu](gpu-ocr-diagram.png)

*圖片替代文字:* 「說明如何在 Aspose OCR Java 程式碼中啟用 GPU 的圖示 – how to enable gpu」

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}