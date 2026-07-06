---
date: 2026-06-29
description: 了解如何使用 Aspose.OCR for .NET 保存 OCR 結果 – 步驟說明如何儲存 OCR 輸出、將影像轉換為可搜尋的 PDF、從
  PNG 提取文字，並匯出為 DOCX、TXT、PDF 或 XLSX。
keywords:
- how to save ocr
- image to searchable pdf
- extract text from png
- create searchable pdf
- ocr result to txt
linktitle: 如何將 OCR 結果儲存為文件
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Learn how to save OCR results with Aspose.OCR for .NET – a step‑by‑step
    guide on how to save ocr output, convert image to searchable pdf, extract text
    from png, and export to DOCX, TXT, PDF, or XLSX.
  headline: How to Save OCR Result as Document
  type: TechArticle
- description: Learn how to save OCR results with Aspose.OCR for .NET – a step‑by‑step
    guide on how to save ocr output, convert image to searchable pdf, extract text
    from png, and export to DOCX, TXT, PDF, or XLSX.
  name: How to Save OCR Result as Document
  steps:
  - name: Initialize Aspose.OCR
    text: AsposeOcr is the primary class that performs OCR operations. Set the path
      to your working directory and create an instance of the OCR engine.
  - name: Recognize Image
    text: RecognitionResult holds the text and layout information extracted from the
      image. Pass the image file (e.g., a PNG) to the recognizer. This is where we
      **recognize text images** and turn them into a `RecognitionResult`.
  - name: Save Result in Different Formats
    text: Now we export the recognized text. Choose the format that fits your workflow—whether
      you need to **convert image to searchable pdf**, **extract text from png**,
      or generate a spreadsheet.
  - name: Display Success Message
    text: A simple console message confirms that the process completed without errors.
  type: HowTo
- questions:
  - answer: It refers to persisting the text recognized from an image into a file
      format like DOCX, PDF, etc.
    question: What does “how to save ocr” mean?
  - answer: DOCX, TXT, PDF, and XLSX are supported out‑of‑the‑box.
    question: Which formats can I export to?
  - answer: A free trial works for evaluation; a commercial license is required for
      production use.
    question: Do I need a license?
  - answer: Yes—save the OCR result as PDF to get a searchable PDF document.
    question: Can I convert image to PDF directly?
  - answer: Absolutely; you can **extract text from PNG** images with the same API.
    question: Is PNG supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
title: 如何將 OCR 結果儲存為文件
url: /zh-hant/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何將 OCR 結果儲存為文件

## 介紹

在本教學中，您將了解 **儲存 OCR** 輸出使用 Aspose.OCR for .NET。我們將示範辨識圖像中的文字，然後將文字轉換為常見的文件格式，如 DOCX、 TXT、 PDF 和 XLSX。完成後，您即可自動從圖片中擷取資料，並將其儲存為可搜尋、可編輯的檔案——非常適合用於歸檔、報告或後續處理。

## 快速解答
- **「如何儲存 OCR」是什麼意思？** 它指的是將從圖像辨識出的文字持久化為 DOCX、PDF 等檔案格式。  
- **我可以匯出哪些格式？** 支援直接匯出為 DOCX、TXT、PDF 以及 XLSX。  
- **我需要授權嗎？** 免費試用可用於評估；正式使用則需商業授權。  
- **我可以直接將圖像轉換為 PDF 嗎？** 可以——將 OCR 結果儲存為 PDF，即可得到可搜尋的 PDF 文件。  
- **支援 PNG 嗎？** 當然可以；您可以使用相同的 API **從 PNG 圖像擷取文字**。

## 什麼是 OCR 以及為何要將結果儲存為文件？

OCR（Optical Character Recognition）將圖像中的印刷或手寫文字轉換為機器可讀的字串。將這些字串儲存為文件，可讓您建立 **可搜尋的 PDF**、填寫試算表、產生可編輯的報告，或存檔純文字日誌。Aspose.OCR 能在一步之內將掃描圖片轉換為 **可搜尋的 PDF**，省去額外的 PDF‑creation tools。

## 前置條件

在開始之前，請確保您已具備：

- 已安裝 Aspose.OCR for .NET。您可在 **[此處](https://releases.aspose.com/ocr/net/)** 下載。  
- 在您的電腦上建立一個資料夾，用於存放來源圖像與輸出文件。請在程式碼中將 `dataDir` 變數更新為指向該資料夾的路徑。

## 匯入命名空間

我們需要一些 .NET 命名空間來存取檔案 I/O 與 Aspose OCR 類別。

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### 步驟 1：初始化 Aspose.OCR

AsposeOcr 是執行 OCR 操作的主要類別。設定工作目錄的路徑，並建立 OCR 引擎的實例。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### 步驟 2：辨識圖像

RecognitionResult 保存從圖像中擷取的文字與版面資訊。將圖像檔案（例如 PNG）傳遞給辨識器。這裡我們 **辨識文字圖像** 並將其轉換為 `RecognitionResult`。

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### 步驟 3：以不同格式儲存結果

現在我們匯出辨識出的文字。選擇符合工作流程的格式——無論是 **將圖像轉換為可搜尋的 PDF**、**從 PNG 擷取文字**，或是產生試算表。

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### 步驟 4：顯示成功訊息

簡單的主控台訊息可確認程序已順利完成，且未發生錯誤。

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## 常見陷阱與技巧

- **檔案路徑：** 請始終使用絕對路徑，或確保 `dataDir` 以路徑分隔符（`\` 或 `/`）結尾。  
- **圖像品質：** 高解析度的圖像可提升辨識準確度；建議進行前處理（去斜、去噪）以獲得更佳結果。  
- **授權模式：** 評估模式下，輸出可能會帶有浮水印；請套用有效授權以移除浮水印。

## 常見問題

**Q1. Aspose.OCR 是否相容於不同的圖像格式？**  
A1: 是的，Aspose.OCR 支援超過 30 種圖像格式，包括 PNG、JPEG、TIFF、BMP 以及 GIF，確保在 OCR 任務中的彈性。

**Q2. 我可以自訂辨識設定以提升準確度嗎？**  
A2: 當然可以！Aspose.OCR 提供 `RecognitionSettings`，讓您依據特定需求微調 OCR 流程。

**Q3. 是否提供免費試用？**  
A3: 有的，您可透過 **[此處](https://releases.aspose.com/)** 開始免費試用。

**Q4. 我該如何取得 Aspose.OCR 的臨時授權？**  
A4: 可於 **[此處](https://purchase.aspose.com/temporary-license/)** 取得臨時授權。

**Q5. 我可以在哪裡尋求協助或加入社群？**  
A5: 請前往 **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** 加入 Aspose.OCR 社群，獲取支援與討論。

---

**最後更新：** 2026-06-29  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< blocks/products/products-backtop-button >}}

## 相關教學

- [使用 Aspose.OCR .NET 從圖像擷取文字](/ocr/net/image-and-drawing-recognition/)
- [將圖像轉換為 PDF C# – 儲存多頁 OCR 結果](/ocr/net/ocr-optimization/save-multipage-result-as-document/)
- [擷取文字圖像 – OCR 設定](/ocr/net/ocr-settings/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}