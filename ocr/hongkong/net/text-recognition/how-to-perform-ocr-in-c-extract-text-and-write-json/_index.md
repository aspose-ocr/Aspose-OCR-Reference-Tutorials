---
category: general
date: 2026-02-09
description: 學習如何在 C# 中執行 OCR，從圖像提取文字、辨識 PNG 文字，並快速寫入 JSON 檔案。
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: zh-hant
og_description: 如何在 C# 中執行 OCR？請跟隨此一步一步的指南，從圖像中提取文字、識別 PNG 中的文字，並高效地在 C# 中寫入 JSON
  檔案。
og_title: 如何在 C# 中執行 OCR — 擷取文字並寫入 JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: 如何在 C# 中執行 OCR – 擷取文字並寫入 JSON
url: /zh-hant/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 完整指南

在需要 **extract text from image** 檔案時，如何在 C# 中執行 OCR 是一個常見的障礙。在本指南中，我們將逐步說明如何從 PNG 識別文字、將詳細結果匯出為 JSON 字串，最後以 **write JSON file C#** 方式寫入。是否曾盯著掃描的表單，想知道如何將那些雜亂的筆劃轉換成可搜尋的文字？你並不孤單；許多開發者在早期都會碰到這個問題。

我們將使用 Aspose.OCR 函式庫，因為它可直接提供每個符號的信心分數，且能與 .NET 6+ 專案良好相容。完成本教學後，你將擁有一個可直接執行的主控台應用程式，能載入 PNG、提取每個字元，並儲存整齊的 JSON 檔案，供資料庫或 AI 模型使用。沒有神祕的「請參考文件」捷徑——只有完整的自給自足解決方案。

## 需要的環境

- **.NET 6 SDK**（或更新版本）– 撰寫時的最新 LTS 版。
- **Aspose.OCR for .NET** NuGet 套件 – `Install-Package Aspose.OCR`。
- 你想要掃描的 PNG 圖片（例如 `form.png`）。
- 任意 IDE 或編輯器 – Visual Studio、VS Code、Rider – 只要你習慣即可。

就這樣。如果你已備妥上述項目，就可以開始了。

![如何執行 OCR 示例](ocr-example.png "如何在 C# 中執行 OCR")

*圖片說明：展示 C# 主控台應用程式處理 PNG 的 OCR 示意圖。*

## 步驟 1：設定專案並加入相依性

首先，建立一個新的主控台專案，並加入 Aspose OCR 函式庫。

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **Pro tip:** 若想明確鎖定目標框架，請使用 `--framework net6.0` 參數。

此步驟的重要性在於：NuGet 套件內含我們將依賴的 `OcrEngine`、`ImageStream` 與 `JsonExporter` 類別。若未加入，編譯器根本不會知道「OCR」是什麼。

## 步驟 2：撰寫核心 OCR 邏輯

開啟 `Program.cs`（或建立新檔案），將其內容替換為下列程式碼。每個區段都有註解，讓你了解其用途。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### 為何每個部分都很重要

- **OcrEngine**：可視為整個作業的核心大腦。它會載入語言模型並建立推論管線。
- **ImageStream.FromFile**：支援任何 PNG、JPEG、BMP 等格式，抽象化檔案 I/O 的細節。
- **RecognitionResult**：保存原始文字與信心分數。這裡提供你下游驗證所需的細部資料。
- **JsonExporter**：將豐富的 `RecognitionResult` 轉換為整潔的 JSON 負載，十分適合 API 使用。
- **File.WriteAllText**：簡單的 .NET 方法，可 **write JSON file C#**，不需額外相依性。

## 步驟 3：執行應用程式並驗證輸出

編譯並執行程式：

```bash
dotnet run
```

你應該會看到類似以下的主控台訊息：

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

開啟 `form.json` – 你會看到類似以下內容：

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

**extract text from image** 步驟已成功完成，現在你擁有每個字元的機器可讀 JSON 表示。

## 步驟 4：處理常見例外情況

### 檔案遺失或損毀

若 PNG 路徑錯誤，`ImageStream.FromFile` 會拋出 `FileNotFoundException`。請將載入程式碼包在 try‑catch 區塊中：

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### 低信心分數

有時候對於噪點較多的掃描，OCR 會回傳低信心分數。你可以在匯出前過濾符號：

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

這樣可確保 JSON 只包含相對可靠的字元——在將資料餵入下游驗證流程時相當有用。

### 大檔案與記憶體

處理多 MB 的 PNG 可能會導致記憶體使用激增。可考慮分塊串流圖像，或使用 `OcrEngine.RecognizeAsync`（在較新 Aspose 版本中提供）以保持 UI 響應。

## 步驟 5：擴充解決方案（可選）

- **Batch processing**：遍歷 PNG 目錄，為每個檔案產生對應的 JSON。
- **Database storage**：將 JSON 插入 SQL 的 `NVARCHAR(MAX)` 欄位，以供日後分析。
- **Language selection**：若需要非英語支援，請設定 `ocrEngine.Language = OcrLanguage.Spanish;`。

所有這些擴充皆遵循我們建立的 **how to perform OCR** 流程——初始化、識別、匯出與持久化。

## 常見問題

**Q: 這能支援 JPG 或 TIFF 嗎？**  
A: 絕對可以。`ImageStream.FromFile` 會自動偵測格式，因此你可以將 PNG 替換為任何支援的點陣圖檔案。

**Q: 如果我要從 PDF 提取文字該怎麼辦？**  
A: 先將每一頁 PDF 轉換為影像（例如使用 `Aspose.PDF`），再將 PNG 輸入本教學所述的 OCR 流程。

**Q: 能否將 OCR 結果輸出為 XML 而非 JSON？**  
A: 可以。Aspose.OCR 也提供 `XmlExporter`。將 `JsonExporter` 換成 `XmlExporter`，並調整檔案副檔名即可。

## 結論

我們已從頭到尾說明了在 C# 中 **how to perform OCR** 的完整流程，示範了如何 **extract text from image**、**recognize text from PNG**，以及 **write JSON file C#**，全程順暢。完整且可執行的範例位於上述程式碼片段，你現在也了解每個步驟背後的原因——初始化引擎、處理例外情況、以及持久化結果。

接下來，你可以探索批次 OCR 流程、將 JSON 輸出整合至 Azure Cognitive Search，或嘗試自訂語言模型。掌握了 C# OCR 的基礎後，未來的可能性無限。

如果在實作過程中遇到任何問題或有進一步的擴充想法，歡迎在下方留言。祝開發愉快，盡情將那些像素化的掃描檔轉換成乾淨、可搜尋的資料！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}