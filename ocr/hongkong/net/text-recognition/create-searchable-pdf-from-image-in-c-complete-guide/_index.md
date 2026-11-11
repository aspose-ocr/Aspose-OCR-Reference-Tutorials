---
category: general
date: 2026-02-19
description: 使用 Aspose OCR 在 C# 中將圖片轉換為可搜尋的 PDF。了解如何從圖片提取文字並將圖片生成可搜尋的 PDF。
draft: false
keywords:
- create searchable pdf
- extract text from image
- image to searchable pdf
- ocr image c#
- searchable pdf from image
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中從圖像建立可搜尋的 PDF。本教學將逐步說明如何從圖像提取文字並產生可搜尋的 PDF。
og_title: 在 C# 中將影像轉換為可搜尋的 PDF – 完整指南
tags:
- C#
- OCR
- PDF
title: 在 C# 中從圖像建立可搜尋 PDF – 完整指南
url: /zh-hant/net/text-recognition/create-searchable-pdf-from-image-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 從影像建立可搜尋的 PDF – 完整教學

是否曾需要 **建立可搜尋的 PDF**，卻不知從何下手？你並不孤單；許多開發者在首次面對 OCR 工作流程時都會卡關。好消息是，只要幾行 C# 程式碼加上 Aspose OCR，就能在數秒內把任何位圖（TIFF、JPEG、PNG…）轉換成可搜尋的 PDF。

在本教學中，我們將一步步說明整個流程——從安裝函式庫、從影像擷取文字，到寫入最終的 **影像轉可搜尋 PDF** 檔案。途中也會提及 **從影像擷取文字** 的其他應用情境，以及為何「隱藏文字層」對後續搜尋引擎很重要。

> **快速說明：** 以下所有程式碼皆可直接執行；不需要額外搜尋片段或外部文件。

## 需要的前置條件

在開始之前，請先確認你已具備以下項目：

| 前置條件 | 為什麼重要 |
|--------------|----------------|
| .NET 6 SDK（或更新版） | 現代語言功能與更佳效能 |
| Visual Studio 2022（或 VS Code） | 具備 IntelliSense 的 IDE 讓開發更順手 |
| Aspose.OCR NuGet 套件 | 提供 OCR 引擎與 PDF 寫入功能 |
| 範例影像（`input.tif`） | 你要轉換成可搜尋 PDF 的來源檔案 |

如果你已經有 .NET 專案，可略過「建立新專案」的步驟，直接進入 NuGet 安裝。

## 步驟 1：安裝 Aspose OCR NuGet 套件

首先，加入負責核心運算的函式庫。

```bash
dotnet add package Aspose.OCR
```

這行指令會一次拉下 OCR 引擎、PDF 寫入器以及所有原生相依套件。在 Visual Studio 中，你也可以右鍵點擊專案 → **Manage NuGet Packages** → 搜尋 *Aspose.OCR* 並點選 **Install**。

> **專業小技巧：** 請保持套件為最新版本。截至 2026 年 2 月，版本 23.9 為最新，並包含對高解析度 TIFF 的效能優化。

## 步驟 2：建立專案骨架

如果還沒有專案，建立一個簡易的 Console App：

```bash
dotnet new console -n PdfDemo
cd PdfDemo
```

開啟 `Program.cs`（或如果你想使用具名類別，可改為 `PdfDemo.cs`），把預設的 “Hello World” 程式碼全部清除。我們將以完整、可執行的範例取代它，**從影像建立可搜尋的 PDF**。

## 步驟 3：初始化 OCR 引擎 – 「從影像擷取文字」

OCR 引擎需要知道你要辨識的語言。對大多數英文合約而言，只要設定 `Language.English` 即可。若文件包含多語言，Aspose 亦支援稍後載入語言套件。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;

class PdfDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine and set the language to English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // 2️⃣ Perform OCR on the input image – this is where we **extract text from image**
        OcrResult ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/input.tif");

        // 3️⃣ Write the OCR result to a searchable PDF (image + hidden text layer)
        PdfResultWriter.Write(ocrResult, @"YOUR_DIRECTORY/contract_searchable.pdf");

        // 4️⃣ Notify that the PDF has been created
        Console.WriteLine("Searchable PDF created.");
    }
}
```

### 為什麼要這樣初始化引擎

* **語言選擇** 讓辨識器預期的字元集合更精確，顯著提升準確度。  
* **`RecognizeImage`** 會回傳 `OcrResult`，其中同時包含原始位圖與擷取出的 Unicode 文字。這個雙重表示法正是之後 **影像轉可搜尋 PDF** 的關鍵。

## 步驟 4：寫入隱藏文字層 – 產生 **影像轉可搜尋 PDF**

`PdfResultWriter` 會接收 `OcrResult`，並產生一個 PDF：每頁同時顯示原始點陣圖 **以及** 一層不可見的文字層。搜尋引擎（以及 PDF 檢視器）會索引這層隱藏文字，使文件可被搜尋。

```csharp
// Inside Main, after OCR succeeds
PdfResultWriter.Write(ocrResult, @"YOUR_DIRECTORY/contract_searchable.pdf");
```

在背後，Aspose 會利用 PDF 的 *ActualText* 屬性嵌入文字。若在 Adobe Acrobat 中開啟產生的檔案並嘗試選取文字，你會發現即使畫面上是影像，仍能複製到底層的文字。

## 步驟 5：驗證輸出

執行程式：

```bash
dotnet run
```

你應該會看到：

```
Searchable PDF created.
```

前往 `YOUR_DIRECTORY`，開啟 `contract_searchable.pdf`。試著選取一個單字——若選取區域呈現隱形文字，代表你已成功 **create searchable pdf** 從原始影像。

### 快速檢查

*在 PDF 內使用文字擷取工具（例如 Adobe Reader → Edit → Copy）測試。如果能貼上可讀的文字，隱藏層即運作正常。* 若出現亂碼，請確認來源影像解析度足夠（300 dpi 為良好基準）。

## 步驟 6：處理常見例外情況

### 低解析度掃描

若 TIFF 低於 200 dpi，OCR 準確度可能下降。先使用 `System.Drawing` 或 `ImageSharp` 進行影像放大，通常能取得較好結果。

```csharp
using System.Drawing;

// Load, upscale, then feed to OCR
Bitmap lowRes = new Bitmap(@"YOUR_DIRECTORY/input.tif");
Bitmap highRes = new Bitmap(lowRes, new Size(lowRes.Width * 2, lowRes.Height * 2));
highRes.Save(@"YOUR_DIRECTORY/upscaled.tif");
```

### 多頁文件

處理多頁 TIFF 時，需遍歷每一個影格：

```csharp
using System.Drawing.Imaging;

// Assume input.tif contains multiple frames
using (Image multiPage = Image.FromFile(@"YOUR_DIRECTORY/input.tif"))
{
    int pageCount = multiPage.GetFrameCount(FrameDimension.Page);
    for (int i = 0; i < pageCount; i++)
    {
        multiPage.SelectActiveFrame(FrameDimension.Page, i);
        string tempPath = $@"YOUR_DIRECTORY/page_{i}.tif";
        multiPage.Save(tempPath, ImageFormat.Tiff);

        OcrResult pageResult = ocrEngine.RecognizeImage(tempPath);
        PdfResultWriter.Write(pageResult, $@"YOUR_DIRECTORY/page_{i}_searchable.pdf");
    }
}
```

之後可使用 Aspose.PDF 或其他 PDF 函式庫將各頁 PDF 合併。

## 完整範例（所有步驟合併於單一檔案）

以下程式碼為完整、獨立的範例，你只要複製貼上到 `Program.cs` 即可。它涵蓋安裝、OCR、PDF 產生，以及簡易的錯誤處理。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;

class PdfDemo
{
    static void Main()
    {
        // Path to the source image – adjust to your environment
        const string inputPath = @"YOUR_DIRECTORY/input.tif";
        const string outputPath = @"YOUR_DIRECTORY/contract_searchable.pdf";

        try
        {
            // 👉 Step 1: Initialize OCR engine (English language)
            OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

            // 👉 Step 2: Run OCR – this **extracts text from image**
            Console.WriteLine("Running OCR on image...");
            OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

            // 👉 Step 3: Convert OCR result to a searchable PDF
            Console.WriteLine("Creating searchable PDF...");
            PdfResultWriter.Write(ocrResult, outputPath);

            Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

### 預期結果

* 目錄中會產生名為 `contract_searchable.pdf` 的檔案。  
* 用任何 PDF 檢視器開啟時，會看到原始掃描畫面，但選取文字時會複製到實際文字。  
* 使用文件搜尋（Ctrl + F）即可即時找到擷取出的關鍵字。

## 常見問題

**Q: 這能支援其他語言嗎？**  
A: 當然可以。只要把 `Language.English` 改成 `Language.French`、`Language.German` 等，或從 Aspose 載入自訂語言套件。

**Q: 如果我只需要純文字 PDF 該怎麼做？**  
A: OCR 完成後，你可以跳過影像，直接呼叫 `PdfResultWriter.WriteTextOnly(ocrResult, path)`（在較新版本的 Aspose 中提供）。

**Q: 能否嵌入字型以改善顯示效果？**  
A: 可以。PDF 寫入器會自動嵌入標準字型集，若需要公司專屬字型，只要提供自訂的 `PdfSaveOptions` 物件即可。

## 結語

我們已使用 C# 與 Aspose OCR **create searchable pdf** 從影像完成全流程，涵蓋 **extract text from image** 到最終的 **image to searchable pdf** 檔案。此程式碼已具備生產環境可用性，現在你可以輕鬆擴展至大量批次、不同語言，或將流程整合至 Web API。

### 接下來可以做什麼？

* 嘗試一次轉換整個資料夾的掃描檔，並合併成單一可搜尋 PDF。  
* 研究 Aspose PDF 的加密功能以

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}