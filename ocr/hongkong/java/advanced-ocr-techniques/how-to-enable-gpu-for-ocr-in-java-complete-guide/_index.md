---
category: general
date: 2026-02-19
description: 如何啟用 GPU 以加快 OCR 處理。學習載入高解析度影像、辨識文字影像，並使用 Aspose OCR 提取文字。
draft: false
keywords:
- how to enable gpu
- load high resolution image
- recognize text image
- how to extract text
- enable gpu processing
language: zh-hant
og_description: 如何啟用 GPU 以加快 OCR 處理。本指南將示範如何載入高解析度影像、辨識文字圖像，並使用 Aspose OCR 提取文字。
og_title: 如何在 Java 中啟用 GPU 進行 OCR – 完整指南
tags:
- OCR
- Java
- GPU
- Aspose
title: 如何在 Java 中啟用 GPU 進行 OCR – 完整指南
url: /zh-hant/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-complete-guide/
---

.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中啟用 GPU 進行 OCR – 完整指南

有沒有想過 **如何啟用 GPU** 來加速你的 OCR 工作流程，省下幾秒鐘的處理時間？你並不孤單。在許多以圖像為主的專案中，瓶頸往往是 CPU 受限的文字擷取步驟，而改用 GPU 則可能徹底改變局面。

在本教學中，我們將示範如何載入 **高解析度影像**、設定 Aspose OCR 在 GPU 上執行，最後僅用幾行 Java 程式碼即可 **recognize text image** 與 **extract text**。完成後，你將擁有一個可直接執行的範例程式，完整展示 **enable GPU processing** 的全流程。

## 你需要的環境

- Java 17 或更新版本（程式碼使用模組系統，但在較舊 JDK 上只要稍作調整亦可運作）  
- Aspose OCR for Java 23.10（或最新版本）——可從 Aspose 官方網站取得 Maven 坐標  
- 具備 CUDA 12+ 驅動程式的 NVIDIA GPU（否則函式庫將無法啟動）  
- 你想要辨識文字的高解析度樣本影像（PNG 或 JPEG）  

就這樣。無需外部服務、無需雲端額度，只要你的機器與正確的驅動程式堆疊即可。

![GPU OCR 工作流程 – 如何啟用 GPU 處理](gpu-ocr-workflow.png)

*圖片說明：示意圖說明如何在 Java 中啟用 GPU 進行 OCR 處理。*

## 步驟實作說明

以下我們將解決方案拆分為多個邏輯區塊。每個章節都包含簡潔的程式碼片段、說明此步驟 **為何** 重要的解說，以及一些你之後可能會感激的實用小技巧。

### 如何啟用 GPU 進行 OCR – 步驟 1：安裝相依性與驗證 CUDA

在執行任何 Java 程式碼之前，必須能找到本機的 CUDA 執行環境。於 Windows 系統可使用以下指令驗證：

```bat
nvcc --version
```

在 Linux 上：

```bash
nvidia-smi
```

如果指令顯示驅動程式版本與 GPU 資訊，代表已可使用。否則請前往 NVIDIA 官方網站下載相應的驅動程式，並安裝 CUDA 工具組（務必確保版本符合 Aspose OCR 的需求——目前為 12.x）。

**提示：** 請保持 GPU 驅動程式為最新穩定版，但避免使用「latest‑beta」版；此類版本有時會破壞 Aspose 原生函式庫的二進位相容性。

### 如何啟用 GPU 進行 OCR – 步驟 2：加入 Aspose OCR Maven 相依性

將以下內容加入你的 `pom.xml`。此設定會下載核心 OCR 引擎以及 Windows、Linux、macOS 的原生 GPU 二進位檔。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

如果你偏好使用 Gradle，等價的設定如下：

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

重新整理專案後，`OcrEngine`、`OcrDeviceType` 與 `ImageStream` 類別即可使用。

### 如何啟用 GPU 進行 OCR – 步驟 3：建立 OCR 引擎並啟用 GPU

現在我們實際告訴 Aspose 在 GPU 上執行。`OcrEngine` 會公開一個 `Device` 物件，我們可以在此切換處理裝置類型。

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 3.1: Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3.2: Enable GPU processing (requires a CUDA‑enabled driver & runtime)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Optional: limit the number of GPU streams for better resource control
        ocrEngine.getDevice().setStreamCount(2);

        // Step 3.3: Load the high‑resolution image to be recognized
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample-highres.png"));

        // Step 3.4: Perform OCR and retrieve the recognized text
        String recognizedText = ocrEngine.recognize().getText();

        // Step 3.5: Display the extracted text
        System.out.println("=== OCR RESULT ===");
        System.out.println(recognizedText);
    }
}
```

**為何重要：** 設定 `OcrDeviceType.GPU` 會將底層推論引擎從僅 CPU 的實作切換為 CUDA 加速版。可選的 `setStreamCount` 呼叫讓你控制平行度；在大多數消費級顯示卡上，兩個串流是安全的預設值。

### 如何啟用 GPU 進行 OCR – 步驟 4：載入高解析度影像

高解析度的來源能為 OCR 模型提供更多視覺細節，進而提升準確度，尤其是對於小字體或複雜文字。`ImageStream.fromFile` 輔助函式會將檔案讀取為引擎所需的格式。

如果你需要從 URL 或記憶體位元組陣列 **載入高解析度影像**，可以使用：

```java
byte[] imageBytes = java.nio.file.Files.readAllBytes(Paths.get("remote-image.png"));
ocrEngine.setImage(ImageStream.fromBytes(imageBytes));
```

**邊緣情況：** 部分 GPU 的最大紋理尺寸有限制（常見為 16384 × 16384）。若影像超過此尺寸，請考慮縮小至仍能保持可讀性的大小（例如 3000 × 2000）。若在載入前呼叫 `ocrEngine.setResizeFactor(0.5)`，OCR 引擎會自動調整大小。

### 如何啟用 GPU 進行 OCR – 步驟 5：辨識文字影像並擷取文字

呼叫 `ocrEngine.recognize()` 會在 GPU 上觸發神經網路推論。此方法會回傳 `OcrResult` 物件；使用 `getText()` 可取得純文字字串。若需要更豐富的資訊，亦可取得邊界框、信心分數或原始 JSON。

```java
OcrResult result = ocrEngine.recognize();
String plainText = result.getText();
System.out.println("Detected text length: " + plainText.length());

// Optional: iterate over each line with its confidence
result.getPages().forEach(page -> {
    page.getLines().forEach(line -> {
        System.out.printf("Line: \"%s\" (Confidence: %.2f%%)%n",
                line.getText(), line.getConfidence() * 100);
    });
});
```

**為何需要這樣做：** `recognize text image` 步驟正是 GPU 發揮威力之處——大型影像在 CPU 上可能需要數秒，而在 GPU 上僅需一小段時間。信心分數可用於過濾低品質結果，這在你之後 **如何擷取文字** 以進行下游分析時相當實用。

### 專業提示與常見陷阱

| Situation | What to Do |
|-----------|------------|
| **GPU 記憶體不足** 錯誤 | Reduce `setStreamCount` to 1, or down‑scale the image before feeding it to the engine. |
| **未辨識的字元** 儘管解析度高 | Ensure the language model (`ocrEngine.setLanguage(OcrLanguage.ENGLISH)`) matches the text language. |
| **CUDA 版本不匹配** | Align the CUDA toolkit version with the one bundled in Aspose OCR (check the release notes). |
| **多顯示卡** | Use `ocrEngine.getDevice().setDeviceId(1)` to pick the second GPU if the first is busy. |
| **在無頭伺服器上執行** | No extra steps needed; the GPU driver works without a display. |

## 如何擷取文字 – 驗證輸出

執行上述類別時，你應該會看到類似以下的輸出：

```
=== OCR RESULT ===
Welcome to the Aspose OCR demo!
Your GPU is now accelerating text extraction.
```

若輸出呈現亂碼，請再次確認影像確實為高解析度且 GPU 驅動程式已正確安裝。你也可以開啟詳細日誌：

```java
ocrEngine.setLogLevel(OcrLogLevel.DEBUG);
```

日誌會顯示原生 CUDA 核心是否成功載入。

## 後續步驟與相關主題

- **批次處理：** 將 `OcrEngine` 包在迴圈中，並提供影像路徑清單。記得重複使用同一個引擎實例，以避免重複的 GPU 初始化開銷。  
- **語言偵測：** Aspose OCR 支援超過 30 種語言。可使用 `ocrEngine.setLanguage(OcrLanguage.FRENCH)` 進行切換。  
- **後處理：** 使用正規表達式清理擷取的字串，或將其送入下游的 NLP 流程。  
- **替代裝置：** 若沒有支援 CUDA 的 GPU，可改用 `OcrDeviceType.CPU`。相同程式碼仍可運作，只需更改裝置類型。  
- **效能基準測試：** 使用 `System.nanoTime()` 在 `recognize()` 前後測量時間差，以量化 **enable GPU processing** 所帶來的效益。

---

### 總結

我們已說明如何在 Java 中 **啟用 GPU** 以使用 Aspose OCR，從安裝正確的驅動程式、載入 **高解析度影像**、**recognize text image**，最後 **如何擷取文字**。上述完整且可執行的範例應能在任何現代 NVIDIA GPU 上直接運作。

試著執行它，實驗不同的影像尺寸，觀察 OCR 吞吐量的提升。若遇到任何問題，請回顧提示部分或查閱 Aspose 的發行說明，以取得最新的 **enable GPU processing** 建議。

祝開發順利，願你的 GPU 在處理文字時保持涼爽！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}