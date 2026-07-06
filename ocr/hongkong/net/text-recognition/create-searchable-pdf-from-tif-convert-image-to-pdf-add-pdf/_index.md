---
category: general
date: 2026-04-04
description: 在 C# 中從 TIF 圖像建立可搜尋的 PDF – 了解如何將圖像轉換為 PDF、加入 PDF 中繼資料，並使用 Aspose.OCR
  產生可搜尋的文件。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: zh-hant
og_description: 使用 C# 從 TIF 檔案建立可搜尋的 PDF。將影像轉換為 PDF，加入 PDF 中繼資料，並使用 Aspose.OCR 產生可搜尋的文件。
og_title: 從 TIF 建立可搜尋 PDF – 步驟教學
tags:
- Aspose.OCR
- C#
- PDF generation
title: 從 TIF 建立可搜尋的 PDF – 將影像轉換為 PDF，加入 PDF 中繼資料
url: /zh-hant/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 TIF 建立可搜尋的 PDF – 完整 C# 教學

是否曾需要從掃描的發票 **建立可搜尋的 PDF**，卻不確定如何保持文字可搜尋且檔案中繼資料整潔？你並不孤單。在許多自動化專案中，PDF 必須同時具備機器可讀性，並正確標記如標題、作者以及信心門檻等資訊。  

在本指南中，我們將逐步說明一個完整的解決方案，該方案 **將影像轉換為 PDF**、注入 **PDF 中繼資料**，並過濾低信心的 OCR 結果——全部使用 Aspose.OCR 函式庫。完成後，你將擁有一段可直接放入任何 .NET 專案的即用程式碼片段，並提供一些處理例外情況的技巧。

## 前置條件

- .NET 6.0 或更新版本（此程式碼亦可於 .NET Framework 4.6+ 上執行）  
- Aspose.OCR NuGet 套件（`Install-Package Aspose.OCR`）  
- 欲轉換為可搜尋 PDF 的 TIF 影像（例如 `input.tif`）  
- 具備 C# 與 Visual Studio（或你慣用的 IDE）的基本知識  

不需要其他外部服務——整個流程皆在本機執行。

## 步驟 1 – 設定 OCR 引擎（建立可搜尋 PDF 核心）

我們首先需要一個 `OcrEngine` 實例，用以指定要辨識的語言。在大多數商業情境下，英語已足夠，但你可以將 `Language.English` 替換為任何支援的語言。

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**為何這很重要：** OCR 引擎負責將點陣像素轉換為 Unicode 文字。正確設定語言可提升辨識準確度，並減少之後需要過濾的低信心詞彙。

> **專業提示：** 若處理多語言文件，可實例化多個引擎，或使用 `Language.Multilingual` 讓 Aspose 自動偵測語言。

## 步驟 2 – 載入 TIF 影像（從 TIF 建立 PDF）

現在我們將引擎指向來源檔案。`ImageStream.FromFile` 輔助函式會將影像讀入串流，供 OCR 引擎使用。

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

你可能會想，*「我可以改用 JPEG 或 PNG 嗎？」* 當然可以——Aspose.OCR 支援大多數點陣格式。只要更改檔案副檔名即可。

## 步驟 3 – 設定 PDF 選項（加入 PDF 中繼資料）

在轉換之前，我們先建立 `PdfOptions` 物件。這裡可 **加入 PDF 中繼資料**（如標題與作者），同時告訴引擎過濾掉信心低於門檻的詞彙。

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**這裡發生了什麼？**  
- `Title` 與 `Author` 會成為 PDF 文件資訊字典的一部份，使檔案在文件管理系統中更易於索引。  
- `MinConfidence` 是一道防護欄：OCR 常會誤讀淡淡的字元，過濾它們可保持可搜尋層的乾淨，並提升後續文字擷取的品質。

若需自訂中繼資料（例如 `Subject`、`Keywords`），可透過 `PdfOptions.CustomProperties` 設定。

## 步驟 4 – 將影像轉換為可搜尋的 PDF（將影像轉為 PDF）

在引擎已備妥且選項設定完成後，最後的呼叫會執行轉換。它會將可搜尋的 PDF 寫入磁碟，將 OCR 文字層嵌入於原始影像之下。

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

執行此行程式碼後，`output.pdf` 會包含：  
- 原始 TIF 影像作為視覺背景  
- 隱形的文字層，供搜尋引擎與複製貼上操作讀取  
- 先前定義的中繼資料（標題、作者等）

### 預期結果

在 Adobe Reader 或任何 PDF 檢視器中開啟產生的 PDF，嘗試選取文字。你應該能複製與原始掃描相符的句子。文件的 **屬性** 對話框會顯示標題 “Invoice #12345” 與作者 “MyCompany”。

## 步驟 5 – 驗證信心過濾（為何 MinConfidence 有幫助）

確認低信心詞彙確實已被移除是很有用的。你可以使用 `pdftotext` 等工具檢視 PDF 的隱藏文字：

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

若該詞根本未出現，表示 `MinConfidence` 過濾如預期運作。若需更嚴格或寬鬆的過濾，可調整門檻值（例如 `0.7f`）。

## 步驟 6 – 處理多頁（從多頁 TIF 建立可搜尋 PDF）

許多發票是以多頁 TIFF 形式存在。Aspose.OCR 會自動將每個影格視為獨立頁面。只要將引擎指向多頁檔案，同一個 `ConvertToSearchablePdf` 呼叫即會產生多頁可搜尋的 PDF。

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**例外情況：** 若頁面為空白，OCR 仍可能產生空的文字層，這不會造成問題。然而，你可以在轉換前檢查 `ocrEngine.HasText` 以跳過空白頁面。

## 步驟 7 – 打包完整範例（全部步驟合併）

以下是一個可直接執行的完整程式，將所有步驟串接在一起。請將 `YOUR_DIRECTORY` 替換為你機器上的實際資料夾路徑。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

執行程式（`dotnet run` 或在 Visual Studio 按 **F5**）後，你會看到確認訊息。產生的 PDF 會與來源影像同目錄，隨時可供索引或存檔使用。

## 常見問題與注意事項

| 問題 | 答案 |
|----------|--------|
| **我可以為可搜尋層加入自訂字型嗎？** | OCR 層使用 Unicode；視覺外觀由底層影像決定，無需額外嵌入字型。 |
| **如果我的 TIF 是彩色的呢？** | Aspose.OCR 會自動將彩色影像轉為灰階以供 OCR 使用，但你可以透過設定 `PdfOptions.PreserveColor = true` 於 PDF 中保留原始顏色。 |
| **此函式庫是執行緒安全的嗎？** | 每個 `OcrEngine` 實例應僅由單一執行緒使用。若需平行處理，請為每個執行緒建立獨立的引擎。 |
| **我要如何加密 PDF？** | 在 OCR 轉換完成後，使用 `PdfOptions.Security` 設定密碼與權限即可。 |

## 後續步驟（擴充你的 PDF 工具組）

- **批次處理：** 迴圈處理資料夾中的 TIFF，為每個檔案產生可搜尋的 PDF。  
- **後處理：** 使用 Aspose.PDF 將產生的 PDF 合併為單一主文件。  
- **進階中繼資料：** 填入自訂 XMP 欄位，以便更好地與 SharePoint 或 ECM 系統整合。  

所有這些延伸功能皆基於我們剛剛討論的核心模式：**建立可搜尋 PDF**、**將影像轉為 PDF**，以及 **加入 PDF 中繼資料**。

---

*祝開發順利！若遇到任何問題，歡迎在下方留言，或查閱 Aspose.OCR 文件以取得最新 API 更新。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}