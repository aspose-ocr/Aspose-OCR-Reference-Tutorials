---
category: general
date: 2026-02-14
description: 如何在 Aspose OCR Java 中啟用 GPU，以快速從圖像提取文字。學習將 TIFF 轉換為文字、設定 GPU 設備 ID，並從
  TIFF 檔案讀取文字。
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert tiff to text
- set gpu device id
- read text from tiff
language: zh-hant
og_description: 如何在 Aspose OCR Java 中啟用 GPU，以快速從圖像提取文字。請跟隨本指南將 TIFF 轉換為文字、設定 GPU 裝置
  ID，並從 TIFF 讀取文字。
og_title: 如何啟用 GPU 以進行 OCR – 從 TIFF 提取文字
tags:
- OCR
- Java
- GPU acceleration
title: 如何啟用 GPU 進行 OCR 並從 TIFF 中提取文字
url: /zh-hant/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何啟用 GPU 進行 OCR 並從 TIFF 中提取文字

有沒有想過在對大型 TIFF 檔案執行 OCR 時 **如何啟用 GPU**？你並非唯一這樣想的人——開發人員不斷追求額外的速度提升，特別是當來源影像是多兆位元組的 TIFF 時。好消息是？使用 Aspose OCR for Java，你只需切換一個開關、指向正確的 GPU，即可看到引擎在影像上飛奔。

在本教學中，我們將逐步說明完整工作流程：載入 TIFF、啟用 GPU 加速、（可選）指定特定 GPU 裝置、執行 OCR，最後 **從影像中提取文字**。完成後，你將能在幾行程式碼內 **將 TIFF 轉換為文字**，同時也會看到如何在任何支援平台上 **從 TIFF 讀取文字**。

## 您需要的環境

- Java 17 或更新版本（程式碼同樣支援 Java 8+）
- Aspose OCR for Java 23.10（或撰寫時的最新版本）
- 支援 CUDA 的 GPU，並已安裝最新驅動程式
- 一個多頁 TIFF 範例（我們稱之為 `sample_large.tif`）

沒有 Maven 魔法？沒問題——只要把 JAR 放入 classpath 即可使用。

![在 Java 中啟用 GPU 進行 OCR 的教學](gpu-ocr.png)

*Image alt text: 在 Java 中啟用 GPU 進行 OCR 的教學*

## 步驟 1：載入 TIFF 影像以進行 OCR

首先，你需要一個 `OcrEngine` 實例以及來源影像。Aspose OCR 幾乎可以讀取任何點陣圖格式，但 TIFF 是掃描文件的常見選擇。

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **為何這很重要：** `setImage` 會將檔案包裝成 `ImageStream`，讓引擎能直接處理多頁 TIFF，無需手動切割。如果找不到檔案，會拋出清晰的 `FileNotFoundException`——請務必再次確認路徑。

## 步驟 2：啟用 GPU 加速

現在魔法發生了。開啟 GPU 只是一個布林旗標，但它能為處理時間削減數秒，甚至數分鐘。

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **專業提示：** 若你的機器有多張 GPU，預設通常是第一張（device 0）。你可以讓 Aspose 自動挑選最佳裝置，但手動指定可避免在多 GPU 工作站上出現意外。

## 步驟 3：設定 GPU 裝置 ID（可選）

有時你清楚知道要使用哪張 GPU——例如第二張卡專門負責 AI 工作負載。這時 `setGpuDeviceId` 就派上用場。

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **邊緣情況：** 若傳入無效的 ID，引擎會拋出 `IllegalArgumentException`。快速執行 `System.out.println(ocrEngine.getEngineOptions().getAvailableGpuDevices())` 即可列出可用的 ID。

## 步驟 4：處理影像並 **從影像中提取文字**

引擎配置完成後，就可以執行 OCR。結果物件會返回原始字串，若需要還能取得信心分數。

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

如果 TIFF 包含文字 “Hello, World!” ，你應該會看到類似以下的結果：

```
Recognized text:
Hello, World!
```

引擎會自動處理換行、標點符號，甚至基本的版面偵測。若需更細緻的控制（例如逐頁提取文字），可探索 `ocrResult.getPages()`。

## 步驟 5：驗證輸出並處理常見問題

### 為何 GPU 可能未被使用？

- **驅動程式不匹配：** GPU 驅動程式必須至少符合 Aspose 推薦的版本（請參閱發行說明）。
- **記憶體不足：** 超大影像可能超出 GPU VRAM。此時引擎會優雅地回退至 CPU，並在主控台顯示警告。
- **硬體不支援：** 整合式顯示卡通常缺乏所需的計算能力。

### 如何以程式方式回退至 CPU

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### 在迴圈中從 TIFF 讀取文字

如果你有一個資料夾裡放滿了 TIFF，可以這樣遍歷：

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

上述程式碼示範了如何 **批次從 TIFF 讀取文字**，同時仍能受惠於 GPU 加速。

## 常見問題 (FAQ)

**Q: 這在 Linux 上能運作嗎？**  
A: 當然可以——Aspose OCR 是跨平台的。只要確保已安裝 CUDA 工具包與驅動程式即可。

**Q: 若我沒有 GPU 該怎麼辦？**  
A: 設定 `setUseGpu(false)` 或直接省略該呼叫。引擎預設會使用 CPU。

**Q: 我可以從其他格式提取文字嗎？**  
A: 可以，`setImage` 方法同樣支援 JPEG、PNG、BMP，甚至 PDF 串流。

**Q: 低解析度的 TIFF OCR 準確度如何？**  
A: 當解析度低於 300 dpi 時，準確度會下降。建議在送入引擎前先進行前處理（二值化、去斜）以提升效果。

## 結論

現在你已了解 **如何啟用 GPU** 於 Aspose OCR Java、如何 **設定 GPU 裝置 ID**，以及最重要的 **如何從影像中提取文字**，特別是 **將 TIFF 轉換為文字** 與 **從 TIFF 讀取文字** 的高效方法。只要切換一個旗標，並視需要指定裝置，即可在不改寫 OCR 邏輯的前提下獲得巨大的效能提升。

準備好進一步嘗試了嗎？可以試著實驗以下方向：

- **批次處理** 數百個 TIFF，使用平行執行緒。
- **自訂語言套件** 以提升對特定文件的辨識率。
- **後處理**：使用正規表達式清理抽取出的字串格式。

如有任何問題，歡迎留言討論，祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}