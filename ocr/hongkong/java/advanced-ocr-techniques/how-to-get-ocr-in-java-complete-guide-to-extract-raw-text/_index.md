---
category: general
date: 2026-05-25
description: 如何在 Java 中使用 OCR 並從圖像中提取原始文字。學習關閉拼寫校正、辨識手寫文字，以及如何高效載入圖像。
draft: false
keywords:
- how to get ocr
- extract raw text
- turn off spell correction
- recognize handwritten text
- how to load image
language: zh-hant
og_description: 如何在 Java 中使用 OCR 並從圖像中提取原始文字。本指南說明如何關閉拼寫校正、識別手寫文字，以及如何正確載入圖像。
og_title: 如何在 Java 中使用 OCR – 逐步提取原始文字
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to get OCR in Java and extract raw text from images. Learn to turn
    off spell correction, recognize handwritten text, and how to load image efficiently.
  headline: How to Get OCR in Java – Complete Guide to Extract Raw Text
  type: TechArticle
- description: How to get OCR in Java and extract raw text from images. Learn to turn
    off spell correction, recognize handwritten text, and how to load image efficiently.
  name: How to Get OCR in Java – Complete Guide to Extract Raw Text
  steps:
  - name: Maven Dependency
    text: If you’re using Maven, paste this into your `pom.xml`. It pulls the latest
      Aspose.OCR library (as of May 2026).
  - name: Gradle Alternative
    text: '```gradle implementation ''com.aspose:aspose-ocr:23.11'' ```'
  - name: Expected Output
    text: 'Assuming `handwritten.png` contains the phrase *“Hello World”* written
      in cursive, you’ll see something like:'
  type: HowTo
tags:
- OCR
- Java
- Aspose.OCR
title: 如何在 Java 中使用 OCR – 完整提取原始文字指南
url: /zh-hant/java/advanced-ocr-techniques/how-to-get-ocr-in-java-complete-guide-to-extract-raw-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中取得 OCR – 完整指南：提取原始文字

有沒有想過 **如何取得 OCR** 結果而不經過函式庫的自動清理？也許你正在處理手寫筆記，需要引擎看到的精確字元，而不是「美化」過的版本。在本教學中，我們將手把手示範，說明 **如何取得 OCR** 輸出、如何 **提取原始文字**，以及在辨識手寫文字時為何以及如何 **關閉拼寫校正**。最後，你還會了解 **如何載入影像** 檔案到 Aspose OCR 引擎，毫無障礙。

我們將使用 Aspose.OCR for Java，但這些概念同樣適用於任何提供拼寫校正切換功能的 OCR SDK。沒有繁重理論——只是一個實用、可直接複製貼上的解決方案，今天就能執行。

---

## 你將學到什麼

- 如何在 Java 專案中設定 Aspose.OCR  
- 取得 **如何取得 OCR** 原始輸出的確切步驟  
- 為何以及 **如何關閉拼寫校正** 以獲得純淨文字  
- 最佳的 **如何載入影像** 檔案方式，以獲得最佳辨識效果  
- 如何 **辨識手寫文字** 並驗證結果  

先決條件相當簡單：已安裝 Java 8 以上、支援 Maven 的 IDE（IntelliJ、Eclipse 或 VS Code），以及一張包含手寫字元的範例影像。若缺少任何項目，只需從 Oracle 下載 JDK，並從手機取得影像——沒問題。

![說明 OCR 工作流程的圖示，展示如何從影像取得 OCR 原始文字](/images/ocr-workflow.png){: .center alt="如何取得 OCR 原始文字工作流程"}

---

## 第一步：將 Aspose.OCR 加入專案

### Maven 相依性

如果你使用 Maven，請將以下內容貼入 `pom.xml`。它會取得最新的 Aspose.OCR 函式庫（截至 2026 年 5 月）。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.11</version>
</dependency>
```

> **專業提示：** 請務必檢查官方 Aspose Maven 套件庫，以取得更新的版本。`23.11` 版加入了對手寫連筆文字的更佳支援，當你 **辨識手寫文字** 時相當方便。

### Gradle 替代方案

```gradle
implementation 'com.aspose:aspose-ocr:23.11'
```

相依性解析完成後，你就可以撰寫實際 **取得 OCR** 結果的程式碼了。

---

## 第二步：建立 OCR 引擎實例

引擎是整個流程的核心。建立它相當簡單，但真正的魔法在於你對它的設定。

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();
```

為何需要一個專屬的 `OcrEngine` 物件？它會儲存所有執行時選項，包括我們接下來會提到的拼寫校正切換。將引擎獨立化也能讓你平行執行多個辨識而不會互相干擾。

---

## 第三步：關閉拼寫校正（若需要原始輸出）

大多數 OCR 函式庫會自動校正拼寫錯誤，以提供協助。這對印刷文字很有幫助，但對原始資料提取卻是災難。以下說明如何 **關閉拼寫校正**：

```java
        // Step 3: Turn off the built‑in spell‑corrector to get raw text
        engine.getEngineOptions().setSpellCorrectorEnabled(false);
```

當此旗標為 `false` 時，引擎會回傳位圖上看到的原始內容，保留換行、標點，甚至偶爾的雜散字形。當你之後將輸出送入期望原始雜訊的機器學習管線時，這點至關重要。

---

## 第四步：載入影像 – 正確方式

你可能認為 `engine.getImage().loadFromFile("path")` 已足夠，但仍有一些細節需要注意：

1. **絕對路徑與相對路徑** – 使用 `Paths.get(...)` 以確保跨平台相容性。  
2. **支援的格式** – Aspose.OCR 支援 PNG、JPEG、BMP、TIFF 與 GIF。  
3. **解析度重要** – 較高 DPI 可提升辨識效果，特別是手寫連筆文字。

以下是一段穩健的程式碼範例，示範 **如何安全載入影像**：

```java
        // Step 4: Load the image that contains handwritten text
        String imagePath = "YOUR_DIRECTORY/handwritten.png";
        // Validate the file exists
        java.nio.file.Path path = java.nio.file.Paths.get(imagePath);
        if (!java.nio.file.Files.exists(path)) {
            throw new IllegalArgumentException("Image file not found: " + imagePath);
        }

        // Load the image into the OCR engine
        engine.getImage().loadFromFile(path.toAbsolutePath().toString());
```

如果你處理的是串流（例如從網頁表單上傳），請將 `loadFromFile` 改為 `loadFromStream`。關鍵在於：在將檔案送入引擎前務必先驗證，因為缺少檔案會拋出模糊的 `NullPointerException`，難以除錯。

---

## 第五步：執行辨識

現在關鍵時刻到來——**如何取得 OCR** 結果。`recognize()` 方法會執行內部管線，套用語言模型、分割，並（若啟用）進行拼寫校正。因為我們已關閉校正，將會得到未經處理的字元。

```java
        // Step 5: Perform OCR recognition
        OcrResult result = engine.recognize();
```

`OcrResult` 物件不只包含文字；你也可以取得信心分數、邊界框，甚至每個字元的機率。本教學將重點放在純文字上。

---

## 第六步：輸出原始 OCR 結果

最後，將結果印到主控台。這是 **提取原始文字** 用於除錯或後續處理的最簡單方式。

```java
        // Step 6: Output the raw OCR result
        System.out.println("Raw OCR output:");
        System.out.println(result.getText());
    }
}
```

### 預期輸出

假設 `handwritten.png` 包含以連筆書寫的 *“Hello World”* 文字，你會看到類似以下的結果：

```
Raw OCR output:
H e l l o   W o r l d
```

請注意額外的空格——這是有意為之，因為引擎保留了偵測到的精確間距。若之後需要壓縮空白，請在自行的後處理步驟中完成。

---

## 常見陷阱與避免方法

| 問題 | 發生原因 | 解決方案 |
|-------|----------------|-----|
| **Empty string** | 影像 DPI 太低或影像全白。 | 確保來源影像至少為 300 DPI；使用 `engine.getImage().setResolution(300, 300)`。 |
| **Garbage characters** | 檔案格式錯誤或位元組損毀。 | 使用影像檢視器驗證檔案；重新匯出為 PNG。 |
| **Spell‑corrector still active** | 程式碼其他地方不小心重新啟用。 | 在建立引擎後立即保留 `setSpellCorrectorEnabled(false)` 呼叫。 |
| **Handwritten text not recognized** | 引擎預設語言設定為英文印刷文字。 | 呼叫 `engine.getEngineOptions().setLanguage(Language.English);`，並可選擇 `engine.getEngineOptions().setUseDictionary(false);`。 |

---

## 擴充範例：辨識手寫文字

如果你的使用情境特別針對 **辨識手寫文字**，可以調整幾個選項以提升準確度：

```java
        // Enable handwritten mode (available in 23.11+)
        engine.getEngineOptions().setRecognitionMode(RecognitionMode.Handwritten);
```

此設定會告訴內部神經網路偏好連筆模式而非印刷字形。實際上，你會看到簽名、筆記或速寫的信心分數顯著提升。

---

## 完整可執行範例（可直接複製貼上）

以下是完整、獨立的 Java 類別，整合了我們討論的所有步驟。只需將 `YOUR_DIRECTORY/handwritten.png` 替換為你自己的影像路徑，然後執行即可。

```java
import com.aspose.ocr.*;

import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Turn off spell correction to get raw output
        engine.getEngineOptions().setSpellCorrectorEnabled(false);

        // Optional: set handwritten mode if needed
        // engine.getEngineOptions().setRecognitionMode(RecognitionMode.Handwritten);

        // 3️⃣ Load the image (how to load image safely)
        String imagePath = "YOUR_DIRECTORY/handwritten.png";
        Path path = Paths.get(imagePath);
        if (!Files.exists(path)) {
            throw new IllegalArgumentException("Image file not found: " + imagePath);
        }
        engine.getImage().loadFromFile(path.toAbsolutePath().toString());

        // 4️⃣ Perform OCR (how to get OCR raw text)
        OcrResult result = engine.recognize();

        // 5️⃣ Print raw result (extract raw text)
        System.out.println("Raw OCR output:");
        System.out.println(result.getText());
    }
}
```

以以下方式執行：

```bash
mvn compile exec:java -Dexec.mainClass=SpellCorrectDemo
```

你應該會看到原始字元，正如引擎讀取的那樣。

---

## 結論

我們已說明了在 Java 中 **如何取得 OCR** 原始結果，示範了正確的 **關閉拼寫校正** 方法，展示了最佳實踐 **如何載入影像**，並解釋了 **辨識手寫文字** 的細節。遵循這些步驟，你就能可靠地 **提取原始文字**，無論是建構文件數位化管線、法醫分析工具，或是簡易筆記應用程式。

接下來，你可能想探索：

- **後處理**：去除空白、正規化 Unicode，或將輸出送入語言模型。  
- **批次處理**：遍歷影像目錄，將結果存入資料庫。  
- **進階選項**：調整 `EngineOptions` 以支援多語言或自訂字典。  

試試看這些，並隨時在留言區提出問題。祝程式開發順利，願你的 OCR 永遠精準！

## 相關教學

- [如何使用 Aspose.OCR 以語言辨識影像文字](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [使用 Aspose.OCR 偵測區域模式從影像中提取文字（Java）](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [辨識影像文字的完整 Java OCR 教學 – 使用 Aspose OCR](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}