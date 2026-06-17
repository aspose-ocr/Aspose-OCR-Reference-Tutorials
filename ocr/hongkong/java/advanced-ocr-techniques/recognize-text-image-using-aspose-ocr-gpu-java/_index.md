---
category: general
date: 2026-02-17
description: 使用 Aspose OCR 的 GPU 支援在 Java 中快速辨識文字影像。了解如何從影像提取文字，並設定 GPU 裝置 ID 以獲得最佳效能。
draft: false
keywords:
- recognize text image
- extract text from image
- set gpu device id
- Aspose OCR Java
- GPU acceleration OCR
language: zh-hant
og_description: 在 Java 中使用 Aspose OCR GPU 支援快速辨識文字圖像。本指南說明如何從圖像中提取文字並設定 GPU 裝置 ID。
og_title: 使用 Aspose OCR GPU 進行文字圖像辨識 – Java
tags:
- Java
- OCR
- Aspose
- GPU
title: 使用 Aspose OCR GPU 進行文字圖像辨識 – Java
url: /zh-hant/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

## Performance Tips" we translated.

Make sure to keep markdown formatting.

Now output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR GPU – Java 識別文字圖像

曾經需要在 Java 應用程式中 **recognize text image**，但 CPU 在處理大型檔案時吃緊嗎？你並非唯一遭遇此問題的人——許多開發者在處理高解析度掃描時都會碰到這個瓶頸。好消息是，Aspose OCR 讓你可以在 GPU 上 **extract text from image**，大幅縮短處理時間。  

在本教學中，我們將逐步示範一個完整、可直接執行的範例，說明如何設定授權、啟用 GPU 加速，以及在擁有多張顯示卡時 **set gpu device id**。完成後，你將擁有一個獨立的程式，能將識別出的文字印到主控台——無需其他步驟。

## 需要的條件

- **Java 17** 或更新版本（API 相容於 Java 8+，但最新的 LTS 版提供更佳效能）。  
- **Aspose OCR for Java** 函式庫（從 Aspose 官方網站下載 JAR）。  
- 有效的 **Aspose OCR license file**（`Aspose.OCR.lic`）。免費試用版可用，但 GPU 功能需授權版才能啟用。  
- 一個包含清晰機器可讀文字的影像檔（`sample-image.png`）。  
- 支援 GPU 的環境（以相容 NVIDIA CUDA 的顯示卡為佳）。  

如果上述項目聽起來陌生，別擔心——我們會在教學中逐一說明。

## 步驟 1：將 Aspose OCR 加入專案

首先，將 Aspose OCR 的 JAR 加入 classpath。若使用 Maven，請在 `pom.xml` 中加入以下相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Gradle 的寫法如下：

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

如果偏好手動方式，請將 JAR 放入 `libs/` 資料夾，並在 IDE 中加入模組路徑。

> **小技巧：** 請保持版本號與函式庫的發行說明同步；較新版本通常會帶來 GPU 處理效能的優化。

## 步驟 2：載入 Aspose OCR 授權（GPU 使用必須）

若未載入授權，`setEnableGpu(true)` 會默默退回至 CPU 模式。請在 `main` 方法開始時載入授權：

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

將 `YOUR_DIRECTORY` 替換為存放 `.lic` 檔案的絕對或相對路徑。若路徑錯誤，Aspose 會拋出 `FileNotFoundException`，請務必檢查拼寫。

## 步驟 3：建立 OCR 引擎並啟用 GPU 加速

現在我們實例化 `OcrEngine`，並指示其使用 GPU。`setGpuDeviceId` 方法可在多張顯示卡時選擇特定的卡片。

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

為什麼需要設定裝置 ID？在多 GPU 伺服器上，你可能會將一張卡片保留給影像前處理，另一張給 OCR。設定 ID 可確保正確的硬體負責繁重運算。

## 步驟 4：準備輸入影像

Aspose OCR 支援多種格式（PNG、JPG、BMP、TIFF）。將檔案包裝成 `OcrInput` 物件：

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

若需處理串流（例如上傳的檔案），請改用 `ocrInput.add(InputStream)`。

## 步驟 5：執行識別程序並取得結果

`recognize` 方法會回傳 `OcrResult`，其中包含純文字、信心分數，若需要亦可取得版面資訊。

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

主控台會顯示類似以下內容：

```
Recognized text:
Hello, world!
This is a sample image.
```

若影像模糊或語言不受支援，結果可能為空。此時請檢查 `ocrResult.getConfidence()`（0‑100）的值，以決定是否需透過前處理重新嘗試。

## 完整、可執行範例

將上述所有程式碼組合起來，即可得到一個可直接貼到 IDE 中的單一 Java 類別：

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

> **預期輸出：** 主控台會印出 `sample-image.png` 中的完整文字。若 GPU 已啟用，你會發現處理時間從數秒（CPU）下降至典型 300 dpi 掃描的不到一秒。

## 常見問題與特殊情況

### 這能在無頭伺服器上運作嗎？

可以。只要安裝 GPU 驅動即可，無需顯示器。請確保 `CUDA` 工具組（或相應的 GPU 工具）已加入系統 `PATH`。

### 如果有多於一張 GPU，想使用 GPU 1 該怎麼做？

Change the device ID:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

### 如何在不同語言下從影像中提取文字？

Set the language before calling `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose 支援超過 30 種語言；完整列表請參考 API 文件。

### 如果影像包含多頁（例如 PDF 轉成多張影像）該怎麼辦？

Create a separate `OcrInput` entry for each page, or loop over the files:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

引擎會依序串接各頁的結果。

### 如何處理低信心的結果？

Check the confidence score:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

常見的前處理步驟包括二值化、降噪或調整至 300 dpi。

## 效能優化建議

- **批次處理：** 將多張影像加入同一個 `OcrInput` 可減少重複初始化 GPU 內容的開銷。  
- **預熱：** JVM 啟動後先執行一次測試識別；首次呼叫會因驅動程式初始化而產生延遲。  
- **記憶體管理：** 完成後釋放大型 `OcrInput` 物件（`ocrInput.clear()`），以釋放 GPU 記憶體。  

## 結論

現在你已了解如何在 Java 中使用 Aspose OCR 的 GPU 引擎高效 **recognize text image**、如何在任何支援的語言中 **extract text from image**，以及在多張顯示卡環境下如何 **set gpu device id**。上述完整可執行的程式碼應可直接使用，只需替換你的授權檔與影像路徑即可。

準備好進一步了嗎？試著處理整個掃描 PDF 資料夾、實驗不同的 `setLanguage` 設定，或將 OCR 與機器學習模型結合進行後處理。可能性無窮，而 GPU 加速帶來的效能提升更讓大型專案變得可行。

祝開發順利，若遇到任何問題，歡迎留下評論！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}