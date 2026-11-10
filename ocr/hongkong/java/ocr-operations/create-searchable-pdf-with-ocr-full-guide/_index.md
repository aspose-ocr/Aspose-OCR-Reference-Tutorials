---
category: general
date: 2026-06-22
description: 使用 Java 的光學文字辨識 (OCR) 建立可搜尋的 PDF。了解如何停用壓縮，並快速將掃描圖像 PDF 轉換為可搜尋的 PDF。
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- ocr to searchable pdf
- how to disable compression
- pdf without compression
language: zh-hant
og_description: 使用 Java 的 OCR 建立可搜尋的 PDF。本指南說明如何停用壓縮、轉換掃描圖像 PDF，並產生未壓縮的 PDF。
og_title: 使用 OCR 建立可搜尋的 PDF – 完整 Java 教學
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  headline: Create Searchable PDF with OCR – Full Guide
  type: TechArticle
- description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  name: Create Searchable PDF with OCR – Full Guide
  steps:
  - name: Set the output format to `PDF_SEARCHABLE`.
    text: Set the output format to `PDF_SEARCHABLE`.
  - name: Turn off PDF compression with `PdfCompression.NONE`.
    text: Turn off PDF compression with `PdfCompression.NONE`.
  - name: Run OCR and capture the `PdfDocument`.
    text: Run OCR and capture the `PdfDocument`.
  - name: Save the file to disk.
    text: Save the file to disk.
  type: HowTo
tags:
- OCR
- PDF
- Java
- Document Processing
title: 使用 OCR 製作可搜尋的 PDF – 完整指南
url: /zh-hant/java/ocr-operations/create-searchable-pdf-with-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 OCR 建立可搜尋 PDF – 完整指南

是否曾需要從一批掃描圖像 **建立可搜尋 PDF**，卻不確定要調整哪些設定？你並非唯一遇到此問題的人——大多數開發者在輸出變成龐大且無法閱讀的檔案時，都會卡在同一個障礙。  

在本教學中，我們將示範一個乾淨、端對端的範例，完整說明如何使用 Java OCR 引擎 **建立可搜尋 PDF**、**轉換掃描圖像 PDF**，以及最關鍵的 **如何停用壓縮**，讓最終檔案保持原始尺寸。完成後，你將擁有可直接執行的程式碼片段，並清楚了解每個設定為何重要。

## 您將學習到

* 如何設定 OCR 引擎以 **ocr to searchable pdf**。  
* 為何要關閉 PDF 壓縮，以及如何取得 **pdf without compression**。  
* 完整的 Java 程式，將掃描圖像執行 OCR 後儲存為 **searchable PDF**。  
* 處理多頁掃描或低解析度來源等邊緣案例的技巧。  

**Prerequisites** – 已安裝 Java 8 以上、相容的 OCR SDK（範例使用 ABBYY FineReader Engine API，但概念同樣適用於任何提供 `setOutputFormat` 與 `setPdfCompression` 的函式庫）。使用 IntelliJ IDEA 或 Eclipse 等 IDE 會更方便，但簡易文字編輯器亦可。

---

![建立可搜尋 PDF 工作流程](image-placeholder.png "示意圖顯示從掃描圖像到最終 PDF 的建立可搜尋 PDF 流程")

## 步驟 1：將 OCR 引擎設定為 **建立可搜尋 PDF**

首先，你必須告訴 OCR 引擎你期望的輸出類型。預設情況下許多 SDK 只會輸出純文字或光柵 PDF，這些檔案無法搜尋。切換格式即可為你完成繁重的工作。

```java
// Step 1: Tell the engine we want a searchable PDF
engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

*Why this matters*: `PDF_SEARCHABLE` 旗標指示引擎在掃描圖像下方嵌入一層隱形文字層。搜尋工具便能索引文件，使其行為如同在 Adobe Reader 中開啟的任何原生 PDF。

## 步驟 2：停用壓縮 – 正確的 **如何停用壓縮**

如果跳過此步驟，引擎會壓縮每一頁以節省空間，但壓縮可能會模糊細節——在之後需要擷取高解析度圖像時尤其成問題。

```java
// Step 2: Turn off PDF compression to keep original image quality
engine.getConfig().setPdfCompression(PdfCompression.NONE);
```

**Pro tip**: 當你計畫保存法律文件或醫療掃描（每個像素都很重要）時，必須停用壓縮。產生的檔案雖較大，但能保留原始尺寸與清晰度。

## 步驟 3：執行 OCR 並取得產生的文件

現在引擎已知道要輸出什麼以及如何處理圖像，你可以執行辨識。此呼叫會回傳一個 `PdfDocument` 物件，可直接儲存或進一步操作。

```java
// Step 3: Run OCR and capture the searchable PDF in memory
PdfDocument pdf = engine.recognizeToPdf();
```

*What’s happening under the hood?* 引擎會逐頁處理輸入圖像、執行字元辨識，並將隱形文字層貼合於圖像上。若有多頁，會自動串接。

## 步驟 4：將 **可搜尋 PDF** 儲存至磁碟

最後，將記憶體中的 PDF 寫入檔案。選擇一個你有寫入權限的路徑，並為檔案取一個具意義的名稱。

```java
// Step 4: Persist the searchable PDF on disk
pdf.save("YOUR_DIRECTORY/searchable.pdf");
```

當你在檢視器中開啟 `searchable.pdf` 時，會發現即使可見內容仍是原始掃描圖像，你仍能選取並搜尋文字。

### 完整範例

以下是一個自包含的 Java 類別，將上述四個步驟整合在一起。隨意複製貼上、調整輸入路徑，即可直接執行。

```java
import com.abbyy.ocrsdk.Engine;
import com.abbyy.ocrsdk.OcrOutputFormat;
import com.abbyy.ocrsdk.PdfCompression;
import com.abbyy.ocrsdk.PdfDocument;

/**
 * Demonstrates how to create searchable PDF from scanned images.
 * This example uses the ABBYY FineReader Engine Java API.
 */
public class SearchablePdfCreator {

    public static void main(String[] args) {
        // ---- 1. Initialize the OCR engine -------------------------------------------------
        Engine engine = new Engine();
        // (Assume license activation and engine initialization are handled elsewhere)

        // ---- 2. Configure output to be a searchable PDF ----------------------------------
        engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);

        // ---- 3. Disable compression for a PDF without compression -------------------------
        engine.getConfig().setPdfCompression(PdfCompression.NONE);

        // ---- 4. Load the scanned image(s) --------------------------------------------------
        // For simplicity, we let the engine auto‑detect images in the working folder.
        // You could also call engine.addImage("path/to/image.tif") for explicit control.
        engine.addImage("YOUR_DIRECTORY/scanned-page.tif");

        // ---- 5. Perform OCR and retrieve the PDF -----------------------------------------
        PdfDocument pdf = engine.recognizeToPdf();

        // ---- 6. Save the result -----------------------------------------------------------
        pdf.save("YOUR_DIRECTORY/searchable.pdf");

        System.out.println("✅ Searchable PDF created successfully at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Expected output** – 執行程式後，你會在主控台看到上述訊息，且 `searchable.pdf` 會出現在 `YOUR_DIRECTORY`。在任何 PDF 閱讀器中開啟後，你應能：

* 標記文字。  
* 使用內建搜尋（Ctrl + F）定位關鍵字。  
* 如有需要，匯出隱形文字層。

---

## 為何停用壓縮？了解 **無壓縮 PDF**

你可能會想，「壓縮不是永遠都好嗎？」答案其實很微妙：

| 情況 | 保留壓縮 (`NORMAL`) | 停用壓縮 (`NONE`) |
|-----------|-----------------------------|------------------------------|
| 法律合約的存檔 | ❌ 可能改變像素真實度 | ✅ 確保原始外觀 |
| 大量低解析度掃描 | ✅ 節省儲存空間 | ❌ 增加檔案大小卻無效益 |
| 需要在極小字體上取得 OCR 準確度 | ❌ 使細節模糊 | ✅ 保留每一筆畫 |

簡而言之，**如何停用壓縮**是儲存空間與影像忠實度之間的取捨。對於大多數只需要搜尋文字而非重新列印圖像的可搜尋 PDF 工作流程，關閉壓縮是最安全的選擇。

## 直接轉換 **掃描圖像 PDF**

有時你已經有一個只包含掃描圖像的 PDF（「僅圖像 PDF」）。若要 **convert scanned image pdf** 成為可搜尋版本，只要將整個 PDF 傳給引擎，而非單獨的圖像：

```java
engine.addPdf("YOUR_DIRECTORY/scanned-image-only.pdf");
PdfDocument searchable = engine.recognizeToPdf();
searchable.save("YOUR_DIRECTORY/searchable-from-pdf.pdf");
```

相同的設定旗標（`PDF_SEARCHABLE` 與 `PdfCompression.NONE`）仍然適用，因而即使從 PDF 容器開始，也能得到 **pdf without compression**。

## 常見陷阱與避免方法

* **Forgot to set the output format** – 引擎預設為光柵 PDF，無法搜尋。務必在呼叫 `recognizeToPdf()` 前先執行 `setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE)`。  
* **Running out of memory on large batches** – 以批次方式載入與處理頁面，或使用 SDK 提供的串流 API。  
* **Incorrect file paths** – 使用絕對路徑或確保工作目錄正確設定，否則 `pdf.save()` 會拋出 `IOException`。  
* **License not activated** – 大多數商業 OCR SDK 需要有效授權；若缺少授權，引擎會拋出執行時例外。

---

## 結論

你現在已擁有完整、可直接執行的解決方案，示範了 **how to create searchable PDF**、**convert scanned image PDF**，以及精確的 **how to disable compression**，從而產生 **pdf without compression**。關鍵步驟如下：

1. 將輸出格式設定為 `PDF_SEARCHABLE`。  
2. 使用 `PdfCompression.NONE` 停用 PDF 壓縮。  
3. 執行 OCR 並取得 `PdfDocument`。  
4. 將檔案儲存至磁碟。

接下來，你可以嘗試字型、加入浮水印，或批次處理整個資料夾。若你想了解如何加入 OCR 語言套件、處理多頁 TIFF，或將此工作流程整合至 Web 服務，請關注我們即將推出的「OCR language selection in Java」與「Streaming OCR for large document sets」教學。

有任何問題或發現卡關的地方嗎？歡迎在下方留言——祝開發順利，享受全新可搜尋的 PDF 吧！

## 接下來您可以學習什麼？

以下教學與本指南所示技術緊密相關，能幫助你進一步掌握 API 功能並探索其他實作方式：

- [辨識 PDF 文字 – 使用 Aspose.OCR for Java 的 OCR 操作](/ocr/english/java/ocr-operations/)
- [在 Aspose.OCR for Java 中 OCR 辨識 PDF 文件](/ocr/english/java/ocr-operations/recognize-pdf/)
- [將影像轉換為 PDF (C#) – 儲存多頁 OCR 結果](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}