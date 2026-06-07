---
category: general
date: 2026-06-06
description: 學習如何建立可搜尋的 PDF 以及使用 OCR 將圖像轉換為 PDF。包括圖層添加、壓縮設定，以及完整的 C# 程式碼。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- how to ocr image
- how to add layer
- how to set compression
language: zh-hant
og_description: 使用 OCR 從圖像建立可搜尋的 PDF。本指南說明如何加入隱藏文字層、設定壓縮，並將圖像轉換為 PDF。
og_title: 建立可搜尋的 PDF – 完整 C# 教學
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  headline: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  name: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - The
      Aspose.OCR and Aspose.Pdf NuGet packages (or any equivalent library that offers
      `OcrEngine` and `PdfSaveOptions`). - A sample image, e.g., `invoice.png`, placed
      in a folder you can reference. - A basic understanding of C# syntax'
  - name: Full Working Example
    text: 'Putting it all together, here’s the complete, ready‑to‑run program:'
  - name: Pro tip
    text: If you need to **convert image to PDF** without OCR (just a plain image
      PDF), set `AddTextLayer = false`. The same `PdfSaveOptions` still lets you control
      compression, which is handy for archiving scanned documents that don’t need
      searchability.
  type: HowTo
tags:
- OCR
- PDF
- C#
- Aspose
title: 從圖像建立可搜尋 PDF – 完整逐步指南
url: /zh-hant/net/ocr-configuration/create-searchable-pdf-from-an-image-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立可搜尋 PDF – 完整 C# 教學

有沒有想過如何在不花費數小時於圖形介面工具的情況下，從掃描的發票**建立可搜尋的 PDF**？你並不孤單。許多開發者在需要將影像轉換成既保留原始外觀又能讓使用者複製或搜尋文字的 PDF 時，常會卡關。

在本教學中，我們將逐步說明**將影像轉換為 PDF**、執行 OCR、加入隱藏文字層，甚至微調壓縮設定的完整流程。完成後，你將擁有一段可直接放入任何 .NET 專案的 C# 程式碼片段。

## 你將學到

- 設定 OCR 引擎，並了解**如何對影像執行 OCR**。
- 使用**如何加入圖層**選項，嵌入可搜尋的文字覆蓋層。
- 套用**如何設定壓縮**，以取得更小的 ZIP 壓縮 PDF。
- 將普通圖片轉換為**建立可搜尋 PDF**的工作流程，並可自動化。
- 常見陷阱與專業技巧，讓你的 PDF 保持清晰且快速。

### 前置條件

- .NET 6.0 或更新版本（程式碼亦相容 .NET Framework 4.7+）。
- Aspose.OCR 與 Aspose.Pdf NuGet 套件（或任何提供 `OcrEngine` 與 `PdfSaveOptions` 的等效函式庫）。
- 一張範例影像，例如 `invoice.png`，放置於可參照的資料夾中。
- 基本的 C# 語法概念——不需要深入的 OCR 知識。

> **專業提示:** 若你使用 Visual Studio，請透過套件管理員主控台安裝套件：  
> `Install-Package Aspose.OCR`  
> `Install-Package Aspose.Pdf`

---

![建立可搜尋 PDF 範例，顯示將發票影像轉換為含隱藏文字層的 PDF](/images/create-searchable-pdf.png)

## 第一步：初始化 OCR 引擎 – **how to ocr image**

首先，我們需要一個能夠從圖片讀取英文文字的 OCR 引擎。`OcrEngine` 類別是入口點；只要設定語言，之後再提供影像即可。

```csharp
using Aspose.OCR;
using Aspose.Pdf;

// Create and configure the OCR engine
OcrEngine engine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

*為何重要:* 使用正確語言初始化引擎可大幅提升辨識準確度。若省略此步，可能會得到亂碼。

## 第二步：載入影像 – **convert image to pdf**

現在我們將引擎指向要處理的檔案。`ImageStream.FromFile` 會讀取位元組並為 OCR 做好準備。

```csharp
// Load the image you want to turn into a searchable PDF
engine.Image = ImageStream.FromFile(@"C:\Docs\invoice.png");
```

如果影像來自網路請求或資料庫，也可以從 `MemoryStream` 載入。

## 第三步：執行 OCR 辨識 – **how to ocr image**

影像載入後，繁重的工作只需一次呼叫即可完成。`Recognize` 方法會回傳 `OcrResult`，其中包含擷取的文字與原始位圖。

```csharp
// Perform OCR on the loaded image
OcrResult ocrResult = engine.Recognize();
```

*背後運作:* 引擎會分析每個像素、偵測字元，並組成 Unicode 字串。它同時保留建立隱藏文字層所需的位置資料。

## 第四步：設定 PDF 儲存選項 – **how to add layer** & **how to set compression**

這就是可搜尋 PDF 的魔法所在。我們建立一個 `PdfSaveOptions` 物件，告訴 Aspose.Pdf 如何嵌入原始影像、加入隱藏文字覆蓋層，並壓縮最終檔案。

```csharp
// Set up PDF options for a searchable PDF
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    IncludeImage = true,          // Keep the original image in the PDF
    AddTextLayer = true,          // Add a hidden text layer with OCR results
    Compression = PdfCompression.Zip   // Use ZIP compression for smaller size
};
```

- **IncludeImage** 確保原始掃描的視覺忠實度。
- **AddTextLayer** 建立一個隱形圖層，讓瀏覽器與 PDF 閱讀器能索引搜尋。
- **Compression** 在不犧牲品質的前提下降低檔案大小；ZIP 為大多數文件的良好預設。

## 第五步：儲存結果 – **create searchable pdf**

最後，我們使用剛才定義的選項將 OCR 結果寫入磁碟。`Save` 方法接受目標路徑與 `PdfSaveOptions` 實例。

```csharp
// Save the OCR result as a searchable PDF
ocrResult.Save(@"C:\Docs\invoice_searchable.pdf", pdfOptions);
```

當你在 Adobe Reader 或任何現代檢視器中開啟 `invoice_searchable.pdf` 時，會看到原始影像，但現在可以像原生 PDF 一樣選取、複製與搜尋文字。

### 完整範例程式

將上述步驟整合起來，以下是完整、可直接執行的程式：

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine engine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the source image
            string imagePath = @"C:\Docs\invoice.png";
            engine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            OcrResult result = engine.Recognize();

            // 4️⃣ Configure PDF options (layer + compression)
            PdfSaveOptions pdfOptions = new PdfSaveOptions
            {
                IncludeImage = true,
                AddTextLayer = true,
                Compression = PdfCompression.Zip
            };

            // 5️⃣ Save as searchable PDF
            string pdfPath = @"C:\Docs\invoice_searchable.pdf";
            result.Save(pdfPath, pdfOptions);

            Console.WriteLine($"Searchable PDF created at: {pdfPath}");
        }
    }
}
```

**預期輸出**（於主控台）:  
`Searchable PDF created at: C:\Docs\invoice_searchable.pdf`

開啟產生的檔案，按 **Ctrl F**，輸入發票上看到的字詞，即可看到檢視器立即跳至該處。這就是 **create searchable pdf** 的核心運作。

## 常見問題與避免方法

| 問題 | 發生原因 | 解決方法 |
|-------|----------------|-----|
| 文字無法搜尋 | `AddTextLayer` 設為 `false` 或使用較舊的 Aspose 版本 | 確保 `AddTextLayer = true`，並更新至最新的 NuGet 套件 |
| PDF 檔案過大（兆位元） | 壓縮設定為 `PdfCompression.None` | 改為 `PdfCompression.Zip` 或對影像使用 `PdfCompression.Jpeg` |
| 文字亂碼 | 語言設定錯誤或影像解析度過低 | 正確設定 `engine.Language`，並提供至少 300 dpi 的影像 |
| 某些檢視器看不到隱藏圖層 | PDF 產生時使用非標準 PDF 版本 | 使用 `PdfSaveOptions.PdfVersion = PdfVersion.PDF_1_7`（預設），或升級檢視器 |

### 專業提示

如果你只想**將影像轉換為 PDF**而不進行 OCR（僅產生純影像 PDF），只需將 `AddTextLayer = false`。相同的 `PdfSaveOptions` 仍可控制壓縮，對於不需要搜尋功能的掃描文件歸檔相當便利。

## 擴充解決方案

- **Multiple pages**: 迭代影像檔案清單，逐一設定 `engine.Image = ...`，並使用 `PdfDocument` 聚合將結果累積成單一 PDF。
- **Different languages**: 將 `engine.Language = OcrLanguage.Spanish`（或任何支援的語言）改為其他語言，以處理多語言發票。
- **Custom compression**: 對於彩色豐富的影像，可使用 `PdfCompression.Jpeg` 並設定品質 (`pdfOptions.JpegQuality = 80`) 以進一步縮小檔案。

## 結論

我們已完整說明如何使用 C# 從影像**建立可搜尋的 PDF**檔案。從初始化 OCR 引擎、載入圖片、執行辨識、設定隱藏文字層，到壓縮設定——每一步皆是打造快速、可搜尋文件的關鍵。  

現在，你可以自動化發票處理、歸檔合約，或建構批次掃描工具，將紙本資料瞬間轉換為可搜尋的 PDF。  

準備好接受下一個挑戰了嗎？試著加入浮水印、合併多個可搜尋 PDF，或將此邏輯以 Web API 形式公開，讓整個組織能即時上傳影像並取得可搜尋的 PDF。

*如果你覺得本指南對你有幫助，請給它一顆 ⭐，與同事分享，或留下你的客製化建議。祝開發愉快！*

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，進一步延伸所示技巧。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索其他實作方式。

- [如何在 .NET 使用 Aspose.OCR 進行 PDF OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [將影像轉換為 PDF C# – 儲存多頁 OCR 結果](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [如何 OCR 影像 – 在 OCR 影像辨識中執行 OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}