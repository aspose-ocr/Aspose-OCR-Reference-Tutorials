---
category: general
date: 2026-01-09
description: 使用 Aspose OCR 在 C# 中從 TIFF 檔案提取文字。了解如何在本分步教學中取得每個結果的前 50 個字元。
draft: false
keywords:
- extract text from tiff
- get first 50 characters
- aspose ocr c# tutorial
language: zh-hant
og_description: 使用 Aspose OCR 於 C# 從 TIFF 提取文字。本指南逐步說明如何取得每個 OCR 結果的前 50 個字元。
og_title: 使用 Aspose OCR 從 TIFF 提取文字 – 完整 C# 指南
tags:
- Aspose OCR
- C#
- TIFF processing
title: 使用 Aspose OCR C# 從 TIFF 提取文字 – 完整教學
url: /zh-hant/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-c-full-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 TIFF 提取文字 – 完整 Aspose OCR C# 教程

是否曾經需要 **從 TIFF 提取文字** 圖片，但不確定該信任哪個函式庫？你並不孤單。許多開發者在嘗試從多頁 TIFF 中提取可搜尋文字時會卡住，尤其在性能很重要的情況下。

在本 **aspose ocr c# tutorial** 中，我們將示範一個即時可執行的範例，不僅能提取完整文字，還會示範如何 **取得每頁前 50 個字元** 以快速預覽。完成後，你將擁有一個可直接放入任何 .NET 專案的獨立程式。

## 需要的環境

- .NET 6（或任何較新的 .NET 版本）– 此程式碼可在 .NET Core 與 .NET Framework 上編譯。  
- 有效的 Aspose.OCR for .NET 授權（可先使用免費試用版）。  
- 包含一個或多個欲處理的 `.tif` 檔案的資料夾。  
- Visual Studio、VS Code 或任何你偏好的 IDE – 範例是純 C#，編輯器選擇不影響。

> **專業提示：** 若你在 CI 伺服器上，請將 Aspose.OCR NuGet 套件 (`Aspose.OCR`) 加入你的專案檔；此函式庫為完全受管理，且沒有原生相依性。

## 第一步：安裝 Aspose OCR NuGet 套件

首先，讓我們把 OCR 引擎加入專案。於解決方案資料夾開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

此指令會取得最新的穩定版（截至 2026 年 1 月為 23.9），並自動更新你的 `.csproj`。不需要手動處理 DLL。

## 第二步：初始化 OCR 引擎

現在我們建立 `OcrEngine` 的實例。可將其視為會讀取每一頁 TIFF 的「大腦」。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: tweak recognition settings if you know the language
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300; // higher DPI can improve accuracy
```

為什麼只實例化一次引擎？因為 `RecognizeImages` 能接受檔案路徑集合，讓引擎重複使用內部緩衝區，顯著加快批次處理速度。

## 第三步：一次性收集所有 TIFF 檔案

與其自行遍歷目錄，我們讓 .NET 處理繁重工作。`Directory.GetFiles` 方法會回傳 `IEnumerable<string>`，可直接傳入 OCR 呼叫。

```csharp
            // Step 3: Collect all TIFF images from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }
```

> **如果我的影像是 JPEG 或 PNG 呢？** 只需更改搜尋模式（`"*.jpg"` 或 `"*.*"`）。Aspose OCR 支援所有常見的點陣圖格式。

## 第四步：對整個集合執行 OCR

以下這行程式碼會一次處理所有檔案。此方法回傳一個字典，鍵為檔案路徑，值為包含辨識文字的 `OcrResult` 物件。

```csharp
            // Step 4: Perform OCR on the entire collection in one call
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);
```

為什麼要批次處理？它減少了重複載入 OCR 引擎的開銷，且在多核心機器上，Aspose 會在內部平行化工作，為你帶來顯著的速度提升。

## 第五步：顯示預覽 – 取得前 50 個字元

大多數 UI 情境只需要一小段文字，而非整份文件。我們將擷取前 50 個字元（若頁面較短則更少），並與檔名一起印出。

```csharp
            // Step 5: Display each file name with a preview of the recognized text
            foreach (var entry in ocrResults) // entry.Key = file path, entry.Value = OcrResult
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;
                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));

                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

`Math.Min(50, fullText.Length)` 這行確保不會超出字串範圍——一個小小的保護措施，可防止在 OCR 結果少於 50 個字元時拋出 `ArgumentOutOfRangeException`。

### 預期的 Console 輸出

假設你有兩個 TIFF 檔案（`invoice1.tif` 與 `receipt2.tif`），Console 可能會顯示：

```
invoice1.tif → Invoice Number: 2025-07-14 Date: 07/14/...
receipt2.tif → Store: QuickMart Total: $23.45 Date: ...
```

每行以省略號（`...`）結尾，表示預覽僅是較長文字區塊的開頭。

## 第六步：處理邊緣情況與常見陷阱

### 空檔或損毀檔案

如果檔案無法讀取，`RecognizeImages` 仍會回傳一個 `Text` 屬性為空的項目。你可以將其過濾掉：

```csharp
if (string.IsNullOrWhiteSpace(fullText))
{
    Console.WriteLine($"{fileName} → (No recognizable text)");
    continue;
}
```

### 大批次處理

處理數千個 TIFF 可能會佔用大量記憶體。此時可使用接受每張影像 `Stream` 的重載，或將清單分成較小的批次處理：

```csharp
var batches = imageFiles.Chunk(100); // .NET 6+ extension
foreach (var batch in batches)
{
    var batchResults = ocrEngine.RecognizeImages(batch);
    // handle batchResults...
}
```

### 語言與字型支援

若文件包含非拉丁字元，請在呼叫 `RecognizeImages` 前設定語言：

```csharp
ocrEngine.Language = Language.Spanish; // or Language.MultiLanguage
```

此小調整可大幅提升辨識準確度。

## 第七步：完整可執行範例（直接複製貼上）

以下是完整程式碼，你可以貼到新建的 console 專案（`dotnet new console`）中直接執行（只需將 `YOUR_DIRECTORY/Batch` 替換為實際路徑）。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: set language or DPI for better accuracy
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300;

            // Collect all TIFF files from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }

            // Perform OCR on the entire collection
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);

            // Show a preview – get first 50 characters of each result
            foreach (var entry in ocrResults)
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;

                if (string.IsNullOrWhiteSpace(fullText))
                {
                    Console.WriteLine($"{fileName} → (No recognizable text)");
                    continue;
                }

                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));
                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

使用 `dotnet run` 執行程式。你應該會看到每個 TIFF 檔案的簡短預覽，證明你已成功使用 Aspose OCR **從 TIFF 提取文字**。

## 常見問題 (FAQ)

**Q: 這能處理多頁 TIFF 嗎？**  
A: 可以。Aspose OCR 會在內部將每頁視為獨立影像，因此多頁 TIFF 會產生每個檔案一個合併的字串。之後如有需要可再分割。

**Q: OCR 的即時準確度如何？**  
A: 對於乾淨且高解析度（300 DPI 或以上）的掃描，英文文字的準確率可超過 95%。前處理（去斜、二值化）可進一步提升。

**Q: 我可以將結果輸出為 CSV 檔嗎？**  
A: 當然可以。將 `Console.WriteLine` 改成 `StreamWriter`，寫入 `fileName,preview` 行。記得對預覽文字中的逗號進行跳脫。

## 後續步驟與相關主題

- **持久化 OCR 結果** – 將完整文字存入資料庫，以供可搜尋的檔案庫使用。  
- **結合 PDF 轉換** – 使用 Aspose.PDF 將提取的文字嵌入可搜尋的 PDF。  
- **在 Azure Functions 上批次處理** – 無需自行管理伺服器即可擴展 OCR 工作。

所有這些延伸皆圍繞著高效 **從 TIFF 提取文字** 的核心概念，同時仍能讓你 **取得前 50 個字元** 以供 UI 快速預覽。

---

*祝程式開發順利！若遇到任何問題，歡迎在下方留言，我會盡力協助你微調 OCR 流程。*

![Extract text from TIFF using Aspose OCR](https://example.com/images/extract-text-from-tiff.png "Extract text from TIFF using Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}