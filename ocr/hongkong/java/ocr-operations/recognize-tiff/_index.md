---
date: 2026-09-03
description: 了解如何使用 Java OCR 函式庫從 TIFF 圖片擷取文字，並將其轉換為可搜尋的內容。逐步指南，包含設定、程式碼與最佳實踐。
keywords:
- java ocr library
- how to extract tiff
- process tiff images
- convert tiff searchable
- java ocr tutorial
- author: Aspose
  dateModified: '2026-09-03'
  description: Learn how to use a Java OCR library to extract text from TIFF images
    and convert them into searchable content.
  headline: How to use a Java OCR library to extract TIFF text
  type: TechArticle
- description: Learn how to use a Java OCR library to extract text from TIFF images
    and convert them into searchable content.
  name: How to use a Java OCR library to extract TIFF text
  steps:
  - name: Set Up Your Project
    text: Create a new Java project (IDE or command line) and place the Aspose.OCR
      JAR on the classpath.
  - name: Define Your Document Directory and Image Path
    text: Set `dataDir` to the folder that contains your TIFF files, e.g., `String
      dataDir = "C:/Images/";`.
  - name: Create AsposeOCR Instance
    text: Instantiate `AsposeOCR ocr = new AsposeOCR();` to access OCR functions.
  - name: Set Recognition Options
    text: Create a `DocumentRecognitionSettings` object to specify language, mode,
      and output options.
  - name: Perform Text Recognition
    text: The method returns an `OcrResult` containing the extracted text and metadata.
  - name: Print Recognition Results
    text: Iterate over the `OcrResult` fields to display the recognized text.
  - name: Implement the `printResult` Method
    text: The `printResult` helper formats and outputs the OCR data to the console.
  type: HowTo
- questions:
  - answer: It means converting the visual characters inside a TIFF image into editable,
      searchable text using OCR.
    question: What does “extract text from tiff” mean?
  - answer: Aspose.OCR for Java, available from the official Aspose site.
    question: Which library should I use?
  - answer: Yes—use a free trial for evaluation, then purchase a commercial license
      for deployment.
    question: Is a license required for production?
  - answer: Absolutely; the `RecognizeTiff` method processes all pages automatically.
    question: Can I handle multi‑page TIFFs?
  - answer: Java 8 or later is fully supported.
    question: What Java version is supported?
  type: FAQPage
lastmod: 2026-09-03
linktitle: OCR 識別 TIFF 圖片（Aspose.OCR for Java）
og_description: 了解如何使用 Java OCR 函式庫從 TIFF 圖片擷取文字，並將其轉換為可搜尋的內容。逐步指南，包含設定與程式碼。
og_image_alt: Screenshot of Java OCR library extracting text from a TIFF file
og_title: 如何使用 Java OCR 函式庫擷取 TIFF 文字（55 個字元）
schemas:
- author: Aspose
  dateModified: '2026-09-03'
  description: Learn how to use a Java OCR library to extract text from TIFF images
    and convert them into searchable content. Step‑by‑step guide with setup, code,
    and best practices.
  headline: How to use a Java OCR library to extract TIFF text
  type: TechArticle
- description: Learn how to use a Java OCR library to extract text from TIFF images
    and convert them into searchable content. Step‑by‑step guide with setup, code,
    and best practices.
  name: How to use a Java OCR library to extract TIFF text
  steps:
  - name: set up your project
    text: Create a new Java project (IDE or command line) and place the Aspose.OCR
      JAR on the classpath.
  - name: define your document directory and image path
    text: Set `dataDir` to the folder that contains your TIFF files, e.g., `String
      dataDir = "C:/Images/";`.
  - name: create AsposeOCR instance
    text: Instantiate `AsposeOCR ocr = new AsposeOCR();` to access OCR functions.
  - name: set recognition options
    text: DocumentRecognitionSettings configures OCR parameters such as language,
      mode, and output format. Create a `DocumentRecognitionSettings` object to specify
      language, mode, and output options.
  - name: perform text recognition
    text: OcrResult holds the OCR output, including plain text, confidence scores,
      and layout information. The method returns an `OcrResult` containing the extracted
      text and metadata.
  - name: print recognition results
    text: '`OcrResult` encapsulates the recognized text, confidence scores, and layout
      metadata returned by the OCR engine. Iterate over the `OcrResult` fields to
      display the recognized text.'
  - name: implement the `printResult` method
    text: The `printResult` helper formats and outputs the OCR data to the console.
  type: HowTo
- questions:
  - answer: It means converting the visual characters inside a TIFF image into editable,
      searchable text using OCR.
    question: What does “extract text from tiff” mean?
  - answer: Aspose.OCR for Java, available from the official Aspose site.
    question: Which library should I use?
  - answer: Yes—use a free trial for evaluation, then purchase a commercial license
      for deployment.
    question: Is a license required for production?
  - answer: Absolutely; the `RecognizeTiff` method processes all pages automatically.
    question: Can I handle multi‑page TIFFs?
  - answer: Java 8 or later is fully supported.
    question: What Java version is supported?
  type: FAQPage
second_title: Aspose.OCR Java API
tags:
- java ocr
- tiff extraction
- aspose.ocr
- searchable tiff
- ocr tutorial
title: 如何使用 Java OCR 函式庫擷取 TIFF 文字
url: /zh-hant/java/ocr-operations/recognize-tiff/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.OCR for Java 從 TIFF 圖像提取文字

在本完整指南中，您將學習如何使用 Aspose.OCR for Java **從 tiff 檔案提取文字**。無論您需要用於文件管理系統的可搜尋 PDF，或是想索引掃描的合約，本教學都會一步步帶領您——從安裝函式庫到列印 OCR 結果——讓您在數分鐘內開始處理 TIFF 圖像。

## 快速解答
- **什麼是「從 tiff 提取文字」的意思？** 它指的是使用 OCR 將 TIFF 圖像內的視覺字元轉換為可編輯、可搜尋的文字。  
- **我應該使用哪個函式庫？** Aspose.OCR for Java，可從官方 Aspose 網站取得。  
- **在正式環境是否需要授權？** 是——可先使用免費試用版評估，之後購買商業授權以部署。  
- **我能處理多頁 TIFF 嗎？** 當然可以；`RecognizeTiff` 方法會自動處理所有頁面。  
- **支援哪個 Java 版本？** 完全支援 Java 8 及以上版本。

## 什麼是從 tiff 提取文字？
*從 tiff 提取文字* 是一種 OCR 操作，會讀取 TIFF 檔案中的像素資料，並將底層字元以 Unicode 文字回傳。這使得全文搜尋、索引與後續資料分析成為可能。透過將掃描圖像轉換為機器可讀的字串，您可以將內容整合至資料庫、套用自然語言處理，或產生可搜尋的 PDF 以供保存。

## 為什麼使用 Aspose.OCR for Java？
Aspose.OCR 支援 **超過 50 種輸入與輸出格式**，且可在不將整份文件載入記憶體的情況下處理高達 **500 MB** 的 TIFF 檔案。此 API 為純 Java，**無外部相依性**，且對印刷英文文字的即時辨識精度超過 **95 %**。這些可量化的能力使其成為企業級文件流程的可靠選擇。

## 前置條件
- 已安裝 Java Development Kit (JDK) 8 或更新版本。  
- 已下載 Aspose.OCR for Java 函式庫並加入至專案。可從官方下載頁面 **[Aspose OCR Java download page](https://releases.aspose.com/ocr/java/)** 取得。  
- 一張包含您想提取文字的 TIFF 圖像。  
-（可選）若您偏好手動檔案處理，需具備使用 `java.io` 讀取 TIFF 檔案的基本知識。

## 匯入套件
`AsposeOCR` 是 Aspose.OCR for Java 函式庫中提供 OCR 功能的主要類別。  
`AsposeOCR` 類別與相關設定位於 `com.aspose.ocr` 命名空間。請在來源檔案的最上方匯入它們。

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.DetectAreasMode;
import com.aspose.ocr.DocumentRecognitionSettings;
import com.aspose.ocr.Language;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionResult.LinesResult;
import com.aspose.ocr.pdf.AsposeOCRPdf;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.util.ArrayList;
```

## 如何使用 Java OCR 函式庫從 TIFF 圖像提取文字？
`recognizeTiff()` 方法會處理 TIFF 檔案並回傳 OCR 結果。使用 `new AsposeOCR()` 載入您的 TIFF，然後呼叫 `recognizeTiff()`——此單一呼叫會讀取每一頁、套用語言特定模型，並回傳包含純文字、段落版面與信心分數的 `OcrResult` 物件。這個兩步驟的模式適用於大多數掃描文件，且只需少量 Java 程式碼。

### 步驟 1：設定專案
建立一個新的 Java 專案（IDE 或命令列），並將 Aspose.OCR JAR 放置於 classpath 中。

### 步驟 2：定義文件目錄與影像路徑
將 `dataDir` 設為包含 TIFF 檔案的資料夾，例如 `String dataDir = "C:/Images/";`。

```java
String dataDir = "Your Document Directory";
String file = dataDir + "multipage.tif";
```

### 步驟 3：建立 AsposeOCR 實例
實例化 `AsposeOCR ocr = new AsposeOCR();` 以存取 OCR 功能。

```java
AsposeOCR api = new AsposeOCR();
```

### 步驟 4：設定辨識選項
DocumentRecognitionSettings 用於設定 OCR 參數，如語言、模式與輸出格式。  
建立 `DocumentRecognitionSettings` 物件以指定語言、模式與輸出選項。

```java
DocumentRecognitionSettings settings = new DocumentRecognitionSettings(2);
settings.setDetectAreasMode(DetectAreasMode.PHOTO);
```

### 步驟 5：執行文字辨識
OcrResult 包含 OCR 輸出，包括純文字、信心分數與版面資訊。  
此方法回傳包含提取文字與中繼資料的 `OcrResult`。

```java
ArrayList<RecognitionResult> result = api.RecognizeTiff(file, settings);
```

### 步驟 6：列印辨識結果
`OcrResult` 封裝了 OCR 引擎回傳的已辨識文字、信心分數與版面中繼資料。  
遍歷 `OcrResult` 的欄位以顯示已辨識的文字。

```java
for (RecognitionResult r : result) {
    printResult(r);
}
```

### 步驟 7：實作 `printResult` 方法
`printResult` 輔助函式會格式化並將 OCR 資料輸出至主控台。

```java
static void printResult(RecognitionResult result) {
    // Your implementation here
}
```

## 如何使用 Java OCR 函式庫處理 TIFF 圖像？
在設定好 `DocumentRecognitionSettings` 後，將檔案路徑傳入 `recognizeTiff()` 即可處理 TIFF 圖像；引擎會自動處理多頁檔案，並為每一頁回傳結構化結果。它亦會自動偵測影像解析度並套用適當的前處理以提升精度。此方法免除手動分頁的需求，並加速批次工作流程。

## 如何將 TIFF 轉換為可搜尋的內容？
透過 Aspose.OCR 提取文字後，將結果嵌入 PDF 或儲存至資料庫，即可將 TIFF 轉換為可搜尋的內容。提取的 Unicode 字串可被搜尋引擎索引，實現對掃描檔案的全文查詢。

## 常見問題與解決方案

| 問題 | 發生原因 | 解決方法 |
|-------|----------------|------------|
| **未返回文字** | 檔案路徑錯誤或不支援的 TIFF 壓縮。 | 確認 `dataDir` 路徑，確保 TIFF 未損毀，並盡可能使用未壓縮的 TIFF。 |
| **雜訊字元** | 解析度過低或對比度不足。 | 在呼叫 `recognizeTiff` 前先前處理影像（將 DPI 提升至 300+，增強對比度）。 |
| **不支援的語言** | `DocumentRecognitionSettings` 中未設定語言。 | 在辨識前加入 `settings.setLanguage(Language.SPANISH);`（或您目標的語言）。 |

## 常見問答

**Q1: Aspose.OCR 是否適合辨識多語言文字？**  
A: 是，Aspose.OCR 支援超過 60 種語言，您可在 `DocumentRecognitionSettings` 中設定目標語言。

**Q2: 我可以將 Aspose.OCR 整合到 Web 服務中嗎？**  
A: 當然可以。此函式庫可在任何相容 Java 的伺服器上執行，您亦可透過 REST 端點公開 OCR 功能。

**Q3: 有哪些授權方案可供選擇？**  
A: 您可查看授權方案並於 **[Aspose OCR licensing page](https://purchase.aspose.com/buy)** 購買授權。

**Q4: 是否提供免費試用？**  
A: 有——可從 **[Aspose OCR trial download page](https://releases.aspose.com/)** 下載試用版，免費評估全部功能。

**Q5: 我可以在哪裡取得社群支援？**  
A: 加入 **[Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)** 討論區，取得技巧、程式碼片段與除錯協助。

**最後更新：** 2026-09-03  
**測試環境：** Aspose.OCR for Java 24.11 (latest at time of writing)  
**作者：** Aspose

## 相關教學

- [提取文字圖像 – Aspose.OCR for Java OCR 基礎](/ocr/java/ocr-basics/)
- [在 Aspose.OCR for Java 中辨識 PDF 文件的 OCR](/ocr/java/ocr-operations/recognize-pdf/)
- [使用 Aspose.OCR 偵測區域模式在 Java 中提取圖像文字](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}