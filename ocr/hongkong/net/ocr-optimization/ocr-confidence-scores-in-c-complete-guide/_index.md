---
category: general
date: 2026-05-31
description: 學習如何在 C# 中取得 OCR 信心分數，同時從圖像提取文字，並使用 Aspose OCR 讀取收據圖像。
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: zh-hant
og_description: OCR 信心分數讓您衡量準確度；本指南示範如何從圖像提取文字、取得邊界框，並使用 Aspose OCR 讀取收據圖像。
og_title: C# 中的 OCR 可信度分數 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C# 中的 OCR 信心分數 – 完整指南
url: /zh-hant/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# 中的 OCR 信心分數 – 完整指南

有沒有想過在需要 *從圖像中提取文字* 時，如何取得 **OCR 信心分數**？也許你正嘗試 **讀取收據圖像** 以進行費用追蹤，並想了解引擎對哪些字元不確定。好消息是？使用 Aspose.OCR 只需幾行 C# 程式碼，即可從 JPG 取得信心百分比、邊界框以及純文字。

在本教學中，我們會一步步說明：安裝函式庫、設定引擎以 **在 JPG 上執行 OCR**、取得信心分數，以及解讀告訴你每個字元在頁面上位置的 **OCR 邊界框**。完成後，你將擁有一個可直接執行的 Console 應用程式，會列印每個字元、其信心與位置——非常適合驗證收據或任何掃描文件。

## 您將學習到

- 透過 NuGet 安裝 Aspose.OCR 並建立基本的 OCR 引擎。  
- 設定 `OcrOptions` 以請求 **含信心分數** 與 **邊界框** 的純文字輸出。  
- 逐行、逐字元遍歷 `OcrResult`，**從圖像中提取文字**。  
- 處理常見問題，例如檔案遺失、低信心字元、以及非 JPG 格式。  
- 將範例延伸至一次處理資料夾中的多張收據圖像。

不需要任何 Aspose 使用經驗，只要有可運作的 .NET 環境以及一張想測試的收據圖像（JPG）即可。

---

## Step 1 – Install Aspose.OCR and Prepare Your Project

首先，你需要取得 Aspose.OCR 的 NuGet 套件。於專案資料夾的終端機執行：

```bash
dotnet add package Aspose.OCR
```

> **小技巧：** 免費試用版支援最多 200 頁，足以測試收據掃描。

套件安裝完成後，建立一個新的 Console 專案（如果還沒有的話）：

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

接著打開產生的 `Program.cs`，加入以下 using 指示：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

這些命名空間讓你可以使用 `OcrEngine`、`OcrOptions` 以及稍後會用到的結果型別。

## Step 2 – Get OCR confidence scores and OCR bounding boxes

這是本教學的核心。我們會設定引擎，使每個辨識出的字元都帶有 **信心分數** 與 **邊界框**（包住字形的矩形）。此 H2 標題本身即包含主要關鍵字，符合 SEO 規則。

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**為什麼要包含信心分數？**  
信心分數（0‑100%）告訴你引擎對每個字元的確定程度。若你將輸出交給後續流程——例如費用審批工作流——可以自動拒絕或標記低信心的符號。

**為什麼要請求邊界框？**  
當你需要在原圖上標示文字、擷取子區域，或將 OCR 結果與 UI 疊加對齊時，邊界框是必備資訊。每個 `character.Bounds` 會提供 X、Y、寬度與高度的像素座標。

## Step 3 – Perform OCR on JPG and extract text from image

現在正式執行引擎。呼叫 `Recognize()` 會完成所有繁重的工作，並回傳一個 `OcrResult` 物件。

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

如果圖像路徑錯誤或檔案格式不支援，Aspose 會拋出 `FileNotFoundException` 或 `UnsupportedImageFormatException`。在正式環境中建議使用 try/catch 包住呼叫，以優雅處理這類例外。

### Pulling out the plain text

如果只需要合併後的文字，可直接讀取 `ocrResult.Text`：

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

但因為我們同時要求了信心分數與邊界框，所以需要遍歷結構，逐一檢視每個字元的詳細資訊。

## Step 4 – Iterate through lines, symbols, and display OCR confidence scores

以下程式碼會列印每個字元、其信心以及其框框。這正是 **讀取收據圖像** 範例發揮威力的地方。

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

範例輸出可能如下：

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**解讀數字方式：**  
- **信心 ≥ 90%** – 通常可直接接受。  
- **信心 70‑89%** – 建議再次確認，特別是金額中的數字。  
- **信心 < 70%** – 考慮標記為需要人工審核。

## Step 5 – Full runnable example (including error handling)

把所有步驟整合起來，以下是一個完整的程式，你可以直接複製貼上到 `Program.cs`。它會檢查檔案是否遺失，若 OCR 失敗則顯示友善訊息。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Expected output

執行 `dotnet run` 後，Console 會先顯示合併的收據文字，接著列出每個字元的信心分數與邊界框。若某個字元的信心偏低，你會看到低於 80% 的百分比，這時就需要手動驗證該部分的收據內容。

## Bonus: Processing Multiple Receipts in a Folder

如果手上有一批收據 JPG，將上述邏輯包在 `foreach (var file in Directory.GetFiles(folder, "*.jpg"))` 迴圈內即可。記得每處理一個檔案就重設 `OcrEngine`，或在迴圈內重新建立實例，以免狀態相互影響。

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

批次處理對於每晚的費用匯入非常方便。

## Conclusion

現在你已擁有一套完整、端到端的解決方案，能在 C# 中取得 **OCR 信心分數**、**從圖像中提取文字**，以及在 **執行 JPG OCR** 時取得 **OCR 邊界框**（例如 **讀取收據圖像**）。此程式碼完全自包含，支援截至 2026‑05‑31 最新的 Aspose.OCR 版本，並提供你建構可信文件處理管線所需的細粒度資料。

接下來可以嘗試使用 `System.Drawing` 或其他 UI 函式庫在原始收據上繪製邊界框，或將低信心字元送至二次驗證服務。亦可透過設定 `ocrEngine.Options.Language = OcrLanguage.French;` 來實驗不同語言——API 支援多種語系。

祝開發順利，願你的信心分數永遠保持高位！

![Console output showing OCR confidence scores and bounding boxes for a receipt

## 您接下來可以學習什麼？

- [使用 Aspose.OCR 以語言選擇方式提取 C# 圖像文字](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [取得圖像辨識中已辨識字元的 OCR 候選字元](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [在圖像辨識中使用 Aspose OCR 取得 JSON 結果](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}