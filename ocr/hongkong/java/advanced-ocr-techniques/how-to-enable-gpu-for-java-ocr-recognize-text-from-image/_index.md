---
category: general
date: 2026-02-22
description: 學習如何在 Java OCR 中啟用 GPU，使用 Aspose OCR 快速辨識圖像文字並從發票提取文字。
draft: false
keywords:
- how to enable gpu
- recognize text from image
- extract text from invoice
- java ocr example
- load image for ocr
language: zh-hant
og_description: 如何在 Java OCR 中啟用 GPU，辨識圖像文字，並使用完整的 Java OCR 範例從發票中提取文字。
og_title: 如何在 Java OCR 中啟用 GPU – 快速指南
tags:
- Java
- OCR
- GPU
- Aspose
title: 如何在 Java OCR 中啟用 GPU – 從圖像辨識文字
url: /zh-hant/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java OCR 中啟用 GPU – 從影像辨識文字

有沒有想過在 Java 進行 OCR 時**如何啟用 GPU**？你並不孤單——許多開發者在處理大型、高解析度的文件（例如發票）時會遇到效能瓶頸。好消息是？使用 Aspose OCR 只要切換一個開關，就能讓顯示卡承擔繁重的運算。本教學將示範一個**java ocr 範例**，說明如何載入影像、啟用 GPU 處理，並即時從發票中擷取文字。

我們會從安裝函式庫說起，直到處理缺少 GPU 驅動程式等邊緣案例。完成後，你將能即時**從影像辨識文字**，並擁有一套可供未來 OCR 專案使用的完整範本。全程不需外部參考，只要純粹、可執行的程式碼。

## 前置條件

- 已在電腦上安裝 **Java Development Kit (JDK) 11** 或更新版本。  
- **Maven**（或 Gradle）用於相依性管理。  
- 配備 **GPU** 且已安裝最新驅動程式（NVIDIA、AMD 或 Intel）。  
- 一張發票影像檔（例如 `large_invoice_300dpi.png`）。  

若缺少上述任一項，請先完成安裝；本指南的後續步驟皆假設已具備這些條件。

## 步驟 1：將 Aspose OCR 加入專案

首先需要取得 Aspose OCR 函式庫。使用 Maven 時，只要在 `pom.xml` 中加入以下片段：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

> **小技巧：** 版本號會不定期更新，請前往 Maven Central 查看最新發行版以保持同步。

如果你偏好 Gradle，等價的設定如下：

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

相依性解析完成後，即可開始撰寫與 OCR 引擎互動的程式碼。

## 步驟 2：在 Aspose OCR 引擎中啟用 GPU

接下來就是本教學的重點——開啟 GPU 處理。Aspose OCR 提供三種處理模式：

| 模式 | 說明 |
|------|------|
| `CPU_ONLY` | 完全使用 CPU，適用於任何機器。 |
| `GPU_ONLY` | 強制使用 GPU，若無相容裝置則會失敗。 |
| `AUTO_GPU` | 偵測 GPU 並在可用時使用，否則回退至 CPU。 |

對於大多數情境，我們建議使用 **`AUTO_GPU`**，因為它兼具效能與相容性。以下示範如何啟用：

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Enable GPU processing (AUTO_GPU uses GPU when available)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // The rest of the steps follow...
    }
}
```

> **為什麼重要：** 啟用 GPU 後，300 dpi 的發票處理時間可從數秒縮短至不到一秒，具體效能取決於硬體規格。

## 步驟 3：載入影像以供 OCR – 從影像辨識文字

在引擎能讀取之前，必須先提供影像。Aspose OCR 的 `OcrInput` 類別支援檔案路徑、串流，甚至 `BufferedImage` 物件。為了簡化示範，我們使用檔案路徑：

```java
// Step 3.1: Prepare the input image
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png"); // <-- replace with your actual path
```

> **邊緣案例：** 若影像檔案大於 5 MB，建議先進行降採樣，以免在 GPU 上發生記憶體不足的錯誤。

## 步驟 4：執行 OCR 並從發票擷取文字

現在請引擎施展魔法。`recognize` 方法會回傳一個 `OcrResult` 物件，內含擷取的文字、信心分數與版面資訊。

```java
// Step 4.1: Run the recognition
OcrResult ocrResult = ocrEngine.recognize(ocrInput);

// Step 4.2: Print the extracted text to console
System.out.println("=== Extracted Text ===");
System.out.println(ocrResult.getText());
```

執行程式後，預期會看到類似以下的輸出：

```
=== Extracted Text ===
Invoice #12345
Date: 2026-02-20
Total: $1,245.67
...
```

若輸出文字雜亂，請確認影像清晰且 OCR 語言設定正確（Aspose 預設為英文，可透過 `ocrEngine.setLanguage(OcrEngine.Language.SPANISH)` 等方式切換）。

## 步驟 5：完整可執行範例（直接複製貼上）

以下提供完整、獨立的 Java 類別。將程式貼到 IDE 中，調整影像路徑後即可 **執行**。

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU (auto‑detect)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace with the absolute or relative path to your invoice image
        ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png");

        // 4️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### 預期輸出

在清晰的 300 dpi 發票上執行此程式，通常會得到文件每一行的純文字表示。具體內容取決於發票版面，但會出現如 *Invoice Number*、*Date*、*Total Amount* 以及各項目描述等欄位。

## 常見問題與解決方式

| 症狀 | 可能原因 | 解決方法 |
|------|----------|----------|
| **`java.lang.UnsatisfiedLinkError`** | 缺少或不相容的 GPU 驅動程式 | 從 NVIDIA/AMD/Intel 下載並安裝最新驅動程式。 |
| **處理速度非常慢** | GPU 靜默回退至 CPU | 確認 `ocrEngine.getProcessingMode()` 回傳 `AUTO_GPU`，且 `SystemInfo.isGpuAvailable()` 為 true。 |
| **輸出為空白** | 影像過暗或對比度不足 | 在送入 OCR 前先前處理影像（提升對比、二值化）。 |
| **記憶體不足** | 影像過大（>10 MP） | 調整影像尺寸或將其切割成多塊，分別處理。 |

## 步驟回顧（快速參考）

| 步驟 | 你完成了什麼 |
|------|--------------|
| 1 | 加入 Aspose OCR 相依性 |
| 2 | 建立 `OcrEngine` 並設定 `AUTO_GPU` |
| 3 | 透過 `OcrInput` 載入發票影像 |
| 4 | 呼叫 `recognize` 並印出 `ocrResult.getText()` |
| 5 | 處理常見錯誤並驗證輸出結果 |

## 往更遠的方向 – 後續步驟

- **批次處理：** 迴圈讀取資料夾內的多張發票，將結果寫入資料庫。  
- **語言支援：** 使用 `ocrEngine.setLanguage(OcrEngine.Language.FRENCH)` 以辨識多語言發票。  
- **後處理：** 透過正規表達式從原始文字中抽取 *Invoice Number*、*Total Amount* 等欄位。  
- **GPU 調校：** 若系統有多張 GPU，可使用 `ocrEngine.setGpuDeviceId(int id)` 選擇效能最佳的裝置。

## 結論

我們示範了**如何在 Java OCR 中啟用 GPU**，提供了一個乾淨的**java ocr 範例**，並完整說明了從**載入影像以供 OCR**到**從發票擷取文字**的全流程。透過 Aspose 的 `AUTO_GPU` 模式，你可以在不犧牲相容性的前提下獲得效能提升，無論是開發機還是生產伺服器皆適用。

快試試看，調整影像前處理方式，或是實作批次作業。結合 GPU 加速與強大的 OCR 函式庫，讓你的應用程式飛躍無限可能。

---

![顯示 GPU 加速 OCR 流程圖 – 如何在 Java OCR 中啟用 GPU](https://example.com/images/gpu-ocr-pipeline.png "如何在 Java OCR 中啟用 GPU")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}