---
category: general
date: 2026-05-06
description: 使用 Aspose OCR 於 C# 從圖像擷取文字。了解如何將 JPG 轉換為文字、設定 OCR 語言，並有效率地讀取 JPG 中的文字。
draft: false
keywords:
- extract text from image
- convert jpg to text
- image to text c#
- read text from jpg
- set OCR language
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中從圖像提取文字。本指南說明如何將 JPG 轉換為文字、設定 OCR 語言，以及從 JPG 讀取文字。
og_title: 在 C# 中從圖片提取文字 – 完整教學
tags:
- OCR
- C#
- Aspose
title: 在 C# 中從圖像提取文字 – 逐步指南
url: /zh-hant/net/text-recognition/extract-text-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字（C#） – 完整程式教學

是否曾需要 **從圖像中提取文字**，卻不確定該選哪個函式庫？你並不孤單——開發者常問：「如何在不將資料上傳雲端的情況下，把 JPG 轉成文字？」好消息是，Aspose OCR 提供完整的離線解決方案，直接在 .NET 應用程式內運作。

在本教學中，我們會一步步說明所有必備知識：從安裝 Aspose OCR NuGet 套件、**設定 OCR 語言**（以俄文為例），到最後 **從 JPG 讀取文字**。完成後，你將擁有一段可重複使用的程式碼，直接貼到任何 C# 專案，即可即時從圖像中擷取文字。

> **學完你會得到**  
> • 一個可直接執行的範例，**從圖像檔案提取文字**。  
> • 使用 Aspose OCR 引擎 **將 JPG 轉成文字** 的完整流程。  
> • 多語系情境下 **設定 OCR 語言** 的技巧。  
> • 處理無法辨識圖像與缺少語言套件的邊緣案例。

## 前置條件

在開始之前，請確認你已具備以下項目：

| 前置條件 | 為何重要 |
|-------------|----------------|
| .NET 6.0 或更新版本（任何近期的 .NET 執行環境） | Aspose OCR 以 .NET Standard 2.0+ 為目標，較新的執行環境可提供最佳效能。 |
| Visual Studio 2022（或安裝 C# 擴充功能的 VS Code） | 友善的 IDE 能讓你快速除錯 OCR 流程。 |
| 只需 **一次** 的網路連線以下載 Aspose OCR NuGet 套件 | 首次安裝後即可啟用 **離線資源**，避免之後再下載。 |
| 一張包含俄文文字的範例 JPG 圖片（`input.jpg`），或任何你打算使用的語言 | 教學示範使用俄文範例，你可以自行換成已安裝語言套件的圖像。 |

若上述項目對你來說陌生，別擔心。安裝 NuGet 套件只需要一條指令，其他步驟對所有 Aspose 支援的圖像格式皆相同。

## 解決方案概觀

高層次的流程如下：

1. **建立** `OcrEngine`，並啟用離線資源，避免執行時自動下載語言資料。  
2. **設定** 目標語言（例如俄文），使用 `OcrLanguage` 列舉。  
3. **呼叫** `RecognizeImage` 讀取本機 JPG 檔案。  
4. **輸出** 取得的字串至主控台，或自行串接到其他工作流程。

以下示意圖說明資料流向：

![Extract text from image using Aspose OCR in C#](https://example.com/placeholder-image.png){.align-center alt="extract text from image using Aspose OCR in C#"}

*此圖僅為示意，實際的運算由程式碼完成。*

## 從圖像中提取文字 – 核心概念

在撰寫程式碼前，先釐清幾個常讓開發者卡關的概念：

- **OfflineResources** – 設為 `true` 時，Aspose OCR 只會搜尋你事先下載好的語言套件，避免在生產環境因自動下載而造成啟動延遲。  
- **OcrLanguage** – 此列舉包含數十種語言代碼（`English`、`Russian`、`Japanese` …），正確選擇可大幅提升辨識準確度，因為引擎會套用語言專屬的啟發式演算法。  
- **影像品質** – OCR 在高對比、無噪點的圖像上表現最佳。若結果雜亂，建議先做前處理（例如二值化）再交給引擎。

了解這些要點後，你就能判斷何時需要 **手動設定 OCR 語言**，以及為何 **將 JPG 轉成文字** 並非單行程式即可完成。

## 步驟 1：安裝 Aspose OCR NuGet 套件

在專案資料夾的終端機中執行：

```bash
dotnet add package Aspose.OCR
```

*小技巧：首次安裝後，加上 `-v latest` 參數可確保每次取得最新的穩定版。套件大小約 15 MB，對大多數桌面或伺服器部署而言相當合理。*

## 步驟 2：將 JPG 轉成文字 – 初始化引擎

套件安裝完成後，建立一個支援離線模式的 `OcrEngine`。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine with offline resources.
        // This prevents the SDK from trying to download language data at runtime.
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            OfflineResources = true   // <-- crucial for production stability
        });

        // Step 2.2: Choose the language pack you need.
        // Here we use Russian; replace with OcrLanguage.English for English text.
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 2.3: Perform OCR on a local JPG file.
        // The file path can be absolute or relative to the executable.
        var result = ocrEngine.RecognizeImage("YOUR_DIRECTORY/input.jpg");

        // Step 2.4: Output the extracted text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(result.Text);
    }
}
```

### 為何這麼做

- **離線模式** 確保啟動時間可預測——部署到受限伺服器時不會有意外的網路呼叫。  
- **設定語言** (`OcrLanguage.Russian`) 讓引擎使用俄文字元集，對乾淨的圖像，辨識正確率可從約 70 % 提升至 >95 %。  
- `RecognizeImage` 方法接受 Aspose 支援的任何影像格式（`.jpg`、`.png`、`.tiff` …），因此我們能 **直接從 JPG 讀取文字**，不必額外轉檔。

## 步驟 3：設定 OCR 語言 – 處理多語系

有時文件會混雜多種語言（例如俄文與英文）。Aspose OCR 允許你指定 *備援* 語言陣列：

```csharp
// Example: Russian primary, English secondary
ocrEngine.Language = OcrLanguage.Russian;
ocrEngine.AdditionalLanguages = new[] { OcrLanguage.English };
```

當主要語言無法辨識某個字元時，引擎會自動檢查備援清單。此技巧特別適合發票等同時包含西里爾字母公司名稱與英文商品代碼的情境。

> **注意：** 語言套件必須放在專案的 `Resources` 資料夾內。若出現 `FileNotFoundException`，請從 Aspose 入口網站下載缺少的套件，並放置於執行檔旁。

## 步驟 4：從 JPG 讀取文字 – 常見問題與解決方式

即使語言套件正確，仍可能遇到以下情況：

| 問題 | 常見徵兆 | 快速解法 |
|-------|-----------------|-----------|
| 低對比度 | 輸出雜亂或空白 | 使用 `System.Drawing` 先做簡易對比度拉伸。 |
| 影像旋轉 | 文字呈側向 | 在呼叫 `RecognizeImage` 前設定 `ocrEngine.ImageRotation = OcrRotation.Rotate90;`（或 180/270）。 |
| 檔案過大 | 辨識緩慢、記憶體占用高 | 將長邊縮減至最多 2000 px，辨識品質仍能維持。 |

以下是一段緊湊的輔助函式，會在送入引擎前先調整大小與增強影像：

```csharp
using System.Drawing;
using System.Drawing.Imaging;

static string PreprocessAndRead(string jpgPath)
{
    // Load the original image
    using var original = new Bitmap(jpgPath);

    // Resize while preserving aspect ratio (max 2000px)
    int maxDim = 2000;
    int newWidth, newHeight;
    if (original.Width > original.Height)
    {
        newWidth = maxDim;
        newHeight = original.Height * maxDim / original.Width;
    }
    else
    {
        newHeight = maxDim;
        newWidth = original.Width * maxDim / original.Height;
    }

    using var resized = new Bitmap(original, new Size(newWidth, newHeight));

    // Optional: increase contrast (simple linear stretch)
    var contrast = new ImageAttributes();
    float[][] matrix = {
        new float[] {1.2f, 0, 0, 0, 0},
        new float[] {0, 1.2f, 0, 0, 0},
        new float[] {0, 0, 1.2f, 0, 0},
        new float[] {0, 0, 0, 1, 0},
        new float[] {0, 0, 0, 0, 1}
    };
    contrast.SetColorMatrix(new ColorMatrix(matrix));

    using var graphics = Graphics.FromImage(resized);
    graphics.DrawImage(resized, new Rectangle(0, 0, newWidth, newHeight), 0, 0, newWidth, newHeight, GraphicsUnit.Pixel, contrast);

    // Save to a temporary file (Aspose OCR works with file paths)
    string tempPath = Path.GetTempFileName() + ".jpg";
    resized.Save(tempPath, ImageFormat.Jpeg);

    // Run OCR
    var engine = new OcrEngine(new OcrEngineSettings { OfflineResources = true });
    engine.Language = OcrLanguage.Russian;
    var res = engine.RecognizeImage(tempPath);
    File.Delete(tempPath); // clean up
    return res.Text;
}
```

現在你可以呼叫 `Console.WriteLine(PreprocessAndRead("YOUR_DIRECTORY/input.jpg"));`，取得更乾淨的結果。

## 完整範例 – 一檔搞定全部步驟

以下是可直接貼到 `Program.cs` 的 **完整程式**，內含安裝說明、語言設定、前處理與錯誤處理。

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        string imagePath = "YOUR_DIRECTORY/input.jpg";

        try
        {

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}

提供 ONLY the translated content, no explanations.