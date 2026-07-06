---
category: general
date: 2026-03-17
description: c# OCR 教學 – 探索如何從圖像檔案提取文字、從 WebP 照片讀取文字，以及使用簡易 OcrEngine 將圖像轉換為文字。
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: zh-hant
og_description: c# OCR 教學示範如何從圖像檔案中提取文字、從 WebP 照片中讀取文字，並只需幾行程式碼即可將圖像轉換為文字。
og_title: C# OCR 教學 – 只需數分鐘即可從圖像中提取文字
tags:
- C#
- OCR
- Image Processing
title: C# OCR 教學：從圖像（WebP、相片）提取文字 – 快速指南
url: /zh-hant/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

the payoff?" etc.

Make sure to keep markdown formatting.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教學 – 從圖片 (WebP、相片) 提取文字

有沒有需要 **從圖片檔案提取文字**，卻不知道在 C# 該從哪裡開始？也許你手上有 WebP 截圖、收據的 JPEG，或是掃描的 PDF 頁面，只想取得裡面的文字。這篇 **c# OCR 教學** 會一步步示範完整、可直接執行的範例，讀取相片中的文字、處理 WebP 及其他現代格式，並將圖片轉換成純文字——只需幾行程式碼。

**有什麼好處？** 你可以把任何文字圖片變成可搜尋的字串，寫入資料庫，或傳給後續的 AI 流程。沒有魔法，只有穩定的 OCR 引擎、幾個 .NET API，以及每一步背後「為什麼」的說明。

## 需要的環境

在開始之前，請確保你已經有：

- **.NET 6 SDK**（或更新版本）。以下程式碼在 .NET 6+ 編譯，能在 Windows、Linux 或 macOS 上執行。
- **Visual Studio 2022** 或你慣用的編輯器（VS Code 也可以）。
- **`Microsoft.Windows.SDK.Contracts`** NuGet 套件（提供 `Windows.Media.Ocr`）。使用以下指令安裝：

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- 一張想要處理的圖片檔案——本教學使用名為 `photo.webp` 的 **WebP** 相片，放在 `YOUR_DIRECTORY` 資料夾內。

> Pro tip: 若你使用非 Windows 平台，可以把 `OcrEngine` 換成跨平台的 **Tesseract**。其餘程式碼基本保持不變。

## 步驟 1：建立 C# OCR 教學專案

先建立一個全新的 console app。打開終端機並執行：

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

安裝上述必要套件，然後在 IDE 中開啟專案。這樣的腳手架讓我們有一個乾淨的起點，開始 **c# OCR 教學**。

## 步驟 2：匯入命名空間並準備圖片

我們需要幾個 `using` 指令，讓編譯器知道 `OcrEngine`、`SoftwareBitmap` 以及圖片載入輔助程式在哪裡。

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **為什麼要匯入這些命名空間？**  
> `Windows.Media.Ocr` 包含實際執行辨識的 `OcrEngine` 類別。`Windows.Graphics.Imaging` 讓我們將圖片（包括 WebP）解碼成 `SoftwareBitmap`，供引擎使用。`System.IO` 與 `Windows.Storage.Streams` 則負責簡化檔案載入。

接著載入圖片。內建的解碼器能處理 WebP、HEIF、PNG、JPEG 等格式，讓你 **從 WebP 讀取文字** 而不需要額外外掛。

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **邊緣情況：** 若圖片已是黑白的，可以省略轉換步驟。灰階轉換雖小，但能提升效能，且常能改善噪點照片的辨識率。

## 步驟 3：執行 OCR 引擎 – 從相片辨識文字

以下是 **c# OCR 教學** 的核心。我們建立 `OcrEngine` 實例、傳入 bitmap，最後取得辨識結果。

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**發生了什麼事？**  
- `TryCreateFromUserProfileLanguages()` 會使用 Windows 使用者個人檔案設定的語言，通常涵蓋英文、中文等。如需特定語言，可改用 `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`。
- `RecognizeAsync` 會在背景執行繁重的辨識工作，回傳包含原始字串、單字邊界框與信心分數的 `OcrResult`。
- 最後我們印出 `ocrResult.Text`，得到 **將圖片轉換成文字** 的結果，之後可以自行處理。

## 步驟 4：完整、可執行的範例

把所有程式碼整合起來，以下是一個可直接貼到 `Program.cs` 的自包含程式。它會編譯、執行，並印出 `photo.webp` 中提取的文字。

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### 預期輸出

若 `photo.webp` 內的文字為 “Hello, world! This is a test.”，你會看到類似以下的結果：

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

實際的換行會依原圖版面而異，但 **從圖片提取文字** 的結果始終是一個純字串，方便後續操作。

## 常見問題與邊緣情況

### 能否支援其他圖片格式？

當然可以。使用的解碼器 (`BitmapDecoder`) 會自動偵測 JPEG、PNG、BMP、GIF、**WebP**、HEIF 等格式。因此你可以 **從 WebP、JPEG，甚至 TIFF** 讀取文字，無需更改程式碼。

### 若 OCR 引擎回傳的信心分數太低該怎麼辦？

可以檢查 `ocrResult.Lines` 以及每個 `OcrWord` 的 `ConfidenceScore`。若分數低於某個門檻（例如 0.6），可考慮：

- 前處理圖片（提升對比、銳化、去除傾斜）。
- 使用更高解析度的原始圖片。
- 改用支援多語言的專門庫，例如 **Tesseract**。

### 如何處理同一張圖片中出現多種語言？

為每種語言建立獨立的 `OcrEngine` 實例，依序執行，或使用支援混合語言偵測的第三方庫。對於內建引擎，可傳入 `Language` 物件：

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### 能在 Linux/macOS 上執行嗎？

`Windows.Media.Ocr` API 只支援 Windows。若在非 Windows 平台，請將 OCR 部分換成 **Tesseract**（透過 `Tesseract.Net.SDK`）。載入與前處理程式碼保持不變，其他部分仍適用於本 **c# OCR 教學**。

## 提升準確度的進階技巧

- **縮放** 大尺寸圖片至長邊不超過 2000 px —— OCR 引擎在中等大小的圖片上速度更快。
- **去噪**：若照片顆粒感強，可使用簡單的高斯模糊。
- **去傾斜**：若文字未完全水平，先將 `SoftwareBitmap` 旋轉後再傳入 `OcrEngine`。
- **快取** `OcrEngine` 實例：若一次處理大量圖片，重複建立會增加開銷，建議保留同一個實例。

## 相關主題探索

- 使用 **Tesseract** 進行 **將圖片轉換成文字** 的跨平台方案。
- 先將 **PDF 轉成圖片**，再 **從 PDF 提取文字**。
- **批次 OCR** 實作

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}