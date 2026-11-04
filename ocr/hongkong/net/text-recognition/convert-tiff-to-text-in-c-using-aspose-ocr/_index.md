---
category: general
date: 2026-03-05
description: 使用 Aspose OCR 在 C# 中快速將 TIFF 轉換為文字。了解如何在幾分鐘內顯示多頁 TIFF 檔案的 OCR 文字。
draft: false
keywords:
- convert tiff to text
- aspose ocr c#
- display ocr text
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中將 TIFF 轉換為文字。本指南逐步說明如何從多頁 TIFF 圖像顯示 OCR 文字。
og_title: 在 C# 中將 TIFF 轉換為文字 – 完整 Aspose OCR 指南
tags:
- Aspose
- OCR
- C#
- TIFF
title: 使用 Aspose OCR 在 C# 中將 TIFF 轉換為文字
url: /zh-hant/net/text-recognition/convert-tiff-to-text-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 在 C# 中將 TIFF 轉換為文字

需要在 C# 中 **將 TIFF 轉換為文字** 嗎？你並不孤單——許多開發者都在與從多頁 TIFF 檔案中提取可讀字串的問題奮鬥。好消息是 Aspose OCR C# 讓這項工作幾乎毫不費力，而且你可以在幾秒內 **在主控台顯示 OCR 文字** 或將其輸入其他系統。

在本教學中，我們將逐步說明一個完整、可直接執行的範例，展示如何載入多頁 TIFF、執行 OCR，並列印每頁的文字。沒有隱藏步驟，也沒有「參考文件」的捷徑。完成後，你將擁有一個可自行包含的程式，能直接放入任何 .NET 專案中。

## 需要的條件

- .NET 6.0 或更新版本（範例以 .NET 6 為目標，但 .NET 5 亦可使用）  
- 有效的 Aspose OCR 授權檔案 (`Aspose.OCR.lic`)。即使未使用授權，程式庫仍可運作，但會出現 20 秒的試用水印。  
- 你想要處理的多頁 TIFF 檔案（此處稱為 `multipage.tif`）。  
- Visual Studio 2022 或任何你偏好的編輯器——不需特殊工具。

如果你已滿足上述條件，讓我們開始吧。

## 步驟 1：安裝 Aspose OCR NuGet 套件

在執行任何程式碼之前，你必須先取得此函式庫。於專案資料夾中開啟終端機，執行以下指令：

```bash
dotnet add package Aspose.OCR
```

此單行指令會下載最新的穩定版（截至 2026 年 3 月為 23.9）。  
> **小技巧：** 請保持套件為最新版本；較新的發行版通常會針對大型 TIFF 進行效能優化。

## 步驟 2：設定 Aspose OCR C# 授權（可選但建議）

在未設定授權的情況下仍可執行 OCR 引擎，但輸出會加上試用警告。為避免此情況，請將引擎指向你的 `.lic` 檔案：

```csharp
using Aspose.OCR;

// ...

// Step 2: Apply your Aspose OCR license (optional but recommended)
var ocrEngine = new OcrEngine();
ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

即使跳過此步驟，程式仍可運作——只需留意結果中會出現額外的文字。

## 步驟 3：載入並辨識多頁 TIFF

現在我們真正 **將 TIFF 轉換為文字**。`ImageStream.FromFile` 輔助函式會將檔案讀取為引擎可理解的格式。之後呼叫 `Recognize()`，它會回傳一個 `OcrResult` 物件，內含每頁的文字。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 3: Load the multi‑page TIFF image to be processed
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\multipage.tif");

// Step 4: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize();
```

> **為何重要：** `Recognize()` 承擔了繁重的工作——像素分析、語言偵測與文字行重建——全部以原生 C# 程式碼執行。結果物件提供逐頁存取，對於之後 **顯示 OCR 文字** 十分理想。

## 步驟 4：遍歷頁面並 **顯示 OCR 文字**

取得結果後，我們只需遍歷各頁並列印。這就是實際看到從影像轉為純文字的過程。

```csharp
// Step 5: Iterate through each page of the result and display the recognized text
for (int pageIndex = 0; pageIndex < ocrResult.PageCount; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResult.GetPageText(pageIndex));
    Console.WriteLine(); // Blank line for readability
}
```

執行程式會產生類似以下的輸出（實際文字會依 TIFF 內容而異）：

```
--- Page 1 ---
Hello, world!
This is the first page of our multi‑page TIFF.

--- Page 2 ---
Second page starts here.
More sample text follows.
```

就這樣——你已成功 **將 TIFF 轉換為文字**，且 **顯示了每頁的 OCR 文字**。

## 完整範例程式

以下是完整程式碼，你可以直接貼到新的主控台專案 (`dotnet new console`) 中。它包含所有 using 指令、授權處理與錯誤檢查。

```csharp
// ConvertTiffToText.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ConvertTiffToText
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -----------------------------------------------------------------
            // Step 2: Apply your Aspose OCR license (optional but recommended)
            // -----------------------------------------------------------------
            try
            {
                ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
            }
            catch (Exception ex)
            {
                Console.WriteLine("License file not found or invalid. Running in trial mode.");
                Console.WriteLine($"Details: {ex.Message}");
            }

            // -----------------------------------------------------------------
            // Step 3: Load the multi‑page TIFF image to be processed
            // -----------------------------------------------------------------
            const string tiffPath = @"C:\Images\multipage.tif";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"Error: TIFF file not found at {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -----------------------------------------------------------------
            // Step 4: Perform OCR – this is where we convert TIFF to text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize();

            // -----------------------------------------------------------------
            // Step 5: Iterate through each page and display OCR text
            // -----------------------------------------------------------------
            Console.WriteLine($"Successfully processed {ocrResult.PageCount} page(s).");
            for (int i = 0; i < ocrResult.PageCount; i++)
            {
                Console.WriteLine($"--- Page {i + 1} ---");
                Console.WriteLine(ocrResult.GetPageText(i));
                Console.WriteLine(); // Add spacing between pages
            }

            // Keep the console window open when debugging
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**預期輸出**（為簡潔起見已截斷）如前所示。若看到試用水印，請再次確認授權路徑是否正確。

## 轉換 TIFF 為文字時的常見陷阱

| 問題 | 為何會發生 | 如何解決 |
|-------|----------------|------------|
| **大型 TIFF 記憶體不足** | 引擎會將整張影像載入記憶體。 | 使用 `ImageStream.FromFile(..., loadOnlyFirstPage: false)`，並分批處理頁面，或提升程式的記憶體上限。 |
| **雜訊字元** | 低解析度的來源影像會使 OCR 引擎困惑。 | 在送入 Aspose OCR 前先對 TIFF 進行前處理（例如將 DPI 提升至 300）。 |
| **授權未套用** | `SetLicense` 拋出例外但被忽略。 | 如範例所示，將呼叫包在 try/catch 中，並記錄錯誤。 |
| **缺少語言資料** | 預設情況下 OCR 假設使用英文。 | 在 `Recognize()` 前設定 `ocrEngine.Language = OcrLanguage.French;`（或任何支援的語言）。 |

處理這些邊緣情況可確保你的轉換在正式環境中順利執行。

## 往後的步驟：超越簡單顯示

既然你已能 **將 TIFF 轉換為文字** 且 **顯示 OCR 文字**，接下來可能想要：

- **將擷取的文字儲存**至 `.txt` 檔案或資料庫，以供日後分析。  
- **將多個 TIFF 合併**為單一可搜尋的 PDF，使用 Aspose.PDF。  
- **套用後處理**（拼寫檢查、正規表達式清理）以提升準確度。  

所有這些延伸功能皆建立在我們剛剛介紹的核心模式上。

---

### TL;DR

我們已完整示範一個使用 Aspose OCR C# **將 TIFF 轉換為文字** 的 C# 解決方案。程式碼會建立 `OcrEngine`，可選擇載入授權，讀取多頁 TIFF，執行 OCR，並逐頁 **顯示 OCR 文字**。有了這個完整範例，你可以將它放入任何 .NET 專案，即刻開始擷取文字。

對效能、語言支援或與其他 Aspose 產品整合有任何疑問嗎？歡迎在下方留言——祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}