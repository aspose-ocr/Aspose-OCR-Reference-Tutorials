---
category: general
date: 2026-05-03
description: Aspose OCR Java 範例展示如何載入影像進行 OCR，並在僅幾行程式碼內從特定區域提取文字。
draft: false
keywords:
- aspose ocr java example
- load image for OCR
- extract text from region
language: zh-hant
og_description: Aspose OCR Java 示例展示了載入圖像進行 OCR 並從特定區域提取文字，非常適合發票處理。
og_title: Aspose OCR Java 示例 – 區域文字提取
tags:
- Aspose OCR
- Java
- Image Processing
title: Aspose OCR Java 範例：從區域提取文字
url: /zh-hant/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java Example: Extract Text from a Region

想要一個 **Aspose OCR Java 範例**，只抓取影像中需要的那一部分文字嗎？本教學將帶您一步步完成 **載入影像進行 OCR** 以及 **從指定區域擷取文字**，非常適合發票號碼、表單欄位或任何隱藏在較大圖片中的資料。

您可能會好奇，為什麼要把 OCR 限制在矩形區域，而不是掃描整頁？簡短的答案是：速度與準確度。當引擎只看定義好的切片時，會跳過不相關的雜訊、執行更快，且往往產生更乾淨的結果。完成本教學後，您將擁有一個完整的 Java 程式，能夠做到上述功能，並提供一些避免新手常見陷阱的技巧。

## What You’ll Need

在開始之前，請先確保您已具備：

- **Java Development Kit (JDK) 11** 或更新版本。
- **Aspose.OCR for Java** 函式庫（可從 Maven Central 或 Aspose 下載入口取得最新 JAR）。
- 一張包含欲讀取文字的影像檔——本示範使用 `invoice.png`，其發票號碼位於右上角附近。
- 您慣用的 IDE 或簡易文字編輯器加上終端機；任意建置工具（Maven、Gradle，或純 `javac`）皆可。

就這樣。無需額外的 OCR 引擎、原生二進位檔，只要純 Java 加上 Aspose。

![Aspose OCR Java example screenshot](/images/aspose-ocr-java-example.png "Aspose OCR Java example showing region extraction")

## Aspose OCR Java Example – Initialize the OCR Engine

任何 OCR 工作流程的第一步都是建立引擎實例。Aspose 提供輕量級的 `OcrEngine` 類別，負責從影像載入到語言選擇的全部工作。

```java
import com.aspose.ocr.*;

public class RegionOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**Why this matters:** 事先建立引擎可讓您得到一個乾淨的物件以供設定。若要批次處理多張影像，您可以重複使用同一個 `OcrEngine`，從而節省記憶體與初始化時間。

## Load Image for OCR

接著告訴引擎要掃描哪張圖片。Aspose 的 `ImageStream.fromFile` 輔助方法，抽象化了低階的 `FileInputStream` 寫法。

```java
        // Step 2: Load the image that contains the invoice
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Tip:** 把 `YOUR_DIRECTORY` 替換成指向 `invoice.png` 所在位置的絕對路徑或相對路徑。若找不到檔案，Aspose 會拋出 `IOException`，因此在正式環境建議使用 try‑catch 包裹。

## Define and Extract Text from a Region

現在輪到重點：告訴引擎要看哪個矩形區域。`java.awt.Rectangle` 建構子接受 `(x, y, width, height)`，單位皆為像素。

```java
        // Step 3: Define the region where the invoice number is located (x, y, width, height)
        java.awt.Rectangle invoiceRegion = new java.awt.Rectangle(120, 250, 300, 80);
        ocrEngine.setRegion(invoiceRegion);   // restrict recognition to this area
```

**How it works:** 透過 `setRegion`，您將 OCR 掃描限制在寬 300 像素、高 250 像素、左邊距 120 像素的切片內。請依照自己的版面調整這些數值；快速取得座標的方法是使用任何能顯示像素座標的圖形編輯器開啟影像。

## Enable Language and Run Recognition

Aspose OCR 支援多種語言，但對於發票號碼只需要 English。只啟用必要語言可大幅降低誤判。

```java
        // Step 4: Enable English language for recognition
        ocrEngine.getLanguage().setEnglish(true);

        // Step 5: Perform recognition and output the extracted text
        if (ocrEngine.recognize()) {
            System.out.println("Extracted region text: " + ocrEngine.getText());
        } else {
            System.err.println("OCR recognition failed.");
        }
    }
}
```

**Why enable English only?** 若同時啟用多種語言，OCR 引擎會嘗試匹配所有語言的字元，對於單純的英數字會造成混淆。縮小語言範圍可提升速度與精確度。

### Expected Output

若一切順利，您會看到類似以下的結果：

```
Extracted region text: INV-12345
```

若矩形位置偏差幾個像素，輸出可能會變成雜亂或空白。這是一個簡易的驗證步驟：執行程式、檢查主控台，確認文字與影像中看到的相符。

## Run the Code and Verify the Output

假設您使用 Maven，請在 `pom.xml` 中加入 Aspose OCR 相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

編譯並執行：

```bash
mvn compile exec:java -Dexec.mainClass=RegionOcrExample
```

或是直接使用 `javac`：

```bash
javac -cp "aspose-ocr-23.10.jar" RegionOcrExample.java
java -cp ".:aspose-ocr-23.10.jar" RegionOcrExample
```

您應該會在主控台看到 **Extracted region text** 行。如果出現 “OCR recognition failed”，請再次確認檔案路徑，並確保矩形內確實有可辨識的字元。

## Edge Cases & Common Variations

| 情境 | 需要調整的地方 |
|-----------|----------------|
| **Multiple languages** (e.g., English + Spanish) | 呼叫 `ocrEngine.getLanguage().setSpanish(true);` 同時保留 English 設定。 |
| **Region outside image bounds** | Aspose 會自動裁切矩形，但會遺失資料。可使用 `ImageInfo` (`ocrEngine.getImage().getWidth()`) 先取得影像尺寸，再設定區域。 |
| **Dynamic invoices** (different layouts) | 考慮先對整張影像做輕量級預掃描，找出 “Invoice #” 等關鍵字，再程式化計算矩形位置。 |
| **Higher DPI images** | 提升 `ocrEngine.getImage().setResolution(300);` 以提升掃描文件的辨識精度。 |
| **Performance tuning** | 關閉不必要的語言、盡量縮小區域、在多檔案情況下重複使用同一個 `OcrEngine` 實例。 |

## Pro Tips From the Trenches

- **Pro tip:** 若只需要數字（常見於發票號碼），可啟用數字模式 `ocrEngine.getLanguage().setDigits(true);`，可排除字母雜訊。
- **Watch out for:** 透明 PNG。Aspose 有時會誤判 alpha 通道；先將影像轉為實心背景的 JPEG 可解決空白輸出問題。
- **Remember:** 矩形使用的是影像本身的座標系統，而非螢幕上看到的 UI 縮放。務必以實際要處理的檔案測試。

## What’s Next?

現在您已掌握 **Aspose OCR Java 範例** 進行區域式擷取，接下來可以往以下方向延伸：

- **Batch processing:** 迴圈處理整個發票資料夾，重複使用同一個 `OcrEngine` 以提升吞吐量。
- **Data validation:** 使用正規表達式如 `INV-\\d{5}` 驗證擷取出的文字是否為有效的發票號碼。
- **Integration with PDF:** 結合 Aspose.PDF，將擷取的文字覆寫回原始 PDF，形成稽核追蹤。
- **Cloud deployment:** 將程式封裝成輕量級 REST 服務（Spring Boot），讓其他系統可隨時呼叫。

上述步驟皆圍繞相同核心概念——**載入影像進行 OCR**、**從區域擷取文字**，以及**處理結果**——因此轉換過程相當順暢。

---

*Happy coding! If you hit any snags, drop a comment below or check the Aspose forums where the community shares real‑world tweaks for tricky layouts.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}