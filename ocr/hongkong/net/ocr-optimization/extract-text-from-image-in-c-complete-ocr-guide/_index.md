---
category: general
date: 2026-02-11
description: 使用 Aspose OCR 在 C# 中從圖像提取文字。了解如何載入圖像進行 OCR、提升 OCR 準確度，並透過拼寫檢查修正 OCR 錯誤。
draft: false
keywords:
- extract text from image
- image to text c#
- improve ocr accuracy
- load image for ocr
- fix ocr errors
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中從圖像提取文字。本指南展示如何載入圖像進行 OCR、提升 OCR 準確度以及修正 OCR 錯誤。
og_title: 在 C# 中從圖像提取文字 – 完整 OCR 指南
tags:
- C#
- OCR
- Aspose
- Text Extraction
title: 在 C# 中從圖像提取文字 – 完整 OCR 指南
url: /zh-hant/net/ocr-optimization/extract-text-from-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字（C#）– 完整 OCR 指南

曾經需要 **extract text from image** 但結果看起來像亂碼嗎？你並不是唯一一個。 在許多實際應用中——想像收據掃描、筆記數位化或舊文件遷移——從圖片中取得乾淨的文字是第一步，且往往是最難的關卡。

幸運的是，使用 Aspose OCR，你可以 **load image for OCR**、執行拼寫檢查，並得到整潔、可搜尋的文字。在本教學中，我們將逐步說明完整流程，從讀取 JPEG 到優化輸出，並讓你看到如何 **improve OCR accuracy**。

> **你將會得到：** 一個可直接執行的 C# 主控台程式，能夠 **extract text from image**，校正常見的 OCR 錯誤，並同時印出原始與清理後的結果。

---

## 需要的環境

- .NET 6 或更新版本（此程式碼亦可在 .NET Framework 4.7+ 上執行）
- Visual Studio 2022（或任何你喜歡的 IDE）
- 免費的 Aspose OCR 試用金鑰或正式授權版
- 包含手寫或印刷文字的圖像檔（例如 `typed_note.jpg`）

不需要其他第三方函式庫——Aspose 會自動處理語言模型與拼寫檢查。

## 第一步 – 安裝 Aspose OCR NuGet 套件

在我們能夠 **extract text from image** 之前，必須先在機器上安裝 OCR 引擎。

```powershell
# From the Package Manager Console
Install-Package Aspose.OCR
```

或者，如果你偏好使用 CLI：

```bash
dotnet add package Aspose.OCR
```

此套件已包含語言資料，但設定 `AutomaticResourceDownload = true`（稍後會這樣做）可確保在執行時自動下載任何缺少的字典。

## 第二步 – 載入圖像以進行 OCR

引擎首先需要的是位圖。你可以提供任何 `System.Drawing.Image` 支援的格式，如 PNG、JPEG、BMP 或 TIFF。

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Path to your source picture – change this to your own folder
string imagePath = @"C:\MyImages\typed_note.jpg";

// Load the image inside a using block so the file handle is released promptly
using (Image image = Image.FromFile(imagePath))
{
    // The rest of the OCR pipeline lives inside this block
}
```

> **為什麼要使用 `using` 區塊？** 它會自動釋放 `Image` 物件，避免因忘記釋放資源而導致的檔案鎖定問題。

## 第三步 – 執行 OCR – 「Image to Text C#」實作

現在我們真正開始 **extract text from image**。`OcrEngine` 類別負責主要的運算。

```csharp
// Step 3: Initialise the OCR engine
var ocrEngine = new OcrEngine
{
    AutomaticResourceDownload = true, // pulls language packs if missing
    Language = OcrLanguage.English    // set to your document's language
};

// Inside the using block from Step 2
var ocrResult = ocrEngine.Recognize(image);
string rawText = ocrResult.Text;
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

此時你已取得一個字串，與引擎在圖片中看到的內容相同。實際上，輸出可能會包含雜散字元、辨識錯誤的單詞，或換行異常——因此需要下一步處理。

## 第四步 – 使用拼寫檢查提升 OCR 準確度

Aspose 內建專用的 `SpellChecker`，能辨識你所處理的語言。對原始字串執行它通常能修正最明顯的錯誤。

```csharp
// Step 4: Initialise spell‑check (resources are auto‑downloaded)
var spellChecker = new SpellChecker(OcrLanguage.English);

// Correct the OCR output
string correctedText = spellChecker.Correct(rawText);
Console.WriteLine("\nCorrected OCR output:");
Console.WriteLine(correctedText);
```

> **專業提示：** 若你處理領域特定的詞彙（例如醫學術語），可以透過 `SpellChecker` 的多載方法提供自訂字典。

## 第五步 – 手動修正 OCR 錯誤（可選）

即使是最好的拼寫檢查器也可能漏掉與語境相關的錯誤。快速的後處理步驟可以捕捉到例如「l」與「1」或「O」與「0」之類的問題。

```csharp
// Simple regex to replace common OCR confusions
string finalText = System.Text.RegularExpressions.Regex.Replace(
    correctedText,
    @"\b([lI])\b", // isolated l or I
    "1");

// Additional custom rules can be added here
Console.WriteLine("\nFinal cleaned text:");
Console.WriteLine(finalText);
```

歡迎自行擴充此部分的啟發式規則——例如商品代碼的查詢表或已知縮寫清單。

## 完整範例程式

以下是完整程式碼，你可以直接複製貼上到新的 Console App 專案中。它包含了所有前述步驟，並附有說明註解。

```csharp
// ------------------------------------------------------------
// Extract Text from Image in C# – Full Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR engine – automatic download ensures language data is present
        var ocrEngine = new OcrEngine
        {
            AutomaticResourceDownload = true,
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to analyse
        string imagePath = @"C:\MyImages\typed_note.jpg";
        using (Image image = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR – this is where we *extract text from image*
            var ocrResult = ocrEngine.Recognize(image);
            string rawText = ocrResult.Text;
            Console.WriteLine("Before (raw OCR):");
            Console.WriteLine(rawText);
            Console.WriteLine(new string('-', 40));

            // 4️⃣ Spell‑check to *improve OCR accuracy*
            var spellChecker = new SpellChecker(OcrLanguage.English);
            string correctedText = spellChecker.Correct(rawText);
            Console.WriteLine("After (spell‑checked):");
            Console.WriteLine(correctedText);
            Console.WriteLine(new string('-', 40));

            // 5️⃣ Optional custom clean‑up – *fix OCR errors* that the spell‑checker missed
            string finalText = Regex.Replace(correctedText,
                @"\b([lI])\b", // replace isolated 'l' or 'I' with '1'
                "1");

            Console.WriteLine("Final (post‑processed):");
            Console.WriteLine(finalText);
        }
    }
}
```

### 預期輸出

假設 `typed_note.jpg` 內的文字為「Hello world, this is a test 123」，主控台將會顯示類似以下內容：

```
Before (raw OCR):
H3llo w0rld, th1s is a test 123

After (spell‑checked):
Hello world, this is a test 123

Final (post‑processed):
Hello world, this is a test 123
```

請注意，拼寫檢查器將「H3llo」修正為「Hello」，而正規表達式則清除出現在「th1s」中的多餘「1」。

## 常見問題與特殊情況

| 問題 | 答案 |
|----------|--------|
| **我可以使用其他語言嗎？** | 可以。設定 `ocrEngine.Language = OcrLanguage.Spanish`（或任何支援的列舉）並將相同語言傳遞給 `SpellChecker`。 |
| **如果我的圖像非常大怎麼辦？** | 在送入 OCR 前先縮小圖像；`Image` 提供 `GetThumbnailImage` 可快速調整大小。 |
| **需要網路連線嗎？** | 只在首次缺少語言包時需要下載；之後資源會緩存於本機。 |
| **如何處理多頁 PDF？** | 將每一頁轉為圖像（例如使用 `PdfRenderer`），然後對每頁執行相同的流程。 |
| **拼寫檢查器是否具備語言感知？** | 當然。它使用與 OCR 引擎相同的語言模型，確保前後一致。 |

## 後續步驟與相關主題

- **批次處理：** 使用 `foreach` 迴圈包住程式碼，以處理整個圖像資料夾。
- **手寫文字：** 改用 `OcrLanguage.EnglishHandwritten` 以獲得手寫筆記的更佳結果。
- **平行處理：** 使用 `Parallel.ForEach` 在多核心機器上加速大量工作負載。
- **匯出為 JSON/CSV：** 將 `finalText` 連同中繼資料（檔名、信心分數）序列化，以供後續分析。

如果你想了解如何將提取的字串轉換為可搜尋的 PDF，請參考我們的 **「Create searchable PDF from image in C#」** 教學。它直接基於我們剛剛介紹的 OCR 流程。

## 結論

我們剛剛示範了一種實用的方式，使用 Aspose OCR 在 C# 中 **extract text from image**，同時說明了如何 **load image for OCR**、**improve OCR accuracy**，以及如何利用內建的拼寫檢查器與簡易的正規表達式清理 **fix OCR errors**。完整範例即開即用，只需一個 NuGet 套件，且可擴充以符合幾乎所有文件數位化的情境。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}