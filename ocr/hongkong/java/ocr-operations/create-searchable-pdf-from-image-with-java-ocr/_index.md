---
category: general
date: 2026-05-06
description: 使用 Aspose OCR 在 Java 中從圖像建立可搜尋的 PDF。了解如何將圖像轉換為 PDF、啟用拼寫校正，並使用 OCR GPU
  以獲得快速結果。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: zh-hant
og_description: 使用 Aspose OCR 在 Java 中將圖像轉換為可搜尋的 PDF。本指南說明如何將圖像轉換為 PDF、啟用拼寫校正，以及使用
  OCR GPU。
og_title: 使用 Java OCR 從圖像建立可搜尋的 PDF
tags:
- OCR
- Java
- PDF
title: 使用 Java OCR 從圖片建立可搜尋的 PDF
url: /zh-hant/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java OCR 從圖像建立可搜尋的 PDF

是否曾需要從掃描圖片**建立可搜尋的 PDF**，卻不知從何開始？你並不孤單——大多數開發者在首次處理基於圖像的 PDF 時都會碰到這個問題。幸運的是，使用 Aspose OCR for Java，你可以**將圖像轉換為 PDF**，將文字轉為可選取的內容，甚至加入拼寫校正以獲得更完善的結果。

在本教學中，我們將逐步說明一個完整、可直接執行的範例，展示如何在可用時**使用 OCR GPU**、如何有效**處理圖像 OCR**，以及為何啟用拼寫校正對後續搜尋很重要。完成後，你將擁有一鍵產生可搜尋 PDF 的方式，能夠提供給使用者或作為合規存檔。

> **專業提示：**如果你在沒有 GPU 的機器上執行，程式碼會自動回退到 CPU，無需重新編寫任何程式。

---

## 需要的環境

- **Java 8+**（程式碼可在 JDK 8 及更新版本編譯）
- **Aspose OCR for Java** 函式庫（從 Aspose 官方網站下載最新 JAR）
- **輸入圖像**（JPEG、PNG、TIFF 等），用於轉換為可搜尋的 PDF
- （可選）具備 CUDA 支援的 **GPU**，若想獲得最快的辨識速度

不需要額外框架，也不需要 Maven/Gradle 魔法——只要在 classpath 中放入單一 JAR，即可開始。

---

## 步驟 1：初始化 OCR 引擎 – 流程核心  

首先，我們建立 `OcrEngine` 實例並指向來源檔案。此物件是執行讀取圖像、運行神經網路並回傳文字的主要工作者。

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*為何重要：*只初始化一次引擎並重複使用，可避免重複載入原生函式庫的開銷——這在批次處理數十個檔案時會累積成顯著的效能提升。

---

## 步驟 2：選擇處理裝置 – 盡可能使用 OCR GPU  

如果你的工作站具備相容的 GPU，可指示 Aspose 在其上執行繁重運算。否則引擎會自動切換至 CPU。

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*有何好處？*GPU 加速可為每頁節省數秒，尤其是高解析度掃描時。回退機制確保相同程式碼在任何環境皆可執行，這也是我們建議將 **use OCR GPU** 設為預設設定的原因。

---

## 步驟 3：加速掃描 – 利用所有 CPU 核心  

即使 GPU 正在忙碌，周邊的前處理步驟仍可平行化。將執行緒數設定為可用處理器核心數，可讓引擎同時處理多個資料塊。

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*注意：*在 4 核心筆記型電腦上會啟動四個執行緒；在 16 核心工作站上則可獲得完整效益。請留意，執行緒數增多會導致記憶體使用量提升。

---

## 步驟 4：清理圖像 – 前處理濾鏡  

模糊或雜訊過多的掃描會產生垃圾文字。加入幾個內建濾鏡可大幅提升準確度。

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*為何使用這些濾鏡？*`DeskewFilter` 校正文件在掃描時因角度導致的旋轉。`NoiseRemovalFilter` 移除會被誤判為字元的雜散像素。可將其視為給 OCR 引擎一張乾淨的紙張閱讀。

---

## 步驟 5：開啟智慧功能 – 啟用拼寫校正與自動語言偵測  

若處理多語言文件，或僅想減少錯別字，可開啟內建拼寫檢查器，讓引擎自動偵測語言。

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*何時有用？*假設掃描文件同時包含英文與西班牙文段落。自動偵測功能會即時切換字典，而拼寫校正則會修正如將 “0” 誤讀為 “O” 等錯誤。此步驟對產生實際能返回正確結果的 **searchable PDF** 至關重要。

---

## 步驟 6：儲存結果 – 將圖像轉換為 PDF 並使其可搜尋  

最後，我們請引擎輸出一個 PDF，原始圖像位於隱形文字層之下。這是經典的 **convert image to PDF** 工作流程，但 PDF 現在已具備可搜尋功能。

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

輸出檔案 (`output-searchable.pdf`) 可在任何 PDF 檢視器中開啟；你將能像原生 PDF 一樣選取、複製與搜尋文字。無需額外工具。

---

## 完整範例 – 直接貼上執行  

以下為完整程式碼，已可直接編譯。將 `YOUR_DIRECTORY` 替換為存放 `input.jpg` 的資料夾路徑。

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**預期輸出：**執行程式時，你會在主控台看到 *“Searchable PDF generated successfully.”* 的訊息。於 Adobe Reader 開啟 `output-searchable.pdf`，即可在搜尋框輸入原始圖像中的文字，立即跳至相應位置。

---

## 常見問題與邊緣案例  

- **如果未偵測到 GPU？**  
  `setDeviceType(OcrDeviceType.GPU)` 呼叫不會拋出例外；它僅指示引擎先嘗試使用 GPU。若失敗，則會靜默回退至 CPU。

- **是否可以一次處理多張圖像？**  
  可以。將程式碼包在迴圈中，每次迭代更換檔名，並重複使用同一個 `OcrEngine` 實例，以降低記憶體使用。

- **我的 PDF 太大——如何縮小？**  
  OCR 完成後，你可以使用 Aspose 的 PDF 最佳化 API，或在送入引擎前先縮小來源圖像（例如 `ImageStream.fromFile(...).setResolution(150)` 以 150 DPI）。

- **我需要保留原始圖像解析度以符合法規要求。**  
  `PDF_SEARCHABLE` 格式會完整保留原始位圖；隱形文字層會疊加於上方，且不會改變視覺品質。

---

## 視覺摘要  

![建立可搜尋 PDF 範例](placeholder-image.png "建立可搜尋 PDF 範例")

*Alt text:* *建立可搜尋 PDF 範例 – Java OCR 引擎將掃描的 JPG 轉換為可搜尋的 PDF。*

---

## 結論  

現在，你已擁有使用 Aspose OCR for Java 將任何圖像轉換為 **searchable PDF** 的 **完整、端到端解決方案**。透過 **convert image to PDF**、**啟用拼寫校正**，以及在可能時 **使用 OCR GPU**，即可獲得快速、精確且可搜尋的結果，且能跨平台運作。

接下來可以嘗試以下實驗：

- **不同的輸出格式**（`PDF`、`DOCX`、`HTML`）以觀察文字層的表現。
- **自訂字典**，若你處理特定領域的術語。
- **批次處理**，自動處理數千張掃描檔。

隨意調整執行緒數、替換濾鏡，或接入自己的前處理流程。核心模式保持不變：載入 → 前處理 → 設定 → OCR → 儲存。

祝程式開發順利，願你的 PDF 永遠可搜尋！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}