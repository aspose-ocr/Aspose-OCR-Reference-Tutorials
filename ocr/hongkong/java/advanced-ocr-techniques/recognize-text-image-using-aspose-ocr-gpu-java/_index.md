---
category: general
date: 2026-10-30
description: 了解如何在 Java 中利用 Aspose OCR GPU 支援快速從圖像提取文字。本指南說明如何設定 GPU device ID 以實現高效能
  OCR。
draft: false
keywords:
- extract text from image
- how to extract text
- aspose ocr gpu
- recognize text image java
- gpu acceleration OCR
lastmod: 2026-10-30
og_description: 了解如何在 Java 中利用 Aspose OCR GPU 支援快速從圖像提取文字。本指南說明如何設定 GPU device ID
  以獲得最佳效能。
og_image_alt: 'Developer guide: extract text from image using Aspose OCR GPU in Java'
og_title: 如何在 Java 中使用 Aspose OCR GPU 從圖像提取文字
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to extract text from image quickly with Aspose OCR GPU support
    in Java. This guide shows how to set GPU device ID and achieve high‑performance
    OCR.
  headline: How to extract text from image with Aspose OCR GPU in Java
  type: TechArticle
- questions:
  - answer: Yes—just install a valid Aspose OCR license. The free trial is for evaluation
      only.
    question: Can I use this in a commercial application?
  - answer: Absolutely; as long as the NVIDIA driver and CUDA toolkit are installed,
      the library runs on headless Linux environments.
    question: Does the GPU version work on Linux servers?
  - answer: Aspose OCR can process images up to **5000 × 5000 px** without loading
      the whole file into memory.
    question: What is the maximum image size supported?
  - answer: Replace the old JAR with the new one and update your Maven/Gradle dependency
      version number.
    question: How do I upgrade to the latest Aspose OCR version?
  - answer: Yes—`OcrResult` provides layout information, including word‑level bounding
      boxes, when you enable the `setIncludeLayout(true)` option.
    question: Is there a way to get bounding‑box coordinates for each word?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: 如何在 Java 中使用 Aspose OCR GPU 從圖像提取文字
url: /zh-hant/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR GPU 在 Java 中從圖像提取文字

如果您曾在 Java 應用程式中嘗試 **extract text from image**，卻發現 CPU 在高解析度掃描時吃緊，您並不孤單。許多開發者在處理大型文件時都會遇到效能瓶頸。Aspose OCR for Java 透過讓您在 GPU 上執行 OCR，徹底解決這個問題，顯著縮短處理時間。在本教學中，您將看到一個完整、可直接執行的範例，說明如何設定授權、啟用 GPU 加速，並在多張顯示卡存在時 **set gpu device id**。

## 快速回答
- **What is the fastest way to extract text from image in Java?** 使用帶 GPU 加速的 Aspose OCR，並設定適當的 GPU 裝置 ID。  
- **Which Java version is required?** 建議使用 Java 17 或更新版本，以獲得最佳效能。  
- **Do I need a license for GPU support?** 是的——GPU 功能僅在擁有有效的 Aspose OCR 授權時解鎖。  
- **Can I run this on a headless server?** 完全可以；只需安裝 GPU 驅動程式與 CUDA 工具組。  
- **How many languages are supported?** 超過 30 種語言，包括英文、中文、阿拉伯文與印地語。

## 什麼是從圖像提取文字？
從圖像提取文字指的是將 PNG、JPG 或 TIFF 等位圖格式中儲存的字符視覺表示，轉換為可編輯、可搜尋的 Unicode 文字。此過程稱為光學字符辨識（OCR），可支援後續的索引、翻譯與資料抽取等工作。

## 為什麼使用 Aspose OCR GPU？
Aspose OCR 利用 GPU 加速，能比僅使用 CPU 更有效率地處理大型、高解析度圖像。它支援超過 30 種輸入格式，且可處理最高 5000 × 5000 px 的圖像，同時保持低記憶體使用量，在現代 NVIDIA GPU 上提供最高五倍的辨識速度提升。

## 您需要的項目
- **Java 17** 或更新版本（相容於 Java 8+，但 LTS 版提供更佳的 JIT 效能）。  
- **Aspose OCR for Java** 函式庫（從 Aspose 官方網站下載 JAR）。  
- 有效的 **Aspose OCR license file**（`Aspose.OCR.lic`）。免費試用可用，但 GPU 功能需授權版。  
- 包含清晰、機器可讀文字的圖像檔（`sample-image.png`）。  
- 支援 CUDA 的 NVIDIA GPU（或等效硬體）並安裝相應驅動程式。

如果上述項目您不熟悉，別擔心，我們會逐一說明。

## 步驟 1：將 Aspose OCR 加入您的專案
首先，將 Aspose OCR JAR 加入 classpath。若使用 Maven，請在 `pom.xml` 中加入以下相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Gradle 使用方式如下：

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

若偏好手動方式，請將 JAR 放入 `libs/` 資料夾，並在 IDE 中加入模組路徑。

> **Pro tip:** 保持版本號與發行說明同步；較新版本通常包含 GPU 處理的效能改進。

## 步驟 2：載入 Aspose OCR 授權（GPU 使用所需）
若未載入授權，`setEnableGpu(true)` 會靜默回退至 CPU 模式。請在 `main` 方法一開始載入授權：

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

將 `YOUR_DIRECTORY` 替換為存放 `.lic` 檔案的絕對或相對路徑。路徑錯誤會拋出 `FileNotFoundException`，請務必確認拼寫正確。

## 步驟 3：建立 OCR 引擎並啟用 GPU 加速
`OcrEngine` 類別是執行圖像 OCR 的核心元件。

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

為什麼需要設定裝置 ID？在多 GPU 環境下，您可以將一張卡片專用於前置處理，另一張卡片專用於 OCR。設定 ID 可確保繁重工作在指定硬體上執行。

## 步驟 4：準備輸入圖像
`OcrInput` 類別代表您要處理的圖像集合。

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

若需處理串流（例如上傳的檔案），請改用 `ocrInput.add(InputStream)`。

## 步驟 5：執行辨識程序並取得結果
`OcrResult` 類別封裝了純文字、信心分數以及可選的版面資訊。

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

執行結果會在主控台顯示類似以下內容：

```
Recognized text:
Hello, world!
This is a sample image.
```

若圖像模糊或語言不支援，結果可能為空。此時可檢查 `ocrResult.getConfidence()`（0‑100）以決定是否需先前處理再重試。

## 完整、可執行範例
將所有程式碼組合起來，即可得到一個可直接貼到 IDE 的單一 Java 類別：

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **Expected output:** 主控台會印出 `sample-image.png` 中的完整文字。啟用 GPU 後，典型的 300 dpi 掃描處理時間通常會從數秒（CPU）縮短至不到一秒。

## 常見問題與邊緣案例

### 這在無頭伺服器上可行嗎？
可以。只要安裝 GPU 驅動程式，即可在不需要顯示器的環境下執行。確保 `CUDA` 工具組（或相容 GPU 的等效套件）已加入系統 `PATH`，即可在雲端或容器化環境中運行 OCR。

### 如果我有多於一張 GPU 且想使用 GPU 1，該怎麼做？
將裝置 ID 如下修改：

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

將 ID 設為 `1` 後，OCR 引擎會使用系統中的第二張 GPU，這在第一張 GPU 已被其他工作佔用時特別有用。

### 如何在不同語言中提取圖像文字？
在呼叫 `recognize` 前設定語言：

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose OCR 支援 **超過 30 種語言**，包括阿拉伯文與希伯來文等從右至左的腳本。正確選擇語言可大幅提升辨識準確度。

### 如果圖像包含多頁（例如 PDF 轉為圖像），該怎麼辦？
為每一頁建立獨立的 `OcrInput` 條目，或在檔案上迴圈：

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

引擎會依序串接結果，保留頁面順序於最終輸出。

### 如何處理低信心結果？
檢查信心分數：

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

常見的前置處理步驟包括二值化、降噪或調整至 300 dpi。經過這些處理後重新執行 OCR，通常能提升信心分數。

## 效能提示
- **批次處理：** 將多張圖像一次加入同一個 `OcrInput`，可減少重複初始化 GPU 上下文的開銷。  
- **暖機：** JVM 啟動後先執行一次空白辨識，以降低首次呼叫的驅動程式初始化延遲。  
- **記憶體管理：** 完成後呼叫 `ocrInput.clear()` 釋放大型 `OcrInput` 物件，以釋放 GPU 記憶體。  

## 結論
您現在已掌握如何在 Java 中使用 Aspose OCR 的 GPU 引擎高效 **extract text from image**，以及在多張顯示卡環境下 **set gpu device id** 的方法，並了解多語言情境的處理方式。上述完整、可執行的程式碼可直接使用——只需替換成您的授權與圖像路徑。

準備好進一步操作了嗎？試著處理整個資料夾的掃描 PDF，實驗不同的 `setLanguage` 選項，或將 OCR 輸出結合機器學習模型進行後處理。GPU 加速帶來的效能提升，使大規模專案變得可行。

祝開發順利，若遇到任何問題，歡迎留言討論！

## 常見問答

**Q: Can I use this in a commercial application?**  
A: Yes—just install a valid Aspose OCR license. The free trial is for evaluation only.

**Q: Does the GPU version work on Linux servers?**  
A: Absolutely; as long as the NVIDIA driver and CUDA toolkit are installed, the library runs on headless Linux environments.

**Q: What is the maximum image size supported?**  
A: Aspose OCR can process images up to **5000 × 5000 px** without loading the whole file into memory.

**Q: How do I upgrade to the latest Aspose OCR version?**  
A: Replace the old JAR with the new one and update your Maven/Gradle dependency version number.

**Q: Is there a way to get bounding‑box coordinates for each word?**  
A: Yes—`OcrResult` provides layout information, including word‑level bounding boxes, when you enable the `setIncludeLayout(true)` option.

---

**最後更新：** 2026-10-30  
**測試環境：** Aspose OCR for Java 24.11  
**作者：** Aspose

## 相關教學

- [Recognize Text From Image Java Ocr With Gpu Acceleration](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [How To Enable Gpu For Ocr In Java Extract Text From Image](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)
- [Extract Text From Image With Aspose Ocr Java Quick Guide](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}