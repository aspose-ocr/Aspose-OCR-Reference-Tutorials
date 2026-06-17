---
category: general
date: 2026-03-21
description: c# OCR 教學：學習如何使用 C# 透過 OCR 從 PNG 圖片中擷取烏爾都文文字。包含逐步程式碼、語言設定與實用技巧。
draft: false
keywords:
- c# ocr tutorial
- extract urdu text
- recognize text image
- how to extract urdu
- ocr from png file
language: zh-hant
og_description: c# OCR 教學：學習如何使用 C# 透過 OCR 從 PNG 圖像中提取烏爾都文文字。完整指南，附程式碼與技巧。
og_title: C# OCR 教學 – 從 PNG 圖像提取烏爾都文字
tags:
- OCR
- C#
- Urdu
- Image Processing
title: C# OCR 教學 – 從 PNG 圖像中提取烏爾都語文字
url: /zh-hant/net/text-recognition/c-ocr-tutorial-extract-urdu-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr 教程 – 從 PNG 圖像提取烏爾都文字

是否曾經需要一個 **c# ocr 教程**，能真正從 PNG 檔案中提取烏爾都文字？你並不孤單。在許多專案——發票處理、文件歸檔，甚至快速翻譯工具——你都會遇到必須辨識圖像文字資料的情況，而語言是關鍵。

在本指南中，我們將逐步說明一個完整、可直接執行的解決方案，使用 OCR 引擎從 PNG 中提取烏爾都文字。你將了解每一行程式碼的原因、如何處理缺少的語言套件，以及當圖像不夠完美時該怎麼辦。完成後，你將有信心將此程式碼套用到其他語言或檔案類型。

## 你將學到

- 如何設定 C# OCR 函式庫（沒有隱藏的魔法）
- 從 PNG 檔案 **提取烏爾都文字** 的完整步驟
- 為何將語言設定為烏爾都很重要，以及引擎如何自動下載缺少的資料
- 驗證輸出的方法以及排除常見問題的技巧

不需要外部文件連結——所有你需要的資訊都在這裡。

## 前置條件（開始前需要的項目）

| 需求 | 為何重要 |
|------|----------|
| .NET 6.0+（或 .NET Core 3.1） | 現代 API 與 async 支援 |
| Visual Studio 2022（或配備 C# 擴充功能的 VS Code） | 具備 IntelliSense 的 IDE 讓程式碼更清晰 |
| 提供 `OcrEngine` 的 OCR 函式庫（例如 **Microsoft.Windows.SDK.Contracts** 或第三方 NuGet） | 提供 `Language.Urdu` 與 `Recognize` 方法 |
| 包含烏爾都文字的 PNG 圖像（例如 `urdu_invoice.png`） | **recognize text image** 操作的來源 |

如果尚未安裝 OCR 套件，請在 Package Manager Console 中執行以下單行指令：

```powershell
Install-Package Microsoft.Windows.SDK.Contracts
```

這會將我們稍後會使用的 `OcrEngine` 類別加入專案。

> **小技巧：** SDK 會在首次使用時自動下載語言資料，因此不需要手動下載烏爾都語言套件。

## 步驟 1：安裝並參考 OCR 函式庫

在建立引擎之前，必須先在專案中參考 OCR 套件。請在檔案頂部加入以下 `using` 指令：

```csharp
using System;
using Windows.Media.Ocr;          // Core OCR classes
using Windows.Graphics.Imaging;   // For loading PNG files
using Windows.Storage;            // File handling helpers
```

這些命名空間讓我們可以使用 `OcrEngine`、`Language` 以及圖像載入工具。如果你使用其他函式庫，請尋找相對應的命名空間。

## 步驟 2：建立 OCR 引擎實例  

現在我們實際啟動引擎。可以把引擎想像成將像素模式解讀為字元的大腦。

```csharp
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));
if (ocrEngine == null)
{
    Console.WriteLine("Failed to create OCR engine for Urdu. Check your language pack.");
    return;
}
```

**為何重要：** `TryCreateFromLanguage` 若語言資料不存在會回傳 `null`，讓我們能夠快速失敗，而不是稍後崩潰。

## 步驟 3：載入 PNG 圖像  

OCR 引擎使用 `SoftwareBitmap` 物件，而非原始檔案路徑。以下輔助程式會從磁碟載入 PNG 並轉換為所需的格式。

```csharp
// Step 3: Load the PNG image into a SoftwareBitmap
async Task<SoftwareBitmap> LoadImageAsync(string path)
{
    StorageFile file = await StorageFile.GetFileFromPathAsync(path);
    using var stream = await file.OpenReadAsync();
    var decoder = await BitmapDecoder.CreateAsync(stream);
    // Convert to Gray8 for best OCR accuracy
    return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
}
```

**邊緣情況：** 若 PNG 為彩色圖，轉換為灰階 (`Gray8`) 通常能提升辨識率，特別是對於像烏爾都這類擁有細緻變音符號的文字。

## 步驟 4：從圖像辨識文字  

這就是 **c# ocr 教程** 的核心——請求引擎讀取圖像。

```csharp
// Step 4: Perform OCR on the loaded bitmap
async Task<string> RecognizeUrduAsync(string imagePath)
{
    SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
    OcrResult result = await ocrEngine.RecognizeAsync(bitmap);
    return result.Text;
}
```

`OcrResult.Text` 屬性包含原始的 Unicode 字串。因為我們先前將語言設定為烏爾都，引擎會套用正確的文字規則。

## 步驟 5：輸出並驗證提取的文字  

最後，我們將結果印到主控台。在實際應用中，你可能會將它儲存至資料庫或傳送給翻譯服務。

```csharp
// Step 5: Run the OCR and display the result
static async Task Main(string[] args)
{
    string imageFile = @"C:\Images\urdu_invoice.png"; // adjust path as needed
    string extracted = await RecognizeUrduAsync(imageFile);
    Console.WriteLine("=== Extracted Urdu Text ===");
    Console.WriteLine(extracted);
}
```

**預期結果：** 若圖像清晰，你會看到類似以下的輸出：

```
=== Extracted Urdu Text ===
بل نمبر: 12345
تاریخ: 21/03/2026
کل رقم: 5,000 روپے
```

如果輸出呈現亂碼，請檢查圖像品質（對比度、噪點），並考慮先行前處理（例如二值化）。

## 如何從 PNG 檔案提取烏爾都文字 – 常見陷阱  

1. **低對比度** – 當前景與背景顏色相近時 OCR 會困難。請在執行程式前使用圖像編輯工具提升對比度。  
2. **DPI 不正確** – 以 300 dpi 或更高的解析度掃描，可提供引擎更多細節。  
3. **缺少語言套件** – 第一次呼叫 `TryCreateFromLanguage` 可能會觸發下載；請確保你的機器能連上網路。  

解決上述問題可大幅提升 **recognize text image** 的成功率。

## Recognize Text Image：擴展至其他格式  

雖然本教程以 PNG 為例，但相同的工作流程同樣適用於 JPEG、BMP 或 TIFF——只需更改檔案副檔名並確保解碼器支援即可。關鍵程式碼仍為 `await ocrEngine.RecognizeAsync(bitmap);`。

## PNG 檔案 OCR 小技巧 – 效能與擴充性  

- **批次處理：** 將多張圖像載入清單，使用 `Task.WhenAll` 平行執行辨識。  
- **快取引擎：** 建立單一 `OcrEngine` 實例並在多次呼叫間重複使用；重複建構會增加額外負擔。  
- **記憶體管理：** 使用完畢後釋放 `SoftwareBitmap` 物件（`bitmap.Dispose()`），以保持程式執行效能。

## 完整可執行範例（直接複製貼上）  

以下是完整程式碼，你可以直接編譯執行。它包含所有 using 陳述式、非同步處理與錯誤檢查。

```csharp
// Full C# OCR tutorial – Extract Urdu text from a PNG file
using System;
using System.Threading.Tasks;
using Windows.Media.Ocr;
using Windows.Graphics.Imaging;
using Windows.Storage;

class Program
{
    // Initialize the OCR engine for Urdu
    private static OcrEngine _ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));

    static async Task Main(string[] args)
    {
        if (_ocrEngine == null)
        {
            Console.WriteLine("Urdu language pack not available. Ensure internet connectivity for automatic download.");
            return;
        }

        string imagePath = @"C:\Images\urdu_invoice.png"; // <-- change to your image location
        string text = await RecognizeUrduAsync(imagePath);
        Console.WriteLine("=== Extracted Urdu Text ===");
        Console.WriteLine(text);
    }

    // Load PNG and convert to grayscale bitmap
    private static async Task<SoftwareBitmap> LoadImageAsync(string path)
    {
        StorageFile file = await StorageFile.GetFileFromPathAsync(path);
        using var stream = await file.OpenReadAsync();
        var decoder = await BitmapDecoder.CreateAsync(stream);
        return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
    }

    // Perform OCR and return the recognized text
    private static async Task<string> RecognizeUrduAsync(string imagePath)
    {
        SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
        OcrResult result = await _ocrEngine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

**預期輸出：** 主控台會印出圖像中找到的烏爾都字元，保持從右至左的順序。

## 結論  

你剛完成一個 **c# ocr 教程**，示範如何從 PNG **提取烏爾都文字**、設定語言並安全處理結果。這些步驟——安裝函式庫、建立引擎、載入圖像、辨識文字以及輸出——構成可重複使用的模式，適用於任何文字或檔案類型。

接下來，你可以嘗試在多頁 PDF（先將每頁轉為 PNG）上使用 **recognize text image**，或整合翻譯 API，自動將提取的烏爾都文字轉為英文。掌握此核心工作流程後，無所不能。

祝程式開發愉快，願你的 OCR 結果清晰如水晶！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}