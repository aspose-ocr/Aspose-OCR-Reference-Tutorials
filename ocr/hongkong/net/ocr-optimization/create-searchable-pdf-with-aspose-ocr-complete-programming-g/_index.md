---
category: general
date: 2026-05-21
description: 使用 Aspose OCR 建立可搜尋的 PDF，同時提升 OCR 準確度，並學習如何在 C# 中載入影像進行 OCR。一步一步教學。
draft: false
keywords:
- create searchable PDF
- improve OCR accuracy
- load image for OCR
- Aspose OCR C#
- PDF output with OCR
language: zh-hant
og_description: 使用 Aspose OCR 建立可搜尋的 PDF。了解如何提升 OCR 準確度，並在單一可執行範例中載入影像進行 OCR。
og_title: 使用 Aspose OCR 建立可搜尋 PDF – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Create searchable PDF using Aspose OCR while you improve OCR accuracy
    and learn how to load image for OCR in C#. Step‑by‑step tutorial.
  headline: Create Searchable PDF with Aspose OCR – Complete Programming Guide
  type: TechArticle
tags:
- OCR
- Aspose
- PDF
- C#
title: 使用 Aspose OCR 建立可搜尋 PDF – 完整程式設計指南
url: /zh-hant/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 建立可搜尋 PDF – 完整程式指南

是否曾需要 **建立可搜尋的 PDF**，卻不知從何著手？你並不孤單——許多開發者在首次接觸 OCR 專案時都會卡在這裡。好消息是 Aspose OCR 讓整個流程——載入影像、優化圖片以提升辨識效果，最後儲存為可搜尋 PDF——變得相當簡單。

在本指南中，我們將示範一個完整的端對端範例，不僅說明如何 **建立可搜尋 PDF**，同時展示如何 **提升 OCR 準確度** 以及正確的 **載入影像供 OCR 使用** 方法。完成後，你將擁有一個可直接執行的 C# 主控台應用程式，能輸出內嵌原始影像的可搜尋 PDF。

## 你將學到

- 設定 Aspose OCR（含可選的 GPU 加速）  
- 為法文（或任何語言）配置引擎以 **提升 OCR 準確度**  
- 使用 `ImageStream` 正確 **載入影像供 OCR 使用**  
- 建立影像過濾管線，在辨識前清理圖片  
- 將結果儲存為內嵌來源影像的可搜尋 PDF  

不需要除 Aspose OCR 之外的外部相依性，程式碼可在 .NET 6+（或 .NET Framework 4.6+）上執行。現在就開始吧。

---

![Aspose OCR 產生的可搜尋 PDF 範例 – 建立可搜尋 PDF 示例](images/searchable-pdf-sample.png "建立可搜尋 PDF 示例")

## 步驟 1：建立可搜尋 PDF – 啟用 GPU 並設定資源路徑  

如果你有相容的 GPU，開啟它可以大幅加速辨識。即使不使用，其他程式碼仍能正常運作。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// Enable GPU acceleration (optional)
OcrEngine.EnableGpu(true);

// Tell Aspose where to find language data files (offline mode)
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");
```

**為什麼重要：** GPU 加速能減少大量批次的延遲，而設定資源路徑則確保引擎在無網路連線的環境下仍能運作——非常適合 CI 流程或隔離環境。

> **小技巧：** 若你在無頭伺服器上執行，請確認 CUDA 驅動版本與 Aspose OCR 隨附的版本相符；版本不匹配可能導致靜默失敗。

## 步驟 2：提升 OCR 準確度 – 選擇正確的語言  

選擇正確的語言模型是提升準確度的快速方法。此處我們使用法文，你也可以將 `OcrLanguage.French` 換成任何支援的語言。

```csharp
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.French   // improves OCR accuracy for French documents
};
```

**為什麼重要：** 語言特定的字典能協助引擎解決模糊字元（例如 “œ” 與 “oe” 的差異）。若省略此步驟，引擎會預設使用英文，對非英文文字的 **提升 OCR 準確度** 會大幅下降。

## 步驟 3：載入影像供 OCR 使用 – 使用 ImageStream  

現在我們 **載入影像供 OCR 使用**。`ImageStream.FromFile` 輔助方法抽象了原始 bitmap 的處理，支援大多數常見格式（JPG、PNG、TIFF）。

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

**為什麼重要：** 以此方式載入影像可確保 Aspose 取得可高效處理的格式。若直接傳入原始 `Bitmap`，在處理大型檔案時可能會遇到記憶體管理的怪異行為。

## 步驟 4：建立影像過濾管線以提升準確度  

乾淨的影像是成功的一半。以下管線會校正圖片傾斜並去除背景雜訊——兩個常見的 **提升 OCR 準確度** 的殺手。

```csharp
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());   // corrects rotation
filterPipeline.Add(new DenoiseFilter()); // reduces grainy artifacts

// Apply the pipeline and replace the original image
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);
```

**為什麼重要：** 校正傾斜可讓文字行保持水平，去噪則減少錯誤字元的產生。若你的掃描品質特別差，也可以加入 `ContrastFilter` 等其他過濾器。

## 步驟 5：執行 OCR 辨識  

經過前置處理後，我們終於讓引擎發揮魔法。

```csharp
ocrEngine.Recognize();
```

這一行會觸發 Aspose OCR 背後的深度學習模型，將文字填入 `ocrEngine.Text`，同時準備 PDF 輸出。

> **如果文字顯示亂碼該怎麼辦？** 請再次確認第 2 步的語言設定，並考慮在管線中加入 `BinarizeFilter`。

## 步驟 6：將結果儲存為可搜尋 PDF  

最後一步是儲存 **可搜尋 PDF**，讓抽取出的文字隱藏於原始影像之下——這正是法律文件或歸檔需求所需要的。

```csharp
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });
```

**為什麼重要：** `EmbedOriginalImage = true` 能保留掃描圖的視覺完整性，同時提供文字搜尋功能。若設定為 `false`，PDF 只會包含抽取的文字，適合需要輕量化檔案的情境。

### 可選：列印辨識文字與 JSON  

若想檢視原始輸出，可使用以下程式碼將純文字與結構化的 JSON 資料列印出來。

```csharp
Console.WriteLine(ocrEngine.Text);               // plain text
Console.WriteLine(ocrEngine.GetResultAsJson());  // JSON with layout info
```

**預期輸出：** 執行程式後，控制台會顯示法文句子，接著是一個包含文字框座標、信心分數與語言資訊的 JSON 物件。

---

## 完整可執行範例（直接複製貼上）

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// 1️⃣ Enable GPU (optional) and set resources path
OcrEngine.EnableGpu(true);
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");

// 2️⃣ Create and configure the OCR engine (improve OCR accuracy)
var ocrEngine = new OcrEngine { Language = OcrLanguage.French };

// 3️⃣ Load the source image (load image for OCR)
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");

// 4️⃣ Build filter pipeline (deskew + denoise)
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());
filterPipeline.Add(new DenoiseFilter());
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);

// 5️⃣ Recognize text
ocrEngine.Recognize();

// 6️⃣ Save as searchable PDF (create searchable PDF)
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });

// Optional: output text and JSON
Console.WriteLine(ocrEngine.Text);
Console.WriteLine(ocrEngine.GetResultAsJson());
```

執行程式，將 `YOUR_DIRECTORY` 指向包含 `input.jpg` 與 Aspose OCR 資源的資料夾，即可在同一目錄下產生 `output.pdf`。

---

## 結論

現在你已掌握使用 Aspose OCR **建立可搜尋 PDF** 的完整、可投入生產的作法，同時學會 **提升 OCR 準確度** 以及正確的 **載入影像供 OCR 使用**。整個管線——GPU（可選）→語言選擇→影像載入→過濾鏈→辨識→PDF 儲存——涵蓋所有關鍵步驟，讓你能輕鬆套用到其他語言、大批次或不同輸出格式。

接下來可以嘗試將 `PdfSaveOptions` 換成 `DocxSaveOptions`，產生可搜尋的 Word 文件；或加入 `ContrastFilter` 等額外過濾器；甚至將此程式碼整合到 ASP.NET Core API，實現即時 PDF 產生。可能性無限，只要有此基礎，你就能應對任何 OCR 相關挑戰。

有問題或卡關嗎？歡迎留言，祝開發順利！

## 相關教學

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}