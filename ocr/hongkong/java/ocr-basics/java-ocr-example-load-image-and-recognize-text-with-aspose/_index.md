---
category: general
date: 2026-06-16
description: Java OCR 範例，示範如何載入圖像進行 OCR、使用 Java 辨識文字，並從 JPG 檔案中以少量程式碼提取 Aspose 文字。
draft: false
keywords:
- java ocr example
- load image ocr
- recognize text java
- recognize jpg text
- extract text aspose
language: zh-hant
og_description: Java OCR 範例示範載入圖像、辨識 JPG 文字，並使用 Aspose OCR 函式庫提取。
og_title: Java OCR 範例 – 載入圖像並辨識文字
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Java OCR example that shows how to load image OCR, recognize text Java,
    and extract text Aspose from a JPG file in just a few lines.
  headline: Java OCR Example – Load Image and Recognize Text with Aspose
  type: TechArticle
- questions:
  - answer: Absolutely. Just point `ImageStream.fromFile("image.png")` to the desired
      file; Aspose auto‑detects the format.
    question: Can I process PNG or TIFF files the same way?
  - answer: Check the image resolution (≥300 dpi is ideal) and consider enabling binarization.
      Also, verify that the correct language is set.
    question: What if the OCR returns garbled characters?
  - answer: 'Yes. `result.getWords()` returns a collection where each `OcrWord` has
      a `getConfidence()` method. ## Conclusion You now have a solid **java ocr example**
      that demonstrates how to **load image ocr**, **recognize text java**, and **extract
      text aspose** from a JPEG file. The snippet runs out‑of‑the‑b'
    question: Is there a way to get confidence scores for each word?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Java OCR 範例 – 載入圖像並使用 Aspose 進行文字辨識
url: /zh-hant/java/ocr-basics/java-ocr-example-load-image-and-recognize-text-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCR 範例 – 載入影像並辨識文字 (Aspose)

有沒有想過 **java ocr example** 如何快速從圖片中提取文字？你並非唯一有此需求的人——開發者經常需要將掃描的收據、身分證或甚至螢幕截圖轉換成可編輯的字串。好消息是？使用 Aspose.OCR for Java，你可以載入影像、執行 OCR，並在幾行程式碼內取得乾淨的文字。

在本指南中，我們將逐步說明一個完整且可執行的程式，該程式會 **load image ocr** 從 JPEG 載入，**recognize text java**，並示範即使使用評估版也能 **extract text aspose**。完成後，你將擁有一個可直接套用到任何專案的完整範本。

## 你將學到什麼

- 如何將 Aspose.OCR 函式庫加入 Maven 或 Gradle 專案。  
- 從磁碟檔案中 **recognize jpg text** 所需的完整程式碼。  
- 如何偵測評估版並處理浮水印警告。  
- 處理常見問題的技巧，例如不支援的影像格式或低解析度掃描。  

不需要任何 Aspose 的先前經驗；只要具備基本的 Java 環境與一張測試用的影像檔案即可。

## 前置條件

| Requirement | Why it matters |
|-------------|----------------|
| JDK 17 或更新版本（函式庫支援 Java 8+，但較新 JDK 可提供更佳效能） | 確保與最新的 Aspose 二進位檔相容。 |
| Maven 3.x 或 Gradle 7+（或手動加入 JAR） | 簡化相依性管理。 |
| 欲處理的 JPEG 影像（`sample.jpg`） | 範例使用 JPG，但任何支援的格式皆可使用。 |
| Aspose.OCR for Java 授權（可選） | 若未取得授權，會看到評估版浮水印；程式碼會檢查此情況。 |

如果你已經有專案，只需加入以下相依性即可開始使用。

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

> **專業提示：** 保持版本號為最新；Aspose 每季發布的改進可提升辨識準確度，尤其在低對比度影像上。

## 步驟 1：建立 OCR 引擎實例

首先需要的是 `OcrEngine`。可以把它想像成分析像素並將其轉換為字元的大腦。

```java
// Step 1 – Initialize the OCR engine
OcrEngine engine = new OcrEngine();
```

為什麼要使用獨立的引擎物件？它允許在多張影像間重複使用相同設定，節省記憶體與啟動時間。

## 步驟 2：載入 OCR 影像

現在我們真的會從磁碟 **load image ocr** 資料。Aspose 提供便利的 `ImageStream` 包裝器，抽象化原始 `InputStream` 的處理。

```java
// Step 2 – Load the JPEG file you want to process
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

將 `YOUR_DIRECTORY` 替換為 `sample.jpg` 所在的絕對或相對路徑。此方法支援 PNG、BMP、TIFF，甚至多頁 PDF——因此不僅限於 JPG。

> **常見問題：** *如果我的影像是位元組陣列呢？*  
> 請改用 `ImageStream.fromBytes(byteArray)`；其餘流程保持不變。

## 步驟 3：在 Java 中辨識文字

影像已載入記憶體後，我們請 Aspose 執行繁重的工作。呼叫 `recognize()` 會執行 OCR 演算法並回傳 `OcrResult` 物件。

```java
// Step 3 – Perform OCR and get the result object
OcrResult result = engine.recognize();
```

函式庫會自動偵測語言、方向，甚至執行基本的降噪。若需強制指定語言（例如法文），可在呼叫 `recognize()` 前設定 `engine.getLanguage().setLanguage(Language.French);`。

## 步驟 4：處理評估版警告

若使用免費的評估版，結果可能會包含細微的浮水印。`isEvaluation()` 旗標可讓你警告使用者或記錄此情況。

```java
// Step 4 – Check for evaluation mode
if (result.isEvaluation()) {
    System.out.println("[EVALUATION] Result may contain a watermark.");
}
```

當你之後購買授權並透過 `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` 套用時，此區塊將不會被觸發。

## 步驟 5：抽取 Aspose 文字並印出

最後，我們從結果中取得辨識出的字串並顯示。這就是 **extract text aspose** 發生的地方。

```java
// Step 5 – Output the recognized text
System.out.println(result.getText());
```

回傳的字串保留換行，因此能相當忠實地呈現原始版面配置。

### 預期輸出

假設 `sample.jpg` 包含句子 “Hello, Aspose OCR!”，你會看到類似以下的結果：

```
[EVALUATION] Result may contain a watermark.
Hello, Aspose OCR!
```

如果影像模糊或解析度低，可能會出現多餘空格或錯讀字元——這些是常見的 OCR 奇怪現象，我們接下來會討論。

## 步驟 6：提升準確度的技巧（可選增強）

| Tip | How it helps |
|-----|--------------|
| **Increase DPI** – 在送入 `engine` 前將影像縮放至 300 dpi | 較高的解析度提供引擎更多細節以供辨識。 |
| **Pre‑process with binarization** – 使用 `engine.getImageProcessingOptions().setBinarization(true);` 轉換為黑白 | 移除可能干擾字元偵測的背景噪點。 |
| **Specify a language** – `engine.getLanguage().setLanguage(Language.English);` | 指示 OCR 引擎，減少相似字形的誤判。 |
| **Batch processing** – 為多個檔案重複使用相同的 `OcrEngine` 實例 | 減少物件建立的開銷。 |

在從掃描的收據或名片（常為低品質 JPEG） **recognize jpg text** 時，這些調整特別有用。

## 完整範例程式

以下是完整、獨立的 Java 類別，可直接複製貼上至 IDE。它包含上述的可選增強功能，若想要最小範例可將其註解掉。

```java
import com.aspose.ocr.*;

public class JavaOcrExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // OPTIONAL: Improve accuracy for low‑resolution JPEGs
        // engine.getImageProcessingOptions().setBinarization(true);
        // engine.getLanguage().setLanguage(Language.English);

        // Load the image (replace the path with your own)
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Perform OCR
        OcrResult result = engine.recognize();

        // Detect evaluation mode
        if (result.isEvaluation()) {
            System.out.println("[EVALUATION] Result may contain a watermark.");
        }

        // Print the extracted text
        System.out.println(result.getText());
    }
}
```

> **注意：** 若在未授權的情況下執行，輸出會包含評估版通知。加入有效授權檔後，通知將消失，並取得純淨文字。

## 常見問答

**Q: 我可以用相同方式處理 PNG 或 TIFF 檔案嗎？**  
A: 當然可以。只要將 `ImageStream.fromFile("image.png")` 指向目標檔案；Aspose 會自動偵測格式。

**Q: 若 OCR 回傳亂碼該怎麼辦？**  
A: 檢查影像解析度（≥300 dpi 為理想），並考慮啟用二值化。亦請確認已設定正確的語言。

**Q: 有辦法取得每個單字的信心分數嗎？**  
A: 有。`result.getWords()` 會回傳集合，其中每個 `OcrWord` 都有 `getConfidence()` 方法。

## 結論

現在你已擁有一個完整的 **java ocr example**，示範如何 **load image ocr**、**recognize text java**，以及 **extract text aspose** 從 JPEG 檔案中取得文字。此程式碼可直接執行，處理評估版警告，並提供明確的方向以提升較難影像的辨識準確度。

接下來的步驟？試著將多張發票餵入引擎、實驗不同的語言設定，或將輸出接入資料庫以建立可搜尋的檔案庫。Aspose OCR 函式庫足夠彈性，能支援從簡易桌面工具到大型文件處理管線的各種應用。

還有其他問題或想分享有趣的使用案例嗎？在下方留言吧，祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索替代實作方式。

- [使用 Aspose OCR 識別影像文字 – 完整 Java OCR 教程](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [使用 Aspose.OCR 偵測區域模式從影像提取文字（Java）](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [使用 Aspose.OCR BufferedImage 在 Java 中將影像轉換為文字](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}