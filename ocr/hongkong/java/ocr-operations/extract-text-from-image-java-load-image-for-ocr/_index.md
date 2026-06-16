---
category: general
date: 2026-04-29
description: 使用 Aspose OCR 的 Java 從圖像提取文字 – 學習如何載入圖像進行 OCR，並以 JSON 格式辨識收據文字。
draft: false
keywords:
- extract text from image java
- load image for OCR
- recognize text from receipt
- Aspose OCR Java
- JSON OCR result
language: zh-hant
og_description: 使用 Aspose OCR 在 Java 中從圖像提取文字。本教程展示如何載入圖像進行 OCR，並從收據中識別文字，輸出為 JSON。
og_title: 從圖片中提取文字（Java）– 完整指南
tags:
- Java
- OCR
- Aspose
title: 從圖像提取文字 Java – 載入圖像以作 OCR
url: /zh-hant/java/ocr-operations/extract-text-from-image-java-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從影像中提取文字（Java） – 完整指南

是否曾經需要 **extract text from image java**，卻不確定該選擇哪個函式庫？你並不孤單。許多開發者在嘗試 **load image for OCR** 時卡住，然後得到難以處理的原始文字格式。  

在本教學中，我們將逐步說明一個乾淨、端對端的解決方案，不僅能 **load image for OCR**，還能 **recognize text from receipt**，並輸出整齊的 JSON 字串。完成後，你將擁有一個可直接執行的 Java 類別，隨時可放入任何專案——無需額外調整。

## 你將學到

- 如何為 Java 設定 Aspose OCR（讓繁重工作變得輕鬆的函式庫）。  
- 從磁碟載入影像以進行 OCR 的完整步驟 **load image for OCR**。  
- 如何設定引擎以 JSON 格式返回結果，這對後續處理非常理想。  
- 如何 **recognize text from receipt** 圖片並驗證輸出。  

不需要任何 Aspose 的先前經驗；只要有可運作的 JDK 以及你熟悉的 IDE 即可。

## 前置條件

| Requirement | 為何重要 |
|-------------|----------|
| **Java 17+** (or any recent JDK) | Aspose OCR 隨附適用於現代 Java 執行環境的已編譯二進位檔。 |
| **Maven or Gradle** (to pull the Aspose OCR dependency) | 讓相依管理變得輕鬆。 |
| **A sample receipt image** (e.g., `receipt.png`) | 我們將使用此檔案示範 **recognize text from receipt**。 |
| **Internet connection** (once) | 首次需要下載 Aspose JAR 時使用。 |

如果你已具備上述條件，太好了——讓我們開始吧。

## 步驟 1：將 Aspose OCR 加入專案

首先需要的是 Aspose OCR 函式庫。如果你使用 Maven，請將以下程式碼片段加入你的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

若使用 Gradle，則如下所示：

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **專業提示：** 鎖定版本號。之後升級可能會帶來細微的 API 變更，導致程式碼失效。

相依解決後，你就可以撰寫實際執行 **extract text from image java** 的 Java 程式碼了。

## 步驟 2：載入影像以進行 OCR

現在我們展示執行 **load image for OCR** 的精確程式碼行。Aspose 提供了便利的 `ImageStream.fromFile` 輔助方法。

```java
// Step 2: Load the image you want to process
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

將 `YOUR_DIRECTORY` 替換為你的收據檔案的絕對或相對路徑。若路徑錯誤，引擎會拋出 `FileNotFoundException`，請務必再次確認拼寫。

> **為何重要：** 正確載入影像是基礎。如果影像未被讀取，OCR 引擎將無法辨識，最終只會得到空的 JSON 結果。

## 步驟 3：告訴引擎回傳 JSON

Aspose OCR 可以輸出 XML、純文字或 JSON。對於現代 API 來說，JSON 最具彈性，因此我們會明確設定格式。

```java
ocrEngine.getResultSettings()
         .setResultFormat(OcrResultFormat.JSON); // XML is also available
```

如果下游系統偏好 XML，只需將 `OcrResultFormat.XML` 替換即可。此 API 設計為可互換。

## 步驟 4：執行辨識程序

影像已載入且格式已設定後，接下來的步驟是實際執行 **recognize text from receipt**。這裡就是繁重工作發生的地方。

```java
// Step 4: Perform OCR
OcrResult ocrResult = ocrEngine.recognize();
```

`recognize()` 呼叫會阻塞，直到引擎完成影像分析。對於大型影像，你可能想將其放在背景執行緒中執行，但對於一般收據而言，僅需瞬間即完成。

## 步驟 5：取得 JSON 結果

最後，我們擷取原始 JSON 字串並印出。此字串包含所有辨識出的文字、其邊界框、信心分數等資訊。

```java
// Step 5: Retrieve the JSON string
String jsonResult = ocrResult.getResultAsString();
System.out.println(jsonResult);
```

### 預期輸出

對清晰的收據執行完整程式會得到類似以下的結果：

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "rectangle": { "x": 12, "y": 15, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2026-04-28",
          "confidence": 0.95,
          "rectangle": { "x": 12, "y": 50, "width": 180, "height": 20 }
        },
        {
          "text": "Total $23.45",
          "confidence": 0.99,
          "rectangle": { "x": 12, "y": 120, "width": 150, "height": 25 }
        }
      ]
    }
  ]
}
```

請注意，收據的每一行都會成為帶有信心分數的獨立區塊。現在你可以將此 JSON 輸入任意下游系統——存入資料庫、透過 HTTP 傳送，或餵入機器學習模型。

## 完整可執行範例

以下是完整、獨立的 Java 類別，將所有步驟整合在一起。直接複製貼上，調整影像路徑，然後執行 `mvn compile exec:java`（或等效的 Gradle 指令）。

```java
import com.aspose.ocr.*;

public class JsonExportExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Make sure the path points to a real receipt image on your machine
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Configure the engine to return results in JSON format
        ocrEngine.getResultSettings()
                 .setResultFormat(OcrResultFormat.JSON); // XML is also available

        // Step 4: Run the OCR recognition process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Retrieve the raw JSON string and output it
        String jsonResult = ocrResult.getResultAsString();
        System.out.println(jsonResult);
    }
}
```

> **注意事項：**  
> • **檔案路徑錯誤** – 請再次確認 Windows 與 macOS/Linux 的斜線使用。  
> • **記憶體不足** – 大型影像可能需要 `ocrEngine.setMemoryOptimization(true)`。  
> • **語言設定** – 若收據包含非拉丁字元，請在 `recognize()` 前呼叫 `ocrEngine.setLanguage(OcrLanguage.SPANISH)`（或任何支援的語言）。

## 測試解決方案

1. **執行程式** – 你應該會在主控台看到 JSON 資料。  
2. **驗證 JSON** – 將輸出複製到 <https://jsonlint.com/> 以確保其格式正確。  
3. **解析它** – 在實際專案中，你可以使用 Jackson 或 Gson 等函式庫，將 JSON 轉換為 POJO 以便處理。

如果你遇到 `pages` 陣列為空的情況，最常見的原因是：找不到影像檔案，或影像過於模糊，無法符合引擎的預設設定。後者情況下，可嘗試提升 DPI 或在送入 Aspose 前執行前處理步驟（例如二值化）。

## 變體與邊緣案例

| Scenario | What to change |
|----------|----------------|
| **多頁**（例如將多頁 PDF 轉為影像） | 對每張影像迴圈，於迴圈內呼叫 `ocrEngine.setImage(...)`，並彙總 JSON 結果。 |
| **不同的輸出格式** | 將 `OcrResultFormat.JSON` 換成 `OcrResultFormat.XML` 或 `OcrResultFormat.PLAIN_TEXT`。 |
| **效能調校** | 使用 `ocrEngine.setRecognitionMode(OcrRecognitionMode.FAST)` 以提升速度，或 `OcrRecognitionMode.ACCURATE` 以提升品質。 |
| **非收據文件** | 若需要表格抽取，請調整 `ocrEngine.getPageSegmentationSettings().setDetectTables(true)`。 |

這些調整讓你能將核心 **extract text from image java** 流程套用到各種實務問題上。

## 結論

我們剛剛介紹了一個簡潔、可投入生產的方式，使用 Aspose OCR **extract text from image java**。遵循這五個步驟——建立引擎、**load image for OCR**、設定 JSON 輸出、**recognize text from receipt**，最後讀取 JSON，即可輕鬆將 OCR 整合至任何 Java 後端。

從這裡開始，你可能想要：

- 將 JSON 存入 NoSQL 資料庫以供日後分析。  
- 將結果傳送至聊天機器人，回答有關收據的問題。  
- 結合 Apache Tika 處理 PDF、DOCX 及其他格式。

試試看，根據你的文件調整設定，讓機器完成繁重工作，而你專注於創造價值。

---

![從影像中提取文字（Java）](placeholder-image.png "從影像中提取文字（Java）")

*圖示：OCR 流程的視覺化表示——從影像檔案到 JSON 輸出。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}