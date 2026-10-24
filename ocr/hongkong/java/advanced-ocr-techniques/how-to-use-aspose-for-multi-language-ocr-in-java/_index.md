---
category: general
date: 2026-10-24
description: 了解如何使用 Aspose OCR 在 Java 中從圖像提取文字，支援英語、烏克蘭語和阿拉伯語。一步一步的指南，說明如何載入圖像進行 OCR
  以及對圖像執行 OCR。
draft: false
keywords:
- extract text from image
- load image for ocr
- run ocr on image
- Aspose OCR Java
- multi language OCR
lastmod: 2026-10-24
og_description: 了解如何使用 Aspose OCR 在 Java 中從圖像提取文字，支援英語、烏克蘭語和阿拉伯語。載入圖像進行 OCR 並執行 OCR
  的步驟。
og_image_alt: 'Developer guide: extract text from image using Aspose OCR in Java'
og_title: 如何使用 Aspose OCR 在 Java 中從圖像提取文字
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to extract text from image using Aspose OCR in Java, supporting
    English, Ukrainian and Arabic. Step‑by‑step guide to load image for OCR and run
    OCR on image.
  headline: How to extract text from image with Aspose OCR in Java
  type: TechArticle
- questions:
  - answer: No, a single Aspose OCR license covers all bundled language packs.
    question: Do I need a separate license for each language pack?
  - answer: The only practical limit is memory; Aspose processes each image sequentially,
      so you can add hundreds of files without issue.
    question: Is there a limit on the number of images I can add to `OcrInput`?
  - answer: The engine analyses each text block independently, so it can switch languages
      mid‑line and still produce accurate results.
    question: How does auto‑detection handle mixed scripts on the same line?
  - answer: Yes, `OcrResult` provides a `getConfidence()` method for granular quality
      metrics.
    question: Can I get confidence scores for each recognized word?
  - answer: Aspose OCR works with Java 8 through Java 21, including LTS releases.
    question: What Java versions are supported?
  type: FAQPage
tags:
- Aspose
- OCR
- Java
- extract text from image
- multi language OCR
title: 如何使用 Aspose OCR 在 Java 中從圖像提取文字
url: /zh-hant/java/advanced-ocr-techniques/how-to-use-aspose-for-multi-language-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 在 Java 中從圖像提取文字

如果您需要從包含英語、烏克蘭語和阿拉伯語字符混合的圖像檔案中**提取文字**，Aspose OCR 讓這變得簡單。在本教學中，您將看到一個完整、可直接執行的範例，展示如何**載入圖像以進行 OCR**、啟用*多語言 OCR*，最後**對圖像執行 OCR**以取得乾淨、可讀的文字。步驟以簡明語言說明，讓您了解*做什麼*以及*為何重要*。

## 快速解答
- **第一行程式碼是什麼？** `OcrEngine engine = new OcrEngine();`
- **預設支援哪些語言？** 英文 (`en`)、烏克蘭語 (`uk`)、阿拉伯語 (`ar`) 以及另外 27 種語言。
- **測試時需要授權嗎？** 不需要，免費試用即可，但授權會移除浮水印。
- **可以一次處理多張圖像嗎？** 可以，使用 `OcrInput` 在呼叫 `recognize` 前加入多個檔案。
- **需要哪個 Java 版本？** Java 8 或更新版本。

## 如何使用 Aspose OCR 在 Java 中從圖像提取文字？

使用 `OcrInput` 載入圖像，為 `OcrEngine` 設定所需語言，然後呼叫 `engine.recognize(input)`。引擎會自動偵測語言區塊、套用正確的 OCR 模型，並回傳包含已辨識文字的 `OcrResult`。此一步驟流程支援最高 10 000 × 10 000 像素的任何圖像尺寸，並支援超過 30 種語言套件。

## 您將學習到

- 將 Aspose OCR 函式庫加入 Java 專案（Maven 或 Gradle）。  
- 正確初始化 OCR 引擎。  
- 設定引擎以支援*多語言 OCR*並啟用自動偵測。  
- 載入包含多種文字的圖像。  
- 執行辨識並**從圖像提取文字**。  
- 處理常見問題，例如不支援的語言或檔案遺失。

完成後，您將擁有一個可自行使用的 Java 類別，能直接放入任何專案，即時開始處理圖像。

## 前置條件

| 前置條件 | 為何重要 |
|-------------|----------------|
| Java 8 或更新版本 | Aspose OCR 以 Java 8+ 為目標。 |
| Maven 或 Gradle（任何建置工具） | 會自動下載 Aspose OCR JAR。 |
| 含有多語言文字的圖像檔案（例如 `mixed_script.jpg`） | 這就是我們將要**載入圖像以進行 OCR**的檔案。 |
| 有效的 Aspose OCR 授權（可選） | 若未取得授權，輸出會有浮水印，但程式碼仍可正常執行。 |

都準備好了嗎？太好了——讓我們開始吧。

## 步驟 1：將 Aspose OCR 加入您的專案

### Maven

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- latest as of Feb 2026 -->
</dependency>
```

### Gradle

```groovy
// build.gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **專業提示：** Aspose OCR 支援超過 30 種語言套件，且可在不將整個檔案載入記憶體的情況下處理最高 10 000 × 10 000 像素的圖像，讓您能有效處理高解析度掃描。

加入相依性是**如何使用 Aspose**的第一個具體步驟——此函式庫提供我們稍後需要的 `OcrEngine`、`OcrInput` 與 `OcrResult` 類別。

## 步驟 2：初始化 OCR 引擎

`OcrEngine` 類別是 Aspose OCR 的核心元件，負責執行辨識程序。

```java
import com.aspose.ocr.*;

public class MultiLangOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create the OCR engine – the core object that does all the heavy lifting.
        OcrEngine engine = new OcrEngine();

        // Step 2.2: (Optional) Apply your license to avoid watermarks.
        // engine.setLicense("Aspose.Total.lic");
```

**為何重要：**  
如果省略引擎初始化，之後就無法*對圖像執行 OCR*，且會拋出 `NullPointerException`。

## 步驟 3：設定多語言支援與自動偵測

`OcrEngine` 提供 `setRecognitionLanguages` 方法以指定要載入的語言模型，`setAutoDetectLanguage` 則啟用每個文字區塊的自動語言偵測。

```java
        // Step 3.1: Tell the engine which languages you expect.
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });

        // Step 3.2: Enable automatic language detection – crucial for mixed‑script images.
        engine.setAutoDetectLanguage(true);
```

**說明：**  
- `"en"` = 英文，`"uk"` = 烏克蘭語，`"ar"` = 阿拉伯語。  
- 自動偵測讓 Aspose 掃描圖像，判斷每個片段屬於哪種語言，並套用正確的 OCR 模型。若未啟用，您必須分別執行三次辨識——既繁瑣又易出錯。

## 步驟 4：載入圖像以進行 OCR

`OcrInput` 是 Aspose OCR 的容器，可容納一個或多個圖像串流以供處理。

```java
        // Step 4.1: Prepare an OcrInput container.
        OcrInput input = new OcrInput();

        // Step 4.2: Add the image file. Replace the path with your actual location.
        input.add("YOUR_DIRECTORY/mixed_script.jpg");
```

> **為何使用 `OcrInput`：** 它可以容納多頁或多張圖像，讓您日後能以批次模式**載入圖像以進行 OCR**。若檔案未找到，Aspose 會拋出 `FileNotFoundException`。使用快速檢查 (`if (!new File(path).exists())`) 可節省除錯時間。

## 步驟 5：對圖像執行 OCR

`recognize` 方法會分析圖片、偵測語言區塊，並產生包含已辨識文字的 `OcrResult` 物件。

```java
        // Step 5.1: Execute the recognition process.
        OcrResult result = engine.recognize(input);
```

## 步驟 6：從圖像提取文字並顯示

`OcrResult` 包含最終的文字輸出，包含換行與信心分數。

```java
        // Step 6.1: Pull the plain text out of the result.
        String extractedText = result.getText();

        // Step 6.2: Print it to the console – you could also write it to a file.
        System.out.println("=== Extracted Text ===");
        System.out.println(extractedText);
    }
}
```

**您將看到：**  
如果 `mixed_script.jpg` 包含 “Hello мир مرحبا”，控制台輸出將會是：

```
=== Extracted Text ===
Hello мир مرحبا
```

這就是使用 **Aspose** 以多語言**從圖像提取文字**的完整解決方案。

## 邊緣情況與常見問題

### 如果語言未被辨識該怎麼辦？

Aspose 只支援其提供 OCR 模型的語言。若要加入日語，請在 `setRecognitionLanguages` 中加入 `"ja"`。若模型不存在，引擎會退回預設（英文），導致字元亂碼。

### 如何提升低解析度圖像的辨識精度？

`setResolution` 設定引擎對輸入圖像假設的 DPI 值，有助於低解析度掃描。  
`setPreprocessOptions` 選擇 OCR 前的前處理動作，例如自動旋轉。

- 前處理圖像（提升 DPI、套用二值化）。  
- 使用 `engine.setResolution(300)` 告訴引擎預期的 DPI。  
- 啟用 `engine.setPreprocessOptions(OcrEngine.PreprocessOptions.AutoRotate)` 以處理旋轉的掃描。

### 我可以一次處理資料夾內的多張圖像嗎？

當然可以。將 `input.add()` 包在迴圈中，遍歷目錄內所有檔案。相同的 `engine.recognize(input)` 呼叫會回傳每頁合併的文字。

## 完整可執行範例（直接複製貼上）

```java
import com.aspose.ocr.*;

public class MultiLangOcrDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Optional: apply your license to avoid watermarks
        // engine.setLicense("Aspose.Total.lic");

        // Configure languages (English, Ukrainian, Arabic) and enable auto‑detect
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });
        engine.setAutoDetectLanguage(true);

        // Load the image that contains mixed‑language text
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/mixed_script.jpg"); // <-- replace with your path

        // Run the recognition process
        OcrResult result = engine.recognize(input);

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

將此檔案儲存為 `MultiLangOcrDemo.java`，使用 `javac` 編譯，然後執行 `java MultiLangOcrDemo`。若環境設定正確，您將在控制台看到辨識出的文字。

## 常見問答

**Q: 每個語言套件需要單獨的授權嗎？**  
A: 不需要，單一的 Aspose OCR 授權即可涵蓋所有內建語言套件。

**Q: 加入 `OcrInput` 的圖像數量有上限嗎？**  
A: 唯一實際的限制是記憶體；Aspose 會依序處理每張圖像，因此可加入數百個檔案而不會有問題。

**Q: 自動偵測如何處理同一行內的混合文字？**  
A: 引擎會獨立分析每個文字區塊，因而能在同一行中切換語言，仍能產生正確結果。

**Q: 能取得每個辨識單字的信心分數嗎？**  
A: 可以，`OcrResult` 提供 `getConfidence()` 方法以取得細部品質指標。

**Q: 支援哪些 Java 版本？**  
A: Aspose OCR 支援 Java 8 至 Java 21，包括 LTS 版本。

## 結論

我們已完整說明**如何使用 Aspose**：從加入函式庫、設定*多語言 OCR*，到**載入圖像以進行 OCR**、**對圖像執行 OCR**，最後**從圖像提取文字**。此方法具備可擴充性——只需加入更多語言代碼或提供檔案清單，即可在數分鐘內建立穩健的 OCR 流程。

接下來可以嘗試以下想法：

- **批次處理：** 迴圈遍歷目錄，將每個結果寫入獨立的 `.txt` 檔案。  
- **後處理：** 使用正規表達式或 NLP 函式庫清理輸出（移除多餘換行、修正常見 OCR 錯誤）。  
- **整合：** 透過 Spring Boot REST 端點公開 OCR 步驟，讓其他服務能上傳圖像並取得 JSON 編碼的文字。

歡迎自行實驗、嘗試、再修正——這才是真正精通 Aspose OCR 的方式。若遇到任何問題，請在下方留言。祝開發愉快！

---

![展示 Java 程式碼的 Aspose OCR 使用範例](/images/aspose-ocr-demo.png){alt="展示 Java 程式碼的 Aspose OCR 使用範例"}

[展示 Java 程式碼的 Aspose OCR 使用範例](/images/aspose-ocr-demo.png)

**最後更新：** 2026-10-24  
**測試環境：** Aspose OCR 24.11 for Java  
**作者：** Aspose

## 相關教學

- [在 Java 中逐步載入圖像以進行 OCR 的指南](/ocr/java/ocr-operations/load-image-for-ocr-in-java-step-by-step-guide/)
- [在 Java OCR 中自動語言偵測的逐步指南](/ocr/java/advanced-ocr-techniques/automatic-language-detection-in-java-ocr-step-by-step-guide/)
- [在 Java 中啟用 GPU 以進行 OCR 並提取圖像文字的指南](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}