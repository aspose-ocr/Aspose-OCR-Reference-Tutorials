---
category: general
date: 2026-01-02
description: 使用 Aspose OCR 從掃描的圖像 PDF 建立可搜尋的 PDF。了解如何設定 OCR 語言、嵌入文字層 PDF 以及套用高壓縮 PDF
  選項。
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: zh-hant
og_description: 快速建立可搜尋的 PDF。本指南說明如何將掃描圖像 PDF 轉換、嵌入文字層、設定 OCR 語言以及啟用高壓縮 PDF。
og_title: 使用 Aspose OCR 建立可搜尋 PDF – 完整指南
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: 使用 Aspose OCR 建立可搜尋 PDF – 步驟指南
url: /zh-hant/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立可搜尋 PDF – 完整程式教學

有沒有需要 **建立可搜尋 PDF** 檔案，卻不知道從哪裡開始？你並不孤單。在許多以文件為主的工作流程中，只有影像的 PDF 會成為搜尋與索引的死路。  

好消息是，使用 Aspose OCR 只要幾行 Java 程式碼，就能 **將掃描影像 PDF** 轉換成完整可搜尋的文件。本教學將一步步說明——初始化 OCR 引擎、設定高壓縮 PDF、嵌入隱藏文字層，甚至選擇正確的 OCR 語言。

閱讀完本指南後，你將擁有一個可執行的程式，產生可搜尋的 PDF，這個檔案可以直接投入任何搜尋引擎或文件管理系統，毫無障礙。

---

## 建立可搜尋 PDF – 概觀

在深入程式碼前，先說明「建立可搜尋 PDF」到底是什麼意思。可搜尋的 PDF 包含兩個平行層：

1. **視覺層** – 原始掃描影像（或渲染頁面）。  
2. **文字層** – 隱形但機器可讀的文字，由 OCR 抽取。

當你在 Adobe Reader 中開啟此類 PDF 並選取文字時，實際上操作的是隱藏的文字層，而非圖片。這種雙層結構正是 **embed text layer PDF** 功能的核心。

---

## 使用 Aspose OCR 轉換掃描影像 PDF

首先，你需要一張掃描影像（PNG、JPEG、TIFF），想要將它變成 PDF。Aspose OCR 能讀取該影像、執行 OCR，並將結果交給 PDF 寫入器。

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**為什麼這樣可行：**  
- `setCreateSearchablePdf(true)` 告訴 Aspose 產生隱藏文字層，滿足 **embed text layer pdf** 的需求。  
- `setCompressionLevel(9)` 將檔案推向 **high compression pdf** 範圍，在不犧牲 OCR 準確度的前提下縮小最終大小。  
- `RecognitionLanguage.ENGLISH` 參數示範了如何 **set OCR language**；你可以依來源材料改成法文、德文等。

---

## 高壓縮 PDF 設定

大型掃描 PDF 很快就會膨脹到數百 MB。Aspose 提供簡易的壓縮 API，直接作用於 PDF 層級。`setCompressionLevel` 方法接受 0（無壓縮）到 9（最高壓縮）的數值。

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

小技巧：

- **使用無損影像格式**（PNG）處理文字密集的掃描；照片則建議使用 JPEG。  
- 若嵌入自訂字型，**啟用字型子集化**——Aspose 在建立可搜尋 PDF 時會自動執行。  
- **每次變更後測試輸出大小**；有時 8 級壓縮即可減少約 10% 體積，且品質與 9 級相差無幾。

---

## 嵌入文字層 PDF 以實現搜尋功能

如果省略 `setCreateSearchablePdf(true)` 呼叫，產生的檔案看起來沒問題，但無法搜尋內容。隱藏文字層是透過將每個辨識出的字元映射到頁面上的位置而產生的。

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**注意事項：**  

- **多語言文件** – 可能需要分別執行兩次 OCR（每種語言一次），再合併文字層。  
- **複雜版面**（表格、多欄） – Aspose 表現不錯，但仍建議使用能顯示隱藏文字的 PDF 檢視器（例如 Adobe Acrobat 的「編輯 PDF」模式）再次確認。

---

## 設定 OCR 語言以提升辨識準確度

OCR 引擎的準確度取決於你告訴它的語言。Aspose 內建多種語言，也支援自行加入語言套件。

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**何時需要變更語言：**  

- 文件包含 **非拉丁文字**（西里爾文、阿拉伯文）時，切換為相應的 `RecognitionLanguage`。  
- 混合語言頁面 – 可分別以不同語言呼叫 `recognizeImageAndSave`，之後再合併 PDF。

---

## 執行完整範例

以下是完整、可直接執行的程式。將佔位路徑換成實際檔案位置，確保 Aspose OCR JAR 已加入 classpath，然後執行。

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**預期輸出：** 執行程式時，主控台會印出：

```
Searchable PDF created.
```

在任何 PDF 檢視器中開啟 `searchable.pdf`，嘗試選取文字，你會看到隱藏層在運作。你已成功 **create searchable pdf** 從掃描影像。

---

![create searchable pdf example](image-placeholder.png "create searchable pdf example")

*上圖（佔位）通常會顯示 PDF 檢視器中可選取文字的掃描頁面。*

---

## 結論

我們已說明如何使用 Aspose OCR **建立可搜尋 PDF** 檔案的全部步驟：

- 初始化 OCR 引擎。  
- 透過 `recognizeImageAndSave` **Convert scanned image PDF**，將 PNG/JPEG 輸入。  
- 使用 `setCreateSearchablePdf(true)` **embed text layer PDF**。  
- 以 `setCompressionLevel(9)` 產生 **high compression PDF**，保持檔案輕量。  
- 選擇適當的 `RecognitionLanguage` 以 **set OCR language**，達到最高辨識精度。

接下來，你可以嘗試批次處理、不同語言，或將多頁掃描合併成單一可搜尋 PDF。同樣的模式也適用於西班牙文、日文等語言——只要換掉 `RecognitionLanguage` 列舉即可。

如有任何問題，歡迎留言討論，祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}