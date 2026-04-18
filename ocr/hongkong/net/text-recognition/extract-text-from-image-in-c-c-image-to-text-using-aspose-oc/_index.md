---
category: general
date: 2026-04-17
description: 使用 Aspose OCR 在 C# 中提取圖像文字。學習如何從 PNG 讀取文字、將圖像轉換為文字，以及在幾分鐘內載入圖像進行 OCR。
draft: false
keywords:
- extract text from image
- read text from png
- convert image to text
- c# image to text
- load image for ocr
language: zh-hant
og_description: 使用 Aspose OCR 於 C# 從圖像提取文字。本教學示範如何從 PNG 讀取文字、將圖像轉換為文字，以及高效載入圖像進行 OCR。
og_title: 使用 C# 從圖片提取文字 – 完整 Aspose OCR 指南
tags:
- Aspose OCR
- C#
- Image Processing
title: 在 C# 中從圖像提取文字 – 使用 Aspose OCR 的 C# 圖像轉文字
url: /zh-hant/net/text-recognition/extract-text-from-image-in-c-c-image-to-text-using-aspose-oc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字（C#） – 完整 Aspose OCR 指南

有沒有曾經需要**從圖像中提取文字**，卻不確定該選哪個函式庫？你並不孤單。許多開發者在面對 PNG 截圖、掃描發票或多語言標示，想把像素轉換成可搜尋的文字時，都會卡在這裡。  

在本教學中，我們將一步步示範一個實作解決方案，讓你能使用 Aspose OCR **從 PNG 讀取文字**、**將圖像轉換為文字**，以及**載入圖像以進行 OCR**——全部以乾淨、現代的 C# 撰寫。完成後，你將擁有一個可直接放入任何 .NET 專案的即用程式。

## 你將學會

- 如何載入圖像檔案以供 OCR（即「載入圖像以進行 OCR」步驟）  
- 如何為特定語言群組設定 Aspose OCR  
- 如何提取辨識出的字串並在主控台顯示  
- 處理多語言、大檔案與記憶體管理的技巧  

不需要額外文件；以下程式碼片段已包含所有必需資訊。

## 前置條件

- .NET 6+ SDK（或 .NET Core 3.1+——API 相同）  
- Visual Studio 2022、VS Code，或任何你慣用的 IDE  
- NuGet 套件 **Aspose.OCR**（使用 `dotnet add package Aspose.OCR` 安裝）  

如果你已備妥，讓我們開始吧。

![使用 Aspose OCR 在 C# 中提取圖像文字](https://example.com/aspsoe-ocr-demo.png "使用 Aspose OCR 提取圖像文字")

## 步驟 1 – 載入圖像以進行 OCR

首先，你必須提供 OCR 引擎可讀取的圖像。Aspose OCR 支援多種格式，但 PNG 是截圖與掃描圖形的常見選擇。

```csharp
using Aspose.OCR;

// Replace with the actual path to your PNG file
string imagePath = @"C:\Images\sample.png";

// OcrImage.FromFile handles PNG, JPEG, BMP, TIFF, etc.
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

> **為什麼這很重要：** 正確載入圖像可確保引擎看到你預期的像素資料。若傳入損壞的串流，辨識會靜默失敗。

## 步驟 2 – 建立並設定 OCR 引擎

接著，實例化 `OcrEngine`。你可以選擇設定語言群組；對於多數西文字體預設即可，但若處理西里爾文、阿拉伯文或亞洲文字，建議事先告訴引擎使用哪種語言。

```csharp
// The using statement guarantees proper disposal of native resources.
using var ocrEngine = new OcrEngine();

// Example: set language to Cyrillic if your PNG contains Russian or Ukrainian text.
// OcrLanguage.Cyrillic covers several Slavic languages.
ocrEngine.Language = OcrLanguage.Cyrillic;

// If you need to support multiple languages, you can combine flags:
 // ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

> **專業提示：** 設定語言會縮小引擎搜尋的字元集，從而加快辨識速度並提升準確度。

## 步驟 3 – 執行 OCR 並提取文字

現在開始進行繁重的辨識工作。使用先前載入的圖像呼叫 `Recognize`，然後從結果中讀取 `Text` 屬性。

```csharp
// Run OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);

// The recognized string is available via the Text property
string extractedText = ocrResult.Text;

// Output the result to the console (or write to a file, DB, etc.)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(extractedText);
```

### 預期輸出

如果 `sample.png` 包含「Hello, World!」這句話，你會看到：

```
=== OCR Output ===
Hello, World!
```

若圖像較為複雜（例如多行收據），引擎會保留換行，提供一段可直接處理的文字區塊。

## 步驟 4 – 將所有程式碼整合成完整範例

以下是完整、獨立的主控台應用程式範例，你可以直接複製貼上到新的 C# 專案中。程式碼內含錯誤處理與說明每個步驟的註解。

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Load the image you want to recognize
                // Change the path to point at your own PNG file.
                var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.png");

                // 2️⃣ Create an OCR engine instance (disposed automatically)
                using var ocrEngine = new OcrEngine();

                // 3️⃣ Choose the language group.
                // Cyrillic works for Russian, Ukrainian, Bulgarian, etc.
                // For English only, you could use OcrLanguage.English.
                ocrEngine.Language = OcrLanguage.Cyrillic;

                // 4️⃣ Perform OCR
                var ocrResult = ocrEngine.Recognize(ocrImage);

                // 5️⃣ Output the recognized text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Simple error handling – in production you’d log this.
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

在專案資料夾執行程式（`dotnet run`），即可在主控台看到提取出的字串。這就是完整的 **從圖像中提取文字** 工作流程，程式碼不到 30 行。

## 步驟 5 – 常見變化與邊緣情況

### 從 PNG 與其他格式讀取文字的差異

雖然範例使用 PNG，Aspose OCR 亦支援 JPEG、BMP、TIFF 與 GIF。只要更改檔案副檔名，即可使用相同的 `OcrImage.FromFile` 呼叫，無需其他修改。

### 在 Web API 中將圖像轉換為文字

若需透過 HTTP 端點提供此功能，可接受 `IFormFile` 上傳，使用 `OcrImage.FromStream` 將串流轉為 `OcrImage`，再以 JSON 回傳字串。核心 OCR 邏輯保持不變。

```csharp
// Example snippet inside an ASP.NET Core controller action
[HttpPost("api/ocr")]
public async Task<IActionResult> OcrUpload(IFormFile file)
{
    using var stream = file.OpenReadStream();
    var ocrImage = OcrImage.FromStream(stream);
    using var engine = new OcrEngine { Language = OcrLanguage.English };
    var result = engine.Recognize(ocrImage);
    return Ok(new { text = result.Text });
}
```

### 處理大型圖像

大型高解析度圖像會佔用大量記憶體。實務上可在送入引擎前先將圖像縮小：

```csharp
// Reduce resolution to 150 DPI (good trade‑off between speed and accuracy)
ocrEngine.ImagePreprocessing = ImagePreprocessingOptions.AutoResize;
ocrEngine.Dpi = 150;
```

### 多語言文件

若文件同時包含英文與西里爾文，可結合語言旗標：

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

引擎會嘗試辨識兩套字元。

### 釋放資源

`using` 包裹 `OcrEngine` 可確保釋放原生資源。若遺忘此步驟，長時間執行的服務可能會發生記憶體泄漏。

## 可靠 OCR 的專業技巧

- **清晰圖像勝出：** 在 OCR 前使用如 **ImageSharp** 等函式庫進行圖像前處理（去斜、去噪）。  
- **字體大小重要：** 小於 10 px 的文字常被遺漏；可考慮將圖像放大。  
- **檢查 `ocrResult.Confidence`：** `OcrResult` 物件會提供每個單字的信心分數——可用於標記低信心區段以供人工審核。  
- **批次處理：** 若有數十個檔案，重複使用同一個 `OcrEngine` 實例，可避免重複初始化的開銷。

## 結論

你剛剛學會如何在 C# 中使用 Aspose OCR **從圖像中提取文字**，涵蓋從 **載入圖像以進行 OCR** 到 **將圖像轉換為文字** 以及 **從 PNG 讀取文字** 的完整流程。完整且可執行的範例展示了所需的精確程式碼，說明每個步驟的原因，並提供實務情境的變化方式。

準備好接受下一個挑戰了嗎？試著將提取的字串輸入搜尋索引、使用 Azure Cognitive Services 進行翻譯，或以相同文字層產生可搜尋的 PDF。可能性無窮，而你現在已具備任何 **c# image to text** 專案的堅實基礎。

歡迎自行實驗、調整語言設定，或將此程式碼片段整合至更大的應用程式中。若遇到任何問題，請在下方留言——祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}