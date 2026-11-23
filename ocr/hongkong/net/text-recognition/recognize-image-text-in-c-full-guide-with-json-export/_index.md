---
category: general
date: 2026-04-06
description: 使用 Aspose OCR 在 C# 中辨識圖片文字。學習如何提取文字、載入圖片檔案（C#），以及在 C# 中寫入 JSON，並提供簡單的逐步範例。
draft: false
keywords:
- recognize image text
- how to extract text
- write json in c#
- load image file c#
language: zh-hant
og_description: 使用 Aspose OCR 於 C# 識別圖像文字。本指南示範如何快速提取文字、載入圖像檔案以及在 C# 中寫入 JSON。
og_title: 在 C# 中辨識圖像文字 – 完整逐步指南
tags:
- OCR
- C#
- Aspose
title: 在 C# 中辨識圖像文字 – 完整指南與 JSON 匯出
url: /zh-hant/net/text-recognition/recognize-image-text-in-c-full-guide-with-json-export/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中辨識影像文字 – 完整步驟指南

有沒有曾經需要 **辨識影像文字**，例如從掃描的收據中擷取文字，但又不確定該選哪個函式庫？你並不是唯一的疑惑者。於許多實務應用——如費用追蹤、發票處理、甚至無障礙工具——從圖片中抽取文字往往是第一道關卡。

在本教學中，我們將手把手示範如何使用 Aspose OCR 函式庫 **辨識影像文字**、**如何擷取文字**、正確 **載入影像檔案 C#**，最後 **在 C# 中寫入 JSON**，讓你能儲存或傳輸結果。完成後，你將擁有一個可直接執行的 Console 應用程式，能把任意 PNG 轉換成整齊的 JSON 資料。

---

## 你需要的環境

- **.NET 6+**（程式碼同樣支援 .NET Framework 4.8，但 .NET 6 為最佳選擇）。
- **Aspose.OCR for .NET** NuGet 套件。使用 `dotnet add package Aspose.OCR` 安裝。
- 一張範例影像（`input.png`），放在程式可以讀取的位置。  
- Visual Studio 2022 或任何你慣用的編輯器——不需要特殊 IDE 技巧。

> 小技巧：將影像檔放在專案內的 `Resources` 資料夾，能保持路徑整潔，避免「找不到檔案」的麻煩。

---

## 第一步：辨識影像文字 – 載入影像檔案

在 OCR 引擎發揮魔法之前，必須先 **載入影像檔案 C#**。`Image.FromFile` 會在路徑錯誤或檔案格式不支援時拋出例外，我們需要做好防護。

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // Verify the image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // Load the image – this is the “load image file c#” step
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // Continue to OCR...
        }
    }
}
```

*為什麼這很重要*：在 `using` 區塊內載入影像，可確保非受控的 GDI+ 資源即時釋放，避免長時間服務產生記憶體泄漏。

---

## 第二步：如何使用 Aspose OCR 擷取文字

現在 bitmap 已經在記憶體中，我們把它交給 **辨識影像文字** 引擎。Aspose 的 `OcrEngine` 用法相當簡單：建立實例、呼叫 `Recognize`，即可取得包含原始文字、信心分數，甚至邊界框的 `OcrResult` 物件。

```csharp
// Inside the using block from Step 1
var ocrEngine = new OcrEngine();

// Perform OCR – this is the core “how to extract text” operation
OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

// Quick sanity check
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("⚠️ No text detected. Try a clearer image.");
    return;
}
Console.WriteLine("✅ OCR succeeded. Extracted text:");
Console.WriteLine(ocrResult.Text);
```

*說明*：`Recognize` 會執行內建的神經網路。對高對比、300 DPI 的影像效果最佳。若提供模糊的照片，信心分數會下降——在正式環境建議先做前處理（去斜、二值化）。

---

## 第三步：在 C# 中寫入 JSON – 匯出 OCR 結果

大多數 API 都接受 JSON 格式，我們將使用 Aspose 的 `JsonExport` **在 C# 中寫入 JSON**。此函式會序列化整個 `OcrResult`，保留行資訊與信心值。

```csharp
// Still inside the same using block
string jsonResult = JsonExport.ToJson(ocrResult);

// Persist the JSON to disk
File.WriteAllText(outputPath, jsonResult);
Console.WriteLine($"💾 JSON written to {outputPath}");
```

### 預期的 JSON 輸出

```json
{
  "Text": "Total: $12.34\r\nDate: 2026-04-01\r\n...",
  "Words": [
    { "Text": "Total", "Confidence": 0.98, "Rectangle": { "X": 10, "Y": 15, "Width": 50, "Height": 12 } },
    { "Text": "$12.34", "Confidence": 0.96, "Rectangle": { "X": 70, "Y": 15, "Width": 45, "Height": 12 } }
    // … more words …
  ]
}
```

*為什麼使用 JSON*？它語言無關、易於反序列化，且能保留你可能在後續驗證時需要的詳細 OCR 中繼資料。

---

## 第四步：完整、可執行的程式

把前面的片段組合起來，以下就是完整的 Console 應用程式。直接複製貼上、還原 NuGet 套件，然後按 **F5**。

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Configuration – adjust these paths as needed
        // -------------------------------------------------
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // -------------------------------------------------
        // Validate input file
        // -------------------------------------------------
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // -------------------------------------------------
        // Load image (load image file c#)
        // -------------------------------------------------
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // -------------------------------------------------
            // Initialize OCR engine and recognize text
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("⚠️ No text detected. Try a clearer image.");
                return;
            }

            Console.WriteLine("✅ OCR succeeded. Sample output:");
            Console.WriteLine(ocrResult.Text.Substring(0, Math.Min(100, ocrResult.Text.Length)) + "...");

            // -------------------------------------------------
            // Convert result to JSON (write json in c#)
            // -------------------------------------------------
            string jsonResult = JsonExport.ToJson(ocrResult);
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"💾 JSON written to {outputPath}");
        }
    }
}
```

執行程式後開啟 `Resources/output.json`——你應該會看到一個結構良好的 JSON，完整呈現引擎辨識出的內容。

---

## 處理常見的例外情況

| 情境 | 處理方式 | 為什麼 |
|-----------|------------|-----|
| **影像為 null 或已損毀** | 在 `Image.FromFile` 外層加 try/catch，並記錄例外資訊。 | 防止程式當機，提供清晰的錯誤訊息。 |
| **信心分數偏低** | 檢查 `ocrResult.Words[i].Confidence`。若低於 0.75，考慮前處理（提升 DPI、銳化）。 | 提升下游流程（如金額抽取）的可靠度。 |
| **大型檔案（>10 MB）** | 在 OCR 前先縮小影像 (`receiptImage = new Bitmap(receiptImage, new Size(width/2, height/2))`)。 | 降低記憶體壓力，加快辨識速度。 |
| **多語言文件** | 設定 `ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;` | 讓引擎同時偵測多種語言的字元。 |

---

## 加分項：視覺化 OCR 結果（可選）

如果想要在影像上看到每個字的位置，可以畫出邊界框：

```csharp
using (Graphics g = Graphics.FromImage(receiptImage))
{
    foreach (var word in ocrResult.Words)
    {
        var rect = new Rectangle(word.Rectangle.X, word.Rectangle.Y,
                                 word.Rectangle.Width, word.Rectangle.Height);
        g.DrawRectangle(Pens.Red, rect);
    }
    receiptImage.Save(Path.Combine("Resources", "annotated.png"));
}
```

產生的 `annotated.png` 會在每個辨識出的單字周圍畫上紅色矩形——對除錯非常有幫助。

---

## 結語

我們已完整示範如何在 C# 中 **辨識影像文字**：從載入影像檔案、呼叫 Aspose OCR **擷取文字**，最後 **在 C# 中寫入 JSON**，讓資料能隨處傳遞。完整範例可直接執行，額外的技巧則協助你應對模糊收據、大檔案或多語言掃描。

接下來可以嘗試將 Aspose 換成其他引擎（Tesseract、Microsoft OCR），比較信心分數，或把 JSON 匯入資料庫作為費用報表。你也可以把這個 Console 應用程式擴充成 ASP .NET Core Web API，接受影像上傳並即時回傳 JSON。

有關擴充規模、錯誤處理或與 Azure Functions 整合的問題嗎？歡迎在評論區留言或於 GitHub 私訊我。祝開發順利，OCR 永遠清晰！

---

![OCR JSON 輸出截圖 – 辨識影像文字範例](https://example.com/ocr-example.png "辨識影像文字範例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}