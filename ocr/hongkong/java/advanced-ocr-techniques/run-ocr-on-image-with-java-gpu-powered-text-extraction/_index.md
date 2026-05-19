---
category: general
date: 2026-03-07
description: 使用 Java 在影像上執行 OCR。了解如何從 PNG 辨識文字、從收據提取文字，並以完整的 Java OCR 範例載入影像進行 OCR。
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: zh-hant
og_description: 使用 Java 對圖像執行 OCR。本指南示範如何從 PNG 識別文字、從收據提取文字，以及使用完整的 Java OCR 範例載入圖像進行
  OCR。
og_title: 使用 Java 在圖像上執行 OCR – GPU 加速文字提取
tags:
- OCR
- Java
- GPU
- Image Processing
title: 使用 Java 在圖片上執行 OCR – GPU 加速文字提取
url: /zh-hant/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中執行影像 OCR – GPU 加速文字擷取

曾經需要 **在影像上執行 OCR**，但不知在 Java 中從何開始嗎？你並不孤單——許多開發者在首次嘗試從掃描收據或 PNG 截圖中擷取文字時，都會碰到同樣的障礙。  

在本教學中，我們將帶領你完成一個 **完整的 Java OCR 範例**，它不僅 **辨識 PNG 檔案中的文字**，還示範如何 **從收據影像中擷取文字**，同時利用 GPU 加速提升速度。完成後，你將擁有一個可直接執行的程式，能載入影像進行 OCR、處理並輸出純文字結果。

## 你將學會

- 如何使用簡單的 `ImageInputStream` **載入 OCR 影像**。
- 啟用 GPU 支援，使引擎在現代硬體上運行更快。
- 逐步說明 **從 PNG 辨識文字** 並從收據中提取有用字串的完整流程。
- 常見陷阱（例如 GPU 裝置 ID 錯誤）與最佳實踐技巧。
- 完整、可執行的程式碼片段，直接複製貼上至 IDE 使用。

**先決條件**

- Java 17 或更新版本（程式碼使用 `var` 關鍵字以簡化，但若你使用 Java 8，可改為明確的型別）。
- 提供 `OcrEngine`、`ImageInputStream` 與 `OcrResult` 類別的 OCR 函式庫（例如虛構的 *FastOCR* SDK；請換成你實際使用的庫）。
- 若想提升效能，需具備支援 GPU 的機器（非必須，但建議使用）。

---

## 步驟 1：在影像上執行 OCR – 啟用 GPU 加速

首先需要建立 OCR 引擎並告訴它使用 GPU。此步驟至關重要，因為若未啟用 GPU 支援，引擎會退回使用 CPU，對於高解析度的收據而言速度會明顯較慢。

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**為何這很重要：**  
GPU 加速會將 OCR 引擎執行的繁重矩陣計算卸載至顯示卡。如果有多張 GPU，可透過修改 `setGpuDeviceId` 的值來選擇記憶體最大的那一張。忘記啟用 GPU 是導致「為何我的 OCR 那麼慢？」的常見原因。

> **專業提示：** 若你的機器沒有相容的 GPU，`setUseGpu(true)` 呼叫只會被忽略——不會當機，只是處理速度較慢。

---

## 步驟 2：載入 OCR 影像

引擎已就緒後，我們需要提供一張影像。以下範例示範如何載入儲存在磁碟上的 PNG 收據。你可以將路徑換成 OCR 函式庫支援的任何影像格式。

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**邊緣情況：**  
若檔案不存在或路徑錯誤，`ImageInputStream` 會拋出 `IOException`。請將呼叫包在 try‑catch 區塊中，並記錄有用的訊息：

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## 步驟 3：從 PNG 辨識文字

影像載入後，OCR 引擎即可開始發揮魔法。此步驟實際上會 **從 PNG 辨識文字**（或任何其他支援的格式），並回傳 `OcrResult` 物件。

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**底層發生了什麼？**  
引擎會先進行前處理（去斜、二值化），接著執行神經網路偵測字元，最後將字元組合成文字行。由於先前已啟用 GPU，這些神經網路計算會在顯示卡上執行，為總執行時間省下數秒。

---

## 步驟 4：從收據擷取文字

辨識完成後，你通常只需要原始文字。`OcrResult` 類別通常提供 `getText()` 方法，回傳單一 `String`。之後你可以進行後處理（例如使用正規表達式抽取總金額、日期等）。

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**典型的收據輸出範例：**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

現在你可以將此字串傳入自訂的解析器，抽取總金額、項目明細或稅務資訊。

---

## 步驟 5：完整 Java OCR 範例 – 可直接執行

將上述所有步驟整合後，以下是 **完整的 Java OCR 範例**，可直接貼入 `Main.java` 檔案。請確保 OCR 函式庫已加入 classpath。

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**預期的主控台輸出**（假設使用上方的範例收據）：

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

若輸出呈現亂碼，請再次確認影像是否清晰（高 DPI）且 OCR 語言套件與收據語言相符。

---

## 常見問題與注意事項

| Question | Answer |
|----------|--------|
| *如果我的 GPU 未被偵測到怎麼辦？* | 引擎會自動回退至 CPU。請確認驅動程式已安裝，且 `setGpuDeviceId` 與現有裝置相符（可使用 Linux 上的 `nvidia-smi` 進行檢查）。 |
| *我可以處理 JPEG 或 TIFF 檔案嗎？* | 可以——只要在 `ImageInputStream` 中更改檔案副檔名即可。OCR 函式庫通常會自動偵測格式。 |
| *有沒有辦法批次處理多張收據？* | 將辨識程式碼包在迴圈中，重複使用同一個 `OcrEngine` 實例；每張影像重新初始化會浪費 GPU 記憶體。 |
| *如何提升低對比度收據的辨識準確度？* | 在送入 OCR 引擎前先對影像進行前處理（提升對比、轉為灰階）。部分函式庫提供 `preprocess` API 可使用。 |

---

## 結論

現在你已了解如何在 Java 中 **對影像檔案執行 OCR**，從載入圖片到從收據中擷取乾淨文字。此教學涵蓋了 **從 PNG 辨識文字**、**從收據擷取文字**，並示範了一個可套用於任何專案的 **Java OCR 範例**。  

接下來的步驟？可以關閉 GPU 旗標觀察效能差異、嘗試不同的影像解析度，或整合基於正規表達式的解析器自動抽取總金額。若想深入更進階的主題，可研究 **OCR 後處理**、**語言模型校正** 或 **批次處理管線**。  

祝開發順利，願你的收據永遠清晰可讀！  

![執行影像 OCR 範例](/images/run-ocr-on-image.png "執行影像 OCR – Java 範例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}