---
category: general
date: 2026-02-14
description: 學習如何對 TIFF 或影像執行 OCR，並使用 OCR 轉換 PDF 成可搜尋的 PDF——一步一步的 C# 指南。
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: zh-hant
og_description: 探索如何對圖像執行 OCR、使用 OCR 轉換 PDF，並以 Aspose OCR 製作可搜尋的 PDF，簡潔的 C# 教學。
og_title: 如何在 C# 中執行 OCR 並建立可搜尋的 PDF
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: 如何在 C# 中執行 OCR 並建立可搜尋的 PDF
url: /zh-hant/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR 並建立可搜尋的 PDF

是否曾需要 **執行 OCR** 於掃描文件，但不確定如何將結果轉換成可搜尋的 PDF？你並不孤單——許多開發者在處理舊有的 TIFF 檔案或只有影像的 PDF 時，都會卡在這裡。好消息是，只要幾行 C# 程式碼加上 Aspose.OCR 套件，就能在數秒內把 TIFF 或任何影像轉換成完整可搜尋的 PDF。

在本教學中，我們會一步步說明所有必備知識：從安裝套件、載入多頁 TIFF，到呼叫 `RecognizeToPdf`，讓你 **使用 OCR 轉換 PDF** 並 **製作可搜尋的 PDF**，最終得到一個可直接搜尋內容的檔案。完成後，你將擁有一個即時可執行的 Console 應用程式，能從影像來源產生可搜尋的 PDF。

## 前置條件

- **.NET 6.0** 或更新版本（程式碼同樣適用於 .NET Framework 4.7 以上）。
- 有效的 **Aspose.OCR** 授權或臨時評估金鑰（免費試用版已足以測試）。
- Visual Studio 2022（或任何你慣用的編輯器）與 **NuGet** 套件管理員。
- 一個名為 `input.tif` 的輸入檔案，放在你可控制的資料夾中——多頁 TIFF 可直接使用。

> **專業小技巧：** 若你使用 Windows，請將 TIFF 複製到編譯後的 `.exe` 同一資料夾，以免產生路徑相關的問題。

## 第一步：安裝 Aspose.OCR NuGet 套件

在終端機中切換到專案資料夾，執行：

```bash
dotnet add package Aspose.OCR
```

此指令會下載最新的穩定版（截至 2026 年 2 月為 23.10），並加入所有必要的相依套件。還原完成後，你會在 **Solution Explorer** 的 **Dependencies** 下看到 `Aspose.OCR`。

## 第二步：建立最小化的 Console 應用程式

如果尚未有專案，先建立一個新的 Console 專案：

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

將自動產生的 `Program.cs` 替換為 **第 3 步** 中的完整程式碼。此程式會：

1. 建立 OCR 引擎實例。
2. 載入來源影像（或多頁 TIFF）。
3. 執行 OCR，直接輸出為可搜尋的 PDF。
4. 通知使用者處理已成功完成。

## 第三步：完整範例程式碼 – 從影像到可搜尋的 PDF

以下為 **完整** 的來源檔案。請將內容複製貼上至 `Program.cs`。程式內已加入說明註解，說明較不直觀的部分。

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**執行結果說明：** 程式跑完後，目標資料夾會產生 `searchable.pdf`。使用 Adobe Reader 或任何 PDF 閱讀器開啟，搜尋原始 TIFF 中的文字，應能即時找到，證明已成功 **製作可搜尋的 PDF**。

### 執行應用程式

```bash
dotnet run
```

若環境設定正確，畫面會顯示：

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

開啟 PDF，按 `Ctrl+F`，輸入來源中的任意單字，即可看到高亮跳至正確位置。

## 第四步：常見變形與例外情況

### 將一般 PDF（僅影像）轉換為可搜尋的 PDF

若來源是包含掃描影像而非文字的 PDF，仍可使用相同方式，只要改變 `ImageStream` 的來源：

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

即可滿足 **使用 OCR 轉換 PDF** 的需求，無需額外程式碼。

### 處理大型多頁文件

當文件頁數超過數百頁時，建議：

- **提升記憶體上限**（`Engine.MemoryLimit = 2_000; // MB`）。
- **分批處理**：先載入部份頁面，寫入中間 PDF，最後使用 PDF 套件（如 Aspose.PDF）合併。

### 支援非英文語系

Aspose.OCR 內建多種語言支援。辨識前先設定語系：

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

若需要 **tiff 轉可搜尋 pdf** 的非拉丁文字，請先安裝對應的語言套件。

### 輸出 PDF 為空白該怎麼辦？

- 確認輸入檔案未損毀。
- 確認 OCR 引擎已取得有效授權——評估模式可能會限制頁數。
- 檢查影像解析度是否至少 300 dpi，較低解析度會導致辨識不良。

## 第五步：以程式方式驗證結果（可選）

有時需要程式自動確認 PDF 是否真的包含文字層。可使用 Aspose.PDF 來抽取文字：

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

若 `extracted` 非空，即代表已成功 **製作可搜尋 pdf**。

## 結論

我們已說明 **如何在 TIFF（或任何影像）上執行 OCR**，並順利 **使用 OCR 轉換 PDF**，產生如同原生文件般可搜尋的 **PDF**。關鍵步驟如下：

1. 安裝 Aspose.OCR。  
2. 初始化 `Engine`。  
3. 透過 `ImageStream` 載入影像。  
4. 呼叫 `RecognizeToPdf`。  

之後即可探索語言設定、大批次處理，或將輸出與其他 PDF 操作結合。相同模式同樣適用於 **tiff 轉可搜尋 pdf**、**從影像產生可搜尋 pdf**，甚至掃描 PDF。

準備好接受下一個挑戰了嗎？試著將 OCR 嵌入 Web API，讓使用者上傳掃描檔即時取得可搜尋的 PDF，或探索 `OcrEngine` 的手寫筆記辨識進階設定。可能性無限——祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}