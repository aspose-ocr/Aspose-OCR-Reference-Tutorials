---
category: general
date: 2026-01-09
description: 使用 Aspose OCR 快速從 PNG 提取文字。了解如何讀取影像文字、提升 OCR 準確度，並在 C# 中獲得乾淨的結果。
draft: false
keywords:
- extract text from png
- read image text
- improve ocr accuracy
- extract text from image
- aspose ocr tutorial
language: zh-hant
og_description: 使用 Aspose OCR 快速從 PNG 提取文字。了解如何讀取圖像文字、提升 OCR 準確度，並在 C# 中獲得乾淨的結果。
og_title: 從 PNG 提取文字 – 完整 Aspose OCR 教程
tags:
- Aspose OCR
- C#
- Image Processing
title: 從 PNG 提取文字 – 完整 Aspose OCR 教程
url: /zh-hant/net/text-recognition/extract-text-from-png-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 PNG 提取文字 – 完整 Aspose OCR 教學

有沒有曾經需要**從 PNG 提取文字**，卻發現結果充斥著亂碼？你並不孤單。在許多實務專案中——發票、收據或掃描表格——OCR 輸出的品質可能決定自動化流程的成敗。

在本指南中，我們將示範一個**逐步**使用 Aspose OCR 讀取影像文字的方法，加入自訂字典以**提升 OCR 準確度**，清除雜訊，最後輸出整潔的字串。完成後，你將擁有一個可直接執行的 C# 主控台應用程式，可靠地從 PNG 圖片中提取文字。

> **你將學到**  
> * 完整、可執行的程式碼範例。  
> * 為何自訂字典重要的概念。  
> * 處理低對比掃描等邊緣案例的技巧。

## 前置條件

- .NET 6 SDK 或更新版本（程式碼目標為 .NET 6，但 .NET 5 亦可運作）。  
- Visual Studio 2022 或你偏好的任何編輯器。  
- 你想處理的 **PNG** 圖片，例如 `invoice.png`。  
- **Aspose.OCR** NuGet 套件（`dotnet add package Aspose.OCR`）。

不需要額外的設定檔；所有程式碼皆在單一 `.cs` 檔案中。

## 步驟 1 – 安裝並參考 Aspose OCR

首先，將函式庫加入你的專案。於解決方案資料夾開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

這一行指令會取得最新的穩定版（截至 2026 年 1 月，版本 23.9）。此套件包含我們在整個教學中會使用的 `OcrEngine` 類別。

## 步驟 2 – 初始化 OCR 引擎

建立 `OcrEngine` 實例是基礎。可將其想像為開啟一台準備解讀像素的掃描器。

```csharp
using Aspose.OCR;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **專業提示：** 若你打算在迴圈中處理大量影像，請重複使用同一個 `OcrEngine` 實例。它會快取內部資源，提升後續呼叫的速度。

## 步驟 3 – 使用自訂字典提升準確度

即時可用的 OCR 已相當不錯，但在面對領域專屬詞彙如 “Aspose”、 “OCR” 或 “SDK” 時仍可能出錯。將這些詞彙加入**自訂字典**，即可告訴引擎這些字串是有效的，減少辨識錯誤。

```csharp
// Define domain‑specific terms that the engine should recognize
ocrEngine.CustomDictionary = new HashSet<string>
{
    "Aspose",
    "OCR",
    "SDK",
    "invoice"
};
```

### 為何自訂字典有幫助

- OCR 背後的**統計模型**會高度權衡常見語言模式。不常見的詞彙機率低，可能被相似外觀的字元取代。  
- 透過明確列出這些詞彙，你可以覆寫模型的猜測。  
- 這對於包含產品代碼、縮寫或品牌名稱的**讀取影像文字**特別有用。

## 步驟 4 – 從 PNG 檔案辨識文字

現在我們將影像路徑傳入引擎。`RecognizeImage` 方法會回傳原始字串，仍可能包含引擎無法對應的未知符號（例如 “#@!”）。

```csharp
// Path to the PNG you want to process
string imagePath = @"YOUR_DIRECTORY/invoice.png";

// Perform OCR
string rawText = ocrEngine.RecognizeImage(imagePath);
```

> **邊緣情況：** 若檔案未找到，`RecognizeImage` 會拋出 `FileNotFoundException`。在正式環境的程式碼中，請將呼叫包在 try‑catch 區塊內。

## 步驟 5 – 使用 `CleanText` 清理結果

Aspose OCR 內建一個協助工具，可剔除被標記為「未知」的字元。此步驟對於**從影像提取文字**的專案至關重要，因為後續的解析器只接受英數字與基本標點符號。

```csharp
// Remove unknown tokens and extra whitespace
string cleanedText = ocrEngine.CleanText(rawText);
```

`CleanText` 方法同時會正規化換行字元，確保輸出可安全存入資料庫或傳遞給其他服務。

## 步驟 6 – 輸出已清理的文字

最後，顯示或儲存結果。在主控台應用程式中，`Console.WriteLine` 即可完成。

```csharp
Console.WriteLine("=== Cleaned OCR Output ===");
Console.WriteLine(cleanedText);
```

執行程式後，你應該會看到一段整潔的文字，與 `invoice.png` 的內容相符。若影像中包含 “Aspose” 這個詞，自訂字典會確保它正確顯示，而不是變成類似 “A5p0se” 的錯誤。

## 完整範例程式

將所有步驟整合起來，以下是完整的 `Program.cs`，你可以直接複製貼上到新的主控台專案中：

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add domain‑specific terms to improve OCR accuracy
        ocrEngine.CustomDictionary = new HashSet<string>
        {
            "Aspose",
            "OCR",
            "SDK",
            "invoice"
        };

        // 3️⃣ Path to your PNG file (adjust as needed)
        string imagePath = @"YOUR_DIRECTORY/invoice.png";

        try
        {
            // 4️⃣ Recognize raw text from the image
            string rawText = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Clean up unknown tokens
            string cleanedText = ocrEngine.CleanText(rawText);

            // 6️⃣ Show the result
            Console.WriteLine("=== Cleaned OCR Output ===");
            Console.WriteLine(cleanedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

**預期輸出**（假設 PNG 為簡易發票內容）：

```
=== Cleaned OCR Output ===
Invoice #12345
Date: 01/08/2026
Total: $1,250.00
Thank you for your business!
```

若看到雜散符號，請再次檢查影像品質，或在自訂字典中加入更多詞彙。

## 加分項：處理低品質掃描

有時 PNG 以 72 dpi 掃描或有嚴重壓縮雜訊。以下提供幾個快速技巧，能在不離開 C# 的情況下**提升 OCR 準確度**：

1. 使用如 `SixLabors.ImageSharp` 的函式庫**前處理影像**——提升對比、轉為灰階，或稍微模糊以降低雜訊。  
2. 在 `OcrEngine` 上**設定 `Resolution` 屬性**（例如 `ocrEngine.Resolution = 300;`），告訴引擎將影像視為較高解析度。  
3. 若處理非英文文字，**啟用語言套件**（`ocrEngine.Language = Language.English;`）。

上述三種做法皆可在 `RecognizeImage` 呼叫之前加入。

## 常見問題

- **這能用於其他影像格式嗎？**  
  可以。`RecognizeImage` 支援 JPEG、BMP、TIFF，甚至 PDF（作為影像容器）。步驟相同。

- **我可以一次從資料夾內的多個 PNG 提取文字嗎？**  
  當然可以。將核心邏輯包在 `foreach (var file in Directory.GetFiles(folder, "*.png"))` 迴圈中，並將每個結果存入清單或寫入個別檔案。

- **如果需要文字座標怎麼辦？**  
  Aspose OCR 也提供包含邊界框的 `OcrResult` 物件。可使用 `ocrEngine.RecognizeImageToResult(imagePath)` 取得進階資訊。

## 結論

我們已完整示範一個**端對端**的解決方案，使用 Aspose OCR **從 PNG 檔案提取文字**。透過初始化引擎、加入**自訂字典**、清理原始輸出，並處理一些常見的陷阱，你即可在自己的 C# 應用程式中可靠地**讀取影像文字**，並**提升 OCR 準確度**。

準備好下一步了嗎？試著將 PNG 換成掃描收據、在字典中加入更多領域專屬詞彙，或將輸出整合至資料庫以實現自動化發票處理。結合 Aspose OCR 與 .NET 豐富的生態系統，無所不能。

祝程式開發順利，願你的 OCR 永遠精準！ 

![從 png 提取文字範例](/images/extract-text-from-png.png "從 png 提取文字 – Aspose OCR 示範")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}