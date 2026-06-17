---
category: general
date: 2026-03-18
description: 使用 Aspose OCR 於 C# 建立可搜尋的 PDF。將影像轉換為 PDF、加入 OCR 文字層，並在簡單幾個步驟內將 PDF 位元組寫入檔案。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- add ocr text layer
- write pdf bytes to file
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中快速建立可搜尋的 PDF。了解如何將影像轉換為 PDF、加入 OCR 文字層，並將 PDF
  位元組寫入檔案。
og_title: 將圖像轉換為可搜尋的 PDF – 快速 C# OCR 教學
tags:
- OCR
- PDF
- C#
- Aspose
title: 使用 OCR 從圖像建立可搜尋的 PDF – C# 指南
url: /zh-hant/net/text-recognition/create-searchable-pdf-from-image-with-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像建立可搜尋的 PDF（含 OCR） – C# 指南

有沒有需要從掃描的圖片**建立可搜尋的 PDF**？使用 Aspose OCR，你只需要幾行程式碼，無需大型函式庫。在本教學中，我們將**將圖像轉換為 PDF**，在上面加入**OCR 文字層**，最後**將 PDF 位元組寫入檔案**，讓你得到符合標準的 PDF/A‑2b 文件，使用者可以真正搜尋其中的文字。

如果你在想為什麼要使用可搜尋的 PDF 而不是純圖像檔案，請考慮使用者體驗：可搜尋的 PDF 讓人可以複製、選取與索引文字——非常適合檔案保存、法律文件，或任何需要之後提取文字的工作流程。讓我們開始吧。

## 需求條件

- .NET 6 或更新版本（此程式碼亦可在 .NET Framework 4.7+ 上執行）
- Aspose.OCR NuGet 套件（`Aspose.OCR` 版本 23.10 或更新）
- 要轉換成可搜尋 PDF 的點陣圖（`.png`、`.jpg` 等）
- 具備基本的 C# 知識——不需要高階技巧，只要會基礎語法即可

就這樣。無需外部工具或額外轉換器。所有繁重的工作皆由 Aspose OCR 引擎處理。

## 建立可搜尋 PDF – 概觀

在深入程式碼之前，我們先概述流程：

1. **實例化** OCR 引擎——此物件負責從圖片讀取文字。  
2. **載入**來源圖像——我們會將 `ImageStream` 提供給引擎。  
3. **設定** PDF/A‑2b 儲存選項——告訴 Aspose 將辨識出的文字嵌入為隱藏層。  
4. **執行** OCR 並**擷取**產生的 PDF 位元組。  
5. **寫入**這些位元組至磁碟，產生最終的可搜尋 PDF 檔案。

每個步驟都直接對應到一兩行 C# 程式碼，使整個工作流程感覺像是小腳本，而非大型專案。

## 步驟 1：將圖像轉換為 PDF – 載入圖像

首先，我們需要提供 OCR 引擎可讀取的資料。`ImageStream.FromFile` 輔助方法會將檔案載入為 Aspose 可處理的串流。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

// 1️⃣ Load the source image you want to turn into a searchable PDF
ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
```

> **小技巧：** 請將圖像解析度保持在 300 dpi 或更高；低解析度掃描會大幅降低 OCR 準確度。

## 步驟 2：從圖像辨識文字並加入 OCR 文字層

現在我們建立 OCR 引擎並指示它辨識文字。當我們將辨識結果與 `PdfSaveOptions`（其 `IncludeTextLayer = true`）結合時，魔法就會發生。此旗標會強制 Aspose 將擷取的字元嵌入為不可見的文字層，從而使 PDF 可搜尋。

```csharp
// 2️⃣ Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// 3️⃣ Set up PDF/A‑2b save options – includes the hidden text layer
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
{
    PdfCompliance = PdfCompliance.PdfA2b, // ensures PDF/A‑2b compliance
    IncludeTextLayer = true               // this is the key for searchable PDFs
};
```

為什麼選擇 PDF/A‑2b？它是 ISO 標準的保存格式，保證長期保存，且對我們而言，會強制 PDF 包含可搜尋的文字層。如果不需要符合保存規範，你可以完全省略 `PdfCompliance`，但保留它不會增加任何成本。

## 步驟 3：將 PDF 位元組寫入檔案 – 儲存結果

引擎已就緒且選項已設定後，我們執行辨識，並立即要求 Aspose 以 `byte[]` 形式提供 PDF。接著使用 `File.WriteAllBytes` 將這些位元組寫入磁碟。簡單卻強大。

```csharp
// 4️⃣ Perform OCR on the image and get the PDF bytes
byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

// 5️⃣ Write the PDF/A‑2b file to the output location
System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
Console.WriteLine("PDF/A‑2b file created – you now have a searchable PDF!");
```

那行 `Console.WriteLine` 為可選項目，但在終端機執行程式時能即時提供回饋。

## 完整範例程式

將所有步驟整合起來，以下是完整、可直接執行的程式。將它複製貼上到新的 Console 專案，將 `YOUR_DIRECTORY` 替換為實際路徑，然後按 **F5**。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

class PdfA2bDemo
{
    static void Main()
    {
        // Step 1: Load the source image
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");

        // Step 2: Create OCR engine and configure PDF/A‑2b options
        OcrEngine ocrEngine = new OcrEngine();
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
        {
            PdfCompliance = PdfCompliance.PdfA2b,
            IncludeTextLayer = true
        };

        // Step 3: Recognize and save as PDF bytes
        byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

        // Step 4: Write the bytes to a searchable PDF file
        System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
        Console.WriteLine("PDF/A‑2b file created.");
    }
}
```

### 預期輸出

- 在你指定的資料夾中會產生名為 `output.pdf` 的檔案。  
- 使用 Adobe Acrobat Reader 或任何 PDF 檢視器開啟，嘗試選取文字——若能複製文字，即表示你已成功**建立可搜尋的 PDF**。  
- 此文件亦會通過 PDF/A‑2b 驗證工具，因為我們使用了正確的合規旗標。

## 常見問題與特殊情況

**如果我的圖像包含多頁呢？**  
將每一頁各自放入 `ImageStream`，並依序提供給 `OcrEngine`。Aspose 會自動將頁面串接成單一 PDF。

**我可以變更 OCR 語言嗎？**  
當然可以。在呼叫 `Recognize` 前，設定 `ocrEngine.Language = Language.English;`（或任何支援的語言）。

**大量檔案的記憶體使用情況如何？**  
若處理 GB 級別的掃描，建議直接將結果串流至 `FileStream`，而非將整個 `byte[]` 保留在記憶體中：

```csharp
using (var file = new FileStream("output.pdf", FileMode.Create))
{
    ocrEngine.Recognize(image).Save(pdfSaveOptions, file);
}
```

**我需要授權嗎？**  
Aspose 提供免浮水印的免費試用版。若於正式環境使用，請購買授權以移除評估標語並解鎖全部功能。

## 提升 OCR 準確度的技巧

- **前處理**圖像：去斜、去雜訊並提升對比度。  
- **使用無損格式**如 PNG；JPEG 壓縮產生的雜訊會干擾引擎。  
- **避免彩色背景**；純白背景可獲得最佳效果。

## 後續步驟

既然你已能**建立可搜尋的 PDF**，接下來可能想要：

- **批次處理**資料夾內的圖像，使用 `Directory.GetFiles`。  
- 稍後使用 `PdfDocument` API**擷取隱藏文字**以進行索引。  
- **結合 OCR 與數位簽章**，建立防篡改的檔案保存。

以上皆建立在我們先前討論的核心流程：載入、辨識、設定、儲存。

---

*準備好將掃描的檔案轉換為可搜尋的 PDF 了嗎？取得程式碼，指向你的圖像，讓 Aspose 處理繁重工作。祝開發愉快！*

![Create searchable PDF example](/images/create-searchable-pdf.png "Illustration of a searchable PDF generated from an image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}