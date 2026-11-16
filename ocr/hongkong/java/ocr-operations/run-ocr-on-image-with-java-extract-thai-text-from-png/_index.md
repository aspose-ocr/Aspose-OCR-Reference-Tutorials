---
category: general
date: 2026-03-28
description: 在 Java 中使用 Aspose OCR 執行圖像 OCR，將圖像轉換為文字，快速且可靠地從 PNG 中提取泰文。
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: zh-hant
og_description: 使用 Java 與 Aspose OCR 進行圖片文字辨識。了解如何將圖片轉換為文字、從 PNG 中擷取泰文，以及處理常見問題。
og_title: 使用 Java 在圖像上執行 OCR – 快速擷取泰文文字
tags:
- OCR
- Java
- Aspose
- Image Processing
title: 使用 Java 在圖片上執行 OCR – 從 PNG 提取泰文文字
url: /zh-hant/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中執行影像 OCR – 完整功能教學

有沒有想過如何直接在 Java 程式碼中 **run OCR on image** 檔案？或許你手頭有一堆泰文收據、掃描文件或螢幕截圖，需要將文字提取出來而不必手動輸入。這是常見的痛點，尤其當來源是 PNG 且語言為非拉丁文字時。

在本教學中，我們將示範如何使用 Aspose OCR 函式庫 **run OCR on image**，將圖片轉換為純文字，並可靠地抽取泰文字元。完成後，你將能夠 **convert image to text**、**extract text from PNG**，甚至只需幾行程式碼即可 **recognize Thai text**。

## 本教學涵蓋內容

* 在 Maven/Gradle 專案中設定 Aspose OCR 相依性。  
* 初始化 `OcrEngine` 並將其設定為泰文。  
* 對 PNG 檔案執行 OCR 並處理可能的錯誤。  
* 將結果輸出至主控台並驗證輸出內容。  

不需要任何 Aspose 的先前經驗——只要有基本的 Java IDE 與想要處理的影像檔案即可。

## 前置條件

* 已安裝 Java 8 或更新版本（此函式庫亦支援 Java 11+）。  
* 建置工具 – Maven 或 Gradle（我們將示範 Maven 片段）。  
* Aspose OCR 授權（免費試用可用於測試，但授權可移除評估限制）。  
* 含有泰文的 PNG，例如 `input.png`，放置於專案的 resources 資料夾中。

---

## 第一步：將 Aspose OCR 加入您的專案

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Pro tip:** Keep the library version in sync with the official Aspose release notes; newer versions add language packs and performance tweaks.

一旦相依性解決，IDE 應會自動匯入所需的類別。

## 第二步：初始化 OCR 引擎

引擎是整個流程的核心——可視為分析像素模式的「大腦」。我們同時會告訴它只關注泰文字元。

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

為什麼要明確設定語言？因為指定 `"th"` 會縮小字元集，從而加快辨識速度並減少相似字形的誤讀。

## 第三步：對 PNG 檔案執行 OCR

現在我們將想要解碼的影像提供給引擎。`recognizeImage` 方法會回傳一個 `OcrResult` 物件，內含抽取出的字串與信心分數。

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

如果找不到檔案，Aspose 會拋出 `FileNotFoundException`。在正式程式碼中建議使用 `try‑catch` 包裹此呼叫，但本教學為了簡潔直接使用。

## 第四步：輸出辨識文字

最後，我們將結果印出。`getText()` 方法回傳純 Java `String`，你可以將其儲存、傳送至網路或寫入檔案。

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

執行程式時，應會看到類似以下的輸出：

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

如果輸出呈現亂碼，請再次確認來源 PNG 為高解析度（至少 300 dpi），且語言代碼 `"th"` 與目標語言相符。

### 完整程式碼

以下是完整、可直接執行的 Java 檔案。將其貼到 IDE 中，必要時替換影像路徑，然後點擊 **Run**。

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![執行影像 OCR 範例](image.png "執行影像 OCR 範例 – Java 程式碼從 PNG 提取泰文文字")

## 第五步：常見變形與邊緣情況

### 轉換其他格式的影像為文字

如果需要 **convert image to text** 的檔案是 JPEG 或 BMP，只要在 `imagePath` 中更改副檔名即可。Aspose OCR 支援 PNG、JPEG、BMP、TIFF，甚至 PDF 頁面。

### 從 PNG 提取多語言文字

你可以讓引擎同時偵測多種語言：

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

結果會同時包含泰文與英文字元，對於雙語收據相當實用。

### 處理低品質影像

對於模糊的掃描，建議啟用前處理：

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

此設定會觸發內建的去雜訊與對比度增強演算法，提升 **extract text from PNG** 步驟的效果。

### 授權啟用

若未授權，Aspose 會在第 100 頁之後的輸出中插入浮水印行。請盡早啟用授權：

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

將 `.lic` 檔案放在 JAR 旁邊，或以絕對路徑引用。

## 常見問題

**Q: Does this work on Linux?**  
A: Absolutely. Aspose OCR is pure Java, so any JVM‑compatible OS is fine.

**Q: What if the PNG contains handwritten Thai?**  
A: Handwriting recognition is limited; you may need a dedicated neural‑network model. Aspose OCR excels with printed text.

**Q: Can I batch‑process a folder of images?**  
A: Wrap the `recognizeImage` call in a loop over `Files.list(Paths.get("folder"))`. Remember to reuse the same `OcrEngine` instance for performance.

## 結論

我們已完整示範如何在 Java 中 **run OCR on image**，特別是從 PNG 抽取 **extract Thai text**。透過初始化 `OcrEngine`、設定語言、呼叫 `recognizeImage`，再將結果印出，你現在擁有一套可靠的 **convert image to text** 解決方案，無需依賴第三方服務。

從此你可以：

* **extract text from PNG** 檔案批次處理，以支援資料挖掘專案。  
* 結合 OCR 輸出與翻譯 API，取得英文對應。  
* 透過更換語言代碼，探索 Aspose 支援的其他語言，如中文或阿拉伯文。

不妨使用自己的影像試試看——調整前處理設定、測試不同檔案格式，感受此方案在實務工作流中的穩健表現。

祝程式開發順利，願你的 OCR 流程永遠精準！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}