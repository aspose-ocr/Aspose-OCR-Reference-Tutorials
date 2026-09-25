---
category: general
date: 2026-01-07
description: 如何啟用 GPU 進行 OCR 並快速從圖像提取文字。學習從 PNG 識別文字、從相片讀取文字，以及使用 Aspose OCR 將圖像轉換為文字。
draft: false
keywords:
- how to enable gpu
- extract text from image
- recognize text from png
- read text from photo
- convert image to text
language: zh-hant
og_description: 如何在 Java 中啟用 GPU 進行 OCR。本指南將向您展示如何從圖像中提取文字、識別 PNG 圖片中的文字，以及使用 Aspose
  OCR 將圖像轉換為文字。
og_title: 如何啟用 GPU 進行 OCR – 快速文字提取
tags:
- OCR
- Java
- GPU-Acceleration
title: 如何啟用 GPU 以進行 OCR – 快速從圖像提取文字
url: /zh-hant/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-fast-extraction-of-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何啟用 GPU 進行 OCR – 快速從圖像提取文字

有沒有想過 **how to enable GPU** 用於 OCR 並從照片即時取得結果？你並不孤單。在許多電腦視覺專案中，瓶頸往往是 OCR 步驟，尤其是處理高解析度 PNG 檔案時。好消息是 Aspose OCR 只需一行程式碼即可開啟 GPU 加速，能大幅縮短處理時間。

在本教學中，你將學會使用 Aspose OCR 函式庫 **extract text from image** 檔案、**recognize text from PNG** 資源、**read text from photo** 輸入，最終 **convert image to text**。我們會逐步說明每個必要步驟，解釋每項設定的原因，並提供一個完整、可直接執行的 Java 範例，讓你今天就能放入專案中使用。

> **你將獲得的成果：** 一個可運作的 Java 程式，載入 PNG 圖片、啟用 GPU 加速、執行 OCR，並將偵測到的字串印到主控台。

## 前置條件

| 需求 | 為何重要 |
|------|----------|
| Java 17 或更新版本 | Aspose OCR 至少需要 Java 8，但 Java 17 提供長期支援與更佳效能。 |
| Maven 或 Gradle 建置工具 | 自動取得 `aspose-ocr` 相依性。 |
| 相容 CUDA 的 GPU（可選） | `setUseGpu(true)` 呼叫在沒有 GPU 的系統上會被忽略，但若有 GPU 可提升速度。 |
| 已知資料夾中的影像檔案（`sample-photo.png`） | 這是我們將提供給 OCR 引擎的來源。 |

如果缺少上述任一項，你仍可依照程式碼執行——只需跳過 GPU 步驟，函式庫會自動回退至 CPU 處理。

## 專案設定

### 1️⃣ 將 Aspose OCR 加入你的建置

對於 Maven，將以下程式碼片段加入你的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest stable version -->
</dependency>
```

對於 Gradle，將以下內容放入 `build.gradle`：

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

> **小技巧：** 持續關注 Aspose Maven 套件庫，他們會定期發布效能修補。

### 2️⃣ 目錄結構

在專案根目錄建立名為 `resources` 的資料夾，並將 `sample-photo.png` 放入其中。程式碼會使用相對路徑引用它，無需硬編碼絕對位置。

## 步驟實作

以下我們將流程分解為多個邏輯區塊。每個區塊都有自己的 H2 標題，這不僅有助於 SEO，也讓 AI 模型能清晰了解教學結構。

### 步驟 1：初始化 OCR 引擎 – **how to enable GPU**

首先，你需要建立 `OcrEngine` 的實例。此物件保存所有設定，包括關鍵的 GPU 旗標。

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **為何重要：** 沒有 `OcrEngine`，就無法取得影像或硬體選項的上下文。提前實例化也能在載入檔案前調整設定。

### 步驟 2：載入要處理的影像 – **extract text from image**

接著，將引擎指向你想分析的 PNG 檔案。`ImageStream.fromFile` 輔助方法可讀取任何支援的格式，但我們會專注於 PNG，因為它保留無損細節。

```java
        // Step 2: Load the image to be recognized
        ocrEngine.setImage(ImageStream.fromFile("resources/sample-photo.png"));
```

> **邊緣情況：** 若影像位於其他資料夾，請相應調整路徑。處理大量批次時，可遍歷目錄並對每個檔案呼叫 `setImage`。

### 步驟 3：開啟 GPU 加速 – **how to enable GPU**

現在重頭戲登場。將 `useGpu` 設為 `true`，底層原生函式庫會嘗試將繁重工作交給顯示卡。如果未偵測到相容的 GPU，Aspose 會靜默回退至 CPU，程式碼不會崩潰。

```java
        // Step 3: Enable GPU acceleration (optional – ignored if no GPU is available)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **如果我沒有 GPU 呢？** 不會發生錯誤；此呼叫會被忽略，OCR 會在 CPU 上執行。之後可使用 `ocrEngine.getEngineOptions().isUseGpu()` 檢查實際模式。

### 步驟 4：執行 OCR – **recognize text from PNG**

設定完成後，呼叫 `recognize()`。此方法會回傳 `OcrResult` 物件，內含原始文字、信心分數，若需要亦可取得邊界框。

```java
        // Step 4: Perform the OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();
```

> **為何要等到現在才執行？** OCR 過程計算量大；在所有設定完成後執行，可確保最高效能，尤其在 GPU 啟用時。

### 步驟 5：輸出偵測到的字串 – **read text from photo**

最後，印出結果。在實際應用中，你可能會將字串寫入資料庫或傳送至網路，但 `System.out.println` 讓範例保持簡潔。

```java
        // Step 5: Output the recognized text
        System.out.println("Detected text:");
        System.out.println(ocrResult.getText());

        // Optional: Verify GPU usage
        System.out.println("GPU used: " + ocrEngine.getEngineOptions().isUseGpu());
    }
}
```

> **預期輸出：** 若 `sample-photo.png` 包含文字 “Hello World”，主控台將顯示：

```
Detected text:
Hello World
GPU used: true
```

這就是完整程式——不需外部服務，也沒有隱藏的設定檔。

## 視覺概覽

![如何啟用 GPU 進行 OCR](gpu-ocr-diagram.png "圖示說明從載入影像到 GPU 加速 OCR 的流程")

*此圖示說明管線的每個步驟，強調 **how to enable GPU** 旗標所在位置。*

## 常見問題與邊緣情況

| 問題 | 回答 |
|------|------|
| **我可以一次處理多張影像嗎？** | 可以。將步驟 2‑5 包在 `for (File img : folder.listFiles())` 迴圈中。記得對每個檔案呼叫 `ocrEngine.setImage`。 |
| **支援哪些影像格式？** | JPEG、PNG、BMP、TIFF 與 GIF 均為 Aspose OCR 原生支援的格式。 |
| **如何處理低品質掃描？** | 在辨識前調整 `ocrEngine.getEngineOptions().setPreprocessMode(PreprocessMode.Auto)`，讓引擎清除雜訊。 |
| **有辦法取得信心分數嗎？** | `ocrResult.getMeanConfidence()` 會回傳平均信心分數（0‑100）。個別字元的信心可透過 `ocrResult.getTextLines()` 取得。 |
| **在 macOS 使用 Metal GPU 時會有效嗎？** | Aspose OCR 目前僅在 NVIDIA GPU 上使用 CUDA。於 macOS 上若非使用 NVIDIA eGPU，將回退至 CPU。 |

## 效能提示

1. **批次處理：** 先將所有影像載入記憶體，然後一次啟用 GPU 並執行迴圈。可減少驅動程式開銷。  
2. **影像縮放：** 將非常大的 PNG 縮小至長邊最多 2000 px；OCR 準確度仍保持高水平，同時降低 GPU 記憶體使用。  
3. **預熱呼叫：** 在正式工作負載前，於小圖像上執行一次虛擬的 `recognize()`，讓 GPU 驅動程式初始化——可在第一張正式影像上省下數毫秒。  

## 重點回顧與後續步驟

我們已說明了 Aspose OCR 的 **how to enable GPU**，示範了 **extract text from image** 檔案、**recognize text from PNG**，以及 **read text from photo** 與 **convert image to text** 工作流程。上方完整的 Java 程式碼可直接複製貼上，效能說明則能協助你將硬體效能發揮到極致。

接下來可以考慮擴充此解決方案：

* **將 OCR 結果匯出為 JSON**，供後續分析使用。  
* **結合 Spring Boot REST 端點**，讓其他服務提交照片並取得純文字回應。  
* **使用語言特定字典**，透過 `ocrEngine.getEngineOptions().setLanguage(Language.English)` 提升多語言文件的準確度。  

歡迎自行實驗——將 PNG 換成掃描的 PDF、啟用 `setPreserveFormatting(true)`，或對噪點較多的影像串接多次 OCR。只要掌握了 **how to enable GPU**，就能無限發揮。

### 祝開發順利！

如果遇到任何問題或發現巧妙的調整，歡迎在下方留言。記得：少量的 GPU 能力即可將緩慢的 OCR 任務變成閃電般的文字提取管線。 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}