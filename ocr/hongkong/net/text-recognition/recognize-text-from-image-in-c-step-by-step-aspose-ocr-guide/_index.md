---
category: general
date: 2026-08-12
description: 使用 Aspose OCR for C# 從圖像中辨識文字。了解如何從 PNG 提取文字、將圖像轉換為文字，以及處理西里爾語言。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- extract text from png
- convert image to text
- c# image ocr
- aspose ocr c#
language: zh-hant
lastmod: 2026-08-12
og_description: 使用 Aspose OCR 於 C# 識別圖像文字。本指南示範如何從 PNG 提取文字、將圖像轉換為文字，以及處理西里爾文字。
og_image_alt: Diagram showing the OCR processing flow from image file to recognized
  text output
og_title: 在 C# 中辨識圖像文字 – 完整的 Aspose OCR 教學
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: recognize text from image using Aspose OCR for C#. Learn how to extract
    text from PNG, convert image to text, and handle Cyrillic language.
  headline: recognize text from image in C# – step‑by‑step Aspose OCR guide
  type: TechArticle
- description: recognize text from image using Aspose OCR for C#. Learn how to extract
    text from PNG, convert image to text, and handle Cyrillic language.
  name: recognize text from image in C# – step‑by‑step Aspose OCR guide
  steps:
  - name: Expected console output
    text: '``` === Recognized Text === Привет мир! Это пример текста на кириллице.
      ```'
  - name: Recognize text from JPEG or BMP
    text: Replace the PNG file path with a JPEG or BMP file; the same `engine.Image`
      assignment works because Aspose.OCR auto‑detects the format.
  - name: Extract text from multiple pages
    text: 'If you need to **extract text from png** files that represent scanned pages,
      loop over the file list and concatenate the results:'
  - name: Convert image to text in an ASP.NET API
    text: 'Expose the OCR logic through a controller action:'
  type: HowTo
tags:
- Aspose OCR
- C#
- OCR
- Image processing
title: 在 C# 中從圖像辨識文字 – 一步一步 Aspose OCR 教學
url: /zh-hant/net/text-recognition/recognize-text-from-image-in-c-step-by-step-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中從圖像辨識文字 – 步驟式 Aspose OCR 教學

如果您需要在 .NET 應用程式中 **從圖像辨識文字**，本教學提供完整、可直接執行的解決方案。您將看到如何從 PNG 檔案擷取文字、將圖像轉換為文字，以及處理西里爾字元——全部使用 Aspose.OCR C# 程式庫。

本指南涵蓋您今天開始使用 OCR 所需的全部內容：必要的 NuGet 套件、語言設定、圖像載入與錯誤處理。完成後，您將擁有一個在主控台印出辨識字串的程式，並了解如何將程式碼套用至其他圖像格式或語言。

## 前置條件

- .NET 6 SDK 或更新版本（程式碼亦可在 .NET Framework 4.7.2 上執行）
- Visual Studio 2022 或您偏好的任何 C# 編輯器
- 首次執行程式時需要網際網路連線（Aspose.OCR 會自動下載語言模組）
- 一張包含可辨識文字的 PNG 圖像（範例使用 *cyrillic_sample.png*）

> **小技巧：** 請將 PNG 檔案大小控制在 2 MB 以下，以加快處理速度。較大的圖像可在 OCR 前先調整尺寸，以提升辨識準確度。

## 步驟 1：安裝 Aspose.OCR NuGet 套件

在專案資料夾開啟終端機，執行以下指令：

```bash
dotnet add package Aspose.OCR
```

此套件包含核心 OCR 引擎與預設語言模組。當您請求本機未安裝的語言時，Aspose 會自動下載。

## 步驟 2：建立 OCR 引擎並選擇語言

OCR 引擎是執行圖像轉文字的核心物件。對於西里爾文字，您需要將 `Language` 屬性設為 `Language.Cyrillic`。相同的屬性亦可用於其他語言，例如 `Language.English`。

```csharp
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2.1: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Choose the language module – Cyrillic in this example
        engine.Language = Language.Cyrillic;
```

**為什麼重要：** 正確選擇語言可提升字元辨識率，因為引擎會載入該語言的字典與字型。若省略此步驟，引擎會退回使用英語，西里爾字元將會出現亂碼。

## 步驟 3：載入欲處理的圖像

Aspose.OCR 支援多種圖像格式，但 PNG 是常見的無損格式，可保留文字邊緣。使用 `ImageStream.FromFile` 讀取檔案至引擎。

```csharp
        // Step 3: Load the PNG image that contains the text
        engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/cyrillic_sample.png");
```

將 `YOUR_DIRECTORY` 替換為 PNG 檔案的實際路徑。若需從其他資料夾的 **png 檔案擷取文字**，只要相應調整路徑即可。

## 步驟 4：執行 OCR 操作

呼叫 `engine.Recognize()` 會執行 OCR 流程並回傳純文字字串。這即是 **將圖像轉文字** 功能的核心。

```csharp
        // Step 4: Run OCR and get the recognized string
        string recognizedText = engine.Recognize();
```

若圖像無法載入或語言模組下載失敗，該方法會拋出例外。於正式程式碼中請將呼叫包於 try‑catch 區塊。

## 步驟 5：顯示或儲存辨識結果

為了快速示範，您可以將結果寫入主控台。實際應用中則可能將其儲存至資料庫、文字檔，或傳遞給其他服務。

```csharp
        // Step 5: Output the recognized text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

### 預期的主控台輸出

```
=== Recognized Text ===
Привет мир! Это пример текста на кириллице.
```

若圖像包含英文文字，輸出將會是相對應的英文句子。相同程式碼亦可用於多語言的 **c# image ocr** 任務。

## 完整原始碼 – 可直接複製

以下為完整程式碼，包含 `using` 指令與所有步驟於單一檔案中。將其複製至 `Program.cs` 後執行 `dotnet run`。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        try
        {
            // Create an OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Select the Cyrillic language module (downloaded automatically if missing)
            engine.Language = Language.Cyrillic;

            // Load the image that contains Cyrillic text
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/cyrillic_sample.png");

            // Perform the OCR recognition
            string recognizedText = engine.Recognize();

            // Display the recognized text
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"OCR failed: {ex.Message}");
        }
    }
}
```

## 處理常見變化情況

### 從 JPEG 或 BMP 辨識文字

將 PNG 檔案路徑改為 JPEG 或 BMP 檔案；相同的 `engine.Image` 指定仍可使用，因為 Aspose.OCR 會自動偵測格式。

```csharp
engine.Image = ImageStream.FromFile("photo.jpg");
```

### 從多頁擷取文字

若需從代表掃描頁面的 **png 檔案擷取文字**，可遍歷檔案清單並將結果串接起來：

```csharp
string[] files = Directory.GetFiles("scans", "*.png");
var allText = new StringBuilder();

foreach (var file in files)
{
    engine.Image = ImageStream.FromFile(file);
    allText.AppendLine(engine.Recognize());
}
Console.WriteLine(allText.ToString());
```

### 在 ASP.NET API 中將圖像轉文字

透過控制器動作公開 OCR 邏輯：

```csharp
[HttpPost("api/ocr")]
public async Task<IActionResult> Ocr(IFormFile image)
{
    using var stream = image.OpenReadStream();
    OcrEngine engine = new OcrEngine { Language = Language.English };
    engine.Image = ImageStream.FromStream(stream);
    string text = engine.Recognize();
    return Ok(new { text });
}
```

此範例展示了在 Web 服務中的 **c# image ocr**，讓客戶端上傳任意點陣圖並以 JSON 形式取得擷取的文字。

## 效能建議與邊緣情況

- **圖像品質：** 當圖像模糊或對比度低時，OCR 準確度會急劇下降。請在送入引擎前先進行圖像前處理（例如銳化、二值化）。
- **大型檔案：** 若圖像超過 5 MP，請將較長邊縮至最高 2000 px。此舉可減少記憶體使用，同時不影響辨識。
- **語言備援：** 若設定未支援的語言，引擎會預設使用英語。若動態載入語言模組，請在初始化後檢查 `engine.Language`。
- **執行緒安全性：** `OcrEngine` 實例並非執行緒安全。於多執行緒環境（如 ASP.NET Core）請為每個請求建立新引擎。

## 結論

現在您已了解如何在 C# 中使用 Aspose.OCR **從圖像辨識文字**。本教學示範了安裝套件、設定語言、載入 PNG、執行 OCR 以及處理輸出。透過這些基礎，您亦可 **從 png 擷取文字**、**將圖像轉文字**，並為桌面、Web 或雲端情境打造穩健的 **c# image ocr** 解決方案。

接下來，您可以探索其他語言模組（例如 `Language.Spanish`）或將 OCR 結果與自然語言處理函式庫結合。欲進一步效能調校，請參閱 Aspose.OCR 關於圖像前處理與自訂字典的文件。

祝程式開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南技術緊密相關的主題，並提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [使用 Aspose.OCR 以語言選擇擷取 C# 圖像文字](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [從圖像擷取文字 – 使用 Aspose.OCR 進行 .NET OCR 最佳化](/ocr/english/net/ocr-optimization/)
- [如何使用 Aspose.OCR for .NET 擷取圖像文字](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}