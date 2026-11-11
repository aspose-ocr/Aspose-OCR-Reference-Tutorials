---
category: general
date: 2026-09-23
description: 了解如何透過在 Aspose OCR for Java 中啟用 GPU 加速，快速從 TIFF 檔案提取文字。一步一步的指南涵蓋載入 TIFF、設定
  GPU 裝置 ID 以及讀取文字。
draft: false
keywords:
- extract text from tiff file
- gpu acceleration java
- ocr tiff java
- aspose ocr gpu
lastmod: 2026-09-23
og_description: 了解如何透過在 Aspose OCR for Java 中啟用 GPU 加速，快速從 TIFF 檔案提取文字。指南示範載入 TIFF、選擇
  GPU 裝置以及讀取提取的文字。
og_image_alt: 'Tutorial image: enabling GPU for OCR in Java'
og_title: 在 OCR Java 中使用 GPU 加速提取 TIFF 檔案文字
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to extract text from tiff file quickly by enabling GPU acceleration
    in Aspose OCR for Java. Step‑by‑step guide covers loading TIFF, setting GPU device
    ID, and reading text.
  headline: How to extract text from tiff file using GPU in OCR Java
  type: TechArticle
- questions:
  - answer: Absolutely—Aspose OCR runs on Windows, Linux, and macOS as long as the
      CUDA toolkit and drivers are installed.
    question: Does this work on Linux?
  - answer: Omit the `setUseGpu(true)` call or explicitly call `setUseGpu(false)`;
      the engine will run on CPU.
    question: What if I don’t have a GPU?
  - answer: Yes. `setImage` accepts JPEG, PNG, BMP, PDF, and more.
    question: Can I extract text from other formats?
  - answer: Accuracy drops sharply below 300 dpi. Pre‑process the image (binarization,
      deskew) for better results.
    question: How accurate is OCR on low‑resolution TIFFs?
  - answer: The library handles 30+ raster and document formats, including TIFF, JPEG,
      PNG, BMP, PDF, and GIF.
    question: How many formats does Aspose OCR support?
  type: FAQPage
tags:
- OCR
- Java
- GPU acceleration
title: 如何在 OCR Java 中使用 GPU 從 TIFF 檔案提取文字
url: /zh-hant/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 GPU 在 OCR Java 中從 tiff 檔案提取文字

如果您需要快速 **從 tiff 檔案提取文字**，在 Aspose OCR for Java 中開啟 GPU 加速是最快的方法。在前 100 個字中，我們將說明 GPU 為何重要，然後帶您一步步載入 TIFF、啟用 GPU、（可選）選擇特定裝置、執行 OCR，最後讀取提取的文字。完成後，您只需幾行程式碼即可將 TIFF 轉換為文字。

## 快速解答
- **GPU OCR 的主要好處是什麼？** 大型多頁 TIFF 可提升至多 5 倍的處理速度。  
- **需要哪個 Java 版本？** Java 17 或更新版本（Java 8+ 亦可使用）。  
- **需要特殊授權嗎？** 生產環境必須使用有效的 Aspose OCR for Java 授權。  
- **可以在 Linux 上執行嗎？** 可以——Aspose OCR 為跨平台，只需安裝 CUDA 工具包。  
- **GPU 是可選的嗎？** 您可以透過呼叫 `setUseGpu(false)` 回退至 CPU。

## OcrEngine 是什麼？
`OcrEngine` 類別是 Aspose OCR for Java 的核心元件。它封裝了所有 OCR 功能，讓您能載入影像、設定處理選項（如語言與 GPU 使用），並以便利的物件取得辨識文字與信心資料。  
`OcrEngine` 是 Aspose OCR 的核心類別，代表 OCR 處理引擎，提供載入影像、設定選項以及取得結果的方法。

## 如何在 Java 中啟用 GPU 進行 OCR？
載入影像、開啟 GPU，然後呼叫 `recognize`——這就是全部。使用 `setUseGpu(true)` 啟用 GPU 可讓引擎將大量像素運算交給顯示卡，顯著縮短處理時間，尤其是高解析度或多頁 TIFF。

## 您需要的環境
- Java 17 或更新版本（程式碼亦可在 Java 8+ 上執行）。  
- Aspose OCR for Java 23.10（或最新版本）。  
- 具備 CUDA 相容性的 GPU，並已安裝最新驅動程式。  
- 範例多頁 TIFF 檔案（例如 `sample_large.tif`）。  

沒有 Maven？只需將 JAR 放入 classpath 即可。

![如何在 Java 中啟用 GPU 進行 OCR 教學](gpu-ocr.png)

[如何在 Java 中啟用 GPU 教學](gpu-ocr.png)

*圖片說明文字：如何在 Java 中啟用 GPU 進行 OCR*

## 步驟 1：載入 TIFF 影像以進行 OCR
`setImage` 方法會將檔案包裝成 `ImageStream`，讓引擎能處理多頁 TIFF 而無需手動分割。若找不到檔案，會拋出明確的 `FileNotFoundException`。

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **為何重要：** `setImage` 呼叫抽象化了頁面處理，讓您能以單一引擎實例處理整份文件。

## 步驟 2：啟用 GPU 加速
開啟 GPU 只需設定一個布林旗標。大多數系統的預設 GPU 為 device 0，但您可以讓 Aspose 自動選擇最佳裝置。

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **專業提示：** 在擁有多個 GPU 的工作站上，指定裝置 ID 可避免意外回退至較慢的整合式 GPU。

## 步驟 3：設定 GPU 裝置 ID（可選）
如果您知道哪個 GPU 應負責 OCR——例如專用的 AI 卡——可以使用 `setGpuDeviceId` 明確設定。  

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **特殊情況：** 傳入無效的 ID 會觸發 `IllegalArgumentException`。可使用 `ocrEngine.getEngineOptions().getAvailableGpuDevices()` 列出有效的 ID。

## 步驟 4：處理影像並提取文字
執行 OCR 會回傳包含純文字字串與可選信心分數的 `OcrResult`。  

```java
        // Perform OCR – this is where we "convert TIFF to text"
        OcrResult ocrResult = ocrEngine.process();

        // Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

### 預期輸出
如果 TIFF 包含 “Hello, World!”，結果會如下：

```
Recognized text:
Hello, World!
```

引擎會自動處理換行、標點符號與基本版面偵測。若需逐頁提取，可使用 `ocrResult.getPages()`。

## 步驟 5：驗證輸出並處理常見問題
GPU 可能因多種原因被繞過。若已安裝的驅動版本低於最低需求，庫無法初始化 CUDA。顯示記憶體不足會導致引擎回退至 CPU，且某些整合式顯示卡缺乏 OCR 加速所需的運算能力。

### 為何可能未使用 GPU？
- **驅動不匹配：** GPU 驅動必須符合 Aspose 發行說明中列出的最低版本。  
- **記憶體不足：** 超大影像可能超過 VRAM，導致引擎回退至 CPU 並記錄警告。  
- **硬體不支援：** 整合式顯示卡通常缺乏所需的運算能力。

### 如何以程式方式回退至 CPU
若需確保使用 CPU 處理，請以 false 旗標呼叫引擎的選項設定器。這會停用所有 GPU 嘗試，強制 OCR 流程完全在主機處理器上執行，適用於沒有相容顯示卡的機器。

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### 在迴圈中從 TIFF 讀取文字
處理大量檔案時，可在保持 GPU 加速的同時遍歷目錄。

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

此程式碼片段示範如何批次 **從 TIFF 檔案讀取文字**，且不失去效能提升。

## 常見問題 (FAQ)

**Q: 這在 Linux 上能運作嗎？**  
A: 當然可以——只要安裝 CUDA 工具包與驅動，Aspose OCR 可在 Windows、Linux 與 macOS 上執行。

**Q: 如果沒有 GPU 該怎麼辦？**  
A: 省略 `setUseGpu(true)` 呼叫或明確呼叫 `setUseGpu(false)`；引擎將在 CPU 上執行。

**Q: 可以從其他格式提取文字嗎？**  
A: 可以。`setImage` 支援 JPEG、PNG、BMP、PDF 等格式。

**Q: 低解析度 TIFF 的 OCR 準確度如何？**  
A: 解析度低於 300 dpi 時準確度會急劇下降。建議先對影像進行前處理（二值化、去斜）以提升效果。

**Q: Aspose OCR 支援多少種格式？**  
A: 此函式庫支援超過 30 種點陣與文件格式，包括 TIFF、JPEG、PNG、BMP、PDF 與 GIF 等。

## 結論

您現在已了解如何在 Aspose OCR for Java 中使用 GPU 加速 **從 tiff 檔案提取文字**、如何設定特定 GPU 裝置 ID，以及如何有效處理單一或多個 TIFF。只需切換一個旗標，即可在不更改任何 OCR 邏輯的情況下獲得巨大的速度提升。

接下來您可以嘗試：
- 使用平行執行緒批次處理數百個 TIFF。  
- 載入自訂語言套件，以提升對專業詞彙的辨識。  
- 使用正規表達式對提取的文字進行後處理，清理格式。

如果遇到任何問題，請在下方留言。祝開發愉快！

---

**最後更新：** 2026-09-23  
**測試版本：** Aspose OCR for Java 23.10  
**作者：** Aspose

## 相關教學

- [如何一步步啟用 Java OCR 的 GPU](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-step-by-step-guide/)
- [使用 Aspose OCR 完整 Java 指南從影像辨識文字](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)
- [在 Java 中前處理影像 OCR 提升準確度與文字提取](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}