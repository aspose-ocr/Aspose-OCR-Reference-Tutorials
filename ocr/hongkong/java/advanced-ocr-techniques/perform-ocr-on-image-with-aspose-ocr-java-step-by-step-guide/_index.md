---
category: general
date: 2026-02-14
description: 學習如何在 Java 中使用 Aspose OCR 對圖像執行 OCR 並提取圖像文字。包括載入圖像進行 OCR、自訂詞典及拼寫校正。
draft: false
keywords:
- perform OCR on image
- extract text from image
- load image for OCR
- Aspose OCR Java
- spell correction OCR
language: zh-hant
og_description: 在 Java 中使用 Aspose OCR 執行圖像文字辨識。本指南說明如何載入圖像以進行 OCR、從圖像中擷取文字，以及啟用拼寫校正。
og_title: 在圖像上執行 OCR – 完整 Java 教學
tags:
- OCR
- Java
- Aspose
title: 使用 Aspose OCR 於影像執行 OCR – Java 步驟指南
url: /zh-hant/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在圖像上執行 OCR – 完整 Java 教學

有沒有曾經需要 **在圖像上執行 OCR** 檔案，但不知從何入手？你並不孤單；許多開發者在首次嘗試從圖像資料中提取文字時，都會遇到相同的困難。好消息是，使用 Aspose OCR for Java，你只需幾行程式碼即可獲得可靠的結果，而且還可以透過自訂字典與拼寫檢查提升準確度。

在本指南中，我們將逐步說明你需要了解的所有內容：從載入圖像以進行 OCR、啟用拼寫校正，到最終列印清理過的文字。完成後，你將能在自己的 Java 專案中 **在圖像上執行 OCR** 資產，並且還會看到如何 **從圖像中提取文字**，即使是雜訊較多的掃描檔也能正常運作。

## 你需要的條件

在開始之前，請確保你已準備好以下項目：

- **Java Development Kit (JDK) 8+** – 程式碼使用標準的 Java API。
- **Aspose OCR for Java** 程式庫（你可以從 Aspose 官方網站或 Maven Central 取得最新的 JAR）。
- 一個你想要處理的圖像檔案（例如 `invoice.png`）。
- (可選) 一個純文字檔 `custom_dict.txt`，內含領域特定詞彙，每行一個。

就這樣——不需要大型框架，也不需要外部服務。只要純 Java 與 Aspose OCR JAR 即可。

## 步驟 1：設定專案並匯入相依性

首先，建立一個新的 Maven（或 Gradle）專案，並加入 Aspose OCR 的相依性。如果你使用 Maven，你的 `pom.xml` 應該包含以下內容：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

如果你偏好手動下載 JAR，請將其放入 `libs` 資料夾，並加入 classpath。

> **專業提示：** 請務必在撰寫時確認版本號；較新的版本可能會加入語言套件等額外功能。

## 步驟 2：載入圖像以進行 OCR

第一個實際的程式碼步驟是將 OCR 引擎指向你想要分析的圖像。Aspose OCR 使用 `ImageStream` 包裝器，可從檔案、位元組陣列，甚至 URL 讀取。

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

請注意，我們只用單一方法呼叫就 **載入圖像以進行 OCR**——不需要繁瑣的 `BufferedImage` 操作。如果你的圖像位於 resources 中，只需將路徑替換為 `getClass().getResourceAsStream(...)`。

## 步驟 3：啟用拼寫校正（可選但強大）

Aspose OCR 能自動校正常見的 OCR 錯誤（例如 “l” 與 “1” 的混淆）。開啟此功能只需切換一個旗標即可：

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

為什麼要這麼做？想像掃描一張印刷的發票，字體很小且掃描器會產生雜點。拼寫校正通常會將 “Inv0ice” 轉回 “Invoice”，而不需要額外的手動處理。

## 步驟 4：提供自訂字典（客製化引擎）

如果你處理的是行業特定術語——例如醫療代碼、法律用語或產品 SKU——自訂字典可以大幅提升準確度。字典只是一個每行一個詞的文字檔。

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

請確保檔案使用 UTF‑8 編碼；否則非 ASCII 詞彙可能會出現亂碼。

## 步驟 5：執行 OCR 程序

現在我們終於讓引擎發揮魔力。`process()` 呼叫會回傳一個 `OcrResult` 物件，內含辨識出的文字、信心分數，甚至在之後需要時的版面配置。

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

如果你想確認引擎是否拋出例外，請將此呼叫包在 try‑catch 區塊中，並檢查 `ocrResult.getErrorMessage()` 以取得詳細資訊。

## 步驟 6：輸出辨識（且已校正）的文字

最後一步是顯示或儲存提取出的字串。為了快速示範，我們僅將其印到主控台：

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

執行程式後應會印出類似以下內容：

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

如果看到雜亂的字元，請再次檢查自訂字典，並考慮調整圖像品質（例如在送入引擎前提升對比度）。

### 完整可執行範例

將所有步驟整合起來，以下是完整且可直接執行的類別：

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

將此檔案儲存為 `SpellCorrectDemo.java`，調整路徑後，以 `javac` 編譯，並以 `java SpellCorrectDemo` 執行。現在你應該能 **在圖像上執行 OCR** 檔案，並看到提取出的文字被印出。

## 常見問題與邊緣案例

### 如果圖像是其他格式（PDF、TIFF 等）呢？

Aspose OCR 開箱即支援多種點陣圖格式。對於 PDF，你需要先將每頁提取為圖像——Aspose PDF for Java 能很好地完成此工作。只要取得 `BufferedImage` 或位元組串流，即可使用相同的 `setImage` 呼叫。

### 如何處理多頁文件？

對每頁圖像進行迴圈，執行 OCR 步驟，並將結果串接。若希望每頁都有獨立的拼寫校正上下文，請在每頁重設或重新建立 `OcrEngine`。

### 我可以限制語言或字元集嗎？

可以。使用 `ocrEngine.getEngineOptions().setLanguage(Language.English);`（或其他支援的語言）即可減少誤判並加快處理速度。

### 大批量處理的效能如何？

Aspose OCR 在唯讀操作下是執行緒安全的。你可以建立執行緒池，同時處理多張圖像——只要避免在執行緒間共享同一個 `OcrEngine` 實例即可。

## 提升準確度的技巧

- **預先處理圖像**：提升對比度、去除背景雜訊，或轉為灰階。
- **使用高解析度掃描**（300 dpi 或更高）。較低的解析度常會產生亂碼。
- **保持自訂字典精簡**：過多不相關的詞彙會干擾拼寫檢查器。
- **驗證輸出**：若你知道預期的格式（例如日期、數字），可使用正規表達式進行後處理以捕捉異常。

## 後續步驟

現在你已能使用 Aspose OCR **在圖像上執行 OCR** 檔案並 **從圖像中提取文字**，接下來可以探索以下主題：

- **將 OCR 輸出保存為 PDF**，並附加可搜尋的文字層。
- **與資料庫整合**，自動儲存提取的發票資料。
- **套用機器學習後處理**，以在手寫筆記上獲得更高的準確度。
- **在接受使用者上傳圖片的 Web 服務中使用 `load image for OCR` 旗標**。

上述主題皆建立在我們先前討論的核心步驟之上，轉換過程將相當順暢。

---

*祝開發順利！如果遇到任何問題，歡迎留言——沒有什麼比從實務案例中學習更好。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}