---
category: general
date: 2026-02-20
description: c# OCR 教學，示範如何從圖像提取文字、辨識 PNG 文字，並僅用幾行程式碼將圖像轉換為文字。
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from png
- convert image to text
- how to extract text
language: zh-hant
og_description: C# OCR 教學，帶你一步步從圖像檔案提取文字、辨識 PNG 圖片中的文字，並使用 Aspose.OCR 將圖像轉換為文字。
og_title: C# OCR 教學 – 快速指南：從圖像提取文字
tags:
- OCR
- C#
- Aspose
title: c# OCR 教學 – 使用 Aspose.OCR 從圖片提取文字
url: /zh-hant/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教學 – 使用 Aspose.OCR 從圖像提取文字

有沒有曾經需要一個實際可用於真實 PNG 檔案的 **c# OCR 教學**？你並不是唯一遇到這種情況的人。在許多專案中——例如發票掃描、收據歸檔或簡單的螢幕截圖解析——開發者在嘗試 **從圖像提取文字** 時常會卡住，因為缺乏可靠的函式庫。

好消息是 Aspose.OCR 讓整個流程變得輕而易舉。在本指南中，我們將逐步說明一個完整且可執行的範例，展示 **如何從 PNG 提取文字**，說明每一行程式碼的 *原因*，並且觸及授權與圖像前處理等邊緣情況。完成後，你將能夠 **從 png 識別文字** 並 **將圖像轉換為文字**，僅需少量 C# 程式碼。

## 本教學涵蓋內容

- 在 .NET 主控台應用程式中設定 Aspose.OCR 引擎。  
- 從磁碟載入 PNG（或任何支援的點陣圖）。  
- 執行 OCR 並將結果輸出至主控台。  
- 可選的授權、錯誤處理與效能技巧。  

不需要外部服務，也沒有隱藏的魔法——只有純粹的 C# 程式碼，你可以直接複製貼上並執行。如果你曾經想知道 **如何從掃描文件提取文字**，請繼續閱讀；我們會在過程中回答這個問題以及一些「如果…」的情境。

## 前置條件

- .NET 6.0 SDK 或更新版本（程式碼亦可在 .NET Framework 4.7+ 上執行）。  
- Visual Studio 2022（或任何你喜歡的編輯器）。  
- 免費或付費的 Aspose.OCR for .NET NuGet 套件。  
- 一個名為 `sample.png` 的圖像檔案，放置於可參考的資料夾中。  

就這樣——不需要其他第三方工具。

## c# OCR 教學：設定 Aspose.OCR

首先，你需要 Aspose.OCR 函式庫。於專案資料夾的終端機中執行以下指令：

```bash
dotnet add package Aspose.OCR
```

此指令會取得最新的穩定版並加入必要的 DLL 參考。如果你有授權檔案 (`Aspose.OCR.lic`)，請備妥；否則免費試用版仍可使用，但 OCR 結果會帶有浮水印。

### 為何授權很重要

若未提供授權，引擎會以評估模式執行，會在某些語系的輸出中插入「Powered by Aspose」字樣。對於正式環境的程式碼，你應在早期呼叫 `SetLicense`，如下方程式碼所示。這只是一行呼叫，但可移除浮水印並解鎖全速處理。

## 使用 Aspose.OCR 從圖像提取文字

現在讓我們深入實作 OCR 程式碼。以下是一個 **完整、獨立** 的程式，你可以立即編譯並執行。

```csharp
using System;
using System.Drawing;          // Needed for Image class
using Aspose.OCR;               // Core OCR namespace
using Aspose.OCR.Models;       // For OCR settings (optional)

class LicenseCheck
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2 (Optional): Apply your Aspose.OCR license
        // -------------------------------------------------
        // Uncomment and set the correct path if you have a license file.
        // ocrEngine.SetLicense(@"C:\MyLicenses\Aspose.OCR.lic");

        // -------------------------------------------------
        // Step 3: Load the image you want to process
        // -------------------------------------------------
        // You can use any supported format (png, jpg, bmp, tiff, etc.)
        string imagePath = @"C:\Images\sample.png";
        Image inputImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // Step 4: Recognize text from the loaded image
        // -------------------------------------------------
        // The Recognize method returns a plain string.
        string recognizedText = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 5: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**這段程式在做什麼？**  

1. **Engine creation** – `OcrEngine` 為主要入口點，會在內部載入語言資料。  
2. **License loading** – 雖非必須但建議執行；只需指向你的 `.lic` 檔案。  
3. **Image loading** – `Image.FromFile` 可用於任何點陣圖格式；我們使用 PNG 因為它保留無損品質，對 OCR 準確度至關重要。  
4. **Recognition** – `ocrEngine.Recognize` 完成所有繁重的辨識工作，回傳包含偵測到字元的字串。  
5. **Output** – 我們將結果寫入主控台，但也可以輕鬆寫入檔案、資料庫或 UI 控制項。

### 預期輸出

若 `sample.png` 內含文字 “Hello World”，主控台將顯示：

```
=== OCR Result ===
Hello World
```

如果圖像模糊或包含非拉丁字元，輸出可能會出現亂碼。這時就需要前處理（對比度調整、二值化），相關內容將在下一節說明。

## 從 PNG 檔案識別文字 – 提示與技巧

PNG 是常用的格式，因為它儲存像素時不會產生壓縮雜訊。然而，並非所有 PNG 都一樣。以下提供幾個實用的提示，或許對你有幫助：

- **Resolution matters** – 目標解析度至少 300 dpi。低於此值可能導致遺漏字元。  
- **Color vs. Grayscale** – 在 OCR 前將彩色 PNG 轉為灰階可提升速度，同時不影響準確度。  
- **Noise removal** – 小雜訊常會干擾引擎，使用簡單的中值濾波即可改善。  

以下是一段快速程式碼片段，示範如何在送入 Aspose.OCR 前對圖像進行前處理：

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
Bitmap grayBitmap = new Bitmap(inputImage.Width, inputImage.Height);
using (Graphics g = Graphics.FromImage(grayBitmap))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}});
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(inputImage, new Rectangle(0,0,grayBitmap.Width,grayBitmap.Height),
                0,0,inputImage.Width,inputImage.Height, GraphicsUnit.Pixel, attributes);
}

// Optional: Apply a simple binary threshold
Bitmap binBitmap = new Bitmap(grayBitmap.Width, grayBitmap.Height);
for (int y = 0; y < grayBitmap.Height; y++)
{
    for (int x = 0; x < grayBitmap.Width; x++)
    {
        Color pixel = grayBitmap.GetPixel(x, y);
        int bw = pixel.R < 128 ? 0 : 255; // threshold at 128
        binBitmap.SetPixel(x, y, Color.FromArgb(bw, bw, bw));
    }
}

// Now run OCR on the cleaned bitmap
string cleanedText = ocrEngine.Recognize(binBitmap);
Console.WriteLine(cleanedText);
```

**Pro tip:** 若你要處理數十張圖像，請只建立一次 `OcrEngine` 並重複使用。每張圖像重新建立引擎會產生不必要的開銷。

## 圖像轉文字 – 進階選項

Aspose.OCR 不僅限於純文字提取。你可以要求它回傳 **structured data**（例如單字的邊界框），或設定 **language hints** 以提升多語言文件的辨識準確度。

```csharp
// Set language to English + Spanish (ISO codes)
ocrEngine.Language = Language.English | Language.Spanish;

// Request detailed OCR result
OcrResult result = ocrEngine.RecognizeImage(inputImage, OcrOptions.DetectTextBlocks);

// Iterate over detected words
foreach (var word in result.Words)
{
    Console.WriteLine($"{word.Text} (x:{word.Bounds.X}, y:{word.Bounds.Y})");
}
```

`OcrResult` 物件會提供每個單字的座標，這對於在 UI 中標示文字或後續處理（例如隱藏敏感資訊）相當有用。

## 在實務情境中如何提取文字

讓我們來探討幾個在正式環境中常見的「如果…」問題。

### 如果圖像是 PDF 頁面？

Aspose.OCR 可以直接讀取 PDF，但需要先使用 Aspose.PDF 函式庫將每頁光柵化為圖像。工作流程如下：

1. 使用 `Aspose.Pdf.Document` 載入 PDF。  
2. 將頁面轉換為位圖（`PdfConverter`）。  
3. 將位圖送入 `OcrEngine.Recognize`。  

### 如果 OCR 結果出現亂碼？

常見原因包括解析度過低、噪點過多或不支援的字型。可嘗試以下方法：

- 將圖像放大（`Bitmap` 重設大小）。  
- 套用銳化濾波。  
- 指定正確的語言（如前所示）。  

### 如果需要平行處理圖像？

由於 `OcrEngine` 並非執行緒安全，請為每個執行緒建立 **獨立的實例**，或使用執行緒本地的池。以下是 `Parallel.ForEach` 的範例：

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine(); // each thread gets its own engine
    var img = Image.FromFile(path);
    string text = engine.Recognize(img);
    // Store or log 'text' as needed
});
```

## 完整可執行範例

將上述所有內容整合，以下是一個可直接放入全新主控台專案的精簡版本：

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialize OCR engine (single instance for this demo)
        OcrEngine engine = new OcrEngine();

        // Uncomment if you have a license file
        // engine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Path to the PNG you want to read
        string file = @"C:\Images\sample.png";

        // Load, optionally preprocess, then recognize
        using (Image img = Image.FromFile(file))
        {
            string text = engine.Recognize(img);
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(text);
        }
    }
}
```

使用 `dotnet run` 編譯並執行，即可在主控台看到提取的文字。簡單吧？這就是良好設計的魅力所在。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}