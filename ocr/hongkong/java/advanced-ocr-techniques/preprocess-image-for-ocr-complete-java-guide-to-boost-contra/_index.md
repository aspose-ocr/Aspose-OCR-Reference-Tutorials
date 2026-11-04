---
category: general
date: 2026-02-17
description: 使用 Aspose OCR 在 Java 中預處理圖像以進行 OCR。學習如何提升圖像對比度、設定對比度水平，並在短短幾分鐘內從圖像中辨識文字。
draft: false
keywords:
- preprocess image for ocr
- boost image contrast
- recognize text from image
- extract text using OCR
- set contrast level
language: zh-hant
og_description: 使用 Aspose OCR Java 進行影像預處理以供 OCR。本指南說明如何提升影像對比度、設定對比度等級，並快速辨識影像中的文字。
og_title: 圖像前處理（OCR）– Java 教學：提升對比度與擷取文字
tags:
- Java
- OCR
- Image Processing
title: OCR 圖像預處理 – 完整 Java 指南：提升對比度與提取文字
url: /zh-hant/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 預處理影像以進行 OCR – 完整 Java 指南

有沒有過想要 **預處理影像以進行 OCR**，卻不清楚哪些設定真的會產生差異？你並不孤單。大多數開發者會把影像直接丟給 OCR 引擎，期待奇蹟發生，結果卻得到雜亂的輸出。在本教學中，我們將一步步示範一個實用的端對端範例，**提升影像對比度**、調整 **對比度等級**，最後使用 Aspose OCR for Java **從影像辨識文字**。

完成後，你將擁有一段可重複使用的程式碼片段，能在噪點較多的掃描檔上 **可靠地使用 OCR 抽取文字**。沒有隱藏技巧，只有清晰的步驟與背後的原理說明。

## 你需要的環境

- Java 17 或更新版本（程式碼可在任何近期 JDK 上編譯）
- Aspose OCR for Java 套件（從官方 Aspose 網站下載）
- 有效的 Aspose OCR 授權檔 (`Aspose.OCR.lic`)
- 想要讀取的輸入影像 (`input.jpg`)
- 喜愛的 IDE 或簡易的命令列環境

如果你已備妥上述項目，太好了——直接進入下一步。

## 步驟 1：載入 Aspose OCR 授權（主要設定）

在 OCR 引擎執行任何操作之前，必須先告訴它你已取得授權，否則會看到試用水印。

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**為什麼這很重要：** 若未正確設定授權，引擎會以評估模式運作，可能會截斷結果或加入水印。提前設定授權也能確保之後的所有預處理選項都在完整功能模式下生效。

## 步驟 2：初始化 OCR 引擎

建立 `OcrEngine` 實例即可同時取得辨識與預處理管線的存取權。

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**小技巧：** 若你計畫一次處理大量影像，建議將引擎作為 singleton 使用；它會快取內部資源，提升後續呼叫的速度。

## 步驟 3：設定預處理 – 旋轉校正、去噪與對比度增強

這裡就是 **預處理影像以進行 OCR** 的關鍵。我們要調整的三個參數如下：

1. **旋轉校正（Deskew）** – 修正輕微的旋轉角度。  
2. **去噪（Denoise）** – 移除會干擾字元分割的斑點。  
3. **對比度增強（Contrast enhancement）** – 讓深色文字在背景上更突出。

```java
        // Access preprocessing settings
        PreprocessingSettings preprocessing = ocrEngine.getPreprocessing();

        // Enable automatic deskew (helps with scanned pages that are a few degrees off)
        preprocessing.setDeskew(true);
        preprocessing.setDeskewAngleTolerance(0.1); // tolerance in degrees

        // Turn on denoising – median works well for salt‑and‑pepper noise
        preprocessing.setDenoise(true);
        preprocessing.setDenoiseMode(DenoiseMode.MEDIAN); // alternatives: GAUSSIAN

        // Boost contrast – this is the “boost image contrast” step
        preprocessing.setContrastEnhance(true);
        preprocessing.setContrastLevel(1.3f); // 1.0 = no change, >1.0 = stronger contrast
```

### 為什麼要調整對比度等級？

提升對比度等級會拉伸影像的直方圖，使暗像素更暗、亮像素更亮。實務上，`1.3f` 的 **對比度等級** 常能在印刷文件上取得最佳平衡；若超過 `1.5f`，則可能使細線條過曝。隨意嘗試即可，因為此設定改變成本低，卻能顯著提升 **從影像辨識文字** 的成功率。

## 步驟 4：準備輸入影像

`OcrInput` 類別抽象化了檔案處理。如果需要批次處理，你甚至可以一次加入多張影像。

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**邊緣情況：** 若影像是非標準格式（例如多頁 TIFF），可分別載入每一頁，或先轉換成 PNG/JPEG。

## 步驟 5：執行辨識

現在引擎會先跑我們剛設定好的預處理管線，然後把清理過的影像交給核心 OCR 演算法。

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**底層發生了什麼？** Aspose OCR 會先套用旋轉校正，接著執行去噪濾鏡，最後調整對比度，然後將影像送入基於神經網路的辨識器。此順序是刻意設計的，若改變順序可能會導致次佳結果。

## 步驟 6：輸出辨識文字

最後，我們把抽取出的字串印到主控台。實際應用中，你可能會寫入檔案或傳送至網路。

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### 預期輸出

若 `input.jpg` 內含文字 “Hello World!”，主控台應顯示：

```
Hello World!
```

如果輸出雜亂，請再次檢查預處理參數——尤其是 **對比度等級** 與 **去噪模式**，並嘗試不同的影像格式。

## 加分項目：視覺化預處理後的影像（可選）

有時你想看看引擎在旋轉校正、去噪與對比度增強之後看到的畫面。Aspose OCR 允許匯出中間位圖：

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

將 `processed.png` 與原始檔並排開啟；你會注意到水平線更直、文字更清晰。這步驟在排除特定掃描失敗原因時相當有用。

![預處理影像以進行 OCR 範例](/images/ocr-preprocess-example.png "預處理影像以進行 OCR – 對比度提升前後比較")

*上圖說明了透過提升對比度與去噪，如何將模糊掃描轉變為乾淨、適合 OCR 的圖片。*

## 常見陷阱與避免方式

| 陷阱 | 為什麼會發生 | 解決方法 |
|------|--------------|----------|
| **過度對比**（`setContrastLevel` 設定過高） | 背景變白，導致細微字元消失 | 大多數印刷文字的對比度等級保持在 **1.1** 到 **1.4** 之間 |
| **旋轉容差過低** | 小幅旋轉未被校正 | 將 `setDeskewAngleTolerance` 提升至 **0.2** 或 **0.3**（適用於掃描書本） |
| **在二值影像上使用 GAUSSIAN 去噪** | 模糊邊緣，導致字元合併 | 對黑白掃描使用 `DenoiseMode.MEDIAN` |
| **缺少授權** | 引擎退回試用模式，結果被截斷 | 確認 `Aspose.OCR.lic` 的路徑正確且檔案可讀取 |

## 往後的方向：超越基礎預處理

既然已能 **預處理影像以進行 OCR** 並 **使用 OCR 抽取文字**，可以考慮以下延伸：

- **語言套件** – 載入特定語言字典，提升非英文文字的辨識準確度。  
- **感興趣區域（ROI）裁切** – 若只需要頁面的一部分，可只處理該子區域。  
- **批次處理** – 迴圈遍歷資料夾內的多張影像，重複使用同一個 `OcrEngine` 實例以加速。  
- **與 PDF 結合** – 結合 Aspose OCR 與 Aspose PDF，將掃描 PDF 直接轉換為可搜尋的 PDF，形成一條完整管線。

上述每個主題都自然包含我們的次要關鍵字：你仍會 **提升影像對比度**、**設定對比度等級**，並在各種情境下 **從影像辨識文字**。

## 結論

我們已完整說明如何使用 Aspose OCR for Java **預處理影像以進行 OCR**：載入授權、設定旋轉校正、去噪與對比度增強、送入影像，最後 **從影像辨識文字**。有了上述可直接執行的範例，你現在可以在任何適當處理過的圖片上 **使用 OCR 抽取文字**。

試著執行程式碼、調整 **對比度等級**，觀察準確度的提升。準備好之後，可探索語言特定模型或批次管線，將單張影像示範升級為生產等級的解決方案。

*祝程式開發順利，願你的掃描永遠清晰！*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}