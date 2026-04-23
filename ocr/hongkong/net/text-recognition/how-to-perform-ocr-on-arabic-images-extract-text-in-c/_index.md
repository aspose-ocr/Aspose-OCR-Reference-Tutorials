---
category: general
date: 2026-02-13
description: 了解如何對阿拉伯語圖像執行 OCR，並從 JPG 中提取阿拉伯語文字。本分步指南將示範如何使用 C# 讀取圖像文字並將圖像轉換為文字。
draft: false
keywords:
- how to perform OCR
- extract arabic text
- read image text
- extract text jpg
- convert image to text
language: zh-hant
og_description: 如何對阿拉伯語圖片執行 OCR 並提取阿拉伯文字。請參考本完整指南，從 JPG 檔案讀取圖片文字，並在 C# 中將圖片轉換為文字。
og_title: 如何對阿拉伯語圖像執行 OCR – 在 C# 中擷取文字
tags:
- OCR
- C#
- Image Processing
title: 如何對阿拉伯語圖像執行 OCR – 在 C# 中提取文字
url: /zh-hant/net/text-recognition/how-to-perform-ocr-on-arabic-images-extract-text-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在阿拉伯語圖像上執行 OCR – 在 C# 中提取文字  

有沒有想過 **如何在阿拉伯語圖像上執行 OCR** 而不抓狂？你並非唯一遇到這種情況的人——開發者在需要讀取右至左書寫的圖像文字時，常常卡住。  

在本教學中，你將看到一個完整、可執行的解決方案，能夠 **從 JPEG 中提取阿拉伯文字**，示範 **如何讀取圖像文字**，最後 **將圖像轉換為文字**，讓你在應用程式中使用。沒有模糊的說明，只有具體的程式碼與每行背後的原理。  

> **專業提示：** 若你正在處理掃描收據、街道招牌或歷史文件，以下步驟可為你節省數小時的反覆嘗試。  

## 你需要的條件  

- .NET 6 或更新版本（範例使用 console 應用程式）。  
- 支援阿拉伯語的 OCR 函式庫。示範中我們使用虛構的 `SimpleOcr` NuGet 套件，但此模式同樣適用於 Tesseract、IronOCR 或 Microsoft Computer Vision。  
- 一個名為 `arabic_sign.jpg` 的圖像檔案，放置於可參照的資料夾中（例如 `./Images/`）。  

就這樣。無需龐大的 SDK，無需雲端金鑰，只要幾行 C# 程式碼。  

![如何在阿拉伯招牌上執行 OCR](/images/arabic_sign.jpg)

*Image alt text: 如何在阿拉伯招牌上執行 OCR*  

## 如何在阿拉伯語圖像上執行 OCR  

以下我們將流程分為三個邏輯步驟。每個步驟說明我們 **做什麼**、**為何重要**，以及 **程式碼如何協同**。  

### 步驟 1：安裝並初始化 OCR 引擎  

First, add the OCR package to your project:

```bash
dotnet add package SimpleOcr
```

現在建立引擎的實例，並告訴它使用阿拉伯語語言模型。提前設定語言至關重要，否則引擎會將阿拉伯字元視為未知字形。

```csharp
using System;
using SimpleOcr;   // <-- fictional namespace for illustration

// Step 1: Create an OCR engine configured for Arabic
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Arabic   // Enables right‑to‑left processing
};
```

**為何這很重要：** 阿拉伯語使用不同的書寫方向，且字形會根據上下文變化。透過明確選擇 `OcrLanguage.Arabic`，引擎會套用正確的字形規則，顯著提升辨識準確度。  

### 步驟 2：載入 JPEG 並執行辨識  

接著我們將圖像送入引擎。`RecognizeImage` 方法會回傳一個 `OcrResult` 物件，內含原始文字、信心分數，以及可選的邊界框。

```csharp
// Step 2: Recognize text from the input image
string imagePath = @"./Images/arabic_sign.jpg";

OcrResult ocrResult;
try
{
    ocrResult = ocrEngine.RecognizeImage(imagePath);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to process '{imagePath}': {ex.Message}");
    return;
}
```

**邊緣情況說明：** 若找不到檔案或格式不受支援，`catch` 區塊會提供明確的錯誤訊息，而非靜默崩潰。這在批次作業中 **從 JPG 提取文字** 時特別有用。  

### 步驟 3：提取文字並使用  

最後，我們從 `ocrResult` 中取得辨識出的字串並顯示。你也可以將它寫入檔案、透過 API 傳送，或輸入至後續的 NLP 流程。

```csharp
// Step 3: Display the extracted Arabic text
Console.WriteLine("=== Extracted Arabic Text ===");
Console.WriteLine(ocrResult.Text);

// Optional: Save to a .txt file for later processing
System.IO.File.WriteAllText("./output/extracted_text.txt", ocrResult.Text);
```

**Expected output:**  
If `arabic_sign.jpg` contains the phrase “مكتبة المدينة” (City Library), the console will print something like:

```
=== Extracted Arabic Text ===
مكتبة المدينة
```

結果可能包含多餘的空白；如有需要，可使用 `String.Trim()` 或正規表達式進行清理。  

## 常見變化與技巧  

### 從不同格式讀取圖像文字  

相同程式碼可用於 PNG、BMP，甚至 PDF 頁面（若函式庫支援）。只要在 `imagePath` 中更改檔案副檔名即可。記得保留 **主要關鍵字**：每次切換格式仍然是 *如何在新來源執行 OCR*。  

### 提升 **提取阿拉伯文字** 的準確度  

- **預處理圖像**：提升對比、去除傾斜，或套用二值化閾值。  
- **設定較高 DPI**：許多 OCR 引擎需要至少 300 dpi 才能清晰辨識字元。  
- **使用語言套件**：部分函式庫允許載入自訂的阿拉伯語字典，以支援特定領域詞彙。  

### 處理大量批次（在迴圈中 **提取 JPG 文字**）  

If you have a folder full of JPEGs, wrap the recognition step in a `foreach` loop:

```csharp
foreach (var file in Directory.GetFiles("./Images", "*.jpg"))
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text}");
}
```

此模式讓你在大規模時 **將圖像轉換為文字**，而不必重寫程式碼。  

### 當引擎回傳空結果時  

- 確認圖像沒有過暗或模糊。  
- 檢查阿拉伯語語言模型是否正確載入（某些套件需要額外下載）。  
- 嘗試其他 OCR 供應商；例如 Tesseract 通常在低解析度圖像上表現較佳。  

## 完整、可直接執行的範例  

將下方程式碼片段複製到新的 console 專案（`dotnet new console -n ArabicOcrDemo`）中。它包含所有必要的 `using` 陳述式、錯誤處理，以及簡短的註解標頭。

```csharp
// ArabicOcrDemo.csproj
// <Project Sdk="Microsoft.NET.Sdk">
//   <PropertyGroup>
//     <OutputType>Exe</OutputType>
//     <TargetFramework>net6.0</TargetFramework>
//   </PropertyGroup>
//   <ItemGroup>
//     <PackageReference Include="SimpleOcr" Version="1.2.3" />
//   </ItemGroup>
// </Project>

using System;
using SimpleOcr;   // Replace with your actual OCR library namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine for Arabic
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Arabic
        };

        // 2️⃣ Path to the JPEG containing Arabic text
        string imagePath = @"./Images/arabic_sign.jpg";

        // 3️⃣ Run recognition with graceful error handling
        OcrResult result;
        try
        {
            result = ocrEngine.RecognizeImage(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
            return;
        }

        // 4️⃣ Output the extracted text
        Console.WriteLine("=== Extracted Arabic Text ===");
        Console.WriteLine(result.Text);

        // 5️⃣ Optional: persist the text for later use
        System.IO.Directory.CreateDirectory("./output");
        System.IO.File.WriteAllText("./output/extracted_text.txt", result.Text);
    }
}
```

Run it with:

```bash
dotnet run --project ArabicOcrDemo.csproj
```

執行後，你應該會在 console 中看到阿拉伯語句子，且已儲存於 `./output/extracted_text.txt`。  

## 結論  

現在你已了解 **如何在阿拉伯語圖像上執行 OCR**、如何 **提取阿拉伯文字**，以及如何從 JPEG **讀取圖像文字** 並 **將圖像轉換為文字**，在乾淨且可投入生產的 C# console 應用程式中。這三步流程——引擎設定、圖像辨識與結果處理——涵蓋了每個 OCR 任務的核心，無論語言或檔案類型為何。  

準備好迎接下一個挑戰了嗎？試著將語言切換為英文、輸入 PDF，或將輸出整合至翻譯 API。你也可以使用 `Parallel.ForEach` 並行處理 **提取 JPG 文字** 檔案，以應對大規模資料集。  

對於邊緣情況、效能調校或替代函式庫有任何疑問嗎？在下方留言——祝編程愉快！  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}