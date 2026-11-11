---
category: general
date: 2026-03-28
description: 使用 Aspose OCR 進行影像前置處理與文字辨識。了解如何從相片中擷取文字，逐步提升 OCR 準確度的前置處理方法。
draft: false
keywords:
- preprocess image for OCR
- recognize text from image
- extract text from photo
- improve OCR accuracy preprocessing
- Aspose OCR Java
- image preprocessing pipeline
language: zh-hant
og_description: 使用 Aspose OCR Java 預處理圖像以進行 OCR，並從照片中擷取文字。遵循本教學，只需幾個步驟即可提升 OCR 準確度的預處理。
og_title: OCR 圖像前處理 – 完整 Java 指南
tags:
- OCR
- Java
- Image Processing
title: 影像預處理以進行 OCR – 提升 Java 文本提取準確度
url: /zh-hant/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-text-extraction-accuracy-in-j/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 圖像前處理以進行 OCR – 完整的 Java 教學

有沒有試過 **preprocess image for OCR**，結果仍然得到亂碼輸出？你並不孤單。在許多實務專案中，原始掃描或手機拍攝的圖像常帶有傾斜、雜訊或低對比度，會讓即使是最聰明的辨識引擎也失靈。好消息是？只要使用簡短的前處理流程——去傾斜、去雜訊、二值化——就能大幅 **improve OCR accuracy preprocessing**。

在本教學中，我們將逐步示範一個實作範例，說明如何使用 Aspose OCR for Java **recognize text from image**。完成後，你將能夠 **extract text from photo** 檔案，錯誤率大幅降低，並了解每個前處理步驟的意義。

> **你將學到**  
> * 一個完整可執行的 Java 程式，能載入傾斜的照片、套用三個經典濾鏡，並輸出乾淨的文字。  
> * 了解去傾斜、去雜訊與二值化背後的「為什麼」。  
> * 處理邊緣案例的技巧——大型檔案、不同影像格式，以及自訂濾鏡順序。

## 前置條件

- 安裝 Java 8 或更新版本（程式碼亦可在 JDK 11 上編譯）。  
- 使用 Maven 或 Gradle 取得 Aspose OCR 函式庫。  
- 一張範例影像（例如 `angled-photo.jpg`），稍微旋轉且含有一些視覺雜訊。  
- 基本熟悉 Java 的 `main` 方法——不需要深入的 OCR 專業知識。

如果缺少上述任一項，只需從 Oracle 或 OpenJDK 下載最新的 JDK，並在 `pom.xml` 中加入以下 Maven 依賴：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Maven Central for the newest version -->
</dependency>
```

## 第一步 – 建立 OCR 引擎實例

首先需要的是一個 `OcrEngine` 物件。可以把它想像成稍後會讀取處理後影像的大腦。

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **為什麼這很重要：** 引擎封裝了辨識設定、語言套件，以及—對我們而言最重要的—前處理選項。若沒有它，你必須手動串接影像處理函式庫，這樣就失去了乾淨流程的意義。

## 第二步 – 建構前處理管線（de‑skew → denoise → binarize）

Aspose OCR 內建 `PreprocessingOptions` 類別，讓你以所需的精確順序堆疊濾鏡。此處我們加入三個濾鏡：

1. **DE_SKEW** – 使旋轉的文字恢復水平。  
2. **DENOISE** – 平滑顆粒狀像素，避免被誤認為字元。  
3. **BINARIZE** – 將影像轉為純黑白，讓 OCR 引擎的工作更簡單。

```java
        // Step 2: Assemble the preprocessing pipeline
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);   // correct rotation
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);  // remove grain
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE); // high‑contrast B&W

        // Attach the pipeline to the OCR engine
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);
```

> **專業提示：** 濾鏡的順序至關重要。如果在去雜訊之前先二值化，雜訊可能會變成硬邊的黑點，讓辨識器困惑。先去傾斜可確保文字基線水平，進而提升去雜訊與二值化的效果。

## 第三步 – 將影像送入引擎

現在我們將引擎指向要讀取的檔案。路徑可以是絕對路徑或相對於專案根目錄的路徑。

```java
        // Step 3: Run OCR on the target image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

> **如果影像非常大怎麼辦？** Aspose OCR 會自動將長邊超過 2000 px 的影像縮小，但若記憶體是考量點，你可以透過 `ocrEngine.getRecognitionSettings().setMaxImageDimension(1500)` 來覆寫此設定。

## 第四步 – 輸出辨識文字

最後，我們將提取的字串印到主控台。於實際應用中，你可能會將其寫入資料庫、檔案，或傳入後續的 NLP 流程。

```java
        // Step 4: Print the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### 預期輸出

如果 `angled-photo.jpg` 包含句子 *“The quick brown fox jumps over the lazy dog.”*，你應該會看到類似以下的結果：

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

請注意輸出相當乾淨——沒有雜散符號，也沒有斷行。這就是 **preprocess image for OCR** 的威力。

## 第五步 – 驗證與微調（可選）

即使管線已相當穩固，你仍可能遇到邊緣案例：

| 情況 | 建議調整 |
|-----------|-----------------|
| **非常低對比度**（例如，褪色的掃描文件） | 在二值化之前插入額外的 `ContrastAdjustment` 濾鏡。 |
| **彩色背景**（例如，帶有彩色印章的收據） | 加入 `BackgroundRemoval` 濾鏡，或先手動轉為灰階。 |
| **多頁 PDF** | 迭代每一頁的影像，並重複使用相同的 `preprocessingOptions`。 |

你可以透過呼叫 `preprocessingOptions.addFilter(PreprocessFilter.CONTRAST)` 或其他 Aspose OCR API 文件中列出的濾鏡來進行實驗。

## 完整、可執行範例

以下是完整程式碼，可直接複製貼上至名為 `PreprocessExample.java` 的檔案。編譯前請確保已解決 Maven 依賴。

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing: de‑skew → denoise → binarize
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE);
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);

        // 3️⃣ Perform OCR on the chosen image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // 4️⃣ Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

編譯並執行：

```bash
mvn compile exec:java -Dexec.mainClass=PreprocessExample
```

你應該會在主控台看到乾淨的文字，證明你已成功 **preprocess image for OCR** 並 **recognize text from image**。

## 常見問題與解答

**Q1: 這能支援 PNG 或 TIFF 檔案嗎？**  
是的——Aspose OCR 支援 JPEG、PNG、BMP、TIFF 以及其他多種格式。相同的前處理管線適用，函式庫會自動偵測格式。

**Q2: 如果我要從手機拍攝的照片中提取文字該怎麼辦？**  
手機照片常因光線不均而受影響。於二值化之前加入 `LIGHTING_CORRECTION` 濾鏡可協助改善。程式碼變更只需一行：

```java
preprocessingOptions.addFilter(PreprocessFilter.LIGHTING_CORRECTION);
```

**Q3: 我可以更改 OCR 的語言嗎？**  
當然可以。建立引擎後，設定語言：

```java
ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.SPANISH);
```

**Q4: 這如何提升 OCR 的前處理準確度？**  
每個濾鏡都會減少特定的視覺雜訊。去傾斜使文字行對齊，去雜訊去除隨機斑點，二值化產生高對比度影像。三者結合為辨識演算法提供更乾淨的訊號，進而提升字元層級的準確率——在噪聲較大的輸入上常可提升 15‑30 % 。

## 往後步驟與相關主題

- **批次處理：** 將核心邏輯包在迴圈中，以處理整個資料夾的照片。  
- **自訂濾鏡順序：** 嘗試在已具高對比度的文件上先執行 `BINARIZE` 再 `DENOISE`。  
- **效能調校：** 使用 `ocrEngine.getRecognitionSettings().setThreadCount(4)` 在多核心機器上平行化。  
- **替代函式庫：** 將 Aspose OCR 與 Tesseract‑Java 進行比較，以應對開源情境。  
- **後處理：** 對原始輸出套用拼寫檢查或正規表達式清理，取得更乾淨的結果。

掌握 **preprocess image for OCR** 工作流程後，你會發現從照片來源提取文字變成可預測、可重複的任務，而不再是碰運氣的實驗。

---

*準備好提升你的 OCR 流程了嗎？取得程式碼、微調濾鏡，觀察準確率提升。如果遇到問題，請在下方留言——祝編程愉快！*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}