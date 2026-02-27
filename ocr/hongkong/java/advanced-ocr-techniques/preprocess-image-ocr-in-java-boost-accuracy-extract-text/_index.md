---
category: general
date: 2026-02-27
description: 使用 Aspose OCR 於 Java 進行圖像 OCR 前置處理，從圖像中提取文字。了解如何提升 OCR 準確度，並有效轉換掃描圖像文字。
draft: false
keywords:
- preprocess image OCR
- extract text from image
- improve OCR accuracy
- java OCR example
- convert scanned image text
language: zh-hant
og_description: 使用 Aspose OCR 預處理影像文字辨識，以從影像中提取文字。本指南說明如何提升 OCR 準確度，並在 Java 中將掃描影像文字轉換。
og_title: 在 Java 中進行影像 OCR 前處理 – 提升準確度與擷取文字
tags:
- OCR
- Java
- Image Processing
title: 在 Java 中預處理影像 OCR – 提升準確度並擷取文字
url: /zh-hant/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 預處理影像 OCR – 完整 Java 指南

是否曾為 **預處理影像 OCR** 而苦惱，導致擷取出的文字不盡理想？你並不孤單。在許多專案中，原始掃描檔往往充斥著傾斜、斑點或低對比度，而這些微小的缺陷會破壞整個文字擷取流程。

好消息是，只要套用幾個前處理步驟──去傾斜、去噪聲與二值化──就能顯著提升 OCR 效果。在本教學中，我們將示範一個 **java OCR example**，說明如何 **從影像檔案中擷取文字**、提升辨識正確率，並最終 **將掃描影像文字** 轉換為乾淨、可搜尋的字串。

> **你將獲得：** 一個可直接執行的 Java 程式（使用 Aspose OCR）、每個設定項目的說明，以及處理極度旋轉頁面或低解析度掃描等邊緣案例的技巧。

---

## 需要的環境

- **Java Development Kit (JDK) 8** 或更新版本。  
- **Aspose.OCR for Java** 套件（本文撰寫時的最新版本 23.10）。  
- 一個欲讀取的 TIFF/PNG/JPEG 範例檔，假設檔名為 `input.tif`。  
- 你喜愛的 IDE（IntelliJ IDEA、Eclipse、VS Code… 任選其一）。

不需要額外的原生相依或外部工具；Aspose OCR 引擎會自行完成所有繁重工作。

---

## 預處理影像 OCR – 設定引擎

首先，我們建立一個 `OcrEngine` 實例。此物件保存所有後續前處理的設定。

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the configuration follows...
```

**為什麼重要：** 引擎是所有功能的入口──若省略此步驟，之後的設定將不會生效。把它想像成在開始敲擊前先打開工具箱。

---

## 啟用去傾斜以校正旋轉

掃描頁面很少會完全對齊。輕微的傾斜會導致字元被誤讀。啟用去傾斜會讓引擎自動偵測並將影像旋轉回 0°。

```java
        // Step 2: Turn on automatic deskew
        ocrEngine.getConfig().setDeskewEnabled(true);
```

*小技巧：* 去傾斜在文字行清晰可見的影像上表現最佳。若處理手寫筆記，可嘗試 `setDeskewAngleTolerance` 方法（此處未示範）以微調靈敏度。

---

## 套用去噪聲以移除雜訊

雜訊──隨機斑點或背景顆粒──會干擾 OCR 演算法。開啟去噪聲可平滑影像，保留筆畫同時剔除不相關的像素。

```java
        // Step 3: Enable denoising to clean up speckles
        ocrEngine.getConfig().setDenoiseEnabled(true);
```

**邊緣情況：** 對於解析度極低（低於 150 dpi）的掃描，過度去噪可能會抹掉淡弱字元。此時可降低 `setDenoiseLevel`（預設為中等）或直接跳過此步驟。

---

## 調整二值化閾值以提升對比

二值化會將灰階影像轉為黑白，強化墨水與紙張之間的對比。閾值（0‑255）決定了切割點。對大多數乾淨掃描而言，180 是不錯的起點，但仍可能需要微調。

```java
        // Step 4: Set a custom binarization threshold
        ocrEngine.getConfig().setBinarizationThreshold(180);
```

*為什麼是 180？* 這個值足夠高，可讓深色文字保持黑色，同時將較亮的背景變白，讓 OCR 引擎更專注於真正的字元。若來源是已褪色的舊文件，可嘗試較低的值，例如 120。

---

## 處理影像並擷取文字

現在引擎已就緒，我們將檔案路徑傳入。`processImage` 方法會回傳一個 `OcrResult` 物件，內含辨識文字與信心分數。

```java
        // Step 5: Process the image file
        OcrResult ocrResult = ocrEngine.processImage("YOUR_DIRECTORY/input.tif");
```

**如果找不到檔案會怎樣？** 此方法會拋出 `IOException`。在正式程式碼中，你應將此呼叫包在 try‑catch 區塊，並記錄友善的錯誤訊息。

---

## 驗證輸出

最後，我們把擷取到的字串印到主控台。這裡可以檢視前處理是否真的有幫助。

```java
        // Step 6: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(ocrResult.getText());
    }
}
```

預期輸出（為簡潔起見已截斷）：

```
=== OCR Result ===
The quick brown fox jumps over the lazy dog.
```

若結果仍出現雜訊字元，請重新檢查閾值，或考慮在送入 Aspose OCR 前加入自訂濾鏡（例如形態學開運算）。

---

## 使用 Aspose OCR 從影像擷取文字

上方程式碼即為 **java OCR example**，示範完整流程──從載入影像到印出乾淨文字。因所有前處理皆透過 `Config` 物件完成，你可以在不改動核心邏輯的情況下，隨意增減個別步驟。

**快速檢查清單：**

1. 使用 `processImage` **載入** 影像。  
2. 若來源為掃描文件，**啟用** `Deskew` 與 `Denoise`。  
3. 依目視檢查**調整** `BinarizationThreshold`。  
4. 讀取 `ocrResult.getText()`，並依需求儲存──資料庫、檔案或 UI。

---

## 提升 Java OCR 準確度的技巧

- **解析度很重要：** 掃描時至少要 300 dpi。更高的 DPI 能提供更多像素資訊給引擎。  
- **彩色 vs. 灰階：** 在處理前先將彩色掃描轉為灰階，可減少運算時間且不影響準確度。  
- **批次處理：** 若有數十甚至上百個檔案，請重複使用同一個 `OcrEngine` 實例──頻繁建立會增加開銷。  
- **語言套件：** Aspose OCR 支援多種語言；設定 `ocrEngine.getConfig().setLanguage(OcrLanguage.English)`（或其他語言）可提升非英文文字的辨識率。

---

## 將掃描影像文字轉為可編輯字串

取得原始字串後，可能還需要進一步清理──移除換行、正規化空白或執行拼寫檢查。Java 的 `String` 方法以及 Apache Commons Text 等函式庫都能輕鬆完成。

```java
String cleaned = ocrResult.getText()
                          .replaceAll("\\s+", " ")
                          .trim();
System.out.println("Cleaned text: " + cleaned);
```

現在文字已可存為 `.txt` 檔、插入 PDF，或送入下游的 NLP 流程。

---

![preprocess image OCR example](/images/preprocess-ocr-demo.png "preprocess image OCR example showing console output")

*上圖顯示執行完整 Java 程式後的主控台輸出畫面。*

---

## 結論

你剛剛學會如何在 Java 中 **預處理影像 OCR**，透過去傾斜、去噪聲與二值化，**從影像檔案中擷取文字**，且可靠度大幅提升。只要微調幾個設定旗標，即可 **改善 OCR 準確度**、處理棘手的掃描檔，最終 **將掃描影像文字** 轉換為乾淨、可搜尋的字串──全部都在這個精簡的 **java OCR example** 內完成。

準備好下一步了嗎？試著把擷取的文字寫入資料庫、使用 Aspose PDF 產生可搜尋的 PDF，或探索多語言支援。相同的前處理管線同樣適用於 PDF、PNG 與 JPEG，讓你能在任何文件數位化專案中擴展此模式。

祝開發順利，願你的 OCR 結果永遠晶瑩剔透！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}