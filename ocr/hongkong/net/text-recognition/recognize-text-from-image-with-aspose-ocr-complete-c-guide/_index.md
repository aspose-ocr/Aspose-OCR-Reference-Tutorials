---
category: general
date: 2026-02-22
description: 使用 Aspose OCR 於 C# 進行圖像文字辨識。了解如何載入 TIFF 圖像、建立 OCR 引擎，並高效地從圖像中擷取文字。
draft: false
keywords:
- recognize text from image
- load tiff image
- extract text from image
- create OCR engine
language: zh-hant
og_description: 逐步識別圖像中的文字。學習如何載入 TIFF 圖像、建立 OCR 引擎，並使用 Aspose OCR 於 C# 中提取圖像文字。
og_title: 從圖片辨識文字 – 完整 C# Aspose OCR 教學
tags:
- C#
- Aspose OCR
- Image Processing
title: 使用 Aspose OCR 從圖像識別文字 – 完整 C# 指南
url: /zh-hant/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

ensure we didn't translate any code placeholders or shortcodes. Also preserve markdown formatting like **bold**, lists.

Check for any markdown links: none.

Check for any images: none.

All good.

Now produce final content with translations.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像辨識文字 – 完整 C# Aspose OCR 教程

有沒有曾經需要**從圖像辨識文字**，卻在第一行程式碼就卡住了？你並不孤單。在許多專案——發票掃描、檔案數位化，或建立可搜尋的 PDF 資料庫——從圖片中取得乾淨的文字是第一道關卡。  

好消息：使用 Aspose OCR，你可以載入 TIFF 圖片，啟動 OCR 引擎，並在短短幾行程式碼內**從圖像擷取文字**。本教學將逐步說明整個流程，從載入高解析度 TIFF 檔案到列印辨識出的文字與處理時間。  

我們也會討論幾個「如果…」情境，例如停用 GPU 加速或處理多頁 TIFF，讓你在面對實際資料時不會感到意外。完成後，你將擁有一個可直接執行的主控台應用程式，能可靠地**從圖像辨識文字**。

## 前置條件

- .NET 6.0 SDK 或更新版本（此程式碼同樣支援 .NET Core 與 .NET Framework）
- Aspose.OCR NuGet 套件（`dotnet add package Aspose.OCR`）
- 你想處理的 TIFF 檔案（範例使用 `high_res_page.tif`）
- 任意你喜歡的 IDE——Visual Studio、Rider 或 VS Code 都可使用

不需要額外的原生函式庫；Aspose 內部已處理所有事務，包括可選的 GPU 支援。

## 步驟 1：載入 TIFF 圖片

首先需要將圖像資料載入記憶體。Aspose 提供的靜態 `Image.Load` 方法可支援大多數常見格式，亦包括 TIFF。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Load the TIFF file – replace the path with your own image location
var inputImage = Image.Load(@"YOUR_DIRECTORY/high_res_page.tif");
```

**為何重要：** TIFF 檔案常包含多頁或高解析度資料，其他函式庫可能無法處理。Aspose 的載入器能正確讀取檔案並保留像素深度，這對後續的精確 OCR 至關重要。  

*小技巧：* 若處理多頁 TIFF，可遍歷 `inputImage.Frames`，逐一處理每個畫格。如此即可避免遺漏後續頁面隱藏的文字。

## 步驟 2：建立 OCR 引擎

圖像已載入記憶體後，需要一個能辨識字元的引擎。`OcrEngine` 類別用於設定語言、GPU 使用與其他選項。

```csharp
// Initialize the OCR engine with desired settings
var ocrEngine = new OcrEngine
{
    // Enable GPU acceleration for faster processing (optional, requires compatible hardware)
    UseGpu = true,
    // Set the language to English – you can change this to Language.French, etc.
    Language = Language.English
};
```

**為何重要：** 啟用 GPU（`UseGpu = true`）可在支援的機器上大幅縮短處理時間，但若在 CI 伺服器或低階筆記型電腦上執行，關閉亦完全安全。此外，選擇正確的語言能提升字元辨識，因為引擎會載入特定語言的字典。  

*注意：* 若忘記設定 `Language`，引擎預設為英文，對非拉丁文字可能產生奇怪的結果。

## 步驟 3：從圖像辨識文字

引擎就緒後，實際的 OCR 呼叫只需一個方法：`Recognize`。它會回傳一個 `OcrResult` 物件，內含擷取的文字與效能指標。

```csharp
// Perform OCR on the loaded image
var ocrResult = ocrEngine.Recognize(inputImage);
```

`OcrResult` 提供兩個方便的屬性：

- `Text` – 引擎能讀取的所有內容的純文字表示。
- `ProcessingTime` – OCR 所耗費的時間，以毫秒為單位。

## 步驟 4：檢視結果

最後，將結果輸出。實際應用中可能會將文字寫入資料庫，但示範目的只需在主控台印出即可。

```csharp
// Show how long the OCR took and the recognized text
Console.WriteLine($"Recognized in {ocrResult.ProcessingTime} ms");
Console.WriteLine("=== Extracted Text Start ===");
Console.WriteLine(ocrResult.Text);
Console.WriteLine("=== Extracted Text End ===");
```

**預期輸出**（當然你的文字會不同）：

```
Recognized in 842 ms
=== Extracted Text Start ===
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
...
=== Extracted Text End ===
```

若輸出呈現亂碼，請再次確認圖像是否清晰且已選擇正確語言。也可以調整 `ocrEngine` 的屬性，例如 `PreprocessOptions` 以減少雜訊。

## 處理邊緣情況

### 1. 沒有 GPU？沒問題。

```csharp
ocrEngine.UseGpu = false; // fallback to CPU‑only processing
```

CPU 處理較慢（通常慢 2‑3 倍），但可在所有 Windows、Linux 或 macOS 機器上執行。

### 2. 多頁 TIFF

```csharp
foreach (var frame in inputImage.Frames)
{
    var pageResult = ocrEngine.Recognize(frame);
    Console.WriteLine(pageResult.Text);
}
```

每個畫格皆視為獨立圖像，因而會為每頁產生一段文字。

### 3. 不同語言

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, Language.German, etc.
```

切換語言會載入相應的字元集與字典，顯著提升非英文文件的辨識準確度。

## 完整範例程式

以下是完整程式碼，可直接複製貼上至新的主控台專案（`dotnet new console`）。它包含了前述所有部份，並加入了幾項安全檢查。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the TIFF image you want to process
        // -------------------------------------------------
        const string imagePath = @"YOUR_DIRECTORY/high_res_page.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"Error: File not found at {imagePath}");
            return;
        }

        var inputImage = Image.Load(imagePath);

        // -------------------------------------------------
        // Step 2: Create and configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,                 // optional – set to false if GPU not available
            Language = Language.English    // change if you need another language
        };

        // -------------------------------------------------
        // Step 3: Perform OCR on the loaded image
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 4: Display processing time and extracted text
        // -------------------------------------------------
        Console.WriteLine($"Recognized in {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text Start ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("=== Extracted Text End ===");

        // Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

儲存檔案後，執行 `dotnet run`，即可在主控台看到辨識出的文字。就這樣——你的**從圖像辨識文字**流程已經啟動並運作。

## 常見問題

**Q: 這能支援 PNG 或 JPEG 嗎？**  
A: 當然可以。`Image.Load` 會自動偵測格式，所以你可以將 `.tif` 副檔名改為 `.png`、`.jpg`，甚至 `.bmp`。OCR 引擎會以相同方式處理。

**Q: 我的輸出有很多雜亂的符號。**  
A: 嘗試啟用前處理：`ocrEngine.PreprocessOptions = new PreprocessOptions { RemoveNoise = true, Deskew = true };`。此設定會在辨識前清理圖像。

**Q: 我可以取得每個單字的邊界框嗎？**  
A: 可以。`ocrResult.Regions` 包含帶座標的 `OcrRegion` 物件。若需在 UI 中標示單字，可遍歷這些物件。

## 結論

我們剛剛示範了如何在 C# 中使用 Aspose OCR **從圖像辨識文字**。從載入 TIFF 檔案、**建立 OCR 引擎**、執行辨識，到最後顯示結果——每個步驟都簡潔、說明完整，且可直接複製到你的專案中。  

接下來你可以探索批次處理資料夾、將結果儲存於可搜尋的索引，或結合 OCR 與翻譯 API。無論選擇何種方式，核心流程皆相同：載入圖像、設定引擎、辨識，並處理輸出。  

對於載入 TIFF 圖片、從圖像擷取文字，或調整 OCR 引擎還有其他問題嗎？歡迎在下方留言，祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}