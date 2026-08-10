---
category: general
date: 2026-02-27
description: 使用 Aspose OCR，僅需數秒即可將掃描 PDF 轉換為可搜尋的 PDF。了解如何將掃描 PDF 轉換、OCR 轉換 PDF，並輕鬆擷取
  PDF 文字。
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- ocr convert pdf
- extract text from pdf
- convert image pdf
language: zh-hant
og_description: 即時建立可搜尋的 PDF。本教學示範如何將掃描 PDF 轉換、使用 OCR 轉換 PDF，以及使用 Aspose OCR 從 PDF
  中擷取文字。
og_title: 建立可搜尋 PDF – 快速 Aspose OCR 指南
tags:
- Aspose OCR
- C#
- PDF processing
title: 使用 Aspose OCR 從掃描圖像建立可搜尋的 PDF
url: /zh-hant/net/text-recognition/create-searchable-pdf-from-scanned-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 從掃描圖像建立可搜尋 PDF

是否曾需要 **建立可搜尋 PDF**，卻只拿到紙本發票卻不知從何下手？使用 Aspose OCR，只要幾行 C# 程式碼就能 **建立可搜尋 PDF**——不需要外部服務，也不必手動複製貼上。

在本教學中，我們將一步步說明如何 **將掃描的 pdf** 轉換成完整可搜尋的 PDF，解釋每個步驟的原因，並示範如果你只想要原始字串而非 PDF 輸出，如何 **從 pdf 中擷取文字**。完成後，你將擁有一段可重複使用的程式碼，解決「只有影像的 PDF」問題，並提供一些邊緣情況的處理技巧。

![create searchable pdf using Aspose OCR](image-placeholder.png "create searchable pdf using Aspose OCR")

## 需要的環境

- .NET 6.0 或更新版本（API 同時支援 .NET Core、.NET Framework 與 .NET 5+）
- Visual Studio 2022（或任何你慣用的編輯器）
- Aspose OCR NuGet 套件（`Aspose.OCR`）——我們會在第一步安裝它
- 一個掃描過的 PDF 檔（僅影像）——你想要轉成 **可搜尋 PDF** 的檔案

就這些——不需要額外的 OCR 引擎，也不會因試用版授權而卡關。  

現在，讓我們開始吧。

## 步驟 1：安裝 Aspose OCR 函式庫（以及小技巧）

在寫任何程式碼之前，必須先引用函式庫。於專案資料夾開啟終端機，執行：

```bash
dotnet add package Aspose.OCR
```

> **專業小提醒：** 若使用 Visual Studio 的套件管理員，搜尋「Aspose.OCR」並點選 **Install**。免費試用版支援最多 20 頁，非常適合測試。

安裝套件後，你即可使用 `OcrEngine`、`OcrLanguage` 與 `OcrOutputFormat` 這三個類別，來 **ocr convert pdf**。

## 步驟 2：設定 OCR 引擎（建立可搜尋 PDF – 核心設定）

引擎需要知道要辨識的語言與期望的輸出格式。這裡我們要產生英文可搜尋的 PDF。

```csharp
using Aspose.OCR;
using System;

// Step 2: Set up the OCR engine
var ocrEngine = new OcrEngine
{
    // Choose the language of the source document
    Language = OcrLanguage.English,

    // Tell Aspose we want a searchable PDF as the result
    OutputFormat = OcrOutputFormat.SearchablePdf
};
```

為什麼要明確設定 `Language`？當引擎自行猜測語言時，OCR 準確度會大幅下降，尤其是文件中混雜數字或多種文字時。固定為英文可得到較乾淨的文字層，進而提升之後 **從 pdf 中擷取文字** 的效果。

## 步驟 3：將掃描 PDF 轉換為可搜尋 PDF

引擎設定完成後，指向來源檔案並指定輸出位置。這一行程式碼會完成所有繁重工作：將每頁光柵化、執行 OCR，並產生帶有隱形文字層的新 PDF。

```csharp
// Step 3: Perform the conversion
ocrEngine.RecognizePdf(
    @"C:\Docs\invoice_scanned.pdf",   // input – image‑only PDF
    @"C:\Docs\invoice_searchable.pdf" // output – searchable PDF
);
```

若來源 PDF 含有多頁，Aspose OCR 會依序處理，保留原始版面配置。輸出檔可在任何 PDF 閱讀器開啟，你會發現現在可以選取與搜尋先前只能看到的圖片文字。

### 驗證結果（從 PDF 中擷取文字）

為了確保轉換成功，你可以程式化地抽取文字：

```csharp
using Aspose.Pdf;           // Add Aspose.PDF if you also need text extraction
using System.Text;

// Load the newly created searchable PDF
var doc = new Document(@"C:\Docs\invoice_searchable.pdf");
var sb = new StringBuilder();

foreach (Page page in doc.Pages)
{
    // Extract the hidden text layer
    sb.Append(page.Text);
}

Console.WriteLine("Extracted text:\n" + sb.ToString());
```

此程式碼示範如何在 OCR 完成後 **從 pdf 中擷取文字**，方便做索引或將內容餵入搜尋引擎。請注意，此步驟需要額外的 `Aspose.PDF` 套件；它是一個輕量的附加元件。

## 步驟 4：處理常見邊緣情況（當你 **Convert Image PDF** 時）

雖然基本流程適用於大多數 PDF，實務上仍會遇到各種挑戰：

| 情境 | 為何會發生 | 處理方式 |
|-----------|----------------|------------------|
| **頁面旋轉** | 掃描器有時會自動將頁面旋轉 90°。 | 在呼叫 `RecognizePdf` 前設定 `ocrEngine.RotatePages = true`。 |
| **混合語言** | 發票可能同時包含法文或德文詞彙。 | 使用 `OcrLanguage.Multilingual`，或以 `|` 結合多種語言（例如 `OcrLanguage.English \| OcrLanguage.French`）。 |
| **大型檔案（> 100 頁）** | 免費試用版會在檔案中途停止處理。 | 購買授權或使用 `Aspose.Pdf` 先將 PDF 切割成多段再進行 OCR。 |
| **低解析度掃描** | 文字模糊，OCR 準確度下降。 | 透過 `ocrEngine.ImageResolution = 300` 提升 DPI（預設 200）。 |

針對這些情況做好處理，可確保你的 **ocr convert pdf** 工作流程在正式環境中保持穩定。

## 步驟 5：自動化整個流程（封裝成方法）

如果你在建置發票處理服務，通常會需要一個可重複使用的方法。以下是一個精簡版，接受輸入與輸出路徑、處理旋轉，並回傳抽出的文字。

```csharp
using Aspose.OCR;
using Aspose.Pdf;
using System;
using System.Text;

public static class PdfSearchableHelper
{
    /// <summary>
    /// Converts an image‑only PDF to a searchable PDF and returns the hidden text.
    /// </summary>
    /// <param name="inputPath">Path to the scanned PDF.</param>
    /// <param name="outputPath">Path where the searchable PDF will be saved.</param>
    /// <returns>All extracted text as a single string.</returns>
    public static string ConvertAndExtract(string inputPath, string outputPath)
    {
        // 1️⃣ Initialize OCR engine
        var ocr = new OcrEngine
        {
            Language = OcrLanguage.English,
            OutputFormat = OcrOutputFormat.SearchablePdf,
            RotatePages = true,            // fixes rotated scans automatically
            ImageResolution = 300          // improve accuracy on low‑res scans
        };

        // 2️⃣ Perform conversion
        ocr.RecognizePdf(inputPath, outputPath);

        // 3️⃣ Load result and pull out hidden text
        var doc = new Document(outputPath);
        var sb = new StringBuilder();

        foreach (Page page in doc.Pages)
            sb.Append(page.Text);

        return sb.ToString();
    }
}
```

接著即可呼叫：

```csharp
string extracted = PdfSearchableHelper.ConvertAndExtract(
    @"C:\Docs\contract_scanned.pdf",
    @"C:\Docs\contract_searchable.pdf");

Console.WriteLine("OCR completed. Extracted text length: " + extracted.Length);
```

這就是完整的 **convert image pdf** → **searchable PDF** 工作流程，全部封裝在單一方法中，隨時可以放入 ASP.NET Core 服務或 Console 應用程式。

## 常見問題 (FAQ)

**Q: 這在 macOS / Linux 上能跑嗎？**  
A: 完全可以。.NET 6 執行環境與 Aspose OCR 均支援跨平台，程式碼在 Windows、macOS 以及 Linux 容器上皆可執行。

**Q: 若我只需要文字，不在乎可搜尋的 PDF，該怎麼做？**  
A: 省略 `OutputFormat` 設定，改為 `OutputFormat = OcrOutputFormat.Text`。引擎會直接回傳純文字。

**Q: 能保留原始 PDF 的 metadata 嗎？**  
A: 可以。轉換完成後，可將來源 `Document` 物件的 `Info.Title`、`Info.Author` 等屬性複製到新文件。

**Q: 有頁數限制嗎？**  
A: 免費試用版每份文件上限 20 頁。購買正式授權後即無此限制。

## 結論

現在你已掌握如何 **create searchable PDF**  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}