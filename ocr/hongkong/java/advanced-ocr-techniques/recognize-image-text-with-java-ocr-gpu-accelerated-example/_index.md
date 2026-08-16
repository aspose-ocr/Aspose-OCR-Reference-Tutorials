---
category: general
date: 2026-03-28
description: 學習如何在 Java 中使用 Aspose OCR 識別圖像文字、提取文字 PNG 檔案，並利用 GPU 加速快速執行大型圖像的 OCR。
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: zh-hant
og_description: 了解如何在 Java 中辨識影像文字、提取文字 PNG 檔案，並使用 GPU 加速大型影像的 OCR。
og_title: 使用 Java OCR 辨識圖像文字 – GPU 加速範例
tags:
- OCR
- Java
- GPU
title: 使用 Java OCR 識別圖像文字 – GPU 加速範例
url: /zh-hant/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java OCR 識別圖像文字 – GPU 加速範例

是否曾經需要從巨大的 PNG 中 **recognize image text**，但發現 CPU 版執行緩慢？你並非唯一遇到這種情況的人。在許多實務流程中——例如發票掃描或歷史文件的保存——圖像尺寸可能會非常龐大，而預設的 OCR 引擎根本跟不上。  

好消息：Aspose OCR for Java 讓你 **use GPU acceleration**，為流程加速，且程式碼相當精簡。在本教學中，你將看到一個完整、可執行的 Java OCR 範例，能 **extracts text PNG** 檔案、利用支援 CUDA 的 GPU，並以僅幾行程式碼處理 **OCR large image**。完成後，你將清楚知道如何將其整合到自己的 Java 專案，以及每個設定的意義。

## 你將學到什麼

- 如何在 Maven 或 Gradle 專案中設定 Aspose OCR。  
- 在 GPU 上 **recognize image text** 的逐步流程。  
- 為何設定 GPU 串流數量可以提升吞吐量。  
- 如何驗證輸出並排除常見問題。  

> **Prerequisites** – Java 17（或更新版本）、具備最新驅動程式的 CUDA 相容 GPU，以及有效的 Aspose OCR for Java 授權（免費試用可用於評估）。不需要其他外部函式庫。

---

## 步驟 1：加入 Aspose OCR 相依性

首先，將 Aspose OCR 函式庫加入你的建置中。如果使用 **Maven**，請在 `pom.xml` 中加入以下片段：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

對於 **Gradle**，請將以下內容放入 `build.gradle`：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** 最新版本（截至 2026 年 3 月）已加入 GPU 工作負載的效能提升，請務必使用最新發行版。

---

## 步驟 2：初始化 OCR 引擎並啟用 GPU

建立 OCR 引擎相當簡單。關鍵在於開啟 GPU 旗標——否則引擎會退回至 CPU 模式。

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### 為何啟用 GPU？

當你啟用 `setUseGpu(true)` 時，Aspose 會將繁重的卷積神經網路計算卸載至顯示卡。這可在處理 **ocr large image** 時節省數秒，特別是當圖像超過 4000 × 4000 px 時。如果你的環境沒有相容的 GPU，該呼叫只會變成無操作，引擎會繼續在 CPU 上執行——不會當機，只是效能較慢。

---

## 步驟 3：辨識 PNG 圖像並擷取文字

現在將引擎指向你想處理的檔案。範例使用 `sample-large.png`，但你可以換成任何 PNG 或 JPEG。

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

執行程式後，你應該會看到類似以下的輸出：

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

該輸出證實 **recognize image text** 操作成功，且你已成功 **extract text png** 內容。

---

## 步驟 4：驗證 GPU 使用率（可選但有幫助）

如果你想確認 GPU 是否真的被使用，請打開系統的 GPU 監控工具（例如 Linux 上的 `nvidia-smi`）。當 Java 程序執行時，你應該會看到記憶體使用量與計算利用率有適度的上升。

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

若未看到任何活動，請再次確認以下項目：

1. CUDA 驅動程式與 GPU 型號相符。  
2. `setUseGpu(true)` 呼叫未在程式碼後續被覆寫。  
3. 你的授權檔案（若有）未限制 GPU 使用。

---

## 步驟 5：處理常見邊緣情況

### 超出 GPU 記憶體的巨型圖像

當圖像非常龐大（例如 8000 × 8000 px）時，GPU 可能會記憶體不足。快速的解決方法是先將圖像縮小再送入 Aspose：

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

然後將 `"sample-resized.png"` 傳給 `recognizeImage`。這樣可在保持 OCR 準確度的同時，符合 GPU 記憶體限制。

### 多頁 PDF

Aspose OCR 也能逐頁處理 PDF。對每一頁迴圈，將其轉為圖像，再送入引擎。相同的 **use gpu acceleration** 旗標仍適用，為你提供快速的 PDF 轉文字管線。

---

## 完整可執行範例（直接複製貼上）

以下是完整的 Java 類別，可直接編譯執行。將 `YOUR_DIRECTORY` 替換為你的 PNG 檔案路徑。

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Expected output** – 以純文字形式呈現引擎從圖像中讀取的所有內容。若圖像包含表格，會以換行方式串接儲存格內容；Aspose 不會保留版面配置，但你可以自行後處理字串。

---

## 常見問題

| Question | Answer |
|----------|--------|
| **我需要付費授權嗎？** | 試用版支援最多 200 頁，且會移除 OCR 的浮水印。正式環境下，授權可解除限制並解鎖完整的 GPU 功能。 |
| **如果我的 GPU 較舊（例如 GTX 750）怎麼辦？** | 較舊的 GPU 仍可能運作，但速度會較慢；請確保至少具備 Compute Capability 3.0。 |
| **我可以處理 JPG 或 BMP 檔案嗎？** | 當然可以——`recognizeImage` 接受 Java ImageIO 支援的任何格式。 |
| **有沒有辦法批次處理大量圖像？** | 將 OCR 呼叫包在迴圈中，並考慮增加 `setGpuStreams` 以符合你想要的同時串流數量。 |
| **如果我需要保留版面配置怎麼辦？** | 使用 Aspose OCR 的 `LayoutOptions` 取得邊界框；此功能超出本快速指南範圍，但已在 API 中說明。 |

---

## 結論

現在你已擁有一個簡潔、端到端的 **java ocr example**，能 **recognize image text**、**extract text png**，並 **use GPU acceleration** 加速 **ocr large image** 的處理。透過調整 GPU 串流數量，必要時縮小過大的圖像，即可將此解決方案套用於幾乎任何硬體配置。  

準備好進一步嗎？試著將一個資料夾的掃描收據餵入相同管線，或使用 Aspose 的 `TextRegion` API 來保留原始版面。若遇到任何問題，Aspose 論壇與 Javadoc 都是絕佳資源——只要記得本篇所述的基礎即可。  

祝程式開發順利，願你的 OCR 如閃電般快速！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}