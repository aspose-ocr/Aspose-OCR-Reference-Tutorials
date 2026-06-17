---
category: general
date: 2026-02-17
description: 學習如何在 Java 中使用 OCR 從圖像檔案識別文字、從 PNG 收據提取文字，並使用 Aspose OCR 將收據轉換為 JSON。
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: zh-hant
og_description: 一步一步的指南，教你如何在 Java 中使用 OCR 辨識圖像文字、從 PNG 收據中提取文字，並將收據轉換為 JSON。
og_title: 在 Java 中使用 OCR 的方法 – 從圖像辨識文字
tags:
- OCR
- Java
- Aspose
- Image Processing
title: 如何在 Java 中使用 OCR – 快速辨識圖像文字
url: /zh-hant/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

Kong) uses Traditional characters, possibly with some Cantonese style but standard Traditional Chinese is fine.

Let's translate.

Also note: "Pro tip:" -> "專業提示：" maybe.

"Expected Output" -> "預期輸出".

"Common Questions and Edge Cases" -> "常見問題與邊緣情況".

"Pro Tips for Production‑Ready OCR" -> "生產環境 OCR 的專業提示".

"Conclusion" -> "結論".

Make sure to keep code block placeholders unchanged.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 OCR – 快速辨識影像文字

有沒有想過 **如何使用 OCR** 從收據照片中抽取文字？也許你已經試過一些線上工具，卻只得到亂碼或是無法解析的格式。好消息是，只要幾行 Java 程式碼，你就能 **辨識影像中的文字**、**從 PNG 收據抽取文字**，甚至 **將收據轉換為 JSON** 供後續處理。

在本教學中，我們將一步步走過完整流程——從取得 Aspose OCR 函式庫授權，到產生可直接寫入資料庫或機器學習模型的乾淨 JSON 資料。沒有多餘的說明，只有可直接複製貼上到 IDE 的實作範例。完成後，你將擁有一個獨立程式，能將 `receipt.png` 轉換成可直接使用的 JSON 字串。

## 需要的環境

- **Java Development Kit (JDK) 8+** – 任意較新的版本皆可。
- **Aspose OCR for Java** 函式庫（Maven 套件為 `com.aspose:aspose-ocr`）。
- 一個 **有效的 Aspose OCR 授權檔**（`Aspose.OCR.lic`）。免費試用版可用於測試，但正式授權可移除評估限制。
- 一張包含欲辨識文字的影像檔（PNG、JPEG 等），假設檔名為 `receipt.png`，並放置於已知資料夾。
- 你慣用的 IDE（IntelliJ IDEA、Eclipse、VS Code…）——自行選擇即可。

> **專業提示：** 請將授權檔放在來源碼資料夾之外，並以絕對或相對路徑引用，避免將授權檔提交至版本控制系統。

前置條件說明完畢，接下來直接進入程式碼實作。

## 如何使用 OCR – 核心步驟

以下是我們將執行的高階步驟概覽：

1. **載入 Aspose OCR 函式庫** 並套用授權。  
2. **建立 `OcrEngine` 實例** ─ 這是執行 OCR 的核心引擎。  
3. **建立指向欲處理影像的 `OcrInput` 物件**。  
4. **以 `ResultFormat.JSON` 呼叫 `recognize`**，取得抽取文字的 JSON 表示。  
5. **處理 JSON 輸出** ─ 列印、寫入檔案，或進一步解析。

每個步驟的詳細說明會在以下章節中展開。

## 步驟 1 – 安裝 Aspose OCR 並套用授權

若使用 Maven，先在 `pom.xml` 中加入 Aspose OCR 相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

接著在 Java 程式碼中載入授權檔。此步驟必不可少，未授權時函式庫會以評估模式執行，且可能在輸出中加入浮水印。

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **為什麼重要：** `License` 物件告訴 OCR 引擎你已取得完整功能授權，包含高精度辨識與 JSON 匯出。若省略此步驟仍能 **辨識影像中的文字**，但結果可能受到限制。

## 步驟 2 – 建立 OCR 引擎實例

`OcrEngine` 類別是所有 OCR 操作的入口點。它就像「大腦」一樣，負責讀取像素並判斷對應的字元。

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

之後你可以自行客製化引擎（例如設定語言、啟用去斜）以因應收據使用非拉丁文字或掃描角度偏斜的情況。對於大多數美國收據，預設值已足夠。

## 步驟 3 – 載入欲處理的影像

現在把 OCR 引擎指向保存收據的檔案。`OcrInput` 類別可以接受多張影像，但本教學僅示範單一 PNG。

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

若需要批次 **從 PNG 抽取文字**，只要重複呼叫 `input.add()` 或傳入檔案路徑清單即可。

## 步驟 4 – 辨識文字並將收據轉換為 JSON

以下程式碼是本教學的核心。我們要求引擎辨識文字，並以 JSON 格式回傳結果。`ResultFormat.JSON` 旗標會自動完成所有轉換工作。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

JSON 內容包含每一行的文字、邊界框、信心分數以及原始文字。這樣的結構讓 **將收據轉換為 JSON** 變得非常簡單，之後即可送入任何下游 API。

## 步驟 5 – 整合程式並執行

以下是完整、可直接執行的 Java 類別，將前面的步驟串起來。將檔案存為 `JsonExportDemo.java`（或自行命名），然後在 IDE 或命令列執行。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### 預期輸出

執行程式後會印出類似下列的 JSON 字串（實際內容取決於你的收據）：

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

現在你可以把這段 JSON 輸入資料庫、REST 端點，或資料分析管線。**將收據轉換為 JSON** 的步驟已為你完成。

## 常見問題與邊緣情況

### 影像如果被旋轉該怎麼辦？

Aspose OCR 會自動偵測並校正輕微的旋轉。若影像嚴重傾斜，可在辨識前呼叫 `engine.getImagePreprocessingOptions().setDeskew(true)`。

### 如何處理多語言？

使用 `engine.getLanguage()` 設定目標語言，例如 `engine.setLanguage(Language.FRENCH)`。當收據包含多語言文字時，這對 **辨識影像中的文字** 特別有用。

### 能否輸出純文字而非 JSON？

當然可以。將 `ResultFormat.JSON` 改為 `ResultFormat.TEXT`，然後呼叫 `result.getText()` 即可。

### 能否限制 OCR 只辨識特定區域？

可以──使用 `ocrInput.add(imagePath, new Rectangle(x, y, width, height))` 只聚焦於收據區域，這樣可提升速度與準確度。

## 生產環境 OCR 的專業提示

- **快取 License 物件**：若在迴圈中處理大量檔案，重複建立 License 會增加開銷。
- **批次處理**：將所有收據路徑加入同一個 `OcrInput`，一次呼叫 `recognize`。JSON 會包含每頁的陣列。
- **驗證 JSON**：取得字串後，使用 Jackson 等函式庫解析，確保格式正確再寫入。
- **監控信心分數**：JSON 中的 `confidence` 欄位可用來過濾低於門檻（例如 0.85）的行，避免雜訊資料。
- **保護授權檔**：將 `Aspose.OCR.lic` 存放於安全金庫或環境變數，特別是在雲端部署時。

## 結論

我們已說明 **如何在 Java 中使用 OCR** 來 **辨識影像中的文字**、**從 PNG 收據抽取文字**，以及 **將收據轉換為 JSON**，全部透過簡潔的端到端範例。步驟清晰、程式可直接執行，且 JSON 輸出提供結構化資料，方便任何下游系統使用。

接下來，你可以探索更進階的情境：將 JSON 丟入 Apache Kafka 進行即時處理、使用正規表達式抽取項目金額，或整合雲端 OCR 服務以提升可擴充性。無論選擇哪條路，今天學到的基礎都將是堅實的根基。

有任何問題，或在實作過程中遇到卡關，歡迎在下方留言，我們一起排除故障。祝開發順利，玩得開心，將雜亂的收據影像轉變為乾淨、可搜尋的資料吧！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}