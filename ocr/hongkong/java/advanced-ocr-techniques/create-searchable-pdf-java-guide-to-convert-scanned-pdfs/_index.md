---
category: general
date: 2026-02-22
description: 使用 Aspose OCR 在 Java 中將掃描 PDF 轉換為可搜尋的 PDF。學習如何轉換掃描 PDF、壓縮 PDF 圖像，以及高效地進行
  PDF OCR 辨識。
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- compress pdf images
- recognize pdf ocr
- image pdf to text
language: zh-hant
og_description: 使用 Aspose OCR 在 Java 中將掃描 PDF 轉換為可搜尋的 PDF。本逐步教學示範如何轉換掃描 PDF、壓縮 PDF
  圖像，以及執行 PDF OCR 辨識。
og_title: 建立可搜尋 PDF – Java 指南：將掃描的 PDF 轉換為可搜尋 PDF
tags:
- Java
- OCR
- PDF
- Aspose
title: 建立可搜尋 PDF – Java 指南：將掃描 PDF 轉換為可搜尋 PDF
url: /zh-hant/java/advanced-ocr-techniques/create-searchable-pdf-java-guide-to-convert-scanned-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立可搜尋 PDF – Java 指南：將掃描 PDF 轉換

有沒有需要從一堆掃描文件**建立可搜尋 PDF**的時候？這是常見的困擾——PDF 看起來沒問題，但卻無法使用 *Ctrl + F* 來搜尋。好消息是，只要幾行 Java 程式碼加上 Aspose OCR，就能把只有影像的 PDF 變成完整可搜尋的檔案，**convert scanned PDF** 為文字，甚至透過**compressing PDF images** 來縮小檔案大小。  

在本教學中，我們會一步步走過完整、可執行的範例，說明每個設定為何重要，並示範如何針對多頁掃描或低解析度影像等邊緣案例進行調整。完成後，你將擁有一段穩定、可投入生產環境的程式碼，能可靠地**recognize pdf ocr**，並產生整潔的可搜尋文件。

---

## 你需要的環境

- **Java 17**（或任何較新的 JDK；API 與 JDK 無關）  
- **Aspose.OCR for Java** 函式庫 – 可從 Maven Central 取得 (`com.aspose:aspose-ocr`)  
- 一個你想要變成可搜尋的掃描 PDF（僅影像）  
- 你熟悉的 IDE 或文字編輯器（IntelliJ、VS Code、Eclipse…）

不需要大型框架，也不需要外部服務——只要純粹的 Java 加上一個第三方 JAR 即可。  

---

![create searchable pdf example](placeholder-image.png "Illustration of a searchable PDF created from a scanned document")

*Image alt text:* **create searchable pdf** 插圖，顯示掃描 PDF 前後的文字可搜尋化對比。

---

## Step 1 – Initialise the OCR Engine  

首先必須建立 `OcrEngine` 實例。它就像大腦，會分析 PDF 內的每張位圖，並輸出 Unicode 字元。  

```java
import com.aspose.ocr.*;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this object holds licensing info and global settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pro tip:** 若需要連續處理多個 PDF，請重複使用同一個 `OcrEngine`，而不是每次都新建。這樣可以省下幾毫秒的時間，並減少記憶體的頻繁分配。

---

## Step 2 – Configure PDF‑Specific OCR Options  

Aspose 讓你微調輸出 PDF 的建構方式。以下三個設定是對**compress pdf images** 同時保留可搜尋性的最關鍵參數。

```java
        // Configure PDF‑specific options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // Higher DPI = better text recognition
        pdfOcrOptions.setCompressImages(true);           // Shrinks the final file size
        pdfOcrOptions.setEmbedOriginalImages(true);      // Keeps the visual look of the original scan
```

- **Output DPI** – 300 dpi 為最佳平衡；較低的 DPI 會加快速度，但可能遺漏小字體。  
- **CompressImages** – 在底層啟用無損 PNG 壓縮；可搜尋 PDF 仍保持清晰，同時變得更輕。  
- **EmbedOriginalImages** – 若不開啟此旗標，引擎會捨棄原始點陣圖，只留下不可見的文字層。保留影像可確保 PDF 與原始掃描外觀完全相同，這是許多合規團隊的需求。

---

## Step 3 – Load Your Scanned PDF into an `OcrInput`  

Aspose 透過 `OcrInput` 包裝器讀取來源檔案。你可以加入多個檔案，但本示範僅聚焦於單一 **image PDF**。  

```java
        // Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");   // <- replace with the path to your file
```

> **Why not just pass a `File`?** 使用 `OcrInput` 能讓你在 OCR 前串接多個 PDF，甚至混合影像檔（PNG、JPEG）。當你**convert scanned pdf** 可能分散於多個來源時，這是建議的做法。

---

## Step 4 – Perform OCR and Get a Searchable PDF as a Byte Array  

魔法時刻到來。引擎會分析每一頁，執行 OCR，並建立一個同時包含原始影像與隱藏文字層的新 PDF。  

```java
        // Perform OCR – the result is a byte array representing the searchable PDF
        byte[] searchablePdfBytes = ocrEngine.recognizePdf(ocrInput, pdfOcrOptions);
```

若需要原始文字作其他用途（例如建立索引），也可以呼叫 `ocrEngine.recognize(ocrInput)`，它會回傳 `String`。但若目標是**create searchable pdf**，則應以位元組陣列寫入磁碟。

---

## Step 5 – Save the Searchable PDF to Disk  

最後，將位元組陣列寫入檔案。Java 的 NIO 只需要一行程式碼即可完成。  

```java
        // Write the searchable PDF to disk
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/searchable_output.pdf"),
                searchablePdfBytes
        );

        System.out.println("Searchable PDF created.");
    }
}
```

當你在 Adobe Acrobat 或任何現代檢視器中開啟 `searchable_output.pdf`，會發現現在可以選取、複製與搜尋文字——正是**image pdf to text** 轉換所承諾的效果。

---

## Convert Scanned PDF to Text with OCR (Optional)

有時你只需要抽取的純文字，而不需要新 PDF。只要重複使用同一個引擎即可：

```java
        // Optional: extract plain text from the scanned PDF
        String extractedText = ocrEngine.recognize(ocrInput).getText();
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/extracted_text.txt"),
                extractedText.getBytes()
        );
```

此段程式碼示範了如何輕鬆執行**recognize pdf ocr**，以供後續如建立搜尋索引或自然語言分析等處理。

---

## Compress PDF Images for Smaller Files  

如果來源掃描檔非常大（例如 600 dpi 彩色掃描），產出的可搜尋 PDF 仍可能相當龐大。除了 `setCompressImages(true)` 旗標外，你也可以在 OCR 前手動降解析度：  

```java
        // Downscale each page image to 150 dpi before OCR (reduces size dramatically)
        pdfOcrOptions.setOutputDpi(150);
```

降低 DPI 大約可將檔案大小減半，但請測試可讀性——低於 150 dpi 時部分字體可能變得難以辨識。**compress pdf images** 與 OCR 準確度之間的取捨，需要依照你的儲存空間限制自行決定。

---

## Recognize PDF OCR Settings Explained  

| Setting                | Effect on Output                         | Typical Use‑Case                                   |
|------------------------|------------------------------------------|----------------------------------------------------|
| `setOutputDpi(int)`    | 控制 OCR 輸出點陣圖的解析度               | 高品質檔案 (300 dpi) 與輕量化網頁 PDF (150 dpi)   |
| `setCompressImages`    | 啟用 PNG 壓縮                             | 需要透過電子郵件傳送或上傳至雲端時減少檔案大小   |
| `setEmbedOriginalImages`| 保留原始掃描影像                         | 必須保留原始外觀的法律或合規文件                 |
| `setLanguage` (optional) | 強制使用特定語言模型（例如 "eng"）      | 多語言語料庫中，預設自動偵測可能不正確           |

了解這些參數後，你就能更聰明地**recognize pdf ocr**，避免出現「文字模糊」的情況。

---

## Image PDF to Text – Common Pitfalls and How to Avoid Them  

1. **Low‑resolution scans** – OCR 準確度在低於 150 dpi 時會急劇下降。請在送入 Aspose 前將來源升採樣，或向掃描器要求更高 DPI。  
2. **Rotated pages** – 若頁面是側向掃描，請啟用自動旋轉：`pdfOcrOptions.setAutoRotate(true);`。  
3. **Encrypted PDFs** – 引擎無法直接讀取受密碼保護的檔案；請先使用 Aspose.PDF 的 `PdfDocument` 解除加密。  
4. **Mixed raster and text** – 部分 PDF 已內建隱藏文字層。再次執行 OCR 可能會產生重複文字。使用 `PdfOcrOptions.setSkipExistingText(true);` 以保留原有文字層。

解決上述問題後，你的**create searchable pdf** 工作流程即可在真實世界的文件集合中保持穩健。

---

## Full Working Example (All Steps in One File)

以下是完整的 Java 類別，直接複製貼上到 IDE 中使用。將 `YOUR_DIRECTORY` 替換為實際的資料夾路徑。

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure PDF‑specific OCR options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // higher DPI improves accuracy
        pdfOcrOptions.setCompressImages(true);           // reduce output size
        pdfOcrOptions.setEmbedOriginalImages(true);      // keep original visual fidelity

        // 3️⃣ Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");        // <-- your source file

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}