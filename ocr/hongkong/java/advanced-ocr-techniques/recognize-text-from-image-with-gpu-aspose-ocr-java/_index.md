---
category: general
date: 2026-04-26
description: 學習如何在 Java 中使用 Aspose OCR 透過 GPU 加速來辨識影像文字，內容包括設定 GPU 記憶體上限以及載入影像進行 OCR
  的步驟。
draft: false
keywords:
- recognize text from image
- set gpu memory limit
- load image for ocr
- Aspose OCR Java
- GPU acceleration OCR
language: zh-hant
og_description: 探索如何使用 GPU 加速的 Aspose OCR 在 Java 中快速辨識圖像文字。逐步指南，設定 GPU 記憶體上限並載入圖像進行
  OCR。
og_title: 使用 GPU Aspose OCR（Java）辨識圖像文字
tags:
- OCR
- Java
- GPU
- Aspose
title: 使用 GPU 與 Aspose OCR（Java）進行圖像文字辨識
url: /zh-hant/java/advanced-ocr-techniques/recognize-text-from-image-with-gpu-aspose-ocr-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 GPU Aspose OCR（Java）辨識影像文字

是否曾經需要在 Java 後端快速 **辨識影像文字**？使用 Aspose OCR 的 GPU 加速，你可以在每次掃描上節省數秒——不必再等 CPU 處理大量像素。在本教學中，我們將逐步說明如何開啟 GPU、可選地 **設定 GPU 記憶體上限**，以及最後 **載入影像進行 OCR**，只需幾行程式碼即可取得乾淨的文字字串。

我們將涵蓋在支援 CUDA 的顯示卡上執行示範所需的一切，說明每個設定的原因，並提供完整、可直接執行的範例。完成後，你就能將 GPU 加速的 OCR 嵌入任何 Java 服務，無論是文件匯入管線或即時行動後端。

## 需要的條件

- **Java 17** 或更新版本（Aspose OCR JAR 針對現代 JVM）  
- 具備 **CUDA 相容 GPU**，且至少 2 GB VRAM（示範限制使用 1024 MB）  
- **Aspose.OCR for Java** 函式庫（可從 Aspose 官方網站下載或從 Maven 取得）  
- 想要處理的影像檔案——最好是高解析度的掃描或相片  

不需要外部服務、雲端金鑰，只要本機安裝即可。即使尚未擁有 GPU，也能執行程式碼；`setUseGpu(true)` 會自動回退至 CPU。

## 第一步：將 Aspose OCR 加入專案並辨識影像文字

首先，確保 Aspose OCR JAR 已加入 classpath。若使用 Maven，請加入以下內容：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

函式庫可用後，建立 `OcrEngine` 實例。此物件是 **辨識影像文字** 操作的入口點。

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

為什麼要先實例化 `OcrEngine`？它保存所有辨識設定（GPU 旗標、語言套件等），並將每次掃描相互隔離，讓你可以安全地在多張影像間重複使用同一引擎而不會發生記憶體洩漏。

## 第二步：啟用 GPU 加速並可選地 **設定 GPU 記憶體上限**

GPU 加速是讓大規模 OCR 成為可能的關鍵技術。Aspose 只需一個呼叫即可切換它：

```java
// Step 2: Turn on GPU acceleration (requires a CUDA‑enabled GPU)
ocrEngine.getRecognitionSettings().setUseGpu(true);
```

如果你的 GPU 與其他工作共用，可能需要限制引擎可佔用的 VRAM。這時就會用到 **設定 GPU 記憶體上限**：

```java
// Optional: Limit the amount of GPU memory the engine may use (in MB)
ocrEngine.getRecognitionSettings().setGpuMemoryLimit(1024);
```

設定記憶體上限可防止在平行處理大量高解析度影像時發生記憶體不足的錯誤。數值單位為 MB，`1024` 代表「最多使用 1 GB VRAM」。

> **小技巧：** 在 4 GB 顯示卡上，2 GB 的上限通常是安全且平衡的選擇；若發現 GPU 閒置，可嘗試調高數值。

## 第三步：**載入影像進行 OCR** – 指定引擎要處理的檔案

引擎已就緒後，需要告訴它要掃描哪張圖片。Aspose 支援檔案路徑、`java.io.File`，甚至 `java.awt.image.BufferedImage`。為簡化說明，我們使用路徑方式：

```java
// Step 3: Load the high‑resolution image to be processed
ocrEngine.setImage("YOUR_DIRECTORY/high_res_photo.jpg");
```

將 `YOUR_DIRECTORY/high_res_photo.jpg` 替換為實際測試影像的路徑。若影像位於 resources 資料夾，可改用 `getClass().getResource("/images/sample.png").getPath()`。

為什麼載入很重要？引擎會先執行前處理步驟（去斜、二值化），此步驟高度依賴 GPU。提供乾淨且高解析度的檔案可讓 GPU 高效運作，提升 **辨識影像文字** 的準確度。

## 第四步：執行辨識並取得擷取的字串

GPU 已開啟且影像已載入後，最後的呼叫相當簡單：

```java
// Step 4: Run the recognition and retrieve the extracted text
String extractedText = ocrEngine.recognize().getText();
```

`recognize()` 方法會阻塞，直到 GPU 完成，之後 `getText()` 會回傳純文字 `String`。在底層，Aspose 使用在 CUDA 核心上執行的深度學習模型，因此延遲通常只有純 CPU OCR 的一小部分。

## 第五步：輸出結果

讓我們將 OCR 輸出印到主控台，以便驗證是否成功：

```java
// Step 5: Output the GPU‑accelerated OCR result
System.out.println("GPU‑accelerated result:\n" + extractedText);
```

若所有設定正確，你會立即看到轉錄的文字。以一般的 RTX 2060 為例，3000 × 2000 px 的影像可在一秒內完成處理。

![使用 GPU Aspose OCR 辨識影像文字](/images/gpu-ocr-demo.png "GPU 加速 OCR 示範")

*圖片說明文字:* **辨識影像文字** – GPU OCR 後的主控台輸出截圖。

## 預期輸出

對範例收據執行完整程式會得到類似以下的結果：

```
GPU‑accelerated result:
Item      Qty   Price
Apple      2    $1.20
Banana     5    $0.75
Total          $3.75
```

實際文字會因來源影像而異，但上述格式說明引擎能正確擷取換行與數字。

## 常見問題與實用技巧

| Issue | Why it happens | How to fix it |
|-------|----------------|---------------|
| **未偵測到 GPU** | CUDA 驅動程式缺失或 JAR 版本不相容 | 安裝最新的 NVIDIA 驅動程式，確認 `nvidia-smi` 正常運作，並使用 Aspose OCR 23.12 或更新版本 |
| **記憶體不足錯誤** | 影像過大，超過設定的 VRAM 上限 | 提升 `setGpuMemoryLimit` 設定或在載入前縮小影像尺寸 |
| **雜訊字元** | 影像模糊或對比度低 | 使用 `ocrEngine.getPreprocessingSettings().setBinarization(true)` 進行前處理 |
| **首次執行速度緩慢** | GPU 上下文初始化的開銷 | 在正式工作負載前先處理一張小的測試影像以暖機引擎 |

請記住，**設定 GPU 記憶體上限** 為可選項，但

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}