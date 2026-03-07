---
category: general
date: 2026-03-07
description: 使用 Java OCR 從圖像提取文字。了解如何載入圖像進行 OCR、設定語言，並在數分鐘內完成完整的 Java OCR 教學。
draft: false
keywords:
- extract text from image
- load image for ocr
- use OCR in java
- java ocr tutorial
language: zh-hant
og_description: 使用 Java OCR 從圖像中提取文字。本教學示範如何載入圖像進行 OCR、設定語言，並一步一步執行 Java OCR 教程。
og_title: 在 Java 中從圖像提取文字 – 完整 OCR 指南
tags:
- OCR
- Java
- Image Processing
title: 在 Java 中從圖像提取文字 – Java OCR 教學
url: /zh-hant/java/ocr-basics/extract-text-from-image-in-java-java-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字（Java） – 完整 OCR 指南

曾經需要**從圖像中提取文字**卻不知從何開始於 Java 嗎？你並非唯一遇到此問題的人——開發者在將掃描的標誌、收據或手寫筆記轉換為可搜尋的字串時，常常會卡在這裡。  

好消息是？只要幾分鐘，你就能擁有一個可運作的 OCR 流程，能讀取卡納達文、英文或任何支援的語言。在本教學中，我們將**載入圖像以供 OCR**、設定引擎，並逐步說明一個**Java OCR 教學**，讓你可以直接複製貼上並立即執行。

## 本指南涵蓋內容

我們會先列出所需工具，然後直接進入**逐步**實作。完成後你將能夠：

* 將圖像檔載入 Java 的 `ImageInputStream`。
* 設定 OCR 引擎以辨識特定語言（本例為卡納達文）。
* 執行辨識程序並印出提取出的文字。
* 調整設定以提升準確度，並處理常見的陷阱。

不需要額外文件——所有資訊都在此。  

**先決條件**：Java 17 或更新版本、Maven 或 Gradle 等建置工具，以及提供 `OcrEngine` 類別的 OCR 函式庫（例如假想的 *SimpleOCR* SDK）。若使用 Maven，請於稍後加入相應的相依性。

---

## Step 1 – 設定專案並加入 OCR 函式庫

在撰寫任何程式碼之前，先確保專案能看到 OCR 類別。使用 Maven 時，將以下片段放入 `pom.xml`：

```xml
<!-- Maven dependency for SimpleOCR (replace with your actual OCR SDK) -->
<dependency>
    <groupId>com.example</groupId>
    <artifactId>simple-ocr</artifactId>
    <version>1.4.2</version>
</dependency>
```

如果你偏好 Gradle，等價的寫法是：

```gradle
implementation 'com.example:simple-ocr:1.4.2'
```

> **專業提示：** 保持函式庫版本為最新；較新的發行版通常會包含語言模型的改進，提升辨識準確度。

相依性解決後，重新整理 IDE，即可開始編寫程式。

## Step 2 – 匯入必要類別

以下是範例所需的完整匯入清單。為了讓你清楚每個類別的用途，我們盡量保持最小化。

```java
import com.example.ocr.OcrEngine;      // Main OCR engine
import com.example.ocr.OcrResult;      // Holds recognition result
import com.example.io.ImageInputStream; // Wrapper for image files
import java.nio.file.Paths;             // Convenient path handling
import java.io.IOException;             // For proper exception handling
```

> **為什麼需要這些匯入？** `OcrEngine` 與 `OcrResult` 是 OCR 流程的核心，`ImageInputStream` 則抽象化檔案讀取的雜務。使用 `java.nio.file.Paths` 讓程式碼與作業系統無關。

## Step 3 – 載入圖像以供 OCR

接下來是常讓人卡住的部份：將正確的圖像格式傳給引擎。OCR SDK 需要一個 `ImageInputStream`，你可以從磁碟上的任何檔案取得。

```java
// Step 3: Load the image that contains the text you want to extract
String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));
```

> **邊緣情況：** 若圖像損毀或為不支援的格式（例如 GIF），建構子會拋出 `IOException`。請將呼叫包在 try‑catch 中，或事先驗證檔案。

## Step 4 – 設定引擎以辨識特定語言

大多數 OCR 引擎皆支援多語言。為提升準確度，應明確告訴引擎要辨識哪種語言。本例使用語言代碼 `"kn"` 代表卡納達文。

```java
// Step 4: Create and configure the OCR engine for Kannada
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setLanguage("kn"); // 'kn' = Kannada
```

> **為什麼要設定語言？** 限制字元集可減少偽陽性，尤其在面對許多相似字形的文字時更為重要。

若日後需要切換語言，只要更改代碼字串——不必修改其他程式碼。

## Step 5 – 執行 OCR 程序並提取文字

圖像已載入且引擎已設定好後，辨識只需一次方法呼叫。結果物件會回傳純文字，並可選擇提供信心分數。

```java
// Step 5: Run OCR and retrieve the recognized text
OcrResult ocrResult = ocrEngine.recognize(imageStream);
String extractedText = ocrResult.getText();
```

> **常見問題：** *如果 OCR 回傳空字串怎麼辦？*  
> 通常表示圖像品質太差（模糊、對比低）或語言設定不正確。請嘗試前置處理圖像（提升對比、二值化）或再次確認語言代碼。

## Step 6 – 顯示結果

最後，將輸出印到主控台。實際應用中，你可能會把結果寫入資料庫或送入搜尋索引。

```java
// Step 6: Output the recognized Kannada text
System.out.println("Extracted text:");
System.out.println(extractedText);
```

### 預期輸出

若來源圖像包含卡納達文詞句 “ಕರ್ನಾಟಕ” （Karnataka），主控台應顯示：

```
Extracted text:
ಕರ್ನಾಟಕ
```

這樣就完成了一個完整的 **在 Java 中使用 OCR** 工作流程，你可以依需求套用到任何語言或圖像來源。

---

## Full Working Example

以下是完整程式碼，已可直接編譯。請將 `YOUR_DIRECTORY` 替換為實際的圖像檔案路徑。

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.nio.file.Paths;
import java.io.IOException;

public class KannadaOcrExample {
    public static void main(String[] args) {
        try {
            // Create OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Configure for Kannada (language code "kn")
            ocrEngine.getConfig().setLanguage("kn");

            // Load the image you want to extract text from
            String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
            ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));

            // Run the OCR process
            OcrResult ocrResult = ocrEngine.recognize(imageStream);

            // Print the extracted text
            System.out.println("Extracted text:");
            System.out.println(ocrResult.getText());
        } catch (IOException e) {
            System.err.println("Failed to load image or run OCR: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error during OCR: " + e.getMessage());
        }
    }
}
```

> **小技巧：** 於正式環境建議重複使用同一個 `OcrEngine` 實例來處理多張圖像，避免頻繁建立造成效能負擔。

---

## Frequently Asked Questions & Edge Cases

### 如何提升噪點照片的辨識準確度？
- **前置處理** 圖像：轉為灰階、套用中值濾波或提升對比度。
- **調整尺寸** 至至少 300 DPI；大多數 OCR 引擎預設此解析度。
- **設定白名單**（whitelist）字元，若只預期輸出特定字符（例如僅數字）。

### 可以將此方法用於 PDF 嗎？
可以。先將每頁以圖像形式抽取（使用 PDFBox 或 iText），再將這些圖像送入相同的管線。程式碼保持不變，唯一改變的是圖像來源。

### 若一張圖像需要辨識多種語言該怎麼辦？
大多數 SDK 允許傳入以逗號分隔的語言清單，例如 `"en,kn"`。引擎會嘗試匹配任一提供的文字系統。

### 有辦法取得信心分數嗎？
`OcrResult` 通常提供 `getConfidence()` 方法，會回傳每行文字 0~1 之間的浮點數。可利用此分數過濾低信心的結果。

---

## Next Steps

現在你已能使用 Java **從圖像中提取文字**，可以進一步探索：

* **批次處理** – 迴圈遍歷資料夾內的圖像，將結果寫入 CSV。
* **結合 Apache Tika** – 把 OCR 與文件解析結合，建立統一的搜尋索引。
* **伺服器端 API** – 透過 REST 端點公開 OCR 邏輯（Spring Boot 可輕鬆實作）。
* **其他函式庫** – 若需要開源解決方案，可嘗試使用 `tess4j` 包裝的 Tesseract。

上述主題皆建立在本 **java ocr 教學** 的核心概念之上，歡迎自行實驗與擴充程式碼。

---

## Conclusion

我們已完整示範一個 Java 範例，**從圖像中提取文字**，說明如何**載入圖像以供 OCR**、設定語言參數，並**在 Java 中使用 OCR** 取得可讀的字串。程式碼自包含、錯誤處理完善，且可輕鬆嵌入任何 Java 專案。  

快試試看，調整語言代碼，讓你能毫不費力地將掃描文件轉換為可搜尋的資料。祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}