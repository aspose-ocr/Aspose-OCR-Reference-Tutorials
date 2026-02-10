---
category: general
date: 2026-02-09
description: 使用 C# 離線 OCR 從圖像提取文字。完整的 C# OCR 範例示範如何載入圖像進行 OCR、辨識西里爾文字以及從護照中提取文字。
draft: false
keywords:
- extract text from image
- c# ocr example
- load image for ocr
- recognize cyrillic text
- recognize text from passport
language: zh-hant
og_description: 使用 C# 離線 OCR 從圖像中提取文字。學習一步一步的 C# OCR 範例，載入圖像進行 OCR，辨識西里爾文字，並從護照中提取文字。
og_title: 在 C# 中從圖片提取文字 – 離線 OCR 指南
tags:
- OCR
- C#
- Aspose
title: 在 C# 中從圖像提取文字 – 離線 OCR 範例
url: /zh-hant/net/text-recognition/extract-text-from-image-in-c-offline-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字（C#） – 離線 OCR 範例

是否曾需要 **從圖像中提取文字**，卻被依賴網路的 API 卡住？你並不孤單。許多開發者在 OCR 服務嘗試於執行時下載語言包時會碰壁，尤其在受限環境中。

本指南將逐步說明一個完整離線執行的 **c# ocr example**，載入圖像進行 OCR，並辨識護照上的西里爾文字。完成後，你將擁有一個可直接執行的程式，將任何支援圖像的純文字內容直接輸出至主控台。

## 你將學到什麼

- 如何設定 Aspose.OCR 以進行離線處理。  
- 從磁碟 **load image for OCR** 的完整程式碼。  
- 如何設定引擎以 **recognize cyrillic text**。  
- 一個完整、可直接複製貼上的 **c# ocr example**，可從護照樣式的照片中提取文字。  

不需要任何 Aspose 的先前經驗；只要有 .NET 6（或更新）SDK 以及 Visual Studio 2022（或 VS Code）即可。

![使用 Aspose OCR 在護照照片上提取文字](/images/ocr-passport.jpg "從圖像中提取文字")

## 步驟 1：設定專案以提取圖像文字

在撰寫任何程式碼之前，請確保已將 Aspose.OCR NuGet 套件加入專案中：

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** 使用 `--version` 參數鎖定最新的穩定版本（例如 `13.9.0`）。這可確保與 .NET 6 的相容性。

建立新的主控台應用程式非常簡單：

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
```

現在你有一個乾淨的起點，我們將 **extract text from image**，且完全不需要連網。

## 步驟 2：載入圖像以進行 OCR – 讀取護照照片

OCR 引擎首先需要一個代表圖片的 bitmap 或串流。在本範例中，我們將 **load image for OCR** 從本機檔案 `cyrillic_passport.jpg` 讀取。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 2: Load the image file (this is the “load image for ocr” part)
var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

// Validate the file exists – helpful when the path is wrong.
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// ImageStream abstracts the underlying format; it works with JPEG, PNG, etc.
var image = ImageStream.FromFile(imagePath);
```

> **Why this matters:** 提供串流而非原始的 `Bitmap`，可讓 Aspose 內部自行偵測格式，減少樣板程式碼與潛在錯誤。

## 步驟 3：設定離線模式並選擇西里爾語言

Aspose.OCR 能即時下載語言模型，但這會違背離線解決方案的初衷。請關閉網路呼叫，並明確告訴引擎使用哪種語言。

```csharp
// Step 3: Create the OCR engine and switch to offline mode
var ocrEngine = new OcrEngine
{
    Configuration =
    {
        OfflineMode = true,               // No network traffic – perfect for secure environments
        Language = new[] { OcrLanguage.Cyrillic } // We want to **recognize cyrillic text**
    }
};
```

> **Edge case:** 若之後需要在同一文件中辨識拉丁字元，只需將 `OcrLanguage.English` 加入陣列。引擎會自動處理多語言偵測。

## 步驟 4：執行 OCR 引擎並辨識西里爾文字

現在我們真正 **recognize text from passport**‑樣式的圖像。`Recognize` 方法會回傳一個豐富的結果物件，包含純文字、信心分數與邊界框。

```csharp
// Step 4: Perform the OCR operation
OcrResult result = ocrEngine.Recognize(image);

// Step 5: Output the plain text – this is where we finally **extract text from image**
Console.WriteLine("📝 Extracted Text:");
Console.WriteLine("-------------------");
Console.WriteLine(result.PlainText);
```

### 預期的主控台輸出

```
📝 Extracted Text:
-------------------
ПАСПОРТ РФ
Иванов Иван Иванович
01.01.1990
...
```

如果結果出現亂碼，請再次確認來源圖像是否清晰，以及 Aspose 安裝資料夾中（通常為 `\\Aspose.OCR\\resources\\languages`）是否已存在 `OfflineMode` 的西里爾語言包。

## 完整 C# OCR 範例 – 完整原始碼

以下是完整的 **c# ocr example**。將其複製貼上至 `Program.cs`，然後執行 `dotnet run`。所有 **extract text from image** 所需的內容都在此。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class OfflineExample
{
    static void Main()
    {
        // --------------------------------------------------------------
        // Step 1: Create the OCR engine (offline mode)
        // --------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Configuration =
            {
                OfflineMode = true,                     // No network calls
                Language = new[] { OcrLanguage.Cyrillic } // Recognize Cyrillic text
            }
        };

        // --------------------------------------------------------------
        // Step 2: Load the image for OCR (passport photo)
        // --------------------------------------------------------------
        var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ Image not found at {imagePath}");
            return;
        }

        var image = ImageStream.FromFile(imagePath);

        // --------------------------------------------------------------
        // Step 3: Recognize the text
        // --------------------------------------------------------------
        var result = ocrEngine.Recognize(image);

        // --------------------------------------------------------------
        // Step 4: Output the plain text (the final extraction)
        // --------------------------------------------------------------
        Console.WriteLine("📝 Extracted Text:");
        Console.WriteLine("-------------------");
        Console.WriteLine(result.PlainText);
    }
}
```

### 執行範例

```bash
dotnet run
```

你應該會在主控台看到以西里爾文字顯示的護照資訊。這就代表你的 **extract text from image** 流程已正常運作。

## 常見問題與解決方法

| 症狀 | 可能原因 | 解決方式 |
|------|----------|----------|
| 空的 `PlainText` | 語言模型錯誤或圖像過暗 | 確認 `OfflineMode` 包含 `Cyrillic` 語言，並提升圖像對比度 |
| `System.DllNotFoundException` | 缺少原生 Aspose OCR 二進位檔 | 重新安裝 NuGet 套件或將 `Aspose.OCR.Native.dll` 複製至輸出資料夾 |
| 大圖像處理速度慢 | 引擎處理完整解析度 | 在傳入 `ImageStream` 前將圖像縮小至寬度 ≤ 1500 px |
| 文字亂碼 | 圖像旋轉方向不正確 | 在建立串流前使用 `Image.RotateFlip(RotateFlipType.Rotate90FlipNone)` |

## 往後步驟 – 擴充離線 OCR 工作流程

- 在 ASP.NET Core 處理上傳檔案時，從 `MemoryStream` **Load image for OCR**。  
- 透過迴圈處理護照掃描資料夾，以批次模式 **recognize text from passport**。  
- 將結果與 **regular expressions** 結合，抽取護照號碼或出生日期等欄位。  
- 嘗試設定 `ocrEngine.Configuration.UseParallelProcessing = true` 以利用多核心加速。

### 結論

我們剛剛示範了如何使用完全離線的 C# OCR 流程 **extract text from image**。這個簡短且自包含的 **c# ocr example** 會載入圖像、設定引擎以 **recognize cyrillic text**，並將擷取的護照資料印出——全程不需任何網路請求。

歡迎自行調整程式碼、加入更多語言，或將輸出寫入資料庫。只要掌握了載入圖像以進行 OCR 以及辨識護照樣式照片文字的基礎，便可無限發揮。

有任何問題或想分享自己的調整嗎？歡迎在下方留言，祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}