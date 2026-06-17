---
category: general
date: 2026-02-14
description: 使用 Aspose OCR 從圖像中提取文字。了解如何載入圖像進行 OCR、從矩形區域讀取文字，並在幾分鐘內完成此 Aspose OCR
  教學。
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: zh-hant
og_description: 即時從圖像提取文字。本指南示範如何載入圖像進行 OCR、從矩形區域讀取文字，並完成 Aspose OCR 教學。
og_title: 使用 Aspose OCR 從圖像提取文字 – 快速指南
tags:
- Aspose
- OCR
- Java
title: 使用 Aspose OCR 從圖像提取文字 – 逐步示範
url: /zh-hant/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

header row and cells.

Let's construct final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像提取文字（使用 Aspose OCR） – 步驟示範

曾經需要**extract text from image**卻不知從何入手嗎？你並不孤單——許多開發者在首次處理收據掃描或身分驗證時都會遇到這個難題。好消息是？使用 Aspose OCR，你可以載入圖像、定義文字所在的精確區域，並在幾行程式碼內提取字元。

在本**aspose ocr tutorial**中，我們將逐步說明你所需的一切：載入 OCR 圖像、設定告訴引擎搜尋位置的矩形，最後讀取提取的文字。完成後，你將擁有一個可執行的 Java 程式，將 ROI 文字印到主控台——沒有神祕，只是一個清晰、可運作的解決方案。

## 需要的條件

在深入之前，請確保已具備以下基礎：

| 前置條件 | 重要原因 |
|--------------|----------------|
| **Java JDK 8+** | Aspose OCR 以 Java 函式庫形式提供；任何現代 JDK 都可使用。 |
| **Aspose.OCR for Java**（從 Aspose 官方網站下載或透過 Maven 加入） | 提供 `OcrEngine`、`ImageStream` 以及相關類別。 |
| **圖像檔案**（例如 `receipt.jpg`）包含可列印文字 | 我們會將引擎指向此檔案內的矩形區域。 |
| **IDE 或編輯器**（IntelliJ、Eclipse、VS Code…） | 協助你快速編譯與執行範例。 |

如果使用 Maven，請將以下相依性加入你的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **專業提示：** 上述版本號截至 2026 年 2 月為最新。升級至最新發行版可確保取得錯誤修正與效能提升。

## 步驟 1 – 初始化 OCR 引擎

首先，你需要一個 `OcrEngine` 實例。可將其視為分析像素的“大腦”。

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

為什麼要這樣建立？Aspose 將引擎（保存設定）與圖像資料分離，讓你在需要時能重複使用同一個引擎處理多張圖像，具彈性。

## 步驟 2 – 載入圖像以進行 OCR

現在我們實際**load image for OCR**。`ImageStream.fromFile` 輔助方法會將檔案讀入 Aspose 可理解的串流。

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

若找不到檔案，引擎會拋出例外，因此在正式程式碼中可能需要將其包在 try‑catch 區塊。此示範中我們直接讓例外拋出——保持範例簡潔。

## 步驟 3 – 定義矩形（從矩形讀取文字）

這裡是**read text from rectangle**發揮作用的地方。你告訴引擎精確的搜尋區域，可加快處理速度並減少誤判。

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **為什麼使用矩形？**  
> 大多數文件都有可預測的版面——例如收據金額總是出現在底部。聚焦於該區塊，OCR 引擎會忽略不相關的圖形，提升準確度。

**邊緣情況：** 若矩形超出圖像範圍，Aspose 會靜默地將其限制在邊界內，但會遺失資料。快速的合理性檢查可防止此情況發生：

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## 步驟 4 – 處理圖像

設定完成後，我們請引擎施展魔法。

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

`process()` 呼叫會回傳一個 `OcrResult` 物件，內含提取的文字、信心分數，甚至每個單字的邊界框，若日後需要可使用。

## 步驟 5 – 輸出提取的文字

最後，印出結果。在實際應用中，你可能會將其存入資料庫或傳遞給其他服務，但在本教學中，控制台輸出已足夠。

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**預期輸出**（假設矩形捕捉到收據上的總金額）：

```
ROI text:
$12.34
```

若 ROI 為空或圖像模糊，會看到空字串或亂碼。請調整矩形、提升圖像品質，或啟用 Aspose 的前處理選項（例如 `setAutoSkewCorrection(true)`）。

## 完整可執行範例

以下是完整、可直接執行的程式。將其複製貼上至名為 `RoiDemo.java` 的檔案，調整圖像路徑，然後執行 `javac RoiDemo.java && java RoiDemo`。

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **結果驗證：** 執行後，將控制台輸出與矩形內的實際文字比對。若相符，即表示你已成功使用 Aspose OCR **extract text from image**。

## 常見問題與提示

### 如果需要在同一張圖像處理多個 ROI？

為每個區域建立新的 `Rectangle`，再次呼叫 `setRegionOfInterest`，然後重新執行 `process()`。引擎會重用相同的圖像資料，效能仍保持快速。

### Aspose 如何處理不同語言或字型？

你可以透過 `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)` 變更語言模型。對於非拉丁文字，請載入相應的語言套件（可於 Aspose 下載頁面取得）。

### 此函式庫支援 PDF 輸入嗎？

是的——Aspose OCR 可直接接受 PDF 串流。只需將 `ImageStream.fromFile` 替換為 `ImageStream.fromPdfFile("doc.pdf")`，並可選擇指定頁碼。

### 如何提升低品質掃描的準確度？

啟用前處理：

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

## 結論

我們剛剛完整走過一個**aspose ocr tutorial**，示範如何使用 Java **extract text from image**、**load image for OCR** 與 **read text from rectangle**。關鍵步驟包括初始化引擎、提供圖像、定義感興趣區域、處理，最後印出結果。

接下來，你可以探索：

* **Batch processing** – 迭代收據資料夾，將每筆總金額存入資料庫。  
* **Dynamic ROI detection** – 使用影像處理函式庫（如 OpenCV）自動偵測文字區塊。  
* **Post‑processing** – 套用正規表達式或模糊比對，清理 OCR 的異常。  

試試這些想法，調整矩形以符合你的文件，你將很快擁有穩健的文字提取管線。祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}