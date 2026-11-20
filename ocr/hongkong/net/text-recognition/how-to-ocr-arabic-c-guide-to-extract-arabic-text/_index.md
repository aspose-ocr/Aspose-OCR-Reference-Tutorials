---
category: general
date: 2026-04-26
description: 如何在 C# 中對阿拉伯文進行 OCR – 學習將圖像轉換為文字，從 PNG 中提取阿拉伯文字，並使用 Aspose OCR 載入圖像進行
  OCR。
draft: false
keywords:
- how to ocr arabic
- extract arabic text
- convert image to text
- extract text from png
- load image for ocr
language: zh-hant
og_description: 如何在 C# 中進行阿拉伯文 OCR – 一個逐步教學，展示如何將圖像轉換為文字、從 PNG 中提取阿拉伯文字，以及載入圖像進行 OCR。
og_title: 如何 OCR 阿拉伯文 – 完整 C# 指南
tags:
- OCR
- C#
- Aspose
title: 如何 OCR 阿拉伯文 – C# 提取阿拉伯文字指南
url: /zh-hant/net/text-recognition/how-to-ocr-arabic-c-guide-to-extract-arabic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何 OCR 阿拉伯文 – 完整 C# 指南

有沒有想過 **如何 OCR 阿拉伯文** 直接從掃描的合約或螢幕截圖中取得文字？你並不是唯一有此疑問的開發者——大家常問：「我真的可以從 PNG 中提取阿拉伯字元而不失去文字方向嗎？」簡短的答案是可以，而本指南將帶你一步步完成整個流程，從載入影像到輸出結果。  

在接下來的幾分鐘內，你將學會如何 **將影像轉換為文字**、如何使用 Aspose OCR **提取阿拉伯文字**，以及為何正確載入影像很重要。內容直截了當，提供一個可直接放入任何 .NET 專案的可運作範例。  

## 需要的環境

* **.NET 6+**（API 在 .NET Framework 上的行為相同，但最新的執行環境可提供最佳效能）。  
* **Aspose.OCR for .NET** – 可從 NuGet 取得（`Install-Package Aspose.OCR`）。  
* 包含阿拉伯字元的影像檔，例如 `arabic_contract.png`。  
* 具備基本的 C# 知識——只要會寫 `Console.WriteLine` 即可。  

就這樣。無需額外的 OCR 引擎、無需外部服務，只要使用這個單一函式庫即可直接支援從右至左的文字。

## 步驟實作說明

以下我們將解決方案拆解成小段落。每個章節都有清晰的標題、簡短的程式碼片段，以及說明 **為何** 此步驟重要。隨意複製貼上程式碼；最後的區塊是一個可直接執行的完整程式。

### ## 如何使用 Aspose OCR 在 C# 中 OCR 阿拉伯文字

首先，你需要建立 OCR 引擎的實例。此物件保存所有設定選項——語言、頁面版面、影像來源，應有盡有。  

```csharp
using Aspose.OCR;

// Create the OCR engine – this is the core object that does the heavy lifting.
OcrEngine ocrEngine = new OcrEngine();
```

*為何重要：* `OcrEngine` 封裝了辨識演算法。若沒有它，就無法設定語言或提供影像。

### ## 轉換影像為文字 – 正確載入 PNG

引擎建立後，將其指向要處理的影像。Aspose 提供 `ImageStream` 輔助類別，可抽象化檔案系統的細節。  

```csharp
// Load the PNG that contains Arabic text.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/arabic_contract.png");
```

> **專業提示：** 若影像位於串流中（例如來自 Web 請求），請使用 `ImageStream.FromStream(yourStream)` 取代 `FromFile`。這樣可避免產生暫存檔並提升速度。

*為何重要：* **載入 OCR 用的影像** 步驟確保引擎使用你提供的精確位元組。若像素格式不匹配，可能導致字元遺失。

### ## 設定語言 – 精確提取阿拉伯文字

阿拉伯文不只是另一種字母表；它是右至左且具語境形狀變化的文字。必須告訴引擎預期的語言。  

```csharp
// Tell Aspose we are dealing with Arabic.
ocrEngine.Language = Language.Arabic;
```

*為何重要：* 若語言保持預設（通常為英文），引擎會嘗試將阿拉伯字形映射到拉丁字元，導致輸出雜亂。設定 `Language.Arabic` 會啟用正確的字元集與形狀規則。

### ## 啟用右至左排序（可選但建議明確設定）

Aspose OCR 會自動為阿拉伯文切換右至左，但明確設定可讓程式碼自說明。  

```csharp
// Explicitly set text direction—useful when you later switch languages.
ocrEngine.Options.TextDirection = TextDirection.RightToLeft;
```

*為何重要：* 當你之後加入多語言支援（例如同頁同時包含英文與阿拉伯文）時，明確的旗標可防止意外的左至右排序。

### ## 執行 OCR – 從 PNG 提取文字

所有準備工作已完成，現在正式辨識字元。  

```csharp
// Run the recognition engine.
RecognitionResult recognitionResult = ocrEngine.Recognize();
```

*為何重要：* `Recognize()` 會回傳 `RecognitionResult` 物件，內含原始 Unicode 字串、信賴分數，甚至在需要時的邊界框資訊。

### ## 顯示結果 – 驗證提取

最後，將提取的阿拉伯字串印出至主控台。你也可以寫入檔案或資料庫。  

```csharp
// Output the Arabic text.
Console.WriteLine("Extracted Arabic text:");
Console.WriteLine(recognitionResult.Text);
```

**預期輸出**（假設 PNG 包含「عقد إيجار」這句話）：  

```
Extracted Arabic text:
عقد إيجار
```

如果看到問號或空字串，請再次確認影像是否清晰，以及語言是否正確設定。

### ## 完整可執行範例

將所有部份組合起來，以下是一個最小化的主控台應用程式，你可以編譯並執行：  

```csharp
using System;
using Aspose.OCR;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine.
            OcrEngine ocrEngine = new OcrEngine();

            // 2️⃣ Set the language to Arabic – crucial for correct shaping.
            ocrEngine.Language = Language.Arabic;

            // 3️⃣ Load the image you want to process.
            // Replace the path with the actual location of your PNG.
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/arabic_contract.png");

            // 4️⃣ (Optional) Explicitly enforce right‑to‑left ordering.
            ocrEngine.Options.TextDirection = TextDirection.RightToLeft;

            // 5️⃣ Run the recognition.
            RecognitionResult result = ocrEngine.Recognize();

            // 6️⃣ Output the result.
            Console.WriteLine("Extracted Arabic text:");
            Console.WriteLine(result.Text);
        }
    }
}
```

將此檔案儲存為 `Program.cs`，執行 `dotnet run`，即可在主控台看到阿拉伯文字。

## 常見問題與邊緣情況

**如果影像解析度低呢？**  
OCR 的準確度在低於 150 dpi 時會急劇下降。可使用影像增強函式庫（例如 ImageSharp）在送入 Aspose 前進行放大或銳化。

**能否在一次執行中處理多頁影像？**  
可以。遍歷檔案路徑集合，於呼叫 `Recognize()` 前將每個檔案指派給 `ocrEngine.Image`。若每張影像的選項不同，請記得重設。

**需要單獨處理變音符號嗎？**  
不需要。Aspose 的阿拉伯語語言套件已完整支援變音符號。唯一可能需要額外處理的情況是你要將文字正規化以供搜尋索引使用。

**如何從 JPEG 而非 PNG 提取文字？**  
程式碼完全相同——只要更改檔案副檔名即可。Aspose OCR 支援大多數點陣圖格式（`.png`、`.jpg`、`.bmp`、`.tiff`）。

**是否能取得每個單字的信賴分數？**  
`RecognitionResult` 會公開 `Words` 集合，每個項目都有 `Confidence` 屬性。你可以遍歷它以過濾低信賴度的結果。

## 生產環境阿拉伯 OCR 提示

* **預先處理影像：** 二值化、去除傾斜、去除背景噪點。即使是一次簡單的 `ImageProcessor` 呼叫，也能提升 10‑15 % 的準確度。  
* **快取引擎：** 建立 `OcrEngine` 的成本相對低，但在多個請求間重複使用同一實例可減少記憶體波動。  
* **處理右至左 UI：** 在 WinForms 或 Web 應用程式中顯示提取文字時，將控制項的 `RightToLeft` 屬性設為 `Yes`，即可正確呈現阿拉伯文。  
* **記錄原始 Unicode：** 儲存從 `recognitionResult.Text` 取得的完整字串；除非明確需要，否則不要自動進行音譯。

## 結論

現在你已了解如何在 C# 中使用 Aspose OCR **OCR 阿拉伯文**，如何 **將影像轉換為文字**，以及 **載入 OCR 用影像** 與 **從 PNG 檔提取阿拉伯文字** 的完整步驟。上述完整範例可直接放入任何 .NET 解決方案，額外的提示則有助於你從快速示範升級到穩健的生產流程。

準備好接受下一個挑戰了嗎？試著將此與 **從 PNG 提取文字** 結合，處理多語言文件，或將輸出送入翻譯 API，即時取得阿拉伯合約的英文版本。沒有極限——盡情實驗、迭代，讓 OCR 承擔繁重的工作。

如果遇到問題或有聰明的最佳化技巧想分享，請在下方留言。祝開發愉快！  

![如何 OCR 阿拉伯文範例](arabic-ocr-example.png){alt="如何 OCR 阿拉伯文範例"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}