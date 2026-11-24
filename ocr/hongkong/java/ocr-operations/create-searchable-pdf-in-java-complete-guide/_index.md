---
category: general
date: 2026-07-05
description: 使用 Aspose OCR 在 Java 中建立可搜尋的 PDF。了解如何壓縮 PDF 中的圖像、將掃描圖像轉換為 PDF，以及停用字型嵌入以縮小檔案大小。
draft: false
keywords:
- create searchable pdf
- compress images in pdf
- convert scanned image to pdf
- disable font embedding pdf
language: zh-hant
og_description: 使用 Aspose OCR 在 Java 中建立可搜尋 PDF。本教學示範如何壓縮 PDF 中的圖像、將掃描圖像轉換為 PDF，以及停用
  PDF 的字型嵌入。
og_title: 在 Java 中建立可搜尋的 PDF – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to compress
    images in PDF, convert scanned image to PDF, and disable font embedding PDF for
    smaller files.
  headline: Create Searchable PDF in Java – Complete Guide
  type: TechArticle
tags:
- Java
- OCR
- PDF
title: 使用 Java 建立可搜尋 PDF – 完整指南
url: /zh-hant/java/ocr-operations/create-searchable-pdf-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中建立可搜尋的 PDF – 完整指南

是否曾需要從掃描文件**建立可搜尋的 PDF**，卻卡在「該怎麼做」的部份？你並不孤單。在許多專案中，將 TIFF 或 JPEG 轉成可搜尋的 PDF 是*必備*功能，尤其當你還想**在 PDF 中壓縮圖像**以保持檔案大小可控時。

在本教學中，我們將以 Aspose OCR for Java 示範一個實作範例。完成後，你將清楚知道如何**將掃描圖像轉換為 PDF**、調整**在 PDF 中壓縮圖像**設定，甚至**停用 PDF 嵌入字型**以減少幾個 KB。沒有多餘的說明——只提供一個完整、可直接在程式碼中使用的解決方案。

## 你將學會

- 在 Java 專案中設定 Aspose OCR 引擎。  
- 對 TIFF（或任何點陣圖）執行 OCR。  
- 設定 `PdfSaveOptions` 以 **在 PDF 中壓縮圖像** 並 **停用 PDF 嵌入字型**。  
- 將結果儲存為 **可搜尋的 PDF**，即可即時索引或搜尋。

**先決條件**  
- 已安裝 Java 8 或更新版本。  
- 使用 Maven 或 Gradle 進行相依管理（我們將示範 Maven 片段）。  
- 已備妥待處理的掃描圖像檔（TIFF、PNG 或 JPEG）。

如果你已具備上述條件，讓我們開始吧。

![建立可搜尋 PDF 工作流程 – Java OCR 轉 PDF](/images/create-searchable-pdf-workflow.png "展示使用 Aspose OCR 建立可搜尋 PDF 的步驟圖")

## 第一步：加入 Aspose OCR 相依性

首先，將 Aspose OCR 函式庫加入你的專案。使用 Maven 時，將以下內容加入 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

如果你偏好 Gradle，等價的設定如下：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **小技巧：** 留意 Aspose 的發行說明；較新版本通常會提升 OCR 準確度與效能。

## 第二步：初始化 OCR 引擎

建立 OCR 引擎只需要實例化 `OcrEngine`。此物件會處理從載入圖像到文字擷取的所有工作。

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

為什麼需要專屬的引擎？Aspose 將繁重的工作（圖像前處理、語言模型）與應用程式的其他部分分離，讓你可以在多個檔案間重複使用同一個 `engine`，而不必重新初始化大量資源。

## 第三步：對掃描圖像執行 OCR

現在我們將掃描檔案提供給引擎。`recognizeImage` 方法會回傳 `RecognitionResult`，其中包含擷取的文字與版面資訊。

```java
import com.aspose.ocr.RecognitionResult;

// ...

// Step 3: Perform OCR on the source image
String sourcePath = "YOUR_DIRECTORY/document_scan.tif"; // could be .png or .jpg too
RecognitionResult result = engine.recognizeImage(sourcePath);
```

> **如果圖像不是 TIFF 呢？**  
> Aspose OCR 會自動偵測常見的點陣圖格式，你可以直接指向 JPEG、PNG 或 BMP，無需修改程式碼。

## 第四步：設定 PDF 儲存選項（壓縮圖像與停用字型嵌入）

這裡就是次要關鍵字發揮作用的地方。我們會告訴 Aspose **在 PDF 中壓縮圖像** 並 **停用 PDF 嵌入字型**。這兩個設定都能減少最終檔案大小——在大量文件傳遞時非常實用。

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

// ...

// Step 4: Set up PDF save options
PdfSaveOptions pdfOpts = new PdfSaveOptions();

// Reduce PDF size by compressing images
pdfOpts.setCompressImages(true);
pdfOpts.setImageQuality(80); // 0‑100, 80 is a good balance

// Prevent fonts from being embedded – saves a few KB per page
pdfOpts.setEmbedFonts(false);
```

**為什麼要壓縮圖像？**  
掃描頁面通常是高解析度；將品質壓縮至 80% 可將 10 頁 PDF 從 12 MB 縮減至不到 3 MB，且視覺上幾乎無差異。

**為什麼要停用字型嵌入？**  
如果 OCR 引擎使用標準系統字型（如 Arial 或 Times New Roman），嵌入字型是多餘的。關閉此功能可進一步縮減檔案大小，特別是在大量批次時。

## 第五步：將 OCR 結果儲存為可搜尋的 PDF

最後一步將所有元件結合：原始圖像、擷取的文字層，以及剛才設定的 PDF 選項。

```java
// Step 5: Save the OCR result as a searchable PDF
String outputPath = "YOUR_DIRECTORY/document.pdf";
engine.saveAsSearchablePdf(outputPath, pdfOpts);

System.out.println("Searchable PDF created at: " + outputPath);
```

當你在 Adobe Reader 或任何現代檢視器中開啟 `document.pdf` 時，會看到原始掃描圖像**加上**一個隱形的文字層。於搜尋框輸入關鍵字即可高亮匹配結果——正是「建立可搜尋 PDF」所承諾的功能。

### 預期輸出

執行程式並使用有效的 TIFF 檔案，會得到類似以下的結果：

```
Searchable PDF created at: YOUR_DIRECTORY/document.pdf
```

開啟 PDF，按下 `Ctrl+F`，輸入掃描頁面中出現的字詞，即可跳至正確位置。這就是成功的 **建立可搜尋 PDF** 工作流程的標誌。

## 常見陷阱與避免方法

| 問題 | 發生原因 | 解決方法 |
|-------|----------------|-----|
| **空白 PDF** | `PdfSaveOptions` 未傳遞給 `saveAsSearchablePdf`。 | 確保呼叫接受 `PdfSaveOptions` 的重載方法。 |
| **亂碼** | OCR 語言未設定（預設為英文）。 | 在 `recognizeImage` 前使用 `engine.getLanguage().setLanguage(OcrLanguage.FRENCH);`。 |
| **檔案過大** | `setCompressImages(false)` 或 `setEmbedFonts(true)`。 | 保持上述兩個旗標的設定。 |
| **圖像失真** | `setImageQuality` 設定過低（<50）。 | 維持在 70‑90 之間以取得良好平衡。 |

## 擴充範例

現在你已能 **將掃描圖像轉換為 PDF** 並控制檔案大小，接下來可能想要：

- 使用簡單的 `for(File f : folder.listFiles())` 迴圈**批次處理**資料夾中的掃描檔案。  
- 使用 Aspose PDF (`PdfDocument.addWatermarkText`) **加入浮水印**。  
- 將 OCR 文字匯出為 **純 .txt** 檔案，以供索引系統使用（`result.getText().writeToFile("doc.txt")`）。

所有這些擴充功能皆重複使用相同的 `OcrEngine` 實例，降低記憶體使用量。

## 完整、可直接執行的程式碼

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Perform OCR on the source image
        String source = "YOUR_DIRECTORY/document_scan.tif";
        RecognitionResult result = engine.recognizeImage(source);

        // Step 3: Configure PDF save options (compress images & disable fonts)
        PdfSaveOptions pdfOpts = new PdfSaveOptions();
        pdfOpts.setCompressImages(true);      // Reduce PDF size by compressing images
        pdfOpts.setImageQuality(80);          // Image quality (0‑100)
        pdfOpts.setEmbedFonts(false);         // Do not embed fonts to keep file size small

        // Step 4: Save the OCR result as a searchable PDF
        String output = "YOUR_DIRECTORY/document.pdf";
        engine.saveAsSearchablePdf(output, pdfOpts);

        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF created at: " + output);
    }
}
```

將此程式碼貼到 IDE 中，將 `YOUR_DIRECTORY` 替換為實際路徑，然後執行。若設定正確，你將得到一個因圖像壓縮與停用字型嵌入而輕量的 **可搜尋 PDF**。

## 結論

我們剛剛已完整說明如何在 Java 中使用 Aspose OCR **建立可搜尋 PDF** 檔案。從初始化引擎、執行 OCR、調整 **在 PDF 中壓縮圖像** 與 **停用 PDF 嵌入字型**，到最終儲存可搜尋的文件——每一步都說明了背後的原因。

準備好接受下一個挑戰了嗎？試著加入 OCR 語言套件、批次處理整個資料夾，或在 PDF 上加註解。你剛掌握的基礎將讓這些擴充變得輕而易舉。

有任何問題或想分享自己的技巧嗎？在下方留言，祝編程愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通其他 API 功能，並在專案中探索替代實作方式。

- [辨識 PDF 文字 – 使用 Aspose.OCR for Java 的 OCR 操作](/ocr/english/java/ocr-operations/)
- [在 Aspose.OCR for Java 中辨識 PDF 文件](/ocr/english/java/ocr-operations/recognize-pdf/)
- [如何在 .NET 使用 Aspose.OCR 進行 PDF OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}