---
category: general
date: 2026-05-06
description: 如何在 Java 中使用 OCR 從圖像提取文字。學習 OCR 圖像轉文字的轉換、校正 OCR 錯誤，並使用 Aspose OCR 載入圖像進行
  OCR。
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: zh-hant
og_description: 如何在 Java 中使用 Aspose OCR 進行光學字符辨識，從圖像提取文字、校正 OCR 錯誤及載入圖像進行 OCR。
og_title: 在 Java 中使用 OCR 的完整指南
tags:
- OCR
- Java
- Aspose
title: 如何在 Java 中使用 OCR – 從圖像提取文字並進行拼寫校正
url: /zh-hant/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 OCR – 從圖片提取文字並進行拼寫校正

有沒有想過 **如何使用 OCR** 把模糊的收據照片變成乾淨、可搜尋的文字？你並不孤單。無論是支出追蹤應用、發票數位化流程，或是快速筆記腳本，從圖片取得可靠文字往往是第一道關卡。

本教學將一步步示範如何在 Java 中使用 OCR，涵蓋從載入圖片到校正 OCR 錯誤，使最終結果看起來像是人工輸入。完成後，你將能 **從圖片提取文字**、執行 **OCR 圖片轉文字**，並自動修正常見的辨識錯誤。

## 你將會建立的程式

我們會建立一個小型的 Java 主控台程式，功能如下：

1. 將 PNG（或任何支援格式）載入 Aspose OCR 引擎。  
2. 啟用內建的拼寫校正功能以 **校正 OCR 錯誤**。  
3. 執行辨識程序並印出已清理的文字。  

不需要外部服務，也不需要龐大的框架——只要一個 JAR 檔與幾行程式碼。

### 前置條件

- Java Development Kit (JDK) 8 或更新版本。  
- Maven（或任何建置工具）以取得 Aspose OCR 函式庫。  
- 一張你想分析的圖片檔（例如 `receipt.png`）。  

如果缺少 Aspose OCR JAR，請在 `pom.xml` 中加入以下相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **小技巧：** 免費評估版可用於測試，但購買授權後會移除評估水印。

## 步驟 1 – 初始化 OCR 引擎（主要關鍵字實作）

首先需要建立 `OcrEngine` 的實例。把它想像成會閱讀像素並轉換成字元的大腦。

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*為什麼重要：* 初始化引擎會配置內部資源（語言模型、字典等）。若省略此步驟，稍後載入圖片時會拋出 `NullPointerException`。

## 步驟 2 – 載入圖片以供 OCR

現在正式 **載入圖片以供 OCR**。Aspose 提供便利的 `ImageStream.fromFile` 輔助方法，當然你也可以直接傳入 `byte[]`。

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*常見陷阱：* 檔案路徑必須是絕對路徑或相對於工作目錄的路徑。若找不到圖片，引擎會拋出 `IOException`。請特別留意在 IDE 與打包成 JAR 後的路徑差異。

## 步驟 3 – 啟用拼寫校正以 **校正 OCR 錯誤**

預設的 OCR 可能會產生雜訊——例如把 “love” 讀成 “l0ve”，或把 “O” 讀成 “0”。啟用拼寫校正會讓引擎在辨識後執行一次後處理，修正常見錯誤。

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*為什麼需要：* 若不啟用拼寫校正，你可能必須手動清理輸出，這樣就失去了自動化的意義。內建字典對英文及其他幾種語言的支援相當不錯。

## 步驟 4 – 執行辨識（**OCR 圖片轉文字**）

圖片已載入且拼寫校正已開啟，現在可以請引擎進行文字辨識。

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*邊緣情況：* 若圖片對比度低或嚴重傾斜，結果仍可能出現亂碼。建議在送入引擎前先做前處理（例如二值化、去傾斜）。

## 步驟 5 – 輸出已清理的文字

最後一步只需要把結果印出。實務上可能會寫入資料庫或檔案，但此示範只用 `System.out` 即可。

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### 預期輸出

假設 `receipt.png` 包含清晰的商品清單，可能會看到類似以下的輸出：

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

可以看到即使原始掃描中出現了 “Qy”，最終仍正確顯示為 “Qty” 與 “Price”。

## 完整範例程式

以下是完整程式碼，可直接複製貼上至 `SpellCorrectDemo.java`。請確保 Aspose OCR JAR 已加入 classpath。

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

執行方式：

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

執行後，你應該會在主控台看到已清理的文字。

## 加分：調整設定以提升準確度

雖然預設組態已能應付大多數列印文件，特定情境下仍可能需要微調參數：

| 設定 | 功能說明 | 何時調整 |
|------|----------|----------|
| `setLanguage(OcrLanguage.English)` | 強制使用英文字典（降低誤判） | 圖片僅含英文文字時 |
| `setResolution(300)` | 告訴引擎來源圖片的 DPI | 高解析度掃描時 |
| `setEnableAutoSkewCorrection(true)` | 自動校正輕微傾斜的頁面 | 圖片是手機拍攝時 |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## 常見問題

**Q: 這能處理 PDF 嗎？**  
A: 能。先將每頁 PDF 轉成圖片（例如使用 Aspose PDF），再交給 OCR 引擎。

**Q: 我的圖片是 BMP 格式可以嗎？**  
A: `ImageStream.fromFile` 內建支援 PNG、JPEG、BMP、TIFF 與 GIF，只要更換副檔名即可。

**Q: 可以關閉拼寫校正嗎？**  
A: 完全可以——若需要原始 OCR 輸出供後續處理，只要設定 `setEnableSpellCorrection(false)` 即可。

## 結論

現在你已掌握 **如何在 Java 中使用 OCR** 來 **從圖片提取文字**、自動 **校正 OCR 錯誤**，以及正確 **載入圖片以供 OCR** 的完整流程。這五步（初始化、載入、啟用拼寫校正、辨識、輸出）涵蓋了大多數日常 OCR 任務。

接下來，你可以將此邏輯串接至資料庫寫入、REST 端點，或批次處理器，以一次處理多張收據。也可以嘗試上表的額外設定，爭取每一個字元的準確度。

祝程式開發順利，願你的 OCR 結果永遠比咖啡污漬的收據還要乾淨！

![如何使用 OCR 圖示：圖片 → OCR 引擎 → 校正後文字流程]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}