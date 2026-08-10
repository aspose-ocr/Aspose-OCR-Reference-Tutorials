---
category: general
date: 2026-06-19
description: 使用 Aspose OCR 於 C# 識別圖像文字：逐步指南，將圖像轉換為文字並從 jpg 檔案提取文字。
draft: false
keywords:
- recognize text from image
- extract text from jpg
- convert image to text
- perform ocr on image
- set ocr language
language: zh-hant
og_description: 使用 Aspose OCR 於 C# 辨識圖像文字。了解如何設定 OCR 語言、從 jpg 提取文字，以及在數分鐘內將圖像轉換為文字。
og_title: 在 C# 中辨識圖像文字 – 將圖像轉換為文字
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: 'recognize text from image using Aspose OCR in C#: step‑by‑step guide
    to convert image to text and extract text from jpg files.'
  headline: recognize text from image in C# – Convert Image to Text
  type: TechArticle
- description: 'recognize text from image using Aspose OCR in C#: step‑by‑step guide
    to convert image to text and extract text from jpg files.'
  name: recognize text from image in C# – Convert Image to Text
  steps:
  - name: 5.1 Low‑Resolution Images
    text: OCR accuracy drops sharply below 100 dpi. If you notice garbled output,
      try pre‑processing the image (increase contrast, resize, or apply a sharpening
      filter) before feeding it to Aspose OCR.
  - name: 5.2 Multi‑Page Documents
    text: "Even though Community mode caps at 100 pages, you can still process PDFs
      or multi‑page TIFFs. The engine will return concatenated text, preserving page
      breaks with `\f`."
  - name: 5.3 Non‑English Languages
    text: 'Switch the `Language` enum to another supported value:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: 在 C# 中辨識圖片文字 – 圖片轉文字
url: /zh-hant/net/text-recognition/recognize-text-from-image-in-c-convert-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# recognize text from image in C# – Convert Image to Text

有沒有曾經需要 **從圖片辨識文字**，卻不確定哪個函式庫可以在不付高額授權費的情況下完成？你並不孤單。在本教學中，我們將示範如何使用 Aspose OCR 的免費 Community 模式來 **將圖片轉換成文字**、從 jpg 檔案擷取文字，甚至 **設定 OCR 語言** 以因應多語言情境。

我們會從安裝 NuGet 套件說起，並說明如何處理多頁 PDF 或低解析度圖片等邊緣案例。完成後，你將擁有一個可即時 **對圖片執行 OCR** 的可執行主控台應用程式。

## What You’ll Need

- .NET 6 SDK 或更新版本（程式碼同樣支援 .NET Core 3.1+）  
- Visual Studio 2022 或任何你慣用的編輯器  
- 一張包含可讀文字的圖片檔（JPG、PNG、BMP…）  
- 可連網路以下載 `Aspose.OCR` NuGet 套件  

就這麼簡單——不需要額外 DLL、也不需要外部服務，純粹使用 C#。

![recognize text from image example](https://example.com/ocr-screenshot.png "recognize text from image example")

*(螢幕截圖顯示辨識範例 JPG 後的主控台輸出。)*

## Step 1: Install Aspose  OCR via NuGet

首先，將 Aspose OCR 函式庫加入專案。於專案資料夾開啟終端機，執行：

```bash
dotnet add package Aspose.OCR
```

此套件內建 **Community 模式**，每次執行上限 100 頁，正好適合小規模實驗。若日後需要更高上限，只要升級付費授權即可，程式碼不需變更。

## Step 2: Configure the OCR Engine (Set OCR Language)

在 **對圖片執行 OCR** 之前，必須告訴引擎要辨識哪種語言。預設為英文，你只要一行程式碼即可切換成西班牙文、法文，甚至中文。

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;

// Choose the language you need – here we stick with English.
var ocrConfig = new OcrEngineConfig
{
    Language = Language.English,      // set ocr language
    MaxPagesPerRun = 100              // enforced limit in Community mode
};
```

為什麼語言很重要？OCR 模型是以特定字元集訓練的；若把法文文件交給英文模型，會遺失重音與連字。設定正確語言可大幅提升辨識準確度。

## Step 3: Create the OCR Engine and Recognize the Image

設定完成後，在 `using` 區塊內建立引擎，讓資源自動釋放。接著呼叫 `RecognizeImage`，傳入 JPG（或其他支援格式）的路徑。

```csharp
// Step 3: Create the OCR engine and recognize the image
using var ocrEngine = new OcrEngine(ocrConfig);

// Replace with the actual path to your image file.
string imagePath = @"YOUR_DIRECTORY/sample.jpg";

// Perform OCR – this will **recognize text from image**.
var ocrResult = ocrEngine.RecognizeImage(imagePath);
```

需要注意的幾點：

- **執行緒安全性**：`OcrEngine` 實例本身不是執行緒安全的。如果要同時處理多張圖片，請為每個執行緒建立獨立的引擎實例。  
- **支援格式**：除了 JPG，還能接受 PNG、BMP、TIFF，甚至 PDF。相同的方法即可 **從 jpg 擷取文字** 或其他點陣圖。

## Step 4: Output the Recognized Text (Convert Image to Text)

OCR 引擎完成工作後，結果會存於 `OcrResult` 物件。其 `Text` 屬性即為引擎讀取到的純文字內容。

```csharp
// Step 4: Write the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

若以清晰的收據截圖執行程式，會看到類似以下的輸出：

```
=== OCR Output ===
Item        Qty   Price
Apple       2     $1.20
Banana      5     $0.75
Total               $5.55
```

這就是 **將圖片轉換成文字** 的核心——圖片已變成可儲存、搜尋，或傳入其他系統的字串。

## Step 5: Handling Common Edge Cases

### 5.1 Low‑Resolution Images

當解析度低於 100 dpi 時，OCR 準確度會急速下降。若出現亂碼，請在送入 Aspose OCR 前先對圖片做前處理（提升對比、重新調整大小或套用銳化濾鏡）。

```csharp
// Example: Resize a low‑dpi image to improve accuracy
using var bitmap = new Bitmap(imagePath);
var highRes = new Bitmap(bitmap, new Size(bitmap.Width * 2, bitmap.Height * 2));
highRes.Save("highres_sample.jpg");
var highResResult = ocrEngine.RecognizeImage("highres_sample.jpg");
```

### 5.2 Multi‑Page Documents

即使 Community 模式每次上限 100 頁，你仍可處理 PDF 或多頁 TIFF。引擎會回傳串接的文字，並以 `\f` 保留頁分隔。

```csharp
var multiPageResult = ocrEngine.RecognizeImage("multi_page.pdf");
Console.WriteLine(multiPageResult.Text); // contains form‑feed characters between pages
```

### 5.3 Non‑English Languages

將 `Language` 列舉切換成其他支援的語言：

```csharp
ocrConfig.Language = Language.French; // now the engine expects French characters
```

若使用預設以外的語言，請先安裝相應的語言套件；Aspose 以獨立的 NuGet 套件提供。

## Step 6: Full Working Example

以下是一個完整、可直接貼上執行的主控台範例，能 **辨識圖片文字**、**從 jpg 擷取文字**，並依需求 **設定 OCR 語言**。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Configuration;

class OcrDemo
{
    static void Main()
    {
        // 1️⃣ Configure OCR – change Language to match your source.
        var ocrConfig = new OcrEngineConfig
        {
            Language = Language.English,   // set ocr language
            MaxPagesPerRun = 100
        };

        // 2️⃣ Create the engine inside a using block.
        using var ocrEngine = new OcrEngine(ocrConfig);

        // 3️⃣ Path to the image you want to process.
        string imagePath = @"YOUR_DIRECTORY/sample.jpg";

        // 4️⃣ Perform OCR – this **recognize text from image**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 5️⃣ Output – now you have **convert image to text** results.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**預期輸出**（假設範例圖片內的文字為 “Hello World!”）：

```
=== OCR Output ===
Hello World!
```

執行 `dotnet run` 後，主控台會顯示擷取出的字串。

## Pro Tips & Common Pitfalls

- **Pro tip:** 將 OCR 呼叫包在 `try/catch` 中，以優雅處理損毀的檔案。  
- **Watch out for:** 含有浮水印或大量背景噪點的圖片，常會讓引擎搞混。  
- **Tip:** 若要批次處理多個檔案，可遍歷目錄並重複使用同一個 `OcrEngine` 實例——只要記得在每張圖片處理完後重設相關設定。  
- **Remember:** Community 模式的 100 頁上限是「每次執行」的限制，而非「每個檔案」的限制。若 PDF 超過上限，請自行切割。

## Conclusion

現在你已掌握使用 Aspose OCR 在 C# 中 **辨識圖片文字** 的完整程式碼，從安裝 NuGet 套件、**設定 OCR 語言**、處理低解析度圖片，到 **將圖片轉換成文字**，每一步都已說明。歡迎自行實驗——換語言、改用 PNG，或將輸出串接至下游的搜尋索引。

接下來，你可以探索如何在 Azure Function 中大規模 **從 jpg 擷取文字**，或深入了解 Aspose OCR 的進階功能，例如版面分析與手寫辨識。基礎已建好，未來的擴充將更加輕鬆。

Happy coding, and may your images always be legible!

## What Should You Learn Next?

以下教學與本篇內容緊密相關，能進一步深化你所學的技巧。每篇皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能或探索其他實作方式。

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}