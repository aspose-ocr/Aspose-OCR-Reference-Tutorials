---
category: general
date: 2026-05-06
description: 如何在 Java 中使用 Aspose OCR 從圖像中識別文字、啟用自動語言偵測並提升 OCR 速度。
draft: false
keywords:
- how to use aspose
- recognize text from image
- improve ocr speed
- load image for ocr
- enable automatic language detection
language: zh-hant
og_description: 如何使用 Aspose OCR 快速辨識圖像文字、啟用自動語言偵測，並在 Java 中提升 OCR 速度。
og_title: 如何使用 Aspose OCR 處理混合語言圖像
tags:
- Aspose
- OCR
- Java
- Image Processing
title: 如何使用 Aspose OCR 處理混合語言圖像
url: /zh-hant/java/advanced-ocr-techniques/how-to-use-aspose-ocr-for-mixed-language-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR 處理混合語言圖像

有沒有想過 **如何使用 Aspose** 從同時包含多種語言的圖片中擷取文字？你並不孤單——開發者在面對同時混合英文、俄文、印地文或其他文字的圖像時，常常會卡關。好消息是 Aspose OCR 能夠優雅地處理這種情況，甚至可以透過縮小語言集合來更快地 **recognize text from image**。

在本教學中，我們將逐步說明一個完整、可直接執行的 Java 範例，該範例會 **loads image for OCR**、開啟 **automatic language detection**，並展示一個簡單的技巧來 **improve OCR speed**。完成後，你將擁有一個獨立的程式，能將擷取的文字印在主控台上，並了解每個設定的意義。

> **先決條件** – 已安裝 Java 17+、用於相依管理的 Maven 或 Gradle，以及 Aspose OCR 授權（免費試用版可用於評估）。不需要其他函式庫。

---

## 步驟 1 – 將 Aspose OCR 加入專案

在能 **use Aspose** 之前，你必須將此函式庫加入 classpath。使用 Maven 時可如下設定：

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

如果你偏好使用 Gradle：

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **專業提示**：請使用最新的穩定版；較新的版本通常包含效能提升，直接影響 **improve OCR speed**。

---

## 步驟 2 – 建立 OCR Engine 實例  

每個 Aspose OCR 工作流程的核心是 `OcrEngine`。建立它相當簡單，但值得留意的是引擎會保留內部快取。於多張圖片間重複使用同一個實例其實可以 **improve OCR speed**，因為函式庫避免了重複的原生初始化。

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise the OCR engine – one instance per application is ideal
        OcrEngine ocrEngine = new OcrEngine();
```

---

## 步驟 3 – **Load Image for OCR**  

Aspose 支援多種影像格式（PNG、JPEG、TIFF、BMP）。此處示範載入一張包含英文、俄文與印地文的 PNG。`ImageStream.fromFile` 輔助方法抽象化檔案 I/O 細節，確保影像正確串流至引擎。

```java
        // Step 3: Load the picture that holds mixed languages
        // Replace the path with the actual location of your image file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));
```

> **如果影像在記憶體中呢？** 可改用 `ImageStream.fromByteArray(byte[])`——非常適合接收位元組串流的 Web 服務。

---

## 步驟 4 – 啟用自動語言偵測  

預設情況下，Aspose OCR 會假設只有單一語言，這在多語言圖片上會導致文字亂碼。開啟自動偵測後，引擎會在辨識前先偵測每個文字區塊的文字腳本。

```java
        // Step 4: Turn on auto‑detect – this is the key to handling mixed‑language images
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

---

## 步驟 5 – 透過限制語言池 **Improve OCR Speed**  

完整的自動偵測會掃描 Aspose 支援的所有語言（超過 70 種）。若事先知道可能的語言，可提供引擎提示。傳入較小的陣列會減少搜尋範圍，從而 **improves OCR speed**。

```java
        // Step 5 (optional but recommended): Limit detection to known languages
        // "en" = English, "ru" = Russian, "hi" = Hindi
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });
```

> **為什麼這樣有幫助？** 引擎會跳過不需要的語言模型，節省 CPU 時間與記憶體。若之後新增語言，只需更新陣列即可——不必重寫程式碼。

---

## 步驟 6 – 執行辨識並 **Recognize Text from Image**  

現在開始進行繁重的辨識工作。`recognize()` 會回傳一個 `OcrResult` 物件，內含純文字、信心分數，甚至在之後需要時的版面資訊。

```java
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### 預期的主控台輸出

```
=== Extracted Text ===
Hello world!
Привет мир!
नमस्ते दुनिया!
```

若影像含有額外雜訊或傾斜文字，可能會看到這些行的信心分數較低。此時可考慮在送給 Aspose 前先對影像做前處理（去傾、二值化）。

---

## 常見問題與邊緣情況

### 如果影像非常大（例如 >10 MP）？

大型影像會佔用更多記憶體，且可能減慢處理速度。快速提升 **improve OCR speed** 的方法是將影像縮小，同時保留可讀性：

```java
// Example using java.awt for simple resizing (optional)
BufferedImage original = ImageIO.read(new File("large.png"));
int targetWidth = 2000; // adjust based on your needs
BufferedImage resized = new BufferedImage(targetWidth,
        (original.getHeight() * targetWidth) / original.getWidth(),
        BufferedImage.TYPE_INT_RGB);
Graphics2D g = resized.createGraphics();
g.drawImage(original, 0, 0, targetWidth, resized.getHeight(), null);
g.dispose();
ocrEngine.setImage(ImageStream.fromImage(resized));
```

### 如何處理從右至左的文字（例如阿拉伯文）？

Aspose OCR 會自動遵守文字方向，但你可能想在後處理時設定 `RightToLeft` 旗標：

```java
ocrEngine.getSettings().setRightToLeft(true);
```

### 我可以從 PDF 而非影像中擷取文字嗎？

可以——先將每頁 PDF 轉為影像（使用 Aspose PDF 或任何光柵化工具），再將結果送入相同的 OCR 流程。相同的 **recognize text from image** 邏輯同樣適用。

---

## 完整可執行範例（可直接複製貼上）

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates how to use Aspose OCR to recognize text from an image
 * that contains multiple languages, with automatic language detection
 * and a speed‑optimising language whitelist.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine – reuse this instance for many images
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that holds mixed languages (replace with your path)
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));

        // Enable automatic detection of language per text block
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // OPTIONAL: Restrict detection to English, Russian, and Hindi to boost speed
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });

        // Run OCR and capture the result
        OcrResult ocrResult = ocrEngine.recognize();

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

將檔案儲存為 `MixedLanguageDemo.java`，使用 `javac` 編譯，並以 `java MixedLanguageDemo` 執行。若環境設定正確，將會在主控台看到多語言文字。

---

## 結論

現在你已了解 **how to use Aspose** 來 **recognize text from image** 包含多種語言的檔案，如何 **enable automatic language detection**，以及透過限制語言池來 **improve OCR speed** 的實用技巧。上方完整程式碼已可直接複製貼上，說明亦能讓你有信心調整此解決方案——無論是要從串流、位元組陣列，甚至是網路攝影機快照 **load image for OCR**。

接下來的步驟？可以嘗試以下實驗：

* 加入影像前處理（去噪、二值化）以應對低品質掃描。  
* 將 `OcrResult` 匯出為 JSON 供下游服務使用。  
* 將引擎整合至 Spring Boot REST 端點，讓客戶端上傳影像並即時取得擷取文字。

祝開發順利，願你的 OCR 流程快速、精確且支援多語言！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}