---
category: general
date: 2026-02-13
description: 使用 Aspose.OCR 從圖像建立可搜尋的 PDF。學習如何將圖像轉換為 PDF、從圖像擷取文字、在 PDF 中嵌入字型，以及辨識 PNG
  圖片中的文字。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- embed fonts in pdf
- recognize text from png
language: zh-hant
og_description: 使用 Aspose.OCR 從圖像建立可搜尋的 PDF。本指南將示範如何將圖像轉換為 PDF、嵌入字型，並輕鬆從 PNG 提取文字。
og_title: 從圖像建立可搜尋 PDF – 步驟式 C# 教學
tags:
- C#
- OCR
- Aspose
- PDF generation
title: 從圖像建立可搜尋的 PDF – 完整 C# 指南
url: /zh-hant/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

keep bold.

But the instruction: translate all text content naturally. So we translate.

Let's produce.

Also list items.

Make sure to keep code block placeholders.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像建立可搜尋的 PDF – 完整 C# 教學

是否曾需要 **從掃描的 PNG 建立可搜尋的 PDF**，卻不知從何下手？您並不孤單。無論是發票數位化或是舊手冊歸檔，能將圖片轉成可搜尋的 PDF 都是顛覆性的改變。  

在本教學中，我們將一步步說明 **將影像轉成 PDF**、**從影像擷取文字**、嵌入必要字型，最終產生完整的可搜尋 PDF 檔案。沒有模糊的參考，只有可直接複製貼上到 Visual Studio 執行的完整範例。

> **您將獲得：** 一個 C# 主控台應用程式，讀取 `input.png`、執行 OCR、嵌入字型、保留原始點陣圖作為背景，並輸出 `output.pdf`。完成後，您將了解每一行程式碼的意義，以及如何依需求自行調整。

---

## 前置條件

- .NET 6.0 SDK 或更新版本（程式碼亦相容 .NET Framework 4.7+）。  
- Aspose.OCR for .NET – 可從 NuGet 取得 (`Install-Package Aspose.OCR`)。  
- 一張範例 PNG 圖片（`input.png`），放在您自行管理的資料夾內。  
- 基本的 C# 主控台專案概念（若從未建立過，只要開啟 Visual Studio → **建立新專案** → **主控台應用程式** → **C#** 即可）。

> **小技巧：** Aspose 提供免費試用授權；只要把 `.lic` 檔案放在可執行檔旁邊，函式庫即可在不加浮水印的情況下運作。

---

## 步驟 1：設定 OCR 引擎 – 從 PNG 辨識文字

首先，我們需要一個能讀取 PNG 內字元的 OCR 引擎。Aspose.OCR 讓這件事變得相當簡單。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

// Initialize the OCR engine with English language support
OcrEngine ocrEngine = new OcrEngine
{
    // Primary language – you can add more if needed
    Language = OcrLanguage.English
};
```

**為什麼這很重要：**  
設定 `Language` 讓引擎知道要辨識哪種字符集。若省略此設定，引擎會使用通用模式，可能會誤判帶重音符號的字元或數字。若文件包含多語言，可傳入逗號分隔的列表，例如 `OcrLanguage.English | OcrLanguage.French`。

---

## 步驟 2：載入並辨識影像 – 從影像擷取文字

引擎準備好後，將目標 PNG 傳入引擎進行處理。

```csharp
// Path to the source image; adjust as needed
string inputPath = @"YOUR_DIRECTORY/input.png";

// Perform OCR – this populates the engine's internal text representation
ocrEngine.RecognizeImage(inputPath);
```

**背後發生了什麼？**  
`RecognizeImage` 會掃描位圖、辨識文字區塊，並將結果存入 `ocrEngine`。之後若只需要原始字串，可直接存取 `ocrEngine.Text`；但若要產生可搜尋的 PDF，則交由 Aspose 完成轉換。

> **例外情況：** 若 PNG 檔案過大（超過 10 MB），可能會發生記憶體不足。此時可先縮小影像，或改用 `OcrEngine.RecognizeImage(Stream)` 以串流方式讀取資料。

---

## 步驟 3：設定 PDF 匯出選項 – 在 PDF 中嵌入字型

如果字型未嵌入，可搜尋的 PDF 將無法正確顯示；文件在缺少相應字體的機器上會變形。Aspose 允許我們透過簡單的選項物件切換此功能。

```csharp
// Define how the searchable PDF should be built
SearchablePdfOptions pdfOptions = new SearchablePdfOptions
{
    // Guarantees the PDF renders correctly everywhere
    EmbedFonts = true,

    // Keeps the original raster image as a visual background
    KeepOriginalImage = true
};
```

**為什麼要嵌入字型？**  
當 `EmbedFonts` 為 `true` 時，PDF 會把字型資料寫入檔案本身。這確保任何檢視器（Chrome、Adobe Reader 或行動裝置 App）都能正確呈現文字，即使目標系統沒有安裝該字型。

**什麼時候會把 `KeepOriginalImage` 設為 `false`？**  
如果只需要文字且想減小檔案大小，關閉此選項會移除背景影像，產生「純文字」的 PDF。

---

## 步驟 4：匯出為可搜尋的 PDF – 轉換影像為 PDF

有了 OCR 結果與 PDF 選項，最後只需要一行程式碼即可將可搜尋的 PDF 寫入磁碟。

```csharp
// Destination path for the generated PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";

// Export the OCR result as a searchable PDF
ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created.");
```

**您將看到的結果：**  
在任何檢視器開啟 `output.pdf`，皆可選取文字、複製貼上，甚至使用 `Ctrl + F` 搜尋原本只存在於 PNG 像素中的單字。

---

## 完整範例程式

以下是可直接編譯執行的完整程式碼。請將 `YOUR_DIRECTORY` 替換成放置 `input.png` 的資料夾路徑。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine – set language to English
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Recognize text from the PNG image
        string inputPath = @"YOUR_DIRECTORY/input.png";
        ocrEngine.RecognizeImage(inputPath);

        // 3️⃣ Prepare PDF options – embed fonts & keep raster background
        SearchablePdfOptions pdfOptions = new SearchablePdfOptions
        {
            EmbedFonts = true,
            KeepOriginalImage = true
        };

        // 4️⃣ Export to a searchable PDF file
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

        // 5️⃣ Notify the user
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**預期的主控台輸出：**

```
Searchable PDF created.
```

開啟 `output.pdf`，搜尋您知道出現在 `input.png` 中的單字。若能被標示，即代表已成功 **從影像建立可搜尋的 PDF**。

---

## 常見問題與進階小技巧

### 「可以一次處理多張影像嗎？」

當然可以。將辨識與匯出邏輯包在迴圈中，例如使用 `Directory.GetFiles(..., "*.png")`。別忘了為每個 PDF 指定唯一名稱，例如 `Path.GetFileNameWithoutExtension(img) + ".pdf"`。

### 「如果文件同時包含英文與西班牙文該怎麼辦？」

將語言屬性設為組合旗標：

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Aspose 會嘗試同時偵測兩種字母表的字符。

### 「PDF 檔案太大，怎麼壓縮？」

兩個快速技巧：

1. 設定 `pdfOptions.KeepOriginalImage = false` 以移除點陣背景。  
2. 使用 `pdfOptions.ImageCompression = ImageCompression.Jpeg;`（需自行加入此屬性）壓縮嵌入的影像。

### 「正式上線需要授權嗎？」

試用版可用於測試，但若要商業部署，必須購買授權並在程式啟動時盡早註冊：

```csharp
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

---

## 延伸應用

既然已掌握 **建立可搜尋的 PDF**，您可能想進一步：

- **加入浮水印** – 使用 Aspose.PDF 的 `PdfDocument` 在 OCR 後覆蓋文字。  
- **批次處理 PDF** – 使用 `PdfFileEditor` 將多個可搜尋的 PDF 合併成一本。  
- **結合 Azure Blob Storage** – 直接從雲端讀寫影像與 PDF 串流，省去本機檔案 I/O。

上述每項延伸皆遵循相同模式：取得 OCR 結果、設定下一個函式庫的參數，然後串接操作。

---

## 結論

您剛剛學會如何使用 Aspose.OCR 於 C# 中 **從 PNG 影像建立可搜尋的 PDF**。透過初始化 OCR 引擎、辨識文字、設定 `SearchablePdfOptions` 以 **在 PDF 中嵌入字型**，最後匯出，即可得到外觀與原始影像相同、且可全文搜尋的檔案。  

接下來，您可以嘗試批次轉換、支援更多語言或更高壓縮率，依照工作流程自行調整。若遇到問題，Aspose 論壇與 API 文件都是不錯的資源，而上述核心步驟已涵蓋約 90 % 的常見情境。

祝開發順利，願您的 PDF 永遠可搜尋！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}